---
title: Handlingar
description: Upptäck hur sjukvårdsorganisationer använder Adobe Experience Platform för att förbättra patienternas engagemang, effektivisera samordningen av vården och få bättre hälsoresultat.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: 8da82711-a783-488d-a0ed-070b33ecbbc4
source-git-commit: 0236bd326730ee9a0be621ee0e60ddc3d352410d
workflow-type: tm+mt
source-wordcount: '3818'
ht-degree: 0%

---

# Handlingar

Sjukvårdsorganisationer använder Adobe Experience Platform för att skapa enhetliga patientprofiler och leverera personaliserad kommunikation i rätt tid över alla kontaktytor. Genom att knyta samman kliniska data, beteendedata och preferensdata på ett och samma ställe kan vårdpersonal engagera patienter mer effektivt samtidigt som högsta standard för sekretess och efterlevnad upprätthålls.

>[!IMPORTANT]
>Fall av hälso- och sjukvårdsanvändning omfattar skyddad hälsoinformation (PHI) som omfattas av HIPAA och andra tillämpliga bestämmelser. Innan du implementerar något av dessa mönster måste du se till att [!DNL Adobe Experience Platform] har etablerats som en HIPAA-kvalificerad tjänst och att ett Business Associate-avtal (BAA) har skapats med Adobe. De tekniska övervägandena i varje avsnitt belyser viktiga krav på efterlevnad, men är inte uttömmande. Samarbeta med era jurister, regelefterlevnadsteam och säkerhetsteam för att validera implementeringen mot alla tillämpliga lagstadgade krav.

## Påminnelseautomatisering för avtalad tid

Skicka personliga påminnelser om möten via e-post, sms och push-meddelanden baserat på varje patients kommunikationsinställningar och typ av avtalad tid. Automatiska påminnelser minskar antalet missade avtalade tider och håller tidsplanerna smidigt och frigör personal för att fokusera på patientvården.

### Affärspåverkan

Organisationer som implementerar påminnelser om automatiska möten ser mätbara förbättringar av antalet avtalade tider och en meningsfull minskning av kostsamma inga visningar.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Skapande och uppdatering av avtalade tider från schemaläggningssystemet fungerar som naturliga utlösare för relevanta påminnelsemeddelanden i rätt tid. Detta är det rätta mönstret när en diskret avtalad tid utlöses och det svar som krävs är ett enda, tidskänsligt meddelande - snarare än en kontinuerlig engagemangssekvens, eftersom patienterna behöver en omedelbar bekräftelse utan uppföljningssteg.

### Tekniska överväganden

- Se till att all kontaktinformation och information om avtalade tider överförs och lagras i enlighet med HIPAA-kraven och använd lämpliga etiketter för att begränsa obehörig åtkomst.
- Integrera med det elektroniska systemet för schemaläggning av hälsoposter för att i realtid samla in händelser för att skapa, avbryta och schemalägga om möten.
- Använd regler för samtyckeshantering så att påminnelser endast skickas via kanaler som patienten uttryckligen har valt.
- Konfigurera undertryckningsregler för att förhindra dubbletter eller överdrivet många påminnelser när avtalade tider schemaläggs om i snabb följd.


## Kampanjer för läkemedelsefterlevnad

Skicka personliga påminnelser och utbildningsmaterial för att hjälpa patienterna att hålla sig à jour med sina medicineringsscheman och behandlingsplaner. Skräddarsytt budskap baserat på medietyp, doseringsschema och patienthistorik ger bättre följsamhet och förbättrade hälsoresultat.

### Affärspåverkan

Personaliserade uppföljningskampanjer för medicinering bidrar till att förbättra följsamheten, vilket leder till bättre hälsoresultat och färre återbesök på sjukhus.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. För att upprätthålla medicineringen krävs en kontinuerlig, flerberöringsstrategi med eskalerande påminnelser, kontaktpunkter för utbildning och uppföljningskontroller under en behandlingsplan. Det här är det rätta mönstret eftersom medicinering kräver ett sekvensflöde med flera meddelanden på dagar eller veckor med villkorlig förgrening baserat på påfyllnadshändelser och engagemangssignaler - ett enda triggat meddelande kan inte hantera beroendelogiken mellan utbildningssteg och eskaleringsvägar.

### Tekniska överväganden

- Tillämpa strikta etiketter för dataanvändning på all skyddad hälsoinformation som rör läkemedel och diagnos för att förhindra otillåten aktivering längre fram i kedjan.
- Integrera med apotek och elektroniska patientjournalsystem för att ta emot data som fyller i och fyller i receptet och som triggar kundresan.
- Genomför kraftfull hantering av samtycke för att säkerställa att patienterna har gått med på att få läkemedelsrelaterad kommunikation och kan när som helst dra tillbaka sitt samtycke.
- Designa logik för kundresan för att upptäcka icke-engagemangsmönster och eskalera till vårdteamets meddelanden när en patient kan riskera att inte följa reglerna.


## Påminnelser om förebyggande vård

Påminn proaktivt patienter om rekommenderad förebyggande vård såsom vaccination, screening och årliga kontroller baserade på ålder, anamnes och riskfaktorer. Påminnelser om förebyggande vård i rätt tid bidrar till att täppa till luckor i vården och förbättra den allmänna folkhälsan.

### Affärspåverkan

Förebyggande förebyggande vård leder till bättre slutförandegrad av förebyggande vård, vilket bidrar till bättre folkhälsa och minskade kostnader för långtidsbehandling.

### Implementera

Använd mönstret [Aktivera utgående batchmeddelande](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md). Påminnelser om förebyggande vård ges bäst genom schemalagda batchkampanjer som utvärderar patienternas rätt till behandling i förhållande till kliniska riktlinjer med regelbunden uppföljning. Detta är det rätta mönstret när målgruppen är fördefinierad av kliniska riktlinjer och leveranstider är schemalagda på en vanlig cadence snarare än händelsestyrd, och ingen förgrening eller beslut krävs i realtid.

### Tekniska överväganden

- Bygg målgruppssegment med hjälp av kliniska riktlinjer (ålder, kön, familjehistoria, tidigare screeningdatum) och lägg in dataanvändningsetiketter i all skyddad hälsoinformation som används vid segmentering.
- Samordna med kliniska team för att säkerställa att påminnelseinnehållet överensstämmer med befintliga evidensbaserade riktlinjer för förebyggande vård och organisationsprotokoll.
- Implementera frekvensbegränsning för att undvika överväldigande patienter som samtidigt är kvalificerade för flera förebyggande behandlingsrekommendationer.
- Upprätthåll en verifieringskedja över all information om förebyggande vård som skickas för regelmässig rapportering och dokumentation av kvalitetsmått.


## Uppföljningskampanjer efter besök

Skicka automatiskt enkäter, omvårdnadsinstruktioner och påminnelser efter besök baserat på typ av besök och varje patientes specifika behov. En snabb uppföljning ger nöjdare patienter och säkerställer kontinuitet i vården efter varje besök.

### Affärspåverkan

Automatiserade uppföljningskampanjer efter besök ger bättre svarsfrekvens för undersökningar och högre poängvärden för patientnöjdhet.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Besök slutförandehändelser från det elektroniska patientjournalsystemet som ger en naturlig och snabb utlösare för uppföljningskommunikation som är skräddarsydd för påräkningstypen. Det här är det rätta mönstret när en händelse för att slutföra ett besök är utlösaren och det svar som krävs är en omedelbar uppföljning som är skräddarsydd för att hitta typ - snarare än en sekvens i flera steg, eftersom varje besök genererar ett eget oberoende uppföljningsbehov.

### Tekniska överväganden

- Integrera med det elektroniska patientjournalsystemet för att få besök vid avslutningshändelser som omfattar besökstyp, leverantör och relevanta vårdinstruktioner utan att visa fullständiga kliniska anteckningar.
- Lägg in dataetiketter i all vårdinformation för att säkerställa att den skyddade hälsoinformationen endast delas via säkra, patientgodkända kanaler.
- Konfigurera timingregler som tar hänsyn till besökstyp - t.ex. kan uppföljning efter operation kräva annan timing än rutinundersökningar.
- Inkludera säkra länkar till patientportalen för slutförande av undersökningar och schemaläggning av möten i stället för att samla in hälsoinformation via osäkra kanaler.


## Program för hantering av kroniska sjukdomar

