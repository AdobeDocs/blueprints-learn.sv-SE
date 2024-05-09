---
title: Adobe Commerce - RTCDP Blueprint
description: Adobe Experience Platform-integrering med Adobe Commerce för att skapa en enda kundvy och på ett intelligent sätt personalisera upplevelser i en digital butik och i alla kanaler.
solution: Real-Time Customer Data Platform, Commerce
exl-id: e2fc5e1c-c865-4c24-9b82-861a34aba487
source-git-commit: 80a4716a7ed64ec30b9c60b3444affc5bd8984e4
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Adobe Commerce &amp; RTCDP

The [!DNL Data Connection] som hjälper Adobe Commerce-kunder att smidigt integrera med Adobe Experience Platform för att berika kundprofilen och personalisera upplevelser i digitala butiker och andra kanaler.

## Teknisk kapacitet aktiverad

* Data från butiken (kundsidan, som att lägga till i kundvagnen, överge kundvagnen och så vidare) som samlas in och skickas till valfri Adobe Experience Cloud-produkt.
* Status för restorder på alla Adobe Experience Cloud-produkter
* Historiska beställningar kan skickas till Adobe Experience Platform
* Dela och personalisera RTCDP-målgrupper till Adobe Commerce

## Krav

Använd [!DNL Data Connection] måste du ha följande:

* Adobe Commerce 2.4.4 eller senare
* Adobe ID och organisations-ID
* Adobe Experience Platform/RTC
* [Adobe-klientdatalager (ACDL)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html). ACDL krävs för att samla in data om butikshändelser.

## Onboarding-steg

### Datainsamling från Adobe Commerce till Adobe Experience Platform

* [Installera](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/install.html) den [!DNL Data Connection] tillägg.
* [Logga in](https://helpx.adobe.com/manage-account/using/access-adobe-id-account.html) till ditt Adobe-konto och visa för att bekräfta ditt organisations-ID. Organisations-ID är det ID som är kopplat till ditt tilldelade Experience Cloud-företag. Detta ID är en alfanumerisk sträng med 24 tecken, följt av (och måste innehålla) @AdobeOrg.
* [Skapa eller uppdatera](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html) XDM-schemat med Commerce-specifika fältgrupper.
* [Skapa en datauppsättning](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset) baserat på det schema du skapade eller uppdaterade. Den här datauppsättningen innehåller de Commerce-data som du skickar.
* [Skapa ett datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/overview.html) och välj det XDM-schema som innehåller de Commerce-specifika fältgrupperna.
* [Anslut till Commerce Services](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html).
* [Anslut till Adobe Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/connect-data.html).

### Anslut till Commerce destination från Adobe Experience Platform för målgruppsdelning

Så här ansluter du till Adobe Commerce-målet:

* I [Adobe Experience Platform](https://experience.adobe.com/platform/)går du till Destinationer > Katalog.
* Välj Personalisering.
* Markera Adobe Commerce-målet och välj sedan Konfigurera.
* Följ stegen som beskrivs i [självstudiekurs om destinationskonfiguration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html).

## Data som inte är i kartong

* StoreFront-händelser (webbläsare/app)
* Back office-händelser
* Historiska orderdata

En fullständig lista över händelser som stöds finns i [Commerce Events](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/event-forwarding/events.html)

## Arkitektur

<img src="../commerce/assets/commerce_rtcdp.png" alt="Adobe Commerce RTCDP-arkitektur" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## Relaterade implementeringsguider

| Guide | Länk |
|:----|:----|
| Platform Connector | [Adobe Commerce Experience Platform Connector - översikt](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/overview.html) |
| Commerce Destination | [Adobe Commerce Connection i RTCDP](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-commerce.html) |
| Edge Personalization | [Aktivera målgrupper för att kanalisera personaliseringsmål](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations.html) |
