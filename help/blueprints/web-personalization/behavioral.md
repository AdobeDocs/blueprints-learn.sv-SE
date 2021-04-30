---
title: Behavioral Web Personalization Blueprint
description: Personalisera baserat på onlinebeteende och målgruppsdata.
solution: Experience Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7085thumb-web-personalization-scenario1.jpg
exl-id: b9882c2c-cb45-4efa-a85c-8fe48f641a12
translation-type: tm+mt
source-git-commit: 76fe52d8e83e075f9e7ce6e8596880181b01a7fd
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Behavioral skiss för webb/mobilpersonalisering

Personalisera baserat på onlinebeteende och målgruppsdata.

## Användningsexempel

* Optimering av landningssidor
* Beteendeanpassning
* Personalisering baserad på tidigare produkt-/innehållsvyer, produkt-/innehållstillhörighet, miljöattribut, målgruppsdata från tredje part och demografiska data

## Program

* Adobe Target
* Adobe Analytics (valfritt)
* Adobe Audience Manager (valfritt)

## Arkitektur

<img src="assets/behavioral_personalization.svg" alt="Referensarkitektur för beteendeanpassning av webbdesign" style="border:1px solid #4a4a4a" />


## Guardrails

Som standard tillåter segmentdelningstjänsten att högst 75 målgrupper delas för varje Adobe Analytics-rapportserie. Om Audience Manager används för målgruppsdelning finns det ingen gräns för hur många målgrupper som kan delas. 

## Implementeringsmönster

Anpassningsplanen för webb/mobiler kan implementeras med följande metoder som beskrivs nedan.

1. Använda [!UICONTROL Platform Web SDK] eller [!UICONTROL Platform Mobile SDK] och [!UICONTROL Edge Network].
1. Använda traditionella programspecifika SDK:er (till exempel AppMeasurement.js)

### 1. SDK och Edge-strategi för plattformar för webb/mobiler

<img src="assets/web_sdk_flow.svg" alt="Referensarkitektur för [!UICONTROL Platform Web SDK] eller [!UICONTROL Platform Mobile SDK] och [!UICONTROL Edge Network]" style="border:1px solid #4a4a4a" />

### 2. Programspecifik SDK-metod

<img src="assets/app_sdk_flow.png" alt="Referensarkitektur för den programspecifika SDK-metoden" style="border:1px solid #4a4a4a" />

## Krav för implementering

| Program/tjänst | Nödvändigt bibliotek | Anteckningar |
|---|---|---|
| Adobe Target | [!UICONTROL Platform Web SDK]*, at.js 0.9.1+, eller mbox.js 61+ | at.js är att föredra eftersom mbox.js inte längre utvecklas. |
| Adobe Audience Manager (tillval) | [!UICONTROL Platform Web SDK]* eller dil.js 5.0+ |  |
| Adobe Analytics (tillval) | [!UICONTROL Platform Web SDK]* eller AppMeasurement.js 1.6.4+ |  |
| Experience Cloud Identity Service | [!UICONTROL Platform Web SDK]* eller VisitorAPI.js 2.0+ |  |
| Experience Platform Mobile SDK (tillval) | 4.11 eller senare för iOS och Android™ |  |
| Experience Platform Web SDK | 1.0, den aktuella Experience Platform SDK-versionen har [olika användningsfall som ännu inte stöds för Experience Cloud-programmen](https://github.com/adobe/alloy/projects/5) |  |

## Implementeringssteg

1. [Implementera Adobe ](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) Targeting för webb- och mobilapplikationer.

   Om du använder Audience Manager eller Adobe Analytics:

1. [Implementera Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html)
1. [Implementera Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)
1. [Implementera identitetstjänst för Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html)

   >[!NOTE]
   >
   >Varje program måste använda Experience Cloud-ID och vara en del av samma Experience Cloud-organisation för att ge möjlighet till målgruppsdelning mellan program.

1. [Begär etablering för tjänsterna Personer och Målgruppsdelning (delade målgrupper)](https://www.adobe.com/go/audiences)
1. Skapa segment i [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-build.html) eller [Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html) och [konfigurera dessa målgrupper för delning till Experience Cloud (om du använder Audience Manager eller Adobe Analytics)](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)
1. När målgrupperna finns i Adobe Target kan de användas för [målgruppsupplevelser med Adobe Target](https://experienceleague.adobe.com/docs/target/using/audiences/target.html)

## Relaterad dokumentation

* [Experience Cloud målgrupper](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html)
* [Integrera Audience Manager med Adobe Target](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html)
* [Adobe Analytics segmentdelning via Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)


## Relaterade blogginlägg

* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Integrating Adobe Experience Platform Decisioning Engine with AEM Websites]](https://jaeness.medium.com/integrating-adobe-experience-platform-decisioning-engine-with-aem-websites-9c222acd12e2)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our “Customer Zero” Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL How Adobe Experience Platform Can Help Customers Personalize Their Mobile Messaging in Real-Time with Journey Orchestration Service and a Mobile Messaging Vendor]](https://medium.com/adobetech/how-adobe-experience-platform-helped-a-client-personalize-their-mobile-messaging-in-real-time-with-7d634aefa098)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
