---
title: Online/Offline Audience Activation-utkast
description: Online/offline Audience Activation.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
source-git-commit: f527b23587e4ec893532997c3c99270946d7fa31
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Online/Offline Audience Activation-utkast

Använd offlineattribut och händelser som offlineorder, transaktioner, CRM eller lojalitetsdata, tillsammans med onlinebeteende för målinriktning och personalisering.

Aktivera målgrupper för kända profilbaserade destinationer som e-postleverantörer, sociala nätverk och reklamdestinationer.

Online-/offlinedesignen för Audience Activation är i linje med [målgrupps- och profilaktiveringen med Experience Cloud Applications Blueprint](platform-and-applications.md). Mer information finns i [Målgrupps- och profilaktivering med Experience Cloud Applications-utkast](platform-and-applications.md)   som är specifikt för integreringar mellan Experience Platform och Experience Cloud.

## Användningsexempel

* Målgruppsanpassning för kända målgrupper på sociala medier och reklamdestinationer.
* Anpassning online med online- och offlineattribut.
* Aktivera målgrupper för kända kanaler, som e-post och SMS.

## Program

* Adobe Experience Platform
* [!UICONTROL Kunddataplattform i realtid]

## Arkitektur

### Online/offline Audience Activation med destinationer

<img src="assets/online_offline_activation.svg" alt="Referensarkitektur för utkast online/offline i Audience Activation" style="border:1px solid #4a4a4a" />
<br>

## Guardrails

[Se skyddsutkastet på sidan Översikt över målgrupps- och profilaktivering.](overview.md)

## Implementeringssteg

1. [Skapa ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html) scheman för data som ska importeras.
1. [Skapa ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) datauppsättningar för data som ska importeras.
1. [Konfigurera rätt identiteter och ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html) identitetsnamnutrymmen i schemat för att säkerställa att inkapslade data kan sammanfogas till en enhetlig profil.
1. [Aktivera scheman och datauppsättningar för profilen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Ingest ](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) data into Experience Platform.
1. [Tillhandahåll  [!UICONTROL realtidsdelning av kunddata ] Platformsegment ](https://www.adobe.com/go/audiences) mellan Experience Platform och Audience Manager för målgrupper som definieras i Experience Platform som ska delas med Audience Manager.
1. [Skapa ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) segmentering i Experience Platform. Systemet avgör automatiskt om segmentet utvärderas som batch eller direktuppspelning.
1. [Konfigurera ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html) mål för delning av profilattribut och målgruppsmedlemskap till önskade mål.

## Överväganden gällande implementering

* När du delar profildata till mål måste du inkludera det specifika identitetsvärde som används av målet i målnyttolasten. Alla identiteter som är nödvändiga för ett målmål måste hämtas till Platform och konfigureras som en identitet för [!UICONTROL kundprofilen ] i realtid.

* För aktiveringsscenarier där målgrupper delas från Experience Platform till Audience Manager delas alla identiteter som ingår i [!UICONTROL kundprofilen i realtid] till Audience Manager. Målgrupper från Experience Platform kan delas via Audience Manager när de nödvändiga destinationsidentiteterna ingår i [!UICONTROL kundprofilen i realtid], eller där identiteter i [!UICONTROL kundprofilen i realtid] kan relateras till de önskade destinationsidentiteterna som är länkade i Audience Manager.

## Relaterad dokumentation

* [[!UICONTROL Beskrivning av kunddataplattform ] i realtidProduktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Riktlinjer för profil och segmentering](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Segmenteringsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Destinationsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)

## Relaterade videor och Tutorials

* [[!UICONTROL Kunddata ] Platformoverview i realtid](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [Demo av  [!UICONTROL kunddataplattform i realtid]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [Skapa segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
