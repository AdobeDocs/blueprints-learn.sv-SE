---
title: Online/Offline Audience Activation-utkast
description: Online/offline Audience Activation.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
translation-type: tm+mt
source-git-commit: db083e30d8add029e99cade25d561a26da78338e
workflow-type: tm+mt
source-wordcount: '1040'
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

<img src="assets/onoff.svg" alt="Referensarkitektur för utkast online/offline i Audience Activation" style="border:1px solid #4a4a4a" />

## Guardrails

* [Riktlinjer för profil och segmentering](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)

### Gardrutor för segmentutvärdering och aktivering

| Segmenteringstyp | Frekvens | Genomflöde | Latens (segmentutvärdering) | Latens (segmentaktivering) | Aktiveringsnyttolast |
|---|---|---|---|---|---|
| Kantsegmentering | Kantsegmentering är för närvarande en betaversion och gör det möjligt att utvärdera giltig segmentering i realtid i Experience Platform Edge Network för att fatta beslut i realtid via Adobe Target och Adobe Journey Optimizer. |  | ~100 ms | Finns omedelbart för personalisering i Adobe Target, profilsökningar i Edge Profile och aktivering via cookie-baserade destinationer. | Målgruppsmedlemskap finns på Edge för profilsökningar och cookie-baserade destinationer.<br>Målgruppsmedlemskap och profilattribut är tillgängliga för Adobe Target och Journey Optimizer. |
| Strömmande segmentering | Varje gång en ny direktuppspelningshändelse eller inspelning hämtas till kundprofilen i realtid och segmentdefinitionen är ett giltigt direktuppspelningssegment. <br>Se  [segmenteringsdokumentationen ](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html) för vägledning om kriterier för direktuppspelningssegment | Upp till 1 500 händelser per sekund. | ~ p95 &lt;5min | Direktuppspelningsmål: Medlemskap för direktuppspelande målgrupper aktiveras inom ungefär 10 minuter eller mikrobatchas baserat på kraven för destinationen.<br>Schemalagda destinationer: Medlemskap för direktuppspelande målgrupper aktiveras i batch baserat på den schemalagda leveranstiden för destinationen. | Direktuppspelningsmål: Ändringar av målgruppsmedlemskap, identitetsvärden och profilattribut.<br>Schemalagda destinationer: Ändringar av målgruppsmedlemskap, identitetsvärden och profilattribut. |
| Inkrementell segmentering | En gång i timmen för nya data som har importerats till kundprofilen i realtid sedan den senaste stegvisa utvärderingen eller utvärderingen av batchsegment. |  |  | Direktuppspelningsmål: Medlemskap för flera målgrupper aktiveras inom ungefär 10 minuter eller mikrobatchas baserat på destinationens krav.<br>Schemalagda destinationer: Inkrementella målgruppsmedlemskap aktiveras i batch baserat på den schemalagda leveranstiden för destinationen. | Direktuppspelningsmål: Endast ändringar av målgruppsmedlemskap och identitetsvärden.<br>Schemalagda destinationer: Ändringar av målgruppsmedlemskap, identitetsvärden och profilattribut. |
| Gruppsegmentering | En gång per dag baserat på ett förbestämt systemschema, eller manuellt initierat ad ad hoc via API. |  | Ungefär en timme per jobb för upp till 10 TB profibutik, 2 timmar per jobb för 10 TB till 100 TB profillagringsstorlek. Batchsegmentets jobbprestanda beror på talprofiler, profilstorlek och antalet segment som utvärderas. | Direktuppspelningsmål: Medlemskap för gruppanvändare aktiveras inom ungefär 10 dagar efter det att segmenteringsutvärderingen har slutförts eller mikrobatchvis baserat på destinationens krav.<br>Schemalagda destinationer: Batchmålgruppsmedlemskap aktiveras baserat på den schemalagda leveranstiden för destinationen. | Direktuppspelningsmål: Endast ändringar av målgruppsmedlemskap och identitetsvärden.<br>Schemalagda destinationer: Ändringar av målgruppsmedlemskap, identitetsvärden och profilattribut. |

### GuarDRAils for Cross Application Audience Sharing

| Målgruppsintegrering | Frekvens | Genomströmning/volym | Latens (segmentutvärdering) | Latens (segmentaktivering) |
|---|---|---|---|---|
| Kunddataplattform i realtid till Audience Manager | Beroende på segmenteringstyp - se tabellen med segmenteringsskyddsutkast. | Beroende på segmenteringstyp - se tabellen med segmenteringsskyddsutkast. | Beroende på segmenteringstyp - se tabellen med segmenteringsskyddsutkast. | Inom några minuter efter det att segmentutvärderingen har slutförts.<br>Initial målgruppskonfigurationssynkronisering mellan kunddataplattformen i realtid och Audience Manager tar ca 4 timmar.<br>Alla målgruppsmedlemskap som realiseras under 4-timmarsperioden kommer att skrivas till Audience Manager i det efterföljande gruppsegmenteringsjobbet som&quot;befintliga&quot; målgruppsmedlemskap. |
| Kunddataplattform i realtid till Ad Cloud | Observera att delning av målgrupper från kunddataplattformen i realtid till Adobe Advertising Cloud kräver Audience Manager. Samma skyddsräcken som gäller för delning av kunddataplattform i realtid till Audience Manager kommer att användas för integrering av målgrupper i kunddataplattformen i realtid till Advertising Cloud. | - | - | - |
| Adobe Analytics till kunddataplattform i realtid | Inte tillgängligt för tillfället | Inte tillgängligt för tillfället | Inte tillgängligt för tillfället | Inte tillgängligt för tillfället |
| Adobe Analytics till Audience Manager | - | Som standard kan högst 75 målgrupper delas för varje Adobe Analytics rapportserie. Om en Audience Manager-licens används finns det ingen gräns för hur många målgrupper som kan delas mellan Adobe Analytics och Adobe Target eller Adobe Audience Manager och Adobe Target. | - | - |






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
