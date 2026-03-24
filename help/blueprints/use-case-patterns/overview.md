---
title: Använd fallmönster
description: Läs om användningsmönstren för implementering av Adobe Experience Platform och tillämpningar för att uppnå viktiga affärsmål.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
doc-type: overview-page
exl-id: 58caa6ad-0d1c-4290-9614-c68c9c9028bb
source-git-commit: 27f7e230982807ec70ca96af7f737944a6588f27
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# Använd fallmönster

Använd fallmönster för att definiera repeterbara implementeringsmetoder för Adobe Experience Platform och program. Varje mönster beskriver en specifik funktion, funktionskedjan som levererar den, de program som ingår och de [viktiga affärsmålen](/help/blueprints/business-objectives/overview.md) som stöds.

Använd tabellerna nedan för att hitta det mönster som passar dina implementeringsbehov och följ sedan länken till den fullständiga implementeringsreferensen, inklusive alternativ, faser, beslutsvägledning och Experience League-dokumentation.

## Målgruppsuppbyggnad och -aktivering

Följande mönster hjälper er att bygga, utvärdera och aktivera målgruppssegment över olika kanaler och destinationer.

| Mönster | Primär kapacitet | Kärnlösningar |
| --- | --- | --- |
| [Målgruppsaktivering](audience-building-activation/audience-activation-to-destinations.md) | Utvärdera och publicera målgruppssegment till externa destinationer för målinriktning eller undertryckning | [!DNL Real-Time CDP] |
| [Målgrupp Collaboration](audience-building-activation/audience-collaboration-segment-match.md) | Dela och matcha målgruppssegment i sandlådor eller organisationer med segmentmatchning | [!DNL Real-Time CDP], [!DNL Experience Platform] |
| [Vidarebefordran av händelser](audience-building-activation/event-forwarding.md) | Vidarebefordra händelsedata i realtid som samlats in via Edge Network till destinationer utanför Adobe | [!DNL Experience Platform] (Edge Network, vidarebefordran av händelser) |
| [B2B-målgruppsaktivering](audience-building-activation/b2b-audience-activation.md) | Aktivera kontobaserade B2B-målgrupper över webb-, e-post- och annonskanaler | [!DNL Real-Time CDP] B2B edition |

## Personalisering

Följande mönster levererar skräddarsydda upplevelser till kända och okända besökare på webben och i appar.

| Mönster | Primär kapacitet | Kärnlösningar |
| --- | --- | --- |
| [Anonym webbanpassning för besökare](personalization/anonymous-visitor-web-personalization.md) | Leverera personaliserat innehåll baserat på sessionsbeteendesignaler för oidentifierade besökare | [!DNL Journey Optimizer] (webbkanal), [!DNL Real-Time CDP] |
| [Webbadress-/apppersonalisering för kända besökare](personalization/known-visitor-web-app-personalization.md) | Leverera personaliserat innehåll, erbjudanden eller kampanjer till identifierade besökare baserat på realtidsprofil och segmentmedlemskap | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Erbjudandebeslut](personalization/offer-decisioning.md) | Använd centraliserad beslutslogik för att välja nästa bästa erbjudande eller innehåll för en profil i olika kanaler | [!DNL Journey Optimizer] (beslut), [!DNL Real-Time CDP] |
| [Beteenderekommendation](personalization/behavioral-recommendation.md) | Generera rekommendationer för artikel och innehåll med urvalsstrategier och rangordningsmodeller | [!DNL Journey Optimizer] (beslut), [!DNL Real-Time CDP] |

## Kampanjhantering och samordning

Följande mönster omfattar schemalagd, utlöst och flerstegsbaserad meddelandeleverans över flera kanaler.

| Mönster | Primär kapacitet | Kärnlösningar |
| --- | --- | --- |
| [Aktivera utgående batchmeddelande](campaign-management-orchestration/batch-outbound-message-activation.md) | Utvärdera en målgrupp och leverera sedan ett schemalagt utgående meddelande i en enda batchkörning | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Händelseutlösta meddelanden](campaign-management-orchestration/event-triggered-messaging.md) | Lyssna efter en händelse i realtid som rör beteende eller system och leverera sedan ett sammanhangsberoende meddelande till den utlösande profilen | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Samlad resa i flera steg](campaign-management-orchestration/multi-step-orchestrated-journey.md) | Vägled en profil genom en förgreningsprocess med flera kontaktytor, väntetider, villkor och flera meddelandeåtgärder | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Flerkanalsresa med beslut](campaign-management-orchestration/cross-channel-journey-with-decisioning.md) | Samordna en flerstegsresa som innefattar realtidsbeslut för att välja optimala kanaler, innehåll eller erbjudanden | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Köpa gruppbaserad marknadsföring och resehantering](campaign-management-orchestration/buying-group-based-marketing.md) | Utveckla kundresor på kontonivå som kvalificerar leads till inköpsgrupper för att förbättra effektiviteten inom B2B-marknadsföring | [!DNL Journey Optimizer] B2B edition, [!DNL Real-Time CDP] B2B edition |

