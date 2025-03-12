---
title: Kunddataplattform och Adobe Target i realtid
description: Integrera RTCDP-profiler och målgrupper med Adobe Target.
landing-page-description: Integrera RTCDP-profiler och målgrupper med Adobe Target.
short-description: Integrera RTCDP-profiler och målgrupper med Adobe Target.
solution: Real-Time Customer Data Platform, Target, Experience Platform
kt: 7194
thumbnail: thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: b634e14af3ea60e0f4cc9e84a0ef896df293a8c7
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---


# Integrering av kunddataplattform i realtid med Adobe Target

## Användningsfall

* Online-personalisering med kända kunddata
* Optimering av landningssidor
* Personalization som bygger på tidigare produktions-/innehållsvyer, tillhörighet mellan produkt och innehåll, miljöattribut och demografiska data utöver offlinedata som transaktioner, lojalitet och CRM-data samt modellerade insikter
* Dela och inrikta er på målgrupper som definieras i kunddataplattformen i realtid på webbplatser och mobilappar med Adobe Target

## Tillämpningar

* [!UICONTROL Kunddataplattform i realtid]
* Adobe Target

### Referensdokumentation

* [Adobe Target Connection för kunddataplattform i realtid](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html)
* [Edge-dataströmskonfiguration](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)

## Integreringsmönster

| Integreringsmönster | Funktion | Krav |
|--------------------|------------|---------------|
| **Utvärdering av segment i realtid på Edge som delas från kunddataplattform i realtid till mål** | - Utvärdera målgrupper i realtid för samma eller nästa sidpersonalisering på Edge. <br> - Alla segment som utvärderas i strömning eller gruppvis läge projiceras också för Edge Network för att inkluderas i kantsegmentsutvärderingen och personaliseringen. | - Web/Mobile SDK måste implementeras för Edge Network Server API. <br>- Datastream måste konfigureras i Experience Edge med Target- och Experience Platform-tillägget aktiverat. <br>- Målmålet måste konfigureras i kunddataplattformsmål i realtid. <br> - Integrering med Target kräver samma IMS-organisation som Experience Platform-instansen. |
| **Direktuppspelning och gruppmålgruppsdelning från kunddataplattformen i realtid till Target via Edge** | - Dela direktuppspelnings- och gruppmålgrupper från Customer Data Platform i realtid till Target via Edge Network. <br>- Målgrupper utvärderade i realtid kräver implementeringen av Web SDK och Edge Network. | - API-implementering för Web/Mobile SDK eller Edge av Target krävs inte för att dela direktuppspelnings- och batchmålgrupper från RTCDP till Target, men krävs för att aktivera edge segment-utvärdering i realtid. <br>- Om AT.js används stöds bara profilintegrering mot ECID-identitetsnamnområdet. <br>- För anpassade namnområdessökningar för identiteter på Edge krävs Web SDK/Edge API-distributionen och varje identitet måste anges som en identitet på identitetskartan. <br>- Målmålet måste konfigureras i kunddataplatsens mål i realtid. Endast standardproduktionssandlådan i RTCDP stöds. <br> - Integrering med Target kräver samma IMS-organisation som Experience Platform-instansen. |
| **Direktuppspelning och batchdelning av målgrupper från kunddataplattformen i realtid till målgruppen och Audience Manager via Audience Sharing Service** | - Det här integreringsmönstret kan utnyttjas när ytterligare berikning från data från tredje part och målgrupper i Audience Manager önskas. | - Web/Mobile SDK krävs inte för att dela direktuppspelnings- och gruppmålgrupper med Target, men krävs för att aktivera realtidsutvärdering av edge segment. <br>- Om AT.js används stöds bara profilintegrering mot ECID-identitetsnamnområdet. <br>- För anpassade namnområdessökningar för identiteter på Edge krävs Web SDK/Edge API-distributionen och varje identitet måste anges som en identitet på identitetskartan. <br> - Målgruppsprojektion via målgruppsdelningstjänsten måste etableras. <br> - Integrering med Target kräver samma IMS-organisation som Experience Platform-instansen. <br> - Endast målgrupper från standardproduktionssandlådan har stöd för målgruppsdelningens bastjänst. |

## Realtids-, strömnings- och batchmålgruppsdelning till Adobe Target

Arkitektur

![Referensarkitektur för Personalization-utkast online/offline](assets/RTCDP+Target.svg)

Sekvensdetalj

![Referensarkitektur för Personalization-utkast online/offline](assets/RTCDP+Target_flow.svg)

Översikt Arkitektur

![Referensarkitektur för Personalization-utkast online/offline](assets/personalization_with_apps.svg)

## Implementeringsmönster

Kunden Personalization stöds via flera olika implementeringsmetoder.

### Implementeringsmönster 1 - [!DNL Edge Network] med Web/Mobile SDK eller [!DNL Edge Network] API (rekommenderat tillvägagångssätt)

* Använda [!DNL Edge Network] med SDK för webb/mobil. Kantsegmentering i realtid kräver implementeringsmetoden för SDK/Mobile eller Edge.
* [Se Experience Platform Web and Mobile SDK Blueprint](../experience-platform/deployment/websdk.md) för den SDK-baserade implementeringen.
* För användning i Mobile SDK måste tillägget [Adobe Journey Optimizer - Decisioning](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/) vara installerat.
* [Se  [!DNL Edge Network] Server-API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html) för en API-baserad implementering av Adobe Target med Edge Profile.

### Implementeringsmönster 2 - Programspecifika SDK:er

Använda traditionella programspecifika SDK:er (till exempel AT.js och AppMeasurement.js). Utvärdering av Edge-segment i realtid stöds inte med den här implementeringsmetoden. Däremot stöds direktuppspelning och gruppmålgruppsdelning från Experience Platform nav med den här implementeringsmetoden.

[Läs Adobe Target Connector Documentation](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection)
[Se programspecifika SDK Blueprint](../experience-platform/deployment/appsdk.md)

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
