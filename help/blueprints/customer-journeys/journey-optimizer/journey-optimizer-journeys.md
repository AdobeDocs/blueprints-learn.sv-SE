---
title: '[!DNL Journey Optimizer] - utlöst meddelanden och Adobe Experience Platform Blueprint'
description: Kör utlösta meddelanden och upplevelser med Adobe Experience Platform som ett centralt nav för strömmande data, kundprofiler och segmentering.
solution: Journey Optimizer
source-git-commit: 0a3ebcbc6029df46bd988cb8f15ecf838f80c3c9
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 7%

---

# [!DNL Journey Optimizer] - Reseutkast

Adobe Journey Optimizer Journeys är händelsestyrda arbetsflöden i realtid som levererar personaliserade flerstegsupplevelser baserade på individuella kundbeteenden. De har stöd för ett brett urval av kanaler - inklusive e-post, SMS, push-meddelanden, meddelanden i appen, kodbaserade upplevelser och anpassade API-baserade integreringar som gör att varumärken kan engagera kunder i deras kontaktytor.

<br>

## Arkitektur

<img src="images/ajo-journeys-architecture.svg" alt="Referensarkitektur Adobe Journey Optimizer - Journeys Blueprint" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Arkitektur för resor

- **Freshness för profil**: AJO Journeys förlitar sig på uppdateringar i realtid av kundprofilen. Kontrollera att datakällor som matas in i Adobe Experience Platform (AEP) är konfigurerade för låg fördröjning för att behålla profilens precision.
- **Hantering av skalbara händelser:** Kontrollera att infrastrukturen kan hantera stora volymer av utlösare för resan och meddelandeleverans.
- **Modulär integrering:** Designa API:er och anpassade åtgärder för att ansluta AJO till externa system för dynamisk personalisering.
- **Identitetsupplösning**: Korrekt sammanfogning av kundidentiteter mellan enheter och kanaler är avgörande. Felaktiga identiteter kan leda till trasiga eller felriktade resor.
- **Timing för segmentkvalificering**: Målgruppsbaserade resor är beroende av segmentmedlemskap. Förstå hur ofta segment utvärderas och hur den tidpunkten påverkar reseinträde och personalisering.
- **Villkor för reseanmälan**: Profilerna måste uppfylla specifika villkor för att kunna gå in på en resa. Dessa förhållanden bör vara noga utformade för att undvika oavsiktliga undantag eller överlappningar.
- **Målgruppsutvärdering och fördröjning**: Läs målgruppsstegen beror på segmentutvärderingar i Adobe Experience Platform, som kanske inte sker i realtid. Arkitektresor med medvetenhet om utvärderingsfrekvens och tidsfördröjning för att undvika förseningar i målgruppsklassificeringen och säkerställa snabb personalisering.

<br>

## Skyddsräcken

[[!DNL Journey Optimizer] Produktlänk för säkerhetsutkast](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails.html)

[Garantier och Vägledning för svarstid från slut till slut](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=sv-SE)

<br>

## Relaterad dokumentation

- [[!DNL Experience Platform] dokumentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=sv-SE)
- [[!DNL Experience Platform] Dokumentation för taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv)
- [[!DNL Experience Platform Mobile SDK] dokumentation](https://experienceleague.adobe.com/docs/mobile.html?lang=sv-SE)
- [[!DNL Journey Optimizer] dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=sv-SE)
- [[!DNL Journey Optimizer] produktbeskrivning](https://helpx.adobe.com/se/legal/product-descriptions/adobe-journey-optimizer.html)