---
title: Användningsexempel
description: Upptäck hur detaljhandelsorganisationer använder Adobe Experience Platform för att personalisera shoppingupplevelser, återställa övergivna kundvagnar och öka kundlojaliteten.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: 89a5b6b5-bb71-4154-bb3b-f6dbbbef13eb
source-git-commit: 3542d76106fada9019b70a8cc9fd4c74872d4995
workflow-type: tm+mt
source-wordcount: '7216'
ht-degree: 0%

---

# Användningsexempel

Butiksorganisationer använder Adobe Experience Platform för att sammanställa kunddata från onlinebutiker, fysiska platser och lojalitetsprogram i en enda vy över varje kund. Denna grund möjliggör personaliserade shoppingupplevelser, vältajmad utåtriktad marknadsföring som återhämtar förlorade intäkter och lojalitetsstrategier som får kunderna att komma tillbaka.

## Personaliserade produktrekommendationer

Visa anpassade produktrekommendationer för hemsida, kategorisidor och produktinformationssidor baserat på webbläsarhistorik, inköpshistorik och liknande kundbeteende. När kunderna ser produkter som är skräddarsydda efter deras intressen spenderar de mer tid på att utforska och är mer benägna att köpa.

### Affärspåverkan

Detaljhandlarna ser bättre klickfrekvenser och konverteringsgrader när de levererar personaliserade rekommendationer i stället för statiska produktlistor.

### Implementera

