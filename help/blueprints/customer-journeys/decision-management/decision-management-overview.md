---
title: Beslutsledningsplaner
description: Leverera personaliserade erbjudanden på alla kundresor.
solution: Experience Platform, Journey Optimizer
exl-id: 1bc9335c-5321-4d0c-939e-4f402e2e8f51
source-git-commit: 0a3ebcbc6029df46bd988cb8f15ecf838f80c3c9
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# Journey Optimizer - Beslutsledningsplaner

Se följande dokumentation för [Beslutshantering](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)

Se följande dokumentation för skyddsförslag avseende beslutsförvaltning. [Beslutshanteringsriktlinjer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails#decision-management.html)

Adobe Decision Management är en tjänst som tillhandahålls som en del av Adobe Journey Optimizer. Denna plan beskriver användningsfall och teknisk kapacitet i programmet och ger en djupdykning i de olika arkitektoniska komponenterna och överväganden som utgör beslutsstöd.

Journey Optimizer används för att leverera det bästa erbjudandet och upplevelsen till era kunder vid alla kontaktytor vid rätt tidpunkt. Beslutshantering förenklar personaliseringen med ett centralt bibliotek med marknadsföringserbjudanden och en beslutsmotor som tillämpar regler och begränsningar på realtidsprofiler som skapats av Adobe Experience Platform. På så sätt kan ni enkelt skicka rätt erbjudande till kunderna vid rätt tidpunkt.

Beslutsledningskapaciteten består av två huvudkomponenter:

* Det centraliserade erbjudandebiblioteket, som är gränssnittet där du skapar och hanterar de olika elementen som dina erbjudanden består av, och definierar deras regler och begränsningar.
* Beslutsmotorn för erbjudandet som utnyttjar Adobe Experience Platform-data och kundprofiler i realtid, tillsammans med erbjudandebiblioteket, för att välja rätt tid, kunder och kanaler som erbjudandena ska levereras till.

<img src="images/offers_overview.png" alt="Beslutshantering" style="width:100%; border:1px solid #4a4a4a" />

Beslutshanteringen kan användas på ett av två sätt, på kanten eller via navet. Var och en av dessa metoder har en specifik uppsättning gränssnitt och protokoll för att utföra tjänsten enligt beskrivningen i respektive ritning som det hänvisas till nedan. Ytterligare information finns också i [beslutsstyrningsdokumentationen](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery-api/decisioning-vs-edge-apis.html).

## Beslutshantering på navet

Det första är via Adobe Experience Platform nav, som är en central datacenterarkitektur. Hubbarkitekturen är bäst lämpad för kundupplevelser som inte kräver låg latens och hög genomströmning, men som kräver en mer detaljerad bild av kundprofilen. Exempel på sådana är erbjudandebeslut som ges för kioskdatorer eller agentassisterade upplevelser som callcenters eller personliga interaktioner. Erbjudanden som infogas i e-postmeddelanden, SMS-meddelanden eller push-meddelanden och andra utgående kampanjer drivs också av navmetoden. Mer information om beslutshantering för navet finns i [beslutshanteringen för navet](decision-management-hub.md).

* Erbjudandets behörighet kan fungera mot kundprofilen i realtid, inklusive alla attribut och upplevelsehändelser

### Användningsfall för beslutshantering på navet

* Personaliserade erbjudanden på kioskdatorer och butiksupplevelser.
* Personaliserade erbjudanden via agentassisterad upplevelse som callcenters eller säljinteraktioner.
* Erbjudanden som ingår i e-post, SMS eller andra utgående interaktioner.
* Flerkanalsmarknadsföring - ger enhetlighet över webben, mobilen, e-post och andra interaktionskanaler via Adobe Journey Optimizer.

### Beslutsledning om tekniska överväganden

* Tillgång till en fullständig kundprofil i realtid, inklusive målgruppsmedlemskap, attribut och upplevelsehändelser.

## Beslutsfattare i utkanten

Den andra metoden är via upplevelsen [!DNL Edge Network], som är en globalt distribuerad, geografiskt placerad infrastruktur som kan leverera snabba, subsekundära och millisekundsupplevelser. Den slutanvändarupplevelse som utförs av den gränsinfrastruktur som är närmast konsumenternas geografiska plats för att minimera latensen. Beslutshanteringen på Edge är avsedd att betjäna kundupplevelser i realtid, som webb- eller mobilförfrågningar om inkommande personalisering. Om du vill veta mer om beslutshantering för Edge kan du läsa [beslutshanteringen i den översta](decision-management-edge.md)-planen.

### Användningsexempel för beslutshantering i utkanten

* Onlinepersonalisering via webb eller mobilupplevelser.
* Flerkanalsmarknadsföring - ger enhetlighet över webben, mobilen, e-post och andra interaktionskanaler via Adobe Journey Optimizer.

### Beslutsfattare om de tekniska aspekterna

* Tillgång till Edge-realtidsprofil. Endast kantprojicerade målgrupper och profilattribut är tillgängliga i profilen.

## Relaterad dokumentation

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html)
* [Adobe Journey Optimizer Beslutshantering](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)
* [Adobe Journey Optimizer produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
* [Produktbeskrivning för Adobe-beslutshantering](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html)
