---
title: Web/Mobile Personalization - översikt
description: Synkronisera webbpersonalisering med e-post och annan känd och anonym kanalpersonalisering.
landing-page-description: Synkronisera webbpersonalisering med e-post och annan känd och anonym kanalpersonalisering.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7194thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: 817ec1be3d4754ca3fb4fc9767ca79e516b6ab47
workflow-type: tm+mt
source-wordcount: '1331'
ht-degree: 0%

---


# Mobile/Personalization med kända kunddata

## Användningsexempel

* Online-personalisering med kända kunddata
* Optimering av landningssidor
* Personalization bygger på tidigare produktions-/innehållsvyer, tillhörighet mellan produkt och innehåll, miljöattribut och demografiska data utöver offlinedata som transaktioner, lojalitet och CRM-data samt modellerade insikter
* Dela och inrikta er på målgrupper som definieras i Real-time Customer Data Platform på webbplatser och mobilappar med Adobe Target.

## Program

* [!UICONTROL Real-time Customer Data Platform]
* Adobe Target
* Adobe Audience Manager (valfritt): Lägger till målgruppsdata från tredje part, samverkansbaserad enhetsgraf
* Adobe Analytics (valfritt): Lägger till möjligheten att skapa segment baserat på historiska beteendedata och finindelad segmentering från Adobe Analytics-data

## Använd scenarier

<table class="tg" style="undefined;table-layout: fixed; width: 790px">
<colgroup>
<col style="width: 20px">
<col style="width: 276px">
<col style="width: 229px">
<col style="width: 265px">
</colgroup>
<thead>
  <tr>
    <th class="tg-y6fn">#</th>
    <th class="tg-f7v4">Använd scenarier</th>
    <th class="tg-y6fn">Funktion</th>
    <th class="tg-f7v4">Krav</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0lax">1</td>
<td class="tg-73oq">Utvärdering av segment i realtid på den kant som delas från Real-time Customer Data Platform till Target</td>
    <td class="tg-0lax">- Utvärdera målgrupper i realtid för samma eller nästa sidpersonalisering på Edge.<br>- Dessutom kommer alla segment som utvärderas i strömning eller batchmode också att projiceras till Edge Network för att inkluderas i edge segment-utvärderingen och personaliseringen.</td>
    <td class="tg-73oq">- Implementeringsmönster 1 som beskrivs nedan.<br>- Web/Mobile SDK måste implementeras.<br>- Observera att det Mobile SDK-baserade stödet för segmentering i realtid för närvarande inte är tillgängligt<br>- Datastream måste konfigureras i Experience Edge när tillägget Mål och Experience Platform är aktiverat. DataStream-ID anges i målkonfigurationen.<br>- Målmålet måste konfigureras i Real-time Customer Data Platform Destinations.<br>- Integrering med Target kräver samma IMS-organisation som Experience Platform-instansen.</td> 
  </tr>
  <tr>
    <td class="tg-0lax">2</td>
    <td class="tg-73oq">Direktuppspelning och batchvis målgruppsdelning från Real-time Customer Data Platform till Target via Edge-metoden</td>
    <td class="tg-0lax">- Dela strömnings- och gruppmålgrupper från Real-time Customer Data Platform till Target via Edge Network. Publiker som utvärderas i realtid kräver WebSDK och målgruppsutvärdering i realtid som beskrivs i integreringsmönster 1.<br>- Integrationen används vanligtvis för att dela direktuppspelnings- och gruppmålgrupper med traditionella SDK:er i stället för att migrera till Edge Collection och WebSDK som driver både direktuppspelnings- och gruppmålgrupper i realtid enligt beskrivningen i integreringsmönster 1.</td>
    <td class="tg-73oq">- Implementeringsmönster 1 eller 2 beskrivs nedan.<br>- Web/Mobile SDK krävs inte för att dela direktuppspelnings- och gruppmålgrupper med Target, även om det krävs för att aktivera realtidsutvärdering av edge segment enligt integreringsmönster 1. <br>- Om AT.js används stöds bara profilintegrering mot ECID-identitetsnamnutrymmet. <br>- För anpassade namnområdessökningar för identiteter på Edge krävs WebSDK-distributionen och varje identitet måste anges som en identitet på identitetskartan.<br>- Datastream måste konfigureras i Experience Edge. DataStream ID anges i målkonfigurationen.<br>- Målmålet måste konfigureras i Real-time Customer Data Platform Destinations.<br>- Integrering med Target kräver samma IMS-organisation som Experience Platform-instansen.</td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-73oq"><span style="font-weight:400;font-style:normal">Direktuppspelning och batchvis målgruppsdelning från Real-time Customer Data Platform till Target och Audience Manager via Audience Sharing Service</span></td>
    <td class="tg-0lax"><span style="font-weight:400;font-style:normal">- Dela strömnings- och gruppmålgrupper från Real-time Customer Data Platform till Target och Audience Manager via tjänsten Audience Sharing.<br> -Det här integreringsmönstret kan utnyttjas när ytterligare berikning från data från tredje part och målgrupper i Audience Manager önskas. I annat fall är integreringsmönstret 1 och 2 att föredra. Publiker som utvärderas i realtid kräver WebSDK och målgruppsutvärdering i realtid som beskrivs i integreringsmönster 1.</span></td>
    <td class="tg-73oq">- Implementeringsmönster 1 eller 2 beskrivs nedan.<br>- Web/Mobile SDK-distribution krävs inte för den här integreringen.<br>- Målgruppsprojektion via målgruppsdelningstjänsten måste tillhandahållas.<br>- Integrering med Target kräver samma IMS-organisation som Experience Platform-instansen.<br>- Identiteten måste matchas med ECID för att kunna dela till kanten för att Target ska kunna agera på den.</td>
  </tr>
