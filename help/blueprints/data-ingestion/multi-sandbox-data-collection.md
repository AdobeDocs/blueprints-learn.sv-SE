---
title: Formgivning av datainsamling för vidarebefordran av händelser i flera sandlådor
description: Strömma insamlade data från Experience Platform SDK:er till flera sandlådor med hjälp av Event Forwarding
solution: Data Collection
kt: 7202
exl-id: c24a47fe-b3da-4170-9416-74d2b6a18f32
source-git-commit: 5110ee2a7a079945475055cbcfdabf7cdcaa0ab5
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 0%

---

# Formgivning av datainsamling för vidarebefordran av händelser i flera sandlådor

En översikt över datainsamling för vidarebefordran av händelser i flera sandlådor visar hur data som samlats in med Adobe Experience Platform Web och Mobile SDK kan konfigureras för att samla in en enda händelse och vidarebefordras till flera AEP-sandlådor. Det här utkast är ett särskilt användningsexempel som använder funktionen för händelsespridning i Adobe-taggar.

Förutom att replikera händelsen med händelsevidarebefordringsfunktionerna kan du lägga till, filtrera eller ändra de data som ursprungligen samlats in och som uppfyller kraven för andra sandlådor. Sandbox A behöver till exempel ta emot alla händelsedataelement och Sandbox B ska bara ta emot icke-PII-data.

Händelsevidarebefordring använder en separat taggegenskap som innehåller de dataelement, regler och tillägg som behövs för dina datakrav. Med en inkommande händelse kan din händelsevidarebefordringsegenskap samla in data och hantera dem efter behov före vidarebefordran.

Din målsandlåda skulle behöva en konfigurerad slutpunkt för HTTP-direktuppspelning som skulle användas av det händelsevidarebefordrande HTTPS-tillägget.



## Användningsexempel

* Global Data Reporting - När du använder flera sandlådor för att isolera operativmiljöer och behovet av att konsolidera datainsamling till en sandlåda för rapportering över flera sandlådor. Händelse Vidarebefordra till en rapportsandlåda gör att varje sandlådemiljö kan skicka data när de samlas in i realtid till en rapportsandlåda
* Hantera datainsamling över sandlådor baserat på olika dataregler för varje sandlådemiljö. Sådana miljöer som kräver filtrering av känsliga data som hälso- och sjukvård och finansiella tjänster

## Program

* Adobe Experience Platform Data Collection

## Arkitektur

<img src="assets/multi-Sandbox-Data-Collection.svg" alt="Referensarkitektur för vidarebefordran av händelser i flera sandlådor" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

1. Taggförfattare definierar både en taggegenskap och en händelsevidarebefordringsegenskap. Här definierar författare de dataelement, regler och åtgärder som hanterar datainsamling. Tänk på att taggegenskapskoden körs på klienten och distribueras av en CDN-värd. Egenskapskoden för händelsevidarebefordran körs på Adobe Edge Server.

1. Data som samlas in på klienten skickas till Edge Network. Kunderna kan också skicka data till sin egen server först som en metod för att samla in data på serversidan.  Web SDK kan tillhandahålla en server-till-server-samlingsfunktion. Detta kräver dock en annan programmeringsmodell för att implementera. Läs dokumentationen **API-översikt för Edge Network Server** nedan

1. Platform Edge Network tar emot datainsamlingsnyttolaster och strukturerar dataflödet till de system som krävs, till exempel Target och Analytics.

1. Dataelement för händelsevidarebefordringsegenskaper används för att komma åt händelsedata som kommer in i nyttolasten. Regler kan också användas för att ändra händelsedata efter behov innan de vidarebefordras. som att formatera data i den XDM som krävs för direktuppspelad datainmatning

1. Vidarebefordran av händelser ger det HTTPS-tillägg som gör det möjligt att vidarebefordra dina händelsedata till en HTTPS-slutpunkt.

1. Sandbox 2 har konfigurerats med en direktuppspelningsslutpunkt som tar emot den vidarebefordrade händelsen.

## Relaterad dokumentation

* [Dokumentation för vidarebefordran av händelser](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)
* [Videofilmer om hur du vidarebefordrar händelser](https://experienceleague.adobe.com/docs/launch-learn/tutorials/server-side/overview.html)
* [Lektion om vidarebefordran av händelser](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding.html) självstudiekurs för Web SDK
* [Experience Platform Web SDK - översikt](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [API-översikt för Edge Network Server](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html)

## Relaterade blogginlägg

* [[!DNL Boosting Website Performance with Adobe Experience Platform Web SDK and Edge Network]](https://medium.com/adobetech/boosting-website-performance-with-adobe-experience-platform-web-sdk-and-edge-network-329fcf70fdf9)
* [[!DNL Solving Implementation Pain Points with Adobe Experience Platform Web SDK and Edge Network]](https://medium.com/adobetech/solving-implementation-pain-points-with-adobe-experience-platform-web-sdk-and-edge-network-880b635e6819)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Adobe Experience Platform Web SDK — Adobe Target]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-adobe-target-9b9f621d271)
* [[!DNL Adobe Experience Platform Web SDK Migration Scenarios for Adobe Analytics]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-migration-scenarios-for-adobe-analytics-91c255ec82b0)
* [[!DNL Unify Your Adobe Experience Platform Services with Adobe Experience Platform Web SDK]](https://medium.com/adobetech/unify-your-adobe-experience-platform-services-with-adobe-experience-platform-web-sdk-75cf6851a9fc)
* [[!DNL Accelerate Your Mobile Application Development with Adobe Experience Platform Mobile SDK and Launch]](https://medium.com/adobetech/accelerate-your-mobile-application-development-with-adobe-experience-platform-mobile-sdk-and-launch-ed023536d611)
* [[!DNL Simplifying Customer Workflows with Adobe Experience Platform Web SDK]](https://medium.com/adobetech/simplifying-customer-workflows-with-adobe-experience-platform-web-sdk-4e54fe134f4a)
