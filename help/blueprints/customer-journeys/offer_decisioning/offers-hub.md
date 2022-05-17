---
title: offer decisioning på navet
description: Leverera personaliserade erbjudanden till konsumenter i alla kanaler, inklusive kioskdatorer, agentstödda upplevelser och i e-postmeddelanden och andra utgående leveranser.
solution: Experience Platform, Journey Optimizer
exl-id: 5a386e18-bbac-4216-a35f-0a5016785e4a
source-git-commit: 011f5b247ccd606348b4cbb4210218f28eddbd4c
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 0%

---

# Journey Optimizer - Offer decisioning på navet

Mer information om beslutshantering finns i produktdokumentationen [HÄR](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html) och Offera decisioningen [HÄR](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-overview.html)

Adobe Decision Management är en tjänst som tillhandahålls som en del av Adobe Journey Optimizer. Denna plan beskriver användningsexempel och tekniska funktioner i programmet och ger en djupdykning i de olika arkitektoniska komponenterna och överväganden som utgör Offer decisioning.

Journey Optimizer används för att leverera det bästa erbjudandet och upplevelsen till era kunder vid alla kontaktytor vid rätt tidpunkt. offer decisioning förenklar personaliseringen med ett centralt bibliotek med marknadsföringserbjudanden och en beslutsmotor som tillämpar regler och begränsningar på komplexa realtidsprofiler som skapats av Adobe Experience Platform för att hjälpa er att skicka rätt erbjudande till era kunder vid rätt tidpunkt.

Beslutshanteringen kan genomföras på ett av två sätt. Det första är via Adobe Experience Platform nav, som är en central datacenterarkitektur. I naverbjudanden körs, personaliseras och levereras med en fördröjning på över 500 ms. Hub-arkitekturen är därför bäst lämpad för kundupplevelser som inte kräver sekundär fördröjning. Exempel på sådana är erbjudandebeslut som ges för kioskdatorer eller agentassisterade upplevelser som callcenters eller personliga interaktioner. Erbjudanden som infogas i e-postmeddelanden och utgående kampanjer drivs också av navmetoden.

Den andra metoden är via Experience Edge-nätverket, som är en globalt spridd, geografiskt belägen infrastruktur som kan leverera snabba subsekundsupplevelser och millisekundsupplevelser. Den slutanvändarupplevelse som utförs av den gränsinfrastruktur som är närmast konsumenternas geografiska plats för att minimera latensen. Beslutshanteringen på Edge är utformad för att leverera konsumentupplevelser i realtid, som webb- eller mobilförfrågningar om inkommande personalisering.

Denna plan kommer att omfatta de specifika delarna av beslutsförvaltningen på navet.

Om du vill veta mer om beslutshantering på Edge-nivå kan du läsa [Beslutsfattare i utkanten](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-edge.html) utkast.

## Använd ärenden för beslutshantering på navet

* Personaliserade erbjudanden på kioskdatorer och butiksupplevelser.
* Personaliserade erbjudanden via agentassisterad upplevelse som callcenters eller säljinteraktioner.
* Erbjudanden som ingår i e-post, SMS, push-meddelanden för mobiler eller andra utgående interaktioner.
* Erbjud externa ESP- och meddelandesystem för leverans.
* Flerkanalsmarknadsföring - ger enhetlighet över webben, mobilen, e-post och andra interaktionskanaler via Adobe Journey Optimizer.

<br>

## Arkitektur

<img src="../assets/offers_hub.svg" alt="Referensarkitekturens Offer decisioning på den avancerade ritningen" style="width:100%; border:1px solid #4a4a4a" />

<br>

## Förutsättningar

Adobe Experience Platform

* Scheman och datauppsättningar måste konfigureras i systemet innan du kan konfigurera Journey Optimizer-datakällor
* För Experience Event-klassbaserade scheman lägger du till fältgruppen &#39;Orchestration eventID&#39; när du vill att en händelse som inte är en regelbaserad händelse ska aktiveras
* För enskilda profilklassbaserade scheman lägger du till fältgruppen Profiltestinformation för att kunna läsa in testprofiler som ska användas med Journey Optimizer

<br>

## Guardrails

* För Journey Optimizer skyddsräcken, se följande [Journey Optimizer Guardrails](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/limitations.html).
* För skyddsräcken för Offera decisioningar, se följande [Produktbeskrivning för offer decisioning](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html).


### Dataöverföringsskydd

<img src="../assets/aep-data-ingestion-details-latency.svg" alt="Referensarkitektur Journey Optimizer - utkast" style="width:80%; border:1px solid #4a4a4a" />

<br>

### Aktiveringsskydd

<img src="../assets/ajo-activation-details-latency.svg" alt="Referensarkitektur Journey Optimizer - utkast" style="width:80%; border:1px solid #4a4a4a" />

<br>

## Implementeringsmönster

* Implementeras i e-post, SMS och utgående kanaler via direkt integrering med [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/offers-e2e.html).
* För server-API-baserad implementering av Offer decisioning kan du använda [Besluts-API](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/decisioning-vs-edge-apis.html).
* Vid implementering av batchbaserade beslut att leverera större mängder av erbjudanden till ett meddelandeleveransprogram använder du [API för gruppbeslut](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/batch-decisioning-api.html).
* För Edge-baserade realtidsupplevelser använder du Web/Mobile SDK eller Edge Decisioning API enligt riktlinjerna i [offer decisioning på Edge-ritningen](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-edge.html).
<br>

## Implementeringssteg

### Adobe Experience Platform

#### Schema/datauppsättningar

1. [Konfigurera enskilda profiler, upplevelsehändelser och scheman för flera enheter](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) i Experience Platform, baserat på kunddata.
1. [Skapa datauppsättningar](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) i Experience Platform för data som ska importeras.
1. [Lägg till etiketter för dataanvändning](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html) i Experience Platform till datauppsättningen för styrning.
1. [Skapa profiler](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html) som tillämpar styrning av destinationer.

#### Profil/identitet

1. [Skapa alla kundspecifika namnutrymmen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Lägga till identiteter i scheman](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Aktivera scheman och datauppsättningar för profilen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Ställ in sammanfogningsprinciper](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html) för olika vyer av [!UICONTROL Kundprofil i realtid] (valfritt).
1. Skapa segment för reseanvändning.

#### Källor/mål

1. [Infoga data i Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) med direktuppspelnings-API:er och källanslutningar.

## Relaterad dokumentation

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html)
* [Adobe Journey Optimizer Beslutshantering](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)
* [Adobe Journey Optimizer produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
* [Produktbeskrivning för Adobe Offer decisioning](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html)
