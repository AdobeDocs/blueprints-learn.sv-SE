---
title: Online/Offline Audience Activation-utkast
description: Online/offline Audience Activation.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
translation-type: tm+mt
source-git-commit: da21d1796eb9a2c9c0f087d82606874ca55bd4ea
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Online/Offline Audience Activation-utkast

Använd offlineattribut och händelser som offlineorder, transaktioner, CRM eller lojalitetsdata, tillsammans med onlinebeteende för målinriktning och personalisering.

Aktivera målgrupper för kända profilbaserade destinationer som e-postleverantörer, sociala nätverk och reklamdestinationer.

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

### Online/offline Audience Activation med Experience Cloud-program

<img src="assets/activation+apps.svg" alt="Referensarkitektur för online-/offlineutkast för Audience Activation med Experience Cloud-program" style="border:1px solid #4a4a4a" />

## Guardrails

Se skyddsutkastet på sidan Översikt över målgrupps- och profilaktivering - [LINK](overview.md)

## Implementeringssteg

1. Konfigurera scheman och datauppsättningar i Experience Platform.
1. Konfigurera rätt identiteter och identitetsnamnutrymmen i schemat för att säkerställa att inkapslade data kan sammanfogas till en enhetlig profil.
1. Aktivera schema och datauppsättningar för profil.
1. Importera data till Platform.
1. Tillhandahåll [!UICONTROL Kunddataplattform för realtid] för segmentdelning mellan Experience Platform och Audience Manager för målgrupper som definieras i Experience Platform som ska delas med Audience Manager.
1. Skapa segment i Experience Platform som ska utvärderas i batch eller direktuppspelning. Systemet avgör automatiskt om segmentet utvärderas som batch eller direktuppspelning.
1. Konfigurera mål för delning av profilattribut och målgruppsmedlemskap till önskade mål.

## Överväganden gällande implementering

* När du delar profildata till mål måste du inkludera det specifika identitetsvärde som används av målet i målnyttolasten. Alla identiteter som är nödvändiga för ett målmål måste hämtas till Platform och konfigureras som en identitet för [!UICONTROL kundprofilen ] i realtid.

* För aktiveringsscenarier där målgrupper delas från Experience Platform till Audience Manager delas alla identiteter som ingår i [!UICONTROL kundprofilen i realtid] till Audience Manager. Målgrupper från Experience Platform kan delas via Audience Manager när de nödvändiga destinationsidentiteterna ingår i [!UICONTROL kundprofilen i realtid], eller där identiteter i [!UICONTROL kundprofilen i realtid] kan relateras till de önskade destinationsidentiteterna som är länkade i Audience Manager.

## Relaterad dokumentation

* [[!UICONTROL Beskrivning av kunddataplattform ] i realtid](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Riktlinjer för profil och segmentering](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Segmenteringsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Destinationsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)

## Relaterade videor och Tutorials

* [[!UICONTROL Kunddata ] Platformoverview i realtid](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [Demo av  [!UICONTROL kunddataplattform i realtid]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [Skapa segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
