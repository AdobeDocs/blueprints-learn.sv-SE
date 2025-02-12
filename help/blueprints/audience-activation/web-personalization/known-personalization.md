---
title: Personalization - webb/mobil - översikt - Adobe Target & RTCDP
description: Synkronisera webbanpassning med e-post och annan känd och anonym kanalanpassning.
landing-page-description: Synkronisera webbanpassning med e-post och annan känd och anonym kanalanpassning.
short-description: Synkronisera webbanpassning med e-post och annan känd och anonym kanalanpassning.
solution: Real-Time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection, Experience Platform
kt: 7194
thumbnail: thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: 0d65ac8bcc8647683b6361a293d8c941869cd6b5
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 3%

---


# Personalization för webb/mobiler med kunddata

## Användningsfall

* Online-personalisering med kända kunddata
* Optimering av landningssidor
* Personalization som bygger på tidigare produktions-/innehållsvyer, tillhörighet mellan produkt och innehåll, miljöattribut och demografiska data utöver offlinedata som transaktioner, lojalitet och CRM-data samt modellerade insikter
* Dela och inrikta er på målgrupper som definieras i kunddataplattformen i realtid på webbplatser och mobilappar med hjälp av Adobe Target eller Adobe Journey Optimizer Decisioning.

## Tillämpningar

* [!UICONTROL Kunddataplattform i realtid]
* Adobe Target
* Adobe Journey Optimizer Decisioning
* Adobe Audience Manager (valfritt): Lägger till målgruppsdata från tredje part
* Adobe Analytics eller Customer Journey Analytics (valfritt): ger möjlighet att skapa segment som baseras på historiska kund- och beteendedata med detaljerad segmentering

### Referensdokumentation

* [Adobe Target Connection för kunddataplattform i realtid](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html)
* [Adobe Journey Optimizer Decisioning](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/gs-decision)
* [Edge-dataströmskonfiguration](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)
* [Experience Platform segmentdelning med Audience Manager och andra Experience Cloud-lösningar](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)

## Metoder

En metod för känd kundpersonalisering på webben/i mobilen är att integrera kunddataplattformen i realtid med Adobe Target. Nedan följer en detaljerad beskrivning av hur kunddataplattformen i realtid kan integreras för att stärka en känd kundpersonalisering med Adobe Target.

Kundanpassning på webb- och mobilnivå kan också implementeras med Adobe Journey Optimizer Decisioning, som använder Experience Platform kundprofil och segmentering i realtid. Se [Adobe Journey Optimizer-handboken](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/ajo-home) där [Kodbaserade upplevelser](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based-experience/get-started-code-based) eller [Webbkanalsupplevelser](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web) kan användas.

Arkitekturskisser finns också i och i [Journey Optimizer Blueprint](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/journey-optimizer) och [Journey Optimizer Decisioning Blueprint](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-overview) .

## Integreringsmönster

| Integreringsmönster | Funktion | Krav |
|--------------------|------------|---------------|
| **Utvärdering av segment i realtid på Edge som delas från kunddataplattform i realtid till mål** | - Utvärdera målgrupper i realtid för samma eller nästa sidpersonalisering på Edge. <br> - Alla segment som utvärderas i strömning eller gruppvis läge projiceras också för Edge Network för att inkluderas i kantsegmentsutvärderingen och personaliseringen. | - Web/Mobile SDK måste implementeras för Edge Network Server API. <br>- Datastream måste konfigureras i Experience Edge med Target- och Experience Platform-tillägget aktiverat. <br>- Målmålet måste konfigureras i kunddataplattformsmål i realtid. <br> - Integrering med Target kräver samma IMS-organisation som Experience Platform-instansen. |
| **Direktuppspelning och gruppmålgruppsdelning från kunddataplattformen i realtid till Target via Edge** | - Dela direktuppspelnings- och gruppmålgrupper från Customer Data Platform i realtid till Target via Edge Network. <br>- Målgrupper utvärderade i realtid kräver implementeringen av Web SDK och Edge Network. | - API-implementering av SDK för webb/mobiler eller Edge för Target krävs inte för delning av RTCDP-målgrupper och batch-RTCDP-målgrupper till Target, men krävs för att aktivera edge segment-utvärdering i realtid. <br>- Om AT.js används stöds bara profilintegrering mot ECID-identitetsnamnområdet. <br>- För anpassade namnområdessökningar för identiteter på Edge krävs Web SDK/Edge API-distributionen och varje identitet måste anges som en identitet på identitetskartan. <br>- Målmålet måste konfigureras i kunddataplatsens mål i realtid. Endast standardproduktionssandlådan i RTCDP stöds. <br> - Integrering med Target kräver samma IMS-organisation som Experience Platform-instansen. |
| **Direktuppspelning och batchdelning av målgrupper från kunddataplattformen i realtid till målgruppen och Audience Manager via Audience Sharing Service** | - Det här integreringsmönstret kan utnyttjas när ytterligare berikning från data från tredje part och målgrupper i Audience Manager önskas. | - Web/Mobile SDK krävs inte för att dela direktuppspelnings- och gruppmålgrupper med Target, men krävs för att aktivera realtidsutvärdering av edge segment. <br>- Om AT.js används stöds bara profilintegrering mot ECID-identitetsnamnområdet. <br>- För anpassade namnområdessökningar för identiteter på Edge krävs Web SDK/Edge API-distributionen och varje identitet måste anges som en identitet på identitetskartan. <br> - Målgruppsprojektion via målgruppsdelningstjänsten måste etableras. <br> - Integrering med Target kräver samma IMS-organisation som Experience Platform-instansen. <br> - Endast målgrupper från standardproduktionssandlådan har stöd för målgruppsdelningens bastjänst. |

