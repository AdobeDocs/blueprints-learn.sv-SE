---
title: Försäkringsanvändningsfall
description: Upptäck hur försäkringsorganisationer använder Adobe Experience Platform för att personalisera regelhanteringen, förbättra upplevelserna och få kunderna att stanna kvar.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '2494'
ht-degree: 0%

---


# Försäkringsanvändningsfall

Försäkringsorganisationer använder Adobe Experience Platform för att sammanställa uppgifter från försäkringstagarna i olika system för hantering, skadeanmälan och kundinteraktion för att leverera personaliserad kommunikation i alla skeden av kundrelationen. Genom att koppla beteendesignaler till policy- och anspråksinformation kan försäkringsbolagen aktivt engagera kunderna med relevanta erbjudanden, aktuella uppdateringar och meningsfull support som driver lojalitet och livstidsvärde.

## Förnyelsekampanjer för policyer

Skicka personliga påminnelser och erbjudanden om förnyelse av avtal baserat på varje kunds policyhistorik, kravregister och disponeringsinställningar. Relevant förlängning i rätt tid minskar andelen annullationer av försäkringsavtal och stärker långsiktiga kundrelationer genom att göra det enkelt för försäkringstagarna att förstå sina alternativ och vidta åtgärder.

### Affärspåverkan

Organisationer som implementerar personaliserade förnyelsekampanjer för policyer ser vanligtvis en 25-35-procentig förbättring av förnyelsefrekvensen, vilket direkt minskar kundbortfallet och skyddar återkommande premieintäkter.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Förnyelsedatum för försäkringsavtal är naturliga händelseutlösare som initierar en vältajmad, personaliserad strategi vid den tidpunkt då försäkringstagarna fattar sitt beslut om förnyelse.

### Tekniska överväganden

- Integrera med policyhanteringssystemet för att ta emot händelser för förnyelsedatum och aktuell policyinformation, för att säkerställa att meddelandena återspeglar korrekt täckning och premiuminformation.
- Använd datastyrningsetiketter på alla personligt identifierbara och finansiella policydata för att följa statliga försäkringsbestämmelser och integritetskrav.
- Konfigurera spärrregler för att förhindra att meddelanden om förnyelse skickas till försäkringstagare som redan har förnyat eller som har aktiva anspråk som kan påverka deras förnyelsevillkor.
- Koordinera timingen med agent- eller mäklaruppdrag så att direktmeddelanden till kunder som är anpassade till alla utdataområden som den tilldelade agenten också kan genomföra.


## Produktrekommendationer för korsförsäljning

Rekommendera ytterligare försäkringsprodukter som livförsäkring, hemförsäkring eller automatisk täckning baserat på varje kunds befintliga policyer, livsfas och riskprofil. Personaliserade produktrekommendationer hjälper försäkringstagarna att upptäcka luckor i försäkringsskyddet och skapa en mer komplett skyddsportfölj.

### Affärspåverkan

Personaliserade korsförsäljningsrekommendationer genererar vanligtvis en förbättring på 20 till 30 procent av konverteringsgraden för korsförsäljning, vilket ökar policyer per hushåll och det totala kundlivstidsvärdet.

### Implementera

Använd mönstret [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). Vid beslut i realtid utvärderas varje kunds befintliga täcknings-, Live-stage- och beteendesignaler för att välja den mest relevanta produktrekommendationen från den tillgängliga katalogen.

### Tekniska överväganden

- Integrera policydata från alla produktrader i en enhetlig kundprofil så att beslutsmotorn får en fullständig bild av den befintliga täckningen när rekommendationer väljs.
- Konfigurera berättiganderegler i beslutsmodellen för att utesluta produkter som en kund redan har eller som står i konflikt med garantiriktlinjerna för deras riskprofil.
- Tillämpa regler för regelefterlevnad för att säkerställa att produktrekommendationerna uppfyller de statsspecifika kraven på marknadsföring och lämplighet för försäkringar.
- Koordinera beslutsutdata med agentportalen så att rekommenderade produkter visas för tilldelade agenter som kan ha direktkonversationer med kunden.


## Anspråksprocess för Personalization

Anpassa kundprocesskommunikation, statusuppdateringar och supportresurser baserat på typ av anspråk, kundpreferenser och anspråkshistorik. En transparent, välkommunicerad upplevelse av skadeståndsanspråk minskar oron under stressiga stunder och skapar bestående förtroende hos försäkringstagarna.

### Affärspåverkan

Personaliserade kundförfrågningar får normalt en 40-50-procentig förbättring av poängen för kundnöjdhet, vilket minskar antalet klagomål och ökar sannolikheten för förnyad policy efter ett anspråk.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. Anspråksprocessen är en flerstegsupplevelse med distinkta faser - registrering, utredning, justering och avveckling - som alla kräver skräddarsydd kommunikation och anpassningsbar timing.

### Tekniska överväganden

- Integrera med anspråkshanteringssystemet för att få statusändringshändelser i realtid som hjälper kunden genom rätt kundresa.
- Designa logik för förgreningslogik som anpassar ton och innehåll för meddelanden baserat på anspråkstyp, som automatisk kollision jämfört med skadeståndsanspråk.
- Implementera undertryckningsregler vid aktiva förfrågningar för att förhindra att marknadsförings- eller korsförsäljningsmeddelanden når kunder vid känsliga tillfällen.
- Se till att alla anspråksrelaterade data som flödar in i kundprofilen är märkta med lämpliga begränsningar för datastyrning för att förhindra att de används utanför tjänstekommunikationen.


## Riskbedömning och förebyggande

Tillhandahåll personaliserad riskbedömningsinformation och tips för förebyggande åtgärder baserat på varje kunds policytyp, geografiska placering och specifika riskfaktorer. Proaktiv riskutbildning hjälper försäkringstagarna att minska sin exponering för förlust, vilket gynnar både kunden och försäkringsgivaren.

### Affärspåverkan

Personaliserat riskförebyggande arbete ger vanligtvis en 30-40-procentig förbättring av det förebyggande arbetet, vilket bidrar till minskad kundfrekvens och förbättrad kundnöjdhet.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. Riskförebyggande utbildning är mest effektiv som en kontinuerlig multipekresa som levererar relevant vägledning över tid och som anpassas baserat på kundengagemang och säsongsrelaterade riskfaktorer.

### Tekniska överväganden

- Integrera med riskdataoperatörer från tredje part för information om väder, geografiska risker och egendomsrisker som berikar kundprofiler med platsspecifika riskpoäng.
- Utforma logik för säsongsresan som levererar relevant förebyggande innehåll före högriskperioder, t.ex. förberedelser inför orkansäsongen för kustförsäkringstagare eller vädertips för kallt klimat.
- Använd datastyrningsetiketter för att skilja riskbedömningsdata som används för kundutbildning från data som används i försäkringsbeslut.
- samordna riskförebyggande innehåll med försäkringstagarens specifika täckning så att rekommendationer är relevanta för de risker som deras policy faktiskt omfattar.


## Meddelanden om principändringar

Skicka personaliserade meddelanden om policyändringar, disponeringsuppdateringar och nya alternativ baserat på varje kunds specifika policy och kommunikationsinställningar. Tydliga meddelanden håller försäkringstagarna informerade och minskar förvirringen om deras täckningsstatus.

### Affärspåverkan

Anmälningar om personaliserade policyändringar ger vanligtvis en 50-60-procentig förbättring av antalet meddelanden om att kundservice har bekräftats, vilket minskar antalet kundförfrågningar och förbättrar den övergripande förståelsen för försäkringstagarna.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Principändringshändelser från administrationssystemet fungerar som naturliga utlösare för omedelbara, relevanta meddelanden via varje kunds önskade kanal.

### Tekniska överväganden

- Integrera med policyadministrationssystemet för att fånga upp händelser om godkännande, ändring och förnyelse i realtid, så att meddelandena speglar det senaste policytillståndet.
- Följ gällande regler för att säkerställa att meddelandena uppfyller de krav som ställs på kommunikation i samband med policyändringar, inklusive obligatoriska språk- och leveranstider.
- Konfigurera logik för kanalprioritet baserat på hur brådskande och typ av ändring är - t.ex. kan sänkta täckningar göra det möjligt att skapa mer omedelbara kanaler än informationsuppdateringar.
- Bibehåll en leveransverifieringskedja för alla meddelanden om policyändringar som stöd för regelefterlevnad och tvistlösning.


## Återvinning av offertbortfall

Engagera kunder som började men inte slutförde en försäkringsoffert med personaliserade uppföljningsmeddelanden och skräddarsydda erbjudanden igen. Med hjälp av ett system för snabb återställning kan potentiella kunder återgå till offertprocessen och ta itu med vanliga hinder för slutförande.

### Affärspåverkan

Kampanjer för att återhämta offerter leder normalt till en förbättring på 20 till 30 procent av antalet slutförda offerter, vilket konverterar fler potentiella kunder till försäkringstagarna och minskar kundvärvningskostnaderna.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Avbruten offert är en beteendehändelse som utlöser snabb uppföljning medan den potentiella kundens intresse och avsikter fortfarande är aktuella.

### Tekniska överväganden

- Integrera med offertplattformen online för att fånga upp övergivna händelser tillsammans med de offertdetaljer som kunden redan har angett, vilket möjliggör personaliserat återengagemang.
- Konfigurera timingregler som balanserar skyndsamhet med respekt - inledande uppföljning inom några timmar, med ett begränsat antal efterföljande påminnelser under de följande dagarna.
- Använd regler för samtycke och integritet för att säkerställa att uppföljning endast skickas till presumtiva som har valt att marknadsföra meddelanden, särskilt för kunder som ännu inte har etablerat ett politiskt förhållande.
- Inkludera djupa länkar som returnerar potentiella kunder direkt till deras sparade offert i stället för att kräva att de startar om processen från början.


## Produkterbjudanden baserade på livscykelstadium

Identifiera kunder som kommer in i nya livsstadier - som giftermål, hemköp, växande familj eller pension - och erbjud relevanta försäkringsprodukter som matchar deras föränderliga skyddsbehov. Med målgruppsanpassning för livsstadiet kan försäkringstagarna skapa rätt täckning vid rätt tidpunkt.

### Affärspåverkan

Produkter som är baserade på livscykelstadiet har normalt en 35 till 45-procentig förbättring av produktacceptansfrekvensen, vilket fördjupar kundrelationerna under viktiga beslutstillfällen.

### Implementera

Använd mönstret [Flerkanalsresa med beslut](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). Övergångar i livscykelstadiet drar nytta av flerkanalssamordning i kombination med realtidsbeslut för att välja den mest relevanta produkten och leverera den via den kanal kunden föredrar i det optimala ögonblicket.

### Tekniska överväganden

- Bygg modeller för upptäckt av livsstadier med hjälp av beteendesignaler som adressändringar, mottagaruppdateringar och onlineforskningsmönster, i kombination med förändrade politiska händelser.
- Konfigurera beslutsmotorn med regler för produktberättigande och lämplighet som matchar varje livscykelstadium till lämpliga täckningsrekommendationer.
- Samordna livserbjudanden med den tilldelade agenten eller mäklaren så att de är redo att ge kunden konsultation när erbjudandet levereras.
- Använd datastyrningsetiketter på alla datakällor från tredje part som används för att övervaka att dataintegritetsreglerna efterlevs och att marknadsföringsrutinerna är rättvisa.


## Rabatt och besparingar

Identifiera och förmedla anpassade rabattmöjligheter - som paketering, säkra drivrutiner, lojalitet och papperslösa faktureringsrabatter - baserat på varje kunds profil och beteende. Proaktiv information om besparingar visar på värde och stärker förhållandet mellan pris och värde.

### Affärspåverkan

