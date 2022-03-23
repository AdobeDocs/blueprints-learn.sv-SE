---
title: Anonymt Audience Activation Blueprint
description: Lär er målinrikta målgrupper över webben och annonskanaler baserat på anonyma och beteendemässiga kunddata. Denna möjlighet möjliggör personaliserade och enhetliga kundupplevelser i realtid på olika enheter.
landing-page-description: Lär er målinrikta målgrupper över webben och annonskanaler baserat på anonyma och beteendemässiga kunddata.
solution: Experience Platform, Audience Manager
kt: 7211
thumbnail: null
exl-id: f17599f1-2e75-4cbe-841a-9fd1dae71ada
source-git-commit: f46c09a88cf2b49c816ab27c5daef20c01e99b09
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# Anonymt Audience Activation Blueprint

Aktivering av anonyma målgrupper är möjligheten att rikta och personalisera till målgrupper över webben, mobiler och annonskanaler baserat på anonyma enhets- och beteendedata.

## Användningsexempel

* Anonym målgruppsanpassning och personalisering på webbplatsen, i mobilappen eller i de annonskanaler som stöds.
* Optimera landningssidan och förautentiserade upplevelser baserat på kända enhets- och beteendeegenskaper.
* Utnyttja datanätverket från tredje part i Audience Manager för att ytterligare förfina och utöka era målgrupper för målinriktning.


## Program

Både Audience Manager och Real-time Customer Data Platform kan utnyttjas för att driva anonyma Audience Activation för annonseringsplatser och annonsdestinationer. Observera att Real-time Customer Data Platform bara stöder en delmängd av annonsdestinationer med anonyma enhetsidentifierare som finns i [destinationsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/overview.html?lang=en).

Microsoft Bing, Google DV360 och TradeDesk är de främsta reklamdestinationer som stöds av Real-time Customer Data Platform för anonym enhetsbaserad målinriktning. Utöver detta stöder Real-time Customer Data Platform ett antal kända kundbaserade destinationer som katalogiseras i [destinationsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/overview.html?lang=en) och enligt beskrivningen i [känd kundaktiveringsplan](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html).

## Arkitektur

<img src="assets/anonymous_activation.svg" alt="Referensarkitektur för den anonyma Audience Activation-designen" style="width:80%; border:1px solid #4a4a4a" />

## Implementeringssteg

<!-- These steps should link to help. -->

1. [Implementera Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=en#implementation-integration-guides).
1. Samla in data i Audience Manager.
1. Konfigurera signaler och egenskaper för användning i segmentdefinitioner.
1. Skapa segment i Audience Manager.
1. Konfigurera destinationer i Audience Manager för att dela målgrupper.

För implementeringssteg av Real-time Customer Data Platform, se [känd kundaktiveringsplan](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html).

## Relaterad dokumentation

* [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager.html?lang=en)
* [Experience Cloud [!UICONTROL Målgrupper]](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html)
* [Integrera Audience Manager med Target](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html)
* [Adobe Analytics segmentdelning via Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)
* [Kundaktiveringsutkast](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html).
* [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html)
