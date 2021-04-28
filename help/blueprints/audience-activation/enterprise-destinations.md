---
title: Målgrupps- och profilaktivering för företagsdestinationer
description: Målgrupps- och profilaktivering för företagsdestinationer
solution: Experience Platform,Real-time Customer Data Platform
kt: 7475
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5,None
translation-type: tm+mt
source-git-commit: 3a4a0e2387e72d378589edfdc5b0c27a50c42db5
workflow-type: tm+mt
source-wordcount: '1003'
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

### Gardrutor för segmentutvärdering och aktivering

| Segmenteringstyp | Frekvens | Genomflöde | Latens (segmentutvärdering) | Latens (segmentaktivering) | Aktiveringsnyttolast |
|---|---|---|---|---|---|
| Kantsegmentering | Kantsegmentering är för närvarande en betaversion och gör det möjligt att utvärdera giltig segmentering i realtid i Experience Platform Edge Network för att fatta beslut i realtid via Adobe Target och Adobe Journey Optimizer. |  | ~100 ms | Finns omedelbart för personalisering i Adobe Target, profilsökningar i Edge Profile och aktivering via cookie-baserade destinationer. | Målgruppsmedlemskap finns på Edge för profilsökningar och cookie-baserade destinationer.<br>Målgruppsmedlemskap och profilattribut är tillgängliga för Adobe Target och Journey Optimizer. |
| Strömmande segmentering | Varje gång en ny direktuppspelningshändelse eller inspelning hämtas till kundprofilen i realtid och segmentdefinitionen är ett giltigt direktuppspelningssegment. <br>Se  [segmenteringsdokumentationen ](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html) för vägledning om kriterier för direktuppspelningssegment | Upp till 1 500 händelser per sekund. | ~ p95 &lt;5min | Direktuppspelningsmål: Medlemskap för direktuppspelande målgrupper aktiveras inom ungefär 10 minuter eller mikrobatchas baserat på kraven för destinationen.<br>Schemalagda destinationer: Medlemskap för direktuppspelande målgrupper aktiveras i batch baserat på den schemalagda leveranstiden för destinationen. | Direktuppspelningsmål: Ändringar av målgruppsmedlemskap, identitetsvärden och profilattribut.<br>Schemalagda destinationer: Ändringar av målgruppsmedlemskap, identitetsvärden och profilattribut. |
| Inkrementell segmentering | En gång i timmen för nya data som har importerats till kundprofilen i realtid sedan den senaste stegvisa utvärderingen eller utvärderingen av batchsegment. |  |  | Direktuppspelningsmål: Medlemskap för flera målgrupper aktiveras inom ungefär 10 minuter eller mikrobatchas baserat på destinationens krav.<br>Schemalagda destinationer: Inkrementella målgruppsmedlemskap aktiveras i batch baserat på den schemalagda leveranstiden för destinationen. | Direktuppspelningsmål: Endast ändringar av målgruppsmedlemskap och identitetsvärden.<br>Schemalagda destinationer: Ändringar av målgruppsmedlemskap, identitetsvärden och profilattribut. |
| Gruppsegmentering | En gång per dag baserat på ett förbestämt systemschema, eller manuellt initierat ad ad hoc via API. |  | Ungefär en timme per jobb för upp till 10 TB profibutik, 2 timmar per jobb för 10 TB till 100 TB profillagringsstorlek. Batchsegmentets jobbprestanda beror på talprofiler, profilstorlek och antalet segment som utvärderas. | Direktuppspelningsmål: Medlemskap för gruppanvändare aktiveras inom ungefär 10 dagar efter det att segmenteringsutvärderingen har slutförts eller mikrobatchvis baserat på destinationens krav.<br>Schemalagda destinationer: Batchmålgruppsmedlemskap aktiveras baserat på den schemalagda leveranstiden för destinationen. | Direktuppspelningsmål: Endast ändringar av målgruppsmedlemskap och identitetsvärden.<br>Schemalagda destinationer: Ändringar av målgruppsmedlemskap, identitetsvärden och profilattribut. |



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
