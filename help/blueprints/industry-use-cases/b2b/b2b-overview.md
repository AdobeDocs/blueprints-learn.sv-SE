---
title: Användningsexempel inom B2B
description: Upptäck hur B2B-organisationer använder Adobe Experience Platform för att snabba upp flödet, förbättra kvaliteten på leads och få fler kunder.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: 6073bdc4-e148-455e-aa4e-3d5226d4b5a2
source-git-commit: 0236bd326730ee9a0be621ee0e60ddc3d352410d
workflow-type: tm+mt
source-wordcount: '3479'
ht-degree: 0%

---

# Användningsexempel inom B2B

Företag och organisationer använder Adobe Experience Platform för att sammanställa data på konto- och personnivå, så att marknadsförings- och säljteam kan leverera samordnade, relevanta upplevelser i alla faser av köpresan. I allt från produktaccelerering till kundexpansion visar de här användningsexemplen hur B2B-team omvandlar komplexa data till mätbara affärsresultat.

>[!NOTE]
>
>Information om B2B-specifika arkitekturutkast, inklusive kontobaserad aktivering och hantering av inköpsgrupper, finns i [B2B-aktiverings- och marknadsföringsplanerna](/help/blueprints/b2b/overview.md).

## Account-Based Marketing Personalization

Anpassa marknadsföringskommunikation och innehåll för målkonton baserat på kontoprofil, engagemangshistorik och köpsignaler. Genom att anpassa meddelanden efter varje kontos unika kontext kan marknadsföringsteamen bryta igenom bruset och engagera rätt intressenter med rätt innehåll.

### Affärspåverkan

Organisationer som implementerar kontobaserad marknadsföringspersonalisering ser förbättrad kontointeraktion, vilket ger ett starkare flöde och snabbare avtalsutveckling.

### Implementera

Använd mönstret [B2B Audience Activation](/help/blueprints/use-case-patterns/audience-building-activation/b2b-audience-activation.md) för att skapa målgrupper på kontonivå och aktivera personaliserat innehåll i olika kanaler. Det här mönstret är utformat för kontobaserade strategier som stöder både målgruppsanpassning på konto- och personnivå. Detta är det rätta mönstret när målgruppsanpassningen måste fungera på kontonivå snarare än på individnivå - standardgenereringen av RT-CDP-målgruppen stöder inte den kontobaserade datamodell som krävs för ABM-strategier.

### Tekniska överväganden

- Integrera CRM-data (t.ex. [!DNL Salesforce] eller [!DNL Microsoft Dynamics]) för att upprätthålla aktuella kontohierarkier, affärsmöjlighetsfaser och ägarskapstilldelningar.
- Konfigurera profilscheman på kontonivå för att fånga upp firmografiska attribut som bransch, antal anställda, intäktsintervall och teknologi.
- Koppla relationer mellan människor och konton för att säkerställa att enskilda engagemangssignaler kan kombineras med poängsättning och segmentering på kontonivå.
- Koordinera med [!DNL Marketo Engage] för att anpassa kampanjer för automatiserad marknadsföring till plattformsdrivna kontomålgrupper.


## Poäng och undervisning i leads

Automatisk poängsättning av leads baserat på profildata och beteende, och sedan dirigera högkvalitativa leads till försäljning med personaliserade vårdskampanjer för andra. Med den här metoden kan säljarna fokusera på de mest lovande möjligheterna samtidigt som marknadsföringen fortsätter att utveckla sina tidigare potentiella kunder.

### Affärspåverkan

Företag som implementerar beteendestyrd poängsättning och automatiserad vård ser bättre konvertering från tips till tillfälle, snabbare pipeline-hastighet och förbättrad försäljningsproduktivitet.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg för att utforma förgreningsresor som svarar på förändringar i lead-poäng och beteendeutlösare. Det här mönstret har stöd för den villkorliga logik som behövs för att dirigera leads mellan vårdspår och arbetsflöden för försäljning. Det här är det rätta mönstret när användningsfallet kräver ett sekvensflöde med flera meddelanden på flera dagar med villkorlig förgrening baserat på förändringar av lead-poäng och beteendehändelser - ett enda utlöst meddelande kan inte hantera beroendelogiken mellan poängfaser och beslut om routning.

### Tekniska överväganden

- Upprätta dubbelriktad CRM-synkronisering (t.ex. [!DNL Salesforce] eller [!DNL Microsoft Dynamics]) så att lead-poäng och kvalificeringsstatus förblir konsekventa mellan marknadsförings- och försäljningssystem.
- Definiera både demografiska (roll, företagsstorlek, bransch) och beteendemässiga (innehållshämtningar, webbinarier, besök på produktsidor) bedömningsdimensioner.
- Koordinera poängsättningsmodeller för lead med [!DNL Marketo Engage] för att undvika att poängen hamnar i konflikt mellan olika plattformar.
- Ange regler för minskning av bakgrundsmusik för att säkerställa att ledtrådar som är tysta tas bort över tid.


## Content Personalization for Prospects

Anpassa webbplatsinnehåll, resurser och erbjudanden baserat på den potentiella kundens bransch, roll, företagsstorlek och engagemangshistorik. När presumtiva kunder ser innehåll som är relevant för deras specifika situation engagerar de sig djupare och rör sig snabbare genom funnel.

### Affärspåverkan

B2B-organisationer som personaliserar webbupplevelser för kända presumtiva kunder ser bättre innehållsengagemang, vilket leder till mer kvalificerade säljprocesser och kortare säljcykler.

### Implementera

Använd mönstret [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) för att leverera skräddarsytt innehåll baserat på enhetliga profiler för potentiella kunder. Det här mönstret utnyttjar profildata i realtid för att tillhandahålla de mest relevanta resurserna, fallstudier och uppmaningar till åtgärder för varje besökare. Det här är det rätta mönstret när personalisering styrs av profilattribut och segmentmedlemskap snarare än en beteendetillhörighetsmodell - vilket gör att attribut på kontonivå och individnivå styr upplevelsen.

### Tekniska överväganden

- Implementera identitetsupplösning för att matcha anonyma surfbeteenden med kända poster för potentiella kunder när de autentiserar eller skickar in ett formulär.
- Definiera personaliseringsregler baserat på attribut på kontonivå (bransch, segment, avtalsfas) samt attribut på individnivå (roll, tidigare innehållsförbrukning).
- Integrera med ert innehållshanteringssystem för att dynamiskt byta ut hjältebanners, resursrekommendationer och uppmaningar till åtgärder.
- Se till att [!DNL Marketo Engage] webbspårningsdatafeeds finns i den enhetliga profilen för en fullständig beteendebild.


## Evenemangsregistrering och uppföljning

Automatisera personliga bekräftelser, påminnelser och uppföljning efter händelse baserat på händelsetyp och deltagarprofil. Detta håller presumtiva kunder engagerade före, under och efter evenemang samtidigt som marknadsföringsteamet frigörs från manuell samordning.

### Affärspåverkan

Automatiserade, personaliserade arbetsflöden för händelsekommunikation leder till bättre närvaro, maximerar avkastningen på händelseinvesteringar och stärker relationer med potentiella kunder.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg om du vill orkestrera hela händelsens livscykel från registrering till näring efter händelse. Det här mönstret har stöd för tidsbaserade utlösare, villkorsstyrd förgrening efter händelsetyp och uppföljningssekvenser för flera kanaler. Det här är det rätta mönstret när användningsfallet kräver ett sekvensflöde med flera meddelanden på flera dagar med villkorlig förgreningslogik baserat på händelseregistrering och närvaro - bara tidsbaserade meddelanden kan inte hantera den komplexa förgreningslogiken mellan registrerade, övervakade och ej visade sökvägar.

### Tekniska överväganden

- Integrera registreringsdata från webbinarier (t.ex. [!DNL ON24], [!DNL Zoom Webinar]) och in-person-händelsesystem i den enhetliga profilen.
- Hämta närvaro- och engagemangssignaler (sessionslängd, frågor och svar) för att personalisera uppföljningsmeddelanden.
- Koordinera händelseresor med [!DNL Marketo Engage] programstatusar för att bibehålla en konsekvent rapportering mellan olika system.
- Utforma separata resegrenar för deltagare som deltog i kontrast till dem som inte gjorde det, med skräddarsytt innehåll för varje.


## Konverteringskampanjer för testversioner av produkter

Engagera testanvändare med personaliserade produktrekommendationer, utbildningsresurser och erbjudanden för att uppmuntra konvertering till betalda planer. Genom att träffa testanvändare där de arbetar med produktutforskandet kan teamen ta bort friktionen och snabba upp köpprocessen.