## Analys

Följande mönster har stöd för beteendeanalys i flera kanaler och prestandaanalys.

| Mönster | Primär kapacitet | Kärnlösningar |
| --- | --- | --- |
| [Generering av kundanalyser och insikter](analysis/customer-analytics-insight-generation.md) | Bygg arbetsytor för flerkanalsanalys, beräknade mätvärden och paneler för beteende- och prestandaanalys | [!DNL Customer Journey Analytics], [!DNL Experience Platform] |
| [B2B-analys](analysis/b2b-analytics.md) | Inkludera information på kontonivå B2B i kundreseanalys över flera kanaler | [!DNL Customer Journey Analytics] B2B edition, [!DNL Real-Time CDP] B2B edition |

## Konversationsupplevelser

Följande mönster möjliggör AI-driven, varumärkessäker konverteringsinteraktion om digitala resurser.

| Mönster | Primär kapacitet | Kärnlösningar |
| --- | --- | --- |
| [Brand Concierge samtalsupplevelse](conversational-experience/brand-concierge-conversational-experience.md) | Omvandla digitala resurser till varumärkesskyddade, AI-baserade konverteringsinsikter som vägleder kundupptäckt | [!DNL Brand Concierge], [!DNL Experience Platform], [!DNL Real-Time CDP] |

## Scenarioväljare

Använd den här vägledningen när ett scenario kan passa in mer än ett mönster. Svara på förgreningsfrågorna för att hitta det primära mönstret och utöka sedan eventuellt med de listade mönstren.

### Vinn tillbaka med förmånserbjudande

*En kund som inte är kund har inte köpt på 90 dagar. Du vill engagera dem på nytt med ett riktat erbjudande.*

- **Är valet av erbjudande dynamiskt (olika kunder får olika erbjudanden baserat på behörighet eller rankning)?**
   - Ja → [Erbjudandebeslut](personalization/offer-decisioning.md) som erbjudandelager, inkapslat i [Flerstegsdirigerad resa](campaign-management-orchestration/multi-step-orchestrated-journey.md) för återengagemangssekvensen
   - Nej (samma erbjudande till alla kvalificerade förfallna kunder) → [Enbart flerstegsdirigerad resa](campaign-management-orchestration/multi-step-orchestrated-journey.md)

### Uppföljning efter köp

*En kund har just slutfört ett köp. Du vill skicka en bekräftelse, korsförsäljningsrekommendation och meddelanden om förmånsbelöning.*

- **Kräver sekvensen adaptiv förgreningslogik baserat på händelser i realtid (t.ex. belöning som begärts, produkten granskad)?**
   - Ja → [Flerstegsdirigerad resa](campaign-management-orchestration/multi-step-orchestrated-journey.md)
   - Nej (fast sekvens, ingen förgrening) → [Aktivera utgående batchmeddelande](campaign-management-orchestration/batch-outbound-message-activation.md)
- **Innehåller den anpassade produktrekommendationer?**
   - Ja → Utöka med [beteenderekommendation](personalization/behavioral-recommendation.md) i innehållslagret

### Lojalitetens milstolpe-personalisering

*En kund når en ny lojalitetsnivå. Du vill visa anpassat webbinnehåll och skicka ett gratulationsmeddelande.*

- **Är webbinnehållet personaliserat (olika innehåll per skikt eller segment)?**
   - Ja → [Anpassning av webbsidor/appar för kända besökare](personalization/known-visitor-web-app-personalization.md) för webbsidan
- **Är det utgående meddelandet en enda skicka- eller en överordnade sekvens?**
   - Single send → [Händelseutlöst meddelande](campaign-management-orchestration/event-triggered-messaging.md)
   - Sekvens → [Flerstegsdirigerad resa](campaign-management-orchestration/multi-step-orchestrated-journey.md)

### Återengagemangskampanj

*Ett segment med inaktiva användare behöver en multitouch-reaktiveringssekvens.*

- **Behöver enskilda meddelanden väljas bland flera olika erbjudandevarianter i realtid?**
   - Ja → [Flerkanalsresa med beslut](campaign-management-orchestration/cross-channel-journey-with-decisioning.md)
   - Nej → [Flerstegsdirigerad resa](campaign-management-orchestration/multi-step-orchestrated-journey.md)