Använd mönstret [Beteenderekommendation](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Den här metoden använder AI-drivna rekommendationsmodeller som kontinuerligt lär sig av kundinteraktioner för att identifiera de mest relevanta produkterna för varje individ. Det här är det rätta mönstret när objektuppsättningen är stor och ändras kontinuerligt och valet styrs av beteendetillhörighet - snarare än en avgränsad uppsättning erbjudanden som styrs av behörighetsregler.

### Tekniska överväganden

- Produktkatalogdata måste importeras och hållas aktuella, inklusive produktattribut, bilder, priser och tillgänglighet, för att rekommendationerna ska återspegla vad kunderna faktiskt kan köpa.
- Beteendesignaler som produktvisningar, tilläggshändelser och köp måste flöda i nära realtid för att rekommendationerna ska bli aktuella i en enda webbläsarsession.
- Rekommendationsmodellerna kräver en strategi där nya besökare som saknar webbhistorik kan komma igång, och som vanligtvis återgår till trender eller bästsäljande produkter.
- Sidladdningsprestanda måste övervakas noggrant eftersom personaliseringsanrop inte ska ge någon märkbar fördröjning för shoppingupplevelsen.


## Återställning av övergiven kundvagn via e-post

Skicka automatiskt skräddarsydda e-postpåminnelser till kunder som övergett sin kundvagn, inklusive de exakta artiklar som blivit kvar och relevanta erbjudanden för att uppmuntra till slutförande. Att kunden överger en kundvagn är en av de största inkomstkällorna inom detaljhandeln och en snabb uppföljning kan återta en betydande del av försäljningen.

### Affärspåverkan

Effektiva kundvagnsåtervinningsprogram förbättrar kundvagnens återvinningsgrad och kan generera meningsfulla inkrementella intäkter beroende på butikens volym.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Den här metoden är ett svar på en händelse om att kundvagnen överges i realtid, vilket innebär att en påminnelse skickas i tid medan inköpsmetoden fortfarande är hög. Det här är det rätta mönstret när en diskret kundåtgärd är utlösaren och det svar som krävs är ett enda tidskänsligt meddelande - snarare än en sekvens i flera steg eller dynamiskt urval av erbjudanden.

### Tekniska överväganden

- Identifiering av kundöverhoppning kräver att man definierar ett tröskelvärde för inaktivitet (vanligtvis 30-60 minuter) innan den första påminnelsen aktiveras, så att man undviker meddelanden till kunder som fortfarande aktivt handlar.
- E-postinnehåll måste dynamiskt hämta aktuella produktbilder, priser och tillgänglighet från katalogen när de skickas, eftersom artiklar kan sälja ut eller ändra priset mellan nedläggning och leverans.
- Regler för frekvensbegränsning bör förhindra kunder från att ta emot e-postmeddelanden om flera övergivna varukorgar under en kort period, särskilt om de ofta överger varukorgar.
- Listor för samtycke och inaktivering måste kontrolleras innan de skickas och kunder som slutfört sitt köp via en annan kanal bör uteslutas i realtid.


## Lagerbaserade nödkampanjer

Utlös varningar och kampanjer i realtid när produktlagret är lågt, vilket skapar ett akut behov och uppmuntrar till omedelbart köp. Handlare som ser att bara ett fåtal saker återstår är motiverade att agera snabbt i stället för att fördröja sitt beslut.

### Affärspåverkan

Snabba kampanjer med låga lager ökar konverteringsgraden för aktuella produkter samtidigt som de minskar överlagret genom att snabba upp försäljningen av produkter som rör sig långsamt.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Detta tillvägagångssätt svarar på lagertröskelhändelser och aktiverar automatiskt brådskande meddelanden när lagernivåerna underskrider definierade gränser. Det här är det rätta mönstret när utlösaren är en systemhändelse snarare än ett kundbeteende, och den kommunikation som krävs är omedelbar och reaktiv snarare än en kontinuerlig vårdssekvens.

### Tekniska överväganden

- Inventeringsflödena måste integreras med kunddataplattformen i nära realtid så att brådskande meddelanden speglar de faktiska lagernivåerna i stället för gamla data.
- Tröskelvärden bör konfigureras per produktkategori eftersom ett tröskelvärde för&quot;låg lagernivå&quot; för en råvara med hög volym skiljer sig avsevärt från ett för en lyxartikel.
- Meddelanden måste vara sanningsenliga och förenliga med konsumentskyddsreglerna. Om falska brister uppstår kan varumärkesförtroendet skadas och reklamstandarderna på vissa marknader kan överträdas.
- Meddelanden och e-postkanaler på plats bör samordnas så att kunder som redan har köpt inte kan fortsätta få brådskande meddelanden för samma produkt.


## Merförsäljning och merförsäljning

Visa relevanta korsförsäljnings- och merförsäljningsprodukter i kassan, via e-post och på produktsidor baserat på inköpsmönster och produktrelationer. Om du föreslår kompletterande eller premiumalternativ vid rätt tillfälle ökar korgstorleken utan att kunderna själva behöver söka efter relaterade artiklar.

### Affärspåverkan

Välbeprövade strategier för korsförsäljning och merförsäljning ökar det genomsnittliga ordervärdet och ökar intäkterna per transaktion, vilket bidrar till en starkare övergripande korgekonomi.

### Implementera

Använd mönstret [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md). Strategin använder centraliserad beslutslogik för att utvärdera alla tillgängliga erbjudanden och välja det bästa alternativet för korsförsäljning eller merförsäljning för varje kund och kontext. Det här är det rätta mönstret när valet av erbjudanden måste ta hänsyn till marginal, lagertillgänglighet och produktrelationsregler - affärsbegränsningar som kräver styrd beslutslogik i stället för enbart beteendetillhörighet.

### Tekniska överväganden

- Produktrelationsdata, inklusive&quot;ofta köpta&quot; föreningar och uppgraderingsvägar, måste underhållas och uppdateras regelbundet för att återspegla aktuella inköpsmönster.
- Erbjudandets rangordningslogik bör ta hänsyn till marginal-, relevans- och lagernivåer så att de mest lönsamma och tillgängliga alternativen visas först.
- Korsförsäljningsrekommendationer vid utcheckning måste läsas in snabbt och inte störa inköpsflödet. Sakta eller påträngande förslag kan faktiskt minska konverteringsgraden.
- Beslutsreglerna för [!DNL Journey Optimizer] bör innehålla reserverbjudanden så att alla berättigade kunder får en rekommendation, även när det högst rankade alternativet inte är tillgängligt.


## Välkomstserie till nya kunder

Automatisera en välkomstserie för flera e-postmeddelanden för nya kunder med personaliserade produktrekommendationer, varumärkesberättande och specialerbjudanden. De första interaktionerna efter att en kund gått med formar deras långsiktiga relation med varumärket, vilket gör den här serien till ett av de mest slagkraftiga program en återförsäljare kan köra.

### Affärspåverkan

En väldesignad välkomstserie skapar stark interaktion bland nya kunder och förbättrar livstidsvärdet på ett meningsfullt sätt genom att snabbt bygga upp varumärkestillhörigheten.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. Den här multitouch-vårdsresan vägleder nya kunder genom en sekvens av varumärkesintroduktion, produktupptäckt och stimulansmeddelanden som anpassar sig efter deras engagemang. Det här är det rätta mönstret när användningsfallet kräver ett sekvensflöde med flera meddelanden på flera dagar med villkorlig förgrening baserat på engagemangshändelser - ett enda utlöst meddelande kan inte hantera beroendelogiken mellan steg.

### Tekniska överväganden

- Inlösaren för kundinträde måste på ett tillförlitligt sätt fånga upp nya kundskapshändelser från alla registreringskällor, inklusive webben, mobilappar, butiksplatser och externa marknadsplatser.
- Vänta steg mellan e-postmeddelanden ska konfigureras baserat på interaktionsdata. Kunder som öppnar och klickar kan få nästa meddelande snabbare, medan mindre engagerade kunder drar nytta av mer avstånd.
- Produktrekommendationer i välkomstmejl bör återspegla vad kunden bläddrat efter eller köpt under sitt första besök, inte generiska bästsäljare.
- Kunder som gör ett köp under välkomstserien bör gå in i ett postinköpsflöde i stället för att fortsätta att få kundfokuserade meddelanden.


## Avlämningsmeddelanden för pris

Meddela kunderna via e-post eller push-meddelanden när produkter i deras önskelista eller tidigare visade artiklar sjunker till priset. Kunder som visade intresse men inte köpte något är mycket lyhörda för prissänkningar, vilket gör detta till det mest effektiva sättet att omvandla övervägande till försäljning.

### Affärspåverkan

Aviseringar om prisfall genererar förbättrad konverteringsgrad bland mottagare och ökar kundnöjdheten avsevärt genom att hjälpa kunderna att känna att de får det bästa värdet.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Detta tillvägagångssätt svarar på produktprisförändringar och matchar dem mot kundens intressesignaler för att leverera meddelanden i rätt tid. Det här är det rätta mönstret när utlösaren är en katalogsystemhändelse och leveransfönstret är tidskänsligt - en kontinuerlig resa blir för långsam och ingen uppföljning i flera steg behövs efter det första meddelandet.

### Tekniska överväganden

- För prisförändringsdetektering krävs att aktuella priser jämförs med tidigare värden i produktkatalogsflödet, och endast att varningar utlöses för meningsfulla minskningar i stället för mindre fluktuationer.
- Intressesignalerna (önskelistetillägg, produktsidesvisningar, tidsåtgång på produktsidor) måste lagras och matchas effektivt mot potentiellt tusentals dagliga prisförändringar.
- Meddelandena bör innehålla det ursprungliga priset, det nya priset och besparingsbeloppet för att tydligt kunna förmedla värdet, otydliga&quot;prisreducerade&quot; meddelanden undertrycker specifika återgivningshänvisningar.
- [!DNL Real-Time Customer Data Platform] segment för priskänsliga kunder kan användas för att prioritera varningsleverans och anpassa meddelandetonen.


## Påfyllnadspåminnelser

Skicka automatiska påminnelser till kunder om produkter de köper regelbundet, som prenumerationsobjekt och förbrukningsartiklar, för att uppmuntra till upprepade köp innan de tar slut. Proaktiva påminnelser minskar risken att kunder byter till en konkurrent bara för att de har glömt att beställa.

### Affärspåverkan

Påminnelseprogram för påfyllnad ger högre återköpsfrekvenser och förbättrad kundlojalitet genom att göra det enkelt för kunderna att förnya sina produkter.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. Den här återkommande schemalagda resan använder prognoser om inköpsfrekvens för att skicka påminnelser vid den optimala tidpunkten innan en kund sannolikt kommer att behöva fylla på något. Det här är det rätta mönstret när det inte finns någon diskret utlösande händelse och tidsbestämning måste beräknas utifrån inköpsfrekvensmodeller som omkalibreras dynamiskt - händelseutlösta meddelanden kan inte hantera prediktiva schemaläggnings- eller tidsjusteringar när kunderna beställer om tidigt eller sent.

### Tekniska överväganden

- Beräkningen av inköpsfrekvensen måste ta hänsyn till olika förbrukningsfrekvenser för olika produktkategorier. En påminnelse om kaffe bör komma på en annan plats än en för rengöring av leveranserna.
- Resan bör justera sin timing dynamiskt när en kund beställer tidigare eller senare än förväntat, vilket omkalibrerar nästa påminnelse baserat på uppdaterade inköpsdata.
- Påminnelser ska innehålla en direktbeställningslänk eller ett återköpsalternativ med ett klick för att minimera friktionen och maximera konverteringen från meddelandet.
- Kunder som redan har ombeställt via en annan kanal (i butik, prenumerationstjänst) måste ignoreras för att undvika att skicka irrelevanta påminnelser.


## Personaliserade kategorisidor

Anpassa kategorisidor dynamiskt för att visa de mest relevanta produkterna först baserat på varje kunds önskemål, tidigare köp och webbläsarbeteende. När kunderna ser produkter som är anpassade efter sina smak överst på sidan upptäcker de vad de vill ha snabbare och konverterar till högre priser.

### Affärspåverkan

Personaliserade kategorisidor ökar engagemanget och förbättrar produktupptäckt avsevärt, särskilt för detaljhandlare med stora kataloger.

### Implementera

Använd mönstret [Beteenderekommendation](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md). Den här metoden använder urvalsstrategier och rangordningsmodeller för att ordna om produkter på kategorisidor baserat på varje besökares profil och beteende i realtid. Det här är det rätta mönstret när aktiviteten rankas i en stor, öppen produktuppsättning med beteendesignaler - beslut om erbjudanden passar inte här eftersom det inte finns några regler för behörighet eller affärsbegränsningar som begränsar vilka produkter som visas.

### Tekniska överväganden

- Produktrankningen måste utföras tillräckligt snabbt för att undvika upplevda sidladdningsladdningar. Serveranpassning eller kantbaserad beslutsfattande krävs ofta för kategorisidor med hundratals produkter.
- Anpassningslogiken bör kombinera individuella preferenser med försäljningsregler, vilket säkerställer att marknadsförda produkter, nya produkter och säsongsobjekt fortfarande får lämplig synlighet.
- En infrastruktur för A/B-testning bör finnas på plats för att kontinuerligt mäta intäktseffekten av personaliserad sortering jämfört med standardregler för försäljning.
- [!DNL Experience Platform] Webbimplementeringen av SDK måste fånga upp sidinteraktioner i kategorin (rullningsdjup, produktklick, filteranvändning) för att kontinuerligt förfina rangordningsmodellerna.


## Uppföljningskampanjer efter inköp

Skicka e-postmeddelanden efter köp med tips om produkter, produktförslag, granskningsbegäranden och information om lojalitetsprogram. Perioden direkt efter ett köp är när kunderna är mest engagerade i varumärket, vilket gör det till ett idealiskt fönster för att fördjupa relationen och uppmuntra till framtida aktiviteter.

### Affärspåverkan

Effektiva kampanjer efter köp ökar granskningens överföringshastighet och ökar antalet återkommande inköp, vilket gör att engångsköpare blir lojala kunder.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg. I det här flerstegsflödet används förgreningslogik för att skräddarsy uppföljningsmeddelanden baserat på produkttyp, kundsegment och engagemang med tidigare e-postmeddelanden i serien. Detta är det rätta mönstret eftersom uppföljningen sträcker sig över flera dagar, är beroende av händelser för leveransstatus och grenar baserade på produktkategori och returhändelser - ett enda utlöst meddelande kan inte stödja den villkorliga logik som krävs på hela tidslinjen efter köpet.

### Tekniska överväganden

- Resan måste ta hänsyn till orderstatus. Tips och förfrågningar ska skickas först när produkten har levererats, inte omedelbart efter köpet.
- Produktspecifikt innehåll (behandlingsanvisningar, användningsguider, förslag på tillbehör) kräver ett innehållsmappningssystem som associerar varje produktkategori med relevant uppföljningsmaterial.
- Tidpunkten för begäran om översyn bör optimeras baserat på produktkategorin. Elektronik kan behöva en längre användningsperiod innan en meningsfull granskning kan ses över kort efter leveransen.
- Kunder som initierar en retur eller ett utbyte ska automatiskt tas bort från standardflödet efter köp och omdirigeras till en serviceåterställningsväg.


## VIP exklusiva erbjudanden

Identifiera värdefulla kunder och leverera exklusiva erbjudanden, tidig tillgång till försäljning och personaliserade shoppingupplevelser som belönar deras lojalitet. Att behålla kunder i toppskiktet är mycket mer kostnadseffektivt än att skaffa nya, och exklusiv behandling stärker den känslomässiga koppling som håller dem spenderade.

### Affärspåverkan

VIP-program genererar ett starkt engagemang från kunder i toppskiktet och förbättrar på ett mätbart sätt kundens livstidsvärde genom att minska bortfallet bland de mest lönsamma segmenten.

### Implementera

Använd mönstret [Flerkanalsresa med beslut](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md). Detta tillvägagångssätt kombinerar resesamordning med beslut i realtid för att välja erbjudande, vilket säkerställer att alla VIP-kunder får det mest relevanta exklusiva erbjudandet i alla kanaler. Det här är det rätta mönstret när resan måste koordinera leveransen över flera kanaler för att förhindra dubblerade erbjudanden och när valet av erbjudanden kräver regler för behörighet och affärsbegränsningar - flerstegssamordning ger inte ensam det realtidslager som behövs för att styra vilket exklusivt erbjudande varje VIP får.

### Tekniska överväganden

- VIP:s kriterier för segmentering måste vara tydligt definierade med hjälp av statistik om aktuell tid, frekvens och penningvärde, och segmenten bör uppdateras tillräckligt ofta för att fånga upp kunder som nyligen har kvalificerat sig eller diskvalificerats.
- Exklusiva erbjudanden måste verkställas vid inlösen (webb, app, butik) för att förhindra att kunder utanför VIP får tillgång till dem, vilket kräver integrering med kampanjsystem och prissättningssystem.
- Kanalinställningarna varierar avsevärt bland värdefulla kunder, vissa föredrar e-post, andra svarar på appmeddelanden eller direktreklam, så resan bör anpassa leveranskanalerna baserat på tidigare engagemang.
- [!DNL Journey Optimizer]-beslut måste koordineras över alla kanaler för att förhindra att en VIP-kund får samma erbjudande via e-post, push och SMS samtidigt.


## Aviseringar utanför lagret

Låt kunderna registrera sig för meddelanden när färdiga produkter blir tillgängliga och meddela dem sedan automatiskt via e-post eller SMS. Genom att hämta efterfrågan på produkter som inte finns tillgängliga förhindrar du förlorad försäljning och ger kunderna en anledning att återvända till butiken i stället för att köpa från en konkurrent.

### Affärspåverkan

Aviseringar som skickas tillbaka i lager når upp till en hög konverteringsgrad bland abonnenterna och minskar på ett betydande sätt försäljningen av efterfrågade produkter som har tillfälliga lager.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md). Den här metoden utlöser meddelanden om lagerbaserade händelser och matchar lageruppdateringar mot kundmeddelanden för att leverera aviseringar i rätt tid. Det här är det rätta mönstret eftersom utlösaren är en diskret inventeringssystemhändelse, leveransen är tidskritisk (lagret kan gå snabbt att sälja ut igen) och kommunikationen är ett enda meddelande i stället för en pågående resa.

