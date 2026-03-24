---
title: Användningsexempel inom telekommunikation
description: Upptäck hur telekommunikationsorganisationer använder Adobe Experience Platform för att minska bortfall, få enhetsuppgraderingar och förbättra kundengagemanget.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: 653632f0-81be-435c-a703-56c5bc132794
source-git-commit: 0236bd326730ee9a0be621ee0e60ddc3d352410d
workflow-type: tm+mt
source-wordcount: '3822'
ht-degree: 0%

---

# Användningsexempel inom telekommunikation

Telekommunikationsorganisationer använder Adobe Experience Platform för att skapa en enhetlig bild av varje abonnent och leverera personaliserade upplevelser som minskar bortfallet, ökar planerings- och enhetsuppgraderingar och stärker långsiktiga kundrelationer. Genom att koppla samman data om nätverksanvändning, faktureringsinformation och kundinteraktioner kan telekomleverantörer förutse abonnenternas behov och engagera dem i rätt ögonblick via de kanaler de föredrar.

## Rekommendationer för enhetsuppgradering

Identifiera kunder som är berättigade till enhetsuppgraderingar och presentera personaliserade enhetsrekommendationer och uppgraderingserbjudanden baserat på användningsmönster och önskemål. Genom att analysera kontraktstidslinjer, enhetsålder och webbläsarbeteende kan telekomleverantörerna visa de mest relevanta enheterna och finansieringsalternativen för varje abonnent.

### Affärspåverkan

Organisationer som implementerar rekommendationer för enhetsuppgradering ser förbättrade konverteringsgrader genom att leverera rätt erbjudande vid rätt tidpunkt via den kanal kunden föredrar.

### Implementera

Använd mönstret [Cross-Channel Journey med Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) för att samordna uppgraderingsresor som utvärderar varje abonnents behörighet, enhetsinställningar och kanaltillhörighet för att leverera personaliserade uppgraderingserbjudanden via e-post, appmeddelanden och butiksupplevelser. Det här är det rätta mönstret när valet av erbjudanden måste ta hänsyn till enhetsberättigandefönster, kanalinställningar och lagerbegränsningar - begränsningar som kräver styrd beslutslogik snarare än enbart enkla beteenderekommendationer.

### Tekniska överväganden

- Integrera system för inventering och prissättning av enheter för att säkerställa att rekommendationerna återspeglar den aktuella tillgängligheten och kampanjpriserna.
- Koppla samman data från kontraktshantering för att exakt identifiera uppgraderingsberättigande fönster och tidiga uppgraderingserbjudanden.
- Införliva telemetri för enhetsanvändning (lagringskapacitet, batteriljud, prestandamått) för att förstärka rekommendationens relevans.
- Samordna med återförsäljar- och e-handelsplattformar för att upprätthålla en enhetlig uppgraderingsupplevelse i alla digitala kanaler och butikskanaler.


## Planoptimeringskampanjer

Analysera kundanvändningsmönster och rekommendera optimala ändringar av planen för att spara pengar eller få bättre funktioner baserat på deras faktiska behov. Proaktivt nå ut med planrekommendationer bygger upp förtroende och minskar risken för att prenumeranter lämnar företaget för konkurrenter med enklare priser.

### Affärspåverkan

Planoptimeringskampanjer driver till en förbättrad nivå på planändringar, vilket förbättrar kundnöjdheten och samtidigt ökar den genomsnittliga intäkten per användare när prenumeranterna går över till planer som bättre motsvarar deras förbrukning.

### Implementera

Använd mönstret [Multi-Step Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) för att skapa en multi-touch-kampanj som identifierar avvikelser mellan användning och plan, utbildar prenumeranter på bättre alternativ och guidar dem genom avtalsförändringsprocessen med aktuella uppföljningar. Det här är det rätta mönstret när användningsexemplet kräver ett sekvensflöde med flera meddelanden på flera dagar med villkorlig förgrening baserat på prenumerantens engagemang och planens antagande - ett enda utlöst meddelande kan inte hantera utbildningsresan och beroendelogiken mellan utbildnings- och konverteringssteg.

### Tekniska överväganden

- Samla in realtids- och historiska användningsdata (röstminuter, dataförbrukning, internationella samtal) för att identifiera felaktiga planmatchningar.
- Koppla ihop faktureringssystemdata för att beräkna potentiella besparingar eller funktionsvinster för varje rekommenderad ändring av planen.
- Konto för kampanjprissättningsregler och avtalsförpliktelser när ni tar fram planrekommendationer.
- Integrera med självbetjäningsportaler så att prenumeranterna kan slutföra avtalsändringar direkt från kontaktytorna i kampanjen.


## Kravförebyggande för värdefulla kunder

Identifiera värdefulla kunder som riskerar att bli stulna och engagera dem med personaliserade kundlojalitetserbjudanden och proaktiv kundtjänst. Genom att kombinera beteendesignaler som minskad användning, upprepade servicebesök och konkurrenskraftig surfning med livstidsdata kan leverantörerna ingripa innan en prenumerant bestämmer sig för att gå ur.

### Affärspåverkan

Program för att förebygga kronor som riktar sig till värdefulla abonnenter leder till meningsfulla bortfall av bortfall, skyddar betydande återkommande intäkter och minskar kostnaderna för att skaffa nya kunder.

### Implementera

Använd mönstret [Cross-Channel Journey med Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) för att övervaka bortfallsrisksignaler i realtid, fastställa det bästa erbjudandet för kvarhållande för varje prenumerant och samordna personaliserad utåtriktad marknadsföring över digitala kanaler och callcenter. Det här är det rätta mönstret när resan måste koordinera leveransen över digitala och agentstödda kanaler för att förhindra dubblerade kvarhållningserbjudanden och när valet av erbjudanden kräver riskpoäng och affärsbegränsningar - en flerstegssamordning ger inte den realtidskoordinering som behövs.

### Tekniska överväganden

- Skapa poängvärden för kundens benägenhet genom att kombinera användartrender, interaktionshistorik för tjänster och känslomässig information från utskrifter från callcenter.
- Integrera call center och detaljhandelssystem så att handläggarna får insyn i de lojalitetserbjudanden som redan presenteras via digitala kanaler.
- Koppla samman konkurrensdata (portaförfrågningar, jämförelser av konkurrentplaner) för att förfina riskbedömningen och erbjuda strategier.
- Upprätta styrningsregler för att förhindra överkontakt med riskabonnenter, vilket kan snabba upp bortfallet snarare än förhindra det.


## Ny kundintroduktionsresa

Automatisera en personaliserad introduktionsresa för nya kunder med välkomstinformation, vägledning för kontokonfiguration och självstudiekurser. En strukturerad introduktionsupplevelse hjälper abonnenterna att snabbt upptäcka det fulla värdet av sin plan och sina tjänster och lägga grunden för långsiktig lojalitet.

### Affärspåverkan

Väldesignade introduktionsresor ökar antalet aktiverade funktioner, vilket leder till högre nöjdhetspoäng och lägre bortfall i förtid bland nya abonnenter.

### Implementera

Använd mönstret [Multi-Step Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) för att skapa en sekventiell introduktionsupplevelse som anpassar sig utifrån varje abonnents plantyp, enhet och engagemang med föregående introduktionssteg. Det här är det rätta mönstret när användningsfallet kräver ett sekvensflöde med flera meddelanden på flera dagar med villkorlig förgreningslogik baserat på funktionsidentifiering och engagemang - ett enda utlöst meddelande kan inte hantera den adaptiva beroendelogiken mellan startsteg baserat på prenumerationsplan och enhetstyp.

### Tekniska överväganden

