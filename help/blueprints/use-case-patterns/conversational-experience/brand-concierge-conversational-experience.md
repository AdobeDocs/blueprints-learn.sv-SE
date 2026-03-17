---
title: Brand Concierge Conversational Experience
description: Lär dig hur du omvandlar digitala resurser till varumärkesskyddade, AI-baserade konverteringsinsikter som vägleder kundupptäckt.
solution: Experience Platform, Real-Time Customer Data Platform
exl-id: a9545328-316d-446a-9308-18af61c58d1c
source-git-commit: ccfd8c987a0090ca690e15a4bd89f4d96ec9c01f
workflow-type: tm+mt
source-wordcount: '7239'
ht-degree: 0%

---

# Brand Concierge konversationsupplevelse

Den här guiden innehåller en omfattande implementeringsreferens för AI-baserade konversationsupplevelser som använder [!DNL Adobe Brand Concierge], integrerat med [!DNL Adobe Experience Platform] (AEP) och [!DNL Real-Time Customer Data Platform] ([!DNL RT-CDP]). Det är utformat för lösningsarkitekter, marknadsföringsteknologer och implementeringstekniker som behöver driftsätta varumärkessäkra konverteringsagenter för digitala resurser.

Det täcker alla användbara strategier för att skapa konversationsupplevelser, från produktrådgivningstabeller till kompletta navigeringsassistenter för webbplatser, med vägledning om när varje alternativ ska väljas. I planen behandlas agentkonfiguration, varumärkesstyrning, innehållsintegrering, distributionsstrategier, profilberikning från konversationssignaler och analysoptimering.

Med [!DNL Brand Concierge] kan varumärken distribuera intelligenta konverteringsagenter som förstår varumärkesuttrycket, få tillgång till godkända produktkataloger och innehåll, leverera personaliserade rekommendationer baserat på profildata i realtid och fånga upp återgivnings- och känslomässiga signaler i den enhetliga kundprofilen. Resultatet blir en konversation som känns naturlig och varumärkesanpassad samtidigt som organisationens förståelse för varje kund berikas.

## Använd ärendeöversikt

Organisationer försöker i allt större utsträckning omvandla statiska digitala upplevelser till dynamiska, AI-baserade konversationer som vägleder kunderna genom upptäckt, produkturval och köpbeslut. [!DNL Adobe Brand Concierge] åtgärdar detta genom att tillhandahålla ett samordnat konversationsbaserat AI-lager som ligger ovanpå befintliga digitala egenskaper, som drivs av AEP Agent Orchestrator.

Det här mönstret skiljer sig från traditionella chatbot-implementeringar eftersom det är inbyggt i AEP enhetliga profil, använder skyddsprofiler för varumärkesstyrning för att säkerställa att alla svar överensstämmer med varumärkesstandarder och skickar konversationssignaler tillbaka till kunddataplattformen för personalisering och aktivering i efterföljande led.

Målgruppen är digitala upplevelseteam, e-handelschefer, innehållsstrateger och marknadsföringsteknologer som behöver använda intelligenta konversationsupplevelser som driver engagemang, konvertering och profilberikning.

## Viktiga verksamhetsmål

Följande affärsmål stöds av det här användningsmönstret.

### Leverera personaliserade kundupplevelser

Skräddarsy innehåll, erbjudanden och budskap efter enskilda preferenser, beteenden och livscykelsteg.

**KPI:er:** engagemang, konverteringsgrader, kundnöjdhet (CSAT)

[Läs mer om hur ni levererar personaliserade kundupplevelser](/help/blueprints/business-objectives/customer-experience/deliver-personalized-customer-experiences.md)

### Förbättra kundengagemanget

Öka interaktionsfrekvensen och -djupet för alla digitala och fysiska kontaktytor.

**KPI:er:** engagemang, tid på (webb) sida, öppettider

[Läs mer om hur ni kan förbättra kundengagemanget](/help/blueprints/business-objectives/qualification-sales-b2b/improve-customer-engagement.md)

### Öka konverteringsgraden

Förbättra andelen besökare och presumtiva som utför önskade åtgärder, t.ex. inköp, registreringar eller inskickade formulär.

**KPI:er:** Konverteringshastigheter, Leadkonvertering, kostnad per lead

[Läs mer om hur man ökar konverteringsgraden](/help/blueprints/business-objectives/revenue-monetization/increase-conversion-rates.md)

### Skaffa nya kunder

Utöka kundbasen med riktade kampanjer, lookalike-målgrupper och optimering av betalda medier.

**KPI:er:** Merförsäljning/korsförsäljning %, Inkrementell intäkt, Kundens livstidsvärde

