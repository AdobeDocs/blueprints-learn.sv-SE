---
title: '[!DNL Journey Optimizer] - Reseutkast'
description: Kör utlösta meddelanden och upplevelser med Adobe Experience Platform som ett centralt nav för strömmande data, kundprofiler och segmentering.
solution: Journey Optimizer
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: 0a3ebcbc6029df46bd988cb8f15ecf838f80c3c9
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 4%

---

# [!DNL Journey Optimizer] utkast

Adobe [!DNL Journey Optimizer] är ett molnbaserat program som bygger på Adobe Experience Platform och som möjliggör realtidssamordning av kundresor över flera kanaler. Det har stöd för händelsestyrda triggers, målgruppssegmentering och beslutstjänster för att leverera personaliserade upplevelser via e-post, SMS, push, webb och meddelanden i appen. Det kan integreras med inkommande och utgående system, vilket ger en enhetlig målgruppshantering och ett enhetligt engagemang under hela kundlivscykeln.

Den här planen beskriver programmets tekniska funktioner och ger en djup genomgång av de olika arkitektoniska komponenterna som består av [!DNL Journey Optimizer].

<br>

## Användningsfall

>[!BEGINTABS]
>[!TAB Användningsexempel på resa (händelsestyrd, realtid)]

- **Återställning av övergåenden:** Utlös personliga meddelanden när en användare överger en kundvagn, ett formulär eller en session via e-post, push eller i appen.
- **Ny användarregistrering:** Engagera nya användare direkt efter att de har registrerat sig med nya kontoinställningar, relevanta erbjudanden eller förmåner
- **Transaktionsmeddelanden:** Skicka bekräftelser, aviseringar eller uppdateringar i realtid (t.ex. levererad order, lösenordsåterställning) med händelseutlösare.
- **Sammanhangsberoende målgruppsanpassning:** Kommunicera med användarna för tillfället baserat på deras signaler och plats för att hjälpa till att vägleda och dirigera upplevelsen
- **Sammanhangsbaserad merförsäljning/korsförsäljning:** Leverera personaliserade erbjudanden baserat på profilattribut i realtid och senaste interaktioner.

>[!TAB Användningsexempel för kampanjsamordning (schemalagd, varumärkesinitierad)]

- **Kampanjkampanjer**: Starta flerstegskampanjer för produktlanseringar, säsongserbjudanden och försäljningshändelser.
- **Livscykelmarknadsföring**: Automatisera återkommande kampanjer som födelsedagskalendrar, påminnelser om förnyelse eller milstolpar för lojalitet.
- **Målgruppsbaserade trattpenslar**: Segmentera och flytta målgrupper till strukturerade kampanjer baserat på affärslogik eller CRM-attribut.
- **Nyhetsbrev och innehållsdistribution**: Schemalägg och leverera personaliserat innehåll till målgrupper via e-post och mobiler.
- **Återengagemangskampanjer**: Identifiera vilande användare och återintroducera dem i engagemangsflöden baserat på inaktivitetströsklar.

>[!ENDTABS]

<br>

## Arkitektur

<img src="images/ajo-architecture.svg" alt="Referensarkitektur Adobe Journey Optimizer Blueprint" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Scenarier med blå text

| Scenario | Beskrivning |
| :-- | :-- |
| [Resor](journey-optimizer-journeys.md) | AJO Journeys i Adobe Journey Optimizer är automatiserade, personaliserade kundupplevelser som triggas av händelser i realtid eller målgruppssegment, vilket gör att marknadsförarna kan leverera relevanta meddelanden i olika kanaler som e-post, SMS och push-meddelanden. |
| [Kampanjsamordning](journey-optimizer-campaigns.md) | Med AJO Campaign-samordning kan marknadsförarna utforma och genomföra personaliserade flerkanalskampanjer med realtidsdata och målgruppsinsikter. Det har stöd för dynamisk målgruppsanpassning, meddelandeleverans och reselogik för att optimera kundengagemanget i e-post, SMS, push och anpassade kanaler. | |

<br>

## Integrationsmönster

| Integrering | Beskrivning | Tekniska överväganden |
| :-- | :-- | :-- |
| [Meddelanden från tredje part](3rd-party-messaging.md) | Visar hur Adobe [!DNL Journey Optimizer] kan integreras med externa meddelandeplattformar för att samordna och leverera personaliserad kundkommunikation. | <ul><li>Tredjepartssystemet måste ha stöd för **innehavartoken-autentisering**</li><li>**Statiska IP-adresser stöds inte** på grund av multi-tenant-arkitekturen.</li><li>Observera **API-tariffgränser** på tredjepartssystem. Kunder kan behöva köpa ytterligare kapacitet för att hantera trafik från **Adobe Journey Optimizer**.</li><li>**Beslutshantering** stöds inte i meddelandenyttolaster eller leveranslogik.</li></ul> |
| [[!DNL Journey Optimizer] med Adobe Campaign v8](../campaign-v8/ajo-and-campaign-v8.md) | Visar hur Adobe [!DNL Journey Optimizer] kan integreras med Adobe Campaign v8:s transaktionsmeddelandefunktioner för att utföra slutlig meddelandeleverans. | <ul><li>Det finns ingen begränsning för meddelanden. Gräns för 4 000 meddelanden per 5 minuter.</li><li>Stöder endast händelseinitierade resor</li><li>Beslutshantering stöds inte i meddelanden som skickas av Campaign</li></ul> |

<br>

## Förutsättningar

Adobe [!DNL Experience Platform]:

- Scheman och datauppsättningar måste konfigureras i systemet innan du kan konfigurera [!DNL Journey Optimizer]-datakällor
- För XDM Experience Event-klassbaserade scheman lägger du till fältgruppen Orchestration-händelseID när du vill att en händelse som inte är en regelbaserad händelse ska aktiveras
- För XDM-scheman baserade på klassen Individual Profile lägger du till fältgruppen &#39;Profiltestinformation&#39; för att kunna läsa in testprofiler som ska användas med [!DNL Journey Optimizer]

<br>

E-post:

- Måste ha en underdomän klar att användas för att skicka meddelanden
- Underdomänen kan antingen delegeras helt till Adobe (rekommenderas) eller CNAME kan användas för att peka på Adobe-specifika DNS-servrar (anpassad)
- Google TXT-post krävs för varje underdomän för att säkerställa god levererbarhet

<br>

Mobilpush:

- Kunden måste ha en mobilutvecklare tillgänglig för att kunna bygga appen
- Adobe Experience Platform Mobile SDK

<br>

## Skyddsräcken

[[!DNL Journey Optimizer] Produktlänk för säkerhetsutkast](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails.html)

[Garantier och Vägledning för svarstid från slut till slut](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

## Relaterad dokumentation

- [[!DNL Experience Platform] dokumentation](https://experienceleague.adobe.com/docs/experience-platform.html)
- [[!DNL Experience Platform] Dokumentation för taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv)
- [[!DNL Experience Platform Mobile SDK] dokumentation](https://experienceleague.adobe.com/docs/mobile.html)
- [[!DNL Journey Optimizer] dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html)
- [[!DNL Journey Optimizer] produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)