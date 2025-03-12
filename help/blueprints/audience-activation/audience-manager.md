---
title: Audience Manager Design
description: Lär dig att rikta in dig på målgrupper över webben och annonskanaler baserat på anonyma och beteendemässiga kunddata. Denna förmåga möjliggör personanpassade och konsekventa kundupplevelser i realtid på alla enheter.
landing-page-description: Lär dig att rikta in dig på målgrupper över webben och annonskanaler baserat på anonyma och beteendemässiga kunddata.
short-description: Lär dig att rikta in dig på målgrupper över webben och annonskanaler baserat på anonyma och beteendemässiga kunddata.
solution: Audience Manager
kt: 7211
thumbnail: null
exl-id: f17599f1-2e75-4cbe-841a-9fd1dae71ada
source-git-commit: 7cdafaa39e5f46a2d777219be519efca31d3830b
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 20%

---

# Audience Manager Design

Anonym målgruppsaktivering är möjligheten att rikta och personalisera till målgrupper över webben, mobiler och annonskanaler baserat på anonyma enhets- och beteendedata.

## Användningsfall

* Anonym målgruppsanpassning och personalisering på webbplatsen, i mobilappen eller i de annonskanaler som stöds.
* Optimera landningssidan och förautentiserade upplevelser baserat på kända enhets- och beteendeegenskaper.
* Utnyttja Audience Manager datanätverk från tredje part för att ytterligare förfina och utöka era målgrupper för målinriktning.


## Tillämpningar

* Audience Manager
* Kunddataplattform i realtid

Både Audience Manager och kunddataplattformen i realtid kan användas för att driva anonyma Audience Activation för annonsdestinationer och på plats. Observera att kunddataplattformen i realtid bara stöder en delmängd av annonsdestinationer med anonyma enhetsidentifierare som katalogiseras i [måldokumentationen](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/overview.html?lang=en).

Microsoft Bing, Google DV360 och TradeDesk är de främsta annonsmålen för kunddataplattformen i realtid för anonym enhetsbaserad målgruppsanpassning. Utöver detta stöder kunddataplattformen i realtid flera kända kundbaserade mål som katalogiseras i [måldokumentationen](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/overview.html?lang=en) och som beskrivs i [Kundaktiveringsplanen](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html).

## Arkitektur

![Referensarkitektur för den anonyma Audience Activation-designen](assets/anonymous_activation.svg)

<br>

## Implementeringssteg för Audience Manager

* Mer information om hur du implementerar Audience Manager finns i följande [dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html).

## Implementeringssteg för kunddataplattformen i realtid

* Implementeringssteg för kunddataplattformen i realtid finns i följande [dokumentation](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html).

## Relaterad dokumentation

* [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager.html?lang=en)
* [Experience Cloud [!UICONTROL Publiker]](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html)
* [Integrera Audience Manager med Target](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html)
* [Adobe Analytics segmentdelning via Audience Manager](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)
* [Kundaktiveringsplan](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html).
* [Kunddataplattform i realtid](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html)
