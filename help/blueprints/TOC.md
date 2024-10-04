---
user-guide-title: Digital Experience-utkast
breadcrumb-title: Utkast
user-guide-description: Utkast är repeterbara implementeringar som åtgärdar etablerade affärsproblem och innehåller arkitekturdiagram, tekniska överväganden och relevanta dokumentationslänkar.
product: adobe experience platform
mini-toc-levels: 3
role: Architect, Developer, User
source-git-commit: 6a13de73d7f61295092faccfc21172f5e188331d
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 18%

---


# Digital Experience-utkast {#architecture}

+ [Digital Experiences Blueprints](/help/blueprints/overview.md)
+ Lodräta industrimodeller{#vertical-blueprints}
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
      + [Experience Platform Web SDK &amp; [!DNL Edge Network]](/help/blueprints/experience-platform/deployment/websdk.md)
      + [SDK för program](/help/blueprints/experience-platform/deployment/appsdk.md)
      + [Skyddsräcken](/help/blueprints/experience-platform/deployment/guardrails.md)
+ Målgrupps- och profilaktivering{#audience-activation}
   + [Översikt](/help/blueprints/audience-activation/overview.md)
   + [Anonym Audience Activation](/help/blueprints/audience-activation/anonymous.md)
   + Känd kundaktivering (RTCDP) {#known-customer-audience-activation}
      + [Översikt](/help/blueprints/audience-activation/known.md)
      + [Aktivering i sociala kanaler och annonskanaler](/help/blueprints/audience-activation/advertising-activation.md)
      + [Aktivering till mål för fil- och företagsströmning](/help/blueprints/audience-activation/enterprise-destinations.md)
      + [Kundaktivitetsnav](/help/blueprints/audience-activation/customer-activity.md)
      + [Segmentmatchning](/help/blueprints/audience-activation/segment-match.md)
   + [Aktivering med Experience Cloud-program](/help/blueprints/audience-activation/platform-and-applications.md)
   + Webb och mobil - Personalization{#web-personalization}
      + [Översikt](/help/blueprints/audience-activation/web-personalization/overview.md)
      + [Beteendeanpassning - målinriktat](/help/blueprints//audience-activation/web-personalization/behavioral.md)
      + [Känd kundanpassning - mål och RTCDP](/help/blueprints/audience-activation/web-personalization/known-personalization.md)
      + [Beslutsledning](/help/blueprints/audience-activation/web-personalization/decision-management-edge.md)
+ B2B-aktivering och marknadsföring{#b2b-activation}
   + [Översikt](/help/blueprints/b2b/overview.md)
   + [B2B-aktivering](/help/blueprints/b2b/b2bactivation.md)
   + [Aktivera B2B-konto](/help/blueprints/b2b/b2b-account-activation.md)
   + [Köpa gruppbaserad marknadsföring och resehantering](/help/blueprints/b2b/b2b-buying-group-journeys.md)
   + Integreringsutkast för Marketo Engage och Workfront {#marketo-engage-and-workfront-integration-blueprint}
      + [Översikt](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/overview.md)
      + [Infoga och skapa](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md)
      + [Granska och godkänn](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md)
      + [Nöjda kunder](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md)
+ Innehåll och Commerce{#content-commerce}
   + [Adobe Commerce &amp; RTCDP](/help/blueprints/content-commerce/commerce/commerce-rtcdp.md)
+ Customer Journey Analytics{#customer-journey-analytics}
   + [Översikt](/help/blueprints/customer-journey-analytics/overview.md)
   + [Dela CJA-målgrupper med RTCDP](/help/blueprints/customer-journey-analytics/cja-rtcdp.md)
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
      + [[!DNL Campaign Standard]](https://experienceleague.adobe.com/docs/campaign-standard.html){target="_blank"}
      + [Real-Time CDP med Adobe [!DNL Campaign Standard]](https://experienceleague.adobe.com/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/aep-sources-destinations/get-started-sources-destinations.html){target="_blank"}
   + Kampanj v8{#campaign-v8}
      + [Campaign v8](/help/blueprints/customer-journeys/campaign-v8.md)
      + [Real-Time CDP med Adobe [!DNL Campaign] v8](/help/blueprints/customer-journeys/rtcdp-and-campaign-v8.md)
      + [Journey Optimizer med Adobe Campaign v8](/help/blueprints/customer-journeys/ajo-and-campaign-v8.md)
   + Campaign v7{#campaign-v7}
      + [Campaign v7](/help/blueprints/customer-journeys/campaign-v7.md)
      + [Real-Time CDP med Adobe [!DNL Campaign] v7](/help/blueprints/customer-journeys/rtcdp-and-campaign.md)
      + [Journey Optimizer med Adobe [!DNL Campaign] v7](/help/blueprints/customer-journeys/ajo-and-campaign-v7.md)
+ Datainsamling, åtkomst och export{#data-ingestion}
   + [Översikt](/help/blueprints/data-ingestion/overview.md)
   + [Datainsamling för vidarebefordran av händelser i flera sandlådor](/help/blueprints/data-ingestion/multi-sandbox-event-forwarding.md)
   + [Förberedelse och förtäring av data](/help/blueprints/data-ingestion/ingestion.md)
   + [Dataåtkomst och -export](/help/blueprints/data-ingestion/egress.md)
   + [Vidarebefordran av händelser](/help/blueprints/data-ingestion/server-side-collection.md)
+ Dataanalys, intelligens och AI/ML{#data-exploration}
   + [Översikt](/help/blueprints/data-insights/overview.md)
   + [Dataanalys och dataanalys](/help/blueprints/data-insights/analysis.md)
   + [Anpassad datavetenskap för profilberikning](/help/blueprints/data-insights/data-science.md)