- Integrera system för kontoetablering för att utlösa introduktionsresan direkt efter aktiveringen och skräddarsy innehållet efter abonnentens specifika plan och enhet.
- Koppla samman appinteraktionsdata för att spåra vilka funktioner abonnenten har utforskat och justera efterföljande startmeddelanden därefter.
- Samordna med kundsupportplattformen för att se till att agenterna är medvetna om en abonnents introduktionsfas om de ringer in med frågor.
- Stöd för flera startvägar för olika kundsegment, t.ex. enskilda prenumeranter, administratörer av familjeplaner och företagskonton.


## Varningar och rekommendationer om dataanvändning

Skicka personaliserade aviseringar när kunderna närmar sig datagränserna och rekommendera planuppgraderingar eller datatillägg baserat på användningsmönster. Lämpliga meddelanden i rätt tid omvandlar en potentiellt frustrerande upplevelse till ett ögonblick av förtroendeskapande engagemang.

### Affärspåverkan

Proaktiva varningsmeddelanden om dataanvändning ger bättre inköp av tillägg av data samtidigt som man minskar antalet faktureringsproblem och förbättrar kundnöjdheten generellt.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) om du vill skicka realtidsaviseringar när användningströskeln överskrids, med personaliserade rekommendationer baserade på abonnentens historiska konsumtionsmönster och planinformation. Det här är det rätta mönstret när utlösaren är en systemhändelse (korsning av tröskelvärde för användning) i stället för kundbeteende, och den kommunikation som krävs är omedelbar och reaktiv i stället för en kontinuerlig närliggande sekvens.

### Tekniska överväganden

- Anslut till dataflöden för nätverksanvändning som ger nästan realtidsuppdateringar av förbrukningen för att utlösa larm vid meningsfulla tröskelvärden (75 %, 90 %, 100 % av plangränserna).
- Integrera fakturerings- och planhanteringssystem för att presentera korrekta tilläggspriser och möjliggöra köp med ett klick direkt från varningsmeddelandet.
- Konto för delade datapoler för familjeplaner genom att meddela både den enskilda användaren och planadministratören.
- Implementera frekvensbegränsning för att undvika larm trötthet för abonnenter som konsekvent använder stora mängder data varje faktureringscykel.


## Meddelanden om serviceflöde

Meddela kunderna i förväg om avbrott i tjänsten, underhåll eller nätverksproblem i området med personaliserade uppdateringar och kompensationserbjudanden. Att nå ut innan kunderna upplever frustration visar på ansvar och minskar den inkommande supportvolymen avsevärt.

### Affärspåverkan

Proaktiva meddelanden om driftsavbrott ger tydliga bekräftelsegrader och minskar avsevärt kundens volym vid avbrott i tjänsten, vilket minskar supportkostnaderna samtidigt som kundens uppfattning förbättras.

### Implementera

Använd mönstret [Event-Triggered Messaging](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) om du vill identifiera nätverkshändelser och omedelbart meddela berörda prenumeranter via de kanaler de föredrar med relevant information, beräknade lösningstider och lämplig kompensation när så är lämpligt. Det här är det rätta mönstret när utlösaren är en systemhändelse (nätverksavbrott) i stället för kundbeteende, och den kommunikation som krävs är omedelbar och reaktiv i stället för en kontinuerlig närliggande sekvens.

### Tekniska överväganden

- Integrera med övervakningssystem i nätverkets ledningscentral för att ta emot data om driftstopp i realtid och underhållshändelser med geografisk omfångsinformation.
- Använd prenumerantens adress- och platsdata för att identifiera berörda kunder på ett korrekt sätt och undvika att meddela dem utanför det påverkade området.
- Anslut till fakturerings- och kreditsystemet för att automatisera serviceerbjudanden för längre avbrott baserat på prenumerantens plan och hur länge störningen varar.
- Koordinera meddelanden över alla kanaler för att tillhandahålla konsekventa statusuppdateringar och undvika att skicka information som står i konflikt när situationen förändras.


## Hantering av familjeplaner

Anpassa kommunikationen och erbjudandena för administratörer av familjeplaner baserat på användningsmönster och individuella medlemsbehov. Familjeplaner representerar konton med högt värde och flera rader, där engagemang med avtalsadministratören driver lojalitet på alla rader.

### Affärspåverkan

Kommunikation om personaliserad familjerelaterad hantering ökar engagemanget i familjeplanen, vilket leder till högre radlojalitet och högre livstidsvärde per konto.

### Implementera

Använd mönstret [Flerkanalsresor med beslutande](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) om du vill analysera användningen för alla familjemedlemmar, identifiera möjligheter som att lägga till rader eller justera enskilda begränsningar och leverera anpassade rekommendationer till avtalsadministratören. Det här är det rätta mönstret när valet av erbjudanden måste ta hänsyn till hierarkibehörigheter, användningsaggregering för flera medlemmar och integritetsbegränsningar - begränsningar som kräver styrd beslutslogik snarare än individuella prenumerantrekommendationer.

### Tekniska överväganden

- Modellera hierarkier för familjekonton för att skilja mellan avtalsadministratören och enskilda medlemmar, med hänsyn tagen till behörighetsnivåer för kommunikation och kontoändringar.
- Samla in användningsdata för alla rader på kontot för att identifiera mönster och möjligheter på familjenivå, t.ex. underutnyttjade delade data eller ojämna uppgraderingscykler.
- Integrera system för föräldrakontroll och innehållsfiltrering för att stödja familjespecifika funktioner i personalisering.
- Se till att sekretessregler finns på plats så att användningsinformation för enskilda medlemmar delas med avtalsadministratören baserat på kontobehörigheter.


## 5G uppgraderingskampanjer

Rikta er till kunder som är berättigade till 5G-nätverksuppgraderingar med personaliserade erbjudanden och fördelar baserat på deras plats och användningsmönster. När 5G-täckningen utökas kan abonnenterna på nyligen täckta områden med relevanta meddelanden få snabbare acceptans och ökad nätverksanvändning.

### Affärspåverkan

Målinriktade uppgraderingskampanjer för 5G ökar acceptansnivån för 5G bland berättigade prenumeranter, vilket ger bättre avkastning på investeringar i nätverk och konkurrensfördelar.

### Implementera

Använd mönstret [Batch Outbound Message Activation](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md) för att segmentera prenumeranter baserat på 5G-täckning, enhetskompatibilitet och planbehörighet. Leverera sedan personaliserade uppgraderingskampanjer som visar de fördelar som är mest relevanta för varje prenumerations användningsprofil. Det här är det rätta mönstret när målgruppen är fördefinierad och stor, leveranstider är schemalagda i stället för händelsestyrd, och ingen förgrening eller beslutsfattande i realtid krävs - kampanjen kan planeras helt i förväg baserat på tidsramar för lansering av avtal.

### Tekniska överväganden

- Integrera nätverkstäckningskartor för att exakt identifiera abonnenter i områden med aktiv 5G-tjänst och undvika att uppgradera där täckning ännu inte är tillgänglig.
- Koppla samman data om enhetskompatibilitet för att avgöra vilka prenumeranter som behöver en ny enhet jämfört med dem som redan har 5G-kompatibel maskinvara.
- Samordna med butikslagersystem för att säkerställa att de enheter och planer som marknadsförs är tillgängliga i den butik eller online som abonnenten föredrar.
- Segmentera meddelanden efter användningsprofil så att tunga dataanvändare får prestandainriktade fördelar samtidigt som tillfälliga användare får meddelanden om täckning och tillförlitlighet.


## Betalningspåminnelser för faktura

Skicka personliga påminnelser om fakturabetalning via önskade kanaler med betalningsalternativ och kontosaldoinformation. Lämpliga påminnelser i rätt tid minskar försenade betalningar och de därmed sammanhängande kostnaderna för att få in pengar samtidigt som kundrelationen förblir positiv.

