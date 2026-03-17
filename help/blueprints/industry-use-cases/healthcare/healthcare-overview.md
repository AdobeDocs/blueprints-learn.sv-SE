---
title: Handlingar
description: Upptäck hur sjukvårdsorganisationer använder Adobe Experience Platform för att förbättra patienternas engagemang, effektivisera samordningen av vården och få bättre hälsoresultat.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '2356'
ht-degree: 1%

---


# Handlingar

Sjukvårdsorganisationer använder Adobe Experience Platform för att skapa enhetliga patientprofiler och leverera personaliserad kommunikation i rätt tid över alla kontaktytor. Genom att knyta samman kliniska data, beteendedata och preferensdata på ett och samma ställe kan vårdpersonal engagera patienter mer effektivt samtidigt som högsta standard för sekretess och efterlevnad upprätthålls.

## Påminnelseautomatisering för avtalad tid

Skicka personliga påminnelser om möten via e-post, sms och push-meddelanden baserat på varje patients kommunikationsinställningar och typ av avtalad tid. Automatiska påminnelser minskar antalet missade avtalade tider och håller tidsplanerna smidigt och frigör personal för att fokusera på patientvården.

### Affärspåverkan

Organisationer som implementerar påminnelser om automatiska möten ser vanligtvis en 30-40-procentig förbättring av antalet besökstillfällen och en betydande minskning av kostsamma antal ej uträknade möten.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Skapande och uppdatering av avtalade tider från schemaläggningssystemet fungerar som naturliga utlösare för relevanta påminnelsemeddelanden i rätt tid.

### Tekniska överväganden

- Se till att all kontaktinformation och information om avtalade tider överförs och lagras i enlighet med HIPAA-kraven och använd lämpliga etiketter för att begränsa obehörig åtkomst.
- Integrera med det elektroniska systemet för schemaläggning av hälsoposter för att i realtid samla in händelser för att skapa, avbryta och schemalägga om möten.
- Använd regler för samtyckeshantering så att påminnelser endast skickas via kanaler som patienten uttryckligen har valt.
- Konfigurera undertryckningsregler för att förhindra dubbletter eller överdrivet många påminnelser när avtalade tider schemaläggs om i snabb följd.


## Kampanjer för läkemedelsefterlevnad

Skicka personliga påminnelser och utbildningsmaterial för att hjälpa patienterna att hålla sig à jour med sina medicineringsscheman och behandlingsplaner. Skräddarsytt budskap baserat på medietyp, doseringsschema och patienthistorik ger bättre följsamhet och förbättrade hälsoresultat.

### Affärspåverkan

Personaliserade uppföljningskampanjer inom medicin leder normalt till en 20 till 30-procentig förbättring av följsamhetsgraden, vilket leder till mätbart bättre hälsoresultat och färre återbesök på sjukhus.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. För att upprätthålla medicineringen krävs en kontinuerlig, flerberöringsstrategi med eskalerande påminnelser, kontaktpunkter för utbildning och uppföljningskontroller under en behandlingsplan.

### Tekniska överväganden

- Tillämpa strikta etiketter för dataanvändning på all skyddad hälsoinformation som rör läkemedel och diagnos för att förhindra otillåten aktivering längre fram i kedjan.
- Integrera med apotek och elektroniska patientjournalsystem för att ta emot data som fyller i och fyller i receptet och som triggar kundresan.
- Genomför kraftfull hantering av samtycke för att säkerställa att patienterna har gått med på att få läkemedelsrelaterad kommunikation och kan när som helst dra tillbaka sitt samtycke.
- Designa logik för kundresan för att upptäcka icke-engagemangsmönster och eskalera till vårdteamets meddelanden när en patient kan riskera att inte följa reglerna.


## Påminnelser om förebyggande vård

Påminn proaktivt patienter om rekommenderad förebyggande vård såsom vaccination, screening och årliga kontroller baserade på ålder, anamnes och riskfaktorer. Påminnelser om förebyggande vård i rätt tid bidrar till att täppa till luckor i vården och förbättra den allmänna folkhälsan.

### Affärspåverkan

Förebyggande förebyggande vård leder normalt till en ökning på 25 till 35 procent av andelen patienter som färdigställer förebyggande vård, vilket bidrar till förbättrad folkhälsa och minskade kostnader för långtidsbehandling.

### Implementera

Använd mönstret [Aktivera utgående batchmeddelande](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md). Påminnelser om förebyggande vård ges bäst genom schemalagda batchkampanjer som utvärderar patienternas rätt till behandling i förhållande till kliniska riktlinjer med regelbunden uppföljning.

### Tekniska överväganden

- Bygg målgruppssegment med hjälp av kliniska riktlinjer (ålder, kön, familjehistoria, tidigare screeningdatum) och lägg in dataanvändningsetiketter i all skyddad hälsoinformation som används vid segmentering.
- Samordna med kliniska team för att säkerställa att påminnelseinnehållet överensstämmer med befintliga evidensbaserade riktlinjer för förebyggande vård och organisationsprotokoll.
- Implementera frekvensbegränsning för att undvika överväldigande patienter som samtidigt är kvalificerade för flera förebyggande behandlingsrekommendationer.
- Upprätthåll en verifieringskedja över all information om förebyggande vård som skickas för regelmässig rapportering och dokumentation av kvalitetsmått.


## Uppföljningskampanjer efter besök

Skicka automatiskt enkäter, omvårdnadsinstruktioner och påminnelser efter besök baserat på typ av besök och varje patientes specifika behov. En snabb uppföljning ger nöjdare patienter och säkerställer kontinuitet i vården efter varje besök.

### Affärspåverkan

Automatiserade uppföljningskampanjer efter besök ger normalt en 40 till 50 procents förbättring av svarsfrekvensen för undersökningar och mätbart högre poängtal för patientnöjdhet.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Besök slutförandehändelser från det elektroniska patientjournalsystemet som ger en naturlig och snabb utlösare för uppföljningskommunikation som är skräddarsydd för påräkningstypen.

### Tekniska överväganden

- Integrera med det elektroniska patientjournalsystemet för att få besök vid avslutningshändelser som omfattar besökstyp, leverantör och relevanta vårdinstruktioner utan att visa fullständiga kliniska anteckningar.
- Lägg in dataetiketter i all vårdinformation för att säkerställa att den skyddade hälsoinformationen endast delas via säkra, patientgodkända kanaler.
- Konfigurera timingregler som tar hänsyn till besökstyp - t.ex. kan uppföljning efter operation kräva annan timing än rutinundersökningar.
- Inkludera säkra länkar till patientportalen för slutförande av undersökningar och schemaläggning av möten i stället för att samla in hälsoinformation via osäkra kanaler.


## Program för hantering av kroniska sjukdomar

Personalisera kommunikation om hantering av kroniska sjukdomar, utbildningsmaterial och övervaka påminnelser baserat på varje patientes specifika tillstånd och behandlingsplan. Bibehållet, relevant engagemang hjälper patienterna att ta en aktiv roll när det gäller att hantera sin hälsa över tid.

### Affärspåverkan

I personaliserade program för hantering av kroniska sjukdomar ökar programengagemanget med 30 till 40 procent, vilket leder till bättre sjukdomshanteringsresultat och minskat utnyttjande av akutvård.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. Hantering av kronisk sjukdom är i sig en långvarig, flerpunktsupplevelse som kräver adaptiva meddelanden baserat på patientengagemang och milstolpar inom hälsoområdet.

### Tekniska överväganden

- Designa förgreningslogik som anpassar sig efter villkorsspecifika mätvärden (t.ex. blodglukostrender för diabeteshantering eller blodtrycksläsningar för hypertensionsprogram).
- Implementera strikt datastyrning med [!DNL Adobe Experience Platform]-etiketter för dataanvändning för att klassificera och skydda villkorsspecifika hälsodata under hela resan.
- Integrera med fjärranslutna patientövervakningsenheter och patientrapporterade resultatsystem för att mata in hälsodata i realtid till beslutsunderlag för resan.
- Bygg upp eskaleringsvägar för vårdteam under resan så att bristande engagemang eller gällande hälsotrender utlöser larm för lämplig klinisk personal.


## Ny introduktionsresa för patienter

Automatisera en introduktionsresa i flera steg för nya patienter som innehåller välkomstinformation, instruktioner för åtkomst till patientportalen och vägledning om schemaläggning av möten. En smidig introduktionsupplevelse sätter tonen för en engagerad och långsiktig patientrelation.

### Affärspåverkan

Automatiserade nya patientintroduktionsresor ger normalt en 50 till 60-procentig förbättring av portalaktiveringshastigheten och betydligt högre tidig patientinteraktion.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. Patientintroduktion är en naturligt sekventiell flerstegsprocess där varje kommunikation bygger på det tidigare och anpassas beroende på om patienten har slutfört de viktigaste åtgärderna.

### Tekniska överväganden

- Integrera med patientregistreringssystemet för att utlösa introduktionsresan direkt när nya patientjournaler skapas, vilket ger ett snabbt första intryck.
- Använd identitetsupplösning för att sammanfoga befintliga poster (t.ex. från en webbplatsbesök eller en förfrågan om avtalad tid) med den nya patientprofilen för att undvika dubbla kommunikationer.
- Se till att portalaktiveringslänkar och autentiseringsuppgifter levereras via säkra, HIPAA-kompatibla kanaler och förfaller efter en angiven period.
- Designa resan för att upptäcka portalaktivering och händelser i samband med ifyllande av formulär så att efterföljande steg anpassas i stället för att upprepa information som patienten redan har agerat på.


## Personaliserat hälsoinnehållsleverans

Leverera personaliserat innehåll, hälsotips och resurser för hälsoutbildning som är skräddarsydda efter varje patientes villkor, intressen och hälsomål. Relevant innehåll bygger upp förtroende, förbättrar hälsoförståelse och ger patienter möjlighet att fatta välgrundade beslut om sin vård.

### Affärspåverkan

Personaliserat innehåll på hälsoområdet når normalt en 35-45-procentig ökning av engagemanget, vilket leder till avsevärt förbättrad patientutbildning och hälsoförståelse.

### Implementera

Använd mönstret [Flerkanalsresa med beslut](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). Leverans av hälsoinnehåll drar nytta av realtidsbeslut som väljer det mest relevanta innehållet för varje patient baserat på deras villkor, önskemål och tidigare engagemang, som levereras via den kanal de föredrar.

### Tekniska överväganden

- Använd etiketter för innehållsklassificering och dataanvändning på allt hälsoutbildningsmaterial för att säkerställa att villkorsspecifikt innehåll endast levereras till patienter som har samtyckt till att få hälsoinformation om det ämnet.
- Integrera beslutsmotorn med ett innehållsarkiv som regelbundet granskas och godkänns av kliniska team för att säkerställa medicinsk precision.
- Implementera regler för innehållströtthet för att undvika att innehåll på ett och samma tema skickas för mycket och för att balansera utbildningsmaterial över en patients olika hälsobehov.
- Spåra signaler om innehållsengagemang (öppningar, klick, tidsåtgång) för att kontinuerligt förfina innehållets relevans utan att samla in eller lagra ytterligare skyddad hälsoinformation.


## Meddelande om Lab-resultat

Meddela patienterna när labbresultaten är tillgängliga via den kommunikationskanal de föredrar med personaliserade, säkra meddelanden. Snabbmeddelanden uppmuntrar patienterna att granska resultaten snabbt och följa upp med vårdteamet när det behövs.

### Affärspåverkan

Automatiserade labbresultatmeddelanden ger normalt en 60 till 70-procentig ökning av antalet visade resultat, vilket förbättrar patientkommunikationen och möjliggör snabbare klinisk uppföljning när resultaten kräver åtgärder.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Tillgänglighet för Lab-resultat är en diskret händelse som kräver ett omedelbart, enda meddelande via den kanal patienten föredrar.

### Tekniska överväganden

- Inkludera aldrig faktiska labbresultatvärden i meddelandena - meddela bara patienten att resultaten är tillgängliga och dirigera dem till den säkra patientportalen för mer information.
- Integrera med laboratorieinformationssystemet för att ta emot resultatklara händelser samtidigt som strikta dataanvändningsetiketter används för att förhindra att kliniska data flödar in i marknadsföringskanalerna.
- Implementera leverantörsspärrlogik så att aviseringar skickas först efter att den behandlande läkaren har granskat och släppt resultaten för att kunna se dem.
- Kontrollera att alla meddelandelänkar pekar på autentiserade, krypterade patientportalsessioner som uppfyller HIPAA:s säkerhetskrav.


## Verifiering av försäkringsskydd

Kontrollera och förmedla information om försäkringsskydd till patienterna innan de utses för att minska faktureringsöverraskningarna och förbättra den övergripande patientupplevelsen. Tydlig kommunikation med direkt täckning skapar förtroende och minskar antalet faktureringstvister efter besök.

### Affärspåverkan

Proaktiv kontroll av försäkringsskydd resulterar normalt i en 25 till 35-procentig förbättring av bekräftelsefrekvensen före besök och en meningsfull minskning av faktureringstvister och patientklagomål.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Tidsplaneringshändelser för möten fungerar som en utlösare för att påbörja disponeringsverifiering och informera patienten om resultaten före besöket.

### Tekniska överväganden

- Integrera med system för verifiering av försäkringsberättigande för att få täckning i realtid utan att lagra fullständiga data om försäkringsanspråk på kunddataplattformen.
- Använd dataetiketter på all ekonomisk information och försäkringsinformation för att begränsa användningen till faktureringsrelaterad kommunikation.
- Konfigurera meddelandetimingen så att det finns tillräckligt med ledtider innan patienterna kan utses för att lösa eventuella täckningsproblem eller kontakta sin försäkringsleverantör.
- Inkludera tydliga instruktioner och kontaktinformation för faktureringsavdelningen så att patienterna kan ställa frågor eller tillhandahålla uppdaterade försäkringsdetaljer innan besöket.


## Påminnelser om avtalade tider för telehälsa

Skicka personliga påminnelser för telefonmöten med anslutningsanvisningar, tips och teknisk supportinformation. Effektiva påminnelser i telekombranschen minskar antalet missade virtuella besök och hjälper patienterna att känna sig säkra med hjälp av verktygen för digital vård.

### Affärspåverkan

Påminnelser om personliga möten i telekommunikationer leder vanligtvis till en förbättring på 40 till 50 procent av antalet virtuella besök och ökar den totala användningen av telesäkrar i hela patientpopulationen.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Tidsplaneringshändelser för möten inom telehälsa är en naturlig utlösare för påminnelser i rätt tid som innehåller anslutningsinformation och vägledning om förberedelser.

### Tekniska överväganden

- Inkludera plattformsspecifika anslutningsinstruktioner (dator eller mobil) baserat på patientens kända enhetsinställningar eller tidigare telefonhälsosessionsdata.
- Se till att alla länkar och sessionsidentifierare för telehälsoanslutning levereras via krypterade, HIPAA-kompatibla kanaler och förfaller efter det schemalagda fönstret för avtalad tid.
- Integrera med telekomplattformen för att identifiera när en patient har anslutit sig så att sekundära påminnelser kan undertryckas.
- Ange en reservsökväg till kontaktinformation för teknisk support för patienter som inte har anslutit inom ett definierat fönster innan besökets starttid.


## Välfärdsprogramsengagemang

Anpassa kommunikationen, utmaningarna och belöningen för välkända program utifrån varje patientes hälsomål, aktivitetsnivå och önskemål. Engagerande hälsoprogram motiverar patienterna att ta till sig mer hälsosamma vanor och upprätthålla ett långsiktigt välbefinnande.

### Affärspåverkan

Personaliserade kampanjer för hälsoprogram bidrar vanligtvis till att öka deltagandet i programmen med 30 till 40 procent, vilket bidrar till förbättrade hälsoresultat och ökad lojalitet hos patienten.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. Välfärdsprogram är varaktiga engagemangsupplevelser med flera milstolpar, utmaningar och belöningar som kräver adaptiv samordning baserat på patientens deltagande och framsteg.

### Tekniska överväganden

- Integrera med dataflöden för kroppsburna och friskvårdsapplikationer och använd tydliga etiketter för dataanvändning för att skilja mellan hälsodata och data om klinisk hälsa som omfattas av strängare lagstadgade krav.
- Implementera samtyckeshantering som gör det möjligt för patienter att bevilja och återkalla tillstånd för insamling av hälsovårdsuppgifter oberoende av deras kliniska kommunikationsinställningar.
- Designa en logik som anpassar svårighetsgrad och kommunikationsfrekvens baserat på varje patients engagemangsmönster för att undvika obehag eller trötthet.
- Se till att belönings- och stimulansspårning följer gällande regler för hälso- och sjukvård kring patientinduktioner och krav på återförsäkring.


## Samordning mellan olika avdelningar

Möjliggör anpassad kommunikation och samordning mellan patienter och deras vårdpersonal baserat på vårdplanen och individuella önskemål. Bättre samordning leder till mer sömlösa behandlingsövergångar och förbättrade resultat för patienter med komplexa behandlingsbehov.

### Affärspåverkan

Effektiv kommunikation i form av samordning mellan vårdteam resulterar vanligtvis i en 35-45-procentig förbättring av vårdteamets engagemang och mätbart bättre resultat av samordningen mellan vårdplaner för flera vårdgivare.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. Samordning i vårdteam innefattar flera intressenter och kontinuerliga kommunikationsflöden som måste anpassas baserat på milstolpar i vårdplanen, förändringar av patientstatus och leverantörsåtgärder.

### Tekniska överväganden

- Implementera rollbaserade åtkomstkontroller och etiketter för dataanvändning för att säkerställa att varje vårdteammedlem endast får patientinformation som är relevant för deras roll i vårdplanen.
- Integrera med system för hantering av vård och elektroniska patientjournaler för att få uppdateringar av vårdplanen, slutförda hänvisningar och övergångshändelser som utlöser samordningsmeddelanden.
- Designa olika kommunikationsvägar för patienttillvända och leverantörstillvända meddelanden och se till att klinisk terminologi används på rätt sätt för leverantörer medan patientmeddelandena förblir tydliga och tillgängliga.
- Upprätthåll en fullständig verifieringskedja över all kommunikation för samordning av vården för att uppfylla reglerna för kontinuitet och ackrediteringskrav.
