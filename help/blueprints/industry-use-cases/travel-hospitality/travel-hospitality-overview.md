---
title: Travel & Hospitality Use Cases
description: Discover how travel and hospitality organizations use Adobe Experience Platform to personalize booking experiences, recover abandoned reservations, and build guest loyalty.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: fbdcc015-96a4-4015-93e2-3fc7db375c13
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '3648'
ht-degree: 0%

---

# Travel &amp; Hospitality Use Cases

Travel and hospitality organizations use Adobe Experience Platform to bring together guest data from booking engines, loyalty programs, property management systems, and digital touchpoints into a single view of each traveler. This unified foundation powers personalized experiences that inspire bookings, recover abandoned reservations, and build the kind of guest loyalty that drives repeat visits.

## Personalized Homepage for New Visitors

Show personalized cruise, hotel, and destination recommendations on the homepage based on the visitor&#39;s geographic location and browsing behavior. First-time visitors who see relevant travel options immediately are far more likely to explore further and begin the booking process.

### Affärspåverkan

Personalizing the homepage for new visitors drives improved conversion rates by presenting travel options that match the visitor&#39;s location and interests rather than generic content.

### Implementera

Use the [Anonymous Visitor Web Personalization](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md) pattern. This approach delivers tailored content to visitors who have not yet identified themselves, using available signals such as geolocation, device type, and referral source to personalize the experience from the very first page. This is the right pattern when the visitor has not yet identified themselves and personalization must rely on available signals such as geolocation, device type, and referral source — known-visitor personalization requires an authenticated profile that does not yet exist.

### Tekniska överväganden

- Geolocation data must be resolved accurately at the edge to serve region-appropriate destinations, currencies, and departure ports without adding latency to the homepage load.
- Personalization rules should account for seasonal travel trends by region, surfacing warm-weather destinations to visitors in cold climates during winter months, for example.
- Fallback content strategies are essential for visitors whose location cannot be determined or who arrive through anonymizing services.
- Integration with the reservation system&#39;s availability feed ensures that featured properties and itineraries are actually bookable, preventing frustration from promoting sold-out options.


## Cart Abandonment Recovery Journey

Automatically detect when a customer abandons their booking cart and trigger a multi-step email journey with personalized offers to encourage completion. Abandoned reservations represent one of the largest revenue leaks in travel and hospitality, and timely follow-up while the travel intent is still fresh recovers a meaningful share of those bookings.

### Affärspåverkan

Effective booking recovery programs achieve meaningful cart recovery rates and can generate significant incremental revenue depending on booking volume and average trip value.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). This approach responds to a real-time cart abandon event, sending a timely reminder while the customer&#39;s travel intent is still high. Det här är det rätta mönstret när utlösaren är en kundbeteendehändelse i realtid och det svar som krävs är ett enda tidskänsligt meddelande - snarare än en interaktiv sekvens i flera steg eller ett dynamiskt urval som ändras baserat på kundrespons.

### Tekniska överväganden

- Tröskelvärden för att upptäcka när en kund lämnar en vagn bör omfatta längre kurser som är typiska vid reseinköp. En 2-4 timmars fördröjning före den första påminnelsen är ofta lämpligare än de 30-60 minuter som används i detaljhandeln.
- E-postinnehållet måste dynamiskt höja den aktuella prissättningen, rum- eller kabintillgängligheten och bilder från bokningssystemet vid sändning eftersom reseinventeringen och taxan ändras ofta.
- Personaliserade incitament, som kostnadsfria uppgraderingar eller resortkrediter, bör hanteras genom affärsregler som tar hänsyn till marginal, säsongsbundenhet och kundens lojalitetsnivå.
- Undertryckningslogiken måste utesluta kunder som slutfört sin bokning via en annan kanal, som ett callcenter eller en resebyrå, för att undvika irrelevanta uppföljningsmeddelanden.


## Avancerad målgruppsanpassning för besökare

Identifiera besökare med hög inköpsmetod med hjälp av AI-driven benägenhetsbedömning och rikta dem mot personaliserade erbjudanden och innehåll. Genom att känna igen vilka besökare som är mest benägna att boka kan organisationen fokusera sina mest övertygande erbjudanden och utåtriktad försäljning på de resenärer som är närmast att fatta ett beslut.

### Affärspåverkan

Att rikta in sig på besökare med hög återgivning med personaliserade erbjudanden ger förbättrad konvertering för dessa segment och koncentrerar marknadsföringsinvesteringarna där de ger störst avkastning.

### Implementera

Använd mönstret [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md). Den här metoden använder profildata och beteendesignaler i realtid för att personalisera webbupplevelsen för identifierade besökare och leverera skräddarsytt innehåll och erbjudanden som matchar deras nivå av inköpsberedskap. Det här är det rätta mönstret när personalisering styrs av profilattribut och benägenhetspoäng för identifierade kunder snarare än en beteendetillhörighetsmodell - och när kunden redan har autentiserats, gör deras segmentmedlemskap och avsiktssignaler tillgängliga.

### Tekniska överväganden

- Propensitetsmodeller måste utbildas i resespecifika intentalsignaler som datumsökningar, prissättningssidvisningar, rumsjämförelser och återkommande besök på samma plats inom ett kort fönster.
- Insatser med hög återgivning, t.ex. live-chattmeddelanden eller tidsbegränsade erbjudanden, bör visas vid naturliga beslutstillfällen i bokningsflödet i stället för att störa surfupplevelsen.
- Poängmodellen bör skilja mellan forskningsavsikt och bokningsmetod, eftersom resenärer ofta undersöker månader innan de är redo att köpa.
- [!DNL Real-Time Customer Data Platform] beräknade attribut kan samla in beteendesignaler mellan sessioner för att behålla en aktuell intent-poäng för varje besökare.


## Bokför merförsäljningskampanjer

När kunden har avslutat en bokning startar automatiskt merförsäljningskampanjer för kabinuppgraderingar, utflykter i land, matpaket och andra tillhöriga. Perioden mellan bokning och resor är när gästerna är mest intresserade av sin kommande resa och mest mottagliga för att förbättra sin upplevelse.

### Affärspåverkan

Kampanjer för merförsäljning efter bokning ökar det genomsnittliga ordervärdet och ökar därmed intäkterna, vilket gör en enda bokning till en betydligt mer värdefull transaktion.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. Den här flerstegsresan vägleder kunderna genom en tidsbestämd sekvens av merförsäljningsmöjligheter och anpassar erbjudandena baserat på vad gästen redan har köpt och deras engagemang med tidigare meddelanden. Det här är det rätta mönstret när användningsfallet kräver ett sekvensflöde med flera meddelanden på flera dagar med villkorlig förgrening baserat på engagemangshändelser och lagertillgänglighet - ett enda utlöst meddelande kan inte hantera beroendelogiken mellan merförsäljningsstunder eller timingjusteringar baserat på resedatum.

### Tekniska överväganden

- Resan måste integreras med bokningssystemet för att veta exakt vad gästen har bokat, vilka uppgraderingar som finns tillgängliga för respektive resväg och aktuella priser för varje ytterligare alternativ.
- Tidpunkten för merförsäljning bör staggasfalteras strategiskt. Kabinuppgraderingar kan erbjudas kort efter bokningen, medan utflykter och matsalar fungerar bättre när resedatum närmar sig.
- Tillgång till lager och tillgänglighet för hjälpprodukter måste kontrolleras när erbjudandet presenteras, eftersom utstrålningskapaciteten och uppgraderingstillgängligheten ändras kontinuerligt.
- [!DNL Journey Optimizer]-personalisering bör ta hänsyn till antalet resenärer i bokningen och rekommendera familjeanpassade utslag för familjebokningar och parorienterade upplevelser för tvåpersonsbokningar.


## Win-Back Campaigns for Lapsed Customers

Identifiera kunder som inte har bokat på tolv eller fler månader och engagera dem med personaliserade erbjudanden och innehåll baserat på deras tidigare reseönskemål. Det är betydligt mer kostnadseffektivt att engagera återkommande gäster än att skaffa helt nya kunder, och tidigare resenärer har redan en varumärkeskänsla som sänker hindren för att boka om.

### Affärspåverkan

Välinriktade återvinnande kampanjer ger meningsfulla återaktiveringsfrekvenser bland bortgångna kunder och återhämtar intäkter från gäster som annars aldrig skulle kunna återvända.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. Den här flerstegsresan engagerade kunderna på nytt med en progressiv serie meddelanden som utvecklas från inspiration till incitament baserat på kundens respons. Det här är det rätta mönstret när det inte finns någon diskret utlösande händelse och tidsinställning måste beräknas utifrån kundens livscyklmodeller och säsongsbokningsmönster - händelserelaterade meddelanden kan inte hantera den progressiva eskaleringslogiken eller behovet av att hålla erbjudanden runt normala reseplaneringsfönster.

### Tekniska överväganden

- Förlorad kundsegmentering ska ta hänsyn till typisk bokningsfrekvens i resekategorin. En kund som bokar årligen ska inte flaggas som annullerad efter endast sex månaders inaktivitet.
- Återvinningsinnehåll bör hänvisa till kundens tidigare resepreferenser, t.ex. prioriterade destinationer, kabintyper eller resesäsonger, för att visa att varumärket kommer ihåg och värdesätter dem.
- Erbjudandena bör eskalera under hela kundresan, med början med inspirerande innehåll och framsteg till monetära incitament endast om tidigare meddelanden inte genererar engagemang.
- Kundregister måste kontrolleras mot bokningssystemet för bokningar som görs via offlinekanaler som resebyråer eller callcenters för att undvika att skicka återvinnande meddelanden till kunder som faktiskt är aktiva.


## Dynamiska rekommendationer

Visa personaliserade kryssningsrutnät och destinationer baserat på kundens tidigare bokningar, webbhistorik och angivna önskemål. När resenärer ser resvägar som är skräddarsydda efter deras intressen och resestil engagerar de sig djupare i planeringen och går snabbare mot att boka.

### Affärspåverkan

Personaliserade rekommendationer för flygvägar ger ett bättre engagemang med resplan-sidor, vilket hjälper kunderna att hitta rätt resa snabbare och minskar den avgång som inträffar när resenärerna känner sig överväldigade av för många alternativ.

### Implementera

Använd mönstret [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md). Detta tillvägagångssätt personaliserar webbplatsinnehållet för identifierade besökare genom att använda deras profildata och beteendehistorik för att identifiera de mest relevanta resvägarna och destinationerna. Detta är det rätta mönstret när personalisering styrs av profilattribut och bokningshistorik snarare än en beteendetillhörighetsmodell - vilket gör att regelbaserad logik kan ta hänsyn till reselogistik som avreseportar och datum vid sidan av kundens önskemål.

### Tekniska överväganden

- Logiken i reserekommendationer måste inkludera segling- eller vistelsedatum, avgångsportar och varaktighetsinställningar tillsammans med destinationsintresse för att kunna presentera alternativ som både är tilltalande och praktiska för kunden.
- Integreringen med det centrala bokningssystemet säkerställer att rekommenderade tidsplaner har tillgängligt lager och återspeglar aktuella priser, vilket förhindrar frustration att marknadsföra utsålda varor eller fullt bokade egendomar.
- Säsongsrelaterade faktorer bör ha stor inverkan på rekommendationerna. Kunder som tidigare bokade kryssningar i Medelhavet under sommarmånaderna bör se liknande säsongsalternativ istället för alternativ under lågsäsong.
- Profilsammanfogningsprinciper för [!DNL Experience Platform] måste göra webbläsarbeteendet från flera enheter korrekt enhetligt så att forskning som utförs på mobiler återspeglas i skrivbordsrekommendationerna.


## Nyligen lästa produkter på hemsidan

Visa nyligen visade kryssningar, hotell eller destinationer på hemsidan för att påminna besökarna om deras intresse och uppmuntra besökare att återvända. Resenärer undersöker ofta olika sessioner innan de bokar, och om de tar hänsyn till sina tidigare intressen slipper de besväret att börja söka varje gång de återvänder.

### Affärspåverkan

Genom att visa nyligen använda reseprodukter på hemsidan ökar besöksupplevelsen, vilket hjälper kunderna att fortsätta där de slutade och korta vägen till bokningen.

### Implementera

Använd mönstret [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md). Den här metoden använder besökarens lagrade profildata för att återge tidigare visade objekt på hemsidan, vilket skapar kontinuitet mellan olika webbläsarsessioner. Det här är det rätta mönstret när personalisering bygger på beständiga profildata för olika sessioner och enheter i stället för beteendeaffinitet i realtid - och när reglerna för relevans är tidsbaserade (nyligen använda) i stället för algoritmisk rankning.

### Tekniska överväganden

- Data som har visats nyligen måste finnas kvar på olika enheter och sessioner med hjälp av identitetsupplösning, så att en kund som surfar på sin telefon ser samma objekt när de kommer tillbaka på en dator.
- Visade objekt ska visa aktuella priser och tillgänglighetsstatus, med tydliga indikatorer om ett tidigare visat alternativ inte längre är tillgängligt eller om priset har ändrats sedan det senaste besöket.
- Det nya fönstret för visade artiklar bör justeras till bokningscykler för resor. En kryssning som visades för tre månader sedan kan fortfarande vara relevant, till skillnad från en detaljhandelsprodukt som visades för så länge sedan.
- Sekretessöverväganden kräver att nyligen visat innehåll är knutet till kundens medgivandestatus, och ett alternativ för att rensa webbläsarhistoriken bör vara enkelt tillgängligt.


## Avsluta återgivningsmodulen med riktade erbjudanden

När en besökare visar sin avslutningsmetod, ska han/hon visa ett personaliserat modalt erbjudande med relevanta erbjudanden baserat på deras webbläsarbeteende under sessionen. Att fånga en avgående besökare med ett övertygande, sammanhangsberoende erbjudande ger en sista möjlighet att konvertera intresset till en bokning innan de går.

### Affärspåverkan

Modaler för att avsluta med personaliserade reseerbjudanden återskapar meningsfulla konverteringar bland besökare som annars skulle lämna programmet utan att bokföra, vilket fångar upp intäkter som helt skulle gå förlorade.

### Implementera

Använd mönstret [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). Strategin använder centraliserad beslutslogik för att utvärdera alla tillgängliga erbjudanden och välja det som är mest relevant för den avgående besökaren baserat på deras sessionsbeteende och profildata. Det här är det rätta mönstret när valet av erbjudanden måste ta hänsyn till rätt till lojalitetsnivå och affärsbegränsningar runt frekvensbegränsning - begränsningar som kräver styrd beslutslogik i stället för en enkel beteenderekommendation eller ett enda utlöst meddelande.

### Tekniska överväganden

- Avsluta avsiktsidentifiering på resebokningswebbplatser måste ta hänsyn till webbläsarbeteende på flera flikar, eftersom resenärer ofta öppnar flera resvägar eller egenskaper på olika flikar utan att egentligen ha för avsikt att lämna dem.
- Erbjudandevalet bör återspegla vad besökaren bläddrat efter under sessionen, vilket ger en rabatt på den specifika destinationen eller egendomen som de utforskat i stället för en allmän kampanj.
- Modal frekvens bör vara strikt begränsad för att hindra besökarna från att se samma erbjudande på varje besök, vilket urholkar det brådskande och uppfattade exklusiviteten i erbjudandet.
- [!DNL Journey Optimizer]-regler för erbjudande bör beakta besökarens lojalitetsnivå och bokningshistorik för att presentera relevanta förmåner, vilket ger premiumgäster meningsfulla fördelar i stället för små rabatter.


## Lojalitetsprogram Personalization

Anpassa webbplatsupplevelsen, erbjudandena och kommunikationen baserat på kundens lojalitetsnivå, poängbalans och engagemangshistorik. Lojalitetsmedlemmar som ser sin status återspeglas i alla kontaktytor och känns erkända och värderade, vilket stärker deras engagemang i varumärket och uppmuntrar till vidareutveckling av skiktet.

### Affärspåverkan

Nivåbaserad personalisering driver på lojalitetsmedlemmarnas engagemang, fördjupar relationen och snabbar upp intäktsbeteendena och inlösen som ger långsiktiga intäkter.

### Implementera

Använd mönstret [Flerkanalsresa med beslut](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). Strategin kombinerar resesamordning med realtidsbeslut för att leverera rätt erbjudande via rätt kanal för varje lojalitetsmedlem, som anpassas till deras nivå, preferenser och senaste aktivitet. Det här är det rätta mönstret när resan måste koordinera leveransen över flera kanaler för att förhindra dubblerade erbjudanden och när valet av erbjudanden kräver nivåbaserade regler för behörighet och inlösenbegränsningar - endast resesamordning ger inte det flerkanalsbeslutslager som behövs.

### Tekniska överväganden

- Data om lojalitetsprogram, inklusive skiktstatus, poängsaldon och intäktshistorik, måste hämtas in och hållas aktuella för att webbplatspersonaliseringen och erbjudandena ska återspegla kundens faktiska anseende.
- Nivåspecifika fördelar som tidig åtkomst till bokningar, kostnadsfria uppgraderingar och exklusiv prissättning måste tillämpas vid tidpunkten för inlösen, vilket kräver nära integrering med boknings- och prissättningssystemen.
- Poängsaldoförändringar från bokningar, uppehåll och partnertransaktioner bör utlösa en omberäkning av personaliseringsreglerna i nära realtid, så att en kund som precis har tjänat tillräckligt många poäng för en belöning omedelbart ser det alternativet.
- [!DNL Real-Time Customer Data Platform] målgrupper ska struktureras runt lojalitetsnivåer och viktiga milstolpar för engagemang, som att närma sig nästa nivå eller riskera att nivån degraderas.


## Påminnelser om flerkanalsbokning

Skicka personliga bokningspåminnelser via e-post, SMS och push-meddelanden till kunder som har börjat men inte slutfört sina bokningar. Resenärerna börjar ofta bokningsprocessen och blir avbrutna, och når dem via de kanaler de föredrar med en påminnelse och deras sparade reseinformation för dem tillbaka för att slutföra bokningen.

### Affärspåverkan

Påminnelser om flerkanalsbokning förbättrar antalet slutförda bokningar, vilket ger betydande intäkter från kunder som hade för avsikt att boka men som spårades innan de slutfördes.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Den här metoden utlöser påminnelser automatiskt när en ofullständig bokningshändelse upptäcks, vilket ger aktuella meddelanden i de kanaler kunden föredrar. Det här är det rätta mönstret när utlösaren är en diskret kundåtgärd (att starta en bokning) och det svar som krävs är tidskänslig leverans i de kanaler som föredras - i stället för en sekvens i flera steg där varje meddelande är beroende av tidigare engagemang- eller tillgänglighetsändringar.

### Tekniska överväganden

- Logiken för val av kanaler ska respektera kundernas kommunikationsinställningar och optimera leveransen baserat på tidigare interaktionsmönster, och skicka push-meddelanden till kunder som svarar väl på mobiler och e-post till dem som föredrar det.
- Påminnelseinnehållet måste innehålla en djup länk som returnerar kunden direkt till den sparade bokningen med alla markeringar intakta, vilket eliminerar möjligheten att ange resedatum, rumsinställningar och gästinformation igen.
- Regler för timing och frekvens bör samordna alla kanaler för att undvika att överbelasta kunden. Ett e-postmeddelande och ett push-meddelande om samma bokning bör vara lämpligt placerade i stället för att skickas samtidigt.
- Integrationen med egenskapshanteringen eller det centrala reservationssystemet måste verifiera att den rumstyp, det värde och de datum som ursprungligen valts fortfarande är tillgängliga innan påminnelsen skickas och uppdatera meddelandet om tillgängligheten har ändrats.


## Säsongskampanj, Personalization

Anpassa kampanjer och erbjudanden baserat på säsongsinställningar, tidigare säsongsbokningar och aktuella säsongstrender. Resenärerna påverkas mycket av säsonger, och kampanjer som är anpassade till deras visade säsongsintressen och aktuella resetrender är mycket mer övertygande än generiska kampanjer.

### Affärspåverkan

Personaliserade kampanjer med säsongsbunden bokning ökar konverteringsgraden, vilket säkerställer att marknadsföringsinvesteringarna koncentreras till de destinationer och resprodukter som mest troligt får gensvar hos varje kund.

### Implementera

Använd mönstret [Aktivera utgående batchmeddelande](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md). Detta tillvägagångssätt levererar personaliserade säsongskampanjer till stora målgrupper på regelbunden basis och segmenterar kunderna efter deras säsongsrelaterade resemönster och önskemål. Det här är det rätta mönstret när målgruppen är stor och fördefinierad av säsongsbokningshistorik. Leveranstiderna är schemalagda baserat på säsongsrelaterade planeringsfönster snarare än händelsestyrda, och ingen förgrening eller beslut krävs i realtid.

### Tekniska överväganden

- Kundens säsongsinställningar bör bygga på historiska bokningsdata och identifiera mönster som enhetliga semestrar på sommarstrand eller vinterskidresor för att informera om kampanjinriktningen.
- Kampanjplaneringen måste ta hänsyn till ledtider för resebranschen. Sommarsemesterkampanjer bör lanseras i tidig vår när familjer planerar, inte i juni när de flesta bokningar redan görs.
- Priser och tillgänglighetsflöden för säsongsbunden inventering måste integreras så att kampanjerna återspeglar realtidsfrekvenser och den faktiska rums- eller kabintillgängligheten under de aktuella reseperioderna.
- [!DNL Experience Platform] målgrupper bör kombinera säsongsinställningsdata med nyligen använda indikatorer för att prioritera kunder som befinner sig i deras typiska planeringsfönster inför den kommande säsongen.


## Gruppbokningsrekommendationer

Identifiera kunder som ofta bokar gruppresor och proaktivt rekommenderar grupppaket, familjevänliga alternativ eller bokningar i flera rum. Gruppbokningar ger avsevärt högre intäkter per transaktion och kunder med ett påvisat mönster för gruppresor svarar på välstrukturerade alternativ som förenklar planeringsprocessen.

### Affärspåverkan

Förebyggande rekommendationer för gruppbokning ökar det genomsnittliga ordervärdet per bokning, vilket fångar upp hela värdet av gruppresetransaktioner som annars skulle kunna delas upp i flera enskilda reservationer.

### Implementera

Använd mönstret [Beteenderekommendation](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Den här metoden använder AI-drivna modeller som bygger på kundbokningsmönster och beteenden för att rekommendera de mest relevanta gruppresemöjligheterna för varje kund. Det här är det rätta mönstret när artikeluppsättningen är stor och ständigt förändras - grupppaketen utvecklas med prissättning och tillgänglighet - och urvalet drivs av beteendemönster i gruppbokningshistorik snarare än en avgränsad uppsättning erbjudanden som styrs av reglerna för behörighet.

### Tekniska överväganden

- Identifiering av gruppresor kräver analys av bokningshistorik för mönster som till exempel bokningar i flera rum, bokningar med flera passagerare och samordnade bokningar som gjorts i närhet för samma datum och destination.
- Grupppaketpriset måste dras dynamiskt från bokningssystemet eftersom grupppriserna ofta skiljer sig från enskilda priser och kan kräva miniminivåer eller förskottsbokningsfönster.
- Rekommendationsinnehållet ska ta upp grupporganisatörernas unika behov, inklusive information om gruppmatningsalternativ, mötesplatser, blockbokningsrabatter och tillgänglighet för gruppexponering.
- Profilberikning för [!DNL Real-Time Customer Data Platform] ska flagga kunder som gruppreseorganisatörer baserat på deras bokningsmönster, vilket möjliggör riktade kampanjer under högtider för gruppplanering som familjesäsong eller företagsfönster.


## AI Booking Concierge

Rese- och turismorganisationer erbjuder komplexa, värdefulla inköpsresor där gästerna måste navigera bland flyg, rum, rumskategorier, sidotjänster och lojalitetsförmåner innan de förbinder sig till en bokning. Statiska gränssnitt för bläddring och filtrering ger beslutsutmattning och ökar avhoppet. Ett AI-bokningskoncernen engagerar gästerna i en naturlig konversation för att förstå deras reseavsikter, partistorlek, preferenser och budget och vägleder dem sedan steg för steg genom reseplanering, bostadsval och tilläggsalternativ - samtidigt som man ser lojalitetsfördelar som är relevanta för gästens skikt.

### Affärspåverkan

Vägledning om konversationsbokning förbättrar antalet slutförda samtal och därmed sammanhängande bilagor, samtidigt som det minskar antalet besökare som annars skulle ringa för att förtydliga alternativen.

### Implementera

Använd mönstret [Brand Concierge Conversational Experience](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md). Med den här metoden används Product Advisor Agent mot egenskaps- och tidskatalogen, med hjälp av AEP Agent Orchestrator-data och kundprofildata i realtid för att identifiera personaliserade alternativ och lojalitetsrelevanta rekommendationer via guidad fleromvänd dialog. Detta är det rätta mönstret när målet är interaktiv konversationsidentifiering i flera omgångar som bygger på ett komplext bokningsbeslut - skilt från händelseutlösta meddelanden, som reagerar på diskreta resenäråtgärder med enkelriktad utåtriktad marknadsföring, och från personaliserade webbupplevelser, som tar upp rekommendationer passivt utan att engagera gästen i en dialog. Det kräver AEP Agent Orchestrator och varumärkesstyrningskonfiguration.

### Tekniska överväganden

- Tillgänglighets- och prissättningsdata måste hållas aktuella genom nära realtidsintegrering mellan bokningssystemet och Brand Concierge innehållslager, eftersom rekommendationer om otillgängliga rumstyper eller felaktiga priser i en konversation omedelbart undergräver förtroendet.
- Vid sökning efter kundprofiler i realtid måste kundens lojalitetsnivå, lagringshistorik och angivna inställningar visas, så att agenten proaktivt kan bekräfta gästens status och anpassa rekommendationer utan att gästen behöver förklara sina inställningar på nytt vid varje besök.
- Varumärkesstyrningen måste definiera hur agenten hanterar frågor om matchning av frekvens, konkurrentreferenser och situationer där gästens önskade datum eller rumstyp inte är tillgängliga, så att agenten kan reagera smidigt inom varumärkesuttrycket i stället för att presentera en odödlig ände.
- Konversationssignaler - inklusive destinationsintresse, resekomposition och närliggande preferenser som uttrycks under dialogen - måste flöda tillbaka till AEP som ExperienceEvent-data, vilket berikar gästprofilerna för att informera e-post, lojalitet och återengagemangskampanjer längre fram i kedjan.
