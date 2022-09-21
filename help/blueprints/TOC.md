---
user-guide-title: Digital Experience-utkast
breadcrumb-title: Blueprints
user-guide-description: Utkast är repeterbara implementeringar som åtgärdar etablerade affärsproblem och innehåller arkitekturdiagram, tekniska överväganden och relevanta dokumentationslänkar.
product: adobe experience platform
mini-toc-levels: 3
role: Architect, Developer, User
source-git-commit: 9fac27843985da725ffac9c6b01518b595fdb22b
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Digital Experience-utkast {#architecture}

+ [Översikt](/help/blueprints/overview.md)
+ [Se alla användningsfall](/help/blueprints/use-cases.md)
+ Lodräta industriskisser{#vertical-blueprints}
   + [Översikt](/help/blueprints/industry-success-stories/overview.md)
   + [Kläder](/help/blueprints/industry-success-stories/apparel.md)
   + [Detaljhandel](/help/blueprints/industry-success-stories/retail.md)
   + [Telekommunikation](/help/blueprints/industry-success-stories/telecommunications.md)
   + [Resor och turism](/help/blueprints/industry-success-stories/travel-hospitality.md)
+ Arkitekturöversikter{#architecture-overview}
   + [Experience Cloud](/help/blueprints/experience-platform/experience-cloud.md)
   + [Experience Platform och program](/help/blueprints/experience-platform/platform-applications.md)
   + [Experience Platform dataflöde](/help/blueprints/experience-platform/platform-data-flow.md)
   + Distributionsmodeller{#deployment}
      + [Experience Platform Web SDK &amp; Edge Network](/help/blueprints/data-ingestion/websdk.md)
      + [SDK för program](/help/blueprints/data-ingestion/appsdk.md)
+ Målgrupps- och profilaktivering{#audience-activation}
   + [Översikt](/help/blueprints/audience-activation/overview.md)
   + [Anonym Audience Activation (AAM)](/help/blueprints/audience-activation/anonymous.md)
   + Känd kundaktivering (RTCDP) {#known-customer-audience-activation}
      + [Översikt](/help/blueprints/audience-activation/known.md)
      + Aktivering till sociala kanaler och reklamkanaler{#audience-activation}
         + [Aktivering till Facebook anpassade målgrupper](/help/blueprints/audience-activation/destinations/facebook.md)
         + [Aktivering till Google kundmatchning](/help/blueprints/audience-activation/destinations/gcm.md)
      + [Aktivering till mål för fil- och företagsströmning](/help/blueprints/audience-activation/enterprise-destinations.md)
      + [Kundaktivitetshubb](/help/blueprints/audience-activation/customer-activity.md)
   + [Aktivering med Experience Cloud-program](/help/blueprints/audience-activation/platform-and-applications.md)
   + [Segmentmatchning](/help/blueprints/audience-activation/segment-match.md)
+ B2B-aktivering och marknadsföring{#b2b-activation}
   + [Översikt](/help/blueprints/b2b/overview.md)
   + [B2B-aktivering](/help/blueprints/b2b/b2bactivation.md)
+ Customer Journey Analytics{#customer-journey-analytics}
   + [Översikt](/help/blueprints/customer-journey-analytics/overview.md)
   + [Dela CJA-målgrupper till RTCDP](/help/blueprints/customer-journey-analytics/cja-rtcdp.md)
   + [CJA och Journey Optimizer](/help/blueprints/customer-journey-analytics/cja-ajo.md)
+ Kundresor{#customer-journeys}
   + [Översikt](/help/blueprints/customer-journeys/overview.md)
   + Journey Optimizer{#journey-optimizer}
      + [Journey Optimizer](/help/blueprints/customer-journeys/journey-optimizer.md)
      + Beslutshantering{#decision-management}
         + [Översikt](/help/blueprints/customer-journeys/decision_management/decision-management-overview.md)
         + [Beslutsfattare i utkanten](/help/blueprints/customer-journeys/decision_management/decision-management-edge.md)
         + [Beslutshantering på navet](/help/blueprints/customer-journeys/decision_management/decision-management-hub.md)
      + [Journey Optimizer med Adobe Campaign](/help/blueprints/customer-journeys/ajo-and-campaign.md)
      + [Meddelanden från tredje part](/help/blueprints/customer-journeys/3rd-party-messaging.md)
   + Campaign v8{#campaign-v8}
      + [Campaign v8](/help/blueprints/customer-journeys/campaign-v8.md)
   + Campaign v7{#campaign-v7}
      + [Campaign v7](/help/blueprints/customer-journeys/campaign-v7.md)
      + [Real-Time CDP med Adobe Campaign](/help/blueprints/customer-journeys/rtcdp-and-campaign.md)
+ Datainmatning och dataexport{#data-ingestion}
   + [Översikt](/help/blueprints/data-ingestion/overview.md)
   + [Förberedelse och inmatning av data](/help/blueprints/data-ingestion/ingestion.md)
   + [Vidarebefordran av händelser](/help/blueprints/data-ingestion/server-side-collection.md)
   + [Samling med data för flera sandlådor](/help/blueprints/data-ingestion/multi-sandbox-data-collection.md)
+ Dataanalys, intelligens och AI/ML{#data-exploration}
   + [Översikt](/help/blueprints/data-insights/overview.md)
   + [Dataanalys och dataanalys](/help/blueprints/data-insights/analysis.md)
   + [Custom Data Science for Profile Enrichment](/help/blueprints/data-insights/data-science.md)
+ Webb- och mobilpersonalisering{#web-personalization}
   + [Översikt](/help/blueprints/web-personalization/overview.md)
   + [Beteendeanpassning - mål](/help/blueprints/web-personalization/behavioral.md)
   + [Känd kundanpassning - mål och RTCDP](/help/blueprints/web-personalization/known-personalization.md)
   + [Beslutshantering](/help/blueprints/web-personalization/decision-management-edge.md)