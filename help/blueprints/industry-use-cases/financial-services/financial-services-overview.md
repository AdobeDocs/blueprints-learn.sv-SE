---
title: Användningsexempel för finansiella tjänster
description: Se hur finanssektorn använder Adobe Experience Platform för att personalisera sina erbjudanden, förhindra bortfall och fördjupa kundrelationerna.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '2209'
ht-degree: 1%

---


# Användningsexempel för finansiella tjänster

Finanssektorn förlitar sig på Adobe Experience Platform för att sammanställa kunddata över bank-, utlåning- och investeringskanaler, vilket möjliggör personaliserade upplevelser som stärker relationerna och ökar tillväxten. Genom att sammanföra kontoaktivitet, transaktionshistorik och beteendesignaler kan dessa organisationer leverera rätt erbjudande vid rätt tillfälle samtidigt som de upprätthåller det förtroende och den efterlevnad kunderna förväntar sig.

## Högvärdesundervisning

Identifiera värdefulla presumtiva kunder baserat på profildata och beteende och ge dem sedan personaliserat innehåll och erbjudanden via automatiserade resor. Genom att kombinera demografiska detaljer, surfningsaktiviteter och engagemangssignaler kan finansinstitut prioritera de leads som mest sannolikt konverterar och vägleda dem genom en skräddarsydd väg mot att bli kunder.

### Affärspåverkan

Organisationer som implementerar högvärdig ledande tillverkning ser vanligtvis en ökning på 25-35 % av konverteringsgraden från lead till kund och skapar en friskare och mer förutsägbar säljpipeline.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg om du vill skapa automatiserade vårdsekvenser som anpassar sig utifrån den potentiella kundens engagemang och beredskapssignaler.

### Tekniska överväganden

- Integrera CRM-data för ledarbedömning och webbplatsbeteenden i enhetliga profiler för potentiella kunder för att underlätta ingången till kundresan och förgrenade logik.
- Se till att inställningarna för samtycke och deltagande upprätthålls vid alla kontaktytor, särskilt för telefon- och e-postutskick som styrs av regler för finansiell marknadsföring.
- Konfigurera resestoppling för att undvika överväldigande möjligheter med olika kommunikationssätt under korta utvärderingsfönster.
- Ta hänsyn till datalatens mellan lokala interaktioner eller rådgivningsinteraktioner och digitalt engagemang för att hålla meddelanden på rätt plats.


## Produktrekommendation för befintliga kunder

Rekommendera relevanta finansiella produkter som kreditkort, lån och investeringsprodukter till befintliga kunder utifrån deras profil, transaktionshistorik och livscykelstadium. I det här användningsexemplet förvandlas data från det dagliga kontot till användbara insikter som visar på nästa bästa produkt för varje kund.

### Affärspåverkan

Personaliserade produktrekommendationer ger en 20-30-procentig ökning av produktacceptansen och ökar kundens livstidsvärde genom att öka plånboksandelen.

### Implementera

Använd mönstret [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) för att utvärdera varje kund mot berättigade produkterbjudanden i realtid och rangordna rekommendationer utifrån relevans och affärsprioritet.

### Tekniska överväganden

- Sammanställ transaktionsdata, kontosaldon och produktinnehav i en enda kundprofil så att beslutsmodellerna får en fullständig bild av befintliga relationer.
- Använd regler för finansiell lämplighet och lagstadgade begränsningar för behörighet som strikta garantivillkor i beslutsmotorn innan du rangordnar erbjudanden.
- Koordinera leverans av erbjudanden för onlinebanktjänster, mobilappar, e-post och rådgivare för att förhindra konflikter eller dubblerade rekommendationer.
- Implementera frekvensbegränsning per produktkategori för att undvika rekommendationstvång, särskilt för högkvalitativa produkter som hypotekslån och investeringskonton.


## Kampanjer för att förebygga skador

Identifiera kunder som riskerar att bli rejäla med hjälp av AI-driven churn-förutsägelse och engagera dem med lojalitetserbjudanden och personaliserad kommunikation. Tidig upptäckt av uppsägningssignaler gör det möjligt för finansinstituten att ingripa innan en kund stänger konton eller flyttar tillgångar någon annanstans.

### Affärspåverkan

Förebyggande åtgärder mot bortfall av bortfall minskar vanligtvis kundattribueringen med 15-25 %, skyddar återkommande intäktsströmmar och sänker kostnaden för att ersätta kunder.

### Implementera

Använd mönstret [Cross-Channel Journey with Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) om du vill utlösa kvarhållningsresor när bortfallsriskpoäng överskrider definierade tröskelvärden, med inbäddad beslutsamhet om du vill välja det mest övertygande kvarhållningserbjudandet.

### Tekniska överväganden

- Feed-kontoaktivitetstrender, tjänstinteraktionshistorik och interaktionsfrekvens i [!DNL Customer AI] modeller för kurendebenägenhet för att generera riskpoäng.
- Definiera tröskelvärden för bortfallsrisk som är specifika för produktlinjer, eftersom utfallssignaler för kontokontroll skiljer sig från dem för investeringsportföljer.
- Se till att erbjudandena om kvarhållande uppfyller kraven för rättvis utlåning och lika behandling så att högrisksegment får en rättvis behandling.
- Bygg en undertryckningslogik för att utesluta kunder som är bortskurna på grund av bedrägeri eller efterlevnadsåtgärder, där lojalitetsinriktning skulle vara olämpligt.


## Kontrollpanel för anpassat konto

Anpassa onlinebankernas kontrollpanel och mobilappsupplevelsen utifrån varje kunds kontoaktivitet, preferenser och ekonomiska mål. En skräddarsydd kontrollpanel hjälper kunderna att hitta det som är viktigast och hitta relevanta insikter utan att de behöver söka.

### Affärspåverkan

Personaliserade instrumentpaneler ökar engagemanget med 30-40 % och förbättrar kundnöjdheten på ett meningsfullt sätt genom att göra digitala bankkontakter intuitiva och relevanta.

### Implementera

Använd mönstret [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) för att leverera personaliserade innehållsblock, produktspotlights och ekonomiska insikter i realtid i autentiserade digitala upplevelser.

### Tekniska överväganden

- Utnyttja [!DNL Edge Network] för undersekundspersonaliseringsbeslut i autentiserade banksessioner där latensen direkt påverkar användarupplevelsen.
- Samla transaktionsdata i förberäknade profilattribut som utgiftskategorier och trender för besparingar för att undvika att stora datauppsättningar beräknas i realtid.
- Följ tillgänglighetsstandarder och se till att personaliserat innehåll uppfyller samma krav på offentliggörande som statiskt innehåll.
- Samordna personaliseringslogiken mellan webb- och mobilkanaler så att kunderna ser en enhetlig upplevelse oavsett enhet.


## Produkterbjudanden baserade på livscykelstadium

Identifiera kunder som går in i nya livsstadier som giftermål, hemköp eller pension och erbjud proaktivt relevanta finansiella produkter och tjänster. Genom att förutse dessa milstolpar kan institutioner positionera sig som betrodda partner under viktiga finansiella stunder.

### Affärspåverkan

Erbjudanden som triggas av nya livsfaser får en 35-45-procentig produktanvändning, vilket avsevärt överträffar generiska kampanjer, samtidigt som de stärker långsiktiga kundrelationer.

### Implementera

Använd mönstret [Flerkanalsresor med Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) för att identifiera indikatorer för livscykelstadium och skapa multitouch-resor med inbäddat erbjudande som är skräddarsytt för varje milstolpe.

### Tekniska överväganden

- Kombinera förstahandssignaler som adressändringar, öppningar av gemensamma konton och stora insättningar med tillåtna tredjepartsdata för att skapa övergångar i livstid.
- Hantera känsliga händelser i livet med försiktighet med avseende på ton och frekvens för meddelanden, eftersom felaktigt identifierade milstolpar kan urholka förtroendet.
- Lagrets lagkrav kontrolleras i anbudsbesluten så att rekommenderade produkter anpassas till kundens verifierade ekonomiska situation.
- Bygg avkylningsperioder mellan livstidsbaserade kampanjer för att förhindra överlappande outreach när flera indikatorer utlöses i ett kort fönster.


## Transaktionsbaserade aviseringar och rekommendationer

Skicka aviseringar i realtid om transaktioner och skräddarsy rekommendationer baserat på utgiftsmönster och kontoaktivitet. Lämpliga meddelanden i rätt tid håller kunderna informerade och skapar naturliga ögonblick för att få användbar ekonomisk vägledning.

### Affärspåverkan

Transaktionsbaserade aviseringar uppnår en 50-60-procentig engagemangsnivå, vilket dramatiskt förbättrar säkerheten och skapar värdefulla kontaktytor för personaliserade rekommendationer.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) om du vill svara på transaktionshändelser i realtid med varningar och sammanhangsberoende rekommendationer.

### Tekniska överväganden

- Importera transaktionshändelser via en direktuppspelningspipeline med leveransvillkor med låg fördröjning, eftersom säkerhetsvarningar förlorar värde om de fördröjs med mer än några minuter.
- Använd kunddefinierade aviseringsinställningar och tröskelvärden så att meddelanden återspeglar enskilda inställningar i stället för regler som passar alla.
- Skilj de obligatoriska säkerhetsvarningarna från de valfria rekommendationsmeddelandena i meddelandearkitekturen för att säkerställa att meddelanden om regelefterlevnad aldrig inaktiveras.
- Ta hänsyn till stora transaktionsvolymer under perioder med hög belastning, som betaldagar och helger, genom att utforma en flödeskapacitet som kan anpassas efter efterfrågan.


## Återvinning av kreditkortsansökningar

Identifiera kunder som började men inte slutförde kreditkortsansökningar och engagera dem på nytt med personaliserade meddelanden och erbjudanden. Att överge program är en målgrupp med hög återgivning som ofta bara behöver en liten knuff för att slutföra processen.

### Affärspåverkan

Kampanjer för återfinnande av övergivna kunder förbättrar andelen slutförda ansökningar med 20-30 %, vilket direkt ökar antalet nya konton hos en publik som redan har uttryckt intresse.

### Implementera

Använd mönstret [Event-Triggered Messaging](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) om du vill identifiera händelser för programavbrott och utlösa aktuella uppföljningsmeddelanden som åtgärdar vanliga orsaker till programbortfall.

### Tekniska överväganden

- Fånga det specifika steget där programmet övergavs för att skräddarsy meddelanden, eftersom någon som slutade vid identitetsverifieringen behöver en annan trygghet än någon som lämnade villkoren.
- Uppfyll alla regler för kreditmarknadsföring, inklusive obligatoriska upplysningar och regler för rättvis utlåning i all kommunikation om återkrav.
- Implementera tidsminskningslogik så att återställningsutåtgången upphör efter ett definierat fönster, eftersom inaktuella programdata kanske inte längre är giltiga för förkvalificering.
- Koordinera med ansökningssystemet för att utelämna återkravsmeddelanden för sökande som har slutfört via en annan kanal, till exempel ett filialbesök eller ett telefonsamtal.


## Investera Portfolio Recommendations

Tillhandahåll personaliserade investeringsrekommendationer baserade på varje kunds riskprofil, investeringshistorik och finansiella mål. Med datadriven portföljvägledning kan kunderna fatta välgrundade beslut samtidigt som de fördjupar sitt engagemang med förmögenhetshanteringstjänster.

### Affärspåverkan

Personaliserade investeringsrekommendationer leder till en ökning på 25-35 % när det gäller produktanpassning och förbättrar portföljdiversifieringen över hela kundbasen.

### Implementera

Använd mönstret [Beteenderekommendation](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) för att analysera investeringsbeteenden och preferenser och sedan visa relevanta portföljrekommendationer via digitala kanaler och rådgivningsverktyg.

### Tekniska överväganden

- Integrera förmedling och förvaring av dataflöden för att få en korrekt och aktuell bild av varje kunds aktuella innehav och allokering.
- Genomföra lämplighetskrav som regleras av värdepapperslagstiftningen så att rekommendationerna överensstämmer med kundens dokumenterade risktolerans och investeringsmål.
- Ange tydligt personaliserat investeringsinnehåll som utbildningsmaterial eller information där så krävs, och skilj det från formell investeringsrådgivning som uppfyller förvaltningsförpliktelser.
- Uppdatera rekommendationsmodellerna regelbundet för att ta hänsyn till förändringar på marknaden, portföljutveckling och förändringar i kundens mål.


## Bedrägerivarning Personalization

Anpassa varningar om bedrägerier och säkerhetskommunikation baserat på varje kunds kommunikationsinställningar och tidigare interaktionshistorik. Skräddarsydda varningar ökar sannolikheten för att kunderna märker, förstår och agerar på viktiga säkerhetsmeddelanden.

### Affärspåverkan

Personaliserade bedrägerivarningar förbättrar svarsfrekvensen med 40-50 %, vilket avsevärt stärker säkerheten och minskar tidsfönstret för exponering under misstänkt aktivitet.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) för att leverera bedrägerivarningar via varje kunds önskade kanal med kontextuella detaljer som gör det enkelt att bekräfta eller tvisteaktivitet.

### Tekniska överväganden

- Prioritera leveranshastighet och tillförlitlighet framför alla andra designöverväganden, eftersom fördröjning för bedrägerivarning direkt korrelerar med exponering för ekonomiska förluster.
- Vidarebefordra aviseringar via kundens verifierade föredragna kanal och bevara reservkanalerna för att säkerställa leveransen även om den primära kanalen misslyckas.
- Lagra interaktionshistorik för att förbättra framtida larmrelevans och minska den falska positiva tröttheten för kunder som ofta reser eller gör atypiska inköp.
- Se till att allt innehåll och alla arbetsflöden för bedrägerivarning följer banksäkerhetslagstiftningen och att känslig kontoinformation inte visas i förhandsgranskningar eller ämnesrader.


## Lojalitetsprogramengagemang

Anpassa kundens kundrelationer, belöningar och erbjudanden baserat på kundens nivå, poängbalans och inlösenhistorik. Relevant, vältajmad kundlojalitet håller medlemmarna engagerade och främjar ett högre deltagande i programmet.

### Affärspåverkan

Personaliserat lojalitetsengagemang ökar deltagandet i programmet med 30-40 % och driver avsevärt högre poäng på inlösen, vilket stärker programmets uppfattning om värdet.

### Implementera

Använd mönstret [Flerkanalsresa med Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) för att koordinera lojalitetskommunikation över olika kanaler, med inbäddad decimering för att välja den mest relevanta belöningen eller erbjudandet för varje medlem.

### Tekniska överväganden

- Synkronisera data för lojalitetsplattformen inklusive skiktstatus, poängsaldon och inlösenhistorik i kundprofiler i nära realtid för att undvika att befordra utgånna eller felaktiga saldon.
- Segmentera logiken för kundresan efter nivå för att leverera differentierade upplevelser, eftersom medlemmar i högnivågruppen förväntar sig exklusiv behandling och tidig tillgång till kampanjer.
- Samordna lojalitetsmeddelanden med bredare marknadsföringskampanjer för att förhindra att budskapen tröttnar ut och att erbjudandena hamnar i konflikt mellan olika program.
- Spåra inlösenattribuering över flera kanaler för att mäta vilken personaliserad kommunikation som ger störst avkastning på investeringen.


## Kampanjer för förgodkännande av lån

Rikta er till kunder som sannolikt kommer att vara på marknaden för en inteckning baserat på profildata, beteendesignaler och indikatorer för livsfaser. Med proaktivt förhandsgodkännande blir institutionen ett bekvämt förstahandsval i samband med ett av de största finansiella beslut kunden kommer att fatta.

### Affärspåverkan

Inriktade kampanjer före godkännande av lån ökar ansökningsfrekvensen med 20-30 % och förbättrar lånevolymen genom att nå kvalificerade presumtiva kunder vid rätt tillfälle.

### Implementera

Använd mönstret [Multi-Step Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) för att vägleda inteckningspotentiella kunder genom en interaktionssekvens från medvetenhet till förgodkännande, och anpassa den baserat på engagemang- och kvalificeringssignaler.

### Tekniska överväganden

- Kombinera sökbeteenden i fastigheter, trender för sparökning och utgångssignaler för leasing för att skapa en benägenhetsmodell som identifierar sannolika lånesökande.
- Se till att alla meddelanden om förhandsgodkännande följer reglerna för annonsering på hypotekslån, inklusive obligatoriska upplysningar, korrekt taxering och likvärdigt bostadsspråk.
- Samordna kampanjtimingen med prisförändringar så att utåtgången anpassas till förmånliga lånevillkor och undviker föråldrade räntereferenser.
- Bygg arbetsflöden för låneansvariga så att digitalt vårdade leads smidigt kan gå över till den formella ansöknings- och garantiprocessen.


## Personaliserat innehåll för finansiell utbildning

Leverera skräddarsytt utbildningsmaterial, tips och resurser baserat på varje kunds ekonomiska profil, mål och intressen. Relevant utbildningsmaterial bygger upp förtroende, förbättrar den ekonomiska kompetensen och skapar organiska möjligheter att införa relevanta produkter.

### Affärspåverkan

Personaliserat utbildningsinnehåll ökar engagemanget för innehåll med 25-35 % och förbättrar kundens ekonomiska kompetens, vilket i sin tur skapar en säkrare produktanvändning.

### Implementera

Använd mönstret [Flerkanalsresor med beslutande](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) om du vill leverera en strukturerad sekvens av utbildningsinnehåll i olika kanaler, och använda beslut för att matcha ämnen med varje kunds ekonomiska situation och intressen.

### Tekniska överväganden

- Koppla utbildningsinnehåll till attribut i den finansiella profilen, t.ex. skuldsättningsgrad, besparingsgrad och investeringserfarenhet, för att säkerställa ämnesrelevans.
- Tagga innehåll med svårighetsgrad och nödvändiga ämnen för att skapa progressiva utbildningsvägar i stället för att leverera fristående artiklar.
- Spåra innehållsengagemang på ämnesnivå för att förfina personaliseringsmodeller och identifiera nya intresseområden i hela kundbasen.
- Se till att utbildningsmaterial tydligt skiljer sig från produktmarknadsföring för att upprätthålla regelefterlevnad och bevara kundernas förtroende för programmets objektivitet.
