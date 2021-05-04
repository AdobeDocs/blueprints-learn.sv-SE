---
title: Målgrupps- och profilaktivering
description: Leverera målgruppsanpassade och profilcentrerade kundupplevelser med kunddataplattformens ​ i realtid.
solution: Experience Platform, Real-time Customer Data Platform
kt: null
thumbnail: null
exl-id: eeeb4325-d0e8-4fd8-86ab-0b8afdd0b69f
translation-type: tm+mt
source-git-commit: b5d8160235fb510642701ba066434d8bd226b464
workflow-type: tm+mt
source-wordcount: '1201'
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

### Guardrail-diagram

<img src="assets/activation_guardrails.svg" alt="GuarDRAL-diagram för målgrupps- och profilaktiveringsplaner" style="border:1px solid #4a4a4a" />



### Gardrutor för segmentutvärdering och aktivering

| Segmenteringstyp | Användningsexempel | Frekvens | Genomflöde | Latens (segmentutvärdering) | Latens (segmentaktivering) | Aktiveringsnyttolast |
|--------------------------|------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Kantsegmentering | Webb-/mobilpersonalisering (samma sida/nästa sida) | Kantsegmentering är för närvarande i betaversion och är ännu inte allmänt tillgänglig. | - | Cirka 100 millisekunder | Target och Journey Optimizer:<ul><li>Finns omedelbart i samma personaliseringsbegäran.</li></ul>Cookie-baserade destinationer:<ul><li>Tillgängligt för beslut om nästa sida.</li></ul> | Edge Profile Lookups (Target och Journey Optimizer):<ul><li>Målgruppsmedlemskap</li><li>Profilattribut</li></ul>Cookie-baserade destinationer:<ul><li>Målgruppsmedlemskap</li></ul> |
| Strömmande segmentering | Trigger Based Marketing (Streaming) | Varje gång en ny direktuppspelningshändelse eller inspelning hämtas till kundprofilen i realtid och segmentdefinitionen är ett giltigt direktuppspelningssegment. <br>Se segmenteringsdokumentationen för vägledning om  [segmentsegmentkriteriedokumentation för direktuppspelning](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html) | Upp till 1 500 händelser per sekund. | Ungefär 5 minuter, p95 | Direktuppspelningsmål:<ul><li>Ungefär 1 minut till Audience Manager och Target</li><li>Ungefär 10 minuter till externa destinationer eller mikrobatchvis beroende på destinationen.</li></ul>Schemalagda destinationer:<ul><li>Aktiverat till externa destinationer i batch baserat på den schemalagda leveranstiden för destinationen.</li></ul> | Direktuppspelningsmål: <ul><li>Ändringar av målgruppsmedlemskap</li><li>Identitetsvärden</li><li>Profilattribut</li></ul>Schemalagda destinationer:<ul><li>Ändringar av målgruppsmedlemskap</li><li>Identitetsvärden</li><li>Profilattribut</li></ul> |
| Inkrementell segmentering | <li>Batchmeddelanden<li>Målinriktade kampanjer och upplevelser | En gång i timmen för nya data som har importerats till kundprofilen i realtid sedan den senaste stegvisa utvärderingen eller utvärderingen av batchsegment. | Ej tillämpligt | Beroende på antal profiler, profilstorlek och antal segment som utvärderas. | Direktuppspelningsmål:<ul><li>Ungefär 1 minut till Audience Manager och Target</li><li>Ungefär 10 minuter till externa destinationer eller mikrobatchvis beroende på destinationen.</li></ul>Schemalagda destinationer:<ul><li>Aktiverat till externa destinationer i batch baserat på den schemalagda leveranstiden för destinationen.</li></ul> | Direktuppspelningsmål: <ul><li>Ändringar av målgruppsmedlemskap</li><li>Identitetsvärden</li></ul>Schemalagda destinationer:<ul><li>Ändringar av målgruppsmedlemskap</li><li>Identitetsvärden</li><li>Profilattribut</li></ul> |
| Gruppsegmentering | <ul><li>Batchmeddelanden</li><li>Målinriktade kampanjer och upplevelser</li></ul> | En gång per dag baserat på ett förbestämt systemschema, eller manuellt initierat ad ad hoc via API. | Ej tillämpligt | Beroende på antal profiler, profilstorlek och antal segment som utvärderas.<ul><li>Cirka en timme per jobb för upp till 10 TB profibutik</li><li>2 timmar per jobb för 10 TB till 100 TB profillagringsstorlek.</li></ul> | Direktuppspelningsmål:<ul><li>Ungefär 1 minut till Audience Manager och Target</li><li>Ungefär 10 minuter till externa destinationer eller mikrobatchvis beroende på destinationen.</li></ul>Schemalagda destinationer:<ul><li>Aktiverat till externa destinationer i batch baserat på den schemalagda leveranstiden för destinationen.</li></ul> | Direktuppspelningsmål: <ul><li>Ändringar av målgruppsmedlemskap</li><li>Identitetsvärden</li></ul>Schemalagda destinationer:<ul><li>Ändringar av målgruppsmedlemskap</li><li>Identitetsvärden</li><li>Profilattribut</li></ul> |