### Tekniska överväganden

- Inventeringsövervakningen måste snabbt upptäcka nya låshändelser. Om du dröjer några timmar kan produkten gå ut igen innan de anmälda kunderna har chansen att köpa.
- När en populär produkt återställs i en begränsad mängd bör meddelandena fördelas eller prioriteras efter registreringsdatum för att undvika att skicka varningar till fler kunder än vad som finns i det tillgängliga lagret.
- Anmälningsmekanismen måste fånga upp kanalinställningarna (e-post eller SMS) och uppfylla anmälningskraven för varje kanal, särskilt för SMS.
- Profilattributen för [!DNL Real-Time Customer Data Platform] ska spåra vilka produkter varje kund tittar på så att dubblettmeddelanden förhindras om samma produkt återställs flera gånger.


## Korrektur för sociala medier - Personalization

Visa personliga sociala bevis, inklusive recensioner, omdömen och förslag om&quot;kunder som köpt det här också&quot;, baserat på varje kunds profil och önskemål. Skräddarsy sociala bevis för att reflektera upplevelserna hos liknande kunder bygger förtroende effektivare än enbart generiska betyg.

### Affärspåverkan

Personaliserade sociala bevis ökar konverteringsgraden och ökar kundens förtroende, särskilt för förstagångsköpare och högprisprodukter där köpvanheten är störst.

