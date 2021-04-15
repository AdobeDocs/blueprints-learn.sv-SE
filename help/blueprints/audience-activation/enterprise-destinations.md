---
title: Målgrupps- och profilaktivering för företagsdestinationer
description: Målgrupps- och profilaktivering för företagsdestinationer
solution: Experience Platform,Real-time Customer Data Platform
kt: 7475
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5,None
translation-type: tm+mt
source-git-commit: b0664edc3d29d693d33eefc3b3c6da8bf7308224
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# Målgrupps- och profilaktivering för företagsdestinationer

Dela profiler och målgruppsändringar och händelser i strömning eller batch från [!UICONTROL Kunddataplattform i realtid] till datalagring och applikationer för företag. Dessa profil- och målgruppshändelser kan användas för att initiera en sälj- eller supportåtgärd till kunden, som att följa upp en övergiven ansökningsprocess eller registrering av ett webbinarium eller för att uppdatera företagsapplikationer med de senaste kundattributen och intelligensen från [!UICONTROL Customer Data Platform] i realtid.

## Användningsexempel

* Profil- och målgruppsaktivering till molnlagringsdestinationer eller direktuppspelningsdestinationer för företagsspårning, lagring, analys och aktivering av kunddata och insikter.

## Program

* Adobe Experience Platform Activation

## Arkitektur

<img src="assets/enterprise_destination.svg" alt="Referensarkitektur för Enterprise Activation Scenario" style="border:1px solid #4a4a4a" />

## Guardrails

[Riktlinjer för profil och segmentering](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)

Tröskelvärden för fördröjning och genomströmning:

Direktuppspelningssegmentering:

* Upp till 5 minuter för direktuppspelningssegmentering, upp till 1 500 händelser per sekund
* Upp till 11 minuter för direktuppspelningsaktivering

Gruppsegmentering:
En gång per dag eller manuellt initierad ad ad hoc via API.

* Cirka 1 timme per jobb för upp till 10 TB profibutik
* Cirka 2 timmar per jobb för 10 TB till 100 TB profillagringsstorlek

## Implementeringssteg

1. Skapa scheman för data som ska importeras.
1. Skapa datauppsättningar för data som ska importeras.
1. Konfigurera rätt identiteter och identitetsnamnutrymmen i schemat för att säkerställa att inkapslade data kan sammanfogas till en enhetlig profil.
1. Aktivera scheman och datauppsättningar för profilbearbetning.
1. Konfigurera alla källor för dataöverföring.
1. Skapa segment i Experience Platform som ska utvärderas i batch eller direktuppspelning. Systemet avgör automatiskt om segmentet utvärderas som batch eller direktuppspelning.
1. Konfigurera mål för delning av profilattribut och målgruppsmedlemskap till önskade mål.

## Överväganden gällande implementering

Aktivera attribut och identiteter

* [!UICONTROL Real-time Customer Data ] Platform kan aktivera målgruppsmedlemskap samt attribut- och identitetsändringar som sker för profiler som är medlemmar i segment som valts för aktivering. Om målet är att aktivera attribut eller identiteter måste du definiera ett globalt segment som innehåller alla profiler som attribut- och identitetsuppdateringar skickas till. Då kan du markera segmentet och de attribut du vill aktivera som en del av målkonfigurationen.
* Observera att batchdestinationer inte stöder aktivering av endast attributändringar. Fullständigt eller inkrementellt medlemskap kan skickas tillsammans med de valda attributen för aktivering, men du kan inte aktivera endast attributspecifika ändringshändelser via batchdestinationer.

Aktivera batchsegment för direktuppspelningsmål

* Aktivering av gruppsegment till direktuppspelningsmål stöds. Batchsegmentjobb skickar meddelanden i pipeline när segmentjobbet är klart för direktuppspelningsaktivering

Aktivera direktuppspelningssegment för batchmål

* Direktuppspelning av segmentaktivering till batchmål stöds. Batchmålschemat exporterar profilsegmentsmedlemskap baserat på batchmålschemat. Detta inkluderar både segmentmedlemskap som bestäms via direktuppspelning och gruppmetoder.

Aktivera upplevelsehändelser

* Aktivering av raw-upplevelsehändelser stöds inte. För att aktivera mot upplevelsehändelser måste ett segment skapas med nödvändiga regler som inkluderar eller exkluderar logiken för upplevelsehändelser. Detta skapar ett segment som definieras mot upplevelsehändelser och segmentmedlemskapet kan aktiveras som en proxy för aktivering av raw-upplevelsehändelser. Överväg också att använda [!UICONTROL Starta serversidan] för att aktivera obearbetade upplevelsehändelser som samlats in via SDK.

## Relaterad dokumentation

* [Destinationsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)
* [Översikt över destinationer för molnlagring](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=en#catalog)
* [HTTP-mål](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/http-destination.html?lang=en#overview)
* [[!UICONTROL Beskrivning av kunddataplattform ] i realtid](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Riktlinjer för profil och segmentering](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Segmenteringsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)

## Relaterade videor och Tutorials

* [[!UICONTROL Kunddata ] Platformoverview i realtid](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [Demo av  [!UICONTROL kunddataplattform i realtid]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [Skapa segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
