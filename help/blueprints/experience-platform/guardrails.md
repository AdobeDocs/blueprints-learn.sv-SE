---
title: Experience Platform och programskydd
description: Garantier definierar förväntningarna på prestanda och påverkan för komponenter och tjänster i Adobe Experience Platform och program
solution: Experience Platform
thumbnail: null
exl-id: b64cf3e4-cc5d-4984-8a0f-4736d432b8e1
source-git-commit: 75a0f2a77f39a4320dc4c4b0db918879be099dd3
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# Skyddsräcken

Garantierna speglar systembegränsningar, förväntade latenser och prestandaförväntningar för att optimera kundens arkitektur och använda fallissemang och bidra till att säkerställa stabilitet, undvika fel och oväntade resultat.

## Typer av skyddsräcken

| Typ av skyddsräcke | Beskrivning |
|---|---|
| Prestandaskydd (mjuk gräns) | Prestandaskydd är användarbegränsningar som relaterar till omfattningen av dina användningsfall och ger en översikt över förväntade prestanda under normala förhållanden. Om det överskrids kan prestandan försämras och fördröjning uppstå. Prestandaskydd finns dokumenterade i Experience League-dokumenten under respektive lösningsutkast enligt nedan. |
| Statisk gräns (hård gräns) | Det här är begränsningar som framtvingas av systemet och som inte kan överskridas. Statiska begränsningar är vanligtvis bundna och anges i kundkontraktet och i [produktbeskrivningarna](https://helpx.adobe.com/legal/product-descriptions.html). |

>[!NOTE]
>
> Garantier är inte avsedda att vara servicenivåavtal, utan snarare som vägledning för optimala konfigurationer och förväntat systembeteende. Alla skyddsförslag som är system- eller avtalsbegränsningar eller serviceavtal dokumenteras specifikt i kundavtalen och produktbeskrivningarna. Om du är intresserad av att lära dig mer om anpassade begränsningar kontaktar du kundtjänstrepresentanten.

>[!NOTE]
>
> För användningsfall med strikta svarstider eller prestandabehov föreslår Adobe att du diskuterar detaljerna med ditt Adobe kontoteam och din implementeringspartner. Varje kundinställning kan variera mellan olika datainmatningsmönster, profilantal och detaljrikedom, segmentregler och aktiveringskanaler. Därför är det viktigt att du skapar och testar ditt användningssätt för att optimera prestandan och förstå de förväntade prestandaegenskaperna.

## Referensdokumentation för säkerhetsutkast för Adobe Experience Platform och program

Följande sidor innehåller information om säkerhetsutkast för Adobe Experience Platform funktioner, tjänster och program:

**Experience Platform-program**

* [Översikt över Real-Time CDP-skyddsutkast](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/guardrails/overview.html)
* [Customer Journey Analytics målgruppsdelningsplaner](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html#latency)
* [Customer Journey Analytics-åtgärder för dataöverföring](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html#what-is-the-expected-latency-for-analytics-data-on-platform%3F)
* [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html)

**Experience Platform-tjänster**

* [Skyddsförslag för dataöverföring](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html)
* [[!DNL Edge Network] API-stödlinjer](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* [Kundprofil och segmenteringsguardrutor i realtid](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
* [Identitetsgarderobilder](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=en)
* [Frågeserverstänger](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=en)
* [Målaktiveringsguider](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html)

## Latensdiagram från början till slut {#end-to-end-latency}

### Experience Platform Edge Network och Hub - primära observerade latenser {#edge-hub-latencies}

I följande diagram visas den primära kanten och navet som observerats för att vara medveten om när man konstruerar användningsfall för Experience Platform och program.

![Experience Platform [!DNL Edge Network] och navens primära observerade fördröjningar.](/help/blueprints/experience-platform/assets/aep_edge_hub_latency_v1.svg "Experience Platform Edge Network och navens primära observerade fördröjningar"){width="1000" zoomable="yes"}