---
title: Behavioral Web Personalization plan
description: Ta reda på hur du personanpassar innehåll baserat på onlinebeteende och målgruppsdata.
landing-page-description: Lär dig att personanpassa baserat på onlinebeteende och målgruppsdata.
short-description: Lär dig att personanpassa baserat på onlinebeteende och målgruppsdata.
solution: Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection, Experience Platform
kt: 7085
thumbnail: thumb-web-personalization-scenario1.jpg
exl-id: b9882c2c-cb45-4efa-a85c-8fe48f641a12
source-git-commit: b0f106c4dce59137086c8806def34e98b554bb61
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 7%

---

# Beteendeanpassning för webb/mobiler

Personalisera baserat på onlinebeteende och målgruppsdata.

## Användningsexempel

* Optimering av landningssidor
* Beteendeanpassning
* Personalisering baserad på tidigare produkt-/innehållsvyer, produkt-/innehållstillhörighet, miljöattribut, målgruppsdata från tredje part och demografiska data

## Program

* Adobe Target
* Adobe Analytics (valfritt)
* Adobe Audience Manager (valfritt)
* Adobe Real-time Customer Data Platform (valfritt)

## Arkitektur

<img src="assets/behavioral_personalization.svg" alt="Referensarkitektur för beteendeanpassning av webbdesign" style="width:90%; border:1px solid #4a4a4a; margin-bottom: 15px;" class="modal-image" />


## Implementeringsmönster

Anpassningsplanen för webb/mobiler kan implementeras med följande metoder som beskrivs nedan.

1. Använda [!UICONTROL Platform Web SDK] eller [!UICONTROL Plattformsmobil SDK] och [!UICONTROL Edge Network]. [Se Experience Platform Web and Mobile SDK Blueprint](..//experience-platform/deployment/websdk.md)
1. Använda traditionella programspecifika SDK:er (till exempel AppMeasurement.js). [Se programspecifik SDK-skiss](..//experience-platform/deployment/appsdk.md)

## Implementeringssteg

1. [Implementera Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) för webb- och mobilapplikationer.

### Implementeringssteg - Audience Manager eller Adobe Analytics

1. [Implementera Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html)
1. [Implementera Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)
1. [Implementera identitetstjänst för Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html)

   >[!NOTE]
   >
   >Varje program måste använda Experience Cloud-ID och vara en del av samma Experience Cloud-organisation för att ge möjlighet till målgruppsdelning mellan program.

1. [Begär etablering för tjänsterna Personer och Målgruppsdelning (delade målgrupper)](https://www.adobe.com/go/audiences)
1. Bygg segment i [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-build.html) eller [Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html) och [konfigurera dessa målgrupper för delning till Experience Cloud](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)  (om du använder Audience Manager eller Adobe Analytics)
1. När målgrupperna finns i Adobe Target kan de användas för [målinrikta upplevelser med Adobe Target](https://experienceleague.adobe.com/docs/target/using/audiences/target.html)

### Implementeringssteg - Real-time Customer Data Platform

1. [Skapa scheman](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) för data som ska importeras.
1. [Skapa datauppsättningar](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) för data som ska importeras.
1. [Konfigurera rätt identiteter och identitetsnamnutrymmen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html) på schemat för att säkerställa att inkapslade data kan sammanfogas till en enhetlig profil.
1. [Aktivera scheman och datauppsättningar för profilen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Ingrediera data](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) till Experience Platform.
1. [Tillhandahållande [!UICONTROL Real-time Customer Data Platform] segmentdelning](https://www.adobe.com/go/audiences) mellan Experience Platform och Audience Manager för målgrupper som definieras i Experience Platform som ska delas med Audience Manager.
1. [Skapa segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) i Experience Platform. Systemet avgör automatiskt om segmentet utvärderas som batch eller direktuppspelning.
1. [Konfigurera mål](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html) för delning av profilattribut och målgruppsmedlemskap till önskade mål.


## Relaterad dokumentation

* [Experience Cloud målgrupper](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html)
* [Integrera Audience Manager med Adobe Target](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html)
* [Adobe Analytics segmentdelning via Adobe Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)
* [[!UICONTROL Real-time Customer Data Platform] översikt](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [[!UICONTROL Real-time Customer Data Platform] Produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Riktlinjer för profil och segmentering](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Segmenteringsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Destinationsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)

## Relaterade blogginlägg

* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Integrating Adobe Experience Platform Decisioning Engine with AEM Websites]](https://jaeness.medium.com/integrating-adobe-experience-platform-decisioning-engine-with-aem-websites-9c222acd12e2)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our "Customer Zero" Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL How Adobe Experience Platform Can Help Customers Personalize Their Mobile Messaging in Real-Time with Journey Orchestration Service and a Mobile Messaging Vendor]](https://medium.com/adobetech/how-adobe-experience-platform-helped-a-client-personalize-their-mobile-messaging-in-real-time-with-7d634aefa098)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