## Realtids-, strömnings- och batchmålgruppsdelning till Adobe Target

Arkitektur

<img src="assets/RTCDP+Target.svg" alt="Referensarkitektur för Personalization-utkast online/offline" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

Sekvensdetalj

<img src="assets/RTCDP+Target_flow.svg" alt="Referensarkitektur för Personalization-utkast online/offline" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

Översikt Arkitektur

<img src="assets/personalization_with_apps.svg" alt="Referensarkitektur för Personalization-utkast online/offline" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## Implementeringsmönster

Kunden Personalization stöds via flera olika implementeringsmetoder.

### Implementeringsmönster 1 - [!DNL Edge Network] med Web/Mobile SDK eller [!DNL Edge Network] API (rekommenderat tillvägagångssätt)

* Använda [!DNL Edge Network] med SDK för webb/mobil. Kantsegmentering i realtid kräver implementeringsmetoden för SDK/Mobile eller Edge.
* [Se Experience Platform Web and Mobile SDK Blueprint](../../experience-platform/deployment/websdk.md) för den SDK-baserade implementeringen.
* För användning i Mobile SDK måste tillägget [Adobe Journey Optimizer - Decisioning](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/) vara installerat.
* [Se  [!DNL Edge Network] Server-API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html) för en API-baserad implementering av Adobe Target med Edge Profile.

### Implementeringsmönster 2 - Programspecifika SDK:er

Använda traditionella programspecifika SDK:er (till exempel AT.js och AppMeasurement.js). Utvärdering av Edge-segment i realtid stöds inte med den här implementeringsmetoden. Däremot stöds direktuppspelning och gruppmålgruppsdelning från Experience Platform nav med den här implementeringsmetoden.

[Läs Adobe Target Connector Documentation](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection)
[Se programspecifika SDK Blueprint](../../experience-platform/deployment/appsdk.md)

## Implementeringsöverväganden

* Alla primära identiteter kan utnyttjas när implementeringsmönster 1 används som beskrivs ovan med [!DNL Edge Network] och Web SDK.
* Personalisering av första inloggningen med kända kunddata som tidigare importerats till RTCDP kräver att personaliseringsbegäran har en primär identitet som matchar det kända kundidentitetsdiagrammet i kunddataplattformen i realtid. Om det primära ID:t är ECID eller en identitet som ännu inte har sytts ihop med den kända kundprofilen, tar det flera minuter för identitetssammanställningen att realiseras på kanten och för kantanpassning att inkludera tidigare inmatade kända kunddata.
* Edge-profiler har för närvarande 14 dagars TTL. Om en användare inte har loggat in eller varit aktiv på 14 dagar på kanten kan profilen på kanten därför ha gått ut, och kanten måste därför hämta profilen från navet för att få en historisk profilvy för att möjliggöra personalisering, som inkluderar tidigare inmatade profilattribut och segment, kommer detta att leda till personalisering med den historiska vyn över profiler som ska visas på efterföljande sidvisningar jämfört med den första inloggningen.

## Relaterad dokumentation

### SDK-dokumentation

* [Experience Platform Web SDK-dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Experience Platform Tags-dokumentation](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv)
* [Experience Cloud ID-tjänstdokumentation](https://experienceleague.adobe.com/docs/id-service/using/home.html)

### Segmenteringsdokumentation

* [Experience Platform segmenteringsöversikt](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html)
* [Segmentering i realtid](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html)
* [Strömmande segmentering](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Adobe Analytics segmentdelning via Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)
* [Konfiguration av sammanslagningsprincip](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=en#create-a-merge-policy)

### Självstudiekurser

* [Nästa steg i personaliseringen med Real-Time CDP och Adobe Target](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=en)
