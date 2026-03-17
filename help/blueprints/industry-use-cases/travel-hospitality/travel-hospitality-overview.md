---
title: Användningsexempel för resor och turism
description: Upptäck hur rese- och turismorganisationer använder Adobe Experience Platform för att personalisera bokningsupplevelser, återställa övergivna bokningar och bygga gästlojalitet.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '2835'
ht-degree: 0%

---


# Användningsexempel för resor och turism

Rese- och turismorganisationer använder Adobe Experience Platform för att samla gästdata från bokningsmotorer, lojalitetsprogram, egendomsstyrningssystem och digitala kontaktytor i en enda vy över varje resenär. Denna enhetliga grund driver personaliserade upplevelser som inspirerar bokningar, återställer övergivna reservationer och bygger upp den typ av gästlojalitet som driver återkommande besök.

## Personaliserad hemsida för nya besökare

Visa personliga kryssnings-, hotell- och destinationsrekommendationer på hemsidan baserat på besökarens geografiska plats och surfbeteende. Första gången besökare som ser relevanta resealternativ direkt är mycket mer benägna att utforska och påbörja bokningsprocessen.

### Affärspåverkan

Personalisering av hemsidan för nya besökare innebär vanligtvis en 15-20-procentig ökning av konverteringsgraden genom att presentera resealternativ som matchar besökarens plats och intressen i stället för generiskt innehåll.

### Implementera

Använd mönstret [Anonym besökswebb-Personalization](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md). Det här arbetssättet levererar skräddarsytt innehåll till besökare som ännu inte har identifierat sig, med hjälp av tillgängliga signaler som geopositionering, enhetstyp och hänvisningskälla för att personalisera upplevelsen från den allra första sidan.

### Tekniska överväganden

- Geolokaliseringsdata måste tolkas korrekt vid kanten för att betjäna regionsspecifika destinationer, valutor och avgångsportar utan att lägga till latens till startsidans belastning.
- Personalization regler bör ta hänsyn till årstidsutvecklingen för resor per region, surfning av varma väderplatser till besökare i kalla klimat under vintermånaderna, till exempel.
- Strategier för återfallsinnehåll är avgörande för besökare vars position inte kan fastställas eller som kommer via anonyma tjänster.
- Integrationen med bokningssystemets tillgänglighetsflöde säkerställer att aktuella egenskaper och färdvägar verkligen är bokningsbara, vilket förhindrar frustration att marknadsföra utsålda alternativ.


## Återvinning av kundvagnsåtervinning

Identifiera automatiskt när en kund överger sin bokningsvagn och utlöser en e-postresa i flera steg med personaliserade erbjudanden för att uppmuntra till slutförande. Övergivna bokningar är ett av de största intäktsläckorna inom resor och turism, och en snabb uppföljning medan reseavsikten fortfarande återhämtar en meningsfull andel av bokningarna.

### Affärspåverkan

Effektiva program för återfinnande av bokningar ger en 25-35-procentig kundåtervinningsnivå och kan generera ytterligare 50 000-200 000 USD i månadsomsättning beroende på bokningsvolym och genomsnittligt resevärde.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Den här metoden är ett svar på en händelse om att kundvagnen överges i realtid och en påminnelse skickas så fort kundens reseåtergivning är hög.

### Tekniska överväganden

- Tröskelvärden för att upptäcka när en kund lämnar en vagn bör omfatta längre kurser som är typiska vid reseinköp. En 2-4 timmars fördröjning före den första påminnelsen är ofta lämpligare än de 30-60 minuter som används i detaljhandeln.
- E-postinnehållet måste dynamiskt höja den aktuella prissättningen, rum- eller kabintillgängligheten och bilder från bokningssystemet vid sändning eftersom reseinventeringen och taxan ändras ofta.
- Personaliserade incitament, som kostnadsfria uppgraderingar eller resortkrediter, bör hanteras genom affärsregler som tar hänsyn till marginal, säsongsbundenhet och kundens lojalitetsnivå.
- Undertryckningslogiken måste utesluta kunder som slutfört sin bokning via en annan kanal, som ett callcenter eller en resebyrå, för att undvika irrelevanta uppföljningsmeddelanden.


## Avancerad målgruppsanpassning för besökare

Identifiera besökare med hög inköpsmetod med hjälp av AI-driven benägenhetsbedömning och rikta dem mot personaliserade erbjudanden och innehåll. Genom att känna igen vilka besökare som är mest benägna att boka kan organisationen fokusera sina mest övertygande erbjudanden och utåtriktad försäljning på de resenärer som är närmast att fatta ett beslut.

### Affärspåverkan

Att rikta in sig på besökare med hög återgivning med personaliserade erbjudanden ger en 30-40-procentig ökning av konverteringsgraden för dessa segment, och koncentrerar marknadsföringsinvesteringarna där den ger störst avkastning.

### Implementera

Använd mönstret [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md). Den här metoden använder profildata och beteendesignaler i realtid för att personalisera webbupplevelsen för identifierade besökare och leverera skräddarsytt innehåll och erbjudanden som matchar deras nivå av inköpsberedskap.

### Tekniska överväganden

- Propensitetsmodeller måste utbildas i resespecifika intentalsignaler som datumsökningar, prissättningssidvisningar, rumsjämförelser och återkommande besök på samma plats inom ett kort fönster.
- Insatser med hög återgivning, t.ex. live-chattmeddelanden eller tidsbegränsade erbjudanden, bör visas vid naturliga beslutstillfällen i bokningsflödet i stället för att störa surfupplevelsen.
- Poängmodellen bör skilja mellan forskningsavsikt och bokningsmetod, eftersom resenärer ofta undersöker månader innan de är redo att köpa.
- [!DNL Real-Time Customer Data Platform] beräknade attribut kan samla in beteendesignaler mellan sessioner för att behålla en aktuell intent-poäng för varje besökare.


## Bokför merförsäljningskampanjer

När kunden har avslutat en bokning startar automatiskt merförsäljningskampanjer för kabinuppgraderingar, utflykter i land, matpaket och andra tillhöriga. Perioden mellan bokning och resor är när gästerna är mest intresserade av sin kommande resa och mest mottagliga för att förbättra sin upplevelse.

### Affärspåverkan

Bokföringskampanjer med merförsäljning ökar vanligtvis det genomsnittliga ordervärdet med $200-$500 och ökar de extra intäkterna med 15-25 %, vilket gör en enstaka bokning till en betydligt mer värdefull transaktion.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. Den här flerstegsresan vägleder kunderna genom en tidsbestämd sekvens av merförsäljningsmöjligheter och anpassar erbjudandena baserat på vad gästen redan har köpt och deras engagemang med tidigare meddelanden.

### Tekniska överväganden

- Resan måste integreras med bokningssystemet för att veta exakt vad gästen har bokat, vilka uppgraderingar som finns tillgängliga för respektive resväg och aktuella priser för varje ytterligare alternativ.
- Tidpunkten för merförsäljning bör staggasfalteras strategiskt. Kabinuppgraderingar kan erbjudas kort efter bokningen, medan utflykter och matsalar fungerar bättre när resedatum närmar sig.
- Tillgång till lager och tillgänglighet för hjälpprodukter måste kontrolleras när erbjudandet presenteras, eftersom utstrålningskapaciteten och uppgraderingstillgängligheten ändras kontinuerligt.
- [!DNL Journey Optimizer]-personalisering bör ta hänsyn till antalet resenärer i bokningen och rekommendera familjeanpassade utslag för familjebokningar och parorienterade upplevelser för tvåpersonsbokningar.


## Win-Back Campaigns for Lapsed Customers

Identifiera kunder som inte har bokat på tolv eller fler månader och engagera dem med personaliserade erbjudanden och innehåll baserat på deras tidigare reseönskemål. Det är betydligt mer kostnadseffektivt att engagera återkommande gäster än att skaffa helt nya kunder, och tidigare resenärer har redan en varumärkeskänsla som sänker hindren för att boka om.

### Affärspåverkan

Välinriktade återvinnande kampanjer ger en 10-15-procentig återaktiveringsfrekvens bland bortfallna kunder, vilket återhämtar intäkter från gäster som annars aldrig kommer tillbaka.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. Den här flerstegsresan engagerade kunderna på nytt med en progressiv serie meddelanden som utvecklas från inspiration till incitament baserat på kundens respons.

### Tekniska överväganden

- Förlorad kundsegmentering ska ta hänsyn till typisk bokningsfrekvens i resekategorin. En kund som bokar årligen ska inte flaggas som annullerad efter endast sex månaders inaktivitet.
- Återvinningsinnehåll bör hänvisa till kundens tidigare resepreferenser, t.ex. prioriterade destinationer, kabintyper eller resesäsonger, för att visa att varumärket kommer ihåg och värdesätter dem.
- Erbjudandena bör eskalera under hela kundresan, med början med inspirerande innehåll och framsteg till monetära incitament endast om tidigare meddelanden inte genererar engagemang.
- Kundregister måste kontrolleras mot bokningssystemet för bokningar som görs via offlinekanaler som resebyråer eller callcenters för att undvika att skicka återvinnande meddelanden till kunder som faktiskt är aktiva.


## Dynamiska rekommendationer

Visa personaliserade kryssningsrutnät och destinationer baserat på kundens tidigare bokningar, webbhistorik och angivna önskemål. När resenärer ser resvägar som är skräddarsydda efter deras intressen och resestil engagerar de sig djupare i planeringen och går snabbare mot att boka.

### Affärspåverkan

Personaliserade rekommendationer för flygvägar leder till en 20-30-procentig ökning av engagemanget med flygplanssidor, vilket hjälper kunderna att hitta rätt resa snabbare och minskar den minskning som inträffar när resenärerna känner sig överväldigade av för många alternativ.

### Implementera

Använd mönstret [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md). Detta tillvägagångssätt personaliserar webbplatsinnehållet för identifierade besökare genom att använda deras profildata och beteendehistorik för att identifiera de mest relevanta resvägarna och destinationerna.

### Tekniska överväganden

- Logiken i reserekommendationer måste inkludera segling- eller vistelsedatum, avgångsportar och varaktighetsinställningar tillsammans med destinationsintresse för att kunna presentera alternativ som både är tilltalande och praktiska för kunden.
- Integreringen med det centrala bokningssystemet säkerställer att rekommenderade tidsplaner har tillgängligt lager och återspeglar aktuella priser, vilket förhindrar frustration att marknadsföra utsålda varor eller fullt bokade egendomar.
- Säsongsrelaterade faktorer bör ha stor inverkan på rekommendationerna. Kunder som tidigare bokade kryssningar i Medelhavet under sommarmånaderna bör se liknande säsongsalternativ istället för alternativ under lågsäsong.
- Profilsammanfogningsprinciper för [!DNL Experience Platform] måste göra webbläsarbeteendet från flera enheter korrekt enhetligt så att forskning som utförs på mobiler återspeglas i skrivbordsrekommendationerna.


## Nyligen lästa produkter på hemsidan

Visa nyligen visade kryssningar, hotell eller destinationer på hemsidan för att påminna besökarna om deras intresse och uppmuntra besökare att återvända. Resenärer undersöker ofta olika sessioner innan de bokar, och om de tar hänsyn till sina tidigare intressen slipper de besväret att börja söka varje gång de återvänder.

### Affärspåverkan

Genom att visa nyligen använda reseprodukter på hemsidan ökar besöksupplevelsen med 15-20 %, vilket hjälper kunderna att fortsätta där de slutade och korta vägen till bokning.

### Implementera

Använd mönstret [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md). Den här metoden använder besökarens lagrade profildata för att återge tidigare visade objekt på hemsidan, vilket skapar kontinuitet mellan olika webbläsarsessioner.

### Tekniska överväganden

- Data som har visats nyligen måste finnas kvar på olika enheter och sessioner med hjälp av identitetsupplösning, så att en kund som surfar på sin telefon ser samma objekt när de kommer tillbaka på en dator.
- Visade objekt ska visa aktuella priser och tillgänglighetsstatus, med tydliga indikatorer om ett tidigare visat alternativ inte längre är tillgängligt eller om priset har ändrats sedan det senaste besöket.
- Det nya fönstret för visade artiklar bör justeras till bokningscykler för resor. En kryssning som visades för tre månader sedan kan fortfarande vara relevant, till skillnad från en detaljhandelsprodukt som visades för så länge sedan.
- Sekretessöverväganden kräver att nyligen visat innehåll är knutet till kundens medgivandestatus, och ett alternativ för att rensa webbläsarhistoriken bör vara enkelt tillgängligt.


## Avsluta återgivningsmodulen med riktade erbjudanden

När en besökare visar sin avslutningsmetod, ska han/hon visa ett personaliserat modalt erbjudande med relevanta erbjudanden baserat på deras webbläsarbeteende under sessionen. Att fånga en avgående besökare med ett övertygande, sammanhangsberoende erbjudande ger en sista möjlighet att konvertera intresset till en bokning innan de går.

### Affärspåverkan

Modaler för att avsluta med personaliserade reseerbjudanden återfår en konverteringsgrad på 5-10 % bland besökare som annars skulle gå utan bokning, vilket ger intäkter som helt skulle gå förlorade.

### Implementera

Använd mönstret [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). Strategin använder centraliserad beslutslogik för att utvärdera alla tillgängliga erbjudanden och välja det som är mest relevant för den avgående besökaren baserat på deras sessionsbeteende och profildata.

### Tekniska överväganden

- Avsluta avsiktsidentifiering på resebokningswebbplatser måste ta hänsyn till webbläsarbeteende på flera flikar, eftersom resenärer ofta öppnar flera resvägar eller egenskaper på olika flikar utan att egentligen ha för avsikt att lämna dem.
- Erbjudandevalet bör återspegla vad besökaren bläddrat efter under sessionen, vilket ger en rabatt på den specifika destinationen eller egendomen som de utforskat i stället för en allmän kampanj.
- Modal frekvens bör vara strikt begränsad för att hindra besökarna från att se samma erbjudande på varje besök, vilket urholkar det brådskande och uppfattade exklusiviteten i erbjudandet.
- [!DNL Journey Optimizer]-regler för erbjudande bör beakta besökarens lojalitetsnivå och bokningshistorik för att presentera relevanta förmåner, vilket ger premiumgäster meningsfulla fördelar i stället för små rabatter.


## Lojalitetsprogram Personalization

Anpassa webbplatsupplevelsen, erbjudandena och kommunikationen baserat på kundens lojalitetsnivå, poängbalans och engagemangshistorik. Lojalitetsmedlemmar som ser sin status återspeglas i alla kontaktytor och känns erkända och värderade, vilket stärker deras engagemang i varumärket och uppmuntrar till vidareutveckling av skiktet.

### Affärspåverkan

Nivåbaserad personalisering driver på en 25-35-procentig ökning av lojalitetsmedlemmarnas engagemang, fördjupar relationen och snabbar upp intäktsgenereringen och inlösenbeteendena.

### Implementera

Använd mönstret [Flerkanalsresa med beslut](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). Strategin kombinerar resesamordning med realtidsbeslut för att leverera rätt erbjudande via rätt kanal för varje lojalitetsmedlem, som anpassas till deras nivå, preferenser och senaste aktivitet.

### Tekniska överväganden

- Data om lojalitetsprogram, inklusive skiktstatus, poängsaldon och intäktshistorik, måste hämtas in och hållas aktuella för att webbplatspersonaliseringen och erbjudandena ska återspegla kundens faktiska anseende.
- Nivåspecifika fördelar som tidig åtkomst till bokningar, kostnadsfria uppgraderingar och exklusiv prissättning måste tillämpas vid tidpunkten för inlösen, vilket kräver nära integrering med boknings- och prissättningssystemen.
- Poängsaldoförändringar från bokningar, uppehåll och partnertransaktioner bör utlösa en omberäkning av personaliseringsreglerna i nära realtid, så att en kund som precis har tjänat tillräckligt många poäng för en belöning omedelbart ser det alternativet.
- [!DNL Real-Time Customer Data Platform] målgrupper ska struktureras runt lojalitetsnivåer och viktiga milstolpar för engagemang, som att närma sig nästa nivå eller riskera att nivån degraderas.


## Påminnelser om flerkanalsbokning

Skicka personliga bokningspåminnelser via e-post, SMS och push-meddelanden till kunder som har börjat men inte slutfört sina bokningar. Resenärerna börjar ofta bokningsprocessen och blir avbrutna, och når dem via de kanaler de föredrar med en påminnelse och deras sparade reseinformation för dem tillbaka för att slutföra bokningen.

### Affärspåverkan

Påminnelser om flerkanalsbokning förbättrar antalet slutförda bokningar med 20-30 %, vilket återvinner betydande intäkter från kunder som hade för avsikt att boka men som spårades innan de slutfördes.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Den här metoden utlöser påminnelser automatiskt när en ofullständig bokningshändelse upptäcks, vilket ger aktuella meddelanden i de kanaler kunden föredrar.

### Tekniska överväganden

- Logiken för val av kanaler ska respektera kundernas kommunikationsinställningar och optimera leveransen baserat på tidigare interaktionsmönster, och skicka push-meddelanden till kunder som svarar väl på mobiler och e-post till dem som föredrar det.
- Påminnelseinnehållet måste innehålla en djup länk som returnerar kunden direkt till den sparade bokningen med alla markeringar intakta, vilket eliminerar möjligheten att ange resedatum, rumsinställningar och gästinformation igen.
- Regler för timing och frekvens bör samordna alla kanaler för att undvika att överbelasta kunden. Ett e-postmeddelande och ett push-meddelande om samma bokning bör vara lämpligt placerade i stället för att skickas samtidigt.
- Integrationen med egenskapshanteringen eller det centrala reservationssystemet måste verifiera att den rumstyp, det värde och de datum som ursprungligen valts fortfarande är tillgängliga innan påminnelsen skickas och uppdatera meddelandet om tillgängligheten har ändrats.


## Säsongskampanj, Personalization

Anpassa kampanjer och erbjudanden baserat på säsongsinställningar, tidigare säsongsbokningar och aktuella säsongstrender. Resenärerna påverkas mycket av säsonger, och kampanjer som är anpassade till deras visade säsongsintressen och aktuella resetrender är mycket mer övertygande än generiska kampanjer.

### Affärspåverkan

Personaliserade kampanjer med säsongsbaserad annonsering ökar konverteringsgraden för bokning med 15-25 %, vilket säkerställer att marknadsföringsinvesteringarna koncentreras till de destinationer och reseprodukter som är mest troliga att få gensvar hos varje kund.

### Implementera

Använd mönstret [Aktivera utgående batchmeddelande](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md). Detta tillvägagångssätt levererar personaliserade säsongskampanjer till stora målgrupper på regelbunden basis och segmenterar kunderna efter deras säsongsrelaterade resemönster och önskemål.

### Tekniska överväganden

- Kundens säsongsinställningar bör bygga på historiska bokningsdata och identifiera mönster som enhetliga semestrar på sommarstrand eller vinterskidresor för att informera om kampanjinriktningen.
- Kampanjplaneringen måste ta hänsyn till ledtider för resebranschen. Sommarsemesterkampanjer bör lanseras i tidig vår när familjer planerar, inte i juni när de flesta bokningar redan görs.
- Priser och tillgänglighetsflöden för säsongsbunden inventering måste integreras så att kampanjerna återspeglar realtidsfrekvenser och den faktiska rums- eller kabintillgängligheten under de aktuella reseperioderna.
- [!DNL Experience Platform] målgrupper bör kombinera säsongsinställningsdata med nyligen använda indikatorer för att prioritera kunder som befinner sig i deras typiska planeringsfönster inför den kommande säsongen.


## Gruppbokningsrekommendationer

Identifiera kunder som ofta bokar gruppresor och proaktivt rekommenderar grupppaket, familjevänliga alternativ eller bokningar i flera rum. Gruppbokningar ger avsevärt högre intäkter per transaktion och kunder med ett påvisat mönster för gruppresor svarar på välstrukturerade alternativ som förenklar planeringsprocessen.

### Affärspåverkan

Förebyggande rekommendationer för gruppbokning ökar det genomsnittliga ordervärdet med $1 000-$3 000 per bokning, vilket fångar upp det fulla värdet av gruppresetransaktioner som annars skulle kunna delas upp i flera enskilda reservationer.

### Implementera

Använd mönstret [Beteenderekommendation](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Den här metoden använder AI-drivna modeller som bygger på kundbokningsmönster och beteenden för att rekommendera de mest relevanta gruppresemöjligheterna för varje kund.

### Tekniska överväganden

- Identifiering av gruppresor kräver analys av bokningshistorik för mönster som till exempel bokningar i flera rum, bokningar med flera passagerare och samordnade bokningar som gjorts i närhet för samma datum och destination.
- Grupppaketpriset måste dras dynamiskt från bokningssystemet eftersom grupppriserna ofta skiljer sig från enskilda priser och kan kräva miniminivåer eller förskottsbokningsfönster.
- Rekommendationsinnehållet ska ta upp grupporganisatörernas unika behov, inklusive information om gruppmatningsalternativ, mötesplatser, blockbokningsrabatter och tillgänglighet för gruppexponering.
- Profilberikning för [!DNL Real-Time Customer Data Platform] ska flagga kunder som gruppreseorganisatörer baserat på deras bokningsmönster, vilket möjliggör riktade kampanjer under högtider för gruppplanering som familjesäsong eller företagsfönster.
