---
title: Beslutshantering om navplanen
description: Leverera personaliserade erbjudanden till konsumenter i alla kanaler, inklusive kioskdatorer, agentstödda upplevelser och i e-postmeddelanden och andra utgående leveranser.
solution: Experience Platform, Journey Optimizer
exl-id: 5a386e18-bbac-4216-a35f-0a5016785e4a
source-git-commit: f6c4a0f39acdc177ac23c4314d2f50f793cbf270
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Beslutshantering om navplanen

Om du vill veta mer om beslutshantering kan du läsa produktdokumentationen [HERE](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html) och översikten över beslutshantering [HERE](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-overview.html?lang=en)

Adobe Decision Management är en tjänst som tillhandahålls som en del av Adobe Journey Optimizer. Denna plan beskriver användningsfall och teknisk kapacitet i programmet och ger en djupdykning i de olika arkitektoniska komponenterna och överväganden som utgör beslutsstöd.

Journey Optimizer används för att leverera det bästa erbjudandet och upplevelsen till era kunder vid alla kontaktytor vid rätt tidpunkt. Beslutshantering gör personaliseringen enkel med ett centralt bibliotek med marknadsföringserbjudanden och en beslutsmotor som tillämpar regler och begränsningar på komplexa realtidsprofiler som skapats av Adobe Experience Platform för att hjälpa er att skicka rätt erbjudande till era kunder vid rätt tidpunkt.

Beslutshanteringen kan genomföras på ett av två sätt. Det första är via Adobe Experience Platform nav, som är en central datacenterarkitektur. I naverbjudanden körs, personaliseras och levereras med en fördröjning på över 500 ms. Hub-arkitekturen är därför bäst lämpad för kundupplevelser som inte kräver sekundär fördröjning. Exempel på sådana är erbjudandebeslut som ges för kioskdatorer eller agentassisterade upplevelser som callcenters eller personliga interaktioner. Erbjudanden som infogas i e-postmeddelanden och utgående kampanjer drivs också av navmetoden.

Den andra metoden är via upplevelsen [!DNL [!DNL Edge Network]], som är en globalt distribuerad, geografiskt placerad infrastruktur som kan leverera snabba subsekund- och millisekundsupplevelser. Den slutanvändarupplevelse som utförs av den gränsinfrastruktur som är närmast konsumenternas geografiska plats för att minimera latensen. Beslutshanteringen på Edge är avsedd att betjäna kundupplevelser i realtid, som webb- eller mobilförfrågningar om inkommande personalisering.

Denna plan kommer att omfatta de specifika delarna av beslutsförvaltningen på navet.

Om du vill veta mer om beslutshantering för Edge kan du läsa [beslutshanteringen i den översta](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-edge.html?lang=en)-planen.

## Användningsfall för beslutshantering på navet

* Direktuppspelning använder fall där svarstiden för profilkontext inte är strikt - 15 minuter eller högre latens.
* Personaliserade erbjudanden på kioskdatorer och butiksupplevelser.
* Personaliserade erbjudanden via agentassisterad upplevelse som callcenters eller säljinteraktioner.
* Erbjudanden som ingår i e-post, SMS, push-meddelanden för mobiler eller andra utgående interaktioner.
* Erbjud externa ESP- och meddelandesystem för leverans.
* Flerkanalsmarknadsföring - ger enhetlighet över webben, mobilen, e-post och andra interaktionskanaler via Adobe Journey Optimizer.

>[!IMPORTANT]
>
>För erbjudanden och resor krävs åtkomst till profilen för ytterligare information och sammanhang. Det är viktigt att ta hänsyn till den fördröjning det tar att hämta in data till en profil på navet för att se till att informationen är tillgänglig vid beslut. För scenarier där sammanhanget strömmas eller importeras till en profil och där erbjudandet eller resan måste ha det sammanhanget tillgängligt inom några sekunder eller minuter efter erbjudandebeslutet, är dessa scenarier bäst lämpade för beslutshantering på Edge.

## Arkitektur

<img src="../assets/offers_hub.svg" alt="Referensarkitekturbeslutshantering i den främsta planen" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## Skyddsräcken

* För Journey Optimizer skyddsräcken, se följande [Journey Optimizer-skyddsräcken](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/limitations.html).
* För chefsutkast för beslutshantering, se följande [produktbeskrivning för beslutshantering](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html).

[Garantier och Vägledning för svarstid från slut till slut](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

## Implementeringsmönster

* Implementeras i e-post-, SMS- och utgående kanaler via direkt integrering med [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/offers-e2e.html).
* För server-API-baserad implementering av beslutshantering använder du [besluts-API](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/decisioning-vs-edge-apis.html).
* Använd [API:t för gruppbeslut](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/batch-decisioning-api.html) om du vill implementera batchbaserade beslut för att leverera erbjudanden i grupp till ett meddelandeleveransprogram.
* För Edge-baserade realtidsupplevelser använder du Web/Mobile SDK eller Edge Decisioning API så som beskrivs i [Beslutshanteringen för Edge-planen](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-edge.html?lang=en).

## Relaterad dokumentation

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html)
* [Adobe Journey Optimizer Beslutshantering](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)
* [Adobe Journey Optimizer produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
* [Produktbeskrivning för beslutshantering för Adobe](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html)
