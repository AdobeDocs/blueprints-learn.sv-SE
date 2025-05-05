---
title: Experience Platform och programskydd
description: Garantier definierar förväntningarna på prestanda och påverkan för komponenter och tjänster i Adobe Experience Platform och program
solution: Experience Platform
thumbnail: null
exl-id: b64cf3e4-cc5d-4984-8a0f-4736d432b8e1
source-git-commit: a5d127c2a9e18ebbf25012475b9f474c07575362
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 1%

---


# Skyddsräcken

Garantierna speglar systembegränsningar, förväntade latenser och prestandaförväntningar för att optimera kundens arkitektur och använda fallissemang och bidra till att säkerställa stabilitet, undvika fel och oväntade resultat.

## Typer av skyddsräcken

| Typ av skyddsräcke | Beskrivning |
|---|---|
| Prestandaskydd (mjuk gräns) | Prestandaskydd är användarbegränsningar som relaterar till omfattningen av dina användningsfall och ger en översikt över förväntade prestanda under normala förhållanden. Om det överskrids kan prestandan försämras och fördröjning uppstå. Prestandaskydd finns dokumenterade i Experience League-dokumenten under respektive lösnings skyddsavsnitt enligt nedan. |
| Statisk gräns (hård gräns) | Det här är begränsningar som framtvingas av systemet och som inte kan överskridas. Statiska begränsningar är vanligtvis bundna och anges i kundkontraktet och i [produktbeskrivningarna](https://helpx.adobe.com/se/legal/product-descriptions.html). |

>[!NOTE]
>
> Garantier är inte avsedda att vara servicenivåavtal, utan snarare som vägledning för optimala konfigurationer och förväntat systembeteende. Alla skyddsförslag som är system- eller avtalsbegränsningar eller serviceavtal dokumenteras specifikt i kundavtalen och produktbeskrivningarna. Om du är intresserad av att lära dig mer om anpassade begränsningar kontaktar du kundtjänstrepresentanten.

>[!NOTE]
>
> För användningsfall med strikta svarstider eller prestationsbehov föreslår Adobe att ni diskuterar detaljerna med ert kontoteam på Adobe och er implementeringspartner. Varje kundinställning kan variera mellan olika datainmatningsmönster, profilantal och detaljrikedom, segmentregler och aktiveringskanaler. Därför är det viktigt att du skapar och testar ditt användningssätt för att optimera prestandan och förstå de förväntade prestandaegenskaperna.

## Referensdokumentation för säkerhetsutkast för Adobe Experience Platform och program

Följande sidor innehåller information om säkerhetsutkast för Adobe Experience Platform funktioner, tjänster och program:

**Experience Platform-program**

* [Översikt över Real-Time CDP-skyddsutkast](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/guardrails/overview.html?lang=sv-SE)
* [Customer Journey Analytics för målgruppsdelning](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=sv-SE#latency)
* [Skyddsguider för dataöverföring i Customer Journey Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=sv-SE#what-is-the-expected-latency-for-analytics-data-on-platform%3F)
* [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=sv-SE)

**Experience Platform-tjänster**

* [Skyddsförslag för dataöverföring](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html?lang=sv-SE)
* [[!DNL Edge Network] API-stödlinjer](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html?lang=sv-SE)
* [Kundprofil och segmenteringsguardrutor i realtid](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=sv-SE)
* [Identitetsgarderobilder](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=sv-SE)
* [Frågeserverstänger](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=sv-SE)
* [Målaktiveringsguider](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=sv-SE)

## Latensdiagram från början till slut {#end-to-end-latency}

### Experience Platform Edge Network och navens primära observerade latenser {#edge-hub-latencies}

I följande diagram visas den primära kanten och hubben som observerats för att vara medveten om när man konstruerar användningsfall på Experience Platform och program.

![Experience Platform [!DNL Edge Network] och primära latenser för navet som observerats.](/help/blueprints/experience-platform/deployment/assets/aep_edge_hub_latency_v1.svg "Experience Platform Edge Network och primära latenser som observerats via hubb"){width="1000" zoomable="yes"}

### Intag av data {#data-ingestion}

I diagrammet nedan visas förväntade värden för fördröjning av dataöverföring via [direktuppspelningsuppläsning](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=sv-SE) och [batchförtäring](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/getting-started.html?lang=sv-SE) när data hämtas till Real-Time CDP. Klicka på bilden för att se en högupplöst version.

![Översikt över dataöverföring på hög nivå.](/help/blueprints/experience-platform/deployment/assets/aep_data_flow_guardrails.svg "Värden för visuell överblick och fördröjning på hög nivå för dataöverföring"){width="1000" zoomable="yes"}

### Segmentering {#segmentation}

Diagrammet nedan visar förväntade fördröjningsvärden när du arbetar med målgrupper i [Real-Time CDP segmenteringstjänst](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=sv-SE). Klicka på bilden för att se en högupplöst version.

![Översikt över segmentering på hög nivå.](/help/blueprints/experience-platform/deployment/assets/segmentation_guardrails.svg "Segmentering av visuella översikter och latensvärden på hög nivå"){width="1000" zoomable="yes"}

### Real-time Customer Data Platform &amp; [!DNL Edge Network] {#adobe-edge-latency}

Diagrammet nedan visar förväntade fördröjningsvärden när [!DNL Edge Network] utnyttjas, till exempel för att återanvända RTCDP-målgrupper i [Adobe Target](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=sv-SE). Klicka på bilden för att se en högupplöst version.

![Adobe Edge Network och Experience Platform - en överblick på hög nivå.](/help/blueprints/experience-platform/deployment/assets/RTCDP_Edge_guardrails.svg "Exporterar målgrupper till Adobe Target visuella översikt och fördröjning på hög nivå"){width="1000" zoomable="yes"}

### Customer Journey Analytics {#customer-journey-analytics}

Diagrammet nedan visar förväntade fördröjningsvärden när du arbetar med [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=sv-SE). Klicka på bilden för att se en högupplöst version.

![Arbeta med högnivåvisuell översikt på Customer Journey Analytics.](/help/blueprints/experience-platform/deployment/assets/CJA_guardrails.svg "Arbeta med högnivåvisuella översikter och latensvärden för Customer Journey Analytics"){width="1000" zoomable="yes"}

### Journey Optimizer {#journey-optimizer}

I diagrammet nedan visas förväntade fördröjningsvärden när du arbetar med [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=sv-SE). Klicka på bilden för att se en högupplöst version.

![Arbeta med Adobe Journey Optimizer visuella översikt på hög nivå.](/help/blueprints/experience-platform/deployment/assets/AJO_guardrails.svg "Arbeta med Adobe Journey Optimizer högnivåvisuella översikter och latensvärden"){width="1000" zoomable="yes"}