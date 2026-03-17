---
title: Använd fallmönster
description: Läs om användningsmönstren för implementering av Adobe Experience Platform och tillämpningar för att uppnå viktiga affärsmål.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
doc-type: overview-page
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Använd fallmönster

Använd fallmönster för att definiera repeterbara implementeringsmetoder för Adobe Experience Platform och program. Varje mönster beskriver en specifik funktion, funktionskedjan som levererar den, de program som ingår och de [viktiga affärsmålen](/help/blueprints/business-objectives/overview.md) som stöds.

Använd tabellerna nedan för att hitta det mönster som passar dina implementeringsbehov och följ sedan länken till den fullständiga implementeringsreferensen, inklusive alternativ, faser, beslutsvägledning och Experience League-dokumentation.

## Målgruppsuppbyggnad och -aktivering

Följande mönster hjälper er att bygga, utvärdera och aktivera målgruppssegment över olika kanaler och destinationer.

| Mönster | Primär kapacitet | Kärnlösningar |
| --- | --- | --- |
| [Audience Activation till mål](audience-building-activation/audience-activation-to-destinations.md) | Utvärdera och publicera målgruppssegment till externa destinationer för målinriktning eller undertryckning | [!DNL Real-Time CDP] |
| [Målgrupp-Collaboration med segmentmatchning](audience-building-activation/audience-collaboration-segment-match.md) | Dela och matcha målgruppssegment i sandlådor eller organisationer med segmentmatchning | [!DNL Real-Time CDP], [!DNL Experience Platform] |
| [Händelsevidarebefordran](audience-building-activation/event-forwarding.md) | Vidarebefordra händelsedata i realtid som samlats in via Edge Network till destinationer utanför Adobe | [!DNL Experience Platform] (Edge Network, vidarebefordran av händelser) |
| [B2B Audience Activation](audience-building-activation/b2b-audience-activation.md) | Aktivera kontobaserade B2B-målgrupper över webb-, e-post- och annonskanaler | [!DNL Real-Time CDP] B2B edition |

## Personalisering

Följande mönster levererar skräddarsydda upplevelser till kända och okända besökare på webben och i appar.

| Mönster | Primär kapacitet | Kärnlösningar |
| --- | --- | --- |
| [Anonym besökare på Personalization](personalization/anonymous-visitor-web-personalization.md) | Leverera personaliserat innehåll baserat på sessionsbeteendesignaler för oidentifierade besökare | [!DNL Journey Optimizer] (webbkanal), [!DNL Real-Time CDP] |
| [Known-Visitor Web/App Personalization](personalization/known-visitor-web-app-personalization.md) | Leverera personaliserat innehåll, erbjudanden eller kampanjer till identifierade besökare baserat på realtidsprofil och segmentmedlemskap | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Offer Decisioning](personalization/offer-decisioning.md) | Använd centraliserad beslutslogik för att välja nästa bästa erbjudande eller innehåll för en profil i olika kanaler | [!DNL Journey Optimizer] (beslut), [!DNL Real-Time CDP] |
| [Beteenderekommendation](personalization/behavioral-recommendation.md) | Generera rekommendationer för artikel och innehåll med urvalsstrategier och rangordningsmodeller | [!DNL Journey Optimizer] (beslut), [!DNL Real-Time CDP] |

## Kampanjhantering och samordning

Följande mönster omfattar schemalagd, utlöst och flerstegsbaserad meddelandeleverans över flera kanaler.

| Mönster | Primär kapacitet | Kärnlösningar |
| --- | --- | --- |
| [Aktivera utgående batchmeddelande](campaign-management-orchestration/batch-outbound-message-activation.md) | Utvärdera en målgrupp och leverera sedan ett schemalagt utgående meddelande i en enda batchkörning | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Meddelanden som utlösts av händelser](campaign-management-orchestration/event-triggered-messaging.md) | Lyssna efter en händelse i realtid som rör beteende eller system och leverera sedan ett sammanhangsberoende meddelande till den utlösande profilen | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Samlad resa i flera steg](campaign-management-orchestration/multi-step-orchestrated-journey.md) | Vägled en profil genom en förgreningsprocess med flera kontaktytor, väntetider, villkor och flera meddelandeåtgärder | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Flerkanalsresor med beslut](campaign-management-orchestration/cross-channel-journey-with-decisioning.md) | Samordna en flerstegsresa som innefattar realtidsbeslut för att välja optimala kanaler, innehåll eller erbjudanden | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Köpa gruppbaserad marknadsföring och resehantering](campaign-management-orchestration/buying-group-based-marketing.md) | Utveckla kundresor på kontonivå som kvalificerar leads till inköpsgrupper för att förbättra effektiviteten inom B2B-marknadsföring | [!DNL Journey Optimizer] B2B edition, [!DNL Real-Time CDP] B2B edition |

## Analys

Följande mönster har stöd för beteendeanalys i flera kanaler och prestandaanalys.

| Mönster | Primär kapacitet | Kärnlösningar |
| --- | --- | --- |
| [Kundanalys och insiktsgenerering](analysis/customer-analytics-insight-generation.md) | Bygg arbetsytor för flerkanalsanalys, beräknade mätvärden och paneler för beteende- och prestandaanalys | [!DNL Customer Journey Analytics], [!DNL Experience Platform] |
| [B2B-analys](analysis/b2b-analytics.md) | Inkludera information på kontonivå B2B i kundreseanalys över flera kanaler | [!DNL Customer Journey Analytics] B2B edition, [!DNL Real-Time CDP] B2B edition |

## Konversationsupplevelser

Följande mönster möjliggör AI-driven, varumärkessäker konverteringsinteraktion om digitala resurser.

| Mönster | Primär kapacitet | Kärnlösningar |
| --- | --- | --- |
| [Brand Concierge Conversational Experience](conversational-experience/brand-concierge-conversational-experience.md) | Omvandla digitala resurser till varumärkesskyddade, AI-baserade konverteringsinsikter som vägleder kundupptäckt | [!DNL Brand Concierge], [!DNL Experience Platform], [!DNL Real-Time CDP] |