Personalisera kommunikation om hantering av kroniska sjukdomar, utbildningsmaterial och övervaka påminnelser baserat på varje patientes specifika tillstånd och behandlingsplan. Bibehållet, relevant engagemang hjälper patienterna att ta en aktiv roll när det gäller att hantera sin hälsa över tid.

### Affärspåverkan

Personaliserade program för hantering av kroniska sjukdomar ser ökad delaktighet i programmet, vilket leder till bättre sjukdomshanteringsresultat och minskat utnyttjande av akutvård.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. Hantering av kronisk sjukdom är i sig en långvarig, flerpunktsupplevelse som kräver adaptiva meddelanden baserat på patientengagemang och milstolpar inom hälsoområdet. Detta är det rätta mönstret eftersom hantering av kroniska sjukdomar kräver adaptiva meddelanden under en längre period med villkorlig förgrening baserad på kliniska mätvärden och engagemangsmönster - händelseutlösta meddelanden kan inte hantera den pågående dynamiska omprövningen som behövs för att justera interventioner baserat på förändrade hälsodata.

### Tekniska överväganden

- Designa förgreningslogik som anpassar sig efter villkorsspecifika mätvärden (t.ex. blodglukostrender för diabeteshantering eller blodtrycksläsningar för hypertensionsprogram).
- Implementera strikt datastyrning med [!DNL Adobe Experience Platform]-etiketter för dataanvändning för att klassificera och skydda villkorsspecifika hälsodata under hela resan.
- Integrera med fjärranslutna patientövervakningsenheter och patientrapporterade resultatsystem för att mata in hälsodata i realtid till beslutsunderlag för resan.
- Bygg upp eskaleringsvägar för vårdteam under resan så att bristande engagemang eller gällande hälsotrender utlöser larm för lämplig klinisk personal.


## Ny introduktionsresa för patienter

Automatisera en introduktionsresa i flera steg för nya patienter som innehåller välkomstinformation, instruktioner för åtkomst till patientportalen och vägledning om schemaläggning av möten. En smidig introduktionsupplevelse sätter tonen för en engagerad och långsiktig patientrelation.

### Affärspåverkan

Automatiserade nya patientintroduktionsresor bidrar till att öka antalet portalaktiveringar och stärka det tidiga patientengagemanget.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. Patientintroduktion är en naturligt sekventiell flerstegsprocess där varje kommunikation bygger på det tidigare och anpassas beroende på om patienten har slutfört de viktigaste åtgärderna. Det här är det rätta mönstret eftersom introduktionen kräver ett sekventiellt, beroende flöde över flera dagar med förgreningar baserat på patientåtgärder (portalaktivering, ifyllnad av formulär) - ett enda meddelande eller en satsbaserad metod kan inte hantera det inbördes beroendet mellan steg eller anpassa sig till progressiv slutförande.

### Tekniska överväganden

- Integrera med patientregistreringssystemet för att utlösa introduktionsresan direkt när nya patientjournaler skapas, vilket ger ett snabbt första intryck.
- Använd identitetsupplösning för att sammanfoga befintliga poster (t.ex. från en webbplatsbesök eller en förfrågan om avtalad tid) med den nya patientprofilen för att undvika dubbla kommunikationer.
- Se till att portalaktiveringslänkar och autentiseringsuppgifter levereras via säkra, HIPAA-kompatibla kanaler och förfaller efter en angiven period.
- Designa resan för att upptäcka portalaktivering och händelser i samband med ifyllande av formulär så att efterföljande steg anpassas i stället för att upprepa information som patienten redan har agerat på.


## Personaliserat hälsoinnehållsleverans

Leverera personaliserat innehåll, hälsotips och resurser för hälsoutbildning som är skräddarsydda efter varje patientes villkor, intressen och hälsomål. Relevant innehåll bygger upp förtroende, förbättrar hälsoförståelse och ger patienter möjlighet att fatta välgrundade beslut om sin vård.

### Affärspåverkan

Personaliserat innehåll på hälsoområdet når upp till högre engagemang, vilket leder till förbättrad patientutbildning och hälsoförståelse.

### Implementera

Använd mönstret [Flerkanalsresa med beslut](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). Leverans av hälsoinnehåll drar nytta av realtidsbeslut som väljer det mest relevanta innehållet för varje patient baserat på deras villkor, önskemål och tidigare engagemang, som levereras via den kanal de föredrar. Det här är det rätta mönstret när innehållsvalet måste ta hänsyn till patientförhållanden, samtycke och kanalpreferenser samtidigt som det förhindrar duplicering eller utmattning av leveransen - i flerstegssamordning finns inte det realtidslager som behövs för att matcha dynamiskt innehåll med individuella patientbehov.

### Tekniska överväganden

- Använd etiketter för innehållsklassificering och dataanvändning på allt hälsoutbildningsmaterial för att säkerställa att villkorsspecifikt innehåll endast levereras till patienter som har samtyckt till att få hälsoinformation om det ämnet.
- Integrera beslutsmotorn med ett innehållsarkiv som regelbundet granskas och godkänns av kliniska team för att säkerställa medicinsk precision.
- Implementera regler för innehållströtthet för att undvika att innehåll på ett och samma tema skickas för mycket och för att balansera utbildningsmaterial över en patients olika hälsobehov.
- Spåra signaler om innehållsengagemang (öppningar, klick, tidsåtgång) för att kontinuerligt förfina innehållets relevans utan att samla in eller lagra ytterligare skyddad hälsoinformation.


## Meddelande om Lab-resultat

Meddela patienterna när labbresultaten är tillgängliga via den kommunikationskanal de föredrar med personaliserade, säkra meddelanden. Snabbmeddelanden uppmuntrar patienterna att granska resultaten snabbt och följa upp med vårdteamet när det behövs.

### Affärspåverkan

Automatiserade labbresultatmeddelanden hjälper till att öka tittarfrekvensen, förbättrar patientkommunikationen och möjliggör snabbare klinisk uppföljning när resultaten kräver åtgärder.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Tillgänglighet för Lab-resultat är en diskret händelse som kräver ett omedelbart, enda meddelande via den kanal patienten föredrar. Detta är det rätta mönstret när en diskret labbresultathändelse är utlösaren och det svar som krävs är en enda, omedelbar avisering - snarare än en sekvens med flera meddelanden, eftersom patienterna behöver en snabb avisering för att kontrollera portalen utan ytterligare uppföljningskommunikation.

### Tekniska överväganden

- Inkludera aldrig faktiska labbresultatvärden i meddelandena - meddela bara patienten att resultaten är tillgängliga och dirigera dem till den säkra patientportalen för mer information.
- Integrera med laboratorieinformationssystemet för att ta emot resultatklara händelser samtidigt som strikta dataanvändningsetiketter används för att förhindra att kliniska data flödar in i marknadsföringskanalerna.
- Implementera leverantörsspärrlogik så att aviseringar skickas först efter att den behandlande läkaren har granskat och släppt resultaten för att kunna se dem.
- Kontrollera att alla meddelandelänkar pekar på autentiserade, krypterade patientportalsessioner som uppfyller HIPAA:s säkerhetskrav.


## Verifiering av försäkringsskydd

Kontrollera och förmedla information om försäkringsskydd till patienterna innan de utses för att minska faktureringsöverraskningarna och förbättra den övergripande patientupplevelsen. Tydlig kommunikation med direkt täckning skapar förtroende och minskar antalet faktureringstvister efter besök.

### Affärspåverkan

Proaktiv kontroll av försäkringsskydd resulterar i förbättrad bekräftelsefrekvens före besök och en meningsfull minskning av antalet faktureringstvister och patientklagomål.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Tidsplaneringshändelser för möten fungerar som en utlösare för att påbörja disponeringsverifiering och informera patienten om resultaten före besöket. Detta är det rätta mönstret när en diskret avtalad tid-schemaläggningshändelse är utlösaren och det svar som krävs är ett enda tidskänsligt meddelande om täckning - i stället för en interaktionssekvens i flera steg, eftersom patienten behöver ett tydligt meddelande innan han eller hon utses.

### Tekniska överväganden

- Integrera med system för verifiering av försäkringsberättigande för att få täckning i realtid utan att lagra fullständiga data om försäkringsanspråk på kunddataplattformen.
- Använd dataetiketter på all ekonomisk information och försäkringsinformation för att begränsa användningen till faktureringsrelaterad kommunikation.
- Konfigurera meddelandetimingen så att det finns tillräckligt med ledtider innan patienterna kan utses för att lösa eventuella täckningsproblem eller kontakta sin försäkringsleverantör.
- Inkludera tydliga instruktioner och kontaktinformation för faktureringsavdelningen så att patienterna kan ställa frågor eller tillhandahålla uppdaterade försäkringsdetaljer innan besöket.


## Påminnelser om avtalade tider för telehälsa

Skicka personliga påminnelser för telefonmöten med anslutningsanvisningar, tips och teknisk supportinformation. Effektiva påminnelser i telekombranschen minskar antalet missade virtuella besök och hjälper patienterna att känna sig säkra med hjälp av verktygen för digital vård.

### Affärspåverkan

Påminnelser om personliga möten i telekommunikationen bidrar till att förbättra antalet virtuella besök och påskynda det övergripande införandet av telhälso- och sjukvård i hela patientpopulationen.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Tidsplaneringshändelser för möten inom telehälsa är en naturlig utlösare för påminnelser i rätt tid som innehåller anslutningsinformation och vägledning om förberedelser. Detta är det rätta mönstret när ett diskret möte i telekommunikationen är utlösaren och det svar som krävs är en enda, omedelbar påminnelse med teknisk vägledning - snarare än en sekvens i flera steg, eftersom patienterna behöver tydliga instruktioner före tillsättningen utan efterföljande uppföljningsmeddelanden.

### Tekniska överväganden

- Inkludera plattformsspecifika anslutningsinstruktioner (dator eller mobil) baserat på patientens kända enhetsinställningar eller tidigare telefonhälsosessionsdata.
- Se till att alla länkar och sessionsidentifierare för telehälsoanslutning levereras via krypterade, HIPAA-kompatibla kanaler och förfaller efter det schemalagda fönstret för avtalad tid.
- Integrera med telekomplattformen för att identifiera när en patient har anslutit sig så att sekundära påminnelser kan undertryckas.
- Ange en reservsökväg till kontaktinformation för teknisk support för patienter som inte har anslutit inom ett definierat fönster innan besökets starttid.


## Välfärdsprogramsengagemang

Anpassa kommunikationen, utmaningarna och belöningen för välkända program utifrån varje patientes hälsomål, aktivitetsnivå och önskemål. Engagerande hälsoprogram motiverar patienterna att ta till sig mer hälsosamma vanor och upprätthålla ett långsiktigt välbefinnande.

### Affärspåverkan

Personaliserade kampanjer för hälsoprogram leder till ökad delaktighet i programmet, vilket bidrar till bättre hälsoresultat och ökad lojalitet hos patienten.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. Välfärdsprogram är varaktiga engagemangsupplevelser med flera milstolpar, utmaningar och belöningar som kräver adaptiv samordning baserat på patientens deltagande och framsteg. Det här är det rätta mönstret eftersom hälsoprogram kräver ett sekvensflöde med flera meddelanden under en längre period med villkorlig förgrening baserat på milstolpar för deltagande och engagemangsmönster - händelseutlösta meddelanden kan inte hantera den hållbara, adaptiva orkestrering som behövs för att justera utmaningar och belöningar baserat på pågående uppföljning av framsteg.

### Tekniska överväganden

- Integrera med dataflöden för kroppsburna och friskvårdsapplikationer och använd tydliga etiketter för dataanvändning för att skilja mellan hälsodata och data om klinisk hälsa som omfattas av strängare lagstadgade krav.
- Implementera samtyckeshantering som gör det möjligt för patienter att bevilja och återkalla tillstånd för insamling av hälsovårdsuppgifter oberoende av deras kliniska kommunikationsinställningar.
- Designa en logik som anpassar svårighetsgrad och kommunikationsfrekvens baserat på varje patients engagemangsmönster för att undvika obehag eller trötthet.
- Se till att belönings- och stimulansspårning följer gällande regler för hälso- och sjukvård kring patientinduktioner och krav på återförsäkring.


## Samordning mellan olika avdelningar

Möjliggör anpassad kommunikation och samordning mellan patienter och deras vårdpersonal baserat på vårdplanen och individuella önskemål. Bättre samordning leder till mer sömlösa behandlingsövergångar och förbättrade resultat för patienter med komplexa behandlingsbehov.

### Affärspåverkan