### Implementera

Använd mönstret [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md). Det här arbetssättet personaliserar webbinnehåll för identifierade besökare och väljer de mest relevanta granskningarna och elementen för socialt korrektur baserat på kundens profil, önskemål och surfningssammanhang. Det här är det rätta mönstret när personalisering styrs av profilattribut och segmentmedlemskap i stället för en beteendetillhörighetsmodell - beteenderekommendation passar inte här eftersom val av socialt korrektur beror på vem kunden är, inte på vilka objekt de har bläddrat.

### Tekniska överväganden

- Gransknings- och värderingsdata måste struktureras och taggas utifrån kundattribut (t.ex. köpkontext, kundsegment och produktanvändningsfall) för att möjliggöra meningsfull filtrering och personalisering.
- Sociala korrekturrundselement bör läsas in asynkront för att undvika att huvudproduktsidans rendering blockeras, eftersom granskningsdata kan komma från en tredjepartsgranskningsplattform med varierande svarstider.
- Sekretessreglerna kräver att alla kunddata som används för att matcha granskningar mot besökare hanteras enligt medgivandepreferenser. Att visa&quot;kunder som du&quot;-innehåll innebär profilering som kan kräva utlämnande.
- [!DNL Experience Platform]-målgruppsmedlemskap kan användas för att välja vilka recensioner som ska markeras och visa utomhusentusiaster recensioner från utomhusshoppare i stället för generiska topprankade recensioner.


## AI Product Advisor

Onlinebutikerna har tusentals SKU:er i komplexa kategorihierarkier, vilket gör det svårt för kunderna att hitta rätt produkt utan utökad surfning eller övergivna sökningar. En AI-driven produktrådgivare engagerar kunderna i en naturlig flerkanalsdialog - där man ställer frågor om behov, preferenser och budget - och sedan begränsar urvalet till en välstrukturerad uppsättning personaliserade rekommendationer. Upplevelsen speglar den vägledning som ett kunnigt butikstjänstemän skulle ge, levererad i digital skala.

### Affärspåverkan

Handlare som använder guidad konversationsidentifiering kan se förbättrade konverteringsgrader och genomsnittligt ordervärde jämfört med oövervakad surfning, samtidigt som de minskar produktavkastningen genom bättre underbyggda inköpsbeslut.

### Implementera

Använd mönstret [Brand Concierge Conversational Experience](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md). Med den här metoden används Product Advisor Agent mot en strukturerad produktkatalog och AEP Agent Orchestrator och kundprofildata i realtid används för att generera varumärkessäkra, personaliserade produktrekommendationer genom naturlig dialog. Det här är det rätta mönstret när målet är interaktiv konversationsidentifiering i flera omgångar som styrs av kundens angivna behov - skilt från händelseutlösta meddelanden, som är enkelriktade och reaktiva till en viss åtgärd, och från personaliserade webbupplevelser, som visar rekommendationer passivt snarare än att engagera kunderna i konversationer. Det kräver AEP Agent Orchestrator och varumärkesstyrningskonfiguration.

### Tekniska överväganden

- Produktkatalogen måste struktureras med omfattande attributdata - inklusive storlek, material, kompatibilitet, tillgänglighet och priser - eftersom Product Advisor Agent anser att det finns rekommendationer i kataloginnehållet och inte på ett tillförlitligt sätt kan ge råd om produkter med ofullständiga attribut.
- Kundprofilsökning i realtid via RT-CDP måste konfigureras med edge-aktivering så att inköpshistorik, surfbeteende och lojalitetsnivådata är tillgängliga under live-konversationen utan fördröjning som skulle störa upplevelsen.
- Garantier för varumärkesstyrning måste definieras för att specificera hur agenten hanterar artiklar som inte finns i lager, konkurrensutsatta produktjämförelser, kampanjpriser och förbjudna ämnen, så att alla åtgärder överensstämmer med varumärkesstandarder för detaljhandeln.
- Konversationshändelser - inklusive avsiktssignaler, produktinteraktioner och rekommendationer - måste samlas in som XDM Experience Events och strömmas tillbaka till AEP, vilket berikar kundprofiler med produkttillhörighetsdata som förbättrar den framtida personaliseringen i alla kanaler.


## Analys av flerkanalsattribuering

Mät hur varje kontaktyta för marknadsföring - betalsökningar, e-post, sociala kampanjer och butikskampanjer - bidrar till köpkonverteringar online och offline. Återförsäljare som förlitar sig på sista-beröringen-attribuering undervärderar systematiskt de övre funnel-kanalerna och fattar beslut om budgetallokering baserat på en ofullständig bild av köpbanan.

### Affärspåverkan

Marknadsföringsteam inom detaljhandeln som går från sista-beröringen till flerberöringsattribuering får en tydligare bild av vilka kanaler som driver inköpsavsikten, vilket leder till bättre underbyggda budgetbeslut och förbättrad avkastning på marknadsföringsutgifter.

### Implementera

Använd mönstret [Kundanalys och insiktsgenerering](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md). Detta tillvägagångssätt kopplar samman händelsedata online och offline - webbklickningar, e-postärenden, lojalitetstransaktioner och butiksposter - med Customer Journey Analytics, där attribueringsmodeller kan konfigureras och jämföras över hela inköpsvägen. Detta är det rätta mönstret när målet är att mäta och generera insikter över en komplex flerkanalsresa - i stället för att aktivera målgrupper eller utlösa budskap - och när analysen kräver Customer Journey Analytics snarare än ett CDP- eller kampanjverktyg.

### Tekniska överväganden

- Transaktionsdata för butiker och e-handel måste dela en enhetlig kundidentifierare så att konverteringar i butiker och online kan sammanfogas till en enda flerkanalsvy i CJA.
- Flera attribueringsmodeller - first-touch, last-touch, linear och time-decay - bör konfigureras i CJA datavy så att analytiker kan jämföra dem sida vid sida utan att behöva bygga om analysen.
- Betalda mediemått och klickdata från externa annonsplattformar måste hämtas via källanslutningar eller batchöverföringar för att de betalda kanalerna ska ingå i attribueringsvägen bredvid ägda kanaler.
- Konverteringsfönster och kreditsökningsperioder måste definieras per kanaltyp, eftersom det relevanta attribueringsfönstret för ett betalt sökklick skiljer sig avsevärt från det för en säsongsbunden e-postkampanj.

