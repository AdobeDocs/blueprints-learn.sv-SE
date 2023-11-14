---
title: Adobe Commerce - RTCDP Blueprint
description: Adobe Experience Platform-integrering med Adobe Commerce för att skapa en enda kundvy och på ett intelligent sätt personalisera upplevelser i en digital butik och i alla kanaler.
solution: Real-Time Customer Data Platform, Commerce
source-git-commit: abb946358ceeee1af427c5b362ed2f48f733a6c9
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Adobe Commerce &amp; RTCDP

Med den här integrerade upplevelsen kan Adobe Commerce-kunder smidigt integrera med Adobe Experience Platform för att berika kundprofilen och personalisera upplevelser i digitala butiker och andra kanaler.

## Teknisk kapacitet aktiverad

* Lagra data (på kundsidan) som samlats in och skickats till valfri Adobe Experience Cloud-produkt. (lägg till i varukorgen, övergivna varukorgar osv.)
* Status för restorder på alla Adobe Experience Cloud-produkter
* Historiska beställningar kan skickas till Adobe Experience Platform
* Dela och personalisera RTCDP-målgrupper till Adobe Commerce

## Krav

Om du vill använda Experience Platform-kontakten måste du ha följande:

* Adobe Commerce 2.4.4 eller senare
* Adobe ID och organisations-ID
* Adobe Experience Platform/RTC
* [Adobe-klientdatalager (ACDL)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html?lang=en). ACDL krävs för att samla in data om butikshändelser.

## Onboarding-steg

### Datainsamling från Adobe Commerce till Adobe Experience Platform

* [Installera](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/install.html?lang=en) Experience Platform-kontakten.
* [Logga in](https://helpx.adobe.com/manage-account/using/access-adobe-id-account.html) till ditt Adobe-konto och visa för att bekräfta ditt organisations-ID. Organisations-ID är det ID som är kopplat till ditt tilldelade Experience Cloud-företag. Detta ID är en alfanumerisk sträng med 24 tecken, följt av (och måste innehålla) @AdobeOrg.
* [Skapa eller uppdatera](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html?lang=en) XDM-schemat med handelsspecifika fältgrupper.
* [Skapa en datauppsättning](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=en#create-a-dataset) baserat på det schema du skapade eller uppdaterade. Den här datauppsättningen innehåller de Commerce-data som du skickar.
* [Skapa ett datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/overview.html?lang=en) och välj det XDM-schema som innehåller de handelsspecifika fältgrupperna.
* [Anslut till Commerce Services](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html?lang=en).
* [Anslut till Adobe Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/connect-data.html?lang=en).

### Anslut till Commerce Destination från Adobe Experience Platform för målgruppsdelning

Så här ansluter du till Adobe Commerce-målet:

* I [Adobe Experience Platform](https://experience.adobe.com/platform/)går du till Destinationer > Katalog.
* Välj Personalisering.
* Markera Adobe Commerce-målet och välj sedan Konfigurera.
* Följ stegen som beskrivs i [självstudiekurs om destinationskonfiguration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en).

## Data som inte är i kartong

* Händelser för Storefront (webbläsare/app)
* Back office-händelser
* Historiska orderdata

En fullständig lista över händelser som stöds finns i [Commerce Events](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/event-forwarding/events.html?lang=en)

## Arkitektur

<img src="../commerce/assets/commerce_rtcdp.png" alt="Adobe Commerce RTCDP-arkitektur" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## Relaterade implementeringsguider

| Användarhandbok  | Länk |
|:----|:----|
| Platform Connector | [Adobe Commerce Experience Platform Connector - översikt](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/overview.html?lang=en) |
| Commerce Destination | [Adobe Commerce Connection i RTCDP](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-commerce.html?lang=en) |
| Edge Personalization | [Aktivera målgrupper för att kanalisera personaliseringsmål](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations.html?lang=en) | |
