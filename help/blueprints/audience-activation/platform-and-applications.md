---
title: Målgrupps- och profilaktivering med Experience Cloud-program
description: Hantera profiler och målgrupper i Experience Platform och dela dem med Experience Cloud-program.
solution: Real-Time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services
kt: 7722
exl-id: f36014e8-170d-47e1-b4ec-10c0ea70612d
source-git-commit: 2dab717d638bdbc0a903861ec743a81f2aed986d
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 2%

---

# Målgrupps- och profilaktivering med Experience Cloud-program

Hantera profiler och målgrupper i Experience Platform och dela dem med Experience Cloud-program. Bygg och dela avancerade kundsegment och insikter i Experience Platform och dela dem med Experience Cloud-applikationer.

Aktiveringen med Experience Cloud-program överensstämmer med [Kundaktiveringsplanen](known.md).

## Användningsfall

* Anpassa och rikta er mot olika kundinteraktionskanaler som drivs av Experience Cloud.
* Dela målgrupps- och profildata mellan Experience Platform och Experience Cloud.
* Bygg multimediedata från flerkanalsdata, inklusive onlinebeteendedata och datavetenskapsmodeller, för att berika kundprofilen i realtid i Experience Platform som sedan kan delas med Experience Cloud-applikationer.

## Tillämpningar

* Adobe Experience Platform
* [!UICONTROL Real-time Customer Data Platform]
* Aktivering av Experience Platform
* Experience Cloud-program
   * Adobe Audience Manager
   * Adobe Target
   * Adobe Campaign
   * Journey Optimizer
   * Marketo Engage
   * Adobe Commerce
   * Customer Journey Analytics

## Arkitektur

Se avsnittet [Experience Platform och programarkitektur](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html) för ytterligare arkitekturdiagram relaterade till Experience Platform-integreringar med program från Experience Cloud.

### Målgrupps- och profilaktivering med Experience Cloud

<img src="../experience-platform/assets/aep+apps.svg" alt="Referensarkitektur för målgrupps- och profilaktivering med Experience Cloud-program" style="width:90%; border:1px solid #4a4a4a"  class="modal-image" />
<br>

## Skyddsräcken

Se [skyddsutkast på sidan Översikt över målgrupps- och profilaktivering](overview.md) och sidan [distributionsskyddsutkast](../experience-platform/deployment/guardrails.md).

## Implementeringsöverväganden

* När du delar profildata till mål måste du inkludera det specifika identitetsvärde som används av målet i målnyttolasten. Alla identiteter som är nödvändiga för ett målmål måste hämtas till Platform och konfigureras som en identitet för [!UICONTROL kundprofilen i realtid].

### Målgruppsdelning från Real-time Customer Data Platform till Audience Manager

* Mer information finns i följande dokumentation. [Experience Platform-segmentdelning med Audience Manager och andra Experience Cloud-lösningar](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html).

* Målgruppsmedlemskap från RT-CDP delas med Audience Manager på ett strömmande sätt så snart segmentutvärderingen är klar och skriven i kundprofilen i realtid, oavsett om segmentutvärderingen gjordes i batch eller strömning.
* Om den kvalificerade profilen innehåller regional routningsinformation för relaterade profilenheter är målgruppsmedlemskapet från RTCDP kvalificerat för direktuppspelning på den associerade Audience Manager Edge. Om den regionala routningsinformationen har använts på en profil med en tidsstämpel under de senaste 14 dagarna kommer den att utvärderas på Audience Manager Edge i direktuppspelning. Om profilerna från RTCDP inte innehåller någon regional routningsinformation eller om den regionala routningsinformationen är mer än 14 dagar gammal, skickas målgruppsmedlemskapen från RTCDP till Audience Manager navplatsen för batchbaserad utvärdering och aktivering.
* Med regional routningsinformation är dessa profiler berättigade till Edge-aktivering och aktiveras inom några minuter från det att de kvalificerar sig för RTCDP, och profiler som inte är kvalificerade för Edge-aktivering kan kvalificera sig i Audience Manager navet och kan ha en 12-24 timmars tidsram för bearbetning.
* Regional routningsinformation som Edge-Audience Manager-profilen lagras på kan samlas in till Experience Platform från Audience Manager, Visitor ID-tjänsten, Analytics, Launch eller direkt från Web SDK som en separat profilpostklass med hjälp av XDM-fältgruppen&quot;data capture region information&quot;. Mer information finns i dokumentet Hämta regional information om [Länk](https://experienceleague.adobe.com/docs/id-service/using/reference/regions.html?lang=en).
* För aktiveringsscenarier där målgrupper delas från Experience Platform till Audience Manager delas följande identiteter automatiskt: ECID, IDFA, GAID, hash-kodade e-postadresser (EMAIL_LC_SHA256), AdCloud ID. Anpassade namnutrymmen delas för närvarande inte.
* Målgrupper från Experience Platform kan delas via Audience Manager-mål när de nödvändiga destinationsidentiteterna ingår i [!UICONTROL kundprofilen i realtid] eller där identiteter i [!UICONTROL kundprofilen i realtid] kan relateras till de destinationsidentiteter som är länkade i Audience Manager.

### Målgruppsdelning från Real-time Customer Data Platform till Target

* Se [Kundens Personalization - Mål och RTCDP-utkast](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/web-personalization/known-personalization.html) för mer information om delning av profiler och målgrupper från Real-time Customer Data Platform till Target.

### Målgruppsdelning från Real-time Customer Data Platform till Campaign och Journey Optimizer

* Se [Customer Journeys-utkast](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/b2b-activation/b2bactivation.html?lang=en) för mer information om delning av profiler och målgrupper från Real-time Customer Data Platform till Campaign och Journey Optimizer.

### Målgruppsdelning från Real-time Customer Data Platform till Marketo Engage

* Mer information om att dela profiler och målgrupper från Real-time Customer Data Platform till Marketo Engage finns i [B2B-aktiveringsutkast](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/b2b-activation/b2bactivation.html?lang=en) .

### Målgruppsdelning från Real-time Customer Data Platform till Customer Journey Analytics

* Se [RTCDP-målgrupperna som delas med Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/ingest-aep-segments.html?lang=en) för mer information om hur du delar Real-time Customer Data Platform-målgrupper med Customer Journey Analytics.

## Relaterad dokumentation

* [[!UICONTROL Real-time Customer Data Platform] Produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Riktlinjer för profil och segmentering](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Segmenteringsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Destinationsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)

## Relaterade videor och självstudiekurser

* [[!UICONTROL Real-time Customer Data Platform] - översikt](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [Demo av [!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [Skapa segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