## Målgruppssegmentering och -aktivering för betalmedia

Bygg värdefulla målgruppssegment från enhetliga kundprofiler och aktivera dem för betalmediematerial som Google Ads, Meta och The Trade Desk för förvärv och återannonsering av kampanjer. Enhetliga beteendedata, transaktionsdata och lojalitetsdata ger en mer exakt målgruppsanpassning som minskar bortslösade annonskostnader och förbättrar avkastningen på investeringen i kampanjer.

### Affärspåverkan

Återförsäljare som aktiverar förstahandsmålgrupper av hög kvalitet ser förbättrade matchningsfrekvenser på betalda medieplattformar, minskad kostnad per förvärv och större avkastning på annonskostnaderna jämfört med att förlita sig på tredjepartssegment.

### Implementera

Använd mönstret [Audience Activation till destinationer](/help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md) för att utvärdera målgruppsmedlemskap mot enhetliga profiler och publicera segment till anslutna betalda mediemål på schemalagd eller direktuppspelad basis. Detta är det rätta mönstret när det primära kravet är segmentpublicering till externa system snarare än samordnade meddelanden eller realtidsbeslut.

### Tekniska överväganden

- Identitetsupplösning för webben, mobiler och lojalitetsdata krävs för att skapa fullständiga kundprofiler innan aktivering - fragmenterade profiler minskar målgruppernas kvalitet och matchar.
- Målanslutningarna måste konfigureras för varje betald mediaplattform, med lämpliga godkännandeflaggor på profilnivå för att förhindra att icke-godkända data aktiveras.
- Frekvensen för uppdatering av segment bör vara anpassad till kampanjmålen - målgrupper som förvärvar kan behöva dagliga uppdateringar samtidigt som målgrupperna kan dra nytta av uppdateringar i nära realtid för att utesluta nya köpare.
- Överlappningsanalys mellan olika målgrupper inom kundförvärv och kundlojalitet bidrar till att förhindra korskontaminering där befintliga kunder får meddelanden om kundvärvning.


## Inaktivering av kunder för värvningskampanjer

Förhindra befintliga kunder och nya konverterare från att köpa in annonser genom att aktivera exkluderingsmålgrupper till betalda mediematerial, vilket minskar bortslösade utgifter. Kontinuerlig synkronisering av undertryckningslistor säkerställer att betalda budgetar avser nya nettokunder i stället för personer som redan har konverterat eller aktivt engagerat sig.

### Affärspåverkan

Genom att hindra befintliga kunder från att värva upp kampanjer minskar ni bortslösade utgifter för betalda medier, förbättrar kostnaden per kundvärvning och förhindrar befintliga kunder från att ta emot meddelanden som inte är relevanta för deras relationsfas.

### Implementera

Använd mönstret [Audience Activation till destinationer](/help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md) för att publicera exkluderingsmålgrupper - senaste köpare, aktiva prenumeranter och värdefulla kunder - för varje betald mediemål enligt ett ofta återkommande schema. Detta är det rätta mönstret när målet är segmentpublicering för att undertrycka snarare än att skapa en kundinriktad resa.

### Tekniska överväganden

- De som inte vill visa bilder måste ha en tydlig definition av vem de ska utesluta - vanligtvis kunder som har köpt under de senaste 30-90 dagarna, aktiva lojalitetsmedlemmar och nyligen använda e-postkonverteringar.
- Uteslutningslistorna måste uppdateras tillräckligt ofta för att utesluta köpare innan annonserna kan användas. Inaktuella undertryckningslistor orsakar den största varumärkesfriktionen i butiksperioder med stora volymer.
- Identitetsmatchningskvaliteten påverkar direkt dämpningskvaliteten - dålig matchning av e-post eller enhets-ID resulterar i att befintliga kunder fortfarande ser kundvärvningsannonser.
- Se till att de som inte tar emot kampanjer är åtskilda från målgrupperna som vill behålla dem, så att ni kan nå kunder som inte ska hindras.


## Personaliserade webbupplevelser för kända besökare

Leverera personaliserade hjältebanners, produktrekommendationer och marknadsföringsmaterial till autentiserade webbplatsbesökare baserat på deras realtidsprofil, segmentmedlemskap och beteendehistorik. När återkommande kunder ser upplevelser som är skräddarsydda efter deras lojalitetsstatus, inköpshistorik och preferenser, blir engagemangsfrekvensen och konverteringsgraden avsevärt bättre jämfört med generiska hemsidor.

### Affärspåverkan

Återförsäljare som personaliserar för kända besökare ser meningsfulla förbättringar i engagemangsmått, inklusive tid på plats, sidor per session och konverteringsgrad, med störst påverkan bland lojalitetsmedlemmar som besöker ofta.

### Implementera

Använd mönstret [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) för att leverera profilstyrda personaliserade upplevelser vid sidinläsning med segmentmedlemskap i realtid och profilattribut. Detta är det rätta mönstret när upplevelsen måste styras av identitetslänkade profildata snarare än sessionssignaler - och när innehållsbeslut inte kräver komplex rangordning av erbjudanden eller affärsbegränsningar.

### Tekniska överväganden

- Autentisering måste ske innan profildriven personalisering kan aktiveras. Webbplatsen behöver en mekanism för att identifiera besökaren och matcha deras ECID mot en känd profil.
- Profilsökningar i realtid måste slutföras inom sidans budget för tidsfördröjning av inläsning, vilket normalt kräver profilutvärdering som distribueras av edge, i stället för API-anrop på serversidan för den kritiska återgivningssökvägen.
- Innehållsvariationer måste utformas för alla målgruppssegment som ska anpassas, inklusive en standardupplevelse för besökare som inte matchar någon personaliseringsregel.
- Personalization-beslut bör loggas för analys, vilket möjliggör A/B-testning av innehållsvariationer och attribuering av engagemangsförbättringar för specifika segment.


## Anonym besökare på Personalization

Anpassa innehåll för oidentifierade webbplatsbesökare med hjälp av sessionsbeteendesignaler som visade sidor, bläddrade produktkategorier och hänvisningskälla. Eftersom merparten av webbtrafiken inom detaljhandeln är anonym, utökar personaliseringen av okända besökare avsevärt räckvidden för webbplatspersonaliseringen utanför det autentiserade segmentet.

### Affärspåverkan

Återförsäljare som levererar personaliserade upplevelser till anonyma besökare ser bättre engagemang och konverteringsgrader för första besök, med särskilt stor påverkan på besökare som kommer från specifika kampanjkällor eller som surfar på kategorisidor med hög återgivning.

### Implementera

Använd mönstret [Anonym besökswebb-Personalization](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md) för att utvärdera sessionsbeteendesignaler i kanten och leverera relevanta innehållsvariationer utan att någon autentisering krävs. Detta är det rätta mönstret när personalisering måste fungera direkt från den första interaktionen utan att förlita sig på en beständig profil - särskilt för kundvärvstrafik och besökare som ännu inte har loggat in.

### Tekniska överväganden

- Sessionspersonalisering bygger på strömmande händelsedata som samlas in via Edge Network; kantutvärderingsreglerna måste distribueras och testas innan trafik skickas till dem.
- Innehållsvariationer bör utformas kring beteenden med hög signal under sessioner - hänvisningskälla, första sidan ska visas, produktkategori utforskas - istället för lågsignalsattribut som inte förutsäger avsikten på ett tillförlitligt sätt.
- Kraven på integritetsskydd måste utvärderas noggrant. I vissa jurisdiktioner behandlas beteendeanpassning som krav på samtycke även för anonyma besökare.
- Personalization regler för anonyma besökare bör vara enklare och snabbare att utvärdera än kända besökarregler, eftersom begränsningar för gränslatens är strängare.


## Welcome Series Journey

Samordna en välkomstresa i flera steg för nyregistrerade kunder och leverera introduktionsinnehåll, produktutbildning och ett första inköp i e-postkanaler och push-kanaler. En väldesignad välkomstserie sätter tonen för kundrelationen och ökar sannolikheten för att en ny registrant ska gå över till sitt första inköp avsevärt.

### Affärspåverkan

Välkomstserieprogram ger meningsfulla förbättringar av kundaktiveringstakten och konverteringsgraden vid första köpet, med störst effekt när serien kombinerar utbildningsinnehåll med ett vältajmat, personaliserat incitament.

### Implementera

Använd mönstret [Multi-Step Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) för att utforma en introduktionssekvens för flera dagar med väntesteg, kanalförgrening baserad på engagemang och nedtryckning när det första inköpsmålet har uppnåtts. Detta är det rätta mönstret när användningsfallet kräver ett sekventiellt, tidsfördelat kommunikationsflöde med villkorslogik - ett enda meddelande som utlöses är inte tillräckligt för att vägleda en ny kund genom introduktionsupplevelsen.

### Tekniska överväganden

- Reseposten bör aktiveras av kontoregistreringshändelser i realtid så att det första välkomstmeddelandet kommer så fort registreringsavsikten är hög.
- Resan måste innehålla avslutningsvillkor som utesluter återstående meddelanden när en ny kund slutför sitt första köp - att fortsätta välkomstserien efter köpet undergräver meddelandets relevans.
- Kanalinställningarna måste gälla överallt. Steg för push-meddelanden kräver att du installerar appen och anmäler dig till tjänsten, med e-postreservlösningar för kunder utan att anmäla dig.
- Personalization i välkomstserien förbättrar konverteringen men kräver tillräckligt med profildata för att vara meningsfulla - nya profiler behöver ofta en reserv till bestsäljare eller trendprodukter.


## Återställning av kundvagnsavbrott

Trigga e-post i realtid och push-meddelanden när en kund överger sin kundvagn, med personaliserade produktpåminnelser och tidsbegränsade incitament för att slutföra köpet. Att kunden överger sina intäkter är ett av de mest lönsamma användningsområdena inom detaljhandeln, och återfår intäkterna från kunder som redan har visat god inköpsvilja.

### Affärspåverkan

Välgenomförda program för övergivna varukorgar återvinner en meningsfull andel av övergivna intäkter, med högsta återvinningsgrad när det första meddelandet kommer inom en timme efter överlämnandet och inkluderar de exakta artiklarna som återstår i kundvagnen.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) för att svara på händelsen att kundvagnen överges med en omedelbart utlöst kommunikation medan inköpsmetoden fortfarande är aktiv. Det här är det rätta mönstret när en diskret kundåtgärd är utlösaren och det primära kravet är ett personaliserat svar i rätt tid - snarare än en flerveckorsbevakning eller komplexa anbudsbeslut med begränsade affärsmöjligheter.

### Tekniska överväganden

- Identifiering av avbruten kundvagn kräver ett definierat inaktivitetströskelvärde (vanligtvis 30-60 minuter) för att undvika att skicka meddelanden till kunder som fortfarande aktivt bläddrar eller slutför utcheckningsflödet.
- E-postinnehåll måste dynamiskt återge aktuella produktbilder, priser och lagerstatus när de skickas, eftersom artiklar kan sälja ut eller ändra priset mellan nedläggning och meddelandeleverans.
- Undertryckningslogiken måste utesluta kunder som slutfört sitt köp via en annan kanal mellan avhoppsidentifiering och meddelandeutskick.
- Regler för frekvensbegränsning bör förhindra att upprepade kundvagnsövergivna meddelanden visas i korta fönster, särskilt för kunder som vanligtvis överger kundvagnar som surfbeteende.


## Deltagande efter inköp

Leverera postinköpsmeddelanden som orderbekräftelse, leveransuppdateringar, korsförsäljningsrekommendationer och granskningsbegäranden via en samordnad flerstegsresa. Fönstret efter köpet är en av de mest engagerande ögonblicken i kundens livscykel, vilket gör det till ett idealiskt tillfälle att skapa lojalitet och introducera relevanta kompletterande produkter.

### Affärspåverkan

Återförsäljare med strukturerade kundresor kan se förbättrade återköpsfrekvenser och färre kundgranskningar, vilket bidrar till både långsiktig lojalitet och sociala bevis som stöder framtida förvärv.

### Implementera

Använd mönstret [Flerstegsdirigerad resa](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) om du vill orkestrera en sekvens av postköpskommunikation som är tidsbestämd till viktiga milstolpar: orderbekräftelse, leverans, leverans och uppföljning efter leverans. Detta är det rätta mönstret när användningsfallet sträcker sig över flera dagar med flera mål - ett enda utlöst meddelande kan inte rymma bågen från transaktionsbekräftelse till lojalitetsskapande till granskningsbegäran.

### Tekniska överväganden

- Integrering av orderhanteringssystem krävs för att kunna ta emot köp- och leveranshändelser i realtid; förseningar i händelse av förtäring skapar besvärlig timing i kommunikation efter inköp.
- Korsförsäljningsrekommendationer i sekvensen efter inköp kräver realtidsdata i produktkatalogen och rekommendationsmodellslutsatser vid meddelandeåtergivningstiden för att återspegla aktuellt lager och aktuella priser.
- Meddelanden om förfrågningar måste uppfylla plattformens användarvillkor för att ge incitament till granskningar och bör skickas när kunden har haft tillräckligt med tid för att använda produkten.
- Kanalsamordning är viktigt - kunderna bör inte få både e-post och push för samma milstolpe om de inte har engagerat sig i den första kanalen.


## Uppgraderingskampanj för bonusnivå

Identifiera kunder som närmar sig lojalitetströskeln och leverera målinriktade kampanjer som uppmuntrar dem att nå nästa nivå med personaliserade erbjudanden baserade på inköpshistorik och önskemål. När kunderna är inom räckhåll för en nivåuppgradering skapar riktade meddelanden med personaliserade incitament ett trängande behov och driver på inkrementellt köpbeteende.