Effektiv kommunikation i form av samordning av vårdteam leder till bättre engagemang i vårdteam och bättre resultat av samordning av vården över flera vårdplaner.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. Samordning i vårdteam innefattar flera intressenter och kontinuerliga kommunikationsflöden som måste anpassas baserat på milstolpar i vårdplanen, förändringar av patientstatus och leverantörsåtgärder. Detta är det rätta mönstret eftersom vårdsamordning kräver adaptiva meddelandeflöden i flera steg som bygger på milstolpar för vårdplaner och leverantörsåtgärder för flera intressenter - ett enda meddelande eller ett enklare mönster kan inte hantera de komplexa, inbördes beroenden och rollbaserade meddelanderutiner som behövs i alla kliniska team.

### Tekniska överväganden

- Implementera rollbaserade åtkomstkontroller och etiketter för dataanvändning för att säkerställa att varje vårdteammedlem endast får patientinformation som är relevant för deras roll i vårdplanen.
- Integrera med system för hantering av vård och elektroniska patientjournaler för att få uppdateringar av vårdplanen, slutförda hänvisningar och övergångshändelser som utlöser samordningsmeddelanden.
- Designa olika kommunikationsvägar för patienttillvända och leverantörstillvända meddelanden och se till att klinisk terminologi används på rätt sätt för leverantörer medan patientmeddelandena förblir tydliga och tillgängliga.
- Upprätthåll en fullständig verifieringskedja över all kommunikation för samordning av vården för att uppfylla reglerna för kontinuitet och ackrediteringskrav.


## Patientresa Funnel och vårdmellanrumsanalys

Kartlägg hela patientresan, från inledande webbforskning till schemaläggning av möten, leverans av vård och uppföljning, för att identifiera var patienterna faller bort och vilka populationer som har brister i rekommenderad förebyggande eller kronisk vård. Hälsosystem som saknar synlighet för flerkanaliga resor kan inte skilja mellan schemaläggning av friktion och bortfall av patienter - vilket begränsar deras förmåga att förbättra tillgången och täppa till luckor i vården i stor skala.

### Affärspåverkan

Genom att förstå var patienter faller bort från behandlingsvägarna och vilka medlemssegment som har den högsta koncentrationen av vårdluckor kan ansvariga och marknadsföringsteamen fokusera på de yttre resurserna på populationer och friktionspunkter som kommer att ge den största förbättringen av vårdefterlevnaden.

### Implementera

Använd mönstret [Kundanalys och insiktsgenerering](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md). Den här metoden kopplar samman webb- och portalbeteendedata, poster för avtalade tider och vårdanspråk med Customer Journey Analytics, där bortfallsanalys mäter bortfall vid varje schemaläggnings- eller vårdsteg och kohortanalys identifierar vilka medlemssegment som har lägst noggrannhetsgrad. Detta är det rätta mönstret när målet är att generera insikter och analysera populationsnivå - förstå var resorna faller ned och vem som är mest i farozonen - i stället för att utlösa en outreach eller aktivera en suppressionslista.

### Tekniska överväganden

- Uppsägnings- och anspråksdata från kliniska system måste mappas till HIPAA-kompatibla XDM-scheman innan man får in i AEP, och dataanvändningsetiketter måste användas för att begränsa tillgången till skyddad hälsoinformation inom CJA datavyer.
- Identifierare av patienter eller medlemmar i webbportalen, schemaläggningssystemet och EHR måste matchas med ett konsekvent person-ID i CJA-anslutningen för att skapa en sammanhängande systemövergripande resevy utan att behöva duplicera enskilda personer.
- För analys av vårdgap krävs uppslagsuppsättningar med kliniska riktlinjer som kodar definitioner - t.ex. rekommenderade screeningintervall efter ålder och tillstånd - så att CJA härledda fält kan flagga medlemmar som inte har slutfört rekommenderad vård i riktlinjefönstret.
- Schemaläggning av funnel-analys bör fånga både avslutade och övergivna schemaläggningssessioner, inklusive avslutspunkter i schemaläggningsflöden i flera steg, så att friktionspunkter visas på stegnivå i stället för som aggregerade bortfallsfrekvenser.


## Innehåll i patientportal Personalization

Anpassa den autentiserade patientportalupplevelsen genom att ta del av det mest relevanta hälsoinnehållet, verktygen och resurserna baserat på varje patients surfbeteende och engagemangshistorik. En portal som anpassar sig efter vad en patient aktivt undersöker - istället för att presentera samma statiska upplevelse för varje besökare - gör det enklare för patienterna att hitta det de behöver och uppmuntrar till djupare engagemang med tillgängliga hälsoresurser.

### Affärspåverkan

Personalisering av patientportalupplevelsen baserat på engagemangsbeteenden ger förbättrad innehållsidentifiering och snabbare självbetjäning, vilket gör att patienterna kan navigera mer tillförlitligt utan att vårdteamet behöver göra något.

### Implementera

Använd mönstret [Beteenderekommendation](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Beteendesignaler under sessioner från den autentiserade portalen - inklusive visningar av innehållssidor, användning av hälsoverktyg, engagemang i vanliga frågor och schemaläggning av möten - utbilda en rekommendationsmodell som hämtar de mest relevanta resurserna för varje patient baserat på vad de aktivt utforskar, utan att det krävs kliniska data som indata. Detta är det rätta mönstret när personalisering styrs av implicita beteendesignaler i en autentiserad session och målet är relevansrankning av ett innehåll och en resurskatalog - i stället för ett styrt beslut om behörighet, vilket är lämpligare när kliniska kriterier måste styra vad en patient ser.

### Tekniska överväganden

- Begränsa beteendesignaler som används för rekommendationer för interaktionsdata på portalen - innehållsvyer, verktygsanvändning och navigeringsmönster - och implementera dataanvändningsetiketter som förhindrar att misstänkta hälsointressen flödar utanför den autentiserade portalsessionen eller in i marknadsföringskanaler.
- Implementera ett kliniskt granskat innehållsbibliotek som rekommendationspool så att modellen endast kan visa förgodkänt utbildningsmaterial för hälsovård, vilket säkerställer att alla rekommenderade resurser har validerats för precision före driftsättningen.
- Se till att rekommendationssystemet uppfyller HIPAA:s tekniska säkerhetskrav för den autentiserade portalmiljön, inklusive timeout-kontroller för sessioner och granskningsloggning av vilket innehåll som presenteras för varje patient och när.
- Förse patienterna med synliga kontroller för att rensa deras portalwebbhistorik och avanmäla sig från beteendeanpassning, behålla transparensen och förtroendet för hur deras interaktionsdata används i portalupplevelsen.

## Påminnelser om patientengagemang och avtalade tider

Skicka personliga påminnelser om möten, hälsotips och uppföljningsmeddelanden via kompatibla, medgivandemedvetna flerkanalsresor. Automatiserade, personaliserade påminnelser om möten minskar antalet visningar samtidigt som kommunikationen följer sekretesslagstiftningen inom hälso- och sjukvården och patientens önskemål om samtycke.

### Affärspåverkan

Sjukvårdsorganisationer med automatiserade påminnelseprogram för möten ser meningsfulla minskningar av antalet misslyckade besök och avbrutna möten, vilket förbättrar användningen av leverantörsschemat och patienternas hälsa genom bättre tillmötesgående.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) om du vill svara på schemaläggningshändelser för möten med anpassade påminnelser som hålls i tid med optimala intervall före mötesdatumet. Detta är det rätta mönstret när kommunikationen utlöses av en specifik interaktionshändelse och svaret är ett tidskänsligt, individanpassat budskap - snarare än en interaktiv interaktionssekvens på flera veckor eller ett komplext urval av erbjudanden.

### Tekniska överväganden

- All patientkommunikation måste följa tillämpliga regler för hälso- och sjukvårdssekretess; budgivningsinnehåll måste undvika att inkludera skyddad hälsoinformation utöver vad som är absolut nödvändigt för kommunikationen.
- Medgivandehantering måste ske på kanalnivå - patienter som inte har valt att använda SMS-påminnelser får inte ta emot texter, även när SMS skulle vara den mest effektiva påminnelsekanalen för sin demografi.
- Integreringen med schemaläggningssystemet måste leverera avtalade tider i nära realtid för att möjliggöra påminnelsetider som stämmer med det faktiska schemat för avtalad tid, inklusive scheman för ombokningar samma dag och annulleringar.
- Påminnelsesekvenser för flera kanaler måste innehålla en undertryckningslogik så att patienter som bekräftar att de avtalat tid inte får påminnelsemeddelanden för den avtalade tiden.
