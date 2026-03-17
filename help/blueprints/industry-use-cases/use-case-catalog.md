---
title: Använd fallkatalog
description: Bläddra bland branschens användningsexempel efter vertikal nivå, mognadsnivå eller implementeringsmönster för att hitta rätt startpunkt för din Adobe Experience Platform-resa.
doc-type: overview-page
exl-id: 7a3c2f1e-9b4d-4e6a-8f5c-2d1b3a4e7c9f
source-git-commit: 8ad59ff130dae13553f10049eb685cf557a73ead
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 6%

---

# Använd fallkatalog

Utforska branschanvändningsexempel för [!DNL Adobe Experience Platform] och program. Bläddra efter bransch för att se användningsexempel för vertikalt, efter mognadsnivå för att hitta rätt startpunkt för organisationen, eller efter implementeringsmönster för att förstå vilken teknisk strategi som passar era behov.

Varje användningsfall länkar till detaljerad implementeringsvägledning via ett användningsmönster, som beskriver funktionskedjan, beslutspunkter och konfigurationssteg som behövs för att ge användningsexemplet liv.

## Bläddra efter bransch

>[!BEGINTABS]

>[!TAB Detaljhandel]

Butiksorganisationer använder [!DNL Adobe Experience Platform] för att samla kunddata från onlinebutiker, fysiska platser och lojalitetsprogram i en enda vy över varje kund.