Personaliserad information om rabatter och besparingar ger normalt en 25 till 35-procentig förbättring av rabattutnyttjandegraden, vilket ger nöjdare kunder och minskar prisstyrda inköp.

### Implementera

Använd mönstret [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). Vid beslut i realtid utvärderas varje kunds behörighet att få rabatt och den mest effektiva besparingsmöjligheten som presenteras vid rätt tillfälle väljs ut.

### Tekniska överväganden

- Integrera med betygs- och faktureringssystemen för att beräkna rätt rabattberättigande och möjliga besparingar för varje kund i realtid.
- Konfigurera beslutsregler som tar hänsyn till rabattbegränsningar och säkerställer att de sparbelopp som kommuniceras är faktiskt korrekta och godkända av pristeamet.
- Tillämpa statsspecifika regler för rabattmeddelanden, eftersom vissa delstater har begränsningar för hur försäkringsrabatter kan marknadsföras och tillämpas.
- Spåra rabattens användningsresultat för att kontinuerligt förfina beslutsmodellen och prioritera de sparmeddelanden som får flest poäng i olika kundsegment.


## Förebyggande av skadeståndsbedrägerier

Använd intelligent upptäckt av bedrägeri för att identifiera misstänkta anspråksmönster och personalisera kommunikationen med utredningar samtidigt som kundens förtroende upprätthålls. Effektiv förebyggande av bedrägeri skyddar ärliga försäkringstagare genom att hålla premierna rättvisa och se till att legitima fordringar behandlas snabbt.

### Affärspåverkan

Intelligenta program för förebyggande av skadeståndsanspråk ger i allmänhet 15 till 25 procent bättre upptäckt av bedrägerier, minskade bedrägliga utbetalningar och sänkte de totala skadekostnaderna.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Riskbedömningsincidenter för bedrägeri utlöser lämpliga granskningsmeddelanden och processjusteringar i realtid, vilket säkerställer att flaggade anspråk får omedelbar uppmärksamhet.

### Tekniska överväganden

- Integrera riskpoäng för bedrägeri från anspråksanalyssystemet i kundprofilen och använd strikta datastyrningsetiketter för att förhindra att data från bedrägeriutredningar visas i kundcentrerad kommunikation.
- Utforma kommunikationsvägar som bibehåller en professionell, respektfull ton för kunder vars påståenden håller på att granskas, och som bevarar relationen oavsett undersökningsresultat.
- Implementera rollbaserade åtkomstkontroller för att säkerställa att bedrägeriindikatorerna endast är synliga för behöriga utredningsgrupper och aldrig kommer att visas i standardagenternas eller kundtjänsternas vyer.
- Koordinera med identitetsupplösningstjänsten [!DNL Adobe Experience Platform] för att identifiera mönster i relaterade profiler, till exempel delade adresser eller telefonnummer som är länkade till flera misstänkta anspråk.


## Program för att förebygga och skydda hälsa

Anpassa kommunikationen om hälsoprogram, påminnelser om deltagande och belöningsmeddelanden för hälso- och livförsäkringskunder utifrån deras mål och engagemang. Aktiva program för hälsovård förbättrar utfallet för försäkringstagarnas hälsa och skapar en starkare och mer engagerad kundbas.

### Affärspåverkan

Kommunikation om program för personaliserat välbefinnande och förebyggande åtgärder leder normalt till en 30-40-procentig förbättring av deltagandegraden i programmet, vilket bidrar till bättre hälsoresultat och minskad frekvens för skadeanmälningar.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. Välfärdsprogram är varaktiga engagemangsupplevelser med milstolpar, utmaningar och belöningar som kräver adaptiv samordning baserat på varje deltagares aktivitet och framsteg.

### Tekniska överväganden

