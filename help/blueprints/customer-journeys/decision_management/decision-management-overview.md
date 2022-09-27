---
title: Översikt över beslutshantering
description: Leverera personaliserade erbjudanden på alla kundresor.
solution: Experience Platform, Journey Optimizer
exl-id: 1bc9335c-5321-4d0c-939e-4f402e2e8f51
source-git-commit: b3d4e89c7e4170ffee2cc1776ffa26d2e0ce79e6
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 0%

---

# Journey Optimizer - beslutsöversikt

Mer information om beslutshantering finns i produktdokumentationen [HÄR](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)

Adobe Decision Management är en tjänst som tillhandahålls som en del av Adobe Journey Optimizer. Denna plan beskriver användningsfall och teknisk kapacitet i programmet och ger en djupdykning i de olika arkitektoniska komponenterna och överväganden som utgör beslutsstöd.

Journey Optimizer används för att leverera det bästa erbjudandet och upplevelsen till era kunder vid alla kontaktytor vid rätt tidpunkt. Beslutshantering gör personaliseringen enkel med ett centralt bibliotek med marknadsföringserbjudanden och en beslutsmotor som tillämpar regler och begränsningar på komplexa realtidsprofiler som skapats av Adobe Experience Platform för att hjälpa er att skicka rätt erbjudande till era kunder vid rätt tidpunkt.

Beslutsledningskapaciteten består av två huvudkomponenter:

* Det centraliserade erbjudandebiblioteket, som är gränssnittet där du skapar och hanterar de olika elementen som dina erbjudanden består av, och definierar deras regler och begränsningar.
* Beslutsmotorn för erbjudandet som utnyttjar Adobe Experience Platform-data och kundprofiler i realtid, tillsammans med erbjudandebiblioteket, för att välja rätt tid, kunder och kanaler som erbjudandena ska levereras till.

<img src="../assets/offers_overview.png" alt="Beslutshantering" style="width:100%; border:1px solid #4a4a4a" />

Beslutshanteringen kan användas på ett av två sätt, på kanten eller via navet. Var och en av dessa metoder har en specifik uppsättning gränssnitt och protokoll för att köra tjänsten enligt beskrivningen i respektive ritning som det hänvisas till nedan. Ytterligare information finns också i beslutsledningens dokumentation [HÄR](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery-api/decisioning-vs-edge-apis.html).

## Beslutshantering på navet

Det första är via Adobe Experience Platform nav, som är en central datacenterarkitektur. I naverbjudanden körs, personaliseras och levereras med en fördröjning på över 500 ms. Hub-arkitekturen är därför bäst lämpad för kundupplevelser som inte kräver sekundär fördröjning. Exempel på sådana är erbjudandebeslut som ges för kioskdatorer eller agentassisterade upplevelser som callcenters eller personliga interaktioner. Erbjudanden som infogas i e-postmeddelanden, SMS-meddelanden eller push-meddelanden och andra utgående kampanjer drivs också av navmetoden. Om du vill veta mer om beslutshantering för navet kan du läsa [Beslutshantering på navet](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-hub.html?lang=en) utkast.

* Erbjudandets behörighet kan fungera mot kundprofilen i realtid, inklusive alla attribut och upplevelsehändelser

### Använd ärenden för beslutshantering på navet

* Personaliserade erbjudanden på kioskdatorer och butiksupplevelser.
* Personaliserade erbjudanden via agentassisterad upplevelse som callcenters eller säljinteraktioner.
* Erbjudanden som ingår i e-post, SMS eller andra utgående interaktioner.
* Flerkanalsmarknadsföring - ger enhetlighet över webben, mobilen, e-post och andra interaktionskanaler via Adobe Journey Optimizer.

### Beslutsledning om tekniska överväganden

* Begäranden per sekund = 2000.
* Svarstid &lt; 500 ms.
* Tillgång till en fullständig kundprofil i realtid, inklusive målgruppsmedlemskap, attribut och upplevelsehändelser.

## Beslutsfattare i utkanten

Den andra metoden är via Experience Edge-nätverket, som är en globalt spridd, geografiskt belägen infrastruktur som kan leverera snabba subsekundsupplevelser och millisekundsupplevelser. Den slutanvändarupplevelse som utförs av den gränsinfrastruktur som är närmast konsumenternas geografiska plats för att minimera latensen. Beslutshanteringen på Edge är utformad för att leverera konsumentupplevelser i realtid, som webb- eller mobilförfrågningar om inkommande personalisering. Om du vill veta mer om beslutshantering på Edge-nivå kan du läsa [Beslutsfattare i utkanten](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-edge.html?lang=en) utkast.

### Använd fall för beslutshantering i utkanten

* Onlinepersonalisering via webb eller mobilupplevelser.
* Flerkanalsmarknadsföring - ger enhetlighet över webben, mobilen, e-post och andra interaktionskanaler via Adobe Journey Optimizer.

### Beslutsfattare om de tekniska aspekterna

* Begäranden per sekund = 5000.
* Svarstid &lt; 250 ms.
* Tillgång till Edge-realtidsprofil. Endast kantprojicerade målgrupper och profilattribut är tillgängliga i profilen.
* Om personalisering krävs i förstagångsupplevelser kommer navet att vara idealiskt eftersom den fullständiga profilen är tillgänglig. Kantprofilen måste synkroniseras från navet för första gången. Den allra första upplevelsen från kanten kommer därför inte att inkludera tidigare överförda profildata till navet.

## Relaterad dokumentation

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html)
* [Adobe Journey Optimizer Beslutshantering](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)
* [Adobe Journey Optimizer produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
* [Produktbeskrivning för beslutsledning i Adobe](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html)
