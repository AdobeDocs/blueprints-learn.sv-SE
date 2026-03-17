---
title: Användningsexempel inom B2B
description: Upptäck hur B2B-organisationer använder Adobe Experience Platform för att snabba upp flödet, förbättra kvaliteten på leads och få fler kunder.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '2269'
ht-degree: 1%

---


# Användningsexempel inom B2B

Företag och organisationer använder Adobe Experience Platform för att sammanställa data på konto- och personnivå, så att marknadsförings- och säljteam kan leverera samordnade, relevanta upplevelser i alla faser av köpresan. I allt från produktaccelerering till kundexpansion visar de här användningsexemplen hur B2B-team omvandlar komplexa data till mätbara affärsresultat.

>[!NOTE]
>
>Information om B2B-specifika arkitekturutkast, inklusive kontobaserad aktivering och hantering av inköpsgrupper, finns i [B2B-aktiverings- och marknadsföringsplanerna](/help/blueprints/b2b/overview.md).

## Account-Based Marketing Personalization

Anpassa marknadsföringskommunikation och innehåll för målkonton baserat på kontoprofil, engagemangshistorik och köpsignaler. Genom att anpassa meddelanden efter varje kontos unika kontext kan marknadsföringsteamen bryta igenom bruset och engagera rätt intressenter med rätt innehåll.

### Affärspåverkan

Organisationer som implementerar kontobaserad marknadsföringspersonalisering ser vanligtvis en 30-40-procentig ökning av kontots engagemang, vilket driver fram en starkare pipeline och snabbare avtalsutveckling.

### Implementera

Använd mönstret [B2B Audience Activation](/help/blueprints/use-case-patterns/audience-building-activation/b2b-audience-activation.md) för att skapa målgrupper på kontonivå och aktivera personaliserat innehåll i olika kanaler. Det här mönstret är utformat för kontobaserade strategier som stöder både målgruppsanpassning på konto- och personnivå.

### Tekniska överväganden

- Integrera CRM-data (t.ex. [!DNL Salesforce] eller [!DNL Microsoft Dynamics]) för att upprätthålla aktuella kontohierarkier, affärsmöjlighetsfaser och ägarskapstilldelningar.
- Konfigurera profilscheman på kontonivå för att fånga upp firmografiska attribut som bransch, antal anställda, intäktsintervall och teknologi.
- Koppla relationer mellan människor och konton för att säkerställa att enskilda engagemangssignaler kan kombineras med poängsättning och segmentering på kontonivå.
- Koordinera med [!DNL Marketo Engage] för att anpassa kampanjer för automatiserad marknadsföring till plattformsdrivna kontomålgrupper.


## Poäng och undervisning i leads

Automatisk poängsättning av leads baserat på profildata och beteende, och sedan dirigera högkvalitativa leads till försäljning med personaliserade vårdskampanjer för andra. Med den här metoden kan säljarna fokusera på de mest lovande möjligheterna samtidigt som marknadsföringen fortsätter att utveckla sina tidigare potentiella kunder.

### Affärspåverkan

Företag som implementerar beteendestyrd poängsättning och automatiserad vårdsverksamhet får normalt en 25-35-procentig ökning av konverteringsgraden från tips till tillfälle, vilket snabbar upp produktionshastigheten och förbättrar säljproduktiviteten.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg för att utforma förgreningsresor som svarar på förändringar i lead-poäng och beteendeutlösare. Det här mönstret har stöd för den villkorliga logik som behövs för att dirigera leads mellan vårdspår och arbetsflöden för försäljning.

### Tekniska överväganden

- Upprätta dubbelriktad CRM-synkronisering (t.ex. [!DNL Salesforce] eller [!DNL Microsoft Dynamics]) så att lead-poäng och kvalificeringsstatus förblir konsekventa mellan marknadsförings- och försäljningssystem.
- Definiera både demografiska (roll, företagsstorlek, bransch) och beteendemässiga (innehållshämtningar, webbinarier, besök på produktsidor) bedömningsdimensioner.
- Koordinera poängsättningsmodeller för lead med [!DNL Marketo Engage] för att undvika att poängen hamnar i konflikt mellan olika plattformar.
- Ange regler för minskning av bakgrundsmusik för att säkerställa att ledtrådar som är tysta tas bort över tid.


## Content Personalization for Prospects

Anpassa webbplatsinnehåll, resurser och erbjudanden baserat på den potentiella kundens bransch, roll, företagsstorlek och engagemangshistorik. När presumtiva kunder ser innehåll som är relevant för deras specifika situation engagerar de sig djupare och rör sig snabbare genom funnel.

### Affärspåverkan

B2B-organisationer som personaliserar webbupplevelser för kända presumtiva kunder ser vanligtvis en 20-30-procentig ökning av innehållsengagemanget, vilket leder till en mer kvalificerad pipeline och kortare säljcykler.

### Implementera

Använd mönstret [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) för att leverera skräddarsytt innehåll baserat på enhetliga profiler för potentiella kunder. Det här mönstret utnyttjar profildata i realtid för att tillhandahålla de mest relevanta resurserna, fallstudier och uppmaningar till åtgärder för varje besökare.

### Tekniska överväganden

- Implementera identitetsupplösning för att matcha anonyma surfbeteenden med kända poster för potentiella kunder när de autentiserar eller skickar in ett formulär.
- Definiera personaliseringsregler baserat på attribut på kontonivå (bransch, segment, avtalsfas) samt attribut på individnivå (roll, tidigare innehållsförbrukning).
- Integrera med ert innehållshanteringssystem för att dynamiskt byta ut hjältebanners, resursrekommendationer och uppmaningar till åtgärder.
- Se till att [!DNL Marketo Engage] webbspårningsdatafeeds finns i den enhetliga profilen för en fullständig beteendebild.


## Evenemangsregistrering och uppföljning

Automatisera personliga bekräftelser, påminnelser och uppföljning efter händelse baserat på händelsetyp och deltagarprofil. Detta håller presumtiva kunder engagerade före, under och efter evenemang samtidigt som marknadsföringsteamet frigörs från manuell samordning.

### Affärspåverkan

Automatiserade, personaliserade arbetsflöden för händelsekommunikation genererar vanligtvis en ökning på 40-50 % av händelsernas närvaro, vilket maximerar avkastningen på händelseinvesteringar och stärker relationer med potentiella kunder.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg om du vill orkestrera hela händelsens livscykel från registrering till näring efter händelse. Det här mönstret har stöd för tidsbaserade utlösare, villkorsstyrd förgrening efter händelsetyp och uppföljningssekvenser för flera kanaler.

### Tekniska överväganden

- Integrera registreringsdata från webbinarier (t.ex. [!DNL ON24], [!DNL Zoom Webinar]) och in-person-händelsesystem i den enhetliga profilen.
- Hämta närvaro- och engagemangssignaler (sessionslängd, frågor och svar) för att personalisera uppföljningsmeddelanden.
- Koordinera händelseresor med [!DNL Marketo Engage] programstatusar för att bibehålla en konsekvent rapportering mellan olika system.
- Utforma separata resegrenar för deltagare som deltog i kontrast till dem som inte gjorde det, med skräddarsytt innehåll för varje.


## Konverteringskampanjer för testversioner av produkter

Engagera testanvändare med personaliserade produktrekommendationer, utbildningsresurser och erbjudanden för att uppmuntra konvertering till betalda planer. Genom att träffa testanvändare där de arbetar med produktutforskandet kan teamen ta bort friktionen och snabba upp köpprocessen.

### Affärspåverkan

Organisationer som använder personaliserade konverteringskampanjer för testversioner ser vanligtvis en 25-35-procentig ökning av konvertering från testversion till betald, vilket direkt påverkar de nya intäkterna och minskar kundanskaffningskostnaderna.

### Implementera

Använd mönstret [Multi-Step Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) för att skapa tidsbaserade och beteendebaserade konverteringsresor för testanvändare. Det här mönstret har stöd för villkorliga sökvägar baserat på milstolpar för produktanvändning, vilket möjliggör målinriktade knuffar vid rätt ögonblick.

### Tekniska överväganden

- Importera telemetri om produktanvändning (anpassning av funktioner, inloggningsfrekvens, time-in-product) för att skapa interaktionsprofiler för testning i realtid.
- Definiera användningsbaserade milstolpar (t.ex. första projektet som skapats, nyckelfunktion som använts, samarbete som bjudits in) som utlösare för att nå rätt resultat.
- Synkronisera teststatus och konverteringshändelser tillbaka till [!DNL Salesforce] eller [!DNL Microsoft Dynamics] så att säljarna har full insyn i testaktiviteterna.
- Koordinera med [!DNL Marketo Engage] vårdprogram för att undvika överlappande kommunikation under testperioden.


## Nöjda kunder och nyanställda

Personalisera kundintroduktionsresor med relevant utbildning, resurser och support baserat på inköpta produkter och kundprofil. Effektiv introduktion minskar tidsåtgången och lägger grunden till långsiktig kundlojalitet och tillväxt.

### Affärspåverkan

Organisationer med personaliserade introduktionsprogram får normalt 50-60 % ökad användning av funktioner inom de första 90 dagarna, vilket direkt bidrar till högre lojalitetsintäkter och ökade intäkter.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg om du vill skapa startsekvenser som är anpassade efter produkt, plannivå och kundsegment. Det här mönstret har stöd för milstolpe-baserad progression, vilket garanterar att kunderna får rätt vägledning vid varje steg av introduktionen.

### Tekniska överväganden

- Importera telemetri för produktanvändning för att spåra milstolpar för introduktion (första inloggning, första konfiguration, första arbetsflöde slutfört) och utlösa nästa kundsteg därefter.
- Mappa kundprofiler till rätt introduktionsspår baserat på köpt produkt, plannivå och antal licensierade användare.
- Integrera data från framgångsplattformar för att ta fram hälsoresultat och flagga riskkonton för förebyggande åtgärder.
- Synkronisera startstatus och antagandestatistik tillbaka till [!DNL Salesforce] eller [!DNL Microsoft Dynamics] så att ansvariga för kundframgångar kan prioritera utåtriktad marknadsföring.


## Förnyelsekampanjer för kontrakt

Engagera kunder som närmar sig avtalsförnyelse med personaliserade erbjudanden, användningsinsikter och förnyelseincitament. Datadriven förnyelse i rätt tid minskar bortfallet och skyddar återkommande intäkter.

### Affärspåverkan

Företag som implementerar proaktiva, personaliserade förnyelsekampanjer ser vanligtvis en ökning på 30-40 %, vilket skyddar återkommande intäkter och minskar kostnaden för återköp av kunder.

### Implementera

Använd mönstret [Flerkanalsresa med Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) för att leverera rätt förnyelseerbjudande via rätt kanal vid rätt tidpunkt. Det här mönstret kombinerar resesamordning med offertbeslut, vilket möjliggör dynamiska förnyelsebonusar baserat på kontovärde och användning.

### Tekniska överväganden

- Dra in kontraktets slutdatum, förnyelsevillkor och kontovärde från [!DNL Salesforce] eller [!DNL Microsoft Dynamics] för att utlösa förnyelseresor vid lämplig ledtid (t.ex. 90, 60, 30 dagar bort).
- Införliva produktanvändningsdata och kundhälsopoäng för att fastställa förnyelseriskerna och skräddarsy strategin för erbjudandet i enlighet med detta.
- Använd beslut för att välja det optimala förnyelsebonusen (rabatt, utökade villkor, premieuppgradering) baserat på kontots livstidsvärde och sannolikhet för bortfall.
- Koordinera utåtriktad förnyelse med kundframgångs- och säljteam för att undvika konfliktskapande meddelanden via [!DNL Marketo Engage] och CRM-aktivitetstilldelning.


## Merförsäljning och utbyggnadsmöjligheter

Identifiera kunder som är redo för produktuppgraderingar eller ytterligare licenser baserat på användningsmönster, tillväxtindikatorer och kundframgångsuppgifter. Proaktiv utbyggnad gör att kundernas drivkraft förvandlas till ökade intäkter.

### Affärspåverkan

Organisationer som systematiskt identifierar och agerar på expansionssignaler genererar vanligtvis en ökning på 20-30 % av expansionsintäkterna, vilket förbättrar kvarhållandet av nettointäkter och kundens livstidsvärde.

### Implementera

Använd mönstret [Cross-Channel Journey med Decisioning](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) för att leverera personaliserade merförsäljnings- och utbyggnadserbjudanden baserat på realtidsanvändnings- och kontosignaler. Det här mönstret använder decimering för att matcha varje konto med det mest relevanta utbyggnadserbjudandet över alla kanaler.

### Tekniska överväganden

- Importera telemetri för produktanvändning för att upptäcka expanderingssignaler som t.ex. tröskelvärden för licensutnyttjande, takträffar och ökande antal användare.
- Bygg propensitetsmodeller på kontonivå med hjälp av historiska expansionsdata, trender för användning och firmografiska attribut.
- Synkronisera expansionsmöjligheter och rekommenderade erbjudanden tillbaka till [!DNL Salesforce] eller [!DNL Microsoft Dynamics] så att säljarna kan följa upp marknadsföringsgenererade försäljningsförlopp.
- Koordinera med [!DNL Marketo Engage] för att säkerställa att expansionsmeddelanden inte hamnar i konflikt med pågående support- eller förnyelsekommunikation.


## Konkurrenskraftiga ersättningskampanjer

Rikta er till potentiella kunder med hjälp av konkurrentprodukter med personaliserade meddelanden, migrationserbjudanden och konkurrensjämförelser. Genom att ta itu med de specifika problem som är kopplade till varje konkurrent kan marknadsföringsteamen differentiera mer effektivt och snabba upp bytesbesluten.

### Affärspåverkan

B2B-organisationer som kör riktade konkurrenskraftiga ersättningskampanjer får normalt en 15-25-procentig ökning av konkurrensfördelen, fångar in marknadsandelar och förskjuter befintliga leverantörer.

### Implementera

Använd mönstret [Multi-Step Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) om du vill orkestrera kampanjer med flera beröringspunkter som är skräddarsydda för den specifika konkurrent- och potentiella kundprofilen. Det här mönstret har stöd för villkorlig förgreningslogik baserat på identifierade konkurrenter, vilket möjliggör meddelanden som åtgärdar de unika utmaningarna i varje konkurrensscenario.

### Tekniska överväganden

- Integrera konkurrensdata (t.ex. teknikleverantörer, CRM-konkurrentfält) i den enhetliga profilen för att identifiera vilken konkurrent som en potentiell kund för närvarande använder.
- Bygg konkurrentspecifika innehållsresurser (migreringsguider, jämförelsekartor, avkastningskalkylatorer) och mappa dem till innehållsblock på resan.
- Koordinera med [!DNL Marketo Engage] om du inte vill ha några konkurrerande kampanjer för potentiella kunder som redan är aktiva säljcykler eller befintliga kunder.
- Spåra konkurrensutsatt förskjutningsprocess i [!DNL Salesforce] eller [!DNL Microsoft Dynamics] med dedikerad kampanjattribuering för att mäta effektiviteten i programmet.


## Schemaläggning av webbinarium och demo

Anpassa webbinarier och schemaläggning av demo baserat på den potentiella kundens intressen, bransch och engagemang. Relevanta och vältajmade inbjudningar ökar närvaron och genererar ett bättre flöde från live-interaktioner.

### Affärspåverkan

Personaliserade webbinarium- och demoinbjudningsprogram får normalt en 35-45-procentig ökning av antalet besökare på webbinariet, vilket ger en mer kvalificerad pipeline från möjligheter till direktengagemang.

### Implementera

Använd mönstret [Event-Triggered Messaging](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) för att skicka personaliserade inbjudningar när potentiella kunder visar intressesignaler som är kopplade till kommande webbinarier eller demonstrationsämnen. Det här mönstret svarar i realtid på beteendetriggers och ser till att inbjudningar kommer när intresset är som störst.

### Tekniska överväganden

- Definiera intressebaserade utlösande händelser (t.ex. besök på en produktsida, ladda ned en relaterad resurs, engagera med en jämförelse av konkurrenter) som är anpassade till schemalagda webbinarier eller demonstrationsämnen.
- Integrera data för webbinarier-plattformen (t.ex. [!DNL ON24], [!DNL Zoom Webinar]) för att spåra registrering, närvaro och engagemangsmått i den enhetliga profilen.
- Synkronisera demonstrationsbegäranden och schemaläggning av data med [!DNL Salesforce] eller [!DNL Microsoft Dynamics] för att säkerställa att säljarna får meddelanden och kontext i tid.
- Koordinera att inbjudan avbryts med [!DNL Marketo Engage] kommunikationsbegränsningar för att förhindra att potentiella kunder med för många meddelanden kvalificerar sig för flera händelser.


## Fallstudie och avkastning på investering i Personalization

Leverera personaliserade fallstudier, avkastningskalkylatorer och framgångsberättelser baserat på den potentiella kundens bransch, företagsstorlek och användningsexempel. När presumtiva kunder ser korrekturpunkter från organisationer som liknar deras bygger förtroende snabbare och köpbesluten går snabbare.

### Affärspåverkan

Organisationer som personaliserar korrekturpunktsinnehåll ser vanligtvis en 25-35-procentig ökning av engagemanget i fallstudier, vilket bidrar till ökat förtroende och snabbare avslut.

### Implementera

Använd mönstret [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) för att dynamiskt visa de mest relevanta fallstudierna och avkastningen på investeringen baserat på varje potentiell kunders profil. Det här mönstret matchar besökarattribut i ett innehållsbibliotek, vilket säkerställer att alla potentiella kunder ser korrekturpunkter från sin bransch och grupp.

### Tekniska överväganden

- Tagga fallstudier och ROI-innehåll med metadata (bransch, företagsstorlek, användningsfall, produkt) för att möjliggöra dynamisk matchning mot profiler för potentiella kunder.
- Implementera personaliseringsregler som prioriterar branschmatchning först, sedan företagsstorlek och användningsfall, med reservinnehåll för potentiella kunder med begränsade profildata.
- Integrera engagemangssignaler (nedladdningar, sidtid, delningar) tillbaka i den enhetliga profilen för att informera om poängsättning och försäljning.
- Koordinera med [!DNL Marketo Engage] om du vill inkludera personligt korrekturpunktsinnehåll i e-postsekvenser som ska hanteras, inte bara upplevelser på plats.


## Program för kundlobbying

Identifiera och engagera nöjda kunder för att få dem att utnyttja olika möjligheter, t.ex. referenser, fallstudier och utlåtanden baserade på användnings- och nöjesdata. Glna kunder är en kraftfull tillväxtmotor när de är kända och inbjudna att dela med sig av sina framgångar.

### Affärspåverkan

Strukturerade kundrådgivningsprogram ökar vanligtvis engagemanget i lobbying med 20-30 %, vilket ger en stadig ström av referenser, fallstudier och utlåtanden som stöder nya affärsmöjligheter.

### Implementera

Använd mönstret [Orchestrated Journey](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) i flera steg om du vill skapa arbetsflöden för identifiering och engagemang som svarar på nöjda användare och användningssignaler. Det här mönstret stöder progressiva förfrågningar om lobbying, med början med enkelt deltagande (t.ex. en granskning) och fortskridande till mer djupgående åtaganden (t.ex. ett referenssamtal eller en fallstudie).

### Tekniska överväganden

- Resultat från en undersökning om hur nöjda kunderna är (t.ex. Net Promoter Score, kundnöjdhetspoäng) och produktanvändningsdata för att bygga upp en prognos för varje konto.
- Definiera behörighetskriterier som kombinerar trösklar, milstolpar för användning och kontobeständighet för att undvika för tidigt resultat.
- Synkronisera status och deltagarhistorik tillbaka till [!DNL Salesforce] eller [!DNL Microsoft Dynamics] så att säljarna kan referera till kundförespråkare under prospekteringen.
- Koordinera med [!DNL Marketo Engage] för att inaktivera lobbying vid eskalering av aktiv support eller förnyelseförhandlingar.