### Affärspåverkan

Organisationer som använder personaliserade konverteringskampanjer för testversioner får bättre konvertering från testversion till betald, vilket direkt påverkar nya intäkter och minskar kundvärvningskostnaderna.

### Implementera

Använd mönstret [Multi-Step Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) för att skapa tidsbaserade och beteendebaserade konverteringsresor för testanvändare. Det här mönstret har stöd för villkorliga sökvägar baserat på milstolpar för produktanvändning, vilket möjliggör målinriktade knuffar vid rätt ögonblick. Det här är det rätta mönstret när användningsfallet kräver ett sekvensflöde med flera meddelanden som triggas av användarmilstolpar med villkorlig förgrening - händelseutlösta meddelanden kan inte hantera den förutsägbara timing och beroendelogik som behövs för milstolpe-baserad vårdsutveckling.

### Tekniska överväganden

- Importera telemetri om produktanvändning (anpassning av funktioner, inloggningsfrekvens, time-in-product) för att skapa interaktionsprofiler för testning i realtid.
- Definiera användningsbaserade milstolpar (t.ex. första projektet som skapats, nyckelfunktion som använts, samarbete som bjudits in) som utlösare för att nå rätt resultat.
- Synkronisera teststatus och konverteringshändelser tillbaka till [!DNL Salesforce] eller [!DNL Microsoft Dynamics] så att säljarna har full insyn i testaktiviteterna.
- Koordinera med [!DNL Marketo Engage] vårdprogram för att undvika överlappande kommunikation under testperioden.


## Nöjda kunder och nyanställda

Personalisera kundintroduktionsresor med relevant utbildning, resurser och support baserat på inköpta produkter och kundprofil. Effektiv introduktion minskar tidsåtgången och lägger grunden till långsiktig kundlojalitet och tillväxt.

### Affärspåverkan

Organisationer med skräddarsydda introduktionsprogram ser förbättrad användning av funktioner under de första 90 dagarna, vilket direkt bidrar till högre intäkter för bevarande och expansion.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg om du vill skapa startsekvenser som är anpassade efter produkt, plannivå och kundsegment. Det här mönstret har stöd för milstolpe-baserad progression, vilket garanterar att kunderna får rätt vägledning vid varje steg av introduktionen. Det här är det rätta mönstret när användningsfallet kräver ett sekvensflöde med flera meddelanden med villkorsstyrd fortsättning baserat på milstolpar för produktanvändning - händelseutlösta meddelanden kan inte hantera den komplexa mellanlagringslogik som krävs för guidad introduktionsprogression.

### Tekniska överväganden

- Importera telemetri för produktanvändning för att spåra milstolpar för introduktion (första inloggning, första konfiguration, första arbetsflöde slutfört) och utlösa nästa kundsteg därefter.
- Mappa kundprofiler till rätt introduktionsspår baserat på köpt produkt, plannivå och antal licensierade användare.
- Integrera data från framgångsplattformar för att ta fram hälsoresultat och flagga riskkonton för förebyggande åtgärder.
- Synkronisera startstatus och antagandestatistik tillbaka till [!DNL Salesforce] eller [!DNL Microsoft Dynamics] så att ansvariga för kundframgångar kan prioritera utåtriktad marknadsföring.


## Förnyelsekampanjer för kontrakt

Engagera kunder som närmar sig avtalsförnyelse med personaliserade erbjudanden, användningsinsikter och förnyelseincitament. Datadriven förnyelse i rätt tid minskar bortfallet och skyddar återkommande intäkter.

### Affärspåverkan

Företag som implementerar proaktiva, personaliserade förnyelsekampanjer ser förbättrade förnyelsefrekvenser, skyddar återkommande intäkter och minskar kostnaderna för återköp av kunder.

### Implementera

Använd mönstret [Flerkanalsresa med Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) för att leverera rätt förnyelseerbjudande via rätt kanal vid rätt tidpunkt. Det här mönstret kombinerar resesamordning med offertbeslut, vilket möjliggör dynamiska förnyelsebonusar baserat på kontovärde och användning. Det här är det rätta mönstret när resan måste koordinera leveransen över flera kanaler och valet av erbjudande kräver kontovärde och användningsbegränsningar - endast resesamordning ger inte det realtidsbeslutsskikt som behövs för att dynamiskt matcha förnyelseincitament.

### Tekniska överväganden

- Dra in kontraktets slutdatum, förnyelsevillkor och kontovärde från [!DNL Salesforce] eller [!DNL Microsoft Dynamics] för att utlösa förnyelseresor vid lämplig ledtid (t.ex. 90, 60, 30 dagar bort).
- Införliva produktanvändningsdata och kundhälsopoäng för att fastställa förnyelseriskerna och skräddarsy strategin för erbjudandet i enlighet med detta.
- Använd beslut för att välja det optimala förnyelsebonusen (rabatt, utökade villkor, premieuppgradering) baserat på kontots livstidsvärde och sannolikhet för bortfall.
- Koordinera utåtriktad förnyelse med kundframgångs- och säljteam för att undvika konfliktskapande meddelanden via [!DNL Marketo Engage] och CRM-aktivitetstilldelning.


## Merförsäljning och utbyggnadsmöjligheter

Identifiera kunder som är redo för produktuppgraderingar eller ytterligare licenser baserat på användningsmönster, tillväxtindikatorer och kundframgångsuppgifter. Proaktiv utbyggnad gör att kundernas drivkraft förvandlas till ökade intäkter.

### Affärspåverkan

Organisationer som systematiskt identifierar och agerar på expansionssignaler genererar ökade expansionsintäkter, vilket förbättrar kvarhållandet av nettointäkter och kundens livstidsvärde.

### Implementera

Använd mönstret [Cross-Channel Journey med Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) för att leverera personaliserade merförsäljnings- och utbyggnadserbjudanden baserat på realtidsanvändnings- och kontosignaler. Det här mönstret använder decimering för att matcha varje konto med det mest relevanta utbyggnadserbjudandet över alla kanaler. Detta är det rätta mönstret när resan måste koordinera leveransen över flera kanaler och valet av erbjudanden kräver regler för vilka expansionserbjudanden matchar specifika konton - endast resesamordning ger inte det beslutsskikt som behövs för begränsad erbjudandematchning.

### Tekniska överväganden

- Importera telemetri för produktanvändning för att upptäcka expanderingssignaler som t.ex. tröskelvärden för licensutnyttjande, takträffar och ökande antal användare.
- Bygg propensitetsmodeller på kontonivå med hjälp av historiska expansionsdata, trender för användning och firmografiska attribut.
- Synkronisera expansionsmöjligheter och rekommenderade erbjudanden tillbaka till [!DNL Salesforce] eller [!DNL Microsoft Dynamics] så att säljarna kan följa upp marknadsföringsgenererade försäljningsförlopp.
- Koordinera med [!DNL Marketo Engage] för att säkerställa att expansionsmeddelanden inte hamnar i konflikt med pågående support- eller förnyelsekommunikation.


## Konkurrenskraftiga ersättningskampanjer

Rikta er till potentiella kunder med hjälp av konkurrentprodukter med personaliserade meddelanden, migrationserbjudanden och konkurrensjämförelser. Genom att ta itu med de specifika problem som är kopplade till varje konkurrent kan marknadsföringsteamen differentiera mer effektivt och snabba upp bytesbesluten.

### Affärspåverkan

B2B-organisationer som genomför riktade konkurrerande ersättningskampanjer ser förbättrade konkurrensfördelar, ökade marknadsandelar och föråldrade befintliga leverantörer.

### Implementera

Använd mönstret [Multi-Step Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) om du vill orkestrera kampanjer med flera beröringspunkter som är skräddarsydda för den specifika konkurrent- och potentiella kundprofilen. Det här mönstret har stöd för villkorlig förgreningslogik baserat på identifierade konkurrenter, vilket möjliggör meddelanden som åtgärdar de unika utmaningarna i varje konkurrensscenario. Det här är det rätta mönstret när användningsfallet kräver ett sekvensflöde med flera meddelanden och villkorlig förgreningslogik baserat på den specifika profilen för konkurrent och potentiell kund - händelserelaterade meddelanden kan inte hantera komplexiteten hos kundspecifik förgreningslogik över flera kontaktytor.

### Tekniska överväganden

- Integrera konkurrensdata (t.ex. teknikleverantörer, CRM-konkurrentfält) i den enhetliga profilen för att identifiera vilken konkurrent som en potentiell kund för närvarande använder.
- Bygg konkurrentspecifika innehållsresurser (migreringsguider, jämförelsekartor, avkastningskalkylatorer) och mappa dem till innehållsblock på resan.
- Koordinera med [!DNL Marketo Engage] om du inte vill ha några konkurrerande kampanjer för potentiella kunder som redan är aktiva säljcykler eller befintliga kunder.
- Spåra konkurrensutsatt förskjutningsprocess i [!DNL Salesforce] eller [!DNL Microsoft Dynamics] med dedikerad kampanjattribuering för att mäta effektiviteten i programmet.


## Schemaläggning av webbinarium och demo

Anpassa webbinarier och schemaläggning av demo baserat på den potentiella kundens intressen, bransch och engagemang. Relevanta och vältajmade inbjudningar ökar närvaron och genererar ett bättre flöde från live-interaktioner.

### Affärspåverkan

Personaliserade webbinarier och demonstrationsinbjudningsprogram ser bättre närvarofrekvens för webbinarier, vilket ger en mer kvalificerad pipeline från möjligheter till live-engagemang.

### Implementera

Använd mönstret [Event-Triggered Messaging](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) för att skicka personaliserade inbjudningar när potentiella kunder visar intressesignaler som är kopplade till kommande webbinarier eller demonstrationsämnen. Det här mönstret svarar i realtid på beteendetriggers och ser till att inbjudningar kommer när intresset är som störst. Detta är det rätta mönstret när utlösaren är en diskret kundåtgärd som är anpassad efter webbinariets relevans och svaret är en enda, tidskänslig inbjudan - snarare än en sekvens i flera steg eller ett pågående vårdsprogram.

### Tekniska överväganden

- Definiera intressebaserade utlösande händelser (t.ex. besök på en produktsida, ladda ned en relaterad resurs, engagera med en jämförelse av konkurrenter) som är anpassade till schemalagda webbinarier eller demonstrationsämnen.
- Integrera data för webbinarier-plattformen (t.ex. [!DNL ON24], [!DNL Zoom Webinar]) för att spåra registrering, närvaro och engagemangsmått i den enhetliga profilen.
- Synkronisera demonstrationsbegäranden och schemaläggning av data med [!DNL Salesforce] eller [!DNL Microsoft Dynamics] för att säkerställa att säljarna får meddelanden och kontext i tid.
- Koordinera att inbjudan avbryts med [!DNL Marketo Engage] kommunikationsbegränsningar för att förhindra att potentiella kunder med för många meddelanden kvalificerar sig för flera händelser.


## Fallstudie och avkastning på investering i Personalization

Leverera personaliserade fallstudier, avkastningskalkylatorer och framgångsberättelser baserat på den potentiella kundens bransch, företagsstorlek och användningsexempel. När presumtiva kunder ser korrekturpunkter från organisationer som liknar deras bygger förtroende snabbare och köpbesluten går snabbare.

### Affärspåverkan

Organisationer som personaliserar korrekturpunktsinnehåll ser ett förbättrat engagemang i fallstudier, vilket bidrar till ökat förtroende och snabbare avslut.

### Implementera

Använd mönstret [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) för att dynamiskt visa de mest relevanta fallstudierna och avkastningen på investeringen baserat på varje potentiell kunders profil. Det här mönstret matchar besökarattribut i ett innehållsbibliotek, vilket säkerställer att alla potentiella kunder ser korrekturpunkter från sin bransch och grupp. Det här är det rätta mönstret när personalisering styrs av profilattribut och segmentmedlemskap snarare än en beteendetillhörighetsmodell - vilket gör att attribut i bransch- och företagsstorlek kan matcha potentiella kunder med relevanta korrekturpunkter.

### Tekniska överväganden

- Tagga fallstudier och ROI-innehåll med metadata (bransch, företagsstorlek, användningsfall, produkt) för att möjliggöra dynamisk matchning mot profiler för potentiella kunder.
- Implementera personaliseringsregler som prioriterar branschmatchning först, sedan företagsstorlek och användningsfall, med reservinnehåll för potentiella kunder med begränsade profildata.
- Integrera engagemangssignaler (nedladdningar, sidtid, delningar) tillbaka i den enhetliga profilen för att informera om poängsättning och försäljning.
- Koordinera med [!DNL Marketo Engage] om du vill inkludera personligt korrekturpunktsinnehåll i e-postsekvenser som ska hanteras, inte bara upplevelser på plats.


## Program för kundlobbying

Identifiera och engagera nöjda kunder för att få dem att utnyttja olika möjligheter, t.ex. referenser, fallstudier och utlåtanden baserade på användnings- och nöjesdata. Glna kunder är en kraftfull tillväxtmotor när de är kända och inbjudna att dela med sig av sina framgångar.

### Affärspåverkan

Strukturerade kundrådgivningsprogram främjar ökat deltagande i annonsering och genererar en stadig ström av referenser, fallstudier och utlåtanden som stöder nya företagsförvärv.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg om du vill skapa arbetsflöden för identifiering och engagemang som svarar på nöjda användare och användningssignaler. Det här mönstret stöder progressiva förfrågningar om lobbying, med början med enkelt deltagande (t.ex. en granskning) och fortskridande till mer djupgående åtaganden (t.ex. ett referenssamtal eller en fallstudie). Det här är det rätta mönstret när användningsfallet kräver ett sekvensflöde med flera meddelanden med villkorsstyrda framsteg baserat på nöjda kunder och användningssignaler - ett enda utlöst meddelande kan inte hantera den progressiva interaktionslogik som behövs för att eskalera förfrågningar om lobbying över tid.

### Tekniska överväganden

- Resultat från en undersökning om hur nöjda kunderna är (t.ex. Net Promoter Score, kundnöjdhetspoäng) och produktanvändningsdata för att bygga upp en prognos för varje konto.
- Definiera behörighetskriterier som kombinerar trösklar, milstolpar för användning och kontobeständighet för att undvika för tidigt resultat.
- Synkronisera status och deltagarhistorik tillbaka till [!DNL Salesforce] eller [!DNL Microsoft Dynamics] så att säljarna kan referera till kundförespråkare under prospekteringen.
- Koordinera med [!DNL Marketo Engage] för att inaktivera lobbying vid eskalering av aktiv support eller förnyelseförhandlingar.

## B2B kontobaserad Audience Activation

Bygg målgrupper på kontonivå genom att kombinera data på kontonivå, köpa gruppsignaler och engagemang på personnivå och sedan aktivera dem för LinkedIn, DSP och CRM-destinationer. Kontobaserad målgruppsaktivering gör det möjligt för B2B-organisationer att inrikta sig på hela inköpsorganisationer med koordinerad digital annonsering snarare än enskilda kontakter, och att anpassa de betalda medieutgifterna till sina kontoprioriteringar.

### Affärspåverkan

B2B-organisationer med kontobaserad målgruppsaktivering ser större påverkan från betalda medieprogram, med särskilt stor effekt när målgruppssegmenten är anpassade efter försäljningsprioriteringarna och uppdateras ofta allt eftersom kontointeraktionen förändras.

### Implementera

Använd mönstret [B2B Audience Activation](/help/blueprints/use-case-patterns/audience-building-activation/b2b-audience-activation.md) för att skapa kontonivåsegment med hjälp av relationer mellan konton och personer och aktivera dem för betalmediematerial som kan användas i B2B. Det här är det rätta mönstret när målgruppskonstruktionen måste fungera på kontonivå - kombinera signaler från flera kontakter inom en inköpsorganisation - i stället för på individnivå.

### Tekniska överväganden

- Konfiguration av B2B-identitetsdiagram måste exakt länka kända individer till deras kontoposter. Avbrott i personliga associationer leder till ofullständig gruppsignalaggregering.
- Målgruppssegmenten för konton bör uppdateras enligt ett schema som är anpassat till kampanjflygdatum och granskningsresultat för pipeline - segment som avviker från det aktuella pipeline-läget minskar effektiviteten för medieinvesteringarna.
- LinkedIn Matched Audiences och liknande B2B-plattformar matchar på professionella e-postadresser, som kan skilja sig från de personliga e-postadresser som lagras i CRM. Båda e-posttyperna ska inkluderas i målgruppsnyttolasterna.
- Aktiveringsmålgrupper bör utesluta konton i aktiva avtalsfaser där betald annonsering kan skapa krånglig överlappning med direktförsäljning.


## Buying Group Journey Orchestration

