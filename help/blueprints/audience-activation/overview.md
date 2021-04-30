---
title: Målgrupps- och profilaktivering
description: Leverera målgruppsanpassade och profilcentrerade kundupplevelser med kunddataplattformens ​ i realtid.
solution: Experience Platform, Real-time Customer Data Platform
kt: null
thumbnail: null
exl-id: eeeb4325-d0e8-4fd8-86ab-0b8afdd0b69f
translation-type: tm+mt
source-git-commit: 9e0954334e8b8a8c5bf52651611e7afa165f6d21
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 0%

---


# Målgrupps- och profilaktivering

Målgrupps- och profilaktivering är nyckeln till framgång i en datadriven marknadsföringsvärld. Men många varumärken fokuserar fortfarande på aktivering av kanaler först, vilket ofta ger inkonsekvent räckvidd och personalisering.

Med ett kanalbaserat första tillvägagångssätt fungerar varje kanal som en silo där personaliseringssatsningarna endast riktar sig till kunder som interagerar med varumärket i den kanalen. Detta tillvägagångssätt återspeglar inte den verklighet som kunderna interagerar med varumärken över många olika kontaktytor. Med aktivering av målgrupper och profiler kan varumärken koppla samman kundinteraktioner över flera kanaler för att leverera en centraliserad profil och målgrupp som kan aktiveras i alla kanaler.

| Blueprint | Beskrivning | Experience Cloud-program |
|---|---|---|
| **[Anonym Audience Activation](anonymous.md)** | <ul><li>Rikta er till målgrupper över webben och annonskanaler för anonyma och beteendemässiga kunddata.</li><li>Integrera med externa målgruppsdata för ökad personalisering.</li></ul> | <ul><li>Adobe Audience Manager</li></ul> |
| **[Online/offline Audience Activation](online-offline.md)** | <ul><li>Aktivera för kända profilbaserade destinationer, som e-postleverantörer, sociala nätverk och reklamdestinationer. </li><li>Använd offlineattribut och händelser som offlineorder, transaktioner, CRM eller lojalitetsdata tillsammans med onlinebeteende för målinriktning och personalisering.</li></ul> | <ul><li>Adobe Experience Platform</li><li> [!UICONTROL Kunddataplattform i realtid]</li><li>Adobe Audience Manager (valfritt)</li></ul> |
| **[Målgrupps- och profilaktivering för företagsdestinationer](enterprise-destinations.md)** | <ul><li>Replikering och uppdatering av profiler och målgruppsändringar i företagets datalager för aktivering och rapportering av användningsfall. </li></ul><ul><li>Initiera en försäljnings- eller supportåtgärd till kunden genom att meddela en kundåtgärd från [!UICONTROL kunddataplattformen ] i realtid till företagssystem och företagstillämpningar.</li></ul> | <ul><li>Adobe Experience Platform</li><li>[!UICONTROL Kunddataplattform i realtid]</li><li>Aktivering av Experience Platform</li><li>Adobe Audience Manager (valfritt)</li></ul> |
| **[Kundaktivitetshubb](customer-activity.md)** | <ul><li>Ge kunderna ett djupare sammanhang för interaktioner som stöds av agenter, som support och säljupplevelser. Med profilsökningen i Experience Platform kan agenterna få mer kontext om konsumenten, t.ex. senaste köp, kampanjinteraktioner, egenskaper, målgruppsmedlemskap och andra attribut och insikter som lagras i kundprofilen i realtid.</li></ul> | <ul><li>Adobe Experience Platform</li></ul> |

## GuarDRATIONS for Audience and Profile Activation Blueprints

* [Riktlinjer för profil och segmentering](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)

### Gardrutor för segmentutvärdering och aktivering

| Segmenteringstyp | Frekvens | Genomflöde | Latens (segmentutvärdering) | Latens (segmentaktivering) | Aktiveringsnyttolast |
|-|-|-|-|-|-|-
| Kantsegmentering | Kantsegmentering är för närvarande en betaversion och gör det möjligt att utvärdera giltig segmentering i realtid i Experience Platform Edge Network för att fatta beslut i realtid via Adobe Target och Adobe Journey Optimizer. |  | ~100 millisekunder | Finns omedelbart för personalisering i Adobe Target, profilsökningar i Edge Profile och för aktivering via cookie-baserade destinationer. | Målgruppsmedlemskap finns på Edge för profilsökningar och cookie-baserade destinationer.<br>Målgruppsmedlemskap och profilattribut är tillgängliga för Adobe Target och Journey Optimizer.  |
| Direktuppspelningssegmentering | Varje gång en ny direktuppspelningshändelse eller post hämtas till kundprofilen i realtid och segmentdefinitionen är ett giltigt direktuppspelningssegment. <br>Se  [segmenteringsdokumentationen ](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html) för vägledning om kriterier för direktuppspelningssegment | Upp till 1 500 händelser per sekund.  | ~ p95 &lt; 5 minuter | Direktuppspelningsmål: Medlemskap för direktuppspelande målgrupper aktiveras inom ungefär 10 minuter eller mikrobatchas baserat på kraven för destinationen.<br>Schemalagda destinationer: Medlemskap för direktuppspelande målgrupper aktiveras i batch baserat på den schemalagda leveranstiden för destinationen. | Direktuppspelningsmål: Ändringar av målgruppsmedlemskap, identitetsvärden och profilattribut.<br>Schemalagda destinationer: Ändringar av målgruppsmedlemskap, identitetsvärden och profilattribut. |
| Inkrementell segmentering | En gång per timme för nya data som har importerats till kundprofilen i realtid sedan den senaste stegvisa utvärderingen eller utvärderingen av batchsegment. |  |  | Direktuppspelningsmål: Medlemskap för flera målgrupper aktiveras inom ungefär 10 minuter eller mikrobatchas baserat på destinationens krav.<br>Schemalagda destinationer: Inkrementella målgruppsmedlemskap aktiveras gruppvis baserat på den schemalagda leveranstiden för destinationen. | Direktuppspelningsmål: Endast ändringar av målgruppsmedlemskap och identitetsvärden.<br>Schemalagda destinationer: Ändringar av målgruppsmedlemskap, identitetsvärden och profilattribut. |
| Gruppsegmentering | En gång per dag baserat på ett förbestämt systemschema, eller manuellt initierat ad ad hoc via API. |  | Ungefär en timme per jobb för upp till 10 terabyte profilliststorlek, 2 timmar per jobb för 10 terabyte till 100 terabytes profilagestorlek. Batchsegmentets jobbprestanda beror på talprofiler, profilstorlek och antalet segment som utvärderas. | Direktuppspelningsmål: Medlemskap för gruppanvändare aktiveras inom ungefär 10 dagar efter det att segmenteringsutvärderingen har slutförts eller mikrobatchvis baserat på destinationens krav.<br>Schemalagda destinationer: Batchmålgruppsmedlemskap aktiveras baserat på den schemalagda leveranstiden för destinationen. | Direktuppspelningsmål: Endast ändringar av målgruppsmedlemskap och identitetsvärden.<br>Schemalagda destinationer: Ändringar av målgruppsmedlemskap, identitetsvärden och profilattribut. |

### GuarDRAils for Cross Application Audience Sharing

| Målgruppsintegrering | Frekvens | Genomflöde/volym | Latens (segmentutvärdering) | Latens (segmentaktivering) |
|-|-|-|-|-|-
| Kunddataplattform i realtid till Audience Manager | Beroende på segmenteringstyp - se tabellen ovan över skyddsutkast för segmentering. | Beroende på segmenteringstyp - se tabellen ovan över skyddsutkast för segmentering. | Beroende på segmenteringstyp - se tabellen ovan över skyddsutkast för segmentering. | Inom några minuter efter det att segmentutvärderingen har slutförts.<br>Initial målgruppskonfigurationssynkronisering mellan kunddataplattformen i realtid och Audience Manager tar ca 4 timmar.<br>Alla målgruppsmedlemskap som realiseras under 4-timmarsperioden kommer att skrivas till Audience Manager i det efterföljande gruppsegmenteringsjobbet som&quot;befintliga&quot; målgruppsmedlemskap. |
| Kunddataplattform i realtid till Ad Cloud | Observera att delning av målgrupper från kunddataplattformen i realtid till Adobe Advertising Cloud kräver Audience Manager. Samma skyddsräcken som gäller för delning av kunddataplattform i realtid till Audience Manager kommer att användas för integrering av målgrupper i kunddataplattformen i realtid till Advertising Cloud. | - |-  | - |
| Adobe Analytics till kunddataplattform i realtid | Inte tillgängligt för tillfället | Inte tillgängligt för tillfället | Inte tillgängligt för tillfället | Inte tillgängligt för tillfället |
| Adobe Analytics till Audience Manager |-  | Som standard kan högst 75 målgrupper delas för varje Adobe Analytics-rapportserie. Om en Audience Manager-licens används finns det ingen gräns för hur många målgrupper som kan delas mellan Adobe Analytics och Adobe Target eller Adobe Audience Manager och Adobe Target. | - |-  |


### Garantier för aktivering av attribut och identiteter

* [!UICONTROL Real-time Customer Data ] Platform kan aktivera målgruppsmedlemskap samt attribut- och identitetsändringar som sker för profiler som är medlemmar i segment som valts för aktivering. Om målet är att aktivera attribut eller identiteter måste du definiera ett globalt segment som innehåller alla profiler som attribut- och identitetsuppdateringar skickas till. Då kan du markera segmentet och de attribut du vill aktivera som en del av målkonfigurationen.
* Observera att batchdestinationer inte stöder aktivering av endast attributändringar. Fullständigt eller inkrementellt medlemskap kan skickas tillsammans med de valda attributen för aktivering, men du kan inte aktivera endast attributspecifika ändringshändelser via batchdestinationer.

Aktivera batchsegment för direktuppspelningsmål

* Aktivering av gruppsegment till direktuppspelningsmål stöds. Batchsegmentjobb skickar meddelanden i pipeline när segmentjobbet är klart för direktuppspelningsaktivering

Aktivera direktuppspelningssegment för batchmål

* Direktuppspelning av segmentaktivering till batchmål stöds. Batchmålschemat exporterar profilsegmentsmedlemskap baserat på batchmålschemat. Detta inkluderar både segmentmedlemskap som bestäms via direktuppspelning och gruppmetoder.

Aktivera upplevelsehändelser

* Aktivering av raw-upplevelsehändelser stöds inte. För att aktivera mot upplevelsehändelser måste ett segment skapas med nödvändiga regler som inkluderar eller exkluderar logiken för upplevelsehändelser. Detta skapar ett segment som definieras mot upplevelsehändelser och segmentmedlemskapet kan aktiveras som en proxy för aktivering av raw-upplevelsehändelser. Överväg också att använda [!UICONTROL Starta serversidan] för att aktivera obearbetade upplevelsehändelser som samlats in via SDK.


## Relaterade blogginlägg

* [[!DNL Blueprints for Audience Activation in Adobe Experience Platform]](https://medium.com/adobetech/a-blueprint-for-audience-activation-in-adobe-experience-platform-b2b30fae90fd)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
