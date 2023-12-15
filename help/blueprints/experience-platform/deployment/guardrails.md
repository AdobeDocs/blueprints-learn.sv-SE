---
title: Experience Platform och programskydd
description: Garantier definierar förväntningarna på prestanda och påverkan för komponenter och tjänster i Adobe Experience Platform och program
solution: Customer Journey Analytics, Journey Orchestration, Real-Time Customer Data Platform
thumbnail: null
exl-id: b64cf3e4-cc5d-4984-8a0f-4736d432b8e1
source-git-commit: 4cc0eafda6e2670ac5b72b0a0ca59b84e1c0dba1
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# Guardrails

Vi rekommenderar att du anger tröskelvärden som ger vägledning för data, observerad fördröjning och systemanvändning i Adobe Experience Platform och program. Garantierna speglar systembegränsningar och prestandaförväntningar för att optimera kundens arkitektur och använda fallissemang samt hjälper till att undvika fel och oväntade resultat. Garantier är inte avsedda att vara servicenivåavtal.

Information om specifika servicenivåavtal för program och funktioner finns i [Program- och funktionsbeskrivningar](#application-feature-descriptions) längst ned på den här sidan.


## Referensdokumentation för säkerhetsutkast för Adobe Experience Platform och program

Följande sidor innehåller information om säkerhetsutkast för Adobe Experience Platform funktioner, tjänster och program:

**Experience Platform-program**

* [Översikt över Real-Time CDP skyddsutkast](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/guardrails/overview.html)
* [Customer Journey Analytics, skyddsräcken för målgruppsdelning](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html#latency)
* [Customer Journey Analytics skyddsräcken för dataöverföring](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html#what-is-the-expected-latency-for-analytics-data-on-platform%3F)
* [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html)

**Experience Platform**

* [Skyddsförslag för dataöverföring](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html)
* [Guardrutor för Edge Network API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* [Kundprofil och segmenteringsgurkor i realtid](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
* [Identitetsgarantins](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=en)
* [Frågetjänstens säkerhetsbeskrivningar](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=en)
* [Målaktiveringsskydd](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html)

## Latensdiagram från början till slut {#end-to-end-latency}

### Intag av data {#data-ingestion}

Diagrammet nedan visar förväntade fördröjningsvärden för dataöverföring via [direktuppspelning](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html) och [batchintag](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/getting-started.html?lang=en) när data hämtas till Real-Time CDP. Klicka på bilden för att se en högupplöst version.

![Översikt över dataöverföring på hög nivå.](/help/blueprints/experience-platform/deployment/assets/aep_data_flow_guardrails.svg "Högnivåvisuell överblick och fördröjningsvärden för dataöverföring"){width="1000" zoomable="yes"}

### Segmentering {#segmentation}

Diagrammet nedan visar förväntade fördröjningsvärden när du arbetar med målgrupper i [Real-Time CDP segmenteringstjänst](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html). Klicka på bilden för att se en högupplöst version.

![Översikt över segmentering på hög nivå.](/help/blueprints/experience-platform/deployment/assets/segmentation_guardrails.svg "Segmentera visuell översikt och latensvärden på hög nivå"){width="1000" zoomable="yes"}

### REAL-TIME CUSTOMER DATA PLATFORM &amp; ADOBE TARGET {#adobe-target-latency}

Diagrammet nedan visar förväntade fördröjningsvärden när målgrupper exporteras från Real-Time CDP till [Adobe Target](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en). Klicka på bilden för att se en högupplöst version.

![Exportera till Adobe Target högnivåvisuell översikt.](/help/blueprints/experience-platform/deployment/assets/RTCDP_Target_guardrails.svg "Exportera målgrupper till Adobe Target högnivåvisuella översikter och latensvärden"){width="1000" zoomable="yes"}

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
