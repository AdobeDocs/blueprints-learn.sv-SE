---
title: Målgrupps- och profilaktivering
description: Leverera målgruppsanpassade och profilcentrerade kundupplevelser med kunddataplattformens ​ i realtid.
solution: Experience Platform, Real-time Customer Data Platform
kt: null
thumbnail: null
exl-id: eeeb4325-d0e8-4fd8-86ab-0b8afdd0b69f
translation-type: tm+mt
source-git-commit: 5471d9c0f6fdef6fbac72d5d35f32353ea5a5ee8
workflow-type: tm+mt
source-wordcount: '678'
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
| **[Målgrupps- och profilaktivering med Experience Cloud-program](platform-and-applications.md)** | </ul><li>Hantera profiler och målgrupper i Experience Platform och dela dem med Experience Cloud-program</li><li>Bygg och dela avancerade kundsegment och insikter i Experience Platform och dela dem med Experience Cloud-tillämpningar</li></ul> | <ul><li>Adobe Experience Platform</li><li>[!UICONTROL Kunddataplattform i realtid]</li><li>Aktivering av Experience Platform</li><li>Experience Cloud-program</li></ul> |
| **[Kundaktivitetshubb](customer-activity.md)** | <ul><li>Ge kunderna ett djupare sammanhang för interaktioner som stöds av agenter, som support och säljupplevelser. Med profilsökningen i Experience Platform kan agenterna få mer kontext om konsumenten, t.ex. senaste köp, kampanjinteraktioner, egenskaper, målgruppsmedlemskap och andra attribut och insikter som lagras i kundprofilen i realtid.</li></ul> | <ul><li>Adobe Experience Platform</li></ul> |



## GuarDRATIONS for Audience and Profile Activation Blueprints

* [Riktlinjer för profil och segmentering](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)


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
