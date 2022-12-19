---
user-guide-title: Digital Experience-utkast
breadcrumb-title: Blueprints
user-guide-description: Utkast är repeterbara implementeringar som åtgärdar etablerade affärsproblem och innehåller arkitekturdiagram, tekniska överväganden och relevanta dokumentationslänkar.
product: adobe experience platform
mini-toc-levels: 3
role: Architect, Developer, User
source-git-commit: af390011dc068c4289f98d7fc0108ce48a5375c7
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 4%

---


# Digital Experience-utkast {#architecture}

+ [Översikt](/help/blueprints/overview.md)
+ Lodräta industriskisser{#vertical-blueprints}
   + [Översikt](/help/blueprints/vertical-blueprints/overview.md)
   + [Kläder](/help/blueprints/vertical-blueprints/apparel.md)
   + [Detaljhandel](/help/blueprints/vertical-blueprints/retail.md)
   + [Telekommunikation](/help/blueprints/vertical-blueprints/telecommunications.md)
   + [Resor och turism](/help/blueprints/vertical-blueprints/travel-hospitality.md)
+ Arkitekturöversikter{#architecture-overview}
   + [Experience Cloud](/help/blueprints/experience-platform/experience-cloud.md)
   + [Experience Platform och program](/help/blueprints/experience-platform/platform-applications.md)
   + [Experience Platform dataflöde](/help/blueprints/experience-platform/platform-data-flow.md)
   + Distribution{#deployment}
      + [Experience Platform Web SDK &amp; Edge Network](/help/blueprints/experience-platform/deployment/websdk.md)
      + [SDK för program](/help/blueprints/experience-platform/deployment/appsdk.md)
      + [Guardrails](/help/blueprints/experience-platform/deployment/guardrails.md)
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
      + [Segmentmatchning](/help/blueprints/audience-activation/segment-match.md)
   + [Aktivering med Experience Cloud-program](/help/blueprints/audience-activation/platform-and-applications.md)
+ B2B-aktivering och marknadsföring{#b2b-activation}
   + [Översikt](/help/blueprints/b2b/overview.md)
   + [B2B-aktivering](/help/blueprints/b2b/b2bactivation.md)
   + Kampanjleveranskedja med Marketo och Workfront{#optimize-campaign-supply-chain-with-marketo-and-workfront}
      + [Översikt](/help/blueprints/b2b/campaign-supply-chain/overview.md)
      + [Infoga och skapa](/help/blueprints/b2b/campaign-supply-chain/intake-and-create.md)
      + [Nöjda kunder berättar](/help/blueprints/b2b/campaign-supply-chain/customer-success-stories.md)
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
   + Campaign Standard{#campaign-standard}
      + [Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html)
      + [Real-Time CDP med Adobe Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/aep-sources-destinations/get-started-sources-destinations.html)
   + Campaign v8{#campaign-v8}
      + [Campaign v8](/help/blueprints/customer-journeys/campaign-v8.md)
      + [Real-Time CDP med Adobe Campaign v8](/help/blueprints/customer-journeys/rtcdp-and-campaign-v8.md)
      + [Journey Optimizer med Adobe Campaign v8](/help/blueprints/customer-journeys/ajo-and-campaign-v8.md)
   + Campaign v7{#campaign-v7}
      + [Campaign v7](/help/blueprints/customer-journeys/campaign-v7.md)
      + [Real-Time CDP med Adobe Campaign v7](/help/blueprints/customer-journeys/rtcdp-and-campaign.md)
      + [Journey Optimizer med Adobe Campaign v7](/help/blueprints/customer-journeys/ajo-and-campaign-v7.md)
+ Datainsamling, åtkomst och export{#data-ingestion}
   + [Översikt](/help/blueprints/data-ingestion/overview.md)
   + [Förberedelse och inmatning av data](/help/blueprints/data-ingestion/ingestion.md)
   + [Dataåtkomst och -export](/help/blueprints/data-ingestion/egress.md)
   + [Vidarebefordran av händelser](/help/blueprints/data-ingestion/server-side-collection.md)
+ Dataanalys, intelligens och AI/ML{#data-exploration}
   + [Översikt](/help/blueprints/data-insights/overview.md)
   + [Dataanalys och dataanalys](/help/blueprints/data-insights/analysis.md)
   + [Custom Data Science for Profile Enrichment](/help/blueprints/data-insights/data-science.md)
+ Webb- och mobilpersonalisering{#web-personalization}
   + [Översikt](/help/blueprints/web-personalization/overview.md)
   + [Beteendeanpassning - mål](/help/blueprints/web-personalization/behavioral.md)
   + [Känd kundanpassning - mål och RTCDP](/help/blueprints/web-personalization/known-personalization.md)
   + [Beslutshantering](/help/blueprints/web-personalization/decision-management-edge.md)