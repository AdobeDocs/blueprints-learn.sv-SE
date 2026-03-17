---
title: Användningsexempel inom telekommunikation
description: Upptäck hur telekommunikationsorganisationer använder Adobe Experience Platform för att minska bortfall, få enhetsuppgraderingar och förbättra kundengagemanget.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '2295'
ht-degree: 1%

---


# Användningsexempel inom telekommunikation

Telekommunikationsorganisationer använder Adobe Experience Platform för att skapa en enhetlig bild av varje abonnent och leverera personaliserade upplevelser som minskar bortfallet, ökar planerings- och enhetsuppgraderingar och stärker långsiktiga kundrelationer. Genom att koppla samman data om nätverksanvändning, faktureringsinformation och kundinteraktioner kan telekomleverantörer förutse abonnenternas behov och engagera dem i rätt ögonblick via de kanaler de föredrar.

## Rekommendationer för enhetsuppgradering

Identifiera kunder som är berättigade till enhetsuppgraderingar och presentera personaliserade enhetsrekommendationer och uppgraderingserbjudanden baserat på användningsmönster och önskemål. Genom att analysera kontraktstidslinjer, enhetsålder och webbläsarbeteende kan telekomleverantörerna visa de mest relevanta enheterna och finansieringsalternativen för varje abonnent.

### Affärspåverkan

Organisationer som implementerar rekommendationer för enhetsuppgradering ser vanligtvis en 30-40-procentig ökning av konverteringsgraden genom att leverera rätt erbjudande vid rätt tidpunkt via den kanal kunden föredrar.

### Implementera

Använd mönstret [Cross-Channel Journey med Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) för att samordna uppgraderingsresor som utvärderar varje abonnents behörighet, enhetsinställningar och kanaltillhörighet för att leverera personaliserade uppgraderingserbjudanden via e-post, appmeddelanden och butiksupplevelser.

### Tekniska överväganden

- Integrera system för inventering och prissättning av enheter för att säkerställa att rekommendationerna återspeglar den aktuella tillgängligheten och kampanjpriserna.
- Koppla samman data från kontraktshantering för att exakt identifiera uppgraderingsberättigande fönster och tidiga uppgraderingserbjudanden.
- Införliva telemetri för enhetsanvändning (lagringskapacitet, batteriljud, prestandamått) för att förstärka rekommendationens relevans.
- Samordna med återförsäljar- och e-handelsplattformar för att upprätthålla en enhetlig uppgraderingsupplevelse i alla digitala kanaler och butikskanaler.


## Planoptimeringskampanjer

Analysera kundanvändningsmönster och rekommendera optimala ändringar av planen för att spara pengar eller få bättre funktioner baserat på deras faktiska behov. Proaktivt nå ut med planrekommendationer bygger upp förtroende och minskar risken för att prenumeranter lämnar företaget för konkurrenter med enklare priser.

### Affärspåverkan

Planoptimeringskampanjer ger normalt en 25-35-procentig ökning av antalet avtalsändringar, vilket ger nöjdare kunder och ökar även den genomsnittliga intäkten per användare när prenumeranterna går över till planer som bättre motsvarar deras förbrukning.

### Implementera

Använd mönstret [Multi-Step Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) för att skapa en multi-touch-kampanj som identifierar avvikelser mellan användning och plan, utbildar prenumeranter på bättre alternativ och guidar dem genom avtalsförändringsprocessen med aktuella uppföljningar.

### Tekniska överväganden

- Samla in realtids- och historiska användningsdata (röstminuter, dataförbrukning, internationella samtal) för att identifiera felaktiga planmatchningar.
- Koppla ihop faktureringssystemdata för att beräkna potentiella besparingar eller funktionsvinster för varje rekommenderad ändring av planen.
- Konto för kampanjprissättningsregler och avtalsförpliktelser när ni tar fram planrekommendationer.
- Integrera med självbetjäningsportaler så att prenumeranterna kan slutföra avtalsändringar direkt från kontaktytorna i kampanjen.


## Kravförebyggande för värdefulla kunder

Identifiera värdefulla kunder som riskerar att bli stulna och engagera dem med personaliserade kundlojalitetserbjudanden och proaktiv kundtjänst. Genom att kombinera beteendesignaler som minskad användning, upprepade servicebesök och konkurrenskraftig surfning med livstidsdata kan leverantörerna ingripa innan en prenumerant bestämmer sig för att gå ur.

### Affärspåverkan

Program för att förebygga kronor som riktar sig till värdefulla abonnenter brukar få en minskning på 20-30 %, vilket skyddar betydande återkommande intäkter och minskar kostnaderna för att skaffa nya kunder.

### Implementera

Använd mönstret [Cross-Channel Journey med Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) för att övervaka bortfallsrisksignaler i realtid, fastställa det bästa erbjudandet för kvarhållande för varje prenumerant och samordna personaliserad utåtriktad marknadsföring över digitala kanaler och callcenter.

### Tekniska överväganden

- Skapa poängvärden för kundens benägenhet genom att kombinera användartrender, interaktionshistorik för tjänster och känslomässig information från utskrifter från callcenter.
- Integrera call center och detaljhandelssystem så att handläggarna får insyn i de lojalitetserbjudanden som redan presenteras via digitala kanaler.
- Koppla samman konkurrensdata (portaförfrågningar, jämförelser av konkurrentplaner) för att förfina riskbedömningen och erbjuda strategier.
- Upprätta styrningsregler för att förhindra överkontakt med riskabonnenter, vilket kan snabba upp bortfallet snarare än förhindra det.


## Ny kundintroduktionsresa

Automatisera en personaliserad introduktionsresa för nya kunder med välkomstinformation, vägledning för kontokonfiguration och självstudiekurser. En strukturerad introduktionsupplevelse hjälper abonnenterna att snabbt upptäcka det fulla värdet av sin plan och sina tjänster och lägga grunden för långsiktig lojalitet.

### Affärspåverkan

Väldesignade introduktionsresor ökar normalt antalet aktiveringar av funktioner med 50-60 %, vilket leder till högre nöjdhetspoäng och lägre bortfall i förtid hos nya prenumeranter.

### Implementera

Använd mönstret [Multi-Step Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) för att skapa en sekventiell introduktionsupplevelse som anpassar sig utifrån varje abonnents plantyp, enhet och engagemang med föregående introduktionssteg.

### Tekniska överväganden

- Integrera system för kontoetablering för att utlösa introduktionsresan direkt efter aktiveringen och skräddarsy innehållet efter abonnentens specifika plan och enhet.
- Koppla samman appinteraktionsdata för att spåra vilka funktioner abonnenten har utforskat och justera efterföljande startmeddelanden därefter.
- Samordna med kundsupportplattformen för att se till att agenterna är medvetna om en abonnents introduktionsfas om de ringer in med frågor.
- Stöd för flera startvägar för olika kundsegment, t.ex. enskilda prenumeranter, administratörer av familjeplaner och företagskonton.


## Varningar och rekommendationer om dataanvändning

Skicka personaliserade aviseringar när kunderna närmar sig datagränserna och rekommendera planuppgraderingar eller datatillägg baserat på användningsmönster. Lämpliga meddelanden i rätt tid omvandlar en potentiellt frustrerande upplevelse till ett ögonblick av förtroendeskapande engagemang.

### Affärspåverkan

Aviseringar om proaktiv dataanvändning genererar vanligtvis en ökning på 40-50 % av inköpen av tillägg av data, samtidigt som de minskar antalet faktureringstötande klagomål och förbättrar kundnöjdheten.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) om du vill skicka realtidsaviseringar när användningströskeln överskrids, med personaliserade rekommendationer baserade på abonnentens historiska konsumtionsmönster och planinformation.

### Tekniska överväganden

- Anslut till dataflöden för nätverksanvändning som ger nästan realtidsuppdateringar av förbrukningen för att utlösa larm vid meningsfulla tröskelvärden (75 %, 90 %, 100 % av plangränserna).
- Integrera fakturerings- och planhanteringssystem för att presentera korrekta tilläggspriser och möjliggöra köp med ett klick direkt från varningsmeddelandet.
- Konto för delade datapoler för familjeplaner genom att meddela både den enskilda användaren och planadministratören.
- Implementera frekvensbegränsning för att undvika larm trötthet för abonnenter som konsekvent använder stora mängder data varje faktureringscykel.


## Meddelanden om serviceflöde

Meddela kunderna i förväg om avbrott i tjänsten, underhåll eller nätverksproblem i området med personaliserade uppdateringar och kompensationserbjudanden. Att nå ut innan kunderna upplever frustration visar på ansvar och minskar den inkommande supportvolymen avsevärt.

### Affärspåverkan

Proaktiva meddelanden om driftsavbrott ger normalt en bekräftelsefrekvens på 60-70 % och minskar avsevärt kundens volym vid avbrott i tjänsten, vilket minskar supportkostnaderna samtidigt som kundens uppfattning förbättras.

### Implementera

Använd mönstret [Event-Triggered Messaging](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) om du vill identifiera nätverkshändelser och omedelbart meddela berörda prenumeranter via de kanaler de föredrar med relevant information, beräknade lösningstider och lämplig kompensation när så är lämpligt.

### Tekniska överväganden

- Integrera med övervakningssystem i nätverkets ledningscentral för att ta emot data om driftstopp i realtid och underhållshändelser med geografisk omfångsinformation.
- Använd prenumerantens adress- och platsdata för att identifiera berörda kunder på ett korrekt sätt och undvika att meddela dem utanför det påverkade området.
- Anslut till fakturerings- och kreditsystemet för att automatisera serviceerbjudanden för längre avbrott baserat på prenumerantens plan och hur länge störningen varar.
- Koordinera meddelanden över alla kanaler för att tillhandahålla konsekventa statusuppdateringar och undvika att skicka information som står i konflikt när situationen förändras.


## Hantering av familjeplaner

Anpassa kommunikationen och erbjudandena för administratörer av familjeplaner baserat på användningsmönster och individuella medlemsbehov. Familjeplaner representerar konton med högt värde och flera rader, där engagemang med avtalsadministratören driver lojalitet på alla rader.

### Affärspåverkan

Kommunikation om anpassad hantering av familjeplaner ökar vanligtvis familjens engagemang med 30-40 %, vilket leder till högre radlojalitet och högre livstidsvärde per konto.

### Implementera

Använd mönstret [Flerkanalsresor med beslutande](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) om du vill analysera användningen för alla familjemedlemmar, identifiera möjligheter som att lägga till rader eller justera enskilda begränsningar och leverera anpassade rekommendationer till avtalsadministratören.

### Tekniska överväganden

- Modellera hierarkier för familjekonton för att skilja mellan avtalsadministratören och enskilda medlemmar, med hänsyn tagen till behörighetsnivåer för kommunikation och kontoändringar.
- Samla in användningsdata för alla rader på kontot för att identifiera mönster och möjligheter på familjenivå, t.ex. underutnyttjade delade data eller ojämna uppgraderingscykler.
- Integrera system för föräldrakontroll och innehållsfiltrering för att stödja familjespecifika funktioner i personalisering.
- Se till att sekretessregler finns på plats så att användningsinformation för enskilda medlemmar delas med avtalsadministratören baserat på kontobehörigheter.


## 5G uppgraderingskampanjer

Rikta er till kunder som är berättigade till 5G-nätverksuppgraderingar med personaliserade erbjudanden och fördelar baserat på deras plats och användningsmönster. När 5G-täckningen utökas kan abonnenterna på nyligen täckta områden med relevanta meddelanden få snabbare acceptans och ökad nätverksanvändning.

### Affärspåverkan

Riktade uppgraderingskampanjer för 5G ger en 25-35-procentig ökning av 5 G-acceptansnivån bland berättigade prenumeranter, vilket ger bättre avkastning på investeringar i nätverk och konkurrensfördelar.

### Implementera

Använd mönstret [Batch Outbound Message Activation](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md) för att segmentera prenumeranter baserat på 5G-täckning, enhetskompatibilitet och planbehörighet. Leverera sedan personaliserade uppgraderingskampanjer som visar de fördelar som är mest relevanta för varje prenumerations användningsprofil.

### Tekniska överväganden

- Integrera nätverkstäckningskartor för att exakt identifiera abonnenter i områden med aktiv 5G-tjänst och undvika att uppgradera där täckning ännu inte är tillgänglig.
- Koppla samman data om enhetskompatibilitet för att avgöra vilka prenumeranter som behöver en ny enhet jämfört med dem som redan har 5G-kompatibel maskinvara.
- Samordna med butikslagersystem för att säkerställa att de enheter och planer som marknadsförs är tillgängliga i den butik eller online som abonnenten föredrar.
- Segmentera meddelanden efter användningsprofil så att tunga dataanvändare får prestandainriktade fördelar samtidigt som tillfälliga användare får meddelanden om täckning och tillförlitlighet.


## Betalningspåminnelser för faktura

Skicka personliga påminnelser om fakturabetalning via önskade kanaler med betalningsalternativ och kontosaldoinformation. Lämpliga påminnelser i rätt tid minskar försenade betalningar och de därmed sammanhängande kostnaderna för att få in pengar samtidigt som kundrelationen förblir positiv.

### Affärspåverkan

Personaliserade påminnelser om fakturabetalning förbättrar vanligtvis betalningstakten i tid med 20-30 %, vilket minskar indrivningskostnaderna och minimerar antalet avbrott i tjänsten som ökar kundens missnöje.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) om du vill skicka påminnelser vid rätt tidpunkt före förfallodatumet, anpassade med abonnentens saldo, betalningsmetod och en direktlänk för att slutföra betalningen.

### Tekniska överväganden

- Integrera med faktureringsplattformen för att få tillgång till kontosaldon, förfallodatum och betalningshistorik i realtid för korrekt påminnelseinnehåll.
- Anslut till betalningssystem för att aktivera betalning med ett klick direkt från påminnelsemeddelandet.
- Implementera eskaleringslogik som justerar påminnelsens skyndsamhet och frekvens när förfallodatumet närmar sig, samtidigt som kommunikationsinställningarna respekteras.
- Stöd för flera betalningsmetoder (automatisk registrering av betalningar, digital plånbok, banköverföring) och anpassa de presenterade alternativen baserat på prenumerantens historik.


## Rekommendationer för tilläggstjänster

Rekommendera relevanta tilläggstjänster som enhetsförsäkring, molnlagring och strömningspaket baserat på kundens plan, användning och önskemål. Sammanhangsberoende rekommendationer ökar värdet för prenumeranterna som får in från sin relation med leverantören samtidigt som de får en ökad genomsnittlig intäkt per användare.

### Affärspåverkan

Personaliserade rekommendationer för tilläggstjänster genererar vanligtvis en ökning på 15-25 % av antalet tillägg, vilket ökar intäkterna från den befintliga prenumerationsbasen utan att kostnaden för nya kunder ökar.

### Implementera

Använd mönstret [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) för att utvärdera varje abonnents profil, aktuella tjänster och beteendesignaler för att fastställa det mest relevanta tilläggserbjudandet och presentera det via den optimala kanalen och ögonblicket.

### Tekniska överväganden

- Anslut till prenumerantens aktuella tjänstkatalog för att undvika att rekommendera tjänster som de redan har och för att identifiera naturliga komplement till deras befintliga plan.
- Integrera partner- och tredjepartstjänster (direktuppspelningsleverantörer, försäkringsbolag) för att presentera korrekta priser och paketerbjudanden.
- Använd enhets- och användningsdata för att informera om rekommendationer, som att föreslå enhetsförsäkring för prenumeranter med nya premiumenheter eller molnlagring för dem som har ont om enhetslagring.
- Koordinera med personalisering i appar och på webben för att förstärka rekommendationer om tillägg i självbetjäning.


## Personalization för nätverksprestanda

Anpassa information om nätverksprestanda och rekommendationer baserat på kundens plats, enhet och användningsmönster. Genom att hjälpa prenumeranterna att optimera sina anslutningsmöjligheter ökar förtroendet och minskar de supportkontakter som är kopplade till prestandaproblem.

### Affärspåverkan

Personaliserade nätverksprestandaupplevelser ökar vanligtvis appengagemanget med 35-45 %, eftersom prenumeranterna återgår till att kontrollera täckning, felsöka problem och hitta optimeringstips som är skräddarsydda efter deras situation.

### Implementera

Använd mönstret [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) för att leverera anpassade instrumentpaneler för nätverksprestanda, täckningsinformation och optimeringsrekommendationer i prenumerantens app- och webbkontoupplevelse.

### Tekniska överväganden

- Integrera mätvärden för nätverkskvalitet och täckning för att tillhandahålla platsspecifik prestandainformation som är relevant för abonnentens hemsida, arbete och besökta områden.
- Koppla samman diagnostikdata för enheter för att erbjuda skräddarsydda felsökningsrekommendationer baserat på prenumerantens specifika enhetsmodell och programvaruversion.
- Använd [!DNL Adobe Experience Platform]-kanttjänster för att leverera personalisering med låg latens i appupplevelsen utan att påverka prestanda.
- Implementera feedback-slingor så att prenumeranterna kan rapportera täckningsproblem och berika nätverksdata samtidigt som de visar hur lyhörda de är.


## Lojalitetsprogramengagemang

Anpassa kundens kundskikt, poängbalans och inlösenhistorik efter kundens kundrelationer. En välpersonaliserad lojalitetsupplevelse stärker den känslomässiga kopplingen till varumärket och skapar meningsfulla byteskostnader utöver avtalsvillkoren.

### Affärspåverkan

Personaliserat lojalitetsprogram ökar vanligtvis deltagandet i programmet och belönar inlösen med 30-40 %, vilket leder till högre lojalitetsgrad bland registrerade prenumeranter.

### Implementera

Använd mönstret [Cross-Channel Journey med Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) för att skapa personliga kundrelationer som framhäver relevanta belöningar, underrättar prenumeranter om hur skiktet utvecklas och presenterar möjligheter till inlösen i linje med deras preferenser och beteenden.

### Tekniska överväganden

- Integrera lojalitetsplattformen för att få tillgång till poäng i realtid, nivåstatus och inlösenhistorik för korrekt personalisering.
- Koppla ihop partnerbelöningskataloger för att presentera ett stort antal inlösenalternativ som är skräddarsydda efter varje abonnents uppvisade intressen och tidigare inlösen.
- Samordna lojalitetsmeddelanden med andra kampanjresor för att säkerställa att lojalitetserbjudanden och lojalitetsbelöningar kompletterar varandra i stället för att skapa konflikter mellan varandra.
- Supportnivåutvecklingen förbättras genom att man beräknar hur nära en prenumerant är nästa nivå och presenterar åtgärdbara steg för att nå den.