Samordna resor på kontonivå som vårdar medlemmar i inköpsgrupper baserat på deras roller, poängställning och kontokvalificeringsstatus, med automatiserad leverans till försäljning. Genom att samordna reselogiken på köpgruppsnivå snarare än på individnivå säkerställs att varje berörd part får meddelanden som är anpassade till deras roll och beslutsfas, samtidigt som enhetligheten upprätthålls inom kontot.

### Affärspåverkan

B2B-organisationer som använder sig av samordning av inköpsgruppresor ser en förbättrad frekvens för skapande av affärsmöjligheter från rörliga marknadsföringskanaler och en snabbare utveckling genom tidiga avtalsfaser, särskilt när överlämning av säljmaterial aktiveras automatiskt baserat på mätbara tröskelvärden för engagemang.

### Implementera

Använd mönstret [Buying Group-Based Marketing](/help/blueprints/use-case-patterns/campaign-management-orchestration/buying-group-based-marketing.md) för att skapa kontokvalificerade resor som segmenterar köpgruppsmedlemmar efter roll, utvärdera engagemangssignaler på gruppnivå och samordna samordnade flerpersonskampanjer med villkorlig förgreningslogik baserat på kontostatus. Det här är det rätta mönstret när reselogik måste fungera på kontonivå snarare än på individnivå - standardkundnivå kan inte hantera kraven på gruppkvalifikationer och personlig samordning av B2B-inköpsgruppshantering.

### Tekniska överväganden

- Definitioner av gruppmedlemskap måste bevaras i B2B-datamodellen, så att kända kontakter kopplas till deras konton och rollerna tilldelas, t.ex. mästare, ekonomisk köpare eller teknisk utvärderare.
- Bedömningen av kontoengagemang måste samla signaler från flera personer inom inköpsgruppen. En enskild kontakts engagemang är inte tillräckligt för att fastställa beredskapen på kontonivå.
- Reseundertryckning måste synkroniseras med CRM-affärsfaser för att förhindra att automatiserade marknadsföringsmeddelanden hamnar i konflikt med aktiva försäljningskonversationer.
- Varningar och överlämningsmeddelanden måste integreras med CRM och plattformen för säljengagemang så att handläggarna får en snabb och åtgärdbar kontext när kontona når överlämningströskeln.


## Account-Based Marketing (ABM) Personalization

Anpassa marknadsföringskommunikation och innehåll för målkonton baserat på kontoprofil, engagemangshistorik och köpsignaler. ABM-personalisering går bortom kontouppläggning genom att anpassa meddelandeinnehåll och webbupplevelser till varje kontos specifika bransch, storlek och kända affärsutmaningar - vilket skapar relevans som generiska kampanjmeddelanden inte kan uppnå.

### Affärspåverkan

B2B-organisationer med personaliseringsrapport på kontonivå förbättrade engagemangsfrekvensen för utgående kampanjer och högre konverteringsgrad från webben till pipeline för riktade konton, med särskilt starka resultat när personaliseringen sträcker sig över landningssidor och webbplatsupplevelser som besöks via betalda medier.

### Implementera

Använd mönstret [B2B Audience Activation](/help/blueprints/use-case-patterns/audience-building-activation/b2b-audience-activation.md) för att aktivera profilerna på kontonivå för personalisering över webb- och utgående kanaler. Detta är det rätta mönstret när det primära kravet är målgruppsanpassning på kontonivå för personalisering snarare än kundresssamordning - data i kontoprofiler driver personaliseringsbesluten snarare än individuella beteendesignaler.

### Tekniska överväganden

- Företagsdata - bransch, företagsstorlek, geografi, teknologi - måste vara aktuella och konsekvent utformade för att skapa meningsfull innehållspersonalisering utöver allmän målinriktning på branschnivå.
- Webbpersonalisering för kända B2B-besökare kräver IP-till-konto-lösning eller direkt autentisering. IP-baserad upplösning har lägre precision och bör inte förlitas för kontobeslut med högt värde.
- Innehåll måste utvecklas för varje kontosegment med personalisering som mål. Om personalisering aktiveras utan tillräckliga innehållsvariationer får vissa konton oförändrade upplevelser.
- Personalization-beslut på kontonivå bör anpassas till den aktuella CRM-fasen och försäljningsaktiviteten för att undvika att förmedla information om funnel-medvetenhet till konton som redan är aktiva.
