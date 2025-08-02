---
title: Beslutshantering om Edge-planen
description: Leverera personaliserade erbjudanden till konsumenter i alla kanaler, även i realtid via webben och mobilupplevelser.
solution: Experience Platform, Journey Optimizer
exl-id: 31e5f624-5578-49e1-ab92-5cabd596a632
source-git-commit: 75a0f2a77f39a4320dc4c4b0db918879be099dd3
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# Journey Optimizer - [!DNL Decision Management] på Edge-ritningen

[!DNL Decision Management] är en tjänst som tillhandahålls som en del av [!DNL Journey Optimizer]. Denna plan beskriver användningsfall och teknisk kapacitet i programmet och ger en djupdykning i de olika arkitektoniska komponenterna och överväganden som utgör beslutsstöd.

>[!MORELIKETHIS]
>
>Mer information om [!DNL Decision Management] finns i översikten [för utkast](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-overview.html?lang=sv-SE) eller i [produktdokumentationen](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=sv-SE).

[!DNL Decision Management] kan distribueras på ett av två sätt. Det första är via [!DNL Experience Platform]-hubben, som är en enda datacenterarkitektur. I navet-metoden utförs, personaliseras och levereras med andra fördröjning. Hub-arkitekturen är därför bäst lämpad för kundupplevelser som inte kräver en sekundär fördröjning. Exempel på sådana är erbjudandebeslut som ges för kioskdatorer eller agentassisterade upplevelser som callcenters eller personliga interaktioner.

Den andra metoden är via Experience Platform [!DNL Edge Network], som är en globalt distribuerad, geografiskt belägen infrastruktur som kan leverera snabba, subsekundära och millisekundsupplevelser. Den slutanvändarupplevelse som Edge-infrastrukturen närmast konsumenterna kör för att minimera latensen. [!DNL Decision Management] på Edge är utformat för att leverera konsumentupplevelser i realtid. Det kan vara upplevelser som webb- eller mobilförfrågningar om inkommande personalisering.

Denna plan kommer att omfatta de specifika delarna av beslutsförvaltningen på Edge.

Mer information om beslutshantering för navet finns i [beslutshanteringen för navet](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-hub.html?lang=sv-SE).

## Användningsexempel för beslutshantering i utkanten

* Direktuppspelning använder fall där svarstiden för profilkontext är lägre än 15 minuters fördröjning och körning av beslutshantering är mindre än 15 sekunder.
* Onlinepersonalisering via webb eller mobilupplevelser.
* Flerkanalsmarknadsföring - ger enhetlighet över webben, mobilen, e-post och andra interaktionskanaler via Adobe Journey Optimizer.

## Arkitektur

<img src="../assets/offers_edge.svg" alt="Referensarkitekturbeslutshantering i den främsta planen" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## Integreringsmönster

| Integrering | Beskrivning |
| :-- | :--- |
| [Beslutshantering med Adobe Target](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html?lang=sv-SE) | Beslutshantering kan integreras med Adobe Target så att erbjudandena kan testas och levereras som Target-upplevelser. |

## Skyddsräcken

* För Journey Optimizer skyddsräcken, se följande [Journey Optimizer-skyddsräcken](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/limitations.html?lang=sv-SE).

* För chefsutkast för beslutshantering, se följande [produktbeskrivning för beslutshantering](https://helpx.adobe.com/se/legal/product-descriptions/offer-decisioning-app-service.html).

[Garantier och Vägledning för svarstid från slut till slut](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/guardrails.html?lang=sv-SE)

## Relaterad dokumentation

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=sv-SE)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=sv-SE)
* [Adobe Journey Optimizer Beslutshantering](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=sv-SE)
* [Adobe Journey Optimizer produktbeskrivning](https://helpx.adobe.com/se/legal/product-descriptions/adobe-journey-optimizer.html)
* [Produktbeskrivning för Adobe-beslutshantering](https://helpx.adobe.com/se/legal/product-descriptions/offer-decisioning-app-service.html)