### Affärspåverkan

Personaliserade påminnelser om fakturabetalning förbättrar betalningstakten i tid, minskar indrivningskostnaderna och minimerar avbrott i tjänsten som kan leda till missnöjda kunder.

### Implementera

Använd mönstret [Händelseutlöst meddelanden](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) om du vill skicka påminnelser vid rätt tidpunkt före förfallodatumet, anpassade med abonnentens saldo, betalningsmetod och en direktlänk för att slutföra betalningen. Detta är det rätta mönstret när utlösaren är en tidsbaserad systemhändelse (faktureringsdatum) snarare än kundbeteende, och den nödvändiga kommunikationen är omedelbar och transaktionell snarare än en interaktionssekvens i flera steg.

### Tekniska överväganden

- Integrera med faktureringsplattformen för att få tillgång till kontosaldon, förfallodatum och betalningshistorik i realtid för korrekt påminnelseinnehåll.
- Anslut till betalningssystem för att aktivera betalning med ett klick direkt från påminnelsemeddelandet.
- Implementera eskaleringslogik som justerar påminnelsens skyndsamhet och frekvens när förfallodatumet närmar sig, samtidigt som kommunikationsinställningarna respekteras.
- Stöd för flera betalningsmetoder (automatisk registrering av betalningar, digital plånbok, banköverföring) och anpassa de presenterade alternativen baserat på prenumerantens historik.


## Rekommendationer för tilläggstjänster

Rekommendera relevanta tilläggstjänster som enhetsförsäkring, molnlagring och strömningspaket baserat på kundens plan, användning och önskemål. Sammanhangsberoende rekommendationer ökar värdet för prenumeranterna som får in från sin relation med leverantören samtidigt som de får en ökad genomsnittlig intäkt per användare.

### Affärspåverkan

Personaliserade rekommendationer för tilläggstjänster ger förbättrad acceptansgrad för tillägg, vilket ökar intäkterna från den befintliga prenumerationsbasen utan att kostnaden för nya kunder ökar.

### Implementera

Använd mönstret [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) för att utvärdera varje abonnents profil, aktuella tjänster och beteendesignaler för att fastställa det mest relevanta tilläggserbjudandet och presentera det via den optimala kanalen och ögonblicket. Det här är det rätta mönstret när valet av erbjudande måste ta hänsyn till nuvarande ägarskap av tjänster och affärsregler som styr kompletterande tjänsteberättigande - regler som kräver styrd beslutslogik i stället för enbart beteendetillhörighet.

### Tekniska överväganden

- Anslut till prenumerantens aktuella tjänstkatalog för att undvika att rekommendera tjänster som de redan har och för att identifiera naturliga komplement till deras befintliga plan.
- Integrera partner- och tredjepartstjänster (direktuppspelningsleverantörer, försäkringsbolag) för att presentera korrekta priser och paketerbjudanden.
- Använd enhets- och användningsdata för att informera om rekommendationer, som att föreslå enhetsförsäkring för prenumeranter med nya premiumenheter eller molnlagring för dem som har ont om enhetslagring.
- Koordinera med personalisering i appar och på webben för att förstärka rekommendationer om tillägg i självbetjäning.


## Personalization för nätverksprestanda

Anpassa information om nätverksprestanda och rekommendationer baserat på kundens plats, enhet och användningsmönster. Genom att hjälpa prenumeranterna att optimera sina anslutningsmöjligheter ökar förtroendet och minskar de supportkontakter som är kopplade till prestandaproblem.

### Affärspåverkan

Personaliserade nätverksprestandaupplevelser ökar appengagemanget, eftersom prenumeranterna återgår till att kontrollera täckning, felsöka problem och hitta optimeringstips som är skräddarsydda efter deras situation.

### Implementera

Använd mönstret [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) för att leverera anpassade instrumentpaneler för nätverksprestanda, täckningsinformation och optimeringsrekommendationer i prenumerantens app- och webbkontoupplevelse. Det här är det rätta mönstret när personalisering drivs av profilattribut och platsdata i stället för en beteendetillhörighetsmodell.

### Tekniska överväganden

- Integrera mätvärden för nätverkskvalitet och täckning för att tillhandahålla platsspecifik prestandainformation som är relevant för abonnentens hemsida, arbete och besökta områden.
- Koppla samman diagnostikdata för enheter för att erbjuda skräddarsydda felsökningsrekommendationer baserat på prenumerantens specifika enhetsmodell och programvaruversion.
- Använd [!DNL Adobe Experience Platform]-kanttjänster för att leverera personalisering med låg latens i appupplevelsen utan att påverka prestanda.
- Implementera feedback-slingor så att prenumeranterna kan rapportera täckningsproblem och berika nätverksdata samtidigt som de visar hur lyhörda de är.


## Lojalitetsprogramengagemang

Anpassa kundens kundskikt, poängsaldo och inlösenhistorik, samtidigt som ni i realtid fragmenterar olika kanaler i appar, på webben, i SMS och i butik för att förhindra att dubbletter eller motstridiga erbjudanden når samma abonnent. Nivåbaserade begränsningar för behörighet styr vilka belöningar, partnerinlösen och kampanjer som varje prenumerant har tillgång till, och dessa regler måste verkställas på beslutslagret i stället för inbäddade i den enskilda kampanjlogiken. Lojalitetsprogrammet måste också samordna med aktiva lojalitets- och uppgraderingskampanjer så att förebyggande erbjudanden och lojalitetserbjudanden kompletterar varandra i stället för att dubbla erbjudanden skickas till prenumeranter som samtidigt befinner sig på flera resor.

### Affärspåverkan

Personaliserat lojalitetsprogram främjar bättre deltagande och belöningsinlösen, vilket ger högre lojalitetsgrad bland registrerade prenumeranter.

### Implementera

Använd mönstret [Cross-Channel Journey med Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) för att skapa personliga kundrelationer som framhäver relevanta belöningar, underrättar prenumeranter om hur skiktet utvecklas och presenterar möjligheter till inlösen i linje med deras preferenser och beteenden. Det här är det rätta mönstret när resan måste koordinera leveransen över flera kanaler för att förhindra dubbla lojalitetserbjudanden och när valet av erbjudanden kräver nivåstatus och inlösningshistorik - flerstegssamordning ger inte det beslutsskikt i realtid som behövs.

### Tekniska överväganden

- Integrera lojalitetsplattformen för att få tillgång till poäng i realtid, nivåstatus och inlösenhistorik för korrekt personalisering.
- Koppla ihop partnerbelöningskataloger för att presentera ett stort antal inlösenalternativ som är skräddarsydda efter varje abonnents uppvisade intressen och tidigare inlösen.
- Samordna lojalitetsmeddelanden med andra kampanjresor för att säkerställa att lojalitetserbjudanden och lojalitetsbelöningar kompletterar varandra i stället för att skapa konflikter mellan varandra.
- Supportnivåutvecklingen förbättras genom att man beräknar hur nära en prenumerant är nästa nivå och presenterar åtgärdbara steg för att nå den.


## AI Plan Advisor

Teleabonnenter står inför en ständig utmaning: att förstå hur deras nuvarande plan jämfört med tillgängliga alternativ och om en annan plan bättre passar deras faktiska användning. Statiska jämförelsesidor kräver att abonnenterna själva tolkar data som de kanske inte förstår helt, vilket leder till suboptimala planval, faktureringstötar och möjlighet att förhindra bortfall. En AI-plansrådgivare engagerar abonnenterna i en naturlig konversation, granskar deras användningsmönster utifrån deras realtidsprofil, frågar kvalificerande frågor om enhetens behov och hushållets behov och guidar dem till den plan - eller en kombination av planer och tillägg - som bäst passar deras situation.