### GuarDRAils for Cross Application Audience Sharing

| Målgruppsintegrering | Användningsexempel | Frekvens | Genomflöde/volym | Latens (segmentutvärdering) | Latens (segmentaktivering) |
|-|-|-|-|-|-|-
| Kunddataplattform i realtid till Audience Manager | Berika tredjepartsannonsering med kända profilmålgrupper | Beroende på segmenteringstyp - se tabellen ovan över skyddsutkast för segmentering. | Beroende på segmenteringstyp - se tabellen ovan över skyddsutkast för segmentering. | Beroende på segmenteringstyp - se tabellen ovan över skyddsutkast för segmentering. | <ul><li>Inom några minuter efter det att segmentutvärderingen har slutförts.</li><li>Initial målgruppskonfigurationssynkronisering mellan RTCDP och AAM tar ca 4 timmar.</li><li>Alla målgruppsmedlemskap som realiseras under 4-timmarsperioden kommer att skrivas till AAM om det efterföljande batchsegmenteringsjobbet som&quot;befintliga&quot; målgruppsmedlemskap.</li></ul> |
| Adobe Analytics till Audience Manager | Förbättra tredjepartsannonsering med detaljbeteendebaserade målgrupper |  | Som standard kan högst 75 målgrupper delas för varje Adobe Analytics-rapportserie. Om en licens för Audience Manager används finns det ingen begränsning. |  |  |
| Adobe Analytics till kunddataplattform i realtid | Inte tillgängligt just nu. | Inte tillgängligt för tillfället | Inte tillgängligt för tillfället | Inte tillgängligt för tillfället | Inte tillgängligt för tillfället |


### Aktivera attribut och identiteter

* [!UICONTROL Real-time Customer Data ] Platform kan aktivera målgruppsmedlemskap samt attribut- och identitetsändringar som sker för profiler som är medlemmar i segment som valts för aktivering. Om målet är att aktivera attribut eller identiteter måste du definiera ett globalt segment som innehåller alla profiler som attribut- och identitetsuppdateringar skickas till. Då kan du markera segmentet och de attribut du vill aktivera som en del av målkonfigurationen.
* Observera att batchdestinationer inte stöder aktivering av endast attributändringar. Fullständigt eller inkrementellt medlemskap kan skickas tillsammans med de valda attributen för aktivering, men du kan inte aktivera endast attributspecifika ändringshändelser via batchdestinationer.

### Aktivera batchsegment för direktuppspelningsmål

* Aktivering av gruppsegment till direktuppspelningsmål stöds. Batchsegmentjobb skickar meddelanden i pipeline när segmentjobbet är klart för direktuppspelningsaktivering

### Aktivera direktuppspelningssegment för batchmål

* Direktuppspelning av segmentaktivering till batchmål stöds. Batchmålschemat exporterar profilsegmentsmedlemskap baserat på batchmålschemat. Detta inkluderar både segmentmedlemskap som bestäms via direktuppspelning och gruppmetoder.

### Aktivera upplevelsehändelser

* Aktivering av raw-upplevelsehändelser stöds inte. För att aktivera mot upplevelsehändelser måste ett segment skapas med nödvändiga regler som inkluderar eller exkluderar logiken för upplevelsehändelser. Detta skapar ett segment som definieras mot upplevelsehändelser och segmentmedlemskapet kan aktiveras som en proxy för aktivering av raw-upplevelsehändelser. Överväg också att använda [!UICONTROL Starta serversidan] för att aktivera obearbetade upplevelsehändelser som samlats in via SDK.


## Relaterade blogginlägg

* [[!DNL Blueprints for Audience Activation in Adobe Experience Platform]](https://medium.com/adobetech/a-blueprint-for-audience-activation-in-adobe-experience-platform-b2b30fae90fd)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
