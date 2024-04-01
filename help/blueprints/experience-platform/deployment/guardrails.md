---
title: Experience Platform och programskydd
description: Garantier definierar förväntningarna på prestanda och påverkan för komponenter och tjänster i Adobe Experience Platform och program
solution: Customer Journey Analytics, Journey Orchestration, Real-Time Customer Data Platform
thumbnail: null
exl-id: b64cf3e4-cc5d-4984-8a0f-4736d432b8e1
source-git-commit: 60a7785ea0ec4ee83fd9a1e843f0b84fc4cb1150
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---

# Guardrails

Vi rekommenderar att du anger tröskelvärden som ger vägledning för data, observerad fördröjning och systemanvändning i Adobe Experience Platform och program. Garantierna speglar systembegränsningar och prestandaförväntningar för att optimera kundens arkitektur och använda fallissemang samt hjälper till att undvika fel och oväntade resultat. Garantier är inte avsedda att vara servicenivåavtal, servicenivåavtal beskrivs i de produktbeskrivningar som är länkade nedan och i kundlicensavtalen. Garantier är avsedda att ge vägledning i arkitekturen av lösningar för specifika kundanvändningsfall för att säkerställa stabilitet och utförande.

Information om specifika servicenivåavtal för program och funktioner finns i [Program- och funktionsbeskrivningar](#application-feature-descriptions) längst ned på den här sidan.

Observera att för alla kundärenden som har strikta krav på fördröjning eller volym rekommenderar Adobe att du granskar ditt användningsfall i detalj med ditt kontoteam på Adobe och din implementeringspartner. I vissa fall är det tillrådligt att testa och observera en viss implementering av ett visst användningsfall innan produktionen startar användarexemplet för att observera och förstå förväntat beteende - eftersom varje kundimplementering har olika faktorer som är under spel, inklusive typ och frånvaro av datadrag, de specifika egenskaperna hos segmentreglerna som byggs och de olika aktiveringskanalerna och nyttolasterna - kommer varje implementering av användningsfall att ha olika observerade prestanda. Därför är det bäst att fastställa och testa den förväntade prestandan direkt för att säkerställa en korrekt arkitektur och implementering i enlighet med de latens- och prestandakrav som gäller för användningsfallet.


## Referensdokumentation för säkerhetsutkast för Adobe Experience Platform och program

Följande sidor innehåller information om säkerhetsutkast för Adobe Experience Platform funktioner, tjänster och program:

**Experience Platform-program**

* [Översikt över Real-Time CDP skyddsutkast](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/guardrails/overview.html)
* [Customer Journey Analytics, skyddsräcken för målgruppsdelning](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html#latency)
* [Customer Journey Analytics skyddsräcken för dataöverföring](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html#what-is-the-expected-latency-for-analytics-data-on-platform%3F)
* [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html)

**Experience Platform**

* [Skyddsförslag för dataöverföring](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html)
* [[!DNL Edge Network] API-guider](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* [Kundprofil och segmenteringsgurkor i realtid](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
* [Identitetsgarantins](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=en)
* [Frågetjänstens säkerhetsbeskrivningar](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=en)
* [Målaktiveringsskydd](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html)

## Latensdiagram från början till slut {#end-to-end-latency}

### Experience Platform Edge Network och Hub Primär observerad latens {#edge-hub-latencies}

I följande diagram visas den primära kanten och hubben som observerats för att vara medveten om när man konstruerar användningsfall på Experience Platform och program.

![Experience Platform [!DNL Edge Network] och navens primära observerade latenser.](/help/blueprints/experience-platform/deployment/assets/aep_edge_hub_latency.svg "Experience Platform Edge-nätverk och primära latenser för navnätverk"){width="1000" zoomable="yes"}

### Intag av data {#data-ingestion}

Diagrammet nedan visar förväntade fördröjningsvärden för dataöverföring via [direktuppspelning](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html) och [batchintag](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/getting-started.html?lang=en) när data hämtas till Real-Time CDP. Klicka på bilden för att se en högupplöst version.

![Översikt över dataöverföring på hög nivå.](/help/blueprints/experience-platform/deployment/assets/aep_data_flow_guardrails.svg "Högnivåvisuell överblick och fördröjningsvärden för dataöverföring"){width="1000" zoomable="yes"}

### Segmentering {#segmentation}

Diagrammet nedan visar förväntade fördröjningsvärden när du arbetar med målgrupper i [Real-Time CDP segmenteringstjänst](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html). Klicka på bilden för att se en högupplöst version.

![Översikt över segmentering på hög nivå.](/help/blueprints/experience-platform/deployment/assets/segmentation_guardrails.svg "Segmentera visuell översikt och latensvärden på hög nivå"){width="1000" zoomable="yes"}

### REAL-TIME CUSTOMER DATA PLATFORM &amp; [!DNL Edge Network] {#adobe-edge-latency}

Diagrammet nedan visar förväntade fördröjningsvärden när du använder [!DNL Edge Network] - till exempel för att utnyttja RTCDP-målgrupper i [Adobe Target](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en). Klicka på bilden för att se en högupplöst version.

![Adobe Edge Network och Experience Platform.](/help/blueprints/experience-platform/deployment/assets/RTCDP_Edge_guardrails.svg "Exportera målgrupper till Adobe Target visuella översikt och latens på hög nivå"){width="1000" zoomable="yes"}

### Customer Journey Analytics {#customer-journey-analytics}

Diagrammet nedan visar förväntade fördröjningsvärden när du arbetar med [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=en). Klicka på bilden för att se en högupplöst version.

![Arbeta med högnivåvisuell översikt på Customer Journey Analytics.](/help/blueprints/experience-platform/deployment/assets/CJA_guardrails.svg "Arbeta med högnivåvisuell översikt och latensvärden för Customer Journey Analytics"){width="1000" zoomable="yes"}

### Journey Optimizer {#journey-optimizer}

Diagrammet nedan visar förväntade fördröjningsvärden när du arbetar med [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=en). Klicka på bilden för att se en högupplöst version.

![Arbeta med Adobe Journey Optimizer visuella översikt på hög nivå.](/help/blueprints/experience-platform/deployment/assets/AJO_guardrails.svg "Arbeta med Adobe Journey Optimizer högnivåvisuella översikter och latensvärden"){width="1000" zoomable="yes"}

## Program- och funktionsbeskrivningar {#application-feature-descriptions}

Mer information om funktionsspecifika servicenivåavtal finns i produktbeskrivningarna nedan:

* [Experience Platform Collection Enterprise](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-collection-enterprise.html)
* [Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [B2B Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-b2b.html)
* [Aktivering av Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html)
* [Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Intelligenta tjänster](https://helpx.adobe.com/legal/product-descriptions/intelligent-services.html)
* [Data Distiller](https://helpx.adobe.com/legal/product-descriptions/data-distiller.html)
* [Customer Journey Analytics](https://helpx.adobe.com/legal/product-descriptions/customer-journey-analytics.html)
* [Journey Optimizer](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
* [Journey Orchestration](https://helpx.adobe.com/legal/product-descriptions/journey-orchestration.html)
* [Offer decisioning](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html)