### Affärspåverkan

Konversationsplanens vägledning minskar den plansdrivna belastningen, ökar den bifogade uppgraderingen för prenumeranter som är underdimensionerade av sin nuvarande plan och sänker kontaktcentrets volym för fakturerings- och plansändringsfrågor.

### Implementera

Använd mönstret [Brand Concierge Conversational Experience](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md). Med den här metoden distribueras Product Advisor Agent mot planen och tilläggskatalogen med hjälp av AEP Agent Orchestrator-data och kundprofildata i realtid - inklusive användningshistorik och aktuell planinformation - för att vägleda abonnenterna genom personaliserat planval via naturlig dialog. Det här är det rätta mönstret när målet är interaktiv konversationsidentifiering i flera omgångar som hjälper prenumeranter att aktivt utvärdera och välja rätt plan - skilt från händelseutlösta meddelanden, som meddelar prenumeranter reaktivt om tröskelvärden eller planändringar, och från personaliserade webbupplevelser, som visar planjämförelser i bakgrunden utan att engagera prenumeranterna i en kvalificerande dialog. Det kräver AEP Agent Orchestrator och varumärkesstyrningskonfiguration.

### Tekniska överväganden

- Kundprofilsökningen i realtid måste innehålla aktuella plandetaljer, data- och röstanvändningsmönster, enhetskompatibilitet och avtalsstatus så att rådgivaren kan ge korrekt, kontospecifik vägledning i stället för allmänna beskrivningar som kräver att abonnenten själv tillämpar sin situation.
- Planen och tilläggskatalogen måste hållas aktuell genom integrering med produkthanteringssystemet, eftersom ett rekommendation om ett erbjudande eller kampanjpris som inte längre är tillgängligt - eller utelämnande av ett nystartat alternativ - direkt undergräver prenumerantens förtroende och kan skapa serviceförfrågningar.
- Garantierna för varumärkesstyrning måste definiera hur agenten hanterar konkurrensutsatta jämförelser mellan leverantörer, kampanjpriser och avtalsåtaganden, och säkerställa att agentens respons överensstämmer med regler och varumärkesstandarder utan att skapa vilseledande åtaganden som abonnenten senare kan ifrågasätta.
- Konversationssignaler - inklusive angiven storlek för hushåll, antal enheter, internationell användningsränta och planförändringsavsikt som uttrycks under dialoger - måste hämtas som XDM Experience Events och strömmas tillbaka till AEP, vilket berikar prenumerantprofilerna för att informera kampanjer för att förebygga förändringar, uppgradera och korsförsäljning längre fram i kedjan.


## Churn Propensity och Network Experience Analytics

Korrelera mätvärden för nätverksupplevelser - bortfall av anrop, försämrad dataflöde, exponering av driftstopp - med kundtjänstens kontaktfrekvens och utfall av kundbortfall för att identifiera var problem med nätverkskvalitet kan leda till mätbar attribueringsrisk. Telekommunikationsleverantörer som analyserar nätverksprestanda och kundbeteenden i separata system kan inte avgöra vilka fel i tjänstekvaliteten som faktiskt driver bortfall jämfört med vilka som absorberas utan konsekvens.

### Affärspåverkan

Genom att koppla data om nätverksupplevelser till kundbeteenden och bortfall kan nätverksoperations-, produkt- och kundlojalitetsteamen prioritera reparationsinvesteringar baserat på dokumenterad attribueringseffekt i stället för enbart teknisk svårighetsgrad.

### Implementera

Använd mönstret [Kundanalys och insiktsgenerering](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md). Den här metoden kopplar data från nätverkshändelser, kundtjänstinteraktionsposter, digitala beteendesignaler och prenumeranternas livscykelhändelser till Customer Journey Analytics, där korrelerad analys identifierar tröskelvärden för nätverksupplevelser och kontaktmönster som är statistiskt kopplade till bortfall av bortfall och kontraktsförnyelse. Det här är det rätta mönstret när målet är att skapa insikter och analysera rotorsaker - förstå vilka tjänstekvalitetshändelser som skapar attribuering - i stället för att utlösa ett kvarhållningserbjudande eller aktivera en riskgrupp i en CDP.

### Tekniska överväganden

- Händelser för nätverksupplevelser måste kopplas till prenumerantposter med enhets- eller kontoidentifierare som överensstämmer med det person-ID som konfigurerats i CJA-anslutningen, eftersom nätverks-telemetrisystem vanligtvis använder utrustnings-ID i stället för kundidentifierare internt.
- Kontaktdata för kundtjänst - inklusive kontaktorsakskoder, använd kanal och lösningsstatus - måste infogas som händelser med tidsstämplar som gör att analytiker kan skapa sekventiella sökvägar från nätverkshändelser via servicekontakter via bortfall i CJA-flöden eller bortfallsvisualiseringar.
- Prenumerantens kontrakt- och plandata, inklusive kontraktets slutdatum, plannivå och löptid, bör vara tillgängliga som uppslagsdimensioner i datavyn för CJA så att omsättningsanalysen kan segmenteras efter kontraktets närhet och värdenivå i stället för att prenumerationsbasen behandlas som homogen.
- Datavolymer för telemetri i nätverk kan vara mycket stora. Samplingsstrategier för datauppsättningar eller föraggning i AEP bör övervägas för att hålla CJA frågeprestanda inom godtagbara intervall för självbetjäning av analytiker.

## Churn Prevention &amp; Win-Back

Använd prediktiva modeller och beteendesignaler för att identifiera riskkunder och utlösa personaliserade kundlojalitetskampanjer med skräddarsydda erbjudanden innan de faller bort. Telekommunikationspartners utsätts för ständigt tryck på sig, och det är betydligt mer kostnadseffektivt att nå riskabonnenter med rätt erbjudande innan de kontaktar annulleringskön än att vinna tillbaka kampanjer efter detta.

### Affärspåverkan

Telekomleverantörer med proaktiva program för att förebygga bortfall av bortfall ser från meningsfulla minskningar av den frivilliga bortfallet för riktade segment, med störst påverkan bland medelstora kunder där riktade erbjudanden är mer kostnadseffektiva än allmänna rabatter.

### Implementera

Använd mönstret [Cross-Channel Journey med Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) för att skapa en kundresa som identifierar riskabonnenter baserat på poängvärden för bortfallsbenägenhet, väljer lämpligt kvarhållningserbjudande med hjälp av beslutslogik och levererar det i de kanaler som abonnenten föredrar med uppföljningssteg om den första utåtgången ignoreras. Det här är det rätta mönstret när både val av erbjudanden och resesamordning krävs - ett enda meddelande som utlöses kan inte hantera den rangordningslogik och den multitouch-uppföljning som krävs för effektiv lagring.

### Tekniska överväganden

- Manövreringsmodeller måste utbildas i historiska churn-data som omfattar nätverkserfarenhet, faktureringshändelser, servicebesök och enhetsålder - modeller som är utbildade på enbart engagemangsdata underpresterar ofta mot telekomspecifika churn-drivrutiner.
- Bevarandeerbjudanden måste begränsas av tröskelvärden för kostnader som ska behållas per kundvärdessegment. Beslutsmotorn bör förhindra att erbjudanden om högkostnadskvarhållande tillämpas på lågvärdesabonnenter.
- Signalbearbetning i realtid av kanaler måste upptäcka avtalsförfrågningar och besök på sidan för avbrutna tjänster för att utlösa brådskande kvarhållningssvar innan abonnenten eskalerar.
- Kundtjänstintegrering är avgörande - prenumeranter som anropar kvarhållningskön bör identifieras som resande deltagare så att agenterna har kontexten för kvarhållningserbjudandet klar innan samtalet börjar.