[Läs mer om hur man skaffar nya kunder](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

## Exempel på taktiska användningsfall

Följande scenarier visar hur mönstret kan användas i praktiken.

- **Produktidentifieringsassistent** - Distribuera en konversationsagent på produktlistningssidor som frågar kvalificerande frågor och minskar produktrekommendationerna baserat på kundens behov, önskemål och budget
- **Guided comparison advisor** - Hjälp kunderna att jämföra produkter sida vid sida genom naturlig dialog, där skillnaderna som är relevanta för deras angivna prioriteringar markeras
- **Storlek och anpassa kontur** - Stödja kunder med kläder eller skodon genom att välja storlek med hjälp av konversationsfrågor och svar, vilket minskar avkastningen och ökar inköpsförtroendet
- **Prenumerations- eller planväljare** - Gå igenom tjänstenivå eller prenumerationsplansalternativ med personaliserade rekommendationer baserat på användningsmönster och angivna behov
- **Webbplatsnavigeringsassistent** - Hjälp besökarna att hitta relevant innehåll, supportresurser eller produktkategorier baserat på deras angivna avsikt, vilket minskar avhoppsfrekvensen på komplexa webbplatser
- **Konsultation före köp** - Tillhandahåll avancerad inköpsvägledning (t.ex. elektronik, finansiella produkter, försäkring) genom konversationer som bygger på en rekommendation
- **Lojalitetsprogram** - Hjälp lojalitetsmedlemmar att upptäcka belöningar, förstå fördelarna med nivåer och hitta möjligheter till inlösen genom konversationsinteraktion
- **Återupptagen konversation** - Initiera proaktiv konversationsutåtgång för att returnera besökare baserat på tidigare bläddringshistorik eller övergivna kundvagnsobjekt
- **Eskalering av Live-agent med kontext** - Skicka smidigt komplexa frågor till säljare eller supportrepresentanter live samtidigt som konversationskontext och kundprofildata bevaras
- **Support och merförsäljning** - Engagera kunderna efter inköp med hjälp av installationshjälp, förslag på kompletterande produkter och incheckningar av kundnöjdhet via konversationskanaler

## Nyckeltal för prestanda

Följande nyckeltal hjälper till att mäta hur bra det här användningsmönstret är.

| KPI | Beskrivning | Mätningsmetod |
| --- | --- | --- |
| Samtalsengagemangsfrekvens | Procentandel besökare som startar och underhåller en konversation | Konversationer startade/berättigade sidvisningar |
| Slutförandefrekvens för konversation | Procentandel konversationer som når en meningsfull upplösning | Slutförda konversationer/konversationer har startats |
| Konverteringsgrad | Procentandel konversationer som leder till önskad åtgärd (inköp, registrering, lead-formulär) | Konverteringar från konversation/totalt antal konversationer |
| Genomsnittligt konversationsdjup | Antal svängningar per konversation, vilket anger engagemangskvalitet | Genomsnittligt antal meddelanden per session |
| Nöjda kunder (CSAT) | Poäng för nöjda konversationer utifrån feedback | Undersökningssvar eller klassificeringar av tummar upp/ned |
| Godkännandefrekvens för rekommendation | Procent av produktrekommendationer som accepterats eller klickats | Rekommendationer som verkställs / rekommendationer som administreras |
| Frekvens för Live Agent-felmeddelanden | Procentandel konversationer som eskalerats till direktsändare | Överlämningar/totalt antal konversationer |
| Profilökningsgrad | Procentandel konversationer som ger nya återgivnings- eller inställningssignaler | Förbättrade profiler/totala konversationer |
| Intäkter som påverkas av konversation | Inkomster från inköp där en [!DNL Brand Concierge]-konversation föregått konverteringen | Attributionsanalys för konversations-till-inköpsresor |
| Tid till lösning | Genomsnittlig varaktighet från konversationens början till upplösning eller överlämning | Tidsstämpelanalys över konversationshändelser |

## Använd skiftlägesmönster

**Brand Concierge samtalsupplevelse**

Omvandla digitala resurser till varumärkesskyddade, AI-baserade, konversationsupplevelser som vägleder kundupptäckt genom naturlig dialog, berikar profiler med intent- och känslomässiga signaler och levererar personaliserade produktrekommendationer.

**Funktionskedja:** Agentkonfiguration > Inställningar för varumärkesstyrning > Innehållsintegrering > Distribution av konversationsupplevelse > Profilberikning > Analys och optimering

## Tillämpningar

Följande program används för att implementera det här användningsmönstret.

- **[!DNL Brand Concierge]** - AI-styrt program för konversationsupplevelser som tillhandahåller agenten orchestrator, Product Advisor Agent, Site Advisory Agent, varumärkesstyrning och konversationsanalys
- **[!DNL Adobe Experience Platform] (AEP)** - En enhetlig datamall som tillhandahåller XDM-scheman, identitetsupplösning, kundprofiler i realtid och infrastruktur för datainsamling för konversationssignaler
- **[!DNL Real-Time CDP] ([!DNL RT-CDP])** - Kunddataplattform som tillhandahåller profilsökning i realtid för personaliserade konversationer, målgruppssegmentering från konversationssignaler och profilberikning med intent- och känslomedata

## Foundationsfunktioner

Följande grundläggande funktioner måste finnas för det här användningsmönstret. För varje funktion anger statusen om den vanligtvis är obligatorisk, antas vara förkonfigurerad eller inte tillämplig.

| Funktionen Foundation | Status | Vad måste finnas på plats | Experience League referens |
| --- | --- | --- | --- |
| Administration och styrning | Obligatoriskt | Sandlådan har etablerats med [!DNL Brand Concierge]-berättigande aktiverat; roller konfigurerade för konversationsbaserade upplevelseadministratörer, innehållshanterare och analysanvändare; ABAC-principer finns på plats för konversationsdata som innehåller PII-signaler eller känsliga kundsignaler | [Översikt över åtkomstkontroll](https://experienceleague.adobe.com/sv/docs/experience-platform/access-control/home) |
| Datamodellering och förberedelse | Obligatoriskt | XDM-scheman för konverteringshändelser (klassen ExperienceEvent med konversationsspecifika fältgrupper som fångar avsikt, känslouttryck, produktinteraktioner och överlämningshändelser), profilschema utökat med konverteringsalternativ och intent-attribut, sökschema för produktkatalog för avrundningsrekommendationer | [Översikt över XDM-systemet](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/home) |
| Datakällor och samling | Obligatoriskt | [!DNL Web SDK] eller [!DNL Mobile SDK] har konfigurerats med datastreams som cirkulerar konversationshändelsedata till datauppsättningar i AEP; [!DNL Edge Network]-integrering för händelsehantering i realtid under konversationer; produktkatalogdata som hämtas via källanslutningar eller batchmatning | [SDK - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/web-sdk/home) |
| Konfiguration av identitet och profil | Obligatoriskt | Identitetsnamnutrymmen har konfigurerats för besökaridentifiering (ECID för anonym, CRM-ID eller e-post för autentiserad), sammanslagningsprincip har konfigurerats med kantaktivering för profilsökning i realtid under konversationer, regler för identitetslänkning för konversationskontinuitet mellan enheter | [Översikt över identitetstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/home) |
| Målgruppsdefinition och segmentering | Antagen på plats | Målgrupper krävs inte för distribution av konversationer, men behövs för personaliserade konversationsstrategier (t.ex. tar kundsegment med högt värde emot olika konversationsflöden); direktuppspelning eller edge-utvärdering rekommenderas för personalisering av konversationer i realtid | [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/home) |

## Stödfunktioner

Följande funktioner förstärker det här användningsmönstret, men behövs inte för att köra kärnan.

| Stödfunktioner | Status | Varför det spelar någon roll | Experience League referens |
| --- | --- | --- | --- |
| Skapande av beräknat/härlett attribut | Rekommenderad | Samla in konversationssignaler i profilnivåattribut (t.ex. totala konversationer, dominerande produktintressen, genomsnittligt poängvärde) för användning i segmentering och personalisering i efterföljande led | [Översikt över beräknade attribut](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/computed-attributes/overview) |
| Livscykelhantering för data | Rekommenderad | Konfigurera lagringspolicyer för konversationshändelsedata, hantera samtycke för inspelning och profilering av konversationer och ge stöd för begäranden om borttagning av sekretess för konversationstryckningar | [Översikt över livscykelhantering av avancerade data](https://experienceleague.adobe.com/sv/docs/experience-platform/data-lifecycle/home) |
| Dataanvändningsetiketter och -tillämpning | Rekommenderad | Märk konversationsdatafält som innehåller PII-, känslo- eller avsiktssignaler; tillämpa styrningsprinciper som förhindrar att känsliga konversationsdata når obehöriga mål | [Datastyrningsöversikt](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/home) |
| Övervakning och observerbarhet | Rekommenderad | Övervaka händelseinmatningsledningar för konversationer, spåra hur många profiler som har berikats och få meddelanden om dataflödesfel som kan påverka konversationspersonaliseringens kvalitet | [Översikt över Insikter om observabilitet](https://experienceleague.adobe.com/sv/docs/experience-platform/observability/home) |
| Rapportering och analys | Ingår | Analysera konversationsprestanda, kundfeedback, konverteringsattribuering och agenteffektivitet med [!DNL Brand Concierge] inbyggda analyser och [!DNL CJA] för analys av konversationseffekter över flera kanaler | [CJA - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-overview/cja-overview) |

## Programfunktioner

I den här planen används följande funktioner från programfunktionskatalogen. Funktioner mappas till implementeringsfaser i stället för till numrerade steg.

### [!DNL Brand Concierge]

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Konfiguration av agent | Fas 1: Agentkonfiguration | Konfigurera [!DNL Brand Concierge]-agentens koordinator med agentspecialiseringar (produktrådgivare, platsanvisning) och basbeteendeinställningar |
| Inställningar för varumärkesstyrning | Fas 2: Inställningar för varumärkesstyrning | Definiera varumärkesröst, ton, meddelandeskydd, godkända innehållsgränser och förbjudna ämnen som formar all konverteringsinteraktion |
| Integrering av innehåll | Fas 3: Integrering av innehåll | Koppla samman varumärkesgodkända innehållskällor, inklusive AEM-innehåll, produktkataloger, kunskapsbanker och andra tillförlitliga data för att hitta rätt svar |
| Konfiguration av produktrådgivare | Fas 3: Integrering av innehåll | Konfigurera Product Advisor Agent för personaliserade produktrekommendationer, guidade jämförelser och varumärkesanpassade svarsleveranser |
| Konfiguration av platsanvisning | Fas 3: Integrering av innehåll | Konfigurera Site Advisory Agent för att förbättra navigeringen genom att anpassa interaktioner baserat på besökares beteende och avsiktssignaler |
| Driftsättning av konversationsupplevelser | Fas 4: Konversationsupplevelsedistribution | Distribuera konversationsupplevelser i alla kanaler som stöds (webb, mobilapp, anpassad SDK) med stöd för text och röstinteraktion |
| Hantering av lågkodsflöde | Fas 4: Konversationsupplevelsedistribution | Marknadsföringsteamen kan uppdatera konversationston, flöden och innehåll med hjälp av konfigureringsverktyg med låg kod |
| Profilberikning för konversationer | Fas 5: Profilberikning | Berika AEP kundprofiler med återgivning, känslouttryck, produkttillhörighet och beteendesignaler som samlats in under konversationer |
| Konversationsanalys | Fas 6: Analys och optimering | Övervaka interaktionsstatistik, kundfeedback, konverteringsdata och konversationskvalitet via inbyggda analysdashboards |
| Live Agent-handtag | Fas 4: Konversationsupplevelsedistribution | Konfigurera smidig leverans till säljare eller supporttekniker samtidigt som konversationen bevaras |

### [!DNL Real-Time CDP]

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Profilsökning i realtid | Fas 4: Konversationsupplevelsedistribution | Få tillgång till kundprofilattribut och segmentmedlemskap i realtid för att personalisera konversationsrespons baserat på kända kunddata |
| Profilberikning | Fas 5: Profilberikning | Förbättra profiler med beräknade attribut som härletts från konverteringsbeteenden (intent scores, sentiment trends, product affinity) |
| Målgruppsutvärdering | Fas 5: Profilberikning | Utvärdera målgruppsmedlemskap baserat på konversationssignaler för att möjliggöra målinriktning längre fram i kedjan av engagerade konversationssegment |

## Förutsättningar

Följande objekt måste finnas innan implementeringen börjar.

- [!DNL Adobe Brand Concierge]-berättigandet är aktivt för organisationen
- AEP- och [!DNL RT-CDP]-licenser har tilldelats med tillräcklig profil- och händelsenorättighet
- Riktlinjedokument för varumärken som definierar röst, ton, godkända meddelanden och förbjudna ämnen
- Produktkatalog eller innehållslager förberedda för integrering (AEM-resurser, PIM-data eller strukturerad produktfeed)
- Webbegenskaper som identifieras för användning av konversationsupplevelser med teknisk åtkomst för SDK-integrering
- Aktiv agentinfrastruktur tillgänglig om överlämning krävs (kontaktcenterplattform, CRM-integrering)
- Samtyckeshanteringsramverk finns på plats för datainhämtning och profilering via konversationer
- [!DNL Web SDK] eller [!DNL Mobile SDK] har redan distribuerats på målegenskaper (eller planerats för samtidig distribution)
- Intressentanpassning till konversationsomfånget (endast produktrådgivning, webbplatsnavigering eller båda)
- Integritet och juridisk granskning har slutförts för inhämtning och användning av konverteringsdata via AI

## Implementeringsalternativ

I följande avsnitt beskrivs olika sätt att implementera det här användningsmönstret.

### Alternativ A: Driftsättning av produktrådgivare

**Passar bäst för:** E-handels- och detaljhandelsorganisationer som fokuserar på guidad produktupptäckt, jämförelse och rekommendationer som driver konvertering och genomsnittligt ordervärde.

**Så här fungerar det:**

Product Advisor Agent har konfigurerats som primär konversationsspecialisering. Den kopplar samman med produktkatalogen, förstår produktattribut och relationer och vägleder kunderna genom en naturlig dialog för att komma fram till personaliserade rekommendationer. Medarbetaren använder skyddsprofiler för varumärkesstyrning för att säkerställa att rekommendationerna överensstämmer med affärsprioriteringarna (t.ex. marknadsföring av artiklar i lager, framhävning av marginalpositiva produkter).

Product Advisor kan integreras med kundprofilen i realtid för att få tillgång till inköpshistorik, webbläsarbeteende och inställningsdata, vilket möjliggör rekommendationer som tar hänsyn till vad kunden redan äger, har övervägt eller troligen kommer att behöva utifrån deras profil. Konversationer spelas in i takt med att upplevelsehändelser och intent-signaler kommer tillbaka till profilen för nedladdning.

**Viktiga överväganden:**

- Kräver en välstrukturerad produktkatalog med omfattande attributdata för effektiva rekommendationer
- Produktdata måste hållas aktuella för att undvika att rekommendera artiklar som inte finns i lager eller som inte längre används
- Varumärkesstyrningen måste definiera hur agenten hanterar konkurrensutsatta produktomnämnanden och prisjämförelser

**Fördelar:**

- Direkt ger mätbar intäktseffekt genom guidad köpkonvertering
- Minskar produktavkastningen genom bättre beslutsunderlag
- Hämtar värdefulla produkters affinitet och intent-signaler för personalisering i senare led
- Naturlig utvidgning av befintliga e-handelsupplevelser

**Begränsningar:**

- Kräver kontinuerligt underhåll och synkronisering av produktkataloger
- Begränsat till produktcentrerade konversationer; frågor om webbplatsnavigering kan vara oadresserade
- Effektiviteten beror på katalogdatakvaliteten och fullständigheten

**Experience League:**

- [Brand Concierge - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [Brand Concierge produktrådgivare](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/product-advisor)

### Alternativ B: Distribution av platsanvisning

**Passar bäst för:** Organisationer med komplexa digitala egenskaper (medier, finansiella tjänster, hälso- och sjukvård, teknik) där besökarna behöver navigeringshjälp för att hitta relevant innehåll, resurser eller självbetjäningsverktyg.

**Så här fungerar det:**

Site Advisory Agent är konfigurerad som primär konversationsspecialisering. Den indexerar webbplatsens innehållsstruktur, förstår sidrelationer och innehållskategorier och anpassar dess riktlinjer baserat på besökarens beteendesignaler och den angivna avsikten. När en besökare engagerar tolkar agenten sina behov och dirigerar dem till det mest relevanta innehållet, verktygen eller resurserna.

Platsanvisningen använder beteendesignaler i realtid (aktuell sida, hänvisningskälla, navigeringssökväg) i kombination med profildata (tidigare besök, innehållsinställningar, kundnivå) för att ge sammanhangsberoende navigeringshjälp. Detta är särskilt värdefullt på webbplatser med djupa innehållshierarkier, flera produktlinjer eller komplexa självbetjäningsarbetsflöden.

**Viktiga överväganden:**

- Kräver omfattande innehållsindexering och regelbunden omcrawlning när webbplatsinnehållet ändras
- Effektivare på webbplatser med stor innehållsbredd där besökarna ofta kämpar med att hitta det de behöver
- Märkesstyrning bör definiera omfångsgränser (vilka webbplatsområden agenten kan navigera till)

**Fördelar:**

- Minskar avhoppsfrekvensen och förbättrar innehållsidentifieringen på komplexa webbplatser
- Hämtar navigeringsavsiktssignaler som avslöjar luckor i innehållet och problem med användarupplevelsen
- Mindre komplex implementering än Product Advisor (ingen produktkatalogintegration krävs)
- Ger analysinsikter om vad besökare letar efter men inte kan hitta

**Begränsningar:**

- Mindre direkt kopplat till intäktskonvertering än produktfokuserade konversationer
- Kräver att innehållet är välstrukturerat och regelbundet uppdaterat för korrekt vägledning
- Kan behöva omskolning ofta i takt med att webbplatsens struktur utvecklas

**Experience League:**

- [Brand Concierge - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [Webbplatsrådgivare för Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/site-advisor)

### Alternativ C: Kombinerad produktrådgivare + Site Advisory-distribution

**Passar bäst för:** Organisationer som vill ha en omfattande konversationsupplevelse som omfattar både produktupptäckt och webbplatsnavigering, vanligen stora detaljhandels- eller B2C-varumärken med omfattande digitala egenskaper och olika besökaravsikter.

**Så här fungerar det:**

Både Product Advisor Agent och Site Advisory Agent har konfigurerats i [!DNL Brand Concierge]-koordinatorn. Agentorkestratorn använder avsiktsidentifiering för att dirigera konversationer till lämplig specialisering - produktrelaterade frågor går till produktrådgivare medan navigerings- och innehållssökningsfrågor går till Platsanvisning. Orchestrator hanterar sömlösa övergångar mellan specialföretag i en enda konversation.

Den här metoden ger den mest kompletta konversationsupplevelsen och hanterar alla besökarbehov från &quot;Hjälp mig att hitta en produkt&quot; till &quot;Var kan jag kontrollera min orderstatus?&quot; Varumärkesstyrningsgarantierna tillämpas enhetligt i båda specialiseringarna, vilket ger en enhetlig varumärkesröst oavsett vilket samtalsämne det gäller.

**Viktiga överväganden:**

- Komplexa implementeringar kräver integration av både produktkatalog och innehåll
- Avsiktsdirigering mellan specialiseringar måste vara väl anpassad för att undvika felriktade konversationer
- Varumärkesstyrningen är mer omfattande och omfattar både produkt- och navigeringssammanhang

**Fördelar:**

- Ger besökarna den mest omfattande konversationsupplevelsen
- En enda ingångspunkt hanterar olika besökaravsikter utan att kräva separata gränssnitt
- Konversationer om korsspecialisering (till exempel produktfråga som leder till navigeringsstöd) hanteras naturligt
- Avancerad profilberikning från olika konversationssignaler

**Begränsningar:**

- Högsta implementeringsinsats och pågående underhåll
- Kräver samordning mellan produktkataloger och innehållsteam
- Mer komplexa tester och krav på kvalitetssäkring
- Varumärkesstyrningskonfigurationen är mer involverad

**Experience League:**

- [Brand Concierge - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)

### Jämförelse av alternativ

| Kriterier | Alternativ A: Produktrådgivare | Alternativ B: Platsanvisning | Alternativ C: Kombinerat |
| --- | --- | --- | --- |
| Bäst för | E-handel, produktdriven konvertering | Innehållskrävande webbplatser, självbetjäningsnavigering | En fullständig digital upplevelse |
| Komplex | Medelsvåra: | Låg-Medium | Högt |
| Tid till värde | 4-6 veckor | 3-5 veckor | 6-10 veckor |
| Inkomstpåverkan | Hög (direkt konverteringseffekt) | Medium (indirekt via engagemang) | Högsta (både konvertering och engagemang) |
| Innehållskrav | Produktkatalog med omfattande attribut | Webbplatsinnehållsindex | Både produktkatalog och innehållsindex |
| Profilberikning | Produkttillhörighet, inköpsmetod | Navigeringsmetod, innehållsinställningar | Fullständigt signalspektrum |
| Underhållsarbete | Synkronisering av produktkatalog | Omindexering av innehåll | Båda pågående |

### Välj rätt alternativ

Börja med att utvärdera ditt primära affärsmål och egenskaper för digital egendom:

1. **Om ditt primära mål är att öka produktkonverteringen** och din digitala egenskap är inriktad på handel väljer du **Alternativ A (produktrådgivare)**. Detta är den vanligaste utgångspunkten för varumärken inom detaljhandeln och e-handeln.

2. **Om ditt primära mål är att förbättra innehållsidentifieringen** och din webbplats har djupa innehållshierarkier eller komplexa självbetjäningsarbetsflöden väljer du **Alternativ B (Platsanvisning)**. Detta är idealiskt för medie-, finans-, sjukvårds- och teknikföretag.

3. **Om du behöver omfattande täckning** och har behov av både produkthandel och innehållsnavigering väljer du **Alternativ C (kombinerat)**. Överväg att börja med en specialisering och lägga till den andra efter att den första är stabil och optimerad.

Ett stegvis tillvägagångssätt rekommenderas för de flesta organisationer: distribuera först en specialisering, validera prestanda och samla in inlärningar, och sedan utöka den till en kombinerad driftsättning.

## Implementeringsfaser

I följande faser beskrivs den rekommenderade implementeringssekvensen.

### Fas 1: Agentkonfiguration

**Programfunktion:** [!DNL Brand Concierge]: Agentkonfiguration

Konfigurera huvudagentens [!DNL Brand Concierge]-koordinator, inklusive val av agentspecialiseringar (produktrådgivare, platsrådgivning eller båda), konfigurering av basagentbeteende och etablering av anslutningen mellan [!DNL Brand Concierge] och AEP för profilåtkomst och händelsehämtning.

#### Beslut: Val av agentspecialisering

Avgör vilka agentspecialiseringar som ska aktiveras för den här distributionen.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Endast produktrådgivare | Commerce-fokuserad driftsättning för produktupptäckt och konvertering | Kräver integration med produktkataloger, snabbaste väg till intäktseffekt |
| Endast platsanvisning | Innehåll och navigeringsinriktad driftsättning | Lägre komplexitet vad gäller integration; bäst för icke-handelsplatser |
| Båda specialiseringarna | Omfattande samtalstäckning för produkter och innehåll | Högre komplexitet - överväg fasad utrullning som börjar med en |

#### Beslut: Initieringsmodell för konversation

Bestäm hur konversationer ska börja med den digitala egenskapen.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Besökarinitierad (passiv) | Standardmetod där chattwidgeten är tillgänglig men inte aktivt | Lägre risk för avbrott; förlitar sig på besökarens medvetenhet om chattalternativet |
| Proaktivt engagemang (utlöses) | Agenten startar en konversation baserad på beteendesignaler (t.ex. längre uppehållstid, upprepade sidbesök, vagnsseftersitation) | Högre engagemangsgrad men riskerar besökarnas irritation om utlösarna är för aggressiva; kräver beteendeanpassning |
| Hybrid (passiv med sammanhangsberoende uppmaningar) | Chattwidgeten är passiv men visar sammanhangsberoende uppmaningar baserat på sidinnehåll eller besökarbeteende | Balanserad strategi - guide för uppmaningar utan att tvinga engagemang |

#### Konfigurera agenten

**Gränssnittsnavigering:** [!DNL Experience Platform] > AI-assistenten > [!DNL Brand Concierge] > Agentkonfiguration

Information om nyckelkonfiguration:

- Definiera agentnamnet och beskrivningen som ska visas i konversationsgränssnittet
- Välj vilken AEP-sandlåda som innehåller kundprofil och händelsedata som agenten ska komma åt
- Konfigurera agentens koordinator för att dirigera frågor mellan specialiseringar baserat på avsiktsidentifiering
- Ange parametrar för konversationssession (tidsgräns, maximal konversationslängd, gräns för samtidiga sessioner)
- Aktivera integrering av profilsökning i realtid så att agenten kan komma åt besökarprofildata under konversationer

**Var alternativen skiljer sig:**

**För alternativ A (produktrådgivare):**
Aktivera produktAdvisor-specialiseringen och konfigurera anslutningen till produktkatalogens datakälla. Ange produktrekommendationsparametrar, inklusive maximala rekommendationer per svar, visningsinställningar för produktattribut och regler för jämförelsehantering.

**För alternativ B (Platsanvisning):**
Aktivera specialiseringen för platsanvisning och konfigurera anslutningen till webbplatsens innehållsindex. Ange navigeringsparametrar, inklusive innehållsomfångsgränser, hantering av sidkategorier och inställningar för generering av djuplänkar.

**För alternativ C (kombinerat):**
Aktivera båda specialiseringarna och konfigurera orchestrators intent routing logic. Definiera routningsregler som bestämmer när en konversation ska hanteras av produktrådgivare eller Site Advisory, och hur övergångar mellan specialiseringar ska hanteras i en enda konversation.

**Experience League-dokumentation:**

- [Brand Concierge - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [Översikt över AI Assistant](https://experienceleague.adobe.com/sv/docs/experience-platform/ai-assistant/home)
- [AEP Agent Orchestrator](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)

### Fas 2: Inställningar för varumärkesstyrning

**Programfunktion:** [!DNL Brand Concierge]: Inställningar för varumärkesstyrning

Konfigurera skyddsmekanismer för varumärkesstyrning som formar alla konversationsinteraktioner. Detta inkluderar varumärkesuttryck och tondefinitioner, godkända innehållsgränser, förbjudna ämnen, riktlinjer för svarsformat och eskaleringsregler. Varumärkesstyrningen säkerställer att alla AI-genererade lösningar följer varumärkesstandarderna.

#### Beslut: Styrningens stränghetsnivå

Bestäm hur nära varumärkesstyrningsgarantierna ska begränsa konverteringsgraden.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Strikta styrelseformer | Högreglerade branscher (finansiella tjänster, hälso- och sjukvård, försäkring) eller premiumvarumärken som kräver exakt tonkontroll | Begränsar konverteringsgraden; kan leda till mer frekventa&quot;jag kan inte hjälpa till med det&quot;-svar; högsta varumärkessäkerhet |
| Modernt styre | De flesta konsumentvarumärken där varumärkets röst är enhetlig men viss konverteringsflexibilitet är godtagbar | En god balans mellan varumärkessäkerhet och konversationsnatur; rekommenderad utgångspunkt för de flesta implementeringar |
| Flexibel styrning | Varumärken med vardagslivet eller livsstil där konverteringsförmåga och engagemang prioriteras | Den mest naturliga konverteringskänslan; kräver mer kontinuerlig övervakning för respons utanför varumärket |

#### Beslut: Strategi för hantering utanför ämnet

Bestäm hur agenten ska hantera frågor utanför det konfigurerade omfånget.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Omdirigera till omfång | Agenten bekräftar frågan och omdirigerar till ämnen som kan vara till hjälp med | Upprätthåller engagemanget men kan frustrera besökare med legitima ämnesrelaterade behov |
| Leverans till Live Agent | Agenten erbjuder att ansluta besökaren till en handläggare för frågor utanför ämnet | Bästa kundupplevelse men kräver infrastruktur och personal för medarbetare live |
| Skarp nedgång med resurser | Agent förklarar att det inte kan hjälpa till med det ämnet och tillhandahåller länkar till relevanta resurser eller supportkanaler | Låg friktionsåterfall; kräver inte tillgång till livesjälp |

#### Konfigurera varumärkesstyrning

**Gränssnittsnavigering:** [!DNL Experience Platform] > AI-assistenten > [!DNL Brand Concierge] > Märkesstyrning

Information om nyckelkonfiguration:

- Definiera varumärkesattribut: varumärkesnamn, tagline, uppdrag, värderingar och personlighetsattribut som bygger på konverteringsgraden
- Ange färgtonsparametrar: formalitetsnivå, humörtolerans, empatinivå och tillförlitlighet för produktrekommendationer
- Konfigurera godkända innehållsgränser: ämnen som agenten har behörighet att diskutera och ämnen som uttryckligen är förbjudna
- Definiera riktlinjer för svarsformat: maximal svarslängd, användning av listor kontra pros, emoji-princip och länkformatering
- Ställa in eskaleringsutlösare: villkor som automatiskt ska dirigera en konversation till en handläggare (t.ex. för att upptäcka klagomål, upprepade missnöjessignaler, kundidentifiering med högt värde)
- Konfigurera konkurrenskraftig omnämnandehantering: hur agenten ska svara när besökare frågar om konkurrentprodukter
- Definiera ansvarsfriskrivning och krav på rättslig underrättelse: obligatorisk information för reglerade branscher

**Experience League-dokumentation:**

- [Brand Concierge varumärkesstyrning](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [AI Assistant - driftsinsikter](https://experienceleague.adobe.com/sv/docs/experience-platform/ai-assistant/home)

### Fas 3: Integrering av innehåll

**Programfunktion:** [!DNL Brand Concierge]: Innehållsintegrering, Konfiguration av produktrådgivare, Konfiguration av platsanvisning

Konfigurera de innehållskällor som ligger till grund för konversationsrespons i korrekt, varumärkesgodkänd information. Detta omfattar integration av produktkataloger, AEM innehållsanslutningar, import av kunskapsbaser och scheman för uppdatering av innehåll.

#### Beslut: Integreringsmetod för produktkatalog

Bestäm hur produktdata ska skickas till Product Advisor Agent. (Endast alternativ A och C)

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Integrering av AEP dataset | Produktkatalogen har redan importerats till AEP som en uppslagsdatauppsättning via källanslutningar | Utnyttjar befintlig datainfrastruktur; håller produktdata synkroniserade med profildata; kräver grundläggande datamodellering och datainsamling för att inkludera produktkatalog |
| Integrering med direktflöden | Produktkatalogen finns på en PIM- eller e-handelsplattform som kan tillhandahålla en strukturerad feed | Kan erbjuda mer realtidslager och prisdata; kräver konfiguration och planering av flöden |
| Integrering med AEM Content | Produktinnehåll hanteras i AEM och bör fungera som den officiella produktdatakällan | Passar bäst för varumärken där AEM är innehållsnavet; säkerställer enhetlighet mellan webbinnehåll och konverteringssvar |

#### Beslut: Frekvens för innehållsuppdatering

Bestäm hur ofta agentens kunskapsbas för innehåll ska uppdateras.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Realtid/nästan realtid | Produktens tillgänglighet, pris eller innehåll ändras ofta (till exempel blixtförsäljning, lagerkänslig detaljhandel) | Högsta noggrannhet men högre infrastrukturbelastning; kritisk för lagerkänsliga rekommendationer |
| Daglig uppdatering | Innehållsändringar är planerade och schemalagda (t.ex. redaktionella kalendrar, veckokampanjer) | Bra balans mellan noggrannhet och prestanda, lämplig för de flesta implementeringar |
| Uppdatera on demand | Innehållsändringar är ovanliga och kan aktiveras manuellt när uppdateringar sker | Lägsta overhead, lämplig för statiska produktkataloger eller stabila innehållsplatser |

#### Konfigurera innehållskällor

**Gränssnittsnavigering:** [!DNL Experience Platform] > AI-assistenten > [!DNL Brand Concierge] > Innehållskällor

Information om nyckelkonfiguration:

- Koppla samman datakällor i produktkatalogen med fältmappning för produktnamn, beskrivning, attribut, prissättning, tillgänglighet, bilder och kategorihierarki
- Konfigurera innehållsindexering för webbplatssidor, kunskapsbasartiklar, innehåll med vanliga frågor och support
- Ange innehållsomfångsgränser som definierar vilket innehåll agenten kan referera till och vilket som ska exkluderas
- Konfigurera återgångsbeteende för innehåll när agenten inte kan hitta relevant innehåll för att svara på en fråga
- Ställ in regler för innehållskvalitet: lägsta konfidensgräns för innehåll som ska inkluderas i svar, källattribut och källattribuering

**Var alternativen skiljer sig:**

**För alternativ A (produktrådgivare):**
Fokusera på produktkatalogintegrering med avancerad produktattributsmappning. Konfigurera Product Advisor Agent rekommendationslogik, inklusive hur många produkter som ska föreslås, hur artiklar som inte finns i lager ska hanteras, hur produktjämförelser ska presenteras och hur kundprofildata (inköpshistorik, webbläsarbeteende) ska inkluderas i rekommendationsrankningen.

**För alternativ B (Platsanvisning):**
Fokusera på indexering av webbplatsinnehåll med sidhierarkimappning. Konfigurera navigeringslogiken för Site Advisory Agent, bland annat hur besökaravsikten tolkas, vilka innehållskategorier som ska prioriteras, hur tvetydiga navigeringsbegäranden ska hanteras och hur förslag ska anpassas baserat på besökarens aktuella sidsammanhang och sessionsbeteende.

**För alternativ C (kombinerat):**
Konfigurera både produktkataloger och webbplatsinnehållskällor. Se till att innehållsroutningslogiken tilldelar innehåll till rätt specialisering och att korsreferenser mellan produktinnehåll och webbplatsens navigeringsinnehåll mappas korrekt.

**Experience League-dokumentation:**

- [Brand Concierge content configuration](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [Brand Concierge produktrådgivare](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/product-advisor)
- [Webbplatsrådgivare för Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/site-advisor)
- [Översikt över källor](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/home)

### Fas 4: Konversationsupplevelsedistribution

**Programfunktion:** [!DNL Brand Concierge]: Distribuering av konversationsupplevelser, lågkodsflödeshantering, Live Agent-leverans; [!DNL RT-CDP]: Profilsökning i realtid

Distribuera konversationsupplevelsen på digitala målegenskaper, inklusive kanalkonfiguration, anpassning av widgetar, integrering av profilsökningar för personalisering, regler för live-agenthantering och lågkodsverktyg för kontinuerlig innehållshantering.

#### Beslut: Distributionskanal

Bestäm vilka kanaler som konversationsupplevelsen ska distribueras till.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Webb (inbäddad widget) | Primär webbegenskap är den viktigaste kontaktytan för kunderna | Den vanligaste startpunkten; kräver integrering med [!DNL Web SDK]; stöder både anonyma och autentiserade besökare |
| Mobilapp (SDK-integrering) | Mobilappen är en viktig kanal för kundengagemang | Kräver integrering med [!DNL Mobile SDK]. Ta hänsyn till begränsningar för skärmutrymme för konversationsgränssnittet |
| Anpassad driftsättning av SDK | Konversationsupplevelsen måste vara inbäddad i en anpassad applikation, kioskdator eller icke-standard digital egenskap | Maximal flexibilitet; kräver större utvecklingsinsatser; lämpligt för kioskdatorer i butiken eller egna plattformar |
| Flerkanalsdistribution | Konversationsupplevelser krävs för webben, mobiler och andra kanaler samtidigt | Största räckvidd; kräver enhetlig varumärkesstyrning över alla kanaler; konversationskontexten ska finnas över alla kanaler när det är möjligt |

#### Beslut: Personalization djupgående konversationer

Bestäm hur mycket kundprofildata agenten ska använda för att personalisera konversationer.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Endast anonym (sessionskontext) | Integritet först eller när de flesta besökare är oidentifierade | Använder endast beteendesignaler under session; ingen profilsökning krävs; lämplig för anonym produktupptäckt |
| Profilmedveten (autentiserade besökare) | Besökarna är vanligtvis inloggade och personaliserade rekommendationer baserade på historik ger mervärde | Kräver profilsökning i realtid via [!DNL RT-CDP]; avsevärt bättre rekommendationskvalitet för kända kunder |
| Progressiv personalisering | Blandning av anonyma och autentiserade med progressiv profiluppbyggnad under konversation | Börjar med sessionskontext; registrerar sig som besökare som tillhandahåller information eller autentisering; balanserar sekretess och personalisering |

#### Beslut: Konfiguration av Live Agent-hantering

Bestäm om konversationer ska kunna eskaleras till människor.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Ingen beställning (endast självbetjäning) | AI-agenten kan hantera alla förväntade konversationstyper, eller så är direktagenter inte tillgängliga | Enklast driftsättning; kan frustrera besökare med komplexa behov; lämpligt för lågriskscenarier med produktbläddring |
| Regelbaserad leverans | Specifika utlösare bör eskalera till aktiva agenter (t.ex. för att upptäcka klagomål, värdefulla kunder, komplexa förfrågningar) | Förutsägbart eskaleringsbeteende; kräver att eskaleringsregler och -utlösare definieras; kräver integrering med Agentplattform |
| Begärd överlämning av besökare | Besökare kan begära en live-agent när som helst i konversationen | Bästa kundupplevelse; kräver alltid tillgänglig agentpersonal eller köhantering; konversationskontext måste överföras |

#### Distribuera konversationsupplevelsen

**Gränssnittsnavigering:** [!DNL Experience Platform] > AI-assistenten > [!DNL Brand Concierge] > Distribution

Information om nyckelkonfiguration:

- Konfigurera konversationswidgetens utseende: position, färgschema, avatar, välkomstmeddelande och interaktionsformat (text, röst eller båda)
- Integrera med [!DNL Web SDK] eller [!DNL Mobile SDK] för att hämta händelser och profilmatchning
- Konfigurera profilsökning i realtid för att få åtkomst till kundattribut, segmentmedlemskap och senaste aktiviteter under konversationer
- Ställ in integrering med direktsänd agent för kontaktcenterplattformen, inklusive protokoll för kontextöverföring, köroutning och agentmeddelanden
- Använd lågkodsflödeshanteringsverktyg för att uppdatera startsidor för konversationer, kampanjmeddelanden, säsongsinnehåll och flödesvariationer utan att utvecklaren behöver göra något
- Konfigurera regler för konversationssessionens beständighet: hur lång konversationshistorik behålls, om konversationer kan återupptas mellan sessioner och kontinuitet för konversationer mellan olika enheter

**Experience League-dokumentation:**

- [Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [SDK - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/web-sdk/home)
- [Edge Network Server API - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/edge-network-server-api/overview)
- [Slutpunkt för profil-API-entiteter](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/api/entities)
- [Översikt över kundprofiler i realtid](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/home)

### Fas 5: Profilberikning

**Programfunktion:** [!DNL Brand Concierge]: Konversationsprofilsaktivering; [!DNL RT-CDP]: Profilberikning, målgruppsutvärdering

Konfigurera den pipeline för hämtning och berikning som skickar konversationssignaler tillbaka till AEP enhetliga kundprofil. Detta inkluderar mappning av konversationshändelser till XDM, extrahering av intent- och känslomässiga signaler, skapande av beräknade attribut från konversationsdata och byggande av målgrupper baserat på konversationsbeteenden.

#### Beslut: Omfång för konverteringssignalmottagning

Bestäm vilka konversationssignaler som ska hämtas och skrivas till kundprofilen.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Endast viktiga engagemangssignaler | Minimal profilberikning; inledande, avslutande, varaktighet och slutförandestatus för konversation | Lägsta datavolym, tillräcklig för grundläggande analys, begränsat personaliseringsvärde |
| Återgivnings- och inställningssignaler | Fånga upp produktintressen, angivna preferenser och temakategorier som diskuteras | Högt personaliseringsvärde; måttlig datavolym; oftast rekommenderad |
| Fullständig signalinhämtning | Fånga avsikter, känslouttryck, produktinteraktioner, rekommendationssvar, överlämningshändelser och feedback-resultat | Avancerad profilberikning, högsta datavolym, möjliggör avancerad analys och ML-driven personalisering |

#### Beslut: Målgruppsgenerering av konversationsdata

Avgör om målgrupper ska skapas baserat på konversationsbeteenden för aktivering längre fram i kedjan.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Inga konversationsmålgrupper | Konversationsdata används endast för analys, inte för målgruppsaktivering | Det enklaste tillvägagångssättet - lämpligt om konversationer är ett komplement till befintliga engagemangskanaler |
| Avsiktsbaserade målgrupper | Skapa målgrupper baserat på angivna produktintressen eller navigeringsmetoder från konversationer | Möjliggör återmarknadsföring av besökare som visat intresse men inte konverterat; högt värde för e-handel |
| Beteendemålgrupper | Skapa målgrupper baserat på konversationsengagemangsmönster (till exempel högt engagemang, övergivna samtal, upprepade besök) | Möjliggör konversationsbaserad resesamordning och uppföljning över flera kanaler |

#### Konfigurera profilberikning

**Gränssnittsnavigering:** [!DNL Experience Platform] > Kund > Profiler > Beräknade attribut (för härledda signaler); Kund > Publiker > Skapa målgrupp (för konversationsmålgrupper)

Information om nyckelkonfiguration:

- Mappa konversationshändelser till XDM ExperienceEvent-schemafält som fångar konversations-ID, antal meddelanden, ämnen som diskuterats, refererade produkter, attitydpoäng och lösningsstatus
- Konfigurera profilberikning för [!DNL Brand Concierge] för att skriva återgivnings- och inställningssignaler till den enhetliga profilen
- Skapa beräknade attribut utifrån konversationshändelsedata: totalt antal konversationer (livstid), intresse i dominerande produktkategori (30 dagar), genomsnittligt poängvärde (90 dagar), konverteringsgrad konversation-till-köp
- Definiera strömnings- eller gruppmålgruppssegment baserat på konversationssignaler för aktivering längre fram i kedjan (t.ex.&quot;Besökare som diskuterat produktkategori X de senaste 7 dagarna men inte köpt&quot;)
- Validera profilberikning genom att leta upp exempelprofiler för att bekräfta att konversationsattributen har fyllts i

**Experience League-dokumentation:**

- [Översikt över beräknade attribut](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/computed-attributes/overview)
- [Användargränssnittshandbok för beräknade attribut](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/computed-attributes/ui)
- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/ui/segment-builder)
- [Direktuppspelningssegmentering](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Översikt över kundprofiler i realtid](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/home)

### Fas 6: Analys och optimering

**Programfunktion:** [!DNL Brand Concierge]: Konversationsanalys

Ställ in kontrollpaneler för analys och rapportering för att mäta konversationsupplevelsers prestanda, identifiera optimeringsmöjligheter och spåra nyckeltal. Detta inkluderar [!DNL Brand Concierge] inbyggda analyser, valfri [!DNL CJA]-integrering för konsekvensanalys för flerkanalskonversationer och pågående optimeringsarbetsflöden.

#### Beslut: Analysdjup

Bestäm vilken nivå av konversationsanalys som behövs.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Inbyggd [!DNL Brand Concierge]-analys | Standardrapportering om konversationsvolym, engagemang, nöjdhet och konvertering är tillräckligt | Snabbast att aktivera; omfattar nyckeltal; begränsad korrelation mellan kanaler |
| Integrering av [!DNL Brand Concierge] + [!DNL CJA] | Flerkanalsanalys krävs för att förstå hur konversationer påverkar större kundresor | Kräver [!DNL CJA] anslutning och datavykonfiguration; aktiverar attribueringsanalys över konversationer och andra kanaler |
| Fullständig analysstack ([!DNL Brand Concierge] + [!DNL CJA] + anpassade kontrollpaneler) | Rapportering på ledningsnivå, avancerad attribueringsmodellering och anpassad målgruppsgenerering från analysinsikter | Högsta analysfunktioner; kräver [!DNL CJA] expertkunskaper; möjliggör datadriven konversationsoptimering |

#### Konfigurera analys och optimering

**Gränssnittsnavigering:** [!DNL Experience Platform] > AI-assistenten > [!DNL Brand Concierge] > Analytics; [!DNL Analytics Platform] > Workspace (för [!DNL CJA])

Information om nyckelkonfiguration:

- Granska [!DNL Brand Concierge] inbyggda kontrollpaneler för analys: konversationsvolymer, engagemangsfrekvens, slutförandegrad, CSAT-poäng, accepteringsgrad för rekommendationer och överlämningsfrekvens
- Konfigurera anslutningen [!DNL CJA] så att den inkluderar konversationshändelsedatauppsättningar för flerkanalsanalys (om du väljer integrering med [!DNL CJA])
- Skapa [!DNL CJA]-arbetsyteanalys för attribuering av konversation till konvertering, som identifierar vilka konversationsämnen som korrelerar med inköpsbeteende
- Konfigurera övervakning av konversationskvalitet: spåra ämnen där agenten kämpar, vanliga obesvarade frågor och känslouttrender över tid
- Definiera optimeringsarbetsflöden: regelbundna granskningsrundor för uppdateringar av varumärkesstyrningen, utlösare för uppdatering av innehåll och förbättringar av konversationsflödet baserat på analysinformation

**Experience League-dokumentation:**

- [Brand Concierge Analytics](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [CJA Analysis Workspace - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/home)
- [Skapa eller redigera en CJA-anslutning](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-connections/create-connection)
- [Skapa eller redigera en datavy för CJA](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/create-dataview)

## Implementeringsöverväganden

Följande avsnitt behandlar skyddsförslag, vanliga fallgropar, bästa praxis och avbrottsbeslut som ska beaktas vid implementeringen.

### Gardrutor och begränsningar

- [!DNL Brand Concierge] konversationsupplevelser omfattas av hastighetsgränser för generering av AI-svar. Den samtidiga konversationskapaciteten beror på behörighetsnivån
- Profilsökning i realtid under konversationer omfattas av hastighetsbegränsningar för profil-API per sandlåda - [Kundprofilsgardinsnivå i realtid](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/guardrails)
- Inmatning av konversationsdata följer AEP standardgränser för direktuppspelning av inmatning: [Inmatningsskydd](https://experienceleague.adobe.com/sv/docs/experience-platform/ingestion/guardrails)
- Produktkatalogens storlek och innehållsindexvolymen omfattas av [!DNL Brand Concierge] innehållsintegreringsgränser
- Maximalt 25 beräknade attribut per sandlåda gäller för konverteringssignalaggregeringar - [Beräknade attributskyddsdetaljer](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/computed-attributes/overview)
- Maximalt 4 000 segmentdefinitioner per sandlåda gäller för konversationsmålgrupper - [Segmenteringsskydd](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/guardrails)

### Vanliga fallgropar

- **Otillräcklig definition av varumärkesstyrning:** Distribuering utan en grundlig konfiguration av varumärkesstyrning resulterar i svar utanför varumärket som skadar kundförtroendet. Investera mycket tid i fas 2 för att definiera ton, gränser och eskaleringsregler före driftsättningen.
- **Inaktuella produktkatalogdata:** ProduktAdvisor-rekommendationer som baseras på inaktuella lager-, prissättnings- eller tillgänglighetsdata frustrerar kunderna och undergräver förtroendet. Upprätta automatiska pipelines för uppdatering av innehåll med valideringskontroller.
- **Överaggressiva proaktiva interaktionsutlösare:** Om beteendet anges aktiveras för aggressivt (till exempel utlöses konversationer efter 3 sekunder på sidan) irriteras besökarna och studsfrekvensen ökar. Börja med försiktiga triggers och trimma baserat på engagemangsdata.
- **Negativ anonym besökarupplevelse:** Om personalisering bara fokuseras på autentiserade besökare ignoreras merparten av trafiken. Designa konversationsflöden som tillför värde till anonyma besökare med beteendesignaler.
- **Hoppar över konfiguration för profilberikning:** Distribuering av konversationer utan att hämta signaler tillbaka till profilen tar bort värdefulla återgivnings- och inställningsdata. Konfigurera profilberikning parallellt med distributionen, inte som en eftertanke.
- **Ignorerar direktsänd agentupplevelse:** Dåliga överlämningsupplevelser (förlorade sammanhang, upprepade frågor, långa väntetider) skadar den övergripande konversationsupplevelsen mer än att inte erbjuda överlämning alls. Testa hela överföringen från början till slut innan du startar programmet.

### God praxis

- Börja med en enda agentspecialisering (Product Advisor eller Site Advisory) och utöka efter att du har fastställt baslinjeprestanda.
- Genomför varumärkesstyrningsworkshops med intressenter inom marknadsföring, juridik och kundupplevelser innan du konfigurerar skyddsutkast.
- Använd progressiv personalisering: starta konversationer med sessionskontextbaserade svar och fördjupa personaliseringen när besökaren tillhandahåller information eller autentiserar.
- Implementera A/B-testning av startsidor för konversationer, uppmaningar och rekommendationspresentationer med hjälp av lågkodsflödeshanteringsverktygen.
- Schemalägg regelbunden (veckovis eller varannan vecka) granskning av konversationsanalyser för att identifiera innehållsluckor, vanliga felpunkter och optimeringsmöjligheter.
- Skapa en rundgång mellan konversationsanalyser och uppdateringar för varumärkesstyrning - använd konversationsdata för att förfina tonen, lägga till nya godkända ämnen och justera eskaleringsregler.
- Övervaka konversationstrender som ett tidigt varningssystem för produktproblem, webbplatsproblem eller förändringar i varumärkesuppfattningen.
- Designkonversationsflöden som naturligt fångar in profilberikande signaler utan att få interaktionen att kännas som en förhör.

### Avvecklingsbeslut

>[!NOTE]
>Följande beslut om avräkning bör utvärderas baserat på organisationens specifika krav och begränsningar.

**Personalisering av konversationer i detalj jämfört med enkelhet inom sekretess**

Djupare profilintegrering möjliggör mer personaliserade och effektiva konversationer, men ökar komplexiteten i datainsamlingen, kraven på samtycke och kraven på efterlevnad av sekretesskrav.

- **Omfattande personalisering prioriterar:** Högre konverteringsgrad, bättre rekommendationskvalitet, bättre profilberikning och mer engagerande konversationer för återkommande kunder
- **Enkelhet i integritetsfrågor gynnar:** Snabbare driftsättning, enklare hantering av samtycke, lägre regelkrav och varumärkespositionering för sekretess
- **Rekommendation:** Börja med progressiv personalisering som fungerar bra för anonyma besökare och lägger till profilbaserad personalisering för autentiserade sessioner. Detta ger värde på alla identifieringsnivåer samtidigt som sekretessen förblir hanterbar. Implementera inhämtning av samtycke för konversationsprofilering som är anpassad efter befintliga medgivanderamar.

**Styrka varumärkesstyrning jämfört med konversationsljud**

Strikta säkerhetsdetaljer för varumärkesstyrning säkerställer att alla åtgärder är anpassade efter varumärkesstandarder, men alltför stelbenta begränsningar gör att konversationerna känns robotiska och minskar engagemanget.

- **Strikta styrelsefördelar:** Varumärkessäkerhet, regelefterlevnad, konsekventa meddelanden och förutsägbart agentbeteende
- **Flexibel styrning prioriterar:** Naturligt konversationsflöde, högre engagemang, bättre kundnöjdhet och möjlighet att hantera fler frågor
- **Rekommendation:** Börja med måttlig styrning och dra ihop eller slappna av baserat på konversationsanalys. Övervaka frekvensen av&quot;Jag kan inte hjälpa till med det&quot;-svar som en indikator på överbegränsning. Använd lågkodsflödeshanteringsverktygen för att snabbt iterera i styrningsinställningar utan att utvecklaren behöver göra något.

**Innehållsuppdatering i realtid jämfört med systemprestanda**

Synkronisering av innehåll i realtid säkerställer att agenten alltid har aktuella produkt- och innehållsdata, men kontinuerlig uppdatering förbrukar fler infrastrukturresurser och kan skapa latens.

- **Uppdatering i realtid prioriterar:** Noggrannhet för lagerkänsliga rekommendationer, tidskänsliga kampanjer och snabbt föränderligt innehåll
- **Schemalagd uppdatering prioriterar:** Systemstabilitet, förutsägbar resursförbrukning och lägre infrastrukturkostnader
- **Rekommendation:** Använd daglig innehållsuppdatering som standard, med nästan realtidsuppdatering bara för lagertillgänglighet och prisdata som väsentligen påverkar kundupplevelsen. Övervaka mätvärden för innehållets exakthet för att avgöra om uppdateringsfrekvensen är tillräcklig.

**Omfattande signalinhämtning jämfört med datahanteringsinformation**

Genom att hämta in alla konverteringssignaler får du tillgång till den mest omfattande profilberikning och analys, men du får större datavolym, lagringskostnader och komplexitet när det gäller styrning.

- **Fullständig signalinhämtning prioriterar:** Avancerad analys, ML-modellutbildning, omfattande profilberikning och maximalt personaliseringsvärde längre fram i kedjan
- **Selektiv hämtning prioriterar:** Lägre lagringskostnader, enklare datastyrning, snabbare prestanda för profilsökning och enklare efterlevnad av datamängdsprinciper
- **Rekommendation:** Börja med avsiktsregistrering och inhämtning av inställningssignaler (mellangrunden) och utöka till fullständig signalinhämtning först när du har verifierat att ytterligare data skapar mätbart värde längre fram i kedjan. Använd datauppsättningens utgångsprofiler på konversationshändelsedata för att hantera lagringstillväxten.

## Relaterad dokumentation

Följande resurser innehåller ytterligare information för implementering av det här användningsmönstret.

**[!DNL Brand Concierge]**

- [Brand Concierge - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [Brand Concierge produktrådgivare](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/product-advisor)
- [Webbplatsrådgivare för Brand Concierge](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/site-advisor)
- [Översikt över AI Assistant](https://experienceleague.adobe.com/sv/docs/experience-platform/ai-assistant/home)

**[!DNL Adobe Experience Platform]**

- [AEP - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/landing/home)
- [XDM - systemöversikt](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/home)
- [Grundläggande om schemakomposition](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/schema/composition)
- [Översikt över kundprofiler i realtid](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/home)

**Datainsamling och integrering**

- [SDK - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/web-sdk/home)
- [Mobile SDK - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Konfigurera datastreams](https://experienceleague.adobe.com/sv/docs/experience-platform/datastreams/configure)
- [Edge Network Server API - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/edge-network-server-api/overview)
- [Översikt över källor](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/home)

**Identitet och profil**

- [Översikt över identitetstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/home)
- [Översikt över namnutrymmen för identiteter](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/features/namespaces)
- [Översikt över kopplingsprofiler](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/merge-policies/overview)
- [Översikt över beräknade attribut](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/computed-attributes/overview)

**Målgrupper och segmentering**

- [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/home)
- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/ui/segment-builder)
- [Direktuppspelningssegmentering](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/methods/streaming-segmentation)

**Datastyrning och sekretess**

- [Översikt över dataförvaltning](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/home)
- [Fältgruppen för samtycke och inställningar](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/field-groups/profile/consents)
- [Privacy Service - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/privacy/home)
- [Översikt över livscykelhantering av avancerade data](https://experienceleague.adobe.com/sv/docs/experience-platform/data-lifecycle/home)

**Övervakning och observerbarhet**

- [Översikt över Insikter i observationer](https://experienceleague.adobe.com/sv/docs/experience-platform/observability/home)
- [Översikt över aviseringar](https://experienceleague.adobe.com/sv/docs/experience-platform/observability/alerts/overview)

**Analyser och rapporter**

- [CJA - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-overview/cja-overview)
- [CJA Connections overview](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-connections/overview)
- [CJA datavyer - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/data-views)
- [Analysis Workspace - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/home)

**Guardrails**

- [Garantier för kundprofiler i realtid](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/guardrails)
- [Förvaringsskydd](https://experienceleague.adobe.com/sv/docs/experience-platform/ingestion/guardrails)
- [Skyddsritningar för segmentering](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/guardrails)
