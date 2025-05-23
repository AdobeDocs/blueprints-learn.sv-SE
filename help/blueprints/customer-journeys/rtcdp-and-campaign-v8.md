---
title: Real-Time CDP med integreringsmönstret Adobe Campaign v8
description: Visar hur Adobe Experience Platform och dess kundprofil i realtid och centraliserade segmenteringsverktyg kan användas med Adobe Campaign v8 för att leverera personaliserade konversationer.
solution: Real-Time Customer Data Platform, Campaign
exl-id: d0291088-02ed-4e7e-b538-018ea40e38c6
source-git-commit: a1f3aef5b508575019bd651b9706efc7d6db5306
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 3%

---

# [!DNL Real-Time CDP] med integreringsmönstret Adobe [!DNL Campaign] v8

Visar hur Adobe [!DNL Experience Platform] och dess kundprofil i realtid och centraliserade segmenteringsverktyg kan användas med Adobe Campaign för att leverera personaliserade konversationer.

## Tillämpningar

* Adobe [!DNL Experience Platform Real-Time CDP]
* Adobe [!DNL Campaign] v8

## Arkitektur

<img src="assets/rtcdp-campaignv8-architecture.svg" alt="Referensarkitektur för integreringsmönstret Batch Messaging och Adobe Experience Platform" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Förutsättningar

* Kunden måste etableras för Experience Cloud med en giltig IMS-organisation
* Adobe Experience Platform och [!DNL Campaign] rekommenderas att etableras i samma IMS-organisation för en enda inloggnings-URL
* Kunden måste tilldelas V8-instansen av [!DNL Campaign]
* Kunden måste vara berättigad och ha tillgång till RTCDP, Sources, Destinations.
* Produktkontexten för Adobe [!DNL Campaign] måste finnas
<br>

## Implementeringssteg

Läs följande dokumentation om hur du konfigurerar källkopplingen för Campaign v8 till Adobe Experience Platform och målkopplingen för Real-time Customer Data Platform till Campaign v8.
[Kampanj- och AEP-anslutningar](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html?lang=sv-SE)

## Skyddsräcken

### Adobe Campaign

* Läs dokumentationen för Campaign-källanslutningen - [Campaign Source Connector](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/campaign.html?lang=sv-SE)
* Stöder endast driftsättning av enskilda enheter i Adobe Campaign


### Experience Platform Real-time Customer Data Platform segmentdelning

* Se RTCDP Campaign Destination Connector - [RTCDP Campaign Connection](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/adobe-campaign-managed-services.html?lang=sv-SE)

* Visa profiler för profil och dataöverföring för AEP - [Länk](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=sv-SE)
