---
title: Exempel på bilanvändning
description: Upptäck hur bilföretag använder Adobe Experience Platform för att personalisera kundresan, förbättra servicen och skapa lojalitet hos sina ägare.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '1843'
ht-degree: 0%

---


# Användningsexempel

Med Adobe Experience Platform kan bilföretag sammanställa kunddata från bilhandlarinteraktioner, onlineundersökningar, servicejournaler och uppkopplade bilsystem i en enda vy av varje ägare. Denna grund möjliggör personaliserade upplevelser under hela ägarskapets livscykel, från inledande fordonsundersökning till inköp, service och lojalitet.

## Använd ärendesammanfattning

| Användningsfall | Beskrivning | Affärspåverkan | Implementeringsmönster |
| --- | --- | --- | --- |
| [Purchase Journey Personalization](#vehicle-purchase-journey-personalization) | Personalisera fordonets inköpsresa från forskning till inköp med relevanta fordonsrekommendationer, finansieringsalternativ och information om återförsäljare. När potentiella köpare får skräddarsydd vägledning i varje steg går de snabbare och med större självförtroende genom funnel. | 20-30 % ökning av konverteringsgraden mellan leads och inköp, förbättrat försäljningsflöde | [Flerkanalsresor med beslut](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) |
| [Påminnelser om tjänstavtalad tid](#service-appointment-reminders) | Skicka personliga påminnelser om tjänster baserat på bilkörning, servicehistorik och kundönskemål. Proaktiv utåtriktad verksamhet håller kvar fordon och ser till att kunderna återvänder till bilhandlaren i stället för att söka efter tredjepartsleverantörer. | 40-50 % ökning av antalet besökare, ökade serviceintäkter | [Meddelanden som utlösts av händelser](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| [Värdekampanjer för handel](#trade-in-value-campaigns) | Erbjud proaktivt värdebedömningar till kunder som kan vara redo att uppgradera. Att nå ägare vid rätt tidpunkt i ägarcykeln snabbar upp vägen till ett nytt inköp av fordon. | 25-35 % ökning av handelsengagemang, ökad försäljning av nya fordon | [Samlad resa i flera steg](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| [Rekommendationer för delar och tillbehör](#parts-and-accessories-recommendations) | Rekommendera relevanta delar, tillbehör och uppgraderingar baserat på fordonsmodell, ägartid och kundönskemål. Personaliserade eftermarknadsrekommendationer genererar inkrementella intäkter och hjälper ägare att få ut mer av sina fordon. | 30-40 % ökning av inköp av delar/tillbehör, ökade eftermarknadsintäkter | [Beteenderekommendation](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| [Meddelanden om fordonsåterkallande](#vehicle-recall-notifications) | Skicka personaliserade meddelanden om återkallande med alternativ för schemaläggning av tjänst och säkerhetsinformation. Snabb, tydlig kommunikation om återkallande skyddar kundsäkerheten och visar varumärkets engagemang för ansvarsfull ägandesupport. | 60-70% ökning av svarsfrekvens för återkallande, förbättrad efterlevnad av säkerhetskrav | [Meddelanden som utlösts av händelser](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| [Nya startkampanjer för modeller](#new-model-launch-campaigns) | Rikta in er på kunder som kan vara intresserade av att lansera nya modeller baserat på deras aktuella fordon, preferenser och inköpshistorik. Fokuserad målgruppsanpassning maximerar starteffekten och skapar en tidig orderdrivkraft. | 35-45 % ökning av engagemanget för lanseringskampanjer, ökat intresse för nya modeller | [Aktivera utgående batchmeddelande](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md) |
| [Erbjudanden om finansiering och försäkring](#financing-and-insurance-offers) | Presentera skräddarsydda finansierings- och försäkringserbjudanden baserat på kreditprofil, urval av fordon och tidslinje för inköp. Skräddarsydda finansiella produkter undanröjer köphinder och hjälper kunderna att känna sig säkra på sina villkor. | 25-35 % ökning av finansieringsacceptansen, ökade intäkter per försäljning | [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) |
| [Schemaläggning av testenhet](#test-drive-scheduling) | Möjliggör anpassad schemaläggning av testkörningar med återförsäljarrekommendationer och tillgång till fordon. Att göra det enkelt för intresserade köpare att komma bakom hjulet snabbar upp köpprocessen. | 50-60 % ökning av antalet testkörningar, förbättrad försäljningskonvertering | [Meddelanden som utlösts av händelser](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| [Lojalitetsprogram för ägare](#owner-loyalty-programs) | Anpassa kundlojalitetsprogramkommunikation, belöningar och exklusiva erbjudanden baserat på ägarskapshistorik och lojalitetsnivå. Att långsiktiga ägare erkänns stärker den känslomässiga kopplingen till varumärket. | 40-50 % ökning av lojalitetsprogrammets engagemang, fler återkommande inköp | [Flerkanalsresor med beslut](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) |
| [Garantier och utökade serviceplaner](#warranty-and-extended-service-plans) | Rekommendera garantier och utökade serviceplaner vid optimala tidpunkter baserat på fordonets ålder, körsträcka och köpmönster. Vältajmad utåtriktad teknik fångar upp intäkterna innan fabriksgarantierna upphör att gälla. | 20-30 % ökning av utökad garanti, ökade serviceintäkter | [Samlad resa i flera steg](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| [Aktivering av kopplad bilfunktion](#connected-car-feature-activation) | Anpassa anslutna bilar efter behov utifrån fordonets kapacitet och tekniska preferenser. Att hjälpa ägare att upptäcka oanvända funktioner ökar nöjdheten och stärker den digitala relationen. | 35-45 % ökning av antalet aktiverade funktioner, förbättrad kundupplevelse | [Samlad resa i flera steg](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| [Nätverkssamordning för återförsäljare](#dealer-network-coordination) | Möjliggör anpassade rekommendationer för återförsäljare baserat på kundens placering, preferenser och återförsäljarlager. Att knyta samman kunder med rätt återförsäljare förbättrar upplevelsen av köp och service. | 30-40 % ökning av handlarnas engagemang, förbättrad säljsamordning | [Known-Visitor Web/App Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) |

## Tekniska överväganden per användningsfall

### Personalisering av kundresa för fordon

- Fordonsinventeringsdata från hanteringssystem för återförsäljare måste integreras och uppdateras ofta så att rekommendationerna avspeglar den faktiska tillgängligheten hos närliggande återförsäljare.
- Kundens forskningsbeteende på hela webbplatsen, inklusive fordonskonfigurationsaktivitet, användning av jämförelseverktyg och nedladdning av broschyrer, måste samlas in för att exakt identifiera inköpsavsiktssignaler.
- Leadbedömningsmodeller bör ta hänsyn till både online- och offlinesignaler, såsom återförsäljarbesök och telefonförfrågningar, för att prioritera de mest avsiktliga utsikterna.
- [!DNL Real-Time Customer Data Platform] profiler måste sammanfoga anonyma webbundersökningssessioner med kända kundidentiteter när en potentiell kund registrerar eller besöker en återförsäljare.

### Påminnelser om avtalade tider för tjänsten

- Fordonets körsträckor och telematikdata från anslutna bilsystem eller handlarservicedokumentation måste flöda in i kundprofiler för att utlösa påminnelser vid rätt serviceintervall.
- Påminnelsemeddelanden ska innehålla schemaläggningslänkar med ett klick som fyller i kundens fordonsinformation i förväg och rekommenderade serviceartiklar för att minimera bokningsfriktionen.
- Tjänsthistorikposter måste integreras för att undvika att rekommendera tjänster som nyligen har slutförts och för att anpassa påminnelsen med de specifika underhållsobjekten som ska utföras.
- [!DNL Journey Optimizer]-meddelandetimingen ska ta hänsyn till återförsäljarens tjänstkapacitet och öppettider så att kunderna kan boka avtalade tider när de får påminnelsen.

### Prisvärda kampanjer

- Uppgifter om fordonsvärdering från tredjepartsleverantörer måste integreras och uppdateras regelbundet för att säkerställa att de insamlade uppskattningar som delas med kunderna är korrekta och konkurrenskraftiga.
- Livscykelmodeller för ägandeskap bör beakta faktorer som förfallodatum för leasing, tidslinjer för låneutbetalningar och genomsnittlig ägandetid per fordonssegment för att identifiera det optimala utdatafönstret.
- Kampanjmeddelanden ska dynamiskt referera till kundens nuvarande fordon och föreslå specifika uppgraderingsalternativ som passar deras preferenser och budget.
- [!DNL Experience Platform] segment ska exkludera kunder som nyligen har köpt ett fordon eller som för närvarande befinner sig i en aktiv servicetvist för att undvika dåligt tidsåtgång.

### Rekommendationer för delar och tillbehör

- Produktkatalogdata måste innehålla information om fordonskompatibilitet så att rekommendationer endast visar delar och tillbehör som passar kundens specifika fordonsår, tillverkare och modell.
- Säsongsmässiga och regionala faktorer bör påverka rekommendationerna. Tillbehör under vintern bör främjas i kallare klimat, medan prestandauppgraderingar kan få mer genklang i regioner med aktiva entusiastsamhällen.
- Webbläsarbeteendet på delar- och tillbehörssidor måste hämtas och kopplas till kundprofiler för att förfina rekommendationer baserat på det uttryckliga intresset.
- [!DNL Experience Platform] Webbimplementeringen av SDK bör hämta data om identifieringsnummer för fordon från autentiserade sessioner för att säkerställa att kompatibilitetsfiltreringen är korrekt.

### Meddelanden om återkallande av fordon

- Registrering av fordonsidentifieringsnummer måste förvaras korrekt i kundprofiler så att återkallningsmeddelanden når alla berörda ägare och inte går till opåverkade kunder.
- Återkallande av meddelanden måste uppfylla de lagstadgade kraven på innehåll, tidpunkt och leveransbekräftelse för säkerhetsmeddelanden på varje tillämplig marknad.
- Flerkanalsleverans (e-post, SMS, push-meddelanden och fysisk post) bör användas för att maximera räckvidden, eftersom säkerhetskritisk kommunikation kräver större leveranssäkerhet än marknadsföringsmeddelanden.
- [!DNL Journey Optimizer] ska spåra status för återkallelsesvar på individnivå och eskalera uppföljningsmeddelanden för ägare som inte har schemalagt tjänsten inom en angiven tidsram.

### Nya kampanjer för modelllansering

- Målgruppssegmenten för lanseringskampanjer bör beakta aktuell fordonsmodell, ägartid, tidigare modellens intressesignaler och demografisk passning för att identifiera de mest framgångsrika utsikterna.
- Startinnehållet ska vara anpassat för att referera till kundens nuvarande fordon och lyfta fram specifika förbättringar eller funktioner som uppfyller deras troliga prioriteringar.
- Tidsåtgången för kampanjer måste överensstämma med embarkeringsdatum och regionala lanseringsplaner för att säkerställa att kunderna får information vid rätt tidpunkt för sin marknad.
- [!DNL Real-Time Customer Data Platform] målgruppsaktivering ska synkronisera startsegment med annonsplattformar för koordinerat stöd för betalda medier tillsammans med helkanalsutåtriktad marknadsföring.

### Finansierings- och försäkringserbjudanden

- Reglerna för rätten att köpa finansiella erbjudanden måste vara noga konfigurerade så att de uppfyller kraven i lånebestämmelserna och säkerställer att de erbjudanden som skickas till kunderna verkligen är de som de kan kvalificera sig för.
- Integrering av kreditprofildata kräver säker hantering och strikt åtkomstkontroll eftersom den ekonomiska informationen omfattas av högre sekretess- och myndighetskrav.
- Erbjudandet ska innehålla tydliga uppgifter om villkor, räntor och andra villkor i enlighet med konsumentfinansieringsbestämmelserna på varje tillämplig marknad.
- Beslutsreglerna för [!DNL Journey Optimizer] bör ta hänsyn till priser, nedbetalningar och lånevillkor för att rangordna erbjudanden efter relevans snarare än efter ränta.

### Testa enhetsplanering

- Systemen för återförsäljarinventering måste integreras för att bekräfta att den specifika fordonsmodellen och trimningen som kunden är intresserad av finns tillgänglig för testkörning hos den rekommenderade återförsäljaren.
- Platsbaserade rekommendationer för återförsäljare bör ta hänsyn till kundadress, återförsäljarbetyg och tillgänglighet för aktuella avtalade tider för att föreslå det lämpligaste alternativet.
- Bekräftelse och påminnelsemeddelanden för testenheten ska innehålla anvisningar, kontaktinformation för återförsäljaren och vad som ska förväntas, vilket minskar antalet ej visade meddelanden.
- [!DNL Experience Platform] beteendedata bör identifiera det optimala tillfället att föreslå en testkörning, så att man undviker för tidigt utåtriktad verksamhet för forskare som inte är redo ännu.

### Bonusprogram för ägare

- Beräkningar av lojalitetsnivån måste omfatta flera dimensioner av engagemang, inklusive servicebesök, inköp av reservdelar, hänvisningar och närvaro vid händelse, inte bara fordonets inköpshistorik.
- Belöningssystemen vid återförsäljare och servicecenter måste integreras så att förmånerna kan lösas in smidigt vid servicegraften.
- Kommunikationen bör anpassas baserat på ägarskapets livscykelstadium och leverera olika värdeförslag till nya ägare under det första året jämfört med långsiktiga ägare som närmar sig en eventuell uppgradering.
- Resurslogiken för [!DNL Journey Optimizer] bör identifiera nivåändringar i realtid och utlösa gratulations- eller återengagemangsmeddelanden när kunderna rör sig mellan lojalitetsnivåerna.

### Garanti och utökade serviceplaner

- Garantins förfallodatum och täckningsinformation måste spåras korrekt i kundprofiler för att utlösa kontakt vid rätt tidpunkt, vanligtvis 60-90 dagar innan utgång.
- Fordonets körsträcka och användningsmönster från anslutna bildata eller serviceuppgifter bör vara en vägledning för planrekommendationer, eftersom bilförare med hög körsträcka har en annan täckning än ägare med låg körsträcka.
- Innehållet i avtalsjämförelsen ska vara tydligt och jargongfritt, vilket hjälper kunderna att förstå exakt vad som täcks och värdet i förhållande till potentiella reparationskostnader utanför företagets ficka.
- [!DNL Real-Time Customer Data Platform] segment ska skilja mellan kunder med utgångna fabriksgarantier, kunder med befintliga utökade planer som närmar sig förnyelse och kunder utan aktuell täckning.

### Aktivering av anslutna bilfunktioner

- Anslutna data för bilplattformar måste integreras för att identifiera vilka funktioner som finns tillgängliga på varje fordon och vilka som ägaren redan har aktiverat eller använt.
- Spårning av nya funktioner bör fånga upp aktiveringshändelser, användarfrekvens och engagemangsdjup för att personalisera sekvensen och paketeringen av funktionsrekommendationer.
- Meddelandekanaler i fordon bör samordnas med e-post- och appmeddelanden för att leverera funktionsförslag vid det mest relevanta tillfället, till exempel för att föreslå navigeringsfunktioner när en resa upptäcks.
- [!DNL Experience Platform]-profiler ska lagra konfigurationsdata för fordonsteknik, inklusive installerade paket och programvaruversioner, för att säkerställa att funktionsrekommendationerna är kompatibla med ägarens specifika fordon.

### Samordning mellan återförsäljarnätverk

- Lagerflöden från återförsäljare måste integreras och uppdateras ofta för att säkerställa att de fordon som visas för kunderna korrekt återspeglar vad som finns på respektive återförsäljares parti.
- Tilldelningslogik från kund till leverantör bör beakta närhet, återförsäljarspecialisering, språkinställningar och alla befintliga återförsäljarrelationer för att ge bästa matchning.
- Regler för dirigering av leads måste säkerställa att när en kund uttrycker inköpsintresse online kommer förfrågningen snabbt till rätt återförsäljare med fullständig information om kundens forskningsverksamhet.
- Identitetsupplösningen för [!DNL Experience Platform] måste hantera scenarier där en kund interagerar med flera återförsäljare, upprätthålla en enhetlig profil samtidigt som varje återförsäljares syn på sina egna kundrelationer respekteras.
