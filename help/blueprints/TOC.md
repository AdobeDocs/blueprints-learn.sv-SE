---
user-guide-title: Affärsmål för kundupplevelsesamordning, användningsfall, arkitekturdiagram och utkast
breadcrumb-title: Användningsexempel och utkast
user-guide-description: Utforska viktiga affärsmål, fallmönster och exempel på användning i branschen för Adobe Experience Platform och tillämpningar. Diagram över visuell arkitektur och ritningar ger tekniska referenser för systemintegration, dataflöden och lösningsdesign - som kopplar affärsvärde till implementering.
product: adobe experience platform
mini-toc-levels: 3
role: Developer, User
source-git-commit: abed39b6b6f63f2eef6cb36b400319910f8cf472
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 20%

---


# Kundupplevelsesimuleringar {#architecture}

+ [Kundupplevelsesimuleringar](/help/blueprints/overview.md)
+ Viktiga affärsmål för AEP och appar{#business-objectives}
   + [Översikt](/help/blueprints/business-objectives/overview.md)
   + Förvärv och tillväxt{#acquisition-growth}
      + [Skaffa nya kunder](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)
      + [Öka leadgenerering](/help/blueprints/business-objectives/acquisition-growth/increase-lead-generation.md)
      + [Öka webbplatsengagemanget](/help/blueprints/business-objectives/acquisition-growth/increase-website-engagement.md)
   + Intäkter och intäkter{#revenue-monetization}
      + [Öka konverteringsgraden](/help/blueprints/business-objectives/revenue-monetization/increase-conversion-rates.md)
      + [Öka intäkter och försäljning](/help/blueprints/business-objectives/revenue-monetization/increase-revenue-sales.md)
      + [Driv intäkter från korsförsäljning och merförsäljning](/help/blueprints/business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)
      + [Öka kundens lojalitet och livstidsvärde](/help/blueprints/business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)
   + Kostnad och effektivitet{#cost-efficiency}
      + [Minska kostnaden för kundvärvning](/help/blueprints/business-objectives/cost-efficiency/reduce-customer-acquisition-cost.md)
      + [Optimera marknadsföringsutgifter och avkastning](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)
      + [Förbättra datakvalitet och -styrning](/help/blueprints/business-objectives/cost-efficiency/improve-data-quality-governance.md)
      + [Konsolidera och modernisera marknadsföringsteknologi](/help/blueprints/business-objectives/cost-efficiency/consolidate-modernize-marketing-technology.md)
   + Kundupplevelse{#customer-experience-objectives}
      + [Leverera personaliserade kundupplevelser](/help/blueprints/business-objectives/customer-experience/deliver-personalized-customer-experiences.md)
      + [Förbättra kundlojaliteten](/help/blueprints/business-objectives/customer-experience/improve-customer-retention.md)
      + [Förbättra kundintroduktionen](/help/blueprints/business-objectives/customer-experience/improve-customer-onboarding.md)
      + [Återvinn övergivna bilar och resor](/help/blueprints/business-objectives/customer-experience/recover-abandoned-carts-journeys.md)
   + Analyser och insikter{#analytics-insights}
      + [Förbättra analyser och rapporter](/help/blueprints/business-objectives/analytics-insights/improve-analytics-reporting.md)
      + [Aktivera datadriven beslutsfattande](/help/blueprints/business-objectives/analytics-insights/enable-data-driven-decision-making.md)
      + [Förbättra marknadsattribuering](/help/blueprints/business-objectives/analytics-insights/improve-marketing-attribution.md)
   + Kvalificering och försäljning (B2B){#qualification-sales-b2b}
      + [Förbättra talkvalificering och konvertering](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)
      + [Förbättra kundengagemanget](/help/blueprints/business-objectives/qualification-sales-b2b/improve-customer-engagement.md)
+ Använd fallmönster{#use-case-patterns}
   + [Översikt](/help/blueprints/use-case-patterns/overview.md)
   + Målgruppsbyggnad och -aktivering{#audience-building-activation}
      + [Audience Activation till mål](/help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md)
      + [Målgrupps-Collaboration med segmentmatchning](/help/blueprints/use-case-patterns/audience-building-activation/audience-collaboration-segment-match.md)
      + [Vidarebefordran av händelser](/help/blueprints/use-case-patterns/audience-building-activation/event-forwarding.md)
      + [B2B Audience Activation](/help/blueprints/use-case-patterns/audience-building-activation/b2b-audience-activation.md)
   + Personalisering{#personalization-patterns}
      + [Anonym besökare på Personalization](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md)
      + [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md)
      + [Offer Decisioning (erbjudandebeslut)](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md)
      + [Beteenderekommendation](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md)
   + Kampanjhantering och samordning{#campaign-orchestration-patterns}
      + [Aktivering av utgående batchmeddelande](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md)
      + [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md)
      + [Flerstegsdirigerad resa](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md)
      + [Flerkanalsresor med beslut](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md)
      + [Köpa gruppbaserad marknadsföring och resehantering](/help/blueprints/use-case-patterns/campaign-management-orchestration/buying-group-based-marketing.md)
   + Analys{#analysis-patterns}
      + [Kundanalys och insiktsgenerering](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md)
      + [B2B-analys](/help/blueprints/use-case-patterns/analysis/b2b-analytics.md)
   + Konversationsupplevelser{#conversational-experience-patterns}
      + [Brand Concierge Conversational Experience](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md)
+ Exempel på användningsområden inom branschen{#industry-use-cases}
   + [Använd fallkatalog](/help/blueprints/industry-use-cases/use-case-catalog.md)
   + [Bilar](/help/blueprints/industry-use-cases/automotive/automotive-overview.md)
   + [B2B](/help/blueprints/industry-use-cases/b2b/b2b-overview.md)
   + [Finansiella tjänster](/help/blueprints/industry-use-cases/financial-services/financial-services-overview.md)
   + [Hälso- och sjukvård](/help/blueprints/industry-use-cases/healthcare/healthcare-overview.md)
   + [Försäkring](/help/blueprints/industry-use-cases/insurance/insurance-overview.md)
   + [Media och underhållning](/help/blueprints/industry-use-cases/media-entertainment/media-entertainment-overview.md)
   + [Detaljhandel](/help/blueprints/industry-use-cases/retail/retail-overview.md)
   + [Telekommunikation](/help/blueprints/industry-use-cases/telecommunications/telecommunications-overview.md)
   + [Teknik](/help/blueprints/industry-use-cases/technology/technology-overview.md)
   + [Resor och turism](/help/blueprints/industry-use-cases/travel-hospitality/travel-hospitality-overview.md)
+ Arkitekturdiagram och utkast{#architecture-diagrams}
   + Arkitekturöversikter{#architecture-overview}
      + [Experience Cloud](/help/blueprints/experience-platform/experience-cloud.md)
      + [Experience Platform och program](/help/blueprints/experience-platform/platform-applications.md)
      + [Experience Platform dataflöde](/help/blueprints/experience-platform/platform-data-flow.md)
      + [Experience Platform skyddsräcken](/help/blueprints/experience-platform/guardrails.md)
      + Distribuering{#deployment}
         + [Experience Platform Web SDK &amp; [!DNL Edge Network]](/help/blueprints/experience-platform/deployment/websdk.md)
         + [SDK för program](/help/blueprints/experience-platform/deployment/appsdk.md)
   + Målgrupps- och profilaktivering{#audience-activation}
      + [Enhetsbaserad - anonym målgruppsanpassning med Audience Manager](/help/blueprints/audience-activation/audience-manager.md)
      + Real-Time Customer Data Platform (RTCDP) {#known-customer-audience-activation}
         + [Målgruppsaktivering för sociala medier och annonser](/help/blueprints/audience-activation/advertising-activation.md)
         + [Målgrupps- och profilaktivering av företagsapplikationer](/help/blueprints/audience-activation/enterprise-destinations.md)
         + [Profilåtkomst i realtid för support- och säljscenarier](/help/blueprints/audience-activation/customer-activity.md)
         + [Tillgång till kantprofiler i realtid för webb- och mobilpersonalisering](/help/blueprints/audience-activation/real-time-lookup.md)
         + [Målgruppssamarbete med segmentmatchning](/help/blueprints/audience-activation/segment-match.md)
         + [Känd kundpersonalisering med Target](/help/blueprints/audience-activation/rtcdp-target.md)
         + [Anpassad datavetenskap för profilberikning](/help/blueprints/audience-activation/data-science.md)
   + B2B-aktivering och marknadsföring{#b2b-activation}
      + [Översikt](/help/blueprints/b2b/overview.md)
      + [B2B-aktivering](/help/blueprints/b2b/b2bactivation.md)
      + [Aktivera B2B-konto](/help/blueprints/b2b/b2b-account-activation.md)
      + [Köpa gruppbaserad marknadsföring och resehantering](/help/blueprints/b2b/b2b-buying-group-journeys.md)
      + [B2B-resor med Marketo-data](/help/blueprints/b2b/b2b-journeys-with-marketo.md)
      + [B2B betald mediastyrenhet](/help/blueprints/b2b/ajo-b2b-paid-media-controller.md)
      + Integrering av Marketo Engage och Workfront{#marketo-engage-and-workfront-integration-blueprint}
         + [Översikt](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/overview.md)
         + [Infoga och skapa](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md)
         + [Granska och godkänn](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md)
         + [Nöjda kunder](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md)
   + Customer Journey Analytics{#customer-journey-analytics}
      + [Översikt](/help/blueprints/customer-journey-analytics/overview.md)
      + [B2B Customer Journey Analytics](/help/blueprints/customer-journey-analytics/b2b-cja.md)
      + [Dela CJA-målgrupper med RTCDP](/help/blueprints/customer-journey-analytics/cja-rtcdp.md)
      + [CJA och Journey Optimizer](/help/blueprints/customer-journey-analytics/cja-ajo.md)
      + [Dataanalys och dataanalys](/help/blueprints/customer-journey-analytics/analysis.md)
   + Kundresor{#customer-journeys}
      + [Översikt](/help/blueprints/customer-journeys/overview.md)
      + Journey Optimizer{#journey-optimizer}
         + [Journey Optimizer](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-overview.md)
         + [AJO resor](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-journeys.md)
         + [AJO-kampanjer](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-campaigns.md)
         + [Meddelanden från tredje part](/help/blueprints/customer-journeys/journey-optimizer/3rd-party-messaging.md)
      + Beslutshantering{#decision-management}
         + [Översikt](/help/blueprints/customer-journeys/decision-management/decision-management-overview.md)
         + [Beslutshantering för Edge](/help/blueprints/customer-journeys/decision-management/decision-management-edge.md)
         + [Beslutshantering på navet](/help/blueprints/customer-journeys/decision-management/decision-management-hub.md)
      + Campaign V8{#campaign-v8}
         + [Campaign V8](/help/blueprints/customer-journeys/campaign-v8/campaign-v8-overview.md)
         + [Real-Time CDP med Adobe [!DNL Campaign] v8](/help/blueprints/customer-journeys/campaign-v8/rtcdp-and-campaign-v8.md)
         + [Journey Optimizer med Adobe Campaign v8](/help/blueprints/customer-journeys/campaign-v8/ajo-and-campaign-v8.md)
      + Borttagna ritningar{#deprecated-blueprints}
         + Campaign Standard{#campaign-standard}
            + [[!DNL Campaign Standard]](https://experienceleague.adobe.com/en/docs/campaign-standard){target="_blank"}
            + [Real-Time CDP med Adobe [!DNL Campaign Standard]](https://experienceleague.adobe.com/en/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/get-started-sources-destinations)
         + Campaign v7{#campaign-v7}
            + [Campaign v7](/help/blueprints/customer-journeys/campaign-v7/campaign-v7-overview.md)