</tbody>
</table>

## Realtids-, strömnings- och gruppmålgruppsdelning till Adobe Target

Arkitektur

<img src="assets/RTCDP+Target.png" alt="Referensarkitektur för Online/Offline Web Personalization Blueprint" style="width:80%; border:1px solid #4a4a4a" />

Sekvensdetalj

<img src="assets/RTCDP+Target_flow.png" alt="Referensarkitektur för Online/Offline Web Personalization Blueprint" style="width:80%; border:1px solid #4a4a4a" />

Översikt Arkitektur

<img src="assets/personalization_with_apps.png" alt="Referensarkitektur för Online/Offline Web Personalization Blueprint" style="width:80%; border:1px solid #4a4a4a"/>

## Implementeringsmönster

Kunden Personalization stöds via flera olika implementeringsmetoder.

### Implementeringsmönster 1 - Edge Network med Web/Mobile SDK (rekommenderat tillvägagångssätt)

Använda Edge Network med Web/Mobile SDK. Kantsegmentering i realtid kräver implementeringsmetoden för Web/Mobile SDK eller Edge API.

[Se Experience Platform Web and Mobile SDK Blueprint](../data-ingestion/websdk.md)

### Implementeringsmönster 2 - Programspecifika SDK:er

Använda traditionella programspecifika SDK:er (till exempel AT.js och AppMeasurement.js). Utvärdering av Edge-segment i realtid stöds inte med den här implementeringsmetoden. Direktuppspelning och gruppmålgruppsdelning från Experience Platform nav stöds dock med den här implementeringsmetoden.

[Se programspecifik SDK-skiss](../data-ingestion/appsdk.md)

### Implementeringssteg

1. [Implementera Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) för webb- och mobilapplikationer
1. [Implementera Experience Platform och [!UICONTROL Kundprofil i realtid]](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html) säkerställa att målgrupper som skapats aktiveras för Edge genom att konfigurera tillämpliga [sammanfogningsprincip](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=en#create-a-merge-policy) som aktivt på Edge.
1. Implementera [Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html). Experience Platform Web SDK krävs för edge-segmentering i realtid, men krävs inte för delning av strömnings- och batchmålgrupper från Real-time Customer Data Platform till Target. Observera att stöd för segmentering i realtid via Mobile SDK och API inte är tillgängligt för närvarande.
1. [Konfigurera Edge Network med Edge DataStream](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)
1. [Aktivera Adobe Target som mål i Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en)
1. (Valfritt) [Implementera Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html) (valfritt)
1. (Valfritt) [Begär etablering för målgruppsdelning mellan Experience Platform och Adobe Target (delade målgrupper)](https://www.adobe.com/go/audiences) för att dela målgrupper från Experience Platform till Target.

## Guardrails

[Läs mer i skyddsutkastet på sidan Översikt över skräddarsydda webb- och mobilskisser.](overview.md)

## Överväganden gällande implementering

Identitetskrav

* Alla primära identiteter kan utnyttjas när implementeringsmönster 1 används, vilket beskrivs ovan, med Edge-nätverket och WebSDK. Personalisering vid första inloggning kräver att personaliseringsbegäran anger en primär identitet som matchar den primära identiteten för profilen från Real-time Customer Data Platform. Identitetssammanfogning mellan anonyma enheter och kända kunder behandlas på navet och sedan projiceras till utkanten.
* För att kunna dela målgrupper från Adobe Experience Platform till Adobe Target måste ECID användas som identitet när målgruppsdelningstjänsten används, enligt vad som anges i användningsscenario 3 ovan.
* Alternativa identiteter kan även användas för att dela Experience Platform-målgrupper med Adobe Target via Audience Manager. Experience Platform aktiverar målgrupper till Audience Manager via följande namnutrymmen som stöds: IDFA, GAID, AdCloud, Google, ECID, EMAIL_LC_SHA256. Observera att Audience Manager och Target löser medlemskap för målgrupper via ECID-identiteten, så ECID krävs fortfarande för den slutliga målgruppsdelningen i Adobe Target.

## Relaterad dokumentation

### SDK-dokumentation

* [Experience Platform Web SDK-dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Dokumentation för Experience Platform-taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)
* [Experience Cloud ID-tjänstdokumentation](https://experienceleague.adobe.com/docs/id-service/using/home.html)

### Anslutningsdokumentation

* [Adobe Target Connection för Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en)
* [Konfiguration av Edge DataStream](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)
* [Experience Platform segmentdelning med Audience Manager och andra Experience Cloud-lösningar](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)

### Segmenteringsdokumentation

* [Översikt över segmentering i Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html)
* [Segmentering i realtid](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html)
* [Strömmande segmentering](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Adobe Analytics segmentdelning via Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)
* [Konfiguration av sammanfogningsprincip](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=en#create-a-merge-policy)

### Tutorials

* [Nästa steg i personaliseringen med CDP och Adobe Target i realtid](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=en)

### Relaterade blogginlägg

* [Adobe presenterar Same page Förbättrad personalisering med Adobe Target och Real-time Customer Data Platform](https://blog.adobe.com/en/publish/2021/10/05/adobe-announces-same-page-enhanced-personalization-with-adobe-target-real-time-customer-data-platform)
* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Adobe Experience Platform’s Identity Service — How to Solve the Customer Identity Conundrum]](https://medium.com/adobetech/adobe-experience-platforms-identity-service-how-to-solve-the-customer-identity-conundrum-f95e22d16ea9)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our “Customer Zero” Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
