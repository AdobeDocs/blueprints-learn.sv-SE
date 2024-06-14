---
title: Översikt över anpassning för webb/mobiler - Adobe Target och RTCDP
description: Synkronisera webbanpassning med e-post och annan känd och anonym kanalanpassning.
landing-page-description: Synkronisera webbanpassning med e-post och annan känd och anonym kanalanpassning.
short-description: Synkronisera webbanpassning med e-post och annan känd och anonym kanalanpassning.
solution: Real-Time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection, Experience Platform
kt: 7194
thumbnail: thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: 845655a275cdb6d4a9cd397ec7c3515cbf02d321
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 4%

---


# Webb-/mobilpersonalisering med känd kunddataplan

## Användningsfall

* Online-personalisering med kända kunddata
* Optimering av landningssidor
* Personalisering baserad på tidigare produkt-/innehållsvyer, tillhörighet mellan produkt och innehåll, miljöattribut och demografiska data utöver offlinedata som transaktioner, lojalitet och CRM-data samt modellerade insikter
* Dela och inrikta er på målgrupper som definieras i Real-time Customer Data Platform på webbplatser och mobilappar med Adobe Target.

## Tillämpningar

* [!UICONTROL Real-time Customer Data Platform]
* Adobe Target
* Adobe Audience Manager (valfritt): Lägger till målgruppsdata från tredje part
* Adobe Analytics eller Customer Journey Analytics (valfritt): Lägger till möjligheten att skapa segment baserat på historiska kund- och beteendedata med detaljerad segmentering

### Referensdokumentation

* [Adobe Target Connection för Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html)
* [Konfiguration av Edge DataStream](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)
* [Experience Platform segmentdelning med Audience Manager och andra Experience Cloud-lösningar](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)


## Integreringsmönster

| Integreringsmönster | Funktion | Krav |
|---|---|---|
| Utvärdering av segment i realtid på den kant som delas från Real-time Customer Data Platform till Target | <ul><li>Utvärdera målgrupper i realtid för samma eller nästa sidpersonalisering på Edge.</li><li>Dessutom projiceras alla segment som utvärderas i strömning eller batchmode även till [!DNL Edge Network] som ska ingå i utvärderingen och personaliseringen av edge-segment.</li></ul> | <ul><li>Web/Mobile SDK måste implementeras för [!DNL Edge Network] Server-API</li><li>Datastream måste konfigureras i Experience Edge med tillägget Target och Experience Platform aktiverat</li><li>Måldestinationen måste konfigureras i Real-time Customer Data Platform Destinations.</li><li>Integrering med Target kräver samma IMS-organisation som Experience Platform-instansen.</li></ul> |
| Direktuppspelning och batchvis målgruppsdelning från Real-time Customer Data Platform till Target via Edge-metoden | <ul><li>Dela strömnings- och gruppmålgrupper från Real-time Customer Data Platform till Target via [!DNL Edge Network]. Målgrupper som utvärderas i realtid kräver Web SDK och [!DNL Edge Network] implementering.</li></ul> | <ul><li>Webb-/mobilapplikationer för SDK eller Edge API-implementering av Target krävs inte för delning av RTCDP-målgrupper för direktuppspelning och batch-RTCDP-målgrupper till Target, även om det krävs för att aktivera realtidsutvärdering av edge segment enligt ovan.</li><li>Om AT.js används stöds bara profilintegrering mot ECID-identitetsnamnutrymmet.</li><li>För anpassade namnområdessökningar för identiteter på Edge krävs Web SDK/Edge API-distributionen och varje identitet måste anges som en identitet på identitetskartan.</li><li>Måldestinationen måste konfigureras i Real-time Customer Data Platform Destinations. Endast standardproduktionssandlådan i RTCDP stöds.</li><li>Integrering med Target kräver samma IMS-organisation som Experience Platform-instansen.</li></ul> |
| Direktuppspelning och batchvis målgruppsdelning från Real-time Customer Data Platform till Target och Audience Manager via Audience Sharing Service | <ul><li>Det här integreringsmönstret kan utnyttjas när ytterligare berikning från data från tredje part och målgrupper i Audience Manager önskas.</li></ul> | <ul><li>Web/Mobile SDK krävs inte för delning av strömnings- och gruppmålgrupper till Target, men det krävs för att aktivera realtidsutvärdering av edge segment.</li><li>Om AT.js används stöds bara profilintegrering mot ECID-identitetsnamnutrymmet.</li><li>För anpassade namnområdessökningar för identiteter på Edge krävs Web SDK/Edge API-distributionen och varje identitet måste anges som en identitet på identitetskartan.</li><li>Målgruppsprojektion via målgruppsdelningstjänsten måste tillhandahållas.</li><li>Integrering med Target kräver samma IMS-organisation som Experience Platform-instansen.</li><li>Det är bara målgrupper från standardproduktionssandlådan som har stöd för målgruppsdelning.</li></ul> |

