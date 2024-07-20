---
title: Datainsamling för vidarebefordran av händelser i flera sandlådor
description: Lär dig hur data som samlas in med Experience Platform Web och Mobile SDK kan konfigureras för att samla in en enda händelse och vidarebefordras till flera Experience Platform-sandlådor.
solution: Data Collection
kt: 7202
exl-id: ecc94fc8-9fad-4b88-a153-3d0fc00d8d58
source-git-commit: 72eb4e2ff276279a2fc88ead0b17d77cc8e99b97
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---

# Datainsamling för vidarebefordran av händelser i flera sandlådor

Den här planen visar hur data som samlats in med [!DNL Experience Platform] webb- och Mobile SDK:er kan konfigureras för att samla in en enda händelse och vidarebefordra till flera AEP-sandlådor. Denna skiss är specifik för datainsamling med flera sandlådor där [!UICONTROL Händelsevidarebefordran] används för att uppnå detta mål.

Förutom att replikera händelsen med [!UICONTROL funktioner för vidarebefordran av händelser] kan du lägga till, filtrera eller ändra de ursprungliga insamlade data som uppfyller kraven för andra sandlådor.

[!UICONTROL Händelsevidarebefordran] använder en separat egenskap som innehåller de [!UICONTROL dataelement], [!UICONTROL regler] och [!UICONTROL tillägg] som krävs för dina datakrav. Med en inkommande händelse kan din [!UICONTROL händelsevidarebefordring]-egenskap samla in data och hantera dem efter behov före vidarebefordran.

Målsandlådan kräver en konfigurerad slutpunkt för HTTP-direktuppspelning som används av tillägget [!UICONTROL Cloud Connector] i Adobe.

## Användningsfall

* Global datarapportering - När du använder flera sandlådor för att isolera operativmiljöer och behovet av att konsolidera datainsamling till en sandlåda för rapportering över flera sandlådor. Genom att skicka en Experience Edge-händelse via [!UICONTROL Händelsevidarebefordran] till en rapportsandlåda kan varje sandlådeoperativmiljö skicka data när de samlas in i realtid till en rapportsandlåda.

* Hantera datainsamling över sandlådor baserat på olika dataregler för varje sandlådemiljö.

## Tillämpningar

* Datainsamling för [!DNL Experience Platform]
* [!UICONTROL Händelsevidarebefordran]
* AEP [!UICONTROL Tillägg]
* [!UICONTROL Cloud Connector-tillägg]

## Överväganden

Med [!UICONTROL Händelsevidarebefordring] som metod att skicka data till flera sandlådor, finns det saker du bör tänka på när det gäller din lösningsarkitektur.

### Inga HIPAA-data

[!UICONTROL Händelsevidarebefordran] betraktas inte som HIPAA-förberedd och bör inte användas i HIPAA-fall där HIPAA-data samlas in.

Infrastrukturen som används för [!UICONTROL Händelsevidarebefordran] anses dock vara HIPAA-klar och bestäms endast av kunden. När egenskapen [!UICONTROL Händelsevidarebefordran] finns i systemet [!UICONTROL Händelsevidarebefordran] skickas hela datanyttolasten till systemet [!UICONTROL Händelsevidarebefordran] för bearbetning. Den här processen gör [!UICONTROL Händelsevidarebefordran] gällande HIPAA-användningsfall. När hela nyttolasten har levererats till systemet [!UICONTROL Händelsevidarebefordran] inkluderar den här processen alla HIPAA-värden. Trots att reglerna för [!UICONTROL händelsevidarebefordring] filtrerar dessa data innan de skickas till målet, skickas HIPAA-data fortfarande till en infrastruktur som inte är HIPAA-förberedd. Nyttolastdata lagras dock aldrig och är bara en vidarekoppling.

### Olika datastreams- och direktuppspelningsslutpunkter

När data flödar genom datastödraster från [!DNL Platform Edge Network], när [!UICONTROL Event Forwarding] används till en annan AEP-sandlåda, är ett krav att aldrig använda samma datastream- eller direktuppspelningsslutpunkt som den datastream som skapar den ursprungliga samlingen. Detta kan vara skadligt för AEP-instansen och skulle kunna utlösa en DoS-situation.

### Uppskattade trafikvolymer

Trafikvolymer krävs för granskning av varje användningsfall. Detta är viktigt eftersom stora volymer kan resultera i en strypningssituation och kunderna meddelas om detta inträffar.

## Arkitektur

![Flera sandlådor [!UICONTROL Händelsevidarebefordran]](assets/multi-sandbox-data-collection.png)

1. Du måste samla in och skicka händelsedata till [!DNL Platform Edge Network] för att kunna använda [!UICONTROL Händelsevidarebefordran]. Du kan använda Adobe-taggar för klientsidan eller [!DNL Platform Edge Network Server API] för datainsamling från server till server.

   [!DNL Platform Edge Network API] kan tillhandahålla en server-till-server-samlingsfunktion. Detta kräver dock en annan programmeringsmodell för att implementera. Mer information finns i [Edge Network Server API Overview](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=en).

1. Samlade nyttolaster skickas från taggimplementering till [!DNL Platform Edge Network] till tjänsten [!UICONTROL Händelsevidarebefordran] och bearbetas av dess egna [!UICONTROL dataelement], [!UICONTROL regler] och [!UICONTROL åtgärder]. Mer information om skillnaderna finns i [Taggar och [!UICONTROL Vidarebefordra händelser]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=en#differences-from-tags).

1. En [!UICONTROL händelsevidarebefordringsegenskap] krävs också för att ta emot insamlade händelsedata från [!DNL Platform Edge Network], oavsett om händelsedata skickades till [!DNL Platform Edge Network] av en distribuerad taggimplementering eller en server-till-server-samling.

   Författare definierar de dataelement, regler och åtgärder som används för att berika händelsedata innan de vidarebefordras till den andra sandlådan. Använd det anpassade dataelementet [!DNL JavaScript] för kod för att strukturera dina data för sandlådeinmatning. I kombination med plattformsdataförberedelsefunktioner har du flera alternativ för att hantera din datastruktur.

1. För närvarande krävs Adobe [!UICONTROL Cloud Connector Extension] i egenskapen [!UICONTROL Händelsevidarebefordran]. När reglerna har bearbetat eller berikat händelsedata används [!UICONTROL Cloud Connector] i ett hämtningsanrop som har konfigurerats för en POST och som skickar nyttolasten till den andra sandlådan.

1. En slutpunkt för direktuppspelning för datainmatning krävs för den andra sandlådan. Du kan också överväga funktionerna för [!UICONTROL dataprep] i AEP för att underlätta inmatning och mappning av [!UICONTROL händelsevidarebefordring]-nyttolaster till XDM. Läs AEP-dokumentationen Skapa en [HTTP API-direktuppspelningsanslutning med användargränssnittet](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/streaming/http.html?lang=en)
