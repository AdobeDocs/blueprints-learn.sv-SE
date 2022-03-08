---
title: Känd kundaktivering
description: Online/offline Audience Activation.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
source-git-commit: 7611084c357e721f954ff980ef88b965609dd5ed
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---

# Kundaktiveringsutkast

Använd offlineattribut och händelser som offlineorder, transaktioner, CRM eller lojalitetsdata, tillsammans med onlinebeteende för målinriktning och personalisering.

Utökade identifierare med inbyggda styrningskontroller ger fler möjligheter att kommunicera med kända kunder. Aktivera målgrupper för kända profilbaserade destinationer som e-postleverantörer, sociala nätverk och reklamdestinationer.

Ytterligare information finns i [Målgrupps- och profilaktivering med Experience Cloud Applications Blueprint](platform-and-applications.md) som är specifikt för integreringar mellan Experience Platform och Experience Cloud.

## Användningsexempel

* Målgruppsanpassning för kända målgrupper på sociala medier och reklamdestinationer.
* Anpassning online med online- och offlineattribut.
* Aktivera målgrupper för kända kanaler, som e-post och SMS.

## Program

* Adobe Experience Platform
* [!UICONTROL Real-time Customer Data Platform]

## Arkitektur

### Aktivering med online- och offlinedata med destinationer

<img src="assets/online_offline_activation.svg" alt="Referensarkitektur för utkast online/offline i Audience Activation" style="width:80%; border:1px solid #4a4a4a" />
<br>

## Guardrails

[Se skyddsutkastet på sidan Översikt över målgrupps- och profilaktivering](overview.md).

## Implementeringssteg

1. [Skapa scheman](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) för data som ska importeras.
1. [Skapa datauppsättningar](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) för data som ska importeras.
1. [Konfigurera rätt identiteter och identitetsnamnutrymmen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html) på schemat för att säkerställa att inkapslade data kan sammanfogas till en enhetlig profil.
1. [Aktivera scheman och datauppsättningar för profilen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Ingrediera data](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) till Experience Platform.
1. [Tillhandahållande [!UICONTROL Real-time Customer Data Platform] segmentdelning](https://www.adobe.com/go/audiences) mellan Experience Platform och Audience Manager för målgrupper som definieras i Experience Platform som ska delas med Audience Manager.
1. [Skapa segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) i Experience Platform. Systemet avgör automatiskt om segmentet utvärderas som batch eller direktuppspelning.
1. [Konfigurera mål](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html) för delning av profilattribut och målgruppsmedlemskap till önskade mål.

## Överväganden gällande implementering

* När du delar profildata till mål måste du inkludera det specifika identitetsvärde som används av målet i målnyttolasten. Alla identiteter som krävs för ett målmål måste hämtas till Platform och konfigureras som en identitet för [!UICONTROL Kundprofil i realtid].

### Målgruppsdelning från Real-time Customer Data Platform till Audience Manager

* Målgruppsmedlemskap från RT-CDP delas med Audience Manager på ett strömmande sätt så snart segmentutvärderingen är klar och skriven i kundprofilen i realtid, oavsett om segmentutvärderingen gjordes i batch eller strömning. Om den kvalificerade profilen innehåller regional routningsinformation för relaterade profilenheter är målgruppsmedlemskapet från RTCDP kvalificerat för direktuppspelning på associerad Audience Manager Edge. Om den regionala routningsinformationen har använts på en profil med en tidsstämpel under de senaste 14 dagarna utvärderas den på Audience Manager Edge i direktuppspelning. Om profilerna från RTCDP inte innehåller någon regional routningsinformation eller om den regionala routningsinformationen är mer än 14 dagar gammal, skickas profilmedlemskapen till Audience Manager navet för batchbaserad utvärdering och aktivering. Profiler som är berättigade till Edge-aktivering aktiveras inom några minuter efter att segment kvalificerats från RTCDP, profiler som inte är kvalificerade för Edge-aktivering kvalificeras i Audience Manager nav och kan ha en 12-24-timmars tidsram för bearbetning.

* Regional routningsinformation som Edge Audience Manager-profilen lagras på kan samlas in till Experience Platform från Audience Manager, Visitor ID-tjänsten, Analytics, Launch eller direkt från Web SDK som en separat profilpostklass med hjälp av XDM-fältgruppen&quot;data capture region information&quot;.

* För aktiveringsscenarier där målgrupper delas från Experience Platform till Audience Manager delas följande identiteter automatiskt: IDFA, GAID, AdCloud, Google, ECID, EMAIL_LC_SHA256. Anpassade namnutrymmen delas för närvarande inte.

Målgrupper från Experience Platform kan delas via Audience Manager-destinationer när de nödvändiga destinationsidentiteterna ingår i [!UICONTROL Kundprofil i realtid]eller var i [!UICONTROL Kundprofil i realtid] kan kopplas till de önskade målidentiteter som är länkade i Audience Manager.

## Relaterad dokumentation

* [[!UICONTROL Real-time Customer Data Platform] Produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Riktlinjer för profil och segmentering](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Segmenteringsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Destinationsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)

## Relaterade videor och Tutorials

* [[!UICONTROL Real-time Customer Data Platform] översikt](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [Demo av [!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [Skapa segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