## Realtids-, strömnings- och batchmålgruppsdelning till Adobe Target

Arkitektur

<img src="assets/RTCDP+Target.svg" alt="Referensarkitektur för Online/Offline Web Personalization Blueprint" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

Sekvensdetalj

<img src="assets/RTCDP+Target_flow.svg" alt="Referensarkitektur för Online/Offline Web Personalization Blueprint" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

Översikt Arkitektur

<img src="assets/personalization_with_apps.svg" alt="Referensarkitektur för Online/Offline Web Personalization Blueprint" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## Implementeringsmönster

Känd kundanpassning stöds via flera implementeringsmetoder.

### Implementeringsmönster 1 - [!DNL Edge Network] med Web/Mobile SDK eller [!DNL Edge Network] API (rekommenderat tillvägagångssätt)

* Använda [!DNL Edge Network] med Web/Mobile SDK. Kantsegmentering i realtid kräver implementeringsmetoden Web/Mobile SDK eller Edge API.
* [Se Experience Platform Web and Mobile SDK Blueprint](../../experience-platform/deployment/websdk.md) för SDK-baserad implementering.
* För användning i Mobile SDK på [Adobe Journey Optimizer - Beslutstillägg](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer-decisioning) måste vara installerat i Mobile SDK.
* [Se [!DNL Edge Network] Server-API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html) för en API-baserad implementering av Adobe Target med Edge Profile.

### Implementeringsmönster 2 - Programspecifika SDK:er

Använda traditionella programspecifika SDK:er (till exempel AT.js och AppMeasurement.js). Utvärdering av Edge-segment i realtid stöds inte med den här implementeringsmetoden. Direktuppspelning och gruppmålgruppsdelning från Experience Platform nav stöds dock med den här implementeringsmetoden.

[Se Adobe Target Connector Documentation](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection)
[Se programspecifik SDK-skiss](../../experience-platform/deployment/appsdk.md)

## Implementeringsöverväganden

Identitetskrav

* Alla primära identiteter kan utnyttjas när implementeringsmönster 1 som beskrivs ovan används med [!DNL Edge Network] och Web SDK. Personalisering vid första inloggning kräver att personaliseringsbegäran anger en primär identitet som matchar den primära identiteten för profilen från Real-time Customer Data Platform.

## Relaterad dokumentation

### SDK-dokumentation

* [Experience Platform Web SDK-dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Dokumentation för Experience Platform-taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv)
* [Experience Cloud ID-tjänstdokumentation](https://experienceleague.adobe.com/docs/id-service/using/home.html)

### Segmenteringsdokumentation

* [Översikt över segmentering i Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html)
* [Segmentering i realtid](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html)
* [Strömmande segmentering](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Adobe Analytics segmentdelning via Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)
* [Konfiguration av sammanfogningsprincip](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=en#create-a-merge-policy)

### Självstudiekurser

* [Nästa steg i personaliseringen med Real-Time CDP och Adobe Target](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=en)

### Relaterade blogginlägg

* [Adobe presenterar Same page Förbättrad personalisering med Adobe Target och Real-time Customer Data Platform](https://blog.adobe.com/en/publish/2021/10/05/adobe-announces-same-page-enhanced-personalization-with-adobe-target-real-time-customer-data-platform)
* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Adobe Experience Platform's Identity Service — How to Solve the Customer Identity Conundrum]](https://medium.com/adobetech/adobe-experience-platforms-identity-service-how-to-solve-the-customer-identity-conundrum-f95e22d16ea9)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our "Customer Zero" Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
