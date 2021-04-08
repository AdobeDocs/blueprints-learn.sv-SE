---
title: Målgrupps- och profilaktivering för företagsdestinationer
description: Målgrupps- och profilaktivering för företagsdestinationer
solution: Experience Platform,Real-time Customer Data Platform
kt: 7475
exl-id: null
translation-type: tm+mt
source-git-commit: e9e8473f62fa222e483f7aeed33148433f1ec427
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---


# Målgrupps- och profilaktivering för företagsdestinationer

Replikering och uppdatering av profiler och målgruppsändringar i företagets datalager för aktivering och rapportering av användningsfall.

Initiera en försäljnings- eller supportåtgärd till kunden genom att informera om en kundåtgärd från kunddataplattformen i realtid till företagssystem och företagstillämpningar.

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
En gång per dag eller manuellt initierad ad ad hoc via API

* Cirka 1 timme per jobb för upp till 10 TB profibutik
* Cirka 2 timmar per jobb för 10 TB till 100 TB profillagringsstorlek

## Implementeringssteg

1. Skapa scheman för data som ska importeras
1. Skapa datauppsättningar för data som ska importeras
1. Konfigurera rätt identiteter och identitetsnamnutrymmen i schemat för att säkerställa att inkapslade data kan sammanfogas till en enhetlig profil.
1. Aktivera scheman och datauppsättningar för profilbearbetning.
1. Konfigurera källor för datainmatning
1. Skapa segment i Experience Platform som ska utvärderas i batch eller direktuppspelning. Systemet avgör automatiskt om segmentet utvärderas som batch eller direktuppspelning.
1. Konfigurera mål för delning av profilattribut och målgruppsmedlemskap till önskade mål.

## Överväganden gällande implementering

Aktivering av attribut och identiteter

* Real-time Customer Data Platform kan aktivera både målgruppsmedlemskap och attribut- och identitetsändringar som sker för profiler som är medlemmar i segment som har valts för aktivering. Om du vill aktivera attribut och/eller identiteter måste du definiera ett globalt segment som innehåller alla profiler som attribut-/identitetsuppdateringar ska skickas för. När detta är på plats kan segmentet och de attribut som ska aktiveras väljas som en del av målkonfigurationen.
* Observera att batchdestinationer inte stöder aktivering av bara attributändringshändelser. Målgruppsmedlemskapet är fullt eller inkrementellt och kan skickas tillsammans med de valda attributen för aktivering, men endast attribut kan inte aktiveras via batchdestinationer.

Aktivering av gruppsegment till direktuppspelningsmål

* Aktivering av gruppsegment till direktuppspelningsmål stöds. Batchsegmentjobb skickar meddelanden i pipeline när segmentjobbet är klart för direktuppspelningsaktivering

Direktuppspelning av segmentaktivering till batchmål

* Direktuppspelning av segmentaktivering till batchmål stöds. Målschemat för gruppen exporterar segmentmedlemskap för profilerna baserat på målschemat för gruppen. Detta inkluderar både segmentmedlemskap som bestäms via direktuppspelning och gruppmetoder.

Aktivering av upplevelsehändelser

* Aktivering av raw-upplevelsehändelser stöds för närvarande inte. För att aktivera mot upplevelsehändelser måste ett segment skapas med nödvändiga regler som inkluderar/exkluderar den händelslogik som ska aktiveras mot. Detta skapar ett segment som definieras mot upplevelsehändelser och segmentmedlemskapet kan aktiveras som en proxy för aktivering av raw-upplevelsehändelser. Överväg också att använda Launch Server Side för aktivering av obearbetade upplevelsehändelser som samlats in via SDK.

## Relaterad dokumentation

* [Destinationsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)
* [Lagringsmål för Enterprise Cloud](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=en#catalog)
* [HTTP-mål](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/http-destination.html?lang=en#overview)
* [Produktbeskrivning av kunddataplattform i realtid](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Riktlinjer för profil och segmentering](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Segmenteringsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)

## Relaterade videor och Tutorials

* [Översikt över Customer Data Platform i realtid](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [Demo av kunddataplattform i realtid](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [Skapa segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
