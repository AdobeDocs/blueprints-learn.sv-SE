---
title: Scenario för webbpersonalisering online/offline
description: Synkronisera webbpersonalisering med e-post och annan känd och anonym kanalpersonalisering.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7194thumb-web-personalization-scenario2.jpg
translation-type: tm+mt
source-git-commit: 9b6c220a515c5abae22b58fe33558d7d2fed375d
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---



# Scenario för webbpersonalisering online/offline

Synkronisera webbpersonalisering med e-post och annan känd och anonym kanalpersonalisering.

## Användningsexempel

* Optimering av landningssidor
* Riktad beteendeprofil och offlineprofil
* Personalisering baserad på tidigare produkt-/innehållsvyer, produkt-/innehållstillhörighet, miljöattribut, målgruppsdata från tredje part och demografiska data utöver offlineinsikter som transaktioner, lojalitet och CRM-data samt modellerade insikter

## Program

* Kunddataplattform i realtid
* Adobe Target
* Adobe Audience Manager (valfritt): Lägger till målgruppsdata från tredje part, samverkansbaserad enhetsgraf, möjlighet att visa upp plattformssegment i Adobe Analytics samt möjlighet att visa upp Adobe Analytics-segment i Platform
* Adobe Analytics (valfritt): Lägger till möjligheten att skapa segment baserat på historiska beteendedata och finindelad segmentering från Adobe Analytics-data

## Arkitektur

<img src="assets/onoff.svg" alt="Referensarkitektur för webb-personalisering online/offline" style="border:1px solid #4a4a4a" />

## Guardrails

* Segment som delas från Experience Platform till Audience Manager delas inom minuter efter segmentimplementering, oavsett om det sker via direktuppspelning eller satsutvärderingsmetod. Det finns en inledande segmentkonfigurationssynkronisering mellan AEP och AAM på cirka 4 timmar för att AEP-segmentmedlemskap ska börja realiseras i AAM profiler. När de väl finns i AAM är AEP-segmentmedlemskapen tillgängliga för samma sidanpassning via Adobe Target.
* Observera att för segmentimplementeringar som sker inom segmentkonfigurationssynkroniseringen på 4 timmar mellan AEP och AAM, kommer dessa segmentimplementeringar att implementeras i AAM på det efterföljande batchsegmentjobbet som&quot;befintliga&quot; segment.
* Gruppsegmentdelning från AEP - en gång per dag eller manuellt initierad via API. När de här segmentmedlemskapen är klara delas de till AAM inom några minuter och är tillgängliga för samma/nästa sidanpassning i Target.
* Direktuppspelningssegmentering genomförs inom ~ p95 5 min. När dessa segmentimplementeringar inträffar delas de till AAM inom några minuter och är tillgängliga för samma/nästa sidanpassning i Target.
* Som standard tillåter segmentdelningstjänsten att högst 75 målgrupper delas för varje Adobe Analytics-rapportserie. Om kunden har en Audience Manager-licens finns det ingen gräns för hur många målgrupper som kan delas mellan Adobe Analytics och Adobe Target eller Audience Manager och Adobe Target.

## Krav för implementering

