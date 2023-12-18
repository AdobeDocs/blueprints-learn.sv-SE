---
title: Real-Time CDP med integreringsmönstret Adobe Campaign v8
description: Visar hur Adobe Experience Platform och dess kundprofil i realtid och centraliserade segmenteringsverktyg kan användas med Adobe Campaign v8 för att leverera personaliserade konversationer.
solution: Real-Time Customer Data Platform, Campaign
exl-id: d0291088-02ed-4e7e-b538-018ea40e38c6
source-git-commit: 5f9384abe7f29ec764428af33c6dd1f0a43f5a89
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 10%

---

# Real-Time CDP med integreringsmönstret Adobe Campaign v8

Visar hur Adobe Experience Platform och dess kundprofil i realtid och centraliserade segmenteringsverktyg kan användas med Adobe Campaign för att leverera personanpassade konversationer.

<br>

## Program

* Adobe Experience Platform Real-Time CDP
* Adobe Campaign v8

<br>

## Arkitektur

<img src="assets/rtcdp-campaignv8-architecture.svg" alt="Referensarkitektur för integreringsmönstret Batch Messaging och Adobe Experience Platform" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Förutsättningar

* Kunden måste etableras för Experience Cloud med en giltig IMS-organisation
* Adobe Experience Platform och Campaign rekommenderas att etableras i samma IMS-organisation för en enda inloggnings-URL
* Kunden måste tilldelas V8-instansen av Campaign
* Kunden måste vara berättigad och ha tillgång till RTCDP, Sources, Destinations.
* Adobe Campaign produktkontext måste finnas
<br>

## Implementeringssteg

Läs följande dokumentation om hur du konfigurerar källkopplingen för Campaign v8 till Adobe Experience Platform och målkopplingen för Real-time Customer Data Platform till Campaign v8.
[Campaign och AEP Connectors](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html?lang=en)

## Guardrails

### Adobe Campaign

* Läs dokumentationen för Campaign-källanslutningen - [Kampanjkällkoppling](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/campaign.html?lang=en)
* Stöder endast driftsättning av enskilda enheter i Adobe Campaign


### Experience Platform Real-time Customer Data Platform segmentdelning

* Se RTCDP Campaign Destination Connector - [RTCDP Campaign Connection](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/adobe-campaign-managed-services.html)

* Se utkast för profiler och dataöverföringsgarantier för AEP - [Länk](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