### Affärspåverkan

Uppgraderingskampanjer på bonusnivå driver på den stegvisa inköpsvolymen och förbättrar programmets engagemang, med störst effekt bland medlemmar i mellanskiktet som ligger nära nästa tröskelvärde och har visat upp den senaste köpaktiviteten.

### Implementera

Använd mönstret [Multi-Step Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) för att skapa en nivånärhetskampanj som kommer in i kunderna när de når en definierad utgiftsgräns under nästa nivå och guidar dem genom en sekvens av förmånsmeddelanden och bonuserbjudanden. Detta är det rätta mönstret när användningsfallet kräver övervakning av ett beräknat profilattribut över tiden och samordning av en flerstegskampanj som är kopplad till kundens framsteg mot ett mål.

### Tekniska överväganden

- Uppgifter om lojalitetsplattformen - poängbalans, nivåstatus, nivåtröskelvärden - måste hämtas in och hållas aktuella i kundprofilen så att nivånärhetsberäkningarna blir korrekta.
- Uppgraderingskampanjer på nivån ska inte visas för kunder som redan har uppnått målnivån eller vars lojalitetsstatus har ändrats sedan kampanjen introducerades.
- Personaliserade incitament i uppgraderingskampanjen bör begränsas till erbjudanden som kunden verkligen är berättigad till och som inte undergräver det upplevda värdet av nivåstrukturen.
- Kampanjen måste innehålla tydliga avslutningsvillkor för kunder som slutför uppgraderingen av skiktet mitt i kundresan, pivotera till ett gratulationsmeddelande istället för att fortsätta med övertalningssekvensen.


## Samlad flerkanalsmarknadsföring

Samordna samordnade marknadsföringskampanjer i e-post-, SMS-, push- och webbkanaler med förgreningar av resan, väntesteg och frekvensbegränsning för att maximera engagemanget utan trötthet. Samordnad flerkanalssamordning säkerställer att kunderna får en sammanhängande kampanjupplevelse oavsett vilken kanal de först svarar på, vilket eliminerar dubblettmeddelanden och motstridiga erbjudanden.

### Affärspåverkan

Återförsäljare med funktioner för flerkanalsmarknadsföring ser ett högre kampanjengagemang och större konverteringsgrader än kampanjer i en enda kanal, samtidigt som de minskar avabonnemangsfrekvensen på grund av kanalutmattning på grund av osamordnade meddelanden.

### Implementera

Använd mönstret [Flerkanalsresa med Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) för att skapa kampanjer som dirigerar kunder via personaliserade kanalsekvenser baserat på deras interaktionshistorik, kanalpreferenser och realtidssvarssignaler. Det här är det rätta mönstret när kampanjen kräver styrt urval av erbjudanden, kanalpreferenser och dynamisk förgrening baserat på engagemanget under resan - i stället för en fast sekvens som skickas till alla kampanjmottagare.

### Tekniska överväganden

- Globala frekvenshål måste konfigureras över alla kanaler för att förhindra att kunderna får för mycket information när flera resor körs samtidigt.
- Kanalinställningsdata måste vara aktuella och användbara - inställningsprofiler som är månader inaktuella dirigerar kunder till kanaler som de inte längre interagerar med.
- Resehanteringslogiken bör hantera återinträde på ett smidigt sätt, så att kunderna inte kan gå in i samma kampanj två gånger samtidigt som de inte utesluts från verkligt nya kampanjer.
- Realtidsengagemangssignaler (e-post öppnas, länkklick, webbsessioner) bör flöda tillbaka till resan för att möjliggöra kanalbyte och tidig avslutning för kunder som redan har konverterat.


## Brand Concierge Conversational Experience

Driftsätt en AI-driven, varumärkessäker konverteringsagent för digitala resurser för att ge personlig produktvägledning, hjälp med webbplatsnavigering och smidig leverans till aktiva agenter. En AI-konversation på plats utökar den personaliserade tjänsten i stor skala, vilket hjälper kunderna att hitta produkter, jämföra alternativ och slutföra köp utan att de behöver hjälp av handläggare för vanliga frågor.

### Affärspåverkan

Återförsäljare med AI-konverteringsfunktioner rapporterar om förbättrad självbetjäningsupplösning, minskad inkommande supportvolym för produkt- och navigeringsfrågor samt högre konverteringsgrad bland kunder som interagerar med konversationsvägledning före köp.

### Implementera

Använd mönstret [Brand Concierge Conversational Experience](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md) för att distribuera en styrd AI-agent som är baserad på produktkatalogdata, varumärkesriktlinjer och kundprofilskontext i realtid. Det här är det rätta mönstret när användningsfallet kräver en naturlig språkinteraktion över en stor, dynamisk produktuppsättning - istället för en skriptad chattbot med fast avsikt eller ett mönster som matchar en viss kanal som e-post.

### Tekniska överväganden

- AI-agenten måste grunda sig på aktuella produktkatalogdata, inklusive beskrivningar, specifikationer, tillgänglighet och priser för att ge korrekt vägledning. Gamla produktdata leder till felaktiga rekommendationer.
- Garantier för varumärkessäkerhet måste konfigureras för att förhindra agenten från att diskutera konkurrentprodukter, göra prisåtaganden som står i konflikt med kampanjer eller svara på frågor utanför temat.
- Leveranslogik till live-agenter kräver integrering med tjänstplattformen och bör aktiveras när AI-agenten inte kan lösa kundens fråga efter ett definierat antal omgångar.
- Integrering av profildata gör det möjligt för agenten att anpassa svar baserat på inköpshistorik och lojalitetsstatus, men detta kräver att identitetsmatchningen slutförs innan konversationssessionen börjar.

## Påminnelse om incheckning med Appnedladdning CTA

Påminn gästerna om att checka in och uppmuntra dem att hämta appen för att enkelt få tillgång till information. Påminnelser i rätt tid i samband med appnedladdning plus uppmaningar om att öka mobilengagemanget och skapa mer engagerande upplevelser på plats.

### Affärspåverkan

Återförsäljare som kombinerar påminnelser om incheckning med appnedladdningsanrop kan se ökad appanvändning och större engagemang i butiken, eftersom kunder som använder mobilappen oftare interagerar med reklam och webbplatsinnehåll.

### Implementera

Använd mönstret [Event-Triggered Messaging](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) om du vill utlösa en påminnelse om incheckning med programnedladdning av CTA baserat på händelsens närvaro eller reservationsdata. Det här är det rätta mönstret när ett enda meddelande i rätt tid måste skickas som svar på en känd händelse eller en schemalagd utlösare.

### Tekniska överväganden