| Program/tjänst | Nödvändigt bibliotek | Anteckningar |
|---|---|---|
| Adobe Target | Platform Web SDK*, at.js 0.9.1+, eller mbox.js 61+ | at.js är att föredra eftersom mbox.js inte längre utvecklas. |
| Adobe Audience Manager (tillval) | Platform Web SDK* eller dil.js 5.0+ |  |
| Adobe Analytics (tillval) | Platform Web SDK* eller AppMeasurement.js 1.6.4+ | Adobe Analytics tracking måste använda regional datainsamling (RDC). |
| Experience Cloud ID-tjänst | Platform Web SDK* eller VisitorAPI.js 2.0+ | (Rekommenderas) Använd Experience Platform Launch för att distribuera ID-tjänsten för att säkerställa att ID:t anges före eventuella programanrop |
| Experience Platform Mobile SDK (tillval) | 4.11 eller senare för iOS och Android™ |  |
| Experience Platform Web SDK | 1.0, den aktuella Experience Platform SDK-versionen har [olika användningsfall som ännu inte stöds för Experience Cloud-programmen](https://github.com/adobe/alloy/projects/5) |  |


## Implementeringssteg

1. [Implementera Adobe ](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) Targeting för webb- och mobilapplikationer
1. [Implementera Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html)  (valfritt)
1. [Implementera Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)   (valfritt)
1. [Implementera kundprofil för Experience Platform och realtid](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html)
1. Implementera [Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html) eller [Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
   >[!NOTE]
   >
   >Varje program måste använda Experience Cloud-ID och vara en del av samma Experience Cloud-organisation för att ge möjlighet till målgruppsdelning mellan program.
1. [Begär etablering för målgruppsdelning mellan Experience Platform och Adobe Target (delade målgrupper)](https://www.adobe.com/go/audiences)

## Diagram över implementeringsdataflöde

Anpassningsplanen för webb/mobiler kan implementeras med antingen traditionella programspecifika SDK:er (till exempel AppMeasurement.js) eller med hjälp av Platform Web SDK/Mobile SDK och Edge Network.

### SDK och Edge-strategi för plattformar för webb/mobiler

<img src="assets/websdkflow.svg" alt="Referensarkitektur för Platform Web SDK/Mobile SDK och Edge Network Approach" style="border:1px solid #4a4a4a" />

### Programspecifik SDK-metod

<img src="assets/appsdkflow.png" alt="Referensarkitektur för den programspecifika SDK-metoden" style="border:1px solid #4a4a4a" />

## Relaterad dokumentation

* [Experience Platform segmentdelning med Audience Manager och andra Experience Cloud-lösningar](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)
* [Översikt över segmentering i Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html)
* [Strömmande segmentering](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Översikt över Experience Platform Segment Builder](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html)
* [Audience Manager Source Connector](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html)
* [Adobe Analytics segmentdelning via AAM](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)
* [Experience Platform Web SDK-dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Experience Cloud ID-tjänstdokumentation](https://experienceleague.adobe.com/docs/id-service/using/home.html)
* [Experience Platform Launch dokumentation](https://experienceleague.adobe.com/docs/launch/using/home.html)

## Relaterade blogginlägg

* [Design för webbpersonalisering med Adobe Experience Platform kundprofil i realtid](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [Bygg en optimal onlineupplevelse: Förbättra enhetlig profil med frågetjänsten](https://medium.com/adobetech/build-an-optimal-online-experience-enrich-unified-profile-with-query-service-8027c196ab33)
* [Integrera Adobe Experience Platform Decisioning Engine med AEM webbplatser](https://jaeness.medium.com/integrating-adobe-experience-platform-decisioning-engine-with-aem-websites-9c222acd12e2)
* [Adobe Experience Platform identitetstjänst - Så här löser du problemet med kundidentitet](https://medium.com/adobetech/adobe-experience-platforms-identity-service-how-to-solve-the-customer-identity-conundrum-f95e22d16ea9)
* [Hur Adobe Experience Platform Predictive Audiences förbättrar personaliserade upplevelser](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [Adobe Experience Platform Web SDK for Audience Management](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [Implementera Adobe Experience Platform kundprofil i realtid via vårt&quot;Customer Zero&quot;-program](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [Hur Adobe Experience Platform kan hjälpa kunderna att personalisera sina mobilmeddelanden i realtid med Journey Orchestration Service och en mobil meddelandeleverantör](https://medium.com/adobetech/how-adobe-experience-platform-helped-a-client-personalize-their-mobile-messaging-in-real-time-with-7d634aefa098)
* [Segmentering i sekunder: Hur Adobe Experience Platform gjorde kundprofiler i realtid till verklighet](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
* [Bygg en optimal onlineupplevelse: Förbättra enhetlig profil med frågetjänsten](https://medium.com/adobetech/build-an-optimal-online-experience-enrich-unified-profile-with-query-service-8027c196ab33)

