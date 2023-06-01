---
title: Formgivning av datainsamling för vidarebefordran av händelser i flera sandlådor
description: Lär dig hur data som samlas in med Experience Platform Web och Mobile SDK kan konfigureras för att samla in en enda händelse och vidarebefordra till flera AEP-sandlådor.
solution: Data Collection
kt: 7202
source-git-commit: 3410adfd978de2458d257de96a7e484997f268db
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 0%

---


# Formgivning av datainsamling för vidarebefordran av händelser i flera sandlådor

Den här planen visar hur data som samlats in med Experience Platform Web och Mobile SDK kan konfigureras för att samla in en enda händelse och vidarebefordra till flera AEP-sandlådor. Denna plan är ett särskilt användningsexempel för datainsamling i MultiSandbox som använder händelsevidarebefordran för att uppnå detta mål.

Förutom att replikera händelsen med händelsevidarebefordringsfunktionerna kan du lägga till, filtrera eller ändra de ursprungliga insamlade data som uppfyller kraven för andra sandlådor.

Händelsevidarebefordring använder en separat egenskap som innehåller de dataelement, regler och tillägg som behövs för dina datakrav. Med en inkommande händelse kan din händelsevidarebefordringsegenskap samla in data och hantera dem efter behov före vidarebefordran.

Din målsandlåda kräver en konfigurerad slutpunkt för HTTP-direktuppspelning som används av tillägget Adobe Cloud Connector.

## Användningsexempel

* Global Data Reporting - När du använder flera sandlådor för att isolera operativmiljöer och behovet av att konsolidera datainsamling till en sandlåda för rapportering över flera sandlådor. Genom att skicka en Experience Edge-händelse via händelsevidarebefordran till en rapportsandlåda kan varje sandlådeoperativmiljö skicka data när de samlas in i realtid till en rapportsandlåda
* Hantera datainsamling över sandlådor baserat på olika dataregler för varje sandlådemiljö.

## Program

* Adobe Experience Platform Data Collection
* Vidarebefordran av händelser
* AEP-tillägg
* Cloud Connector-tillägg

## Överväganden

Med Händelsevidarebefordran som metod att skicka data till flera sandlådor, finns det saker du bör tänka på när det gäller din lösningsarkitektur.

### Inga HIPAA-data

Händelsevidarebefordran anses inte vara HIPAA-klart och ska inte användas i HIPAA-fall där HIPAA-data samlas in. Den infrastruktur som används för händelsevidarebefordran anses dock vara HIPAA-klar och bestäms av kunden själv. När egenskapen för taggen för händelsevidarebefordran finns i systemet för händelsevidarebefordring skickas hela datanyttolasten till systemet för händelsevidarebefordring för bearbetning. Det är den här processen som gör händelsevidarebefordran gällande HIPAA-användningsfall. När hela nyttolasten har skickats till händelsevidarebefordringssystemet inkluderar detta eventuella HIPAA-värden. Även om reglerna för händelsevidarebefordran kommer att filtrera dessa data innan de skickas till destinationen, kommer HIPAA-data fortfarande att skickas till en infrastruktur som inte är HIPAA-förberedd. Nyttolastdata lagras dock aldrig och är bara en genomströmning.

### Olika dataströmmar och slutpunkter för direktuppspelning

När data flödar genom dataströmmar från plattformens Edge-nätverk är ett HARD-krav att ALDRIG använda samma dataström eller slutpunkt för direktuppspelning som den dataström som gjorde den ursprungliga samlingen när händelsevidarebefordran till en annan AEP-sandlåda används. Detta kan vara skadligt för AEP-instansen och skulle kunna utlösa en DoS-situation.

### Uppskattad trafikvolym

Trafikvolymer krävs för granskning av varje användningsfall. Detta är viktigt eftersom stora volymer kan resultera i en strypningssituation och kunderna meddelas om detta inträffar.

## Arkitektur

![Vidarebefordran av händelser i flera sandlådor](assets/multi-sandbox-data-collection.png)

1. Det krävs att du samlar in och skickar händelsedata till plattforms-Edge-nätverket för att kunna använda händelsevidarebefordran. Kunderna kan använda Adobe-taggar för klient- eller Platform Edge Network Server-API för datainsamling från server till server. Plattformskantens nätverks-API kan tillhandahålla en server-till-server-samlingsfunktion. Detta kräver dock en annan programmeringsmodell för att implementera. Se [API-översikt för Edge Network Server](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=en)

1. Samlade nyttolaster skickas från taggimplementering till plattformskantnätverket till tjänsten för händelsevidarebefordran och bearbetas av dess egna dataelement, regler och åtgärder. Du kan läsa mer om skillnaderna [Taggar och händelsevidarebefordran](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=en#differences-from-tags).

1. En händelsevidarebefordringsegenskap krävs också för att ta emot insamlade händelsedata från plattformens Edge-nätverk. Huruvida händelsedata skickades till plattforms-Edge-nätverket av en implementerad tagg eller en server-till-server-samling. Författare definierar de dataelement, regler och åtgärder som används för att berika händelsedata innan de vidarebefordras till den andra sandlådan. Du bör använda JavaScript-dataelementet för anpassad kod för att strukturera dina data för sandlådeinmatning. I kombination med AEP Data Prep-funktioner har du flera alternativ för att hantera din datastruktur.

1. För närvarande krävs Adobe Cloud Connector Extension i egenskapen för händelsevidarebefordran. När reglerna bearbetar eller berikar händelsedata används Cloud Connector i ett hämtningsanrop som konfigurerats för en POST som skickar nyttolasten till den andra sandlådan.

1. En slutpunkt för direktuppspelning krävs för datainmatning i den andra sandlådan. Du kan också överväga funktionerna för dataförberedelse i AEP för att underlätta inmatning och mappning av händelsevidarebefordrande nyttolaster till XDM. Läs AEP-dokumentationen Skapa en [Anslutning för HTTP-API-direktuppspelning med användargränssnittet](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/streaming/http.html?lang=en)