| | Användningsfall | Beskrivning | Löptid | Mönster |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-product-recommendations.png" alt="Personaliserade produktrekommendationer" width="40"> | [Personaliserade produktrekommendationer](retail/retail-overview.md#personalized-product-recommendations) | Visa personaliserade produkter baserat på bläddring och inköpshistorik | [!BADGE Nya]{type=Informative} | [Beteenderekommendation](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| <img src="assets/use-case-icons/icon-abandoned-cart.png" alt="Övergiven kundvagn" width="40"> | [Återställning av övergiven e-post för kundvagn](retail/retail-overview.md#abandoned-cart-email-recovery) | Skicka personliga påminnelser för övergivna kundvagnar | [!BADGE Foundational]{type=Neutral} | [Meddelanden som utlösts av händelser](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-inventory-urgency.png" alt="Lagerbehov" width="40"> | [Lagerbaserade nödkampanjer](retail/retail-overview.md#inventory-based-urgency-campaigns) | Utlös varningar i realtid när produktlagret är lågt | [!BADGE Foundational]{type=Neutral} | [Meddelanden som utlösts av händelser](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-cross-sell-upsell.png" alt="Merförsäljning" width="40"> | [Korsförsäljning och merförsäljning - rekommendationer](retail/retail-overview.md#cross-sell-and-upsell-recommendations) | Visa relevanta korsförsäljnings- och merförsäljningsprodukter i kassan och via e-post | [!BADGE Avancerat]{type=Caution} | [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) |
| <img src="assets/use-case-icons/icon-welcome-series.png" alt="Välkomstserie" width="40"> | [Nya välkomstserier för kunder](retail/retail-overview.md#new-customer-welcome-series) | Automatisera en välkomstserie med flera e-postmeddelanden med personaliserade rekommendationer | [!BADGE Nya]{type=Informative} | [Samlad resa i flera steg](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| <img src="assets/use-case-icons/icon-price-drop.png" alt="Prisfall" width="40"> | [Varningar om prisfall](retail/retail-overview.md#price-drop-alerts) | Meddela kunderna när önskelistan eller visade objekt sjunker till priset | [!BADGE Foundational]{type=Neutral} | [Meddelanden som utlösts av händelser](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-replenishment.png" alt="Påfyllnad" width="40"> | [Påfyllnadspåminnelser](retail/retail-overview.md#replenishment-reminders) | Skicka automatiska påminnelser för konsumtionsartiklar som köpts regelbundet | [!BADGE Nya]{type=Informative} | [Samlad resa i flera steg](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| <img src="assets/use-case-icons/icon-category-pages.png" alt="Kategorisidor" width="40"> | [Anpassade kategorisidor](retail/retail-overview.md#personalized-category-pages) | Ordna om kategorisidor dynamiskt baserat på varje kunds önskemål | [!BADGE Nya]{type=Informative} | [Beteenderekommendation](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| <img src="assets/use-case-icons/icon-post-purchase.png" alt="Efter köp" width="40"> | [Uppföljningskampanjer efter köp](retail/retail-overview.md#post-purchase-follow-up-campaigns) | Skicka tips, förfrågningar och relaterade produktförslag | [!BADGE Nya]{type=Informative} | [Samlad resa i flera steg](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| | [Exklusiva erbjudanden för VIP-kunder](retail/retail-overview.md#vip-customer-exclusive-offers) | Ge exklusiva erbjudanden och tidig åtkomst till värdefulla kunder | [!BADGE Avancerat]{type=Caution} | [Flerkanalsresor med beslut](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) |
| | [Aviseringar som inte finns i lager](retail/retail-overview.md#out-of-stock-notifications) | Meddela kunderna när färdiga produkter blir tillgängliga | [!BADGE Foundational]{type=Neutral} | [Meddelanden som utlösts av händelser](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| | [Socialt korrektur av Personalization](retail/retail-overview.md#social-proof-personalization) | Visa anpassade recensioner och omdömen baserat på kundprofil | [!BADGE Nya]{type=Informative} | [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) |

>[!TAB Finansiella tjänster]

Användningsexempel inom finanssektorn kommer snart. [Visa aktuella användningsfall för finansiella tjänster &#x200B;](financial-services/financial-services-overview.md).

>[!TAB Hälsovård]

Vårdärenden kommer snart. [Visa aktuella användningsfall för hälso- och sjukvård &#x200B;](healthcare/healthcare-overview.md).

>[!TAB Automatisering]

Vi kommer snart att få fler fall av bilanvändning. [Visa aktuella ärenden för automatisk användning &#x200B;](automotive/automotive-overview.md).

>[!TAB Resor och turism]

Fall av rese- och turismanvändning kommer snart. [Visa aktuella användningsfall för Resor och turism &#x200B;](travel-hospitality/travel-hospitality-overview.md).

>[!TAB Telekommunikation]

Fall av användning inom telekom kommer snart. [Visa aktuella användningsfall för telekommunikation &#x200B;](telecommunications/telecommunications-overview.md).

>[!TAB Media och underhållning]

Användningsexempel inom media och underhållning kommer snart. [Visa aktuella användningsfall för media och underhållning &#x200B;](media-entertainment/media-entertainment-overview.md).

>[!TAB Försäkring]

Försäkringsfall kommer snart. [Visa aktuella försäkringsanvändningsfall &#x200B;](insurance/insurance-overview.md).

>[!TAB B2B]

Användningsexempel inom B2B kommer snart. [Visa aktuella B2B-användningsfall &#x200B;](b2b/b2b-overview.md).

>[!ENDTABS]

## Bläddra efter mognadsnivå

>[!BEGINTABS]

>[!TAB Foundational]

Grundläggande, beprövade mönster med enkanalsleverans. Idealiska startpunkter för organisationer som börjar sin [!DNL Experience Platform]-resa.

| | Användningsfall | Bransch | Affärspåverkan | Mönster |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-abandoned-cart.png" alt="Övergiven kundvagn" width="40"> | [Återställning av övergiven e-post för kundvagn](retail/retail-overview.md#abandoned-cart-email-recovery) | Detaljhandel | 25-35 % kundvagnens återvinningsgrad | [Meddelanden som utlösts av händelser](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-inventory-urgency.png" alt="Lagerbehov" width="40"> | [Lagerbaserade nödkampanjer](retail/retail-overview.md#inventory-based-urgency-campaigns) | Detaljhandel | 30-40 % ökning av konverteringen | [Meddelanden som utlösts av händelser](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-price-drop.png" alt="Prisfall" width="40"> | [Varningar om prisfall](retail/retail-overview.md#price-drop-alerts) | Detaljhandel | 20-30 % konverteringsgrad | [Meddelanden som utlösts av händelser](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| | [Aviseringar som inte finns i lager](retail/retail-overview.md#out-of-stock-notifications) | Detaljhandel | 40-50 % konverteringsgrad | [Meddelanden som utlösts av händelser](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |

>[!TAB Nya]

Mönster för flera kanaler och steg som bygger på grundläggande funktioner med AI-driven personalisering och samordnade resor.

| | Användningsfall | Bransch | Affärspåverkan | Mönster |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-product-recommendations.png" alt="Produktrekommendationer" width="40"> | [Personaliserade produktrekommendationer](retail/retail-overview.md#personalized-product-recommendations) | Detaljhandel | 20-30 % ökning av CTR, 15-25 % konverteringshöjning | [Beteenderekommendation](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| <img src="assets/use-case-icons/icon-category-pages.png" alt="Kategorisidor" width="40"> | [Anpassade kategorisidor](retail/retail-overview.md#personalized-category-pages) | Detaljhandel | 25-35 % ökning av engagemanget | [Beteenderekommendation](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| <img src="assets/use-case-icons/icon-welcome-series.png" alt="Välkomstserie" width="40"> | [Nya välkomstserier för kunder](retail/retail-overview.md#new-customer-welcome-series) | Detaljhandel | 40-50 % engagemangsgrad | [Samlad resa i flera steg](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| <img src="assets/use-case-icons/icon-replenishment.png" alt="Påfyllnad" width="40"> | [Påfyllnadspåminnelser](retail/retail-overview.md#replenishment-reminders) | Detaljhandel | 30-40 % återkommande inköpspris | [Samlad resa i flera steg](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| <img src="assets/use-case-icons/icon-post-purchase.png" alt="Efter köp" width="40"> | [Uppföljningskampanjer efter köp](retail/retail-overview.md#post-purchase-follow-up-campaigns) | Detaljhandel | 15-20 % granskningsfrekvens, 10-15 % upprepat köp | [Samlad resa i flera steg](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| | [Socialt korrektur av Personalization](retail/retail-overview.md#social-proof-personalization) | Detaljhandel | 10-15 % ökning av konverteringsgraden | [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) |

>[!TAB Avancerat]

Flerkanalsmarknadsföring med realtidsbeslut och AI-drivet urval av erbjudanden för de mest avancerade kundupplevelserna.

| | Användningsfall | Bransch | Affärspåverkan | Mönster |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-cross-sell-upsell.png" alt="Merförsäljning" width="40"> | [Korsförsäljning och merförsäljning - rekommendationer](retail/retail-overview.md#cross-sell-and-upsell-recommendations) | Detaljhandel | Ökning med 25-75 dollar i AOV, 10-15 % ökade intäkter | [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) |
| | [Exklusiva erbjudanden för VIP-kunder](retail/retail-overview.md#vip-customer-exclusive-offers) | Detaljhandel | 50-70 % engagemang från VIP-medlemmar | [Flerkanalsresor med beslut](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) |

>[!ENDTABS]

## Bläddra efter implementeringsmönster

>[!BEGINTABS]

>[!TAB Kampanjhantering och samordning]

### Händelseutlöst meddelanden

Svara på beteendehändelser i realtid med aktuella enkanalsmeddelanden.

| | Användningsfall | Bransch | Löptid | Affärspåverkan |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-abandoned-cart.png" alt="Övergiven kundvagn" width="40"> | [Återställning av övergiven e-post för kundvagn](retail/retail-overview.md#abandoned-cart-email-recovery) | Detaljhandel | [!BADGE Foundational]{type=Neutral} | 25-35 % kundvagnens återvinningsgrad |
| <img src="assets/use-case-icons/icon-inventory-urgency.png" alt="Lagerbehov" width="40"> | [Lagerbaserade nödkampanjer](retail/retail-overview.md#inventory-based-urgency-campaigns) | Detaljhandel | [!BADGE Foundational]{type=Neutral} | 30-40 % ökning av konverteringen |
| <img src="assets/use-case-icons/icon-price-drop.png" alt="Prisfall" width="40"> | [Varningar om prisfall](retail/retail-overview.md#price-drop-alerts) | Detaljhandel | [!BADGE Foundational]{type=Neutral} | 20-30 % konverteringsgrad |
| | [Aviseringar som inte finns i lager](retail/retail-overview.md#out-of-stock-notifications) | Detaljhandel | [!BADGE Foundational]{type=Neutral} | 40-50 % konverteringsgrad |

### Flerstegsdirigerad resa

Vägled kunderna genom multitouch-sekvenser som anpassar sig utifrån engagemang och beteende.

| | Användningsfall | Bransch | Löptid | Affärspåverkan |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-welcome-series.png" alt="Välkomstserie" width="40"> | [Nya välkomstserier för kunder](retail/retail-overview.md#new-customer-welcome-series) | Detaljhandel | [!BADGE Nya]{type=Informative} | 40-50 % engagemangsgrad |
| <img src="assets/use-case-icons/icon-replenishment.png" alt="Påfyllnad" width="40"> | [Påfyllnadspåminnelser](retail/retail-overview.md#replenishment-reminders) | Detaljhandel | [!BADGE Nya]{type=Informative} | 30-40 % återkommande inköpspris |
| <img src="assets/use-case-icons/icon-post-purchase.png" alt="Efter köp" width="40"> | [Uppföljningskampanjer efter köp](retail/retail-overview.md#post-purchase-follow-up-campaigns) | Detaljhandel | [!BADGE Nya]{type=Informative} | 15-20 % granskningsfrekvens, 10-15 % upprepat köp |

### Flerkanalsresor med beslut

Samordna flerkanalsupplevelser med offertbeslut i realtid vid alla kontaktytor.

| | Användningsfall | Bransch | Löptid | Affärspåverkan |
| --- | --- | --- | --- | --- |
| | [Exklusiva erbjudanden för VIP-kunder](retail/retail-overview.md#vip-customer-exclusive-offers) | Detaljhandel | [!BADGE Avancerat]{type=Caution} | 50-70 % engagemang från VIP-medlemmar |

>[!TAB Personalization]

### Beteenderekommendation

Använd AI-drivna modeller för att ta fram personaliserat innehåll och produkter baserade på beteendesignaler.

| | Användningsfall | Bransch | Löptid | Affärspåverkan |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-product-recommendations.png" alt="Produktrekommendationer" width="40"> | [Personaliserade produktrekommendationer](retail/retail-overview.md#personalized-product-recommendations) | Detaljhandel | [!BADGE Nya]{type=Informative} | 20-30 % ökning av CTR, 15-25 % konverteringshöjning |
| <img src="assets/use-case-icons/icon-category-pages.png" alt="Kategorisidor" width="40"> | [Anpassade kategorisidor](retail/retail-overview.md#personalized-category-pages) | Detaljhandel | [!BADGE Nya]{type=Informative} | 25-35 % ökning av engagemanget |

### Offer Decisioning (erbjudandebeslut)

Använd centraliserad beslutslogik för att utvärdera och välja det bästa erbjudandet för varje kund och sammanhang.

| | Användningsfall | Bransch | Löptid | Affärspåverkan |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-cross-sell-upsell.png" alt="Merförsäljning" width="40"> | [Korsförsäljning och merförsäljning - rekommendationer](retail/retail-overview.md#cross-sell-and-upsell-recommendations) | Detaljhandel | [!BADGE Avancerat]{type=Caution} | Ökning med 25-75 dollar i AOV, 10-15 % ökade intäkter |

### Known-Visitor Web/App Personalization

Anpassa webb- och appinnehåll för identifierade besökare baserat på profil, preferenser och surfkontext.

| | Användningsfall | Bransch | Löptid | Affärspåverkan |
| --- | --- | --- | --- | --- |
| | [Socialt korrektur av Personalization](retail/retail-overview.md#social-proof-personalization) | Detaljhandel | [!BADGE Nya]{type=Informative} | 10-15 % ökning av konverteringsgraden |

>[!ENDTABS]