- Påminnelser om incheckning måste anges korrekt i förhållande till evenemanget eller besöksdatumet för att maximera engagemanget utan att uppfattas som för tidigt eller för sent.
- Djupa länkar för appnedladdning bör dirigera till rätt appbutik baserat på kundens enhetsplattform (iOS eller Android).
- Kunder som redan har installerat appen bör få en annan meddelandevariant som hoppar över nedladdningen av CTA och fokuserar på incheckningsfunktionen.

## Födelsedagskampanjer för fans

Rikta fansen på sin födelsedag med ett personligt födelsedagsmeddelande och ett exklusivt erbjudande. Födelsedagskampanjer skapar känslomässiga kopplingar med fans och driver inkrementella inköp genom personaliserad utåtriktad marknadsföring.

### Affärspåverkan

Födelsedagskampanjer ger genomgående en högre öppnings- och konverteringsgrad än genomsnittet eftersom de kommer i ett ögonblick av personlig betydelse, skapar mervärde och uppmuntrar fansen att behandla sig själva med ett specialköp.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) om du vill skicka ett personligt födelsedagmeddelande när kundens födelsedatum kommer. Det här är det rätta mönstret när ett enda händelsestyrt meddelande skickas baserat på en utlösare för profilattributsdatum.

### Tekniska överväganden

- Födelsedatum måste registreras i kundprofilen och valideras för att undvika att meddelanden skickas på felaktiga datum.
- Erbjudandena bör ha ett definierat giltighetsfönster (t.ex. födelseveckan) för att skapa ett trängande behov och samtidigt ge kunderna rimlig tid att lösa in.
- Fans utan födelsedag ska uteslutas från kampanjen i stället för att skicka ett generiskt meddelande.

## Födelsedagskampanjer för köpare

Rikta kunderna på deras födelsedag med ett personligt födelsedagsmeddelande och ett exklusivt erbjudande. Födelsedagskampanjer bygger varumärkeslojalitet genom att man erkänner kunderna personligen och uppmuntrar till ett prisvärt köp.

### Affärspåverkan

Personaliserade födelsedagserbjudanden genererar högre inlösenfrekvenser än generiska kampanjer eftersom de är anpassade efter ett ögonblick då kunderna redan är benägna att göra diskretionära inköp åt sig själva.

### Implementera

Använd mönstret [Event-Triggered Messaging](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) om du vill utlösa ett födelsedagsmeddelande och ett erbjudande baserat på köparens attribut för födelsedatumprofil. Det här är det rätta mönstret när ett personligt meddelande måste levereras på ett visst kalenderdatum som är knutet till kundprofilen.

### Tekniska överväganden

- Födelsedatum måste lagras som ett profilattribut och bör samlas in under registrering eller registrering av lojalitet.
- Erbjudandepersonalisering bör ta hänsyn till kundens inköpshistorik och preferenser för att presentera relevanta produktförslag tillsammans med födelsedagserbjudandet.
- Dubblett av undertryckningslogiken behövs för kunder som finns i flera system för att undvika att skicka flera födelsedagskalendern.

## Game Day Promotion Campaign

Rikta fansen mot att köpa biljetter till ett kommande spel med personaliserade kampanjer och erbjudanden. Game day-kampanjer driver försäljningen av biljetter genom att nå rätt målgrupp med aktuella, händelsespecifika meddelanden.

### Affärspåverkan

Målgruppsanpassade erbjudanden för speldagar förbättrar antalet biljettförsäljningspriser genom att nå fansen med relevanta erbjudanden baserat på deras teampreferenser, tidigare närvaro och närhet till platsen.

### Implementera

Använd mönstret [Batch Outbound Message Activation](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md) för att skicka kampanjmeddelanden till segmenterade fangrupper före kommande spel. Det här är det rätta mönstret när en grupp personaliserade meddelanden måste skickas till ett färdigbyggt målgruppssegment på schemalagd basis.

### Tekniska överväganden

- Spelschemadata måste integreras för att utlösa kampanjer vid rätt ledtid före varje händelse.
- Målgruppssegmentering bör ta hänsyn till teamets affinitet, geografiska närhet och tidigare närvaromönster för att maximera relevansen.
- Kunder som redan har köpt biljetter till det framhävda spelet bör inte få något kundförvärvsmeddelande och kan i stället få merförsäljningserbjudanden för uppgraderingar eller tillägg.

## Produktkampanjer

Rikta kunderna till att köpa produkter under en pågående produktkampanj. Kampanjkampanjer genererar intäkter genom att koppla samman rätt kunder med aktuella erbjudanden anpassade till aktiva kampanjer.

### Affärspåverkan

Målinriktade produktmarknadsföringskampanjer överträffar breda kampanjer genom att fokusera på de kunder som mest sannolikt konverterar, minska mängden marknadsföringsslöseri och förbättra avkastningen på marknadsföringsbudgeten.

### Implementera

Använd mönstret [Batch Outbound Message Activation](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md) för att skicka kampanjmeddelanden till kvalificerade målgruppssegment under aktiva kampanjfönster. Detta är det rätta mönstret när en schemalagd batch med personaliserade kampanjmeddelanden måste nå en viss målgrupp under en tidsbunden kampanj.

### Tekniska överväganden

- Start- och slutdatum för kampanjen måste hanteras för att säkerställa att meddelanden bara skickas under det aktiva erbjudandefönstret.
- Målgruppssegmenteringen bör utnyttja inköpshistorik, surfbeteende och produkttillhörighet för att nå målgrupper som är mest benägna att interagera med de produkter som marknadsförs.
- Frekvensbegränsning bör tillämpas för att förhindra reklamtrötthet, särskilt när flera kampanjer körs samtidigt.

## Kundvagnsöverge

Engagera kunder som överger kundvagnen på nytt med personliga påminnelser och incitament för att slutföra köpet. Återvinning av kundöverläggningar är ett av de mest lönsamma användningsområdena inom detaljhandeln.

### Affärspåverkan

Kampanjer för återfinnande av kundsegment återhämtar en meningsfull procentandel av de intäkter som annars gått förlorade genom att engagera kunderna på nytt i det ögonblick de hade störst inköpsavsikt med personaliserade påminnelser och incitament.

### Implementera

Använd mönstret [Event-Triggered Messaging](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) för att utlösa ett återställningsmeddelande när en händelse om att en kundvagn har övergivits identifieras. Det här är det rätta mönstret när ett enda meddelande i realtid måste skickas som svar på en beteendehändelse, till exempel att du lämnar objekt i kundvagnen utan att behöva slutföra utcheckningen.

### Tekniska överväganden

- Identifiering av avbruten kundvagn kräver ett definierat inaktivitetströskelvärde (vanligtvis 30-60 minuter) för att särskilja avbruten kundvagn från kunder som fortfarande surfar.
- Kundvagnsinnehållet måste skickas i händelsenyttolasten för att det ska gå att aktivera anpassade produktpåminnelser i återställningsmeddelandet.
- Kunder som slutför köpet mellan övergivningshändelsen och meddelandet måste ignoreras för att undvika irrelevanta meddelanden.
