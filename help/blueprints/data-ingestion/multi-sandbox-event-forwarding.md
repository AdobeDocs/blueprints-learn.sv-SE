---
title: Datainsamling för vidarebefordran av händelser i flera sandlådor
description: Lär dig hur data som samlas in med Experience Platform Web och Mobile SDK kan konfigureras för att samla in en enda händelse och vidarebefordras till flera Experience Platform-sandlådor.
solution: Data Collection
kt: 7202
exl-id: ecc94fc8-9fad-4b88-a153-3d0fc00d8d58
source-git-commit: 3d6a2416cdb9956e59be4b2918ba19f88cd2150b
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 0%

---

# Datainsamling för vidarebefordran av händelser i flera sandlådor

Den här planen visar hur data som samlats in med Experience Platform Web och Mobile SDK kan konfigureras för att samla in en enda händelse och vidarebefordra till flera AEP-sandlådor. Denna skiss är specifik för datainsamling med flera sandlådor som använder [!UICONTROL Vidarebefordran av händelser] för att uppnå detta mål.

Förutom att replikera händelsen med [!UICONTROL Vidarebefordran av händelser] kan du lägga till, filtrera eller ändra de ursprungliga insamlade data som uppfyller kraven för andra sandlådor.

[!UICONTROL Vidarebefordran av händelser] använder en separat egenskap som innehåller [!UICONTROL Dataelement], [!UICONTROL Regler]och [!UICONTROL Tillägg] nödvändiga för dina databehov. Med en inkommande händelse [!UICONTROL Vidarebefordran av händelser] kan samla in data och hantera dem efter behov före vidarebefordran.

Din målsandlåda kräver en konfigurerad slutpunkt för HTTP-direktuppspelning som används av Adobe [!UICONTROL Cloud Connector] tillägg.

## Användningsexempel

* Global datarapportering - När du använder flera sandlådor för att isolera operativmiljöer och behovet av att konsolidera datainsamling till en sandlåda för rapportering över flera sandlådor. Skicka en Experience Edge-händelse via [!UICONTROL Vidarebefordran av händelser] till en rapportsandlåda gör det möjligt för varje sandlådemiljö att skicka data när de samlas in i realtid till en rapportsandlåda.

* Hantera datainsamling över sandlådor baserat på olika dataregler för varje sandlådemiljö.

## Program

* [!DNL Experience Platform] Datainsamling
* [!UICONTROL Vidarebefordran av händelser]
* AEP [!UICONTROL Tillägg]
* [!UICONTROL Cloud Connector-tillägg]

## Överväganden

Med [!UICONTROL Vidarebefordran av händelser] När det gäller att skicka data till flera sandlådor finns det vissa överväganden som måste beaktas i din lösningsarkitektur.

### Inga HIPAA-data

[!UICONTROL Vidarebefordran av händelser] inte betraktas som HIPAA-klar och bör inte användas i HIPAA-fall där HIPAA-data samlas in. Den infrastruktur som används för [!UICONTROL Vidarebefordran av händelser] är att betrakta som HIPAA-redo och är helt och hållet kundens val. Med [!UICONTROL Vidarebefordran av händelser] Taggegenskapen finns i [!UICONTROL Vidarebefordran av händelser] systemet skickas hela datanyttolasten till [!UICONTROL Vidarebefordran av händelser] system för bearbetning. Det är denna process som [!UICONTROL Vidarebefordran av händelser] för användning av HIPAA. Med hela nyttolasten levererad till [!UICONTROL Vidarebefordran av händelser] system, inkluderar detta alla HIPAA-värden. Trots att [!UICONTROL Vidarebefordran av händelser] regler kommer att filtrera dessa data innan de skickas till destinationen, att HIPAA-data fortfarande skickas till en infrastruktur som inte är HIPAA-förberedd. Nyttolastdata lagras dock aldrig och är bara en genomströmning.

### Olika datastreams- och direktuppspelningsslutpunkter

När data flödar genom datastödraster från [!UICONTROL Platform Edge Network], när du använder [!UICONTROL Vidarebefordran av händelser] till en annan AEP-sandlåda är ett krav att aldrig använda samma datastream- eller direktuppspelningsslutpunkt som den datastream som skapar den ursprungliga samlingen. Detta kan vara skadligt för AEP-instansen och skulle kunna utlösa en DoS-situation.

### Uppskattade trafikvolymer

Trafikvolymer krävs för granskning av varje användningsfall. Detta är viktigt eftersom stora volymer kan resultera i en strypningssituation och kunderna meddelas om detta inträffar.

## Arkitektur

![Flera sandlådor [!UICONTROL Vidarebefordran av händelser]](assets/multi-sandbox-data-collection.png)

1. Samla in och skicka händelsedata till [!UICONTROL Platform Edge Network] krävs för att kunna använda [!UICONTROL Vidarebefordran av händelser]. Kunder kan använda Adobe-taggar för klientsidan eller [!UICONTROL API för plattforms-Edge Network Server] för datainsamling mellan servrar. The [!UICONTROL API för plattformen Edge Network] kan tillhandahålla en server-till-server-samlingsfunktion. Detta kräver dock en annan programmeringsmodell för att implementera. Se [API-översikt för Edge Network Server](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=en).

1. Samlade nyttolaster skickas från taggimplementering till [!UICONTROL Platform Edge Network] till [!UICONTROL Vidarebefordran av händelser] och behandlas av en egen [!UICONTROL Dataelement], [!UICONTROL Regler] och [!UICONTROL Åtgärder]. Du kan läsa mer om skillnaderna [Taggar och [!UICONTROL Vidarebefordran av händelser]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=en#differences-from-tags).

1. An [!UICONTROL Vidarebefordran av händelser] egenskapen krävs också för att ta emot insamlade händelsedata från [!UICONTROL Platform Edge Network]. Om händelsedata skickades till plattforms-Edge-nätverket av en implementerad tagg eller en server-till-server-samling. Författare definierar de dataelement, regler och åtgärder som används för att berika händelsedata innan de vidarebefordras till den andra sandlådan. Överväg att använda anpassad kod [!DNL JavaScript] dataelement som hjälper till att strukturera data för sandlådeinmatning. I kombination med plattformsdataförberedelsefunktioner har du flera alternativ för att hantera din datastruktur.

1. För närvarande används Adobe [!UICONTROL Cloud Connector-tillägg] krävs i [!UICONTROL Vidarebefordran av händelser] Egenskap. När reglerna bearbetar eller berikar händelsedata används Cloud Connector i ett hämtningsanrop som konfigurerats för en POST som skickar nyttolasten till den andra sandlådan.

1. En slutpunkt för direktuppspelning för datainmatning krävs för den andra sandlådan. Du kan också överväga funktionerna för dataprep i AEP för att underlätta intag och mappning av [!UICONTROL Vidarebefordran av händelser] nyttolaster till XDM. Läs AEP-dokumentationen Skapa en [HTTP API Streaming Connection med användargränssnittet](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/streaming/http.html?lang=en)
