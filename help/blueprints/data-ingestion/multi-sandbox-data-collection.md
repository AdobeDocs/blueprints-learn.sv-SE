---
title: Formgivning av datainsamling för vidarebefordran av händelser i flera sandlådor
description: Direktuppspela insamlade data från  [!DNL Experience Platform] (AEP) SDK:er till flera sandlådor med hjälp av händelsevidarebefordran
solution: Data Collection
kt: 7202
exl-id: c24a47fe-b3da-4170-9416-74d2b6a18f32
source-git-commit: 72eb4e2ff276279a2fc88ead0b17d77cc8e99b97
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# Rapport för datainsamling för vidarebefordran av händelser i flera sandlådor

Planen för datainsamling för vidarebefordran av händelser för flera sandlådor visar hur data som samlats in med Adobe [!DNL Experience Platform] Web och Mobile SDK kan konfigureras för att samla in en enda händelse och vidarebefordras till flera [!DNL Experience Platform] (AEP)-sandlådor. Det här utkast är ett särskilt användningsexempel som använder funktionen för händelsespridning i Adobe-taggar.

Förutom att replikera händelsen med händelsevidarebefordringsfunktionerna kan du lägga till, filtrera eller ändra de data som ursprungligen samlats in och som uppfyller kraven för andra sandlådor. Sandbox A behöver till exempel ta emot alla händelsedataelement och Sandbox B ska bara ta emot icke-PII-data.

Händelsevidarebefordring använder en separat taggegenskap som innehåller de dataelement, regler och tillägg som behövs för dina datakrav. Med en inkommande händelse kan din händelsevidarebefordringsegenskap samla in data och hantera dem efter behov före vidarebefordran.

Målsandlådan behöver en konfigurerad slutpunkt för HTTP-direktuppspelning som kan användas av HTTPS-tillägget för händelsevidarebefordran.

## Användningsfall

* Global Data Reporting - När du använder flera sandlådor för att isolera operativmiljöer och behovet av att konsolidera datainsamling till en sandlåda för rapportering över flera sandlådor. Händelse Vidarebefordra till en rapportsandlåda gör att varje sandlådeoperativmiljö kan skicka data när de samlas in i realtid till en rapportsandlåda
* Hantera datainsamling över sandlådor baserat på olika dataregler för varje sandlådemiljö. Sådana miljöer som kräver filtrering av känsliga data som hälso- och sjukvård och finansiella tjänster

## Tillämpningar

* Datainsamling för Adobe [!DNL Experience Platform]

## Arkitektur

<img src="assets/multi-Sandbox-Data-Collection.svg" alt="Referensarkitektur för vidarebefordran av händelser i flera sandlådor" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

1. Taggförfattare definierar både en taggegenskap och en händelsevidarebefordringsegenskap. Här definierar författare de dataelement, regler och åtgärder som hanterar datainsamling. Tänk på att taggegenskapskoden körs på klienten och distribueras av en CDN-värd. Koden [!UICONTROL Händelsevidarebefordringsegenskap] körs på Adobe [!DNL Edge Server].

1. Data som samlas in på klienten skickas till [!DNL Edge Network]. Kunderna kan också skicka data till sin egen server först som en metod för att samla in data på serversidan. Web SDK kan tillhandahålla en server-till-server-samlingsfunktion. Detta kräver dock en annan programmeringsmodell för att implementera. Läs mer i dokumentationen om **[!DNL Edge Network]Server-API-översikt** nedan

1. Plattformen [!DNL Edge Network] tar emot datainsamlingsnyttolaster och organiserar dataflödet till de system som krävs, till exempel Target och Analytics.

1. Dataelement för händelsevidarebefordringsegenskaper används för att komma åt händelsedata som kommer in i nyttolasten. Regler kan också användas för att ändra händelsedata efter behov innan de vidarebefordras. som att formatera data i den XDM som krävs för direktuppspelad datainmatning

1. Vidarebefordran av händelser ger det HTTPS-tillägg som gör det möjligt att vidarebefordra dina händelsedata till en HTTPS-slutpunkt.

1. Sandbox 2 har konfigurerats med en direktuppspelningsslutpunkt som tar emot den vidarebefordrade händelsen.

## Relaterad dokumentation

* [Dokumentation för vidarebefordran av händelser](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)
* [Vidarebefordrar videoklipp](https://experienceleague.adobe.com/docs/launch-learn/tutorials/server-side/overview.html)
* [Lektion om vidarebefordran av händelser](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding.html) i Web SDK-självstudiekursen
* [[!DNL Experience Platform] Web SDK-översikt](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [[!DNL Edge Network] Översikt över server-API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html)

## Relaterade blogginlägg

* [Förbättrar webbplatsprestanda med Adobe [!DNL Experience Platform] Web SDK och [!DNL Edge Network]](https://medium.com/adobetech/boosting-website-performance-with-adobe-experience-platform-web-sdk-and-edge-network-329fcf70fdf9)
* [Löser problem med implementeringen med Adobe [!DNL Experience Platform] Web SDK och [!DNL Edge Network]](https://medium.com/adobetech/solving-implementation-pain-points-with-adobe-experience-platform-web-sdk-and-edge-network-880b635e6819)
* [Adobe [!DNL Experience Platform] Web SDK för målgruppshantering](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [Adobe [!DNL Experience Platform] Web SDK - Adobe Target](https://medium.com/adobetech/adobe-experience-platform-web-sdk-adobe-target-9b9f621d271)
* [Adobe [!DNL Experience Platform] SDK-migreringsscenarier för Adobe Analytics](https://medium.com/adobetech/adobe-experience-platform-web-sdk-migration-scenarios-for-adobe-analytics-91c255ec82b0)
* [Gör Adobe enhetliga [!DNL Experience Platform] tjänster med Adobe [!DNL Experience Platform] Web SDK](https://medium.com/adobetech/unify-your-adobe-experience-platform-services-with-adobe-experience-platform-web-sdk-75cf6851a9fc)
* [Snabba upp utvecklingen av mobilappar med Adobe [!DNL Experience Platform] Mobile SDK och Launch](https://medium.com/adobetech/accelerate-your-mobile-application-development-with-adobe-experience-platform-mobile-sdk-and-launch-ed023536d611)
* [Förenkla kundarbetsflöden med Adobe Experience Platform Web SDK](https://medium.com/adobetech/simplifying-customer-workflows-with-adobe-experience-platform-web-sdk-4e54fe134f4a)