- Integrera med dataflöden från bärbara enheter och hälsoprogram med hjälp av [!DNL Adobe Experience Platform]-direktuppspelning, och använd tydliga etiketter för datastyrning för att skilja på friskhetsdata och anspråksdata.
- införa separata mekanismer för samtycke för insamling av hälsodata för att säkerställa att deltagarna förstår hur deras hälsoaktivitetsdata används och kan avanmäla sig utan att påverka deras policy.
- Designa logik som anpassar programintensiteten och kommunikationsfrekvensen baserat på varje deltagares engagemang för att förhindra trötthet och uppmuntra ett ihållande deltagande.
- Se till att löneförmåner och vinstbelöningsspårning följer gällande försäkringsbestämmelser om försäkringstagares incitament och premiumrabatter.


## Samordning mellan ombud och mäklare

Möjliggör anpassad kommunikation och samordning mellan kunder och deras tilldelade agenter eller mäklare baserat på policybehov, servicehistorik och önskemål. Bättre samordning skapar en smidig upplevelse där kunderna känner sig stödda av en kunnig rådgivare som förstår sitt fullständiga förhållande.

### Affärspåverkan

Effektiv kommunikation mellan agenter och mäklare ger vanligtvis en 35 till 45-procentig förbättring av agenternas engagemang, vilket leder till starkare kundrelationer och högre lojalitet tack vare tillförlitliga rådgivande interaktioner.

### Implementera

Använd mönstret [Aktivera utgående batchmeddelande](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md). Agentsamordning levereras bäst genom schemalagda gruppaktiveringar som ger agenter prioriterade kundutåtriktade listor, samtalspunkter och rekommenderade åtgärder på en regelbunden konferens.

### Tekniska överväganden

- Integrera med agenthanteringssystemet för att upprätthålla korrekta tilldelningar av agenter och kunder och säkerställa att kommunikationen speglar det korrekta förhållandet, särskilt under agentövergångar.
- Utforma dataaktivering på agentportalen så att agenterna får en samlad bild av kundinsikter, kommande förnyelser och rekommenderade åtgärder utan att exponera råbeteendedata.
- Använd etiketter för datastyrning för att begränsa vilka kunddataelement som delas med externa mäklare jämfört med interna medarbetare, med respekt för avtalsbaserade och lagstadgade gränser för datadelning.
- Implementera feedback-slingor från agentinteraktioner tillbaka till kundprofilen så att insikter från personliga samtal eller telefonsamtal berikar den enhetliga vyn och förbättrar den framtida personaliseringen.


## Katastrofisk händelsesvar

Proaktivt kommunicera med kunder i drabbade områden under naturkatastrofer eller andra katastrofer med hjälp av personaliserad supportinformation, riktlinjer för anspråksansökningar och nödresurser. Den snabba, empatiska utåtkomsten under en kris visar försäkringsgivarens engagemang för att vara där när kunderna behöver det som mest.

### Affärspåverkan

Proaktiv kommunikation med katastrofala händelser förbättrar normalt kundkommunikationen med 60 till 70 procent under händelser, vilket avsevärt snabbar upp ansökningsprocessen och stärker kundens långsiktiga förtroende och lojalitet.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Katastrofiska händelsedeklarationer fungerar som högprioriterade utlösare för omedelbar, personaliserad kontakt med alla försäkringstagare i det drabbade geografiska området.

### Tekniska överväganden

- Integrera med tjänster för övervakning av katastrofoffekter och deklarationer om katastrofer från myndigheter för att snabbt utlösa kommunikation när händelser deklareras för specifika geografiska områden.
- Bygg geografiska målgruppssegment med hjälp av data från försäkringstagarnas adresser och platsinformation för att exakt identifiera kunder i det drabbade området utan att överkommunicera med oberörda kunder.
- Konfigurera högprioriterad meddelanderoutning som åsidosätter standardregler för frekvensbegränsning och undertryckning för att säkerställa att viktig säkerhets- och anspråksinformation når kunderna omedelbart.
- Bygg meddelandemallar och färdiga kundresekonfigurationer för vanliga händelsetyper så att kommunikationen kan aktiveras inom några timmar efter en händelsedeklaration i stället för att innehåll måste skapas under krisen.
