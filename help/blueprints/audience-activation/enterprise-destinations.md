---
title: Målgruppsaktivering och profilaktivering av mål för fil- och företagsdirektuppspelning
description: Målgrupps- och profilaktivering för storföretagsdestinationer
solution: Real-Time Customer Data Platform
kt: 7475
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5
source-git-commit: de447727048098ecc0bf8598fe3bca386779f543
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 3%

---

# Målgruppsaktivering och profilaktivering av mål för fil- och företagsdirektuppspelning

Dela profil- och målgruppsändringar och händelser i strömning eller batch från [!UICONTROL Kunddataplattform i realtid] till företagsdatalager och företagsapplikationer. Dessa profil- och målgruppshändelser kan användas för att initiera en sälj- eller supportåtgärd till kunden, som att följa upp en övergiven ansökningsprocess eller registrering av ett webbinarium eller för att uppdatera företagsapplikationer med de senaste kundattributen och intelligensen från [!UICONTROL kunddataplattformen i realtid].

## Användningsfall

* Profil- och målgruppsaktivering till molnlagringsdestinationer eller direktuppspelningsdestinationer för företagsspårning, lagring, analys och aktivering av kunddata och insikter.

## Tillämpningar

* Adobe Experience Platform Activation

## Arkitektur

<img src="assets/known_activation.svg" alt="Referensarkitektur för företagsaktiveringsscenariot" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />


## Skyddsräcken

[Se skyddsritningarna på sidan med skyddsförslag.](../experience-platform/deployment/guardrails.md)

## Implementeringssteg

1. [Skapa scheman](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) för data som ska importeras.
1. [Skapa datauppsättningar](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) för data som ska importeras.
1. [Konfigurera rätt identiteter och identitetsnamnutrymmen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html) i schemat för att säkerställa att inkapslade data kan sammanfogas till en enhetlig profil.
1. [Aktivera scheman och datauppsättningar för profilen ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Infoga data](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) i Experience Platform.
1. [Tillhandahåller [!UICONTROL segmentdelning för kunddataplattformen i realtid]](https://www.adobe.com/go/audiences) mellan Experience Platform och Audience Manager för målgrupper som definieras i Experience Platform som ska delas med Audience Manager.
1. [Skapa segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) i Experience Platform. Systemet avgör automatiskt om segmentet utvärderas som batch eller direktuppspelning.
1. [Konfigurera mål](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html) för delning av profilattribut och målgruppsmedlemskap till önskade mål.

## Relaterad dokumentation

* [Destinationsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)
* [Översikt över molnlagringsmål](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=en#catalog)
* [HTTP-mål](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/http-destination.html?lang=en#overview)
* [[!UICONTROL Kunddataplattform i realtid] Produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Riktlinjer för profil och segmentering](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Segmenteringsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)

## Relaterade videor och självstudiekurser

* [[!UICONTROL Kunddataplattform i realtid] - översikt](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [Demo av [!UICONTROL Kunddataplattform i realtid]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [Skapa segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
