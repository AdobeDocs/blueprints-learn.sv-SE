---
title: Användningsexempel inom media och underhållning
description: Upptäck hur medie- och underhållningsorganisationer använder Adobe Experience Platform för att personalisera innehållsidentifiering, minska antalet prenumeranter och öka publikens engagemang.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: cfcf689f-9579-447f-9ef9-72e0c80c1f27
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '3363'
ht-degree: 0%

---

# Användningsexempel inom media och underhållning

Medie- och underhållningsorganisationer använder Adobe Experience Platform för att sammanställa målgruppsdata från olika strömningsplattformar, innehållsbibliotek och prenumerantkonton i en enda vy av varje visningsprogram eller avlyssnare. Denna grund möjliggör personaliserad innehållsidentifiering, proaktiv lojalitet av prenumeranter och engagemangsstrategier som får åskådarna att komma tillbaka efter mer.

## Innehållsrekommendationsmotor

Tillhandahåll personaliserade rekommendationer för innehåll, inklusive filmer, TV-program, musik och artiklar, baserat på visnings- och avlyssningshistorik, preferenser och liknande användarbeteende. När målgrupperna ser innehåll som är anpassat efter deras intressen lägger de mer tid på att utforska katalogen och upptäcka titlar som de annars skulle ha missat.

### Affärspåverkan

Organisationer som använder personaliserade rekommendationsmotorer ser bättre innehållsengagemang och en meningsfull ökning av den totala bevaknings- eller avlyssningstiden per användare.

### Implementera

Använd mönstret [Beteenderekommendation](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Strategin använder AI-drivna rekommendationsmodeller som kontinuerligt lär sig av målgruppsinteraktioner för att visa det mest relevanta innehållet för varje individ. Det här är det rätta mönstret när objektuppsättningen är stor och ändras kontinuerligt (innehållskataloger) och markeringen styrs av beteendetillhörighet som lärt sig av visningshistoriken - i stället för av en avgränsad uppsättning erbjudanden som styrs av regler för behörighet.

### Tekniska överväganden

- Metadata för innehållskatalogen, inklusive genre, cast, director, stämningstaggar och innehållsklassificeringar, måste importeras och hållas aktuella för att rekommendationerna ska återspegla hela bredden av tillgängliga titlar.
- Signaler för att visa och lyssna måste flöda i nära realtid så att rekommendationerna uppdateras i en enda webbläsarsession när en användare tittar på eller hoppar över innehåll.
- Rekommendationsmodellerna kräver en strategi där man kan börja från början för nya prenumeranter som saknar visningshistorik, som vanligtvis återgår till trender, redaktionellt kuraterat eller regionalt populärt innehåll.
- Innehållslicensiering och tillgänglighetsfönster måste beaktas i rekommendationslogiken så att användare aldrig rekommenderas för titlar som inte är tillgängliga i respektive region eller som har tagits bort från katalogen.


## Förhindra prenumerationskanal

Identifiera abonnenter som riskerar att avbryta och engagera dem med personaliserade innehållsrekommendationer, erbjudanden och kundlojalitetskampanjer. Att behålla befintliga prenumeranter är mycket mer kostnadseffektivt än att skaffa nya, och proaktiv utåtriktad marknadsföring i rätt ögonblick kan förhindra en betydande andel uppsägningar.

### Affärspåverkan

Effektiva program för att förebygga förändringar ger meningsfulla minskningar av antalet abonnenter, skyddar återkommande intäkter och förbättrar det långsiktiga värdet för målgruppens livslängd.

### Implementera

Använd mönstret [Flerkanalsresa med beslut](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). Detta tillvägagångssätt kombinerar resesamordning med realtidsbeslut för att välja det bästa erbjudandet om kvarhållning eller innehållsrekommendation för varje riskabonnent i alla kanaler. Det här är det rätta mönstret när resan måste koordinera leveransen över flera kanaler för att förhindra dubbletterbjudanden för kvarhållande och när valet av erbjudanden kräver regler för kvalificering baserat på prenumerantens värde och risknivå - flerstegssamordning ger inte ensam det beslutsskikt i realtid som behövs.

### Tekniska överväganden

- Kravriskbedömningen måste innehålla engagemangssignaler, t.ex. minskande bevakningstid, minskad inloggningsfrekvens och fall där innehållet fylls i för att identifiera riskabonnenter innan de kommer till annulleringssidan.
- Kvarhållningserbjudandena bör differentieras baserat på prenumerantens värde och risknivå, från personaliserade innehållsmarkeringar till rabatterade plantillägg, för att balansera intäktsskyddet mot marginalpåverkan.
- Resan måste förhindra meddelanden om kvarhållande för prenumeranter som redan har förnyat eller uppgraderat, vilket kräver realtidsintegrering med prenumerationsfaktureringssystemet.
- Beslutsreglerna för [!DNL Journey Optimizer] bör ta hänsyn till prenumerantens plantyp, varaktighet och tidigare erbjudandeinlösenhistorik för att undvika att presentera erbjudanden som känns generiska eller repetitiva.


## Meddelanden om nya innehållsreleaser

Meddela prenumeranterna om nya innehållsreleaser som matchar deras preferenser och visningshistorik. Snabba meddelanden om aktuellt innehåll skapar ett omedelbart engagemang och påminner prenumeranterna om det fortlöpande värdet av deras prenumeration.

### Affärspåverkan

Personaliserade versionsmeddelanden skapar bättre engagemang för nytt innehåll inom den första veckan efter releasen, vilket snabbar upp tittandet och ökar innehållets prestandamått.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Den här metoden är ett svar på innehållsreleaseversionshändelser och matchar nya titlar mot prenumerantprofiler för att leverera aktuella och relevanta meddelanden. Det här är det rätta mönstret när utlösaren är en systemhändelse (innehållsrelease) i stället för ett kundbeteende, och den kommunikation som krävs är omedelbar och reaktiv i stället för en kontinuerlig vårdsekvens.

### Tekniska överväganden

- Kalendrar för innehållsreleaser måste integreras så att meddelanden kan schemaläggas eller utlösas när nya titlar blir tillgängliga, så att du slipper för tidiga aviseringar om innehåll som ännu inte är tillgängligt.
- Prenumerantens preferenser bör ta hänsyn till flera dimensioner, inklusive genre affinitet, favoritskådespelare eller regissörer, tidigare bevakade serier och franchise-intressen, för att säkerställa att meddelandena känns personliga relevanta.
- Anmälningsvolymen måste hanteras noggrant med hjälp av frekvensbegränsning för att förhindra att abonnenterna känner sig överväldigade under perioder med stora mängder innehåll.
- Data för tidszon och visningsvanor bör informera leveranstider så att meddelanden kommer fram när varje prenumerant är mest benägen att engagera sig, i stället för vid en enda global sändningstid.


## Personaliserad upplevelse på hemsidan

Anpassa sidor för hemsida och innehållsidentifiering dynamiskt för att visa det mest relevanta innehållet först baserat på varje användares profil och beteende. När tittarna ser innehåll som är anpassat till sina smak direkt när appen öppnas, interagerar de snabbare och bläddrar längre.

### Affärspåverkan

Personaliserade hemsidesupplevelser ökar engagemanget på hemsidan och förbättrar innehållsidentifieringen avsevärt, särskilt för plattformar med stora och växande innehållsbibliotek.

### Implementera

Använd mönstret [Beteenderekommendation](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Den här metoden använder urvalsstrategier och rangordningsmodeller för att ändra ordning på innehållsrader och beskrivna titlar på hemsidan baserat på varje besökares profil och beteende i realtid. Det här är det rätta mönstret när objektuppsättningen är stor och ändras kontinuerligt och markeringen styrs av beteendetillhörighet för att rangordna innehållsrader dynamiskt, i stället för en statisk kuraterad uppsättning eller enkel attributbaserad personalisering.

### Tekniska överväganden

- Hemsidans personalisering måste utföras tillräckligt snabbt för att undvika upplevda lastförseningar. Kantbaserade beslut eller serversidesrendering krävs ofta för att uppfylla förväntningarna på kortare svarstid.
- Anpassningslogiken ska kombinera individuella preferenser med redaktionella och kampanjrelaterade prioriteringar, vilket säkerställer att interpoleringsreleaser, säsongsinnehåll och titlar som marknadsförs av partners fortfarande får lämplig synlighet.
- Strategier för innehållsrader, som&quot;Fortsätt bevaka&quot;,&quot;Eftersom du bevakar&quot; och&quot;Trending Now&quot;, kräver alla distinkta datainmatningar och rangordningslogik som måste struktureras till en sammanhängande sidlayout.
- [!DNL Experience Platform] Webbimplementeringen av SDK måste fånga upp hemsidesinteraktioner, inklusive radrullningar, panelklickningar och hovringsbeteenden, för att kontinuerligt förfina rangordningsmodellerna.


## Påminnelser om bevakningslistor och favoriter

Skicka påminnelser till användare om innehåll i deras bevakningslista som de inte har tittat på än, tillsammans med personaliserade rekommendationer för liknande titlar. Bevakningslistor representerar starka avsiktssignaler och enkla påminnelser kan konvertera den metoden till faktisk visning.

### Affärspåverkan

Påminnelseprogram för bevakningslistor ökar hastigheten för slutförande av bevakningslistor, omvandlar sparad avsikt till aktivt engagemang och ökar den totala plattformsanvändningen.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Den här metoden utlöser påminnelser baserat på aktivitetssignaler för bevakning och inaktivitetssignaler, och skickar tidskrävande meddelanden när innehållet har sparats men ännu inte startats. Detta är det rätta mönstret när en diskret beteendesignal (inaktivitet i bevakningslistan) är utlösaren och det svar som krävs är ett enda tidskänsligt meddelande - i stället för en sekvens i flera steg eller en kontinuerlig rekommendationsström.

### Tekniska överväganden

- Tidsplaneringen för påminnelser bör kalibreras baserat på hur länge innehållet har funnits på bevakningslistan och om användaren nyligen har varit aktiv på plattformen, så att man slipper påminnelser under tidsperioder då de inte behövs.
- Bevakningslistedata måste synkroniseras mellan olika enheter i realtid så att en titel som läggs till på mobilen omedelbart återspeglas i påminnelseberäkningen och inte dupliceras över olika plattformar.
- Påminnelser bör framhäva kontextuella detaljer som t.ex. utgångsdatum för tillgänglighetsfönster eller nya säsonger med sparade serier för att skapa en naturlig trängsel utan att känna sig ryckig.
- Innehåll som har tagits bort från katalogen eller inte längre är tillgängligt i prenumerantens region måste automatiskt uteslutas från påminnelsemeddelanden och ersättas med alternativa rekommendationer.


## Kostnadsfria testkonverteringskampanjer

Engagera användare av kostnadsfria testversioner med personliga rekommendationer och erbjudanden för att uppmuntra till konvertering av prenumerationer innan testperioden är slut. Testperioden är ett viktigt tillfälle att visa tillräckligt mycket för att användarna är villiga att betala, och en strukturerad konverteringsresa som avsevärt överträffar en påminnelse om att testperioden är slut.

### Affärspåverkan

Väldesignade konverteringskampanjer för testversioner ger meningsfulla förbättringar av konverteringsgraden mellan testversioner och betalningar, vilket direkt ökar prenumerationernas effektivitet och minskar kostnaden per förvärv.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. Den här resan för multitouch-näring guidar testanvändare genom en sekvens av innehållsidentifiering, värdedemonstration och konverteringsmeddelanden, som anpassar sig efter deras engagemang under hela testperioden. Det här är det rätta mönstret när användningsfallet kräver ett sekvensflöde med flera meddelanden på flera dagar med villkorlig förgrening baserat på interaktionshändelser och återstående testtid - ett enda utlöst meddelande kan inte hantera beroendelogiken mellan steg eller behovet av stängningsjusteringar.

### Tekniska överväganden

- Under resan måste du spåra teststart- och slutdatum exakt, med förgreningslogik som justerar meddelandeavsluten baserat på återstående testdagar och observerade engagemangsnivåer.
- Innehållsrekommendationer under resan bör prioritera plattformens mest engagerande och exklusiva titlar för att maximera det upplevda värdet av en betald prenumeration under den begränsade testperioden.
- Användare som konverterar innan testperioden är slut bör automatiskt flyttas från konverteringsresan till ett nytt välkomstflöde för prenumeranter, vilket förhindrar fortsatt testfokuserad meddelandehantering.
- [!DNL Journey Optimizer] resevillkor ska omfatta testplanstyp, hänvisningskälla och enhetsanvändning för att skräddarsy konverteringsmetoden för olika målgruppssegment.


## Visa påminnelser för live-event

Informera användarna om kommande live-event, sportevenemang eller premiärer som matchar deras intressen och tittarhistorik. Live-innehåll driver besöksvisningar som stärker abonnenternas vanor och gör att målgrupperna inte missar händelser de bryr sig om.

### Affärspåverkan

Personaliserade påminnelser för live-event förbättrar tittandet live och maximerar målgruppen för högklassig realtidsprogrammering.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Den här metoden utlöser meddelanden baserat på data för händelseplanering, matchning av kommande händelser mot prenumerantens intresseprofiler för att leverera påminnelser i rätt tid. Det här är det rätta mönstret när utlösaren är en systemhändelse (ett händelseschema) i stället för kundbeteende, och den kommunikation som krävs är omedelbar och tidsbunden i stället för en kontinuerlig vårdsekvens.

### Tekniska överväganden

- Data om scheman för evenemang, inklusive starttider, deltagande team eller talanger samt sändningsinformation, måste hämtas från programmeringssystem och hållas aktuella för att hantera ändringar i sista minuten-schemat eller annulleringar.
- Tidpunkten för påminnelseleverans ska ta hänsyn till tidszoner och vanliga ledtider före händelse. En påminnelse som skickas för tidigt ignoreras, medan en som skickas för sent missar starten.
- Intressematchningen bör omfatta både explicita preferenser, som favoritteam eller -genrer, och implicita signaler som tidigare visningsmönster för live-event för att identifiera relevanta händelser för varje prenumerant.
- Samordning av meddelanden på flera enheter är viktigt så att en prenumerant inte får redundanta påminnelser på sin telefon, surfplatta och smarta TV samtidigt.


## Personlig generering av spellistor

Generera och uppdatera automatiskt personaliserade spellistor baserat på varje användares lyssningshistorik, preferenser och humörindikatorer. Kuraterade spellistor minskar arbetet med att välja innehåll och håller avlyssnarna engagerade under längre sessioner.

### Affärspåverkan

Personlig generering av spellistor ökar engagemanget i spellistan och förlänger den genomsnittliga avlyssningstiden på ett meningsfullt sätt, vilket stärker de dagliga användningsvanorna för plattformen.

### Implementera

Använd mönstret [Beteenderekommendation](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Den här metoden använder AI-drivna modeller som analyserar avlyssningsmönster, hoppbeteende och sammanhangsberoende signaler för att generera och uppdatera spellistor som är anpassade för varje användare. Det här är det rätta mönstret när objektuppsättningen är stor och förändras kontinuerligt och markeringen styrs av beteendetillhörighet från avlyssningshistorik och humörsignaler - i stället för av en avgränsad uppsättning spellistor som styrs av redigeringsregler.

### Tekniska överväganden

- Metadata för musikkatalog, inklusive tempo, genre, stämningstaggar, artistförhållanden och ljudfunktioner, måste vara taggade för att det ska gå att skapa en ny kuration i spellistan som går bortom enkel genmatchning.
- Uppdateringsfrekvensen för spellistor bör balansera nyhet och kännedomen; avlyssnare förväntar sig nya upptäckter men vill också besöka favoriter igen, så modellerna måste kombinera utforskandet med komfort.
- Sammanhangsberoende signaler som tid på dygnet, veckodag och avlyssningsenhet kan ge stämning och energinivå i spellistan och skapa spellistor som känns lämpliga för tillfället.
- [!DNL Experience Platform] beteendedata måste fånga detaljerade lyssningshändelser, inklusive hopp, repeteringar, sparningar och sessionslängd, för att kontinuerligt förfina rekommendationsmodellerna.


## Synkronisering av plattformsövergripande innehåll

Skapa en smidig innehållsupplevelse på olika enheter genom att synkronisera bevakningshistorik, inställningar och rekommendationer i realtid. Tittarna förväntar sig att pausa på en enhet och fortsätta på en annan utan att tappa sin plats, och en enhetlig upplevelse på olika plattformar förstärker de dagliga användningsvanorna.

### Affärspåverkan

Synkronisering av innehåll på olika plattformar ökar engagemanget på olika enheter och minskar på ett meningsfullt sätt friktionen som kan leda till att sessionerna avbryts när användare växlar mellan olika enheter.

### Implementera

Använd mönstret [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md). Detta tillvägagångssätt personaliserar upplevelsen för identifierade användare på olika webb- och appplattformar och säkerställer ett konsekvent innehållsläge och rekommendationer oavsett enhet. Det här är det rätta mönstret när personalisering styrs av profilattribut (enhetsidentitet, bevakning av förloppstillstånd) och segmentmedlemskap i stället för en beteendetillhörighetsmodell eller en färgreformationssekvens.

### Tekniska överväganden

- Enhetsidentitetsupplösningen måste på ett tillförlitligt sätt länka användarsessioner mellan smarta tv-apparater, mobilappar, surfplattor och webbläsare för att upprätthålla en enda enhetlig profil för varje prenumerant.
- Titta på förloppsdata, inklusive exakt uppspelningsposition, status för slutförda avsnitt samt inställningar för undertexter och ljudspår, måste synkroniseras med minimal fördröjning för att ge en verkligt smidig CV-upplevelse.
- Rekommendationsmodeller bör ta hänsyn till enhetskontext, eftersom innehållsinställningarna kan skilja sig mellan en mobil pendationssession och en kvällssession på en stor skärm.
- Profilsammanfogningsprinciper för [!DNL Real-Time Customer Data Platform] måste konfigureras för att hantera samtidiga sessioner på flera enheter utan att skapa tillståndsuppdateringar i konflikt.


## Delning via sociala medier - Personalization

Anpassa uppmaningar och rekommendationer för social delning baserat på varje användares sociala anslutning och innehållsinställningar. Gör det enkelt och tilltalande för tittarna att dela med sig av vad de älskar att förvandla nöjda prenumeranter till organiska förespråkare som driver medvetenhet och värvning.

### Affärspåverkan

Personaliserade möjligheter till social delning uppnår förbättrade delningsnivåer i sociala medier, vilket ökar den ekologiska räckvidden och minskar de betalda anskaffningskostnaderna.

### Implementera

Använd mönstret [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md). Det här sättet personaliserar upplevelser i appdelning för identifierade användare, och visar sammanhangsberoende relevanta delningsfrågor baserat på användarens önskemål och engagemangsmönster. Det här är det rätta mönstret när personalisering drivs av profilattribut och kända engagemangskontext snarare än en beteendeaffinitetsmodell, och målet är att förbättra upplevelsen i ögonblicket utan att skapa en sekvens för kundresan.

### Tekniska överväganden

- Delningsuppmaningar bör utlösas vid naturliga ögonblick av glädje, som att fylla i en serie som är värd att skapa och upptäcka en ny favoritartist, i stället för vid godtyckliga intervall som känns påträngande.
- Förhandsifyllda delningsmeddelanden och -bilder måste genereras dynamiskt baserat på det specifika innehåll som delas, inklusive lämpliga miniatyrbilder, beskrivningar och djupa länkar som får mottagarna tillbaka till plattformen.
- Sekretesskontrollerna måste säkerställa att tittandet endast delas när användaren uttryckligen startar delning. Passiv eller automatisk delning av bevakningshistorik utan samtycke kan skada förtroendet.
- Integreringen med sociala plattformar måste följa respektive nätverks delningsprinciper och hantera autentisering, hastighetsbegränsningar och krav på innehållsformat för plattformar som Instagram, TikTok och X.


## Premium Feature Upsell

Identifiera användare som skulle kunna dra nytta av premiumfunktioner och presentera personaliserade merförsäljningserbjudanden baserat på deras användningsmönster. Riktat merförsäljningsbudskap till användare som redan visar beteenden som är anpassade efter premiumvärdet är mycket effektivare än allmänna uppgraderingskampanjer.

### Affärspåverkan

Personaliserade premiumbaserade merförsäljningskampanjer ger förbättrad användning av premiumfunktioner, ökade genomsnittliga intäkter per användare samtidigt som de levererar funktioner som verkligen matchar prenumerantens behov.

### Implementera

Använd mönstret [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). Strategin använder centraliserad beslutslogik för att utvärdera varje abonnents användningsmönster och välja det mest relevanta premieerbjudandet vid rätt tidpunkt. Det här är det rätta mönstret när valet av erbjudanden måste ta hänsyn till begränsningar för användningsmönster och regler för behörighet på premienivå - begränsningar som kräver styrd beslutslogik i stället för enbart rangordning av beteendetillhörighet.

### Tekniska överväganden

- Analys av användningsmönster måste identifiera specifika beteenden som indikerar premiumberedskap, t.ex. frekvent användning av funktioner som är tillgängliga i begränsad form i grundplanen, användning av flera enheter eller hög innehållskonsumtionsvolym.
- I erbjudandepresentationen bör de specifika premiumfördelar som är mest relevanta för varje användares beteende framhävas i stället för att alla premiumfunktioner i allmänhet anges. En användare som ofta hämtar innehåll bör se offlinevisning framhävd.
- Tidpunkten för merförsäljning bör undvika stunder av frustration, till exempel direkt efter ett betalväggsblock, och i stället utnyttja positiva engagemangstunder när abonnenten är mest mottaglig.
- Beslutsreglerna för [!DNL Journey Optimizer] måste koordinera merförsäljningserbjudanden för meddelanden i appen, e-post och push-meddelanden för att presentera ett konsekvent erbjudande utan att överbelasta prenumeranten över flera kanaler.


## Kampanjer för innehållsslutförande

Påminn användarna om att slutföra tittandet på eller lyssna på innehåll de startat men inte slutfört, tillsammans med personaliserade rekommendationer för vad de ska ta del av härnäst. Ofullständigt innehåll representerar orealiserat engagemang och en enkel knuff konverterar ofta en övergiven session till en slutförd upplevelse.

### Affärspåverkan

Kampanjer för slutförande av innehåll ökar hastigheten för slutförande av innehåll, ökar den totala engagemangstiden och förstärker abonnentens uppfattning om plattformens värde.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Den här metoden utlöser påminnelser baserat på händelser för innehållsutelämnande, och skickar meddelanden i rätt tid när en användare har pausat en del av en titel och inte har returnerat inom ett definierat fönster. Det här är det rätta mönstret när en diskret beteendesignal (innehållsbortfall) är utlösaren och det svar som krävs är ett enda tidskänsligt budskap i rätt sammanhang - snarare än en flerstegsresa eller dynamiskt urval av erbjudanden.

### Tekniska överväganden

- Överlämningströskelvärden ska kalibreras efter innehållstyp. En film som pausas vid 80 %-märket är en stark slutförandekandidat, medan en poddsändning som stoppas efter två minuter kan tyda på ointresse i stället för avbruten avlyssning.
- Påminnelsemeddelanden ska innehålla den specifika innehållstiteln, en visuell miniatyrbild och en direkt djup länk som återupptar uppspelningen exakt där användaren slutade.
- Frekvensbegränsning måste förhindra alltför stora påminnelser för användare som rutinmässigt tar prov på innehåll utan att först ta slut; upprepade knuffar för innehåll som användaren har valt att ge upp kan kännas påträngande.
- Innehållstillgängligheten måste verifieras vid sändning eftersom titlar kan lämna plattformen eller ändra tillgänglighetsområdena mellan övergivningshändelsen och påminnelseleveransen.


## Analys av drivrutin och engagemang för innehåll för prenumerant

Identifiera vilka innehållskonsumtionsmönster, förändringar av engagemangsfrekvensen och kataloginteraktionsbeteenden som föregår abonnentannullering och mät hur innehållets affinitet varierar mellan abonnentsegment och förvärvsmetoder. Strömma och publicera företag som inte kan koppla samman innehållsbeteenden för att ändra resultatet fattar innehållsinvesteringsbeslut baserat på mängdantal snarare än lojalitetseffekt.

### Affärspåverkan

Att korrelera innehållsengagemangsmönster med prenumerantens lojalitetsresultat ger produkt-, innehållsstrategi- och marknadsföringsteam en faktisk grund för att prioritera kataloginvesteringar och utforma återengagemangskampanjer kring de beteenden som faktiskt stöder prenumerationer.

### Implementera

Använd mönstret [Kundanalys och insiktsgenerering](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md). Detta tillvägagångssätt kopplar data från direktuppspelningshändelser, metadata för innehåll, prenumerationslivscykelposter och kampanjinteraktionshistorik till Customer Journey Analytics, där kohortanalyser för kvarhållningsanalys mäter hur innehållstillhörigheten korrelerar med prenumerantens varaktighet och falloutanalys identifierar de släppningsmönster för engagemang som föregår annulleringen. Det här är det rätta mönstret när målet är att förstå beteendedrivkrafter för förändring och innehållsprestanda, i stället för att utlösa ett återvinningsmeddelande eller aktivera en riskfylld målgrupp för undertryckande.

### Tekniska överväganden

- Innehållsförbrukningshändelser måste innehålla både innehållsidentifierare och metadata på sessionsnivå - start-, paus-, slutförings- och hopphändelser - så att engagemangsdjupet kan mätas utöver antalet råformat i CJA.
- Prenumerationens livscykelhändelser, inklusive teststart, konvertering, betalningsfel, nedgradering och annullering, måste infogas som diskreta händelser med exakta tidsstämplar så att beteendefönster för förannullering kan definieras exakt i CJA-filter.
- Attribut för innehållskataloger som genre, format, seriesammanslutning och releaseferens måste vara tillgängliga som en uppslagsdatauppsättning i CJA-anslutningen så att innehållsengagemangsanalysen kan delas upp efter katalogdimension i stället för att behöva analyseras på den enskilda titelnivån.
- Kohortanalyser där man jämför kvarhållningskurvor per inköps- och originalinnehåll som visas kräver att både inköps- och det första visade innehållet hämtas som profil- eller första-händelsedimensioner, som är tillgängliga för kohortdefinition i CJA.
