---
title: Användningsexempel
description: Upptäck hur detaljhandelsorganisationer använder Adobe Experience Platform för att personalisera shoppingupplevelser, återställa övergivna kundvagnar och öka kundlojaliteten.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '2590'
ht-degree: 0%

---


# Användningsexempel

Butiksorganisationer använder Adobe Experience Platform för att sammanställa kunddata från onlinebutiker, fysiska platser och lojalitetsprogram i en enda vy över varje kund. Denna grund möjliggör personaliserade shoppingupplevelser, vältajmad utåtriktad marknadsföring som återhämtar förlorade intäkter och lojalitetsstrategier som får kunderna att komma tillbaka.

## Personaliserade produktrekommendationer

Visa anpassade produktrekommendationer för hemsida, kategorisidor och produktinformationssidor baserat på webbläsarhistorik, inköpshistorik och liknande kundbeteende. När kunderna ser produkter som är skräddarsydda efter deras intressen spenderar de mer tid på att utforska och är mer benägna att köpa.

### Affärspåverkan

Detaljhandlare ser vanligtvis en ökning på 20-30 % av klickfrekvensen och en 15-25-procentig förbättring av konverteringsgraden när de tar emot personaliserade rekommendationer i stället för statiska produktlistor.

### Implementera

Använd mönstret [Beteenderekommendation](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Den här metoden använder AI-drivna rekommendationsmodeller som kontinuerligt lär sig av kundinteraktioner för att identifiera de mest relevanta produkterna för varje individ.

### Tekniska överväganden

- Produktkatalogdata måste importeras och hållas aktuella, inklusive produktattribut, bilder, priser och tillgänglighet, för att rekommendationerna ska återspegla vad kunderna faktiskt kan köpa.
- Beteendesignaler som produktvisningar, tilläggshändelser och köp måste flöda i nära realtid för att rekommendationerna ska bli aktuella i en enda webbläsarsession.
- Rekommendationsmodellerna kräver en strategi där nya besökare som saknar webbhistorik kan komma igång, och som vanligtvis återgår till trender eller bästsäljande produkter.
- Sidladdningsprestanda måste övervakas noggrant eftersom personaliseringsanrop inte ska ge någon märkbar fördröjning för shoppingupplevelsen.


## Återställning av övergiven kundvagn via e-post

Skicka automatiskt skräddarsydda e-postpåminnelser till kunder som övergett sin kundvagn, inklusive de exakta artiklar som blivit kvar och relevanta erbjudanden för att uppmuntra till slutförande. Att kunden överger en kundvagn är en av de största inkomstkällorna inom detaljhandeln och en snabb uppföljning kan återta en betydande del av försäljningen.

### Affärspåverkan

Effektiva kundvagnsåtervinningsprogram ger en 25-35-procentig kundåtervinningsnivå och kan generera ytterligare 100 000-500 000 USD i månadsomsättning beroende på butiksvolym.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Den här metoden är ett svar på en händelse om att kundvagnen överges i realtid, vilket innebär att en påminnelse skickas i tid medan inköpsmetoden fortfarande är hög.

### Tekniska överväganden

- Identifiering av kundöverhoppning kräver att man definierar ett tröskelvärde för inaktivitet (vanligtvis 30-60 minuter) innan den första påminnelsen aktiveras, så att man undviker meddelanden till kunder som fortfarande aktivt handlar.
- E-postinnehåll måste dynamiskt hämta aktuella produktbilder, priser och tillgänglighet från katalogen när de skickas, eftersom artiklar kan sälja ut eller ändra priset mellan nedläggning och leverans.
- Regler för frekvensbegränsning bör förhindra kunder från att ta emot e-postmeddelanden om flera övergivna varukorgar under en kort period, särskilt om de ofta överger varukorgar.
- Listor för samtycke och inaktivering måste kontrolleras innan de skickas och kunder som slutfört sitt köp via en annan kanal bör uteslutas i realtid.


## Lagerbaserade nödkampanjer

Utlös varningar och kampanjer i realtid när produktlagret är lågt, vilket skapar ett akut behov och uppmuntrar till omedelbart köp. Handlare som ser att bara ett fåtal saker återstår är motiverade att agera snabbt i stället för att fördröja sitt beslut.

### Affärspåverkan

Snabba kampanjer med låga lager genererar vanligtvis en 30-40-procentig ökning av konverteringsgraden för aktuella produkter, samtidigt som de minskar överlagret genom att snabba upp försäljningen av produkter som rör sig långsamt.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Detta tillvägagångssätt svarar på lagertröskelhändelser och aktiverar automatiskt brådskande meddelanden när lagernivåerna underskrider definierade gränser.

### Tekniska överväganden

- Inventeringsflödena måste integreras med kunddataplattformen i nära realtid så att brådskande meddelanden speglar de faktiska lagernivåerna i stället för gamla data.
- Tröskelvärden bör konfigureras per produktkategori eftersom ett tröskelvärde för&quot;låg lagernivå&quot; för en råvara med hög volym skiljer sig avsevärt från ett för en lyxartikel.
- Meddelanden måste vara sanningsenliga och förenliga med konsumentskyddsreglerna. Om falska brister uppstår kan varumärkesförtroendet skadas och reklamstandarderna på vissa marknader kan överträdas.
- Meddelanden och e-postkanaler på plats bör samordnas så att kunder som redan har köpt inte kan fortsätta få brådskande meddelanden för samma produkt.


## Merförsäljning och merförsäljning

Visa relevanta korsförsäljnings- och merförsäljningsprodukter i kassan, via e-post och på produktsidor baserat på inköpsmönster och produktrelationer. Om du föreslår kompletterande eller premiumalternativ vid rätt tillfälle ökar korgstorleken utan att kunderna själva behöver söka efter relaterade artiklar.

### Affärspåverkan

Välbeprövade korsförsäljnings- och merförsäljningsstrategier ökar det genomsnittliga ordervärdet med 25-75 dollar och ökar intäkterna per transaktion med 10-15 %.

### Implementera

Använd mönstret [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). Strategin använder centraliserad beslutslogik för att utvärdera alla tillgängliga erbjudanden och välja det bästa alternativet för korsförsäljning eller merförsäljning för varje kund och kontext.

### Tekniska överväganden

- Produktrelationsdata, inklusive&quot;ofta köpta&quot; föreningar och uppgraderingsvägar, måste underhållas och uppdateras regelbundet för att återspegla aktuella inköpsmönster.
- Erbjudandets rangordningslogik bör ta hänsyn till marginal-, relevans- och lagernivåer så att de mest lönsamma och tillgängliga alternativen visas först.
- Korsförsäljningsrekommendationer vid utcheckning måste läsas in snabbt och inte störa inköpsflödet. Sakta eller påträngande förslag kan faktiskt minska konverteringsgraden.
- Beslutsreglerna för [!DNL Journey Optimizer] bör innehålla reserverbjudanden så att alla berättigade kunder får en rekommendation, även när det högst rankade alternativet inte är tillgängligt.


## Välkomstserie till nya kunder

Automatisera en välkomstserie för flera e-postmeddelanden för nya kunder med personaliserade produktrekommendationer, varumärkesberättande och specialerbjudanden. De första interaktionerna efter att en kund gått med formar deras långsiktiga relation med varumärket, vilket gör den här serien till ett av de mest slagkraftiga program en återförsäljare kan köra.

### Affärspåverkan

En väldesignad välkomstserie genererar en 40-50-procentig engagemangsgrad bland nya kunder och förbättrar livstidsvärdet på ett meningsfullt sätt genom att tidigt bygga upp varumärkestillhörigheten.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. Den här multitouch-vårdsresan vägleder nya kunder genom en sekvens av varumärkesintroduktion, produktupptäckt och stimulansmeddelanden som anpassar sig efter deras engagemang.

### Tekniska överväganden

- Inlösaren för kundinträde måste på ett tillförlitligt sätt fånga upp nya kundskapshändelser från alla registreringskällor, inklusive webben, mobilappar, butiksplatser och externa marknadsplatser.
- Vänta steg mellan e-postmeddelanden ska konfigureras baserat på interaktionsdata. Kunder som öppnar och klickar kan få nästa meddelande snabbare, medan mindre engagerade kunder drar nytta av mer avstånd.
- Produktrekommendationer i välkomstmejl bör återspegla vad kunden bläddrat efter eller köpt under sitt första besök, inte generiska bästsäljare.
- Kunder som gör ett köp under välkomstserien bör gå in i ett postinköpsflöde i stället för att fortsätta att få kundfokuserade meddelanden.


## Avlämningsmeddelanden för pris

Meddela kunderna via e-post eller push-meddelanden när produkter i deras önskelista eller tidigare visade artiklar sjunker till priset. Kunder som visade intresse men inte köpte något är mycket lyhörda för prissänkningar, vilket gör detta till det mest effektiva sättet att omvandla övervägande till försäljning.

### Affärspåverkan

Varningar om prisfall genererar en konverteringsgrad på 20-30 % bland mottagarna och ökar kundnöjdheten genom att hjälpa kunderna att känna att de får det bästa värdet.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Detta tillvägagångssätt svarar på produktprisförändringar och matchar dem mot kundens intressesignaler för att leverera meddelanden i rätt tid.

### Tekniska överväganden

- För prisförändringsdetektering krävs att aktuella priser jämförs med tidigare värden i produktkatalogsflödet, och endast att varningar utlöses för meningsfulla minskningar i stället för mindre fluktuationer.
- Intressesignalerna (önskelistetillägg, produktsidesvisningar, tidsåtgång på produktsidor) måste lagras och matchas effektivt mot potentiellt tusentals dagliga prisförändringar.
- Meddelandena bör innehålla det ursprungliga priset, det nya priset och besparingsbeloppet för att tydligt kunna förmedla värdet, otydliga&quot;prisreducerade&quot; meddelanden undertrycker specifika återgivningshänvisningar.
- [!DNL Real-Time Customer Data Platform] segment för priskänsliga kunder kan användas för att prioritera varningsleverans och anpassa meddelandetonen.


## Påfyllnadspåminnelser

Skicka automatiska påminnelser till kunder om produkter de köper regelbundet, som prenumerationsobjekt och förbrukningsartiklar, för att uppmuntra till upprepade köp innan de tar slut. Proaktiva påminnelser minskar risken att kunder byter till en konkurrent bara för att de har glömt att beställa.

### Affärspåverkan

Påminnelseprogram för påfyllnad ger en 30-40-procentig upprepningsfrekvens och avsevärt förbättrad kundlojalitet genom att göra det enkelt för kunderna att förnya sina produkter.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. Den här återkommande schemalagda resan använder prognoser om inköpsfrekvens för att skicka påminnelser vid den optimala tidpunkten innan en kund sannolikt kommer att behöva fylla på något.

### Tekniska överväganden

- Beräkningen av inköpsfrekvensen måste ta hänsyn till olika förbrukningsfrekvenser för olika produktkategorier. En påminnelse om kaffe bör komma på en annan plats än en för rengöring av leveranserna.
- Resan bör justera sin timing dynamiskt när en kund beställer tidigare eller senare än förväntat, vilket omkalibrerar nästa påminnelse baserat på uppdaterade inköpsdata.
- Påminnelser ska innehålla en direktbeställningslänk eller ett återköpsalternativ med ett klick för att minimera friktionen och maximera konverteringen från meddelandet.
- Kunder som redan har ombeställt via en annan kanal (i butik, prenumerationstjänst) måste ignoreras för att undvika att skicka irrelevanta påminnelser.


## Personaliserade kategorisidor

Anpassa kategorisidor dynamiskt för att visa de mest relevanta produkterna först baserat på varje kunds önskemål, tidigare köp och webbläsarbeteende. När kunderna ser produkter som är anpassade efter sina smak överst på sidan upptäcker de vad de vill ha snabbare och konverterar till högre priser.

### Affärspåverkan

Personaliserade kategorisidor ger en 25-35-procentig ökning av engagemanget hos kategorisidor och förbättrar produktupptäckt på ett meningsfullt sätt, särskilt för återförsäljare med stora kataloger.

### Implementera

Använd mönstret [Beteenderekommendation](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Den här metoden använder urvalsstrategier och rangordningsmodeller för att ordna om produkter på kategorisidor baserat på varje besökares profil och beteende i realtid.

### Tekniska överväganden

- Produktrankningen måste utföras tillräckligt snabbt för att undvika upplevda sidladdningsladdningar. Serveranpassning eller kantbaserad beslutsfattande krävs ofta för kategorisidor med hundratals produkter.
- Anpassningslogiken bör kombinera individuella preferenser med försäljningsregler, vilket säkerställer att marknadsförda produkter, nya produkter och säsongsobjekt fortfarande får lämplig synlighet.
- En infrastruktur för A/B-testning bör finnas på plats för att kontinuerligt mäta intäktseffekten av personaliserad sortering jämfört med standardregler för försäljning.
- [!DNL Experience Platform] Webbimplementeringen av SDK måste fånga upp sidinteraktioner i kategorin (rullningsdjup, produktklick, filteranvändning) för att kontinuerligt förfina rangordningsmodellerna.


## Uppföljningskampanjer efter inköp

Skicka e-postmeddelanden efter köp med tips om produkter, produktförslag, granskningsbegäranden och information om lojalitetsprogram. Perioden direkt efter ett köp är när kunderna är mest engagerade i varumärket, vilket gör det till ett idealiskt fönster för att fördjupa relationen och uppmuntra till framtida aktiviteter.

### Affärspåverkan

Effektiva kampanjer efter inköp ökar antalet inskickade granskningar med 15-20 % och ger en 10-15-procentig upprepningsfrekvens, vilket gör att engångsköpare blir lojala kunder.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. I det här flerstegsflödet används förgreningslogik för att skräddarsy uppföljningsmeddelanden baserat på produkttyp, kundsegment och engagemang med tidigare e-postmeddelanden i serien.

### Tekniska överväganden

- Resan måste ta hänsyn till orderstatus. Tips och förfrågningar ska skickas först när produkten har levererats, inte omedelbart efter köpet.
- Produktspecifikt innehåll (behandlingsanvisningar, användningsguider, förslag på tillbehör) kräver ett innehållsmappningssystem som associerar varje produktkategori med relevant uppföljningsmaterial.
- Tidpunkten för begäran om översyn bör optimeras baserat på produktkategorin. Elektronik kan behöva en längre användningsperiod innan en meningsfull granskning kan ses över kort efter leveransen.
- Kunder som initierar en retur eller ett utbyte ska automatiskt tas bort från standardflödet efter köp och omdirigeras till en serviceåterställningsväg.


## VIP exklusiva erbjudanden

Identifiera värdefulla kunder och leverera exklusiva erbjudanden, tidig tillgång till försäljning och personaliserade shoppingupplevelser som belönar deras lojalitet. Att behålla kunder i toppskiktet är mycket mer kostnadseffektivt än att skaffa nya, och exklusiv behandling stärker den känslomässiga koppling som håller dem spenderade.

### Affärspåverkan

VIP-program genererar vanligtvis 50-70 % engagemang från kunder i toppskiktet och förbättrar kundens livstidsvärde genom att minska bortfallet bland de mest lönsamma segmenten.

### Implementera

Använd mönstret [Flerkanalsresa med beslut](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). Detta tillvägagångssätt kombinerar resesamordning med beslut i realtid för att välja erbjudande, vilket säkerställer att alla VIP-kunder får det mest relevanta exklusiva erbjudandet i alla kanaler.

### Tekniska överväganden

- VIP:s kriterier för segmentering måste vara tydligt definierade med hjälp av statistik om aktuell tid, frekvens och penningvärde, och segmenten bör uppdateras tillräckligt ofta för att fånga upp kunder som nyligen har kvalificerat sig eller diskvalificerats.
- Exklusiva erbjudanden måste verkställas vid inlösen (webb, app, butik) för att förhindra att kunder utanför VIP får tillgång till dem, vilket kräver integrering med kampanjsystem och prissättningssystem.
- Kanalinställningarna varierar avsevärt bland värdefulla kunder, vissa föredrar e-post, andra svarar på appmeddelanden eller direktreklam, så resan bör anpassa leveranskanalerna baserat på tidigare engagemang.
- [!DNL Journey Optimizer]-beslut måste koordineras över alla kanaler för att förhindra att en VIP-kund får samma erbjudande via e-post, push och SMS samtidigt.


## Aviseringar utanför lagret

Låt kunderna registrera sig för meddelanden när färdiga produkter blir tillgängliga och meddela dem sedan automatiskt via e-post eller SMS. Genom att hämta efterfrågan på produkter som inte finns tillgängliga förhindrar du förlorad försäljning och ger kunderna en anledning att återvända till butiken i stället för att köpa från en konkurrent.

### Affärspåverkan

Aviseringar som skickas tillbaka i lager når en konverteringsgrad på 40-50 % bland abonnenterna och minskar på ett betydande sätt försäljningen av efterfrågade produkter som har tillfälliga lager.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Den här metoden utlöser meddelanden om lagerbaserade händelser och matchar lageruppdateringar mot kundmeddelanden för att leverera aviseringar i rätt tid.

### Tekniska överväganden

- Inventeringsövervakningen måste snabbt upptäcka nya låshändelser. Om du dröjer några timmar kan produkten gå ut igen innan de anmälda kunderna har chansen att köpa.
- När en populär produkt återställs i en begränsad mängd bör meddelandena fördelas eller prioriteras efter registreringsdatum för att undvika att skicka varningar till fler kunder än vad som finns i det tillgängliga lagret.
- Anmälningsmekanismen måste fånga upp kanalinställningarna (e-post eller SMS) och uppfylla anmälningskraven för varje kanal, särskilt för SMS.
- Profilattributen för [!DNL Real-Time Customer Data Platform] ska spåra vilka produkter varje kund tittar på så att dubblettmeddelanden förhindras om samma produkt återställs flera gånger.


## Korrektur för sociala medier - Personalization

Visa personliga sociala bevis, inklusive recensioner, omdömen och förslag om&quot;kunder som köpt det här också&quot;, baserat på varje kunds profil och önskemål. Skräddarsy sociala bevis för att reflektera upplevelserna hos liknande kunder bygger förtroende effektivare än enbart generiska betyg.

### Affärspåverkan

Personaliserade sociala bevis ökar konverteringsgraden med 10-15 % och ökar kundernas förtroende, särskilt för förstagångsköpare och högprisprodukter där köpvanheten är störst.

### Implementera

Använd mönstret [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md). Det här arbetssättet personaliserar webbinnehåll för identifierade besökare och väljer de mest relevanta granskningarna och elementen för socialt korrektur baserat på kundens profil, önskemål och surfningssammanhang.

### Tekniska överväganden

- Gransknings- och värderingsdata måste struktureras och taggas utifrån kundattribut (t.ex. köpkontext, kundsegment och produktanvändningsfall) för att möjliggöra meningsfull filtrering och personalisering.
- Sociala korrekturrundselement bör läsas in asynkront för att undvika att huvudproduktsidans rendering blockeras, eftersom granskningsdata kan komma från en tredjepartsgranskningsplattform med varierande svarstider.
- Sekretessreglerna kräver att alla kunddata som används för att matcha granskningar mot besökare hanteras enligt medgivandepreferenser. Att visa&quot;kunder som du&quot;-innehåll innebär profilering som kan kräva utlämnande.
- [!DNL Experience Platform]-målgruppsmedlemskap kan användas för att välja vilka recensioner som ska markeras och visa utomhusentusiaster recensioner från utomhusshoppare i stället för generiska topprankade recensioner.
