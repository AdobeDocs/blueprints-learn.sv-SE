---
title: Köpa gruppbaserad marknadsföring och resehantering
description: Lär dig hur ni kan utveckla kundresor på kontonivå som kvalificerar leads till inköpsgrupper för att förbättra effektiviteten i B2B-marknadsföringen.
solution: Journey Optimizer, Real-Time Customer Data Platform
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '7932'
ht-degree: 0%

---


# Köpa gruppbaserad marknadsföring och resehantering

Den här guiden ger en omfattande implementeringsreferens för köp av gruppbaserad marknadsföring och resehantering. Det är utformat för lösningsarkitekter, marknadsföringsteknologer och implementeringstekniker som behöver implementera en resesamordning på kontonivå med att köpa grupphantering med [!DNL Adobe Journey Optimizer B2B Edition] och [!DNL Real-Time CDP B2B Edition].

Använd det här dokumentet för att förstå vad som ska konfigureras, var implementeringsalternativ finns och vilka kompromisser som styr varje beslut.

Till skillnad från kundresemönster fungerar det här mönstret på kontonivå, kvalificerade enskilda leads till köpgrupper som är kopplade till lösningsintressen, poängsätta engagemanget på köpgruppsnivå och samordna flerstegskontoresor som leder konton genom olika faser mot försäljningsberedskapen.

## Använd ärendeöversikt

B2B-organisationer står inför en viktig utmaning: inköpsbeslut fattas sällan av en enskild individ. Komplexa B2B-inköp berör flera intressenter - beslutsfattare, påverkare, chefer, budgetansvariga och tekniska utvärderare - som tillsammans utgör en&quot;köpgrupp&quot;. Traditionell ledande marknadsföring behandlar varje person för sig och saknar den kritiska signalen om rätt kombination av roller inom ett konto är engagerad och redo att köpa.

Genom att köpa gruppbaserad marknadsföring och resehantering kan ni ta itu med detta genom att byta enhet för samordning från enskilda leads till konton och inköpsgrupper. Mönstret gör det möjligt för B2B-marknadsförare att definiera lösningsintressen (de produkter eller tjänster som säljs), skapa inköpsgruppmallar som specificerar vilka roller som krävs för ett inköpsbeslut, kvalificera inkommande leads mot dessa roller, poängsätta engagemang på köpgruppsnivå och samordna kontoresor som svarar på kundgruppens fullständighet och beredskapssignaler.

Önskat resultat är förbättrad kvalitet och hastighet i pipeline: marknadsföring ger konton till försäljning endast när rätt personer på kontot är engagerade och köpgruppen är tillräckligt komplett, vilket minskar bortslösade säljsatsningar och snabbar upp avtalsutvecklingen.

## Viktiga verksamhetsmål

Det här användningsmönstret har stöd för följande affärsmål.

### Förbättra kvalificering och konvertering av leads

Öka ledningskvaliteten och snabba upp utvecklingen av pipeline genom poängsättning, vårdande och personaliserad uppföljning.

**KPI:er:** Leadkonvertering, konvertering av potentiell kund/lead, effektivitet

[Läs mer om hur du förbättrar kvalificering och konvertering av leads](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)

### Öka lead-generering

Generera mer kvalificerade leads för säljflödet via formulär, event, innehåll och flerkanalsengagemang.

**KPI:er:** Prospekt, Kostnad per lead, Leadkonvertering

[Läs mer om hur ni kan öka antalet leads](/help/blueprints/business-objectives/acquisition-growth/increase-lead-generation.md)

### Öka intäkter och försäljning

Öka intäkterna genom optimerade digitala kanaler, kampanjer och kundresor.

**KPI:er:** Intäktstillväxt, pipelinehastighet, slutfrekvens för avtal

[Läs mer om ökade intäkter och ökad försäljning](/help/blueprints/business-objectives/revenue-monetization/increase-revenue-sales.md)

## Exempel på taktiska användningsfall

Här följer några specifika scenarier där mönstret kan användas.

- **Lösningsspecifik inköpsgruppbehörighet** - Definiera inköpsgrupper för varje produktlinje (t.ex.&quot;Enterprise CRM&quot;,&quot;Data Platform&quot;,&quot;Security Suite&quot;) med rollmallar som anger obligatoriska profiler (Economic Buyer, Technical Evaluator, Champion, End User) och kvalificera leads från CRM- och marknadsföringssystemet mot dessa roller.
- **Kontoresa för pipeline-acceleration** - Orchestrera en kontoresa i flera steg som skickar riktade e-postmeddelanden till underengagerade roller inom en inköpsgrupp, utlöser säljaviseringar när tröskelvärden för engagemang nås och överför kontot till ett försäljningsklart stadium.
- **Kampanjer för att slutföra köp av grupper** - Identifiera konton där inköpsgrupper saknar roller (t.ex. ingen ekonomisk köpare identifierad) och starta riktade kampanjer för att engagera rätt personer i dessa konton.
- **Korsförsäljning av kontoresor** - När ett första avtal har avslutats skapar du nya inköpsgrupper för komplementära lösningsintressen och koordinerar kontoresor som vårdar den utökade köpkommittén.
- **Återengagemang för avbrutna avtal** - Identifiera konton där inköpsgruppernas poängpoäng har avböjt och utlösa återengagemangsresor med nytt innehåll, utåtriktad verksamhet eller eventinbjudningar.
- **Försäljnings- och marknadsföringsanpassning via CRM-insikter** - Surface Buy Group-status, interaktionsdata och kontostatus direkt i [!DNL Salesforce] eller [!DNL Dynamics 365] så att säljarna kan se marknadsföringskvalificerade konton i realtid.
- **Händelsedrivna uppdateringar av inköpsgrupper** - Uppdatera automatiskt poängen för köp av grupper när leads går till webbinarier, hämtar rapporter, besöker prissidor eller begär demonstrationer.
- **Kontosamordning med flera regioner** - Hantera inköpsgrupper över globala konton där olika regionala kontakter har olika roller, vilket ger en enhetlig poängsättning för engagemang över olika platser.

## Nyckeltal för prestanda

Följande nyckeltal hjälper till att mäta effekten av det här användningsmönstret.

| KPI | Beskrivning | Mätningsmetod |
| --- | --- | --- |
| Slutförandegrad för inköpsgrupp | Procent av inköpsgrupper med alla nödvändiga roller fyllda | [!DNL AJO B2B] Analysinstrumentpaneler: spåra rolltäckning per inköpsgrupp |
| Buying Group Engagement Score | Sammanställd engagemangspoäng för alla medlemmar i en inköpsgrupp | [!DNL AJO B2B] engagemangsbedömning: poängställning på personnivå summerat till inköpsgrupp |
| Hastighet för kvalificerat marknadsföringskonto | Procent av konton som når det marknadsföringskvalificerade tröskelvärdet | Slutkriterier för kontoresa: kontoövergång till försäljningsfärdig fas |
| Pipelinets hastighet | Genomsnittlig tid från att skapa inköpsgrupper till försäljningskvalificerade affärsmöjligheter | CRM-integrering: spåra scenövergångar från [!DNL AJO B2B] till CRM-pipeline |
| Kvalificeringsgrad för lead-till-köpgrupp | Procentandel leads som har kvalificerats för att köpa grupproller | [!DNL AJO B2B] Buying Group Management: Kvalificerad kontra okvalificerad lead-kvot |
| Svarsfrekvens för försäljningsavisering | Procentandel av försäljningsaviseringar som resulterar i uppföljningsaktiviteter för försäljning | CRM-försäljningsinsikter: spåra konvertering från varning till aktivitet |
| Slutförandefrekvens för kontoresa | Procent av konton som slutför den avsedda resan | [!DNL AJO B2B] Analysinstrumentpaneler: mått för slutförd resa |
| Anskaffningsgrad för e-post (B2B) | Öppen- och klickfrekvens för B2B-e-post | [!DNL AJO B2B]-rapportering: e-postleverans och engagemangsmått |

## Använd skiftlägesmönster

**Köpa gruppbaserad marknadsföring och resehantering**

Utveckla kundresor på kontonivå som kvalificerar leads till inköpsgrupper för att förbättra effektiviteten i B2B-marknadsföringen.

**Funktionskedja:** Kontoidentifiering > Buying Group Definition > Lead Qualification > Account Journey Execution > Engagement Scoring > Reporting

## Tillämpningar

Följande Adobe-program används i det här fallmönstret.

- **[!DNL Journey Optimizer B2B Edition] ([!DNL AJO B2B])** - Organiserar kundresor på kontonivå, hanterar inköpsgrupper med rollmallar och lösningsintressen, betygsätter engagemang på person- och inköpsgruppnivå, författare till B2B-e-postinnehåll, skickar SMS-meddelanden, konfigurerar säljvarningar och tillhandahåller kontrollpaneler för B2B-analyser.
- **[!DNL Real-Time CDP B2B Edition] ([!DNL RT-CDP B2B])** - Enhetaliserar kontoprofiler från B2B-data mellan olika källor, löser relationer mellan personer och konton, utvärderar målgrupper på kontonivå, konfigurerar B2B-specifika mål ([!DNL Marketo Engage], [!DNL LinkedIn], CRM) och tillämpar datastyrning över B2B-data.

## Foundationsfunktioner

Följande grundläggande funktioner måste finnas för det här användningsmönstret. För varje funktion anger statusen om den vanligtvis är obligatorisk, antas vara förkonfigurerad eller inte tillämplig.

| Funktionen Foundation | Status | Vad måste finnas på plats | Experience League referens |
| --- | --- | --- | --- |
| Administration och styrning | Obligatoriskt | Sandlådan har etablerats med [!DNL AJO B2B Edition] och [!DNL RT-CDP B2B Edition] berättiganden aktiverade. Roller konfigurerade för B2B-marknadsförare, säljåtgärder och administratörer med lämplig behörighet för att köpa grupphantering, kontoresor och CRM-integreringsinställningar. | [Översikt över sandlådor](https://experienceleague.adobe.com/sv/docs/experience-platform/sandbox/home), [Översikt över åtkomstkontroll](https://experienceleague.adobe.com/sv/docs/experience-platform/access-control/home) |
| Datamodellering och förberedelse | Obligatoriskt | B2B XDM-scheman konfigurerade med B2B-specifika klasser: XDM Business Account, XDM Business Opportunity, XDM Business Person (lead/kontakt), XDM Business Campaign och XDM Business Marketing List. Fältgrupper för kontoattribut, personattribut och aktivitets-/interaktionsdata måste finnas. Datauppsättningar som har skapats och profilaktiverats för varje schema. | [Systemöversikt för XDM](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/home), [schemaklasser för B2B](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/schema/composition) |
| Datakällor och samling | Obligatoriskt | Rörledningar för B2B-dataöverföring har upprättats, vanligtvis via [!DNL Marketo Engage]-källkopplingen eller [!DNL Salesforce]/[!DNL Dynamics] CRM-källanslutningarna. Data för konto, person, affärsmöjlighet, kampanj och kampanjmedlem måste flöda in i AEP datamängder. Data om beteendeinteraktion (webbbesök, e-postinteraktioner, innehållsnedladdningar) måste också hämtas för engagemangsbedömning. | [Källor - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/home), [Marketo Engage Connector](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) |
| Konfiguration av identitet och profil | Obligatoriskt | B2B-identitetsmatchning konfigurerad för att matcha relationer från människa till konto. Identitetsnamnutrymmen för B2B-identifierare ([!DNL Marketo] person-ID, [!DNL Salesforce] lead/kontakt-ID, konto-ID) måste finnas. Sammanfogningsprinciper som konfigurerats för B2B-profilenhetliga. Kontoprofiler måste vara enhetliga från data från olika källor. | [Översikt över identitetstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/home), [B2B-identitetsupplösning](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview) |
| Målgruppsdefinition och segmentering | Obligatoriskt | Målgruppsdefinitioner på kontonivå som skapats med kontoattribut, personattribut och aktivitetsdata. Kontomålgrupperna identifierar vilka konton som anger inköpsgruppsresor. Batchutvärdering är vanligtvis tillräckligt för B2B-kontoresor, men utvärdering av direktuppspelning kan användas för att utlösa kontokvalificeringsutlösare i realtid. | [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/home), [Kontomålgrupper](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/types/account-audiences) |

## Stödfunktioner

Följande funktioner förstärker det här användningsmönstret, men behövs inte för att köra kärnan.

| Stödfunktioner | Status | Varför det spelar någon roll | Experience League referens |
| --- | --- | --- | --- |
| Skapande av beräknat/härlett attribut | Rekommenderad | Beräknade attribut kan samla ihop engagemangshändelser på personnivå (e-postöppningar, innehållsnedladdningar, webbinarier-närvaro) till interaktionsstatistik på kontonivå som gör att inköpsgrupper kan göra poäng och logik för kontokvalificering. | [Översikt över beräknade attribut](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/computed-attributes/overview) |
| Livscykelhantering för data | Rekommenderad | Samtyckshantering är avgörande för e-post och SMS-kommunikation inom B2B. Förfallotidsprinciper för datauppsättningar hjälper till att hantera livscykeln för tillfälliga engagemangsdata och säkerställa att kraven på datalagring uppfylls. | [Avancerad livscykelhantering för data](https://experienceleague.adobe.com/sv/docs/experience-platform/data-lifecycle/home) |
| Dataanvändningsetiketter och -tillämpning | Rekommenderad | B2B-data innehåller ofta känslig företagsinformation och personuppgifter för affärskontakter. Datastyrningsprinciper säkerställer att B2B-data används korrekt på olika destinationer, särskilt när annonsplattformar eller tredjepartssystem aktiveras. | [Datastyrningsöversikt](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/home) |
| Övervakning och observerbarhet | Rekommenderad | Övervakning säkerställer att dataöverföringsnäten (CRM/[!DNL Marketo]-synk) är felfria, kontoprofiler uppdateras och att kontoresan utförs utan fel. Varningar om fel i källdataflödet är viktiga för att upprätthålla datavaluta. | [Översikt över Insikter om observabilitet](https://experienceleague.adobe.com/sv/docs/experience-platform/observability/home) |
| Rapportering och analys | Ingår | B2B-analysinstrumentpaneler i [!DNL AJO B2B Edition] tillhandahåller inköpsgruppsengagemang, resultat för kontoresan och mätvärden för pipeline. [!DNL CJA B2B Edition] utökar analysen med arbetsyteanalys på kontonivå, analyser av inköpsgrupper och korrelation mellan affärsmöjligheter. | [CJA - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-overview/cja-overview) |

## Programfunktioner

I den här planen används följande funktioner från programfunktionskatalogen. Funktioner mappas till implementeringsfaser i stället för till numrerade steg.

### [!DNL Journey Optimizer B2B Edition] ([!DNL AJO B2B])

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Intressekonfiguration för lösning | Fas 1: Solution Interest &amp; Buying Group Setup | Definiera lösningsintressen som mappar produkter eller tjänster till att köpa kvalificeringskriterier för grupper |
| Buying Group Management | Fas 1: Solution Interest &amp; Buying Group Setup | Skapa och hantera inköpsgrupper med rollmallar, personmappning och definitioner av lösningsintressen |
| Journey Orchestration | Fas 3: Design och utförande av kontoresa | Designa och hantera kontoresor i flera steg med villkor, åtgärder och engagemangsbaserad förgrening |
| Engagement Scoring | Fas 2: Resultatbedömning av kvalificering och engagemang | Få ökat engagemang på personnivå inom inköpsgrupper för att mäta hur väl de är färdiga och redo att köpa grupper |
| Kontokvalificering | Fas 2: Resultatbedömning av kvalificering och engagemang | Använd AI-baserade kontokvalificeringsagenter för att bedöma kontoberedskap och ledningskvalitet |
| B2B-redigering av e-post | Fas 3: Design och utförande av kontoresa | Skapa e-postinnehåll för B2B med mallar, visuella fragment, varumärkesteman och generering av AI-assisterat innehåll |
| SMS-kanalhantering | Fas 3: Design och utförande av kontoresa | Konfigurera och hantera SMS-kommunikation inom B2B-kontoresor |
| Konfiguration av försäljningsavisering | Fas 4: Försäljningsjustering och CRM-integrering | Konfigurera e-postmeddelanden med säljaviseringar för att meddela säljarna om milstolpar för kontointeraktion och inköpssignaler |
| Försäljningsinsikter för CRM | Fas 4: Försäljningsjustering och CRM-integrering | Ange CRM-synlighet ([!DNL Salesforce], [!DNL Dynamics]) för inköpsgruppstatus, engagemangsdata och kontoförloppet |
| Kontrollpaneler för B2B-analys | Fas 5: Rapportering och optimering | Övervaka kundens reseresultat, köp av gruppengagemang och pipeline-statistik via smarta och engagemangspaneler |

### [!DNL Real-Time CDP B2B Edition] ([!DNL RT-CDP B2B])

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Enhetlig kontoprofil | Fas 0: B2B Data Foundation | Konsolidera B2B-data från olika källor i enhetliga kontoprofiler med hjälp av specialiserade XDM B2B-schemaklasser och fältgrupper |
| B2B-identitetsupplösning | Fas 0: B2B Data Foundation | Lös relationer från människa till konto med hjälp av primära identifierare, kontohierarkier på flera nivåer och många-till-många-mappningar från människa till konto |
| Utvärdering av målgrupp för konto | Fas 0: B2B Data Foundation | Utvärdera segmentmedlemskap på kontonivå genom att kombinera kontoattribut, personattribut och aktivitetsdata |
| Konfiguration för kontomål | Fas 4: Försäljningsjustering och CRM-integrering | Konfigurera anslutningar till B2B-specifika mål ([!DNL Marketo Engage], [!DNL LinkedIn], CRM-system) med fältmappning på kontonivå |
| Audience Activation | Fas 4: Försäljningsjustering och CRM-integrering | Publicera kontobaserade målgrupper till destinationer för kontobaserad målgruppsanpassning och inaktivering |
| Integrering av [!DNL Marketo Engage] | Fas 0: B2B Data Foundation | Infoga och aktivera data dubbelriktat med [!DNL Marketo Engage] med hjälp av inbyggda B2B-käll- och målanslutningar |
| B2B-datastyrning | Fas 0: B2B Data Foundation | Använd dataanvändningspolicyer och samtycke i alla processer för centralisering och aktivering av B2B-kontodata |

## Förutsättningar

Slutför följande innan du börjar implementera.

- [!DNL AJO B2B Edition] licens har etablerats och aktiverats i målsandlådan
- [!DNL RT-CDP B2B Edition] licens har etablerats och aktiverats i målsandlådan
- CRM-systemet ([!DNL Salesforce] eller [!DNL Microsoft Dynamics 365]) är åtkomligt med lämpliga API-autentiseringsuppgifter för dubbelriktad datasynkronisering
- [!DNL Marketo Engage]-instansen är ansluten (om [!DNL Marketo] används som plattform för automatiserad marknadsföring) med en källanslutning konfigurerad
- Distribuerade B2B XDM-scheman: Medlemsklasserna Account, Person, Opportunity, Campaign och Campaign med obligatoriska fältgrupper
- Konto- och persondata som hämtas in till AEP med relationer från människa till konto har lösts
- E-postkanal konfigurerad: underdomän delegerad, IP-pool har värvats och kanalyta har skapats för B2B-e-postsändning
- SMS-providern har konfigurerats (om SMS-kanal används i kontoresor): [!DNL Sinch], [!DNL Twilio] eller [!DNL Infobip] autentiseringsuppgifter har angetts
- Säljteamet har anslutit till CRM Sales Insights-komponenten ([!DNL Salesforce] AppExchange-paket eller [!DNL Dynamics]-lösning installerad)
- Innehållsresurser som förberetts: e-postmallar för B2B, varumärkesteman och visuella fragment för vårdar- och säljaviseringar via e-post
- Lösenes räntetaxonomi har definierats: lista över produkter/tjänster som kommer att ha kopplade inköpsgrupper
- Köpa grupprollmallar som utformats: personligheter och roller som krävs för varje lösningsintresse (t.ex. ekonomisk köpare, teknisk utvärderare, mästare)

## Implementeringsalternativ

I detta avsnitt beskrivs de tillgängliga implementeringsmetoderna, som är anpassade efter olika organisatoriska behov och mognadsnivåer.

### Alternativ A: Ett enda lösningsintresse med linjär kontoresa

**Passar bäst för:** Organisationer som inte har börjat med att köpa grupphantering och som vill börja med en enda produktlinje eller lösningserbjudande, validera metoden och iterera innan de skalar efter flera lösningsintressen.

**Så här fungerar det:**

Strategin fokuserar på en enda lösning (en produkt eller tjänst) med en inköpsgruppmall. En linjär kontoresa är utformad med sekventiella steg: kontoidentifiering, bildande av inköpsgrupper, vårdengagemang, poängtröskel för engagemang och försäljning. Färden följer en rak väg utan komplexa förgrenade eller parallella spår.

Leads är kvalificerade att köpa grupproller när de hämtas från CRM eller [!DNL Marketo Engage]. Kontoresan skickar e-postmeddelanden till underengagerade roller, övervakar engagemangsmoment och utlöser en säljavisering när inköpsgruppen når en definierad nivå för fullständighet och engagemang. Detta tillvägagångssätt ger ett tydligt, mätbart konceptbevis innan komplexiteten introduceras.

**Viktiga överväganden:**

- Enklare att implementera och validera, vilket gör den lämplig för en första driftsättning
- Begränsat till en produkt/tjänst i taget
- Linjär resestruktur kanske inte klarar komplexa inköpscykler i flera steg

**Fördelar:**

- Snabbast tid till värde med minimal komplexitet i konfigurationen
- Tydliga framgångsmått knutna till ett enda lösningsintresse
- Enklare att förklara och få företagsköp
- Smidig rapportering och KPI-mätning

**Begränsningar:**

- Beskriver inte korsförsäljning eller flerproduktsscenarier
- Konton som är intresserade av flera lösningar kräver separata, icke-samordnade resor
- Kan inte utnyttja funktionerna för hantering av inköpsgrupper fullt ut

**Experience League:**

- [AJO B2B edition - översikt](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/guide-overview)
- [Skapa inköpsgrupper](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-overview)

### Alternativ B: Flera olika lösningsintressen med förgreningskontoresor

**Passar bäst för:** Organisationer med flera produktlinjer eller tjänsteerbjudanden som behöver hantera distinkta inköpsgrupper per lösningsintresse, med kontoresor där grenen baseras på vilka lösningsintressen som är aktiva och hur långt längs varje inköpsgrupp är i kvalificeringsprocessen.

**Så här fungerar det:**

Flera olika lösningsintressen definieras, var och en med sin egen mall för inköpsgruppsroll. En kontoresa börjar med kontoidentifiering och utvärderar vilka lösningsintressen som gäller för varje konto baserat på beteendesignaler, företagsdata eller uttryckliga avsikter. Resorna är inriktade på varje aktiv lösning och kör parallella plantspår för olika inköpsgrupper inom samma konto.

Bedömningen av engagemanget sker oberoende av inköpsgrupp, vilket gör att en inköpsgrupp kan nå försäljningsberedskap medan en annan fortfarande vårdas. Säljvarningar konfigureras per lösningsintresse så att rätt säljteam eller specialist meddelas när en viss inköpsgrupp kvalificerar sig. CRM-insikter visar alla aktiva inköpsgrupper för ett konto och ger försäljningen en helhetsbild.

**Viktiga överväganden:**

- Kräver en väldefinierad lösning för räntetaxonomi och distinkta inköpsgruppmallar
- Resans komplexitet ökar med varje ytterligare lösningsintresse
- Samordning mellan inköpsgrupper (t.ex. delade kontakter som har roller i flera inköpsgrupper) måste planeras

**Fördelar:**

- Stöder korsförsäljning och flerproduktskonton
- Oberoende poängsättning per inköpsgrupp ger detaljerad insyn i rörliga bilder
- Säljarna får riktade aviseringar per lösningsintresse
- Maximerar [!DNL AJO B2B Edition] funktioner för grupphantering

**Begränsningar:**

- Komplexare implementering och längre driftsättningstid
- Fler innehållsresurser krävs (separata e-postspår per lösningsintresse)
- Rapporteringen är mer komplex med flera inköpsgrupper per konto
- Risk för att skicka meddelanden till kontakter som finns i flera inköpsgrupper (kräver frekvenshantering)

**Experience League:**

- [Lösningsintressen](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/buying-groups/solution-interests)
- [Kontoresor](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/account-journeys/journey-overview)

### Alternativ C: AI-assisterade kontokvalifikationer med automatiserad reseutveckling

**Passar bäst för:** B2B-organisationer med betydande historiska data som vill använda kontokvalificeringsagenter med AI-funktioner för att automatisera bedömningen av kontoberedskap, minska den manuella kvalificeringsinsatsen och dynamiskt justera kundresan baserat på AI-genererade beredskapspoäng.

**Så här fungerar det:**

Den här metoden bygger på Option B:s multi-solution-interest-stiftelse men lägger till kontokvalificering via AI för att automatisera övergången mellan olika kundfaser. Istället för att enbart förlita sig på regelbaserade poängtrösklar utvärderar AI-kvalificeringsagenten kontoberedskapen med en bredare uppsättning signaler - fullständiga inköp, engagemangshastighet, förstklassig anpassning, historiska konverteringsmönster och intent-data.

Kontoresor använder AI-kvalificeringsutdata för att bestämma nästa steg: konton som är högt på beredskapen spåras snabbt till försäljningsvarningar, konton i mellanskiktet får intensivare näring och konton med låg beredskap placeras i långsiktiga informationsspår. AI-agenten utvärderar kontinuerligt om när nya engagemangsdata kommer in, vilket möjliggör dynamisk reseutveckling utan manuell inblandning.

**Viktiga överväganden:**

- Kräver tillräckliga historiska data för att utbilda effektiva kvalifikationsmodeller
- AI-utdata ska valideras mot faktiska pipeline-utfall före fullständig driftsättning
- Kombinerar väl med [!DNL CJA B2B Edition] för att analysera kvalificeringsnoggrannhet och pipeline-korrelation

**Fördelar:**

- Minskar behovet av manuell kvalificering och eliminerar godtyckliga tröskelbaserade överlämningar
- Anpassa dynamiskt till förändrade mönster för kontobeteende och engagemang
- Högre ledningskvalitet genom att lägga in flera signaler utöver enkla engagemangsmätningar
- Kontinuerlig omvärdering förhindrar att konton fastnar i felaktiga kundfaser

**Begränsningar:**

- Kräver historiska konverteringsdata för meningsfull AI-utbildning
- &quot;Black box&quot;-kvalificeringsbeslut kan vara svårare för säljarna att förstå och lita på inledningsvis
- Mer komplicerad att felsöka när konton har kvalificerats oväntat eller inte alls
- Beroende på datakvalitet och fullständighet för alla indatasignaler

**Experience League:**

- [Kontokvalificering](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)
- [AI Assistant i AJO B2B](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/guide-overview)

### Jämförelse av alternativ

| Kriterier | Alternativ A: Intresse för en lösning | Alternativ B: Flera lösningsintressen | Alternativ C: AI-stödd kvalificering |
| --- | --- | --- | --- |
| Bäst för | Första driftsättning, en produktlinje | Flerproduktorganisationer | Mogna organ med historiska data |
| Komplex | Lågt | Medium-High | Högt |
| Tid till värde | 2-4 veckor | 4-8 veckor | 6-12 veckor |
| Lösningsintressen | 1 | Flera | Flera |
| Resestruktur | Linjär | Förgreningar, parallella spår | Dynamisk, AI-styrd progression |
| Bedömningsmetod | Regelbaserade tröskelvärden | Regelbaserad per inköpsgrupp | AI-baserade kvalifikationer + regler |
| Innehållskrav | Minimal (ett moderspår) | Hög (per lösningsintresse) | High + Dynamic Content Selection |
| Försäljningsjustering | Arbetsflöde för enskild avisering | Intresseanmälningar per lösning | Prioriterade AI-poäng-varningar |
| Kräver | Grundläggande B2B-data | Väldefinierad lösningstaxonomi | Historiska konverteringsdata + taxonomi |

### Välj rätt alternativ

Börja med följande frågor för att fastställa den bästa implementeringsmetoden:

1. **Hur många distinkta produkter eller tjänster har oberoende inköpskommittéer?** Om svaret är ett (eller om organisationen vill bevisa konceptet först) börjar du med alternativ A. Om det är flera, gå till fråga 2.

2. **Finns det tillräckligt med historiska data om vunna/förlorade avtal, köpkommittéernas sammansättning och engagemangsmönster?** Om ja, och organisationen vill minimera manuell kompetens, erbjuder alternativ C det mest automatiserade tillvägagångssättet. Om så inte är fallet ger alternativ B stöd för flera lösningar med regelbaserad poängsättning.

3. **Vilken är organisationens ändringshanteringskapacitet?** Alternativen B och C kräver större organisationsanpassning (innehållsproduktion, säljstöd, korsfunktionell samordning). Om kapaciteten är begränsad börjar du med alternativ A och expanderar.

En vanlig utvecklingsväg är: börja med alternativ A för att bevisa konceptet med ett enda lösningsintresse, utöka till alternativ B genom att lägga till lösningsintressen när förtroendet ökar, och sedan skikt i alternativ C:s AI-kvalifikationer när det finns tillräckligt med historiska data för att effektivt kunna utbilda modellerna.

## Implementeringsfaser

I följande faser beskrivs den stegvisa implementeringsprocessen för det här användningsmönstret.

### Fas 0: Bygg B2B-data

**Programfunktioner:** [!DNL RT-CDP B2B]: Kontoprofilens enhetlighet, B2B-identitetsmatchning, [!DNL Marketo Engage] integrering, B2B-datastyrning, utvärdering av kontomåls

I den här fasen etableras B2B-datastrukturen i [!DNL RT-CDP B2B Edition]. Du kommer att samla kontodata från CRM, automatiserad marknadsföring och andra källor i en enda kontoprofil, lösa relationer mellan människor, konfigurera B2B-datastyrning och skapa målgrupper på kontonivå som matas in i [!DNL AJO B2B Edition]-hantering av inköpsgrupper.

#### Beslut: B2B-strategi för datakälla

Vilka system fungerar som de primära källorna för data om konto, person och engagemang?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| [!DNL Marketo Engage] som primär källa | [!DNL Marketo] är organisationens plattform för automatiserad marknadsföring med omfattande engagemangshistorik | Inbyggd dubbelriktad anslutning förenklar konfigurationen, engagemangsdataflöden automatiskt, relationer mellan personer ärvs från [!DNL Marketo] |
| CRM ([!DNL Salesforce]/[!DNL Dynamics]) som primär källa | CRM är systemet för post för konton och kontakter. [!DNL Marketo] används inte | Kräver CRM-källanslutningskonfiguration; interaktionsdata kan behöva ytterligare källor; relationer från människa till konto från CRM-konton till kontaktorganisationer |
| Hybrid: CRM för konton + [!DNL Marketo] för engagemang | CRM äger konto-/kontakthuvuddata medan [!DNL Marketo] fångar beteenden | Det vanligaste mönstret för organisationer som använder båda; kräver noggrann identitetsupplösning för att länka [!DNL Marketo] personer till CRM-kontakter |

#### Beslut: Målgruppsstrategi

Hur ska man definiera vilka målgrupper som ska ha konton för reseinträde?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Firmografiskt baserade målgrupper | Målkonton baserade på bransch, företagsstorlek, intäktsnivå eller geografi | Bra för ABM-mållistor; kräver inga engagemangsdata; kan vara bred |
| Engagemangsbaserade målgrupper | Målkonton där människor har visat beteendeavsiktssignaler | Kräver att engagemangsdata flödar; mer exakt målinriktning; kan missa konton med latent intresse |
| Kombinerad firmografi och engagemang | Målkonton som matchar den perfekta kundprofilen OCH som visar engagemang | Mest exakt; kräver båda datatyperna; rekommenderas för generering av kvalificerade rörledningar |

**Gränssnittsnavigering:** Plattform > Källor > Katalog > Välj källa ([!DNL Marketo Engage], [!DNL Salesforce] osv.) > Ställ in dataflöde

**Information om nyckelkonfiguration:**

- Konfigurera B2B XDM-scheman för varje B2B-enhet (konto, person, möjlighet, kampanj, kampanjmedlem) med obligatoriska fältgrupper
- Ställ in källanslutningar för CRM och/eller [!DNL Marketo Engage] med lämplig schemaläggning (vanligtvis 1-4 timmars intervall för B2B-data)
- Konfigurera identitetsnamnutrymmen för B2B-identifierare ([!DNL Marketo] person-ID, SFDC lead-ID, SFDC kontakt-ID, konto-ID)
- Aktivera B2B-identitetsmatchning för att länka personer till konton
- Skapa målgrupper på kontonivå med funktionen för målgrupper på kontonivå i [!DNL RT-CDP]

**Experience League-dokumentation:**

- [RT-CDP B2B edition - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview)
- [B2B-scheman i Real-Time CDP](https://experienceleague.adobe.com/sv/docs/experience-platform/rtcdp/schemas/b2b)
- [Marketo Engage källanslutning](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Målgrupper](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/types/account-audiences)
- [Identitetsupplösning för B2B](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview)

### Fas 1: Lösningens intresse och inställning av inköpsgrupp

**Programfunktioner:** [!DNL AJO B2B]: Konfiguration av lösningsintresse, Buying Group Management

I den här fasen definieras lösningsintressen (produkter/tjänster) och köpgruppsmallar som utgör kärnan i inköpsgrupphanteringsmodellen. Du skapar lösningsintressen, definierar rollmallar med personuppgiftskrav och konfigurerar hur leads kvalificeras till inköpsgruppsroller.

#### Beslut: Intresseprecision

På vilken nivå ska lösningsintressen definieras?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Lösningsintressen på produktnivå | Varje enskild produkt har en egen inköpsgrupp | Mest detaljerat; möjliggör produktspecifika inköpsgruppmallar; kan resultera i många inköpsgrupper per konto |
| Intresser på lösningsnivå | Gruppera relaterade produkter i lösningskategorier (till exempel&quot;Marketing Cloud&quot; istället för enskilda produkter) | Enklare att hantera; färre inköpsgrupper; roller kan vara mer generiska; rekommenderas för initiala distributioner |
| Intresser på ärendenivå | Definiera intressen kring affärsresultat snarare än produkter (t.ex.&quot;Digital omvandling&quot;) | Justerar med konsultförsäljning; inköpsgruppsroller kan omfatta flera produkter; svårare att mappa till CRM-pipeline-faser |

#### Beslut: Malldesign för köpgruppsroll

Hur ska roller definieras inom varje inköpsgrupp?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Standardrollmall | Använd en gemensam uppsättning roller för alla lösningsintressen (till exempel ekonomisk köpare, teknisk utvärderare, mästare, slutanvändare) | Enhetlig poängsättning och kvalifikationer, enklare att hantera, kanske inte fångar upp lösningsspecifika roller |
| Lösningsspecifika rollmallar | Definiera unika roller per lösningsintresse baserat på den faktiska köpkommittén för produkten | Exaktare kvalifikationer; kräver djupare kunskaper om varje inköpsprocess; högre underhåll |
| Mallar för nivåindelad roll | Definiera obligatoriska roller (måste ha för kvalificering) och valfria roller (utöka fullständigheten men inte obligatorisk) | Balanserar precisionen med flexibilitet; förhindrar att alltför strikta kvalificeringskriterier blockerar rörledningen |

**Gränssnittsnavigering:** [!DNL AJO B2B Edition] > Köpgrupper > Lösningsintressen > Skapa lösningsintresse

**Gränssnittsnavigering:** [!DNL AJO B2B Edition] > Köpgrupper > Rollmallar > Skapa rollmall

**Information om nyckelkonfiguration:**

- Definiera varje lösnings intresse med namn, beskrivning och det affärsresultat som den behandlar
- Skapa rollmallar som anger vilka profiler som krävs för varje inköpsgrupp (t.ex.&quot;Beslutsfattare&quot;,&quot;Influencer&quot;,&quot;Practitioner&quot;,&quot;Executive Sponsor&quot;)
- Konfigurera kvalificeringskriterier för lead-till-roll: hur systemet avgör vilken roll ett lead mappar till (baserat på befattning, avdelning, tjänsteålder eller anpassade attribut)
- Ange tröskelvärden för fullständighet: definiera hur många procent av rollerna som måste fyllas för att en inköpsgrupp ska anses vara&quot;fullständig&quot;
- Länka lösningsintressen till konton eller kontoattribut som visar på potentiella intressen

**Var alternativen skiljer sig:**

**För alternativ A (intresse för en lösning):**
Skapa ett lösningsintresse och en rollmall. Fokusera på en tydlig, välförstådd inköpsrörelse för organisationens primära produkt eller tjänst.

**För alternativ B (flera lösningsintressen):**
Skapa olika lösningsintressen, var och en med en egen rollmall. Mappa varje lösningsintresse till lämplig CRM-produkt/affärsmöjlighetstyp för spårning av pipeline i efterföljande led.

**För alternativ C (AI-assisterad kvalificering):**
Konfigurera lösningsintressen och rollmallar som i alternativ B, men konfigurera även AI-kvalificeringsagenten med historiska data om framgångsrika inköpsgruppskompositioner och avtalsresultat för att utbilda kvalificeringsmodellen.

**Experience League-dokumentation:**

- [Översikt över inköpsgrupper](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-overview)
- [Lösningsintressen](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/buying-groups/solution-interests)
- [Rollmallar](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-role-templates)
- [Skapa inköpsgrupper](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-create)

### Fas 2: Ledningskvalifikationer och poängsättning för engagemang

**Programfunktioner:** [!DNL AJO B2B]: Betygsättning av engagemang, kontokvalificering

I den här fasen anges poängmodellen för engagemang som mäter engagemang på personnivå inom inköpsgrupper och lägger upp den på inköpsgrupper- och kontonivånivå. Ni kommer att konfigurera poängregler, definiera tröskelvärden för kvalificering och eventuellt aktivera kontokvalificering med AI.

#### Beslut: Partnerskapsbedömningsmodell

Hur ska kundengagemanget poängteras på personnivå och köpgruppsnivå?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Aktivitetsbaserad poängsättning | Tilldela poängvärden till specifika åtgärder (e-post öppnad = 5 punkter, innehållshämtning = 15 punkter, demobegäran = 50 punkter) | Genomskinlig och enkel att justera; kräver kontinuerligt underhåll när innehåll och kanaler ändras; är mest välbekant för [!DNL Marketo]-användare |
| Resultatviktad poängsättning | Vikt på senaste aktiviteter som är större än äldre (avskalningsmodell) | Bättre återspeglar den nuvarande avsikten; förhindrar att gamla höga poäng påverkar kvalificeringen; mer komplicerade att konfigurera |
| AI-baserad poängsättning | Använd AI-kvalificeringsagenten [!DNL AJO B2B] för att generera beredskapspoäng baserat på mönsterigenkänning | Mest sofistikerade, anpassar automatiskt, kräver historiska data, kan vara ogenomskinliga för säljarna från början |

#### Beslut: Tröskelvärdesmetod för kvalificering

När ska en inköpsgrupp anses redo för försäljning?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Endast poäng | Köpgruppen kvalificerar sig när aggregerad engagemangspoäng överskrider ett definierat värde | Enkelt att implementera; poängtröskeln kan behöva justeras över tiden; tar inte hänsyn till rolldisposition |
| Slutförandegrad + poängtröskel | Köpgruppen kvalificerar sig när tröskelvärdet för minsta rolltäckning OCH poäng båda uppfylls | Kraftfullare kvalificering - förhindrar överlämning av inköpsgrupper med höga poäng men som saknar nyckelroller |
| AI-bestämd beredskap | AI-kvalificeringsagenten avgör beredskapen med hjälp av flera signaler utöver poängen och fullständigheten | Mest sofistikerad; står för snabbköp, konkurrenssignaler och historiska mönster; endast alternativ C |

**Gränssnittsnavigering:** [!DNL AJO B2B Edition] > Köpgrupper > Betygsättning av engagemang > Konfigurera bedömningsregler

**Information om nyckelkonfiguration:**

- Definiera poängregler för engagemang: tilldela poäng till beteendehändelser (e-postöppningar, klickningar, besök på webbsidor, nedladdningar, formulärinskickning, webbinarier, demonstrationsförfrågningar)
- Konfigurera minskning av poäng eller viktning av senaste poäng om tidskänslig poängsättning används
- Ange aggregering av poäng på inköpsgruppnivå: hur personpoäng kombineras till ett poängvärde för inköpsgrupp (summa, viktat genomsnitt eller minimum-threshold-per-role)
- Definiera kvalificeringströsklar: poängnivåer och fullständighetsnivåer som utlöser övergången till nästa inköpsfas
- Konfigurera AI-kvalificeringsagenten (alternativ C): utbilda med historiska avtalsdata, definiera de signaler som agenten ska beakta och ange tröskelvärden för förtroende

**Experience League-dokumentation:**

- [Engagemangsbedömning](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)
- [Köpgruppsfaser](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)
- [Kontokvalificering](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)

### Fas 3: Design och utförande av kontoresa

**Programfunktioner:** [!DNL AJO B2B]: Journey Orchestration, B2B-redigering för e-post, SMS-kanalhantering

Den här fasen utformar och driftsätter kontoresan som leder till engagemang med medlemmar i inköpsgrupper. Du skapar kontoresor med anmälningsvillkor, åtgärdsnoder (e-post, SMS), villkorsgrenar (baserat på inköpsgruppfas, engagemangspoäng, rolltäckning), väntesteg och avslutningskriterier.

#### Beslut: Inlösare för resan

Vilken händelse eller vilket villkor gör att ett konto går in på resan?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Kvalificering av kontorets målgrupp | Kontot anges när det ansluter till en målkontomålgrupp | Batchorienterad; bra för ABM-listbaserad post; målgruppen måste vara fördefinierad |
| Skapandehändelse för inköpsgrupp | Kontot anges när en inköpsgrupp skapas för första gången för kontot | Händelsestyrd, utlöses av kompetens i ledande ställning i en köpgruppsroll, mer realtid |
| Ändring av kontoattribut | Kontot anges när ett visst attribut ändras (t.ex. intent score, kontonivå) | Kräver att utlösarattributet uppdateras i realtid eller nästan i realtid |

#### Beslut: Kanalblandning för B2B-plantor

Vilka kanaler ska kontoresan använda för att engagera medlemmar i inköpsgrupper?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Endast e-post | De flesta B2B-interaktioner sker via e-post; det finns ingen infrastruktur för SMS-deltagande | Lättast att konfigurera; vanligaste B2B-mönstret; kanske saknar kontakter som sätter mobilen först |
| E-post + SMS | Organisationen har SMS-deltagande från affärskontakter; brådskande meddelanden är berättigade | SMS gäller för tidskänsliga aviseringar (händelsemeddelanden, mötesbekräftelser); kräver SMS-providerkonfiguration |
| E-post + SMS + säljaviseringar | Helspektrum: marknadsföring via e-post/SMS plus säljteammeddelanden | Mest omfattande; kräver att säljarna antar ett varningsarbetsflöde, koordinerar marknadsförings- och säljkontaktytor |

#### Beslut: Förgreningsstrategi för resor

Hur ska kundresan baseras på status för konto och inköpsgrupp?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Scenbaserad förgrening | Gren baserat på inköpsgruppsfas (t.ex. medvetenhet, överväganden, beslut) | Justerar med traditionella funnel-stadier; innehåll mappas till faser; tydlig progressionsväg |
| Rollbaserad förgrening | Filial för att skicka olika innehåll till olika inköpsgrupper (tekniskt innehåll till utvärderare, ROI-innehåll till ekonomiska köpare) | Mer personaliserat; kräver rollspecifika innehållsresurser, högre innehållsproduktionsinsats |
| Engagement-based branching | Förgreningen baseras på tröskelvärden för engagemangsmusik (lågt engagemang = återengagemang, högt = acceleration) | Dynamisk och responsiv; anpassar sig till det verkliga beteendet; kan skapa komplexa förgreningsträd |

**Gränssnittsnavigering:** [!DNL AJO B2B Edition] > Kontoresor > Skapa resa

**Information om nyckelkonfiguration:**

- Skapa arbetsytan för kontoresan med det valda startvillkoret
- Lägg till noder för kontoresa: e-poståtgärder, SMS-åtgärder, väntesteg, villkorsdelningar och förgreningar av sökvägar
- Skapa B2B-material för e-post med B2B-Designer med varumärkesteman, visuella fragment och generering av AI-assisterat innehåll
- Konfigurera personaliseringstoken som refererar till kontoattribut, personattribut och köpgruppsdata
- Ange väntetider mellan kontaktytor (B2B-resor använder vanligtvis längre väntan: 3-7 dagar mellan e-postmeddelanden)
- Definiera avslutningskriterier: villkor under vilka konton lämnar resan (inköpsgruppen når kvalificeringströskeln, affärsmöjligheten skapad i CRM, kontoavanslut)
- Konfigurera SMS-åtgärder om du använder SMS-kanal (kräver SMS-providerkonfiguration och kontaktanmälan)
- Testa resan med testkonton före publicering

**Var alternativen skiljer sig:**

**För alternativ A (intresse för en lösning):**
Utforma en linjär resa med sekventiella steg. Tävlingsbidraget baseras på en enda kontopublik eller en händelse för att skapa en inköpsgrupp. Ett e-postflöde med allt större snabbhet och djupare innehåll.

**För alternativ B (flera lösningsintressen):**
Designa en resa med parallella grenar per lösningsintresse. Använd villkorsnoder för att dirigera konton till rätt vårdspår baserat på vilka inköpsgrupper som finns. Varje gren har sitt eget innehåll och sina poängtrösklar.

**För alternativ C (AI-assisterad kvalificering):**
Designa en resa där villkorsnoderna utvärderar AI-kvalificeringspoängen i stället för (eller utöver) regelbaserade tröskelvärden. Inkludera dynamiskt sökvägsval där AI avgör om ett konto ska accelereras, underhållas eller avprioriteras.

**Experience League-dokumentation:**

- [Översikt över kontoresor](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/account-journeys/journey-overview)
- [Nod för kontoresa](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/account-journeys/journey-nodes)
- [Framtagning av e-post från B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/email-authoring)
- [SMS-kanal i AJO B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sms-authoring)
- [AI-assistenten för att skapa e-post](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/ai-assistant-emails)

### Fas 4: Försäljningsjustering och CRM-integrering

**Programfunktioner:** [!DNL AJO B2B]: Säljaviseringskonfiguration, CRM-försäljningsinsikter; [!DNL RT-CDP B2B]: Kontonas målkonfiguration, Audience Activation-konto

Den här fasen skapar en bro mellan marknadsföring och försäljning genom att konfigurera e-postmeddelanden om försäljning, distribuera CRM-försäljningsinsikter för synlighet i CRM och eventuellt aktivera kontomålgrupper till B2B-mål ([!DNL LinkedIn], [!DNL Marketo], CRM-system).

#### Beslut: Utlösarstrategi för säljavisering

När ska försäljning meddelas om statusen för en inköpsgrupp för ett konto?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Milstolpebaserade aviseringar | Meddela försäljningen när inköpsgruppen når specifika milstolpar (kvalificerat, fullständigt, högt engagemang) | Tydliga, diskreta meddelanden; förhindrar varningströtthet; kan missa gradvisa trender för engagemang |
| Tröskelbaserade aviseringar | Meddela försäljningen när poängen för ärendet överskrider ett definierat tröskelvärde | Kontinuerlig övervakning; kan utlösa flera varningar när poängen varierar nära tröskelvärdet |
| Aviseringar för scenövergångar | Meddela försäljningen när ni köper gruppövergångar till en ny fas (t.ex. från bedömning till beslut) | Justerar med pipeline-faser; klar signal för försäljningsåtgärd; kräver väldefinierade scendefinitioner |

#### Beslut: Integreringsdjup för CRM

Hur djupt bör man hitta gruppdata i CRM?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Endast säljaviseringar (ingen CRM-komponent) | Organisationen använder inte [!DNL Salesforce] eller [!DNL Dynamics], eller så går det inte att integrera CRM | Lägsta integrationsinsats; säljarna får e-postmeddelanden men ingen CRM-instrumentpanel; begränsad synlighet |
| Kontrollpanel för CRM-försäljningsinsikter | Organisationen använder [!DNL Salesforce] eller [!DNL Dynamics] och vill ha en inköpsgruppstatus som är synlig i CRM | Kräver installation av CRM Sales Insights-paketet; ger omfattande information på kontonivå; rekommenderas för de flesta implementeringar |
| Fullständig dubbelriktad CRM-synkronisering | Köpa gruppfaser och bakgrundsmusik som skrivs tillbaka till CRM-objekt, vilket påverkar CRM-arbetsflödet och rapporteringen | Högsta komplexitet i integreringen; möjliggör CRM-intern pipeline-rapportering; kräver anpassad CRM-konfiguration |

**Gränssnittsnavigering:** [!DNL AJO B2B Edition] > Administration > Konfiguration av försäljningsavisering

**Gränssnittsnavigering:** [!DNL AJO B2B Edition] > Administration > CRM Sales Insights > Configure

**Information om nyckelkonfiguration:**

- Konfigurera e-postmallar för säljaviseringar: inkludera inköpsgruppstatus, engagerade profiler, engagemangspoäng och rekommenderade nästa åtgärder
- Definiera regler för varningsdirigering: vilka säljare eller team som får aviseringar baserade på kontoägarskap, territorium eller lösningsintresse
- Installera och konfigurera CRM-försäljningsinsikter för [!DNL Salesforce] eller [!DNL Dynamics 365]
- Mappa inköpsgruppsdata till CRM-objekt så att säljarna kan visa inköpsgruppernas sammansättning, engagemang och kundresan i CRM-arbetsflödet
- Du kan även konfigurera kontodestinationsanslutningar för att aktivera kontomålgrupper till [!DNL LinkedIn] (för ABM-annonsering), [!DNL Marketo Engage] (för uppföljning på leads) eller andra B2B-destinationer

**Experience League-dokumentation:**

- [E-postmeddelanden om försäljningsaviseringar](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sales-alert-email)
- [Försäljningsinsikter för CRM](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/crm-sales-insights)
- [Översikt över destinationer](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/home)
- [LinkedIn Matched Auditions destination](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/social/linkedin)

### Fas 5: Rapportering och optimering

**Programfunktioner:** [!DNL AJO B2B]: B2B-analysinstrumentpaneler

I denna fas fastställs ramverket för rapportering och analys för att mäta hur väl de olika grupperna presterar, hur effektiva deras kundresor är och vilka effekter de får. [!DNL AJO B2B Edition] innehåller inbyggda kontrollpaneler för analys. [!DNL CJA B2B Edition] (om den är licensierad) utökar analysen med djupare insikter på kontonivå mellan olika kanaler.

#### Beslut: Rapporteringsmetod

Vilka analysverktyg ska konfigureras för kontinuerlig prestandaövervakning?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Endast [!DNL AJO B2B] instrumentpaneler | Inbyggda kontrollpaneler för [!DNL AJO B2B Edition] räcker för att köpa grupper och resemått | Snabbast att konfigurera; omfattar B2B-statistik; begränsad kapacitet för anpassad analys |
| [!DNL AJO B2B] instrumentpaneler + [!DNL CJA B2B Edition] | Organisationen behöver djupare flerkanalsanalys, inköpsgruppsanalys, korrelation mellan affärsmöjligheter och anpassad attribuering | Kräver [!DNL CJA B2B Edition] licens; mest omfattande; stöder friformsanalys på kontonivå |
| [!DNL AJO B2B] instrumentpaneler + CRM-rapportering | Organisationen föredrar att centralisera pipelinerapporteringen i CRM tillsammans med köpgruppsmått | Kräver utveckling av kontrollpanelen i CRM; kombinerar marknadsförings- och försäljningsstatistik på ett ställe; begränsas till rapportfunktioner i CRM |

**Gränssnittsnavigering:** [!DNL AJO B2B Edition] > Kontrollpaneler > Översikt över engagemang/intelligent instrumentpanel

**Information om nyckelkonfiguration:**

- Använd [!DNL AJO B2B] Engagement Dashboard för att övervaka poängen för köpgruppsengagemang, fullständighetsgrader och scendistribution
- Använd den intelligenta Dashboard för AI-drivna insikter om kontoberedskap och pipeline-kvalitet
- Om du använder [!DNL CJA B2B Edition]: konfigurera en kontobaserad CJA-anslutning med [!DNL AJO B2B] datauppsättningar, konfigurera en B2B-datavy med Buying Group- och Account-behållare och bygg en arbetsyteanalys för att köpa gruppprogression, korrelation för affärsmöjlighet och attribuering
- Definiera rapportslut: Veckovisa resultatgranskningar av inköpsgrupper, månatlig analys av pipeline-effekter, kvartalsvis programoptimering
- Skapa anteckningar för viktiga händelser (kampanjstarter, innehållsuppdateringar, poängmodelländringar) för att korrelera med prestandatender

**Experience League-dokumentation:**

- [Kontrollpaneler för B2B-analyser](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/dashboards/buying-groups-dashboard)
- [Instrumentpanel för engagemang](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/dashboards/engagement-dashboard)
- [Intelligent kontrollpanel](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/dashboards/intelligent-dashboard)
- [CJA B2B edition - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

## Implementeringsöverväganden

Följande avsnitt behandlar skyddsförslag, vanliga fallgropar, bästa praxis och avbrottsbeslut som ska beaktas vid implementeringen.

### Skyddsritningar och begränsningar

- Gränser för kontoresa, inklusive högsta antal samtidiga resor och högsta antal konton per resa, följer [!DNL AJO B2B Edition] produktsäkerhetsutkast - [AJO B2B-skyddsutkast](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/guide-overview) [!DNL AJO B2B Edition]
- [!DNL RT-CDP B2B Edition] har stöd för upp till 50 B2B-schemaklasser och följer standardprofiler och skyddsprofiler för segmentering - [Kundprofiler i realtid](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/guardrails)
- Utvärdering av målgrupp för konto utförs på batchscheman. Uppdateringar av målgrupper för realtidskonton stöds inte för alla segmenttyper - [Segmenteringsskyddsutkast](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/guardrails)
- Inmatning av B2B-källanslutning har minimala schemaläggningsintervall (vanligtvis 15 minuter för [!DNL Marketo], varierande för CRM-källor) — [Inmatningsskydd](https://experienceleague.adobe.com/sv/docs/experience-platform/ingestion/guardrails)
- E-postkanalsytor är begränsade till 10 per kanaltyp per sandlåda - [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/get-started/guardrails)

### Vanliga fallgropar

- **Om du definierar för många roller per inköpsgrupp:** Överspecificerade roller (t.ex. 8-10 distinkta personer) blir det nästan omöjligt för inköpsgrupper att nå sluttröskeln. Börja med 3-5 viktiga roller och utöka allt eftersom modellen utvecklas.
- **Inställning av tröskelvärden för engagemangspoäng för höga eller för låga:** Om tröskelvärdena är för höga kvalificerar inga inköpsgrupper sig, vilket leder till att pipeline startas. För låg översvämningsförsäljning för okvalificerade konton. Börja med dataanalys av historiska data (om sådan finns) och iterera baserat på försäljningsfeedback.
- **Ignorerar matchningskvalitet från människa till konto:** Om personer inte är korrekt kopplade till konton, kommer inköpsgrupper att ha saknade medlemmar även om rätt personer är engagerade. Investera i kvalitet på identitetsupplösning innan ni börjar köpa gruppresor.
- **Meddelandekontakter i flera inköpsgrupper:** En enskild kontakt kan ha roller i flera inköpsgrupper (till exempel en CTO som är en teknisk utvärderare för både CRM- och Data Platform-inköp). Utan frekvenshantering får den här personen e-post från varje aktiv resa. Implementera regler för frekvens mellan resor.
- **Negerande säljaktivering:** Säljarna måste förstå hur de ska tolka inköpsgruppsdata, engagemangspoäng och försäljningsaviseringar. Utan utbildning och implementering misslyckas överföringen från marknadsföring till försäljning oavsett datakvalitet.
- **Behandlar kontoresor som personresor:** Kontoresor fungerar på kontonivå och skickar e-post till personer inom kontots inköpsgrupper. Resedesignen måste ta hänsyn till att flera personer får meddelanden per körning av kontonod, vilket skiljer sig i grunden från [!DNL AJO]-resor på personnivå.

### God praxis

- **Börja med ett lösningsintresse och expandera** - Bevisa modellarbetet för en inköpsrörelse innan du skalar efter flera lösningsintressen. Detta gör att teamet kan förfina rollmallar, poängsättningsmodeller och innehåll innan de lägger till komplexitet.
- **Justera inköpsgruppsroller med CRM-försäljningsprocessen** - Mappa inköpsgruppsroller till de profiler som säljteamet redan känner igen. Använd samma språk (ekonomisk köpare, Champion osv.) så överlämningen är intuitiv.
- **Implementera en feedbackslinga med försäljning** - Samla regelbundet in feedback om kvaliteten på marknadsföringskvalificerade konton. Använd den här informationen för att finjustera poängtrösklar för engagemang och kriterier för rollkvalificering.
- **Designa innehåll för roller, inte bara för stadier** - Olika inköpsgruppsroller behöver olika innehåll: chefer vill ha ROI och strategisk effekt, tekniska utvärderare vill ha arkitektur och integreringsinformation, slutanvändarna vill ha lättanvända demonstrationer. Mappa innehållsmaterial till roller för effektivare hantering.
- **Konfigurera CRM-försäljningsinsikter tidigt** - Vänta inte tills hela kundresan är live för att distribuera CRM-synlighet. Säljarna måste se hur man skapar gruppdata tidigt för att kunna ge feedback om rollernas exakthet och målgruppsanpassning.
- **Använd väntesteg strategiskt** - B2B-köpcyklerna är långa. Väntestegen för kundresan bör återspegla denna verklighet (5-14 dagars intervall mellan kontakterna) i stället för att vara konsumentvänliga (1-3 dagar).
- **Övervaka engagemangshastigheten, inte bara engagemangspoängen** - En inköpsgrupp som går från poängen 20 till 80 på två veckor signalerar starkare avsikter än en som når 80 på sex månader. Konfigurera poängsättning och kvalificering för att ta hänsyn till snabbheten.

### Avvecklingsbeslut

Följande kompromisser bör utvärderas utifrån din organisations specifika behov.

#### Slutlighet för köp av grupp jämfört med pipeline-volym

Kravet på att alla roller ska fyllas innan en inköpsgrupp kvalificeras maximerar kvaliteten på pipeline men kan avsevärt begränsa volymen kvalificerade konton, särskilt för nya produkter eller marknader där organisationens databas har begränsad täckning.

- **Högre fullständighetströskelvärde prioriterar:** Pipeline-kvalitet; försäljningen får fullt formade inköpsgrupper; högre vinstnivåer per konto
- **Lägre tröskelvärde för fullständighet prioriterar:** Rörvolym; fler konton når försäljning; större täckning; högre volym men eventuellt lägre kvalitet
- **Rekommendation:** Börja med ett måttligt tröskelvärde (60-70 % rolltäckning) och justera baserat på faktiska vinstfrekvensdata. För etablerade marknader med god datatäckning ökar du mot 80 %+. För nya marknader ska du ta emot 50-60 % från början och använda kampanjer för att åtgärda luckor i inköpsgruppen.

#### Korrigera granularitet jämfört med enkel drift

Mycket detaljerade poängsättningsmodeller (med dussintals aktivitetstyper, nyvägning och rollspecifik poängsättning) ger exaktare kvalificeringssignaler men är svårare att underhålla, förklara och felsöka.

- **Högre detaljrikedom:** Kvalifikationsgrad, nyansskillnader mellan konton, bättre anpassning till komplexa inköpsprocesser
- **Mindre granularitet:** Driftenkelhet, enklare att underhålla och förklara för försäljning, snabbare implementering, färre kantfall
- **Rekommendation:** Börja med en enkel poängmodell (10-15 aktivitetstyper, enhetliga poängvärden) och lägg till komplexitet endast när den enkla modellen inte kan särskilja kontokvaliteten. Dokumentera poängmodellen noggrant för försäljningsjustering.

#### Enskild resa jämfört med flera specialiserade resor

En enda heltäckande kontoresa som hanterar alla faser och lösningsintressen på en arbetsyta ger enhetlig kontroll, men kan bli ohanterlig. Flera specialiserade resor (en per fas eller lösningsintresse) är enklare individuellt men svårare att samordna.

- **Enskild resa prioriterar:** Holistisk vy; enklare att säkerställa konsekvent timing och meddelanden; enklare att övervaka; en plats för all logik
- **Flera resor gynnar:** Modularitet, enklare att uppdatera en fas utan att påverka andra, olika team kan äga olika resor, renare design av arbetsytan
- **Rekommendation:** För alternativ A är en enda resa lämplig. För alternativ B och C, använd en primär&quot;orkestrationsresa&quot; som dirigerar konton till specialiserade delresor per lösningsintresse eller inköpsfas.

## Relaterad dokumentation

Följande resurser innehåller mer information om de program och funktioner som det hänvisas till i den här handboken.

### [!DNL AJO B2B Edition]

- [AJO B2B edition - dokumentation - startsida](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/guide-overview)
- [Översikt över inköpsgrupper](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-overview)
- [Lösningsintressen](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/buying-groups/solution-interests)
- [Rollmallar](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-role-templates)
- [Skapa inköpsgrupper](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-create)
- [Köpgruppsfaser](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)
- [Översikt över kontoresor](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/account-journeys/journey-overview)
- [Nod för kontoresa](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/account-journeys/journey-nodes)
- [E-postmeddelanden om försäljningsaviseringar](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sales-alert-email)
- [Försäljningsinsikter för CRM](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/crm-sales-insights)

### E-post och innehåll från B2B

- [Framtagning av e-post från B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/email-authoring)
- [SMS-redigering i AJO B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sms-authoring)
- [AI-assistenten för att skapa e-post](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/ai-assistant-emails)

### B2B-analyser och kontrollpaneler

- [Instrumentpanel för inköpsgrupper](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/dashboards/buying-groups-dashboard)
- [Instrumentpanel för engagemang](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/dashboards/engagement-dashboard)
- [Intelligent kontrollpanel](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/dashboards/intelligent-dashboard)
- [CJA B2B edition - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

### [!DNL RT-CDP B2B Edition]

- [RT-CDP B2B edition - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview)
- [B2B-scheman i Real-Time CDP](https://experienceleague.adobe.com/sv/docs/experience-platform/rtcdp/schemas/b2b)
- [Målgrupper](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/types/account-audiences)
- [Marketo Engage källanslutning](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)

### Data Foundation

- [XDM - systemöversikt](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/home)
- [Översikt över identitetstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/home)
- [Översikt över källor](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/home)
- [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/home)

### Kanalkonfiguration

- [Kom igång med e-postkonfiguration](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Konfigurera SMS-kanal](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)

### Datastyrning och sekretess

- [Översikt över dataförvaltning](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/home)
- [Avancerad livscykelhantering av data](https://experienceleague.adobe.com/sv/docs/experience-platform/data-lifecycle/home)

### Destinationer

- [Översikt över destinationer](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/home)
- [Målkatalog](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/overview)
- [LinkedIn Matched Auditions destination](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/social/linkedin)

### Skyddsräcken

- [Garantier för kundprofiler i realtid](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/guardrails)
- [Skyddsritningar för segmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/guardrails)
- [Förvaringsskydd](https://experienceleague.adobe.com/sv/docs/experience-platform/ingestion/guardrails)
- [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/get-started/guardrails)

### Självstudiekurser och komma igång

- [Komma igång med AJO B2B edition](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/guide-overview)
- [RT-CDP B2B edition, genomgång](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-tutorial)
