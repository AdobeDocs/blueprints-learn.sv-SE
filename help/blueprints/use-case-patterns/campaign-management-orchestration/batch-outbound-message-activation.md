---
title: Aktivering av utgående batchmeddelande
description: Lär dig hur du utvärderar en målgrupp och levererar ett schemalagt utgående meddelande i en enda batchkörning.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 192853ce-02ab-46e6-9092-3db5354bc19c
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '8246'
ht-degree: 1%

---

# Aktivera utgående batchmeddelande

Den här guiden ger en fullständig implementeringsreferens för leverans av schemalagda utgående meddelanden till definierade målgruppssegment med [!DNL Adobe Journey Optimizer] (AJO) och [!DNL Adobe Real-Time Customer Data Platform] (RT-CDP). Det är utformat för lösningsarkitekter, marknadsföringsteknologer och implementeringstekniker som behöver förstå alla genomförbara implementeringsstrategier, de beslutsöverväganden som styr varje val och var detaljerad dokumentation om [!DNL Adobe Experience League] finns.

Batchaktivering av utgående meddelanden är det grundläggande kampanjmönstret för 1:N-meddelanden. Den täcker hela livscykeln från målgruppsdefinition till meddelandeleverans och resultatanalys. Den här guiden innehåller tre implementeringsalternativ - Schemalagd kampanj, Audience-Triggered Journey och API-Triggered Campaign - och ger strukturerad beslutsvägledning för val av rätt metod för varje användningsfall.

Den innehåller implementeringsalternativ, avbrottsanalys, gränssnittsnavigeringssökvägar och [!DNL Experience League] dokumentationsreferenser.

## Använd ärendeöversikt

Organisationer behöver ofta leverera ett enda budskap till ett känt målgruppssegment vid en viss tidpunkt eller som svar på en systemhändelse. Det här mönstret åtgärdar det kravet genom att kombinera målgruppsutvärdering i [!DNL RT-CDP] med meddelanderedigering och kampanjkörning i [!DNL Journey Optimizer].

Affärsscenariot är okomplicerat: definiera vem som ska få meddelandet, skapa meddelandeinnehållet med personalisering, binda målgruppen och meddelandet till en kampanj eller resa och skicka enligt ett schema, med målgruppskvalifikation eller via en systemutlösare. Resultatet blir ett levererat meddelande med fullständig rapportering om resultat, engagemang och konverteringsstatistik.

Det här mönstret används när ett affärsmål kan utvecklas genom att ett enda meddelande skickas till en känd målgrupp i ett enda utförande. Det skiljer sig från händelseutlösta meddelanden, som svarar på beteendehändelser i realtid, och från flerstegssamordnade resor, som vägleder profiler genom flera kontaktytor över tid. Batchaktivering är det enklaste kampanjmönstret och den vanligaste startpunkten för utgående meddelanden.

## Viktiga verksamhetsmål

I det här avsnittet beskrivs de primära affärsmålen som batchaktivering av utgående meddelanden stöder.

### Öka engagemanget i e-post och kampanjer

**Beskrivning:** Förbättra öppningsfrekvenser, klickfrekvens och övergripande kampanjrespons med optimerat innehåll och målinriktning.

**KPI:er:** Öppettider, engagemang, konverteringsgrader

### Öka intäkter och försäljning

**Beskrivning:** Öka intäkterna genom optimerade digitala kanaler, kampanjer och kundresor.

**KPI:er:** Konverteringsgrader, Inkrementell intäkt, Genomsnittligt ordervärde

**Relaterat affärsmål:** [Öka intäkter och försäljning](/help/blueprints/business-objectives/revenue-monetization/increase-revenue-sales.md)

### Effektivisera kampanjutförandet

**Beskrivning:** Minska tiden det tar att bygga kampanjer och förenkla användningen av kampanjer i flera kanaler med hjälp av mallar, automatisering och standardiserade processer.

**KPI:er:** Hastighet till marknad, effektivitet, tidsslutförande %

## Exempel på taktiska användningsfall

Följande scenarier illustrerar vanliga program för batchaktivering av utgående meddelanden.

- **Försäljningsmeddelande eller reklamutskick** - Skicka ett kampanjerbjudande till ett segment av berättigade kunder på ett planerat datum
- **Push-meddelande för produktlansering** - Meddela berörda kunder om en ny produkt finns tillgänglig via push
- **Nyhetsbrev eller e-postmeddelande med sammanfattningar** - Leverera periodiska innehållsrundor till abonnentmålgrupper
- **Inbjudan till händelseregistrering** - Bjud in kvalificerade potentiella kunder till webbinarier, konferenser eller personliga event
- **Påminnelse om förnyelse av prenumeration via e-post** - Påminn kunder som närmar sig förnyelsedatum för att vidta åtgärder
- **Milstolpe-meddelande för bonusprogram** - Grattis till medlemmar som når lojalitetsnivåer eller poängtrösklar
- **Specifik call-to-action-e-postadress** - Kör en riktad åtgärd som att slutföra ett köp, uppdatera inställningar eller registrera ett program
- **SMS-kampanj för flash-försäljning eller tidsbegränsat erbjudande** - Skicka brådskande, tidsbundna kampanjer via SMS till utvalda målgrupper

## Nyckeltal för prestanda

I följande tabell definieras nyckeltal som används för att mäta kampanjens effektivitet.

| KPI | Beskrivning | Mätningsmetod |
| --- | --- | --- |
| Leveransnivå | Procentandel meddelanden som levererats till mottagare | Levererat/skickat x 100 |
| Öppen kurs | Procentandel levererade meddelanden som öppnats av mottagarna | Unika öppningar/levererat x 100 |
| Klickfrekvens (CTR) | Procentandel levererade meddelanden där en länk klickades | Unika klick/levererat x 100 |
| Klick-till-öppningsfrekvens (CTOR) | Procentandel öppnade meddelanden där en länk klickades | Unika klick/unika öppnar x 100 |
| Konverteringsgrad | Procentandel mottagare som slutförde den önskade åtgärden | Konverteringar/leverans x 100 |
| Avbeställningsfrekvens | Procentandel mottagare som avbeställt prenumerationen efter att meddelandet tagits emot | Avbeställ prenumerationer/leverans x 100 |
| Studsfrekvens | Procentandel meddelanden som inte kunde levereras | studsar/skickade x 100 |
| Intäkter per e-post som skickats | Intäkter som tilldelats kampanjen delat med skickade meddelanden | Total intäkt / Skickat |

## Använd skiftlägesmönster

**Aktivera utgående batchmeddelande**

Utvärdera en målgrupp och leverera sedan ett schemalagt utgående meddelande (e-post, SMS, push) till alla kvalificerande profiler i en enda gruppkörning.

**Funktionskedja:** Målgruppsutvärdering > Meddelanderedigering > Kampanjkörning > Rapportering

## Tillämpningar

Följande program används för att implementera mönstret.

- **[!DNL Adobe Journey Optimizer](AJO)** - Meddelanderedigering, kanalkonfiguration, kampanjkörning, resesamordning, innehållsexperiment, frekvensregler och rapportering
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)** - Målgruppsutvärdering, medgivande och tillsyn
- **[!DNL Adobe Experience Platform](AEP)** - Profilarkiv, identitetstjänst, scheman, datauppsättningar, datainsamling

## Foundationsfunktioner

Följande grundläggande funktioner måste finnas för det här användningsmönstret. För varje funktion anger statusen om den vanligtvis är obligatorisk, antas vara förkonfigurerad eller inte tillämplig.

| Foundational Function | Status | Vad måste finnas på plats | Experience League Reference |
| --- | --- | --- | --- |
| Administration och styrning | Antagen på plats | AJO-sandlådan har etablerats med en aktiv kanalkonfiguration. Skickar underdomänen delegerad, IP-poolen tilldelad och IP-värmen har slutförts. Användarroller med tilldelade behörigheter för att skapa kampanj/resa. | [Översikt över sandlådor](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/home), [Översikt över åtkomstkontroll](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Datamodellering och förberedelse | Obligatoriskt | XDM Individual Profile-schema med attribut som används för segmentering och personalisering (t.ex. namn, e-postadress, inställningar, nivå). XDM ExperienceEvent-schemat fångar målkonverteringsåtgärden (t.ex. `commerce.purchases`, `web.webInteraction`) för konverteringsspårning efter kampanj. Profilaktiverade datauppsättningar för båda scheman. | [Systemöversikt för XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [Grundläggande om schemakomposition](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| Datakällor och samling | Antagen på plats | SDK- eller Analytics-taggning på CTA-målet måste vara aktiv för att konverteringshändelser ska kunna fångas. Strömnings- eller batchmatningsledningar för profilattribut måste vara i drift. | [Översikt över Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home), [Översikt över källor](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home) |
| Konfiguration av identitet och profil | Antagen på plats | Identitetsnamnutrymmen för e-post (och eventuella enhetsidentifierare) konfigurerade. Profilattribut som krävs för personalisering mappas, hämtas och kan lösas vid sändning. Sammanslagningsprincip har konfigurerats. | [Översikt över identitetstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [Översikt över sammanslagningsprinciper](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| Målgruppsdefinition och segmentering | Obligatoriskt | Målgrupp definierad i RT-CDP med segmentbyggare eller målgruppskomposition. En publik som publicerats och utvärderat med en population som inte är noll. Täcks i implementeringsfas 1 via RT-CDP Audience Evaluation. | [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [Användargränssnittsguide för segmentbyggaren](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder) |

## Stödfunktioner

Följande funktioner förstärker det här användningsmönstret, men behövs inte för att köra kärnan.

| Stödfunktioner | Status | Varför det spelar någon roll | Experience League Reference |
| --- | --- | --- | --- |
| Skapande av beräknat/härlett attribut | Rekommenderad | Beräknade attribut som dagar sedan förra köpet, antal livstidsorder eller poäng för engagemang förbättrar målgruppens precision och möjliggör en mer omfattande personalisering av budskapen. | [Översikt över beräknade attribut](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| Livscykelhantering för data | Rekommenderad | Datalagringsprinciper (förfallodatum) ska finnas för händelsedatamängder som driver konverteringsspårning. Schemafält för samtycke måste konfigureras för att tillåta val/avanmälan på kanalnivå. | [Översikt över livscykelhantering av avancerade data](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home), [Fältgruppen för samtycke och inställningar](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents) |
| Dataanvändningsetiketter och -tillämpning | Rekommenderad | Myndighetsetiketter på PII-fält som används vid personalisering säkerställer regelefterlevnad under aktiveringen. Förhindrar obehörig användning av känsliga profildata i meddelandeinnehåll eller målgruppsexporter. | [Översikt över datastyrning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [Översikt över etiketter för dataanvändning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/labels/overview) |
| Övervakning och observerbarhet | Ingår | Övervakning av sändning i realtid ingår i rapporteringsfasen. Varningar på plattformsnivå om misslyckade inmatningar eller licensanvändning ger synlighet utöver mätvärdena på kampanjnivå. | [Översikt över Insikter i observabilitet](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home), [Översikt över aviseringar](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview) |
| Rapportering och analys | Ingår | Kampanjrapporter och reserapporter ingår i rapporteringsfasen. För en djupare flerkanalsanalys kan CJA-integrering tillhandahålla funnel-analyser, attribueringsmodellering och kohortanalys utöver AJO inbyggda rapporter. | [CJA - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [AJO + CJA - integreringsguide](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo) |

## Programfunktioner

I den här planen används följande funktioner från programfunktionskatalogen. Funktioner mappas till implementeringsfaser i stället för till numrerade steg.

### [!DNL Journey Optimizer] (AJO)

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Kanalkonfiguration | Fas 2: Kanalkonfiguration | Konfigurera eller validera kanalytan (e-post, SMS eller push) inklusive underdomän, IP-pool, avsändarinställningar och undertryckningslista |
| Redigering av meddelanden | Fas 3: Meddelanderedigering | Skapa meddelandeinnehåll med mallar, e-post-Designer, personaliseringsuttryck, villkorsstyrda innehållsblock och innehållsfragment |
| Kampanjkörning | Fas 4: Kampanj eller reseskapande | Skapa, konfigurera och aktivera en schemalagd eller API-utlöst kampanj som binder målgrupp, meddelande och körningsschema |
| Experimentera med innehåll | Fas 4: Kampanj eller reseskapande | Du kan även konfigurera A/B- eller multivariata innehållsexperiment för att optimera meddelandeprestanda |
| Frekvens och affärsregler | Fas 4: Kampanj eller reseskapande | Om du vill kan du tillämpa regler för frekvensbegränsning för att förhindra att fler meddelanden skickas till flera samtidiga kampanjer |
| Konflikt- och prioritetshantering | Fas 4: Kampanj eller reseskapande | Tilldela prioritetspoäng och konfigurera konfliktlösning när flera kampanjer riktar sig till överlappande målgrupper |
| Rapportering och prestandaanalys | Fas 5: Rapportering och resultatanalys | Övervaka leveransstatistik via liverapporter under körningen och analysera kampanjens resultat via historiska rapporter efter slutförandet |

### [!DNL Real-Time CDP] (RT-CDP)

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Målgruppsutvärdering | Fas 1: Målgruppsutvärdering | Definiera målgruppsregler med Segment Builder eller Audience Composition, välj utvärderingsmetod (batch, streaming eller edge) och validera målgruppspopulationen |
| Verkställande av samtycke och styrning | Fas 1: Målgruppsutvärdering | Använd medgivandeinställningar och dataanvändningspolicyer för att säkerställa att endast godkända profiler tar emot kampanjmeddelandet |

## Förutsättningar

Slutför följande innan du börjar implementera.

- [ ] AJO-sandlådan har etablerats och är aktiv
- [ ] Den sändande underdomänen har delegerats och verifierats (SPF, DKIM, DMARC har konfigurerats)
- [ ] IP-pool har tilldelats och värms upp för produktionsvolym
- [ ] Det finns minst en aktiv kanalyta (e-post, SMS eller push)
- [ ] användarkonton har behörighet att skapa kampanjer/resor och skapa innehåll
- [ ] XDM-profilschemat innehåller attribut som behövs för målgruppssegmentering och meddelandepersonalisering
- [ ] XDM-händelseschemat hämtar konverteringshändelser för uppföljning efter kampanj
- [ ] profildata har importerats och sammanställts via identitetstjänsten
- [ ] Web SDK- eller Analytics-taggning är aktiv på CTA målsida för att hämta konverteringshändelser
- [ ] fält för samtycke fylls i i på profiler för målmeddelandekanalen
- [ ] Innehållsresurser (bilder, logotyper, riktlinjer för varumärken) är tillgängliga för meddelandedesign

## Implementeringsalternativ

I det här avsnittet beskrivs tre implementeringsalternativ för aktivering av utgående batchmeddelanden tillsammans med en jämförelse och riktlinjer för beslut.

### Alternativ A: Schemalagd kampanj (engångsbatchsändning)

**Bäst för:** Datumförankrade meddelanden - försäljningsmeddelanden, produktstarter, deadlines för registrering av evenemang, påminnelser om förnyelse, nyhetsbrev och alla sändningar där körningsdatumet är känt i förväg.

**Så här fungerar det:**

En schemalagd kampanj är den enklaste varianten av utgående batchmeddelanden. Marknadsföraren definierar målgruppen, författare till meddelandeinnehållet, anger ett sändningsdatum och -tid och aktiverar kampanjen. Vid den schemalagda körningen utvärderar AJO målgruppen för att fastställa den aktuella kvalificerade populationen och skickar sedan meddelandet till alla kvalificerande profiler i en enda batch.

Hela konfigurationen sker i AJO Campaigns-gränssnittet - det finns ingen arbetsyta, ingen förgrenade logik och inga väntesteg. Detta gör schemalagda kampanjer till det snabbaste och enklaste att konfigurera och hantera. Kampanjen kan ställas in för omedelbar körning, ett specifikt framtida datum/tid eller ett återkommande schema (varje dag, varje vecka, varje månad).

**Viktiga överväganden:**

- Målgruppen utvärderas vid körning, vilket innebär att profiler som är kvalificerade mellan schemaläggning och körning inkluderas
- Ingen förgrening, väntan eller logik för villkor är tillgänglig - meddelandet levereras till alla kvalificerande profiler
- Stöder innehållsexperiment (A/B-testning) direkt i kampanjkonfigurationen
- Kampanjegenskaperna innehåller en prioritetspoäng för konfliktlösning med andra kampanjer

**Fördelar:**

- Enklare konfiguration med minsta möjliga overhead
- Snabbaste start för enkla batchutskick
- Inbyggt stöd för återkommande scheman
- Experimentera med material
- Målgruppen omvärderades vid körningen för aktualitet

**Begränsningar:**

- Inga väntesteg, villkor eller förgreningar före leverans
- Det går inte att reagera på profilbeteende mellan schemaläggning och körning
- Endast en meddelandeåtgärd - inga multitouch-sekvenser
- Kan inte redigeras när den har aktiverats (måste dupliceras och ändras)

**Experience League:**

- [Kom igång med kampanjer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Skapa en kampanj](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)

### Alternativ B: Målgruppsinriktad resa

**Passar bäst för:** Beteendestyrda utskick - övergivna kundvagnsmeddelanden, påminnelser om att testperioden är slut, milstolpe-firande, kvalificeringsbaserad utträde och alla utskick där utlösaren är målgruppskvalifikation eller en affärshändelse i stället för ett kalenderdatum.

**Så här fungerar det:**

En målgruppsinriktad resa använder arbetsytan för att leverera ett meddelande när en profil kvalificerar sig för en viss målgrupp eller utlöser en kvalificerande händelse. Deltagandet av resan utlöses av ändringar av målgruppsmedlemskapet (profiler som kommer in i målgruppen) i stället för ett fast schema. Med arbetsytan för resan kan du välja väntesteg, villkorsgrenar och undertryckningslogik innan meddelandeåtgärden utförs, vilket ger större flexibilitet än en schemalagd kampanj.

Resan konfigureras i AJO Journeys gränssnitt med hjälp av händelsen Read Audience. När profiler är kvalificerade för målgruppen går de in på resan och går igenom arbetsytans noder. En enkel implementering kan bara innehålla en enda åtgärdsnod för e-post, vilket gör den funktionellt lik en schemalagd kampanj men med en tidsbaserad ingång för målgruppskvalificering. Mer komplexa implementeringar kan lägga till väntenoder (t.ex. vänta 24 timmar efter kvalificeringen), villkorsnoder (t.ex. kontrollera om profilen öppnat ett tidigare e-postmeddelande) eller undertryckningslogik innan meddelandet levereras.

**Viktiga överväganden:**

- Reseposten aktiveras av målgruppskvalifikation, inte av ett kalenderdatum
- Färdens arbetsyta har stöd för väntetider, villkor och delade noder för logik före leverans
- Reglerna för återinträde på resan styr om profiler kan komma in på resan flera gånger
- Skiljevägsinställningarna för resan avgör beteendet när en profil redan befinner sig på en konkurrerande resa

**Fördelar:**

- Flexibel timing baserad på målgruppskvalifikation snarare än fast tidsplan
- Vänta- och villkorsnoderna tillåter logik för förleverans (t.ex. fördröjning, kontroll, utelämna)
- Kontroller för återinträde förhindrar dubblettöverföringar till samma profil
- Kan utökas till en resa i flera steg om användningsexemplet utvecklas
- Stöder rapportering på kundnivå med värden för ingångs-, avslutnings- och nodnivå

**Begränsningar:**

- Mer konfigurationsinformation än en schemalagd kampanj
- Resans arbetsyta gör arbetet ännu mer komplext även vid användning av enstaka meddelanden
- Resan måste publiceras och kan inte redigeras när den är aktiv (måste skapa en ny version)
- Begränsning av antalet profiler som anges i ett tidsfönster

**Experience League:**

- [Kom igång med resor](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Läs målgruppsresan](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)

### Alternativ C: API-utlöst kampanj

**Bäst för:** Systeminitierade meddelanden skickar - orderbekräftelse med merförsäljningsinnehåll, uppföljning av matchning av supportärenden, transaktionsmeddelanden med marknadsföringsinnehåll och alla sändningar där den utlösande händelsen kommer från ett externt system vid ett visst tillfälle.

**Så här fungerar det:**

En API-utlöst kampanj aktiveras via ett REST API-anrop när en utlösande systemhändelse inträffar. Kampanjen är förkonfigurerad i AJO med meddelandeinnehåll och kanalinställningar, men i stället för att binda en fördefinierad målgrupp anger API-anropet mottagarprofilerna och kan skicka kontextuella data som fyller i dynamiska meddelandeparametrar.

Den här varianten är idealisk när sändningstidpunkten bestäms av ett externt system (t.ex. ett orderhanteringssystem, ett CRM-arbetsflöde eller en supportplattform) i stället för av målgruppsutvärdering eller ett kalenderschema. Sammanhangsberoende data som skickas i API:t utlöser nyttolast - som orderdetaljer, biljettnummer eller produktnamn - kan anpassa meddelandeinnehållet med kontextuella attribut som inte lagras i profilen.

**Viktiga överväganden:**

- Ingen förbunden målgrupp krävs - mottagarna anges i API-utlösarbegäran
- Sammanhangsberoende data i utlösarnyttolasten möjliggör dynamisk personalisering utöver profilattribut
- Kampanjen måste vara av typen API-utlöst och måste aktiveras innan den kan ta emot utlösarbegäranden
- Varje API-utlösarbegäran stöder upp till 20 profilmottagare
- Målgruppsutvärdering (fas 1) kan hoppas över eftersom mottagarna kommer från API-anropet

**Fördelar:**

- Utlösande i realtid från externa system vid tidpunkten för händelsen
- Sammanhangsbaserad personalisering med data som inte är lagrade i profilen (beställningsinformation, biljettinformation)
- Inga omkostnader för målgruppsutvärdering - mottagarna anges direkt
- Stöder transaktionsmeddelanden och hybrid-meddelanden för marknadsföring

**Begränsningar:**

- Kräver extern systemintegrering för att skicka API-utlösaren
- Maximalt 20 mottagare per API-utlösarbegäran
- Ingen inbyggd målgruppsutvärdering - det anropande systemet måste avgöra mottagarna
- Mer teknisk komplexitet tack vare API-integreringskrav
- Innehållsexperiment stöds inte för API-utlösta kampanjer

**Experience League:**

- [API-utlösta kampanjer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/api-triggered-campaigns/api-triggered-campaigns)
- [Utlösa kampanjer med API:er](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/api-triggered-campaigns/api-triggered-campaigns)

### Jämförelse av alternativ

I följande tabell jämförs de tre implementeringsalternativen över de viktigaste kriterierna.

| Kriterier | Alternativ A: Schemalagd kampanj | Alternativ B: Målgruppsutlöst resa | Alternativ C: API-utlöst kampanj |
| --- | --- | --- | --- |
| Bäst för | Datumförankrade utskick (kampanjer, lanseringar, nyhetsbrev) | Beteendestyrda utskick (kvalificeringshändelser, milstolpar) | Systeminitierade utskick (orderbekräftelser, transaktion) |
| Komplex | Lågt | Medelsvåra: | Medium-High |
| Utlösartyp | Kalenderdatum/tid eller återkommande schema | Målgruppskvalificering eller affärsevenemang | API-anrop för externt system |
| Förleveranslogik | Ingen | Vänta, villkor, delade noder är tillgängliga | Ingen (logik i anropande system) |
| Målgruppsbindning | Fördefinierad RT-CDP-publik | Fördefinierad RT-CDP-publik | Mottagare angivna i API-nyttolast |
| Sammanhangsberoende data | Endast profilattribut | Endast profilattribut | Profilattribut + API-nyttolastdata |
| Innehållsexperiment | Stöds | Stöds (vid meddelandeåtgärd) | Stöds inte |
| Frekvensbegränsning | Stöds | Stöds | Stöds |
| Kontroll av återinträde | Ej tillämpligt (engångskörning) | Konfigurerbara regler för återregistrering | Ej tillämpligt (per begäran) |
| Konfigurationsgränssnitt | AJO Campaigns | AJO Journeys | AJO Campaigns + externt system |
| Kräver | Målgrupp, kanalyta, budskap | Målgrupp, kanalyta, meddelande, arbetsyta för resan | Kanalyta, meddelande, API-integrering |

### Välj rätt alternativ

Använd följande beslutsflöde för att välja lämpligt implementeringsalternativ:

1. **Utlöses sändningen av en extern systemhändelse (t.ex. beställning placerad, biljett löst)?** Om ja, välj **Alternativ C: API-utlöst kampanj**. Det här är det enda alternativet som stöder systeminitierade utlösare med kontextuella nyttolastdata.

2. **Är sändningen förankrad till ett visst kalenderdatum eller ett återkommande schema?** Om ja, välj **Alternativ A: Schemalagd kampanj**. Det här är det enklaste och snabbaste sättet att konfigurera för datumdrivna meddelanden.

3. **Behöver sändningen reagera på målgruppsklassificering eller kräva logik för förleverans (vänta, villkor, inaktivering)?** Om ja, välj **Alternativ B: Målgruppsutlöst resa**. Resans arbetsyta ger flexibilitet för beteendestyrd inmatning och beslutslogik före leverans.

4. **Är sändningen en enkel sändning till en känd publik utan särskilda krav på timing eller logik?** Välj **Alternativ A: Schemalagd kampanj** för den lägsta konfigurationsoverheadkostnaden.

## Implementeringsfaser

Detta avsnitt går igenom varje genomförandefas i detalj, inklusive beslutspunkter och alternativspecifik vägledning.

### Fas 1: Utvärdera målgruppen

**Programfunktion:** RT-CDP: Målgruppsutvärdering

Den här fasen definierar och utvärderar målgruppssegmentet som tar emot kampanjmeddelandet. Det avgör vilka profiler som kvalificerar sig för sändning baserat på profilattribut, beteendesignaler och undertryckningsregler.

>[!NOTE]
>För alternativ C (API-utlöst kampanj) kan den här fasen hoppas över om mottagarna anges helt i API-utlösarens nyttolast. Även kampanjer som triggas av API-funktioner har dock en dämpad publik som kan filtrera bort profiler som inte ska ta emot meddelanden.

#### Beslut: Målgruppskriterier

Vilka villkor definierar målgruppen? Vilka undertryckningsregler ska exkludera profiler?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Profilattributbaserad målgrupp | Målgruppen definieras av demografiska attribut, preferenser eller statusattribut | Lättaste att bygga; stöder alla utvärderingsmetoder |
| Beteendebaserad publik | Målgruppen definieras av åtgärder som vidtas (eller inte vidtas) inom ett tidsfönster | Kräver inmatning av händelsedata; tidsfönsterregler kan begränsa rätten till direktuppspelning |
| Målgruppskomposition (härledd publik) | Målgruppen kräver rangordnade, delade, exkluderade eller berikande åtgärder för flera olika målgrupper | Kraftfullare men endast gruppbaserad utvärdering; begränsat till 10 kompositioner per sandlåda |

#### Beslut: Utvärderingsmetod

Hur snabbt måste målgruppen uppdateras för att återspegla nya kvalificerings- eller diskvalificeringsprofiler?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Batchutvärdering | Schemalagda kampanjer där målgruppsaktualitet inom en dag är acceptabel, stora, komplexa målgrupper | Standard för de flesta segmenttyper; processer enligt ett dagligt schema eller on demand; stöder alla segmentregelfunktioner |
| Utvärdering av strömning | Målgruppsutlösta resor där profilerna måste gå in i nästan realtid när de kvalificerar sig | Automatiskt för giltiga segmentregeluttryck; alla segmenttyper är inte berättigade för strömning; nästan realtidsfördröjning (sekunder till minuter) |
| Edge-utvärdering | Inte typisk för det här mönstret (används för anpassning av samma sida) | Begränsat stöd för segmentregler; fördröjning i millisekunder; endast relevant om det kombineras med mönster för webbanpassning |

#### Beslut: Sammanslagningspolicy

Vilken sammanfogningsprincip ska målgruppen använda för att lösa profilfragment?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Standardprincip för sammanfogning (tidsstämpelordning har ordnats) | De vanligaste användningsfallen för batchkampanjer | Det senaste attributvärdet vinner; standard för utgående meddelanden |
| Anpassad sammanfogningsprincip (datauppsättningsprioritet) | När en viss datakälla ska prioriteras för nyckelattribut | Användbart när CRM-data ska åsidosätta webbinsamlade data för vissa fält |

#### Gränssnittsnavigering

Kund > Publiker > Skapa målgrupp > Skapa regel

#### Information om nyckelkonfiguration

- Definiera målgruppen med hjälp av segmentverktyget med segmentregler för profilattribut, beteendehändelser och segmentmedlemskap
- Använd undertryckningsregler för att exkludera profiler som redan har konverterats, nyligen fått ett liknande meddelande eller som har avanmält sig
- Kontrollera att målgruppen har en population som inte är noll innan du fortsätter
- För batchkampanjer måste du se till att ett utvärderingsschema för segment är aktivt eller aktivera utvärdering på begäran
- Bekräfta medgivandefält (`consents.marketing.email.val`, `consents.marketing.sms.val` osv.) fylls i och används

#### Var alternativen skiljer sig

**För alternativ A (schemalagd kampanj):**

Batchutvärderingen är normal. Publiken utvärderas på nytt när kampanjen körs, vilket innebär att den mest aktuella kvalificerande populationen är riktad. Definiera målgruppen och kontrollera dess populationer och fortsätt sedan att skapa kampanjer.

**För alternativ B (målgrupputlöst resa):**

Direktuppspelningsutvärdering är att föredra så att profiler går in på resan när de kvalificerar sig. Kontrollera att segmentregeluttrycket är direktuppspelningsbart (enkla händelseutlösare, attributjämförelser, tidsbegränsade fönster). Konfigurera målgruppen och verifiera att direktuppspelningskvalifikationen är aktiv.

**För alternativ C (API-utlöst kampanj):**

Målgruppsutvärderingen kan hoppas över helt. Om det används skapar du en nedtryckande målgrupp för att filtrera profiler som inte ska få meddelandet (t.ex. nyligen avbruten prenumeration, redan konverterad). Det anropande systemet avgör de primära mottagarna.

#### Experience League-dokumentation

- [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Direktuppspelningssegmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Målgruppssammansättning](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Profile Query Language referens](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### Fas 2: Konfigurera kanalen

**Programfunktion:** AJO: Kanalkonfiguration

Den här fasen validerar eller skapar kanalytan (förinställningen) som definierar den sändande infrastrukturen för meddelandet - underdomän, IP-pool, avsändaridentitet, svarsadress och inställningar för att avbryta prenumerationen. Det måste finnas en giltig kanalyta innan meddelandeinnehåll kan skapas eller kampanjer kan aktiveras.

#### Beslut: Målkanal

Vilken meddelandekanal levererar kampanjmeddelandet?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| E-post | De flesta kampanjtyper - nyhetsbrev, kampanjer, meddelanden, förnyelser | Kräver delegerad underdomän, värmad IP-pool, avsändaridentitet och konfiguration för att avbryta prenumeration |
| SMS | Tidskänsliga eller korta meddelanden - blixtförsäljning, påminnelser om möten, engångskoder | Kräver autentiseringsuppgifter för SMS-provider (Sinch, Twilio eller Infobip), högre kostnad per meddelande, striktare krav på medgivande |
| Push-meddelande | Engagerade målgrupper - appuppdateringar, platsbaserade erbjudanden, funktionsmeddelanden i appen | Kräver APN:er (iOS) och/eller FCM-autentiseringsuppgifter (Android). Användarna måste ha appen installerad med push-behörighet |

#### Beslut: Markering av kanalyta

Finns det redan en lämplig kanalyta i sandlådan, eller måste en ny skapas?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Återanvänd befintlig yta | En verifierad, aktiv yta matchar den underdomän, avsändaridentitet och kanaltyp som krävs | Snabbaste sökväg; ingen DNS- eller Warmup-konfiguration behövs |
| Skapa ny yta | Ingen befintlig yta uppfyller kraven eller så behövs en ny underdomän-/avsändaridentitet | Kräver underdomänsdelegering, DNS-verifiering, IP-pooltilldelning och eventuell IP-värmare (2-4 veckor för nya IP-adresser) |

#### Beslut: Avbeställ hanteringen

Hur ska avanmälan hanteras på kanalytan?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Rubrik för att avsluta prenumeration med ett klick | Standard för alla marknadsföringsmeddelanden; krävs av större Internet-leverantörer (Gmail, Yahoo) för leveransbarhet | Lägger till ett mailto- eller URL-baserat prenumerationshuvud som Internet-leverantörer använder som en &quot;Unsubscribe&quot;-knapp |
| Avbeställ länk i e-postbrödtext | Krävs som reserv för e-postklienter som inte har stöd för rubriker för att avbryta prenumerationen på listor | Ta med en länk för att avbryta prenumerationen i e-postsidfoten bredvid sidhuvudet för att avbryta prenumerationen |
| Båda (rekommenderas) | Bästa praxis för alla marknadsföringsmejl | Maximal efterlevnadstäckning och bästa leveransprofil |

#### Gränssnittsnavigering

Administration > Kanaler > Kanalytor > Skapa yta (eller markera befintlig)

#### Information om nyckelkonfiguration

- För e-post: bind den sändande underdomänen, IP-poolen, avsändarens namn, avsändarens e-postadress, svarsadressen och BCC-adressen (om en granskningskopia krävs)
- För SMS: konfigurera autentiseringsuppgifter för SMS-provider och inställningar för kort kod eller lång kod
- För push: konfigurera APN och/eller FCM-autentiseringsuppgifter med programmets certifikat eller servernyckel
- Kontrollera att kanalytan har statusen &quot;Aktiv&quot; innan du fortsätter
- Bekräfta att DNS-poster (SPF, DKIM, DMARC) är korrekt konfigurerade för den sändande underdomänen
- Granska suppressionslistan för gamla poster. Rensa före aktivering

#### Experience League-dokumentation

- [Kom igång med e-postkonfiguration](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegera underdomäner](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Skapa IP-pooler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [Planer för IP-värmare](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Inställningar för e-postyta](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Konfigurera SMS-kanal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Konfigurera kanal för push-meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [Hantera undertryckningslista](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Fas 3: Skriv meddelandet

**Programfunktion:** AJO: Meddelanderedigering

I den här fasen skapas det meddelandeinnehåll som ska levereras till målgruppen. Det innefattar att välja eller skapa en innehållsmall, utforma meddelandelayouten, lägga till personalisering med profilattribut, konfigurera villkorsstyrt innehåll för målgruppsspecifika variationer, skapa återanvändbara innehållsfragment och förhandsgranska/testa meddelandet med exempelprofiler.

#### Beslut: Innehållsstrategi

Hur ska meddelandeinnehållet skapas?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Starta från befintlig mall | Det finns varumärkesgodkända mallar som matchar meddelandetypen (kampanj, transaktion, nyhetsbrev) | Den snabbaste utvecklingsvägen; säkerställer varumärkets enhetlighet; mallarna är sandlådespecifika |
| Designa från grunden | Det finns ingen lämplig mall eller så krävs en unik layout för meddelandet | Mer flexibilitet men mer arbete - spara som en mall för återanvändning |
| Importera HTML | Meddelandedesignen skapades externt (t.ex. i ett designverktyg) och HTML är klart för import | Bevarar extern design; kan behöva justeras för AJO-kompatibilitets- och personaliseringstoken |

#### Beslut: Personalization-djup

Vilka profilattribut ska personalisera meddelandet och behövs villkorliga innehållsblock?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Grundläggande personalisering (namn, hälsning) | Enkla kampanjer där generiskt innehåll med en personlig hälsning är tillräckligt | Låg insats; minimal risk för återgivningsproblem; använder standardprofilattribut |
| Attributbaserad personalisering | Meddelandeinnehållet varierar beroende på profilattribut (nivå, inställning, plats) | Kräver verifierade XDM-sökvägar; testa med flera profiler för att se till att alla variationer återges korrekt |
| Villkorliga innehållsblock | Olika innehållsavsnitt måste visas för olika målgruppssegment i samma meddelande | Mer komplex redigering; varje villkor kräver en standardreserv; testa alla permutationer |
| Sammanhangsbaserad personalisering (endast alternativ C) | API-utlösta kampanjer måste återge data som skickas i utlösarens nyttolast (orderinformation, biljettinformation) | Sammanhangsberoende attribut lagras inte i profilen. Definiera platshållare i meddelandet och mappa till nyttolastfält |

#### Beslut: Fragmentstrategi

Ska delade innehållsblock skapas som återanvändbara fragment?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Återanvändbara fragment | Sidhuvuden, sidfötter, friskrivningsklausuler och block för att avbryta prenumerationen delas upp i flera kampanjer | Ändringar av ett fragment sprids till alla meddelanden som refererar till det (live och utkast); maximalt 30 fragment per meddelande |
| Textbundet innehåll | Enkelt meddelande utan gemensamma element för andra kampanjer | Enklare för enstaka användning; ingen spridningsrisk |

#### Gränssnittsnavigering

Campaigns > Select campaign > Edit content > Email Designer (eller SMS/Push editor)

#### Information om nyckelkonfiguration

- Utforma meddelandelayouten med dra-och-släpp-innehållskomponenter (text, bild, knapp, avgränsare, spalter)
- Ange egenskaper för e-postrubrik: ämnesrad, prerubriktext och avsändaryta
- Infoga personaliseringsuttryck med hjälp av Handlebars syntax (t.ex. `{{profile.person.name.firstName}}`)
- Konfigurera hjälpfunktioner för formatering (datum, nummer, strängändring)
- Lägg till regler för villkorat innehåll för att visa olika innehåll baserat på profilattribut eller segmentmedlemskap
- Konfigurera standardreservinnehåll när inga villkor uppfylls
- Skriv meddelandetexten inom teckenbegränsningen för SMS
- Konfigurera rubrik, brödtext, bild och åtgärd (djuplänk eller URL) för push-meddelanden
- Förhandsgranska meddelandet med exempelprofiler för att verifiera återgivning av personalisering
- Skicka korrekturmeddelanden till interna intressenter för granskning
- Testa återgivning mellan e-postklienter med hjälp av e-poståtergivningsfunktionen

#### Experience League-dokumentation

- [Skapa ett e-postmeddelande](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [Designa e-postinnehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Använda e-postinnehållskomponenter för Designer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/content-components)
- [Lägg till personalisering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization syntax](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Hjälpfunktioner](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Dynamiskt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Arbeta med innehållsmallar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Arbeta med innehållsfragment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Förhandsgranska och testa ditt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [Skicka e-postkorrektur](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/proofs)
- [E-poståtergivning](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/email-rendering)
- [Skapa ett SMS-meddelande](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/create-sms)
- [Utforma ett push-meddelande](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/design-push)

### Fas 4: Skapa kampanjen eller resan

**Programfunktion:** AJO: Kampanjkörning (alternativ A och C) eller AJO: Journey Orchestration (alternativ B)

Den här fasen skapar kampanjen eller resan som binder målgruppen, meddelandet och exekveringsmekanismen till en slutprodukt. Det är här som de tre implementeringsalternativen skiljer sig mest åt.

#### Beslut: Innehållsexperiment

Ska kampanjen innehålla ett A/B-test eller multivariata experiment för att optimera meddelandets prestanda?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Inget experiment | En meddelandevariant med stor självförtroende för innehållets effektivitet | Enklare konfiguration, snabbaste aktivering |
| A/B-test (2 varianter) | Testa ärenderader, CTA:er eller innehållslayouter med en tydlig hypotes | Delad trafik 50/50 eller med viktad fördelning; kräver tillräcklig målgruppsstorlek för statistisk signifikans |
| Multivariata tester (3+ varianter) | Testa flera innehållselement samtidigt | Kräver större målgrupper, längre varaktighet för att nå konfidensgräns, högst 10 behandlingar per experiment |

#### Beslut: Frekvensbegränsning

Bör kampanjen följa globala regler för frekvensbegränsning för att förhindra övermeddelanden?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Använd frekvensregler | Campaign ingår i ett större meddelandeprogram med flera samtidiga utskick | Hindrar kundens trötthet. Profiler som överskrider taket inaktiveras från leverans |
| Undanta från begränsning | Kampanjen är tidskritisk eller transaktionskritisk och måste nå alla kvalificerande profiler oavsett meddelandehistorik | Undanta kampanjer från frekvensregler och utsätt dem för risker vid överbudande |

#### Beslut: Prioritet

Vilken prioritetsnivå ska den här kampanjen ha i förhållande till andra aktiva kampanjer?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Hög prioritet (75-100) | Kritiska kampanjer - större produktlanseringar, tidsbegränsade erbjudanden, meddelanden från myndigheter | Prioriterar kampanjer med lägre prioritet när konflikter uppstår |
| Medium prioritet (25-74) | Standardkampanjer - nyhetsbrev, engagemangskampanjer, allmänna kampanjer | Balanserad mot andra kampanjer. Kan ignoreras om en kampanjkonflikt med högre prioritet uppstår |
| Låg prioritet (0-24) | Bra att ha - informativa uppdateringar, specialerbjudanden | Kommer att undertryckas till förmån för högprioriterade kampanjer |

#### Var alternativen skiljer sig

**För alternativ A (schemalagd kampanj):**

**Gränssnittsnavigering:** Kampanjer > Skapa kampanj > Schemalagd > Marknadsföring

1. Skapa en ny schemalagd marknadsföringskampanj
2. Välj målgrupp från målgruppsväljaren
3. Markera kanalytan och länka det skapade meddelandeinnehållet
4. Konfigurera körningsschemat: omedelbart, specifikt datum/tid eller återkommande
5. Aktivera innehållsexperimenterande och definiera behandlingsvarianter som tillval
6. Konfigurera frekvensbegränsning och prioritetspoäng (valfritt)
7. Granska den fullständiga kampanjkonfigurationen
8. Aktivera kampanjen

**För alternativ B (målgrupputlöst resa):**

**Gränssnittsnavigering:** Resor > Skapa resa

1. Skapa en ny resa med tävlingsbidraget&quot;Läs målgrupp&quot;
2. Välj målgruppen som startkälla
3. Konfigurera regler för återinträde (tillåta återinträde, engångsinmatning eller återinträde efter vänteperioden)
4. Du kan också lägga till väntenoder (t.ex. vänta 24 timmar efter kvalificeringen)
5. Om du vill kan du lägga till villkorsnoder (t.ex. kontrollera om profilen uppfyller ytterligare villkor)
6. Lägg till meddelandeåtgärdsnoden och markera kanalytan och det redigerade innehållet
7. Konfigurera avslutsvillkor (t.ex. profilkonverteringar, avabonnemang på profiler)
8. Alternativt kan du aktivera innehållsexperiment i meddelandeåtgärden
9. Granska och publicera resan

**För alternativ C (API-utlöst kampanj):**

**Gränssnittsnavigering:** Kampanjer > Skapa kampanj > API-utlöst

1. Skapa en ny API-utlöst kampanj
2. Markera kanalytan och länka det skapade meddelandeinnehållet
3. Konfigurera kontextuella personaliseringstoken för data som ska skickas i API-utlösarnyttolasten
4. Granska och aktivera kampanjen
5. Observera kampanj-ID:t som ska användas i det externa systemets API-utlösarintegrering
6. Det anropande systemet skickar utlösarbegäranden till kampanjslutpunkten med mottagarprofiler och kontextuella data

#### Experience League-dokumentation

- [Skapa en kampanj](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Kom igång med kampanjer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [API-utlösta kampanjer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/api-triggered-campaigns/api-triggered-campaigns)
- [Kom igång med resor](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Läs målgruppsresan](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Kom igång med innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Skapa ett innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Frekvensregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Prioritetspoäng](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Identifiera potentiella konflikter](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)

### Fas 5: Analysera rapportering och resultat

**Programfunktion:** AJO: Rapporterings- och prestandaanalys

Den här fasen övervakar leveransstatistik under körning via liverapporter och analyserar kampanjresultat efter slutförande via historiska rapporter. Om du vill kan du konfigurera CJA-integrering för djupare flerkanalsanalyser.

#### Beslut: Rapporteringsmetod

Vilken rapporteringsnivå krävs för den här kampanjen?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Endast inbyggda AJO-rapporter | Standardmått för leverans och engagemang är tillräckliga (skickat, levererat, öppningar, klick, studsar) | Ingen ytterligare konfiguration. Rapporter är inbyggda i gränssnittet för kampanj/resa |
| AJO-rapporter + CJA-analys | Konsekvensanalys över flera kanaler, attribueringsmodellering eller funnel-analys behövs utöver leveransstatistik | Kräver en CJA-anslutning och datavy som är länkad till AJO datamängder; ger större analyskapacitet |
| CJA programmatiska rapporter | Automatiska instrumentpaneler eller schemalagd rapportleverans krävs för intressenter | Kräver API-integrering för CJA Reporting, användbart för chefsinstrumentpaneler och återkommande prestandasammanfattningar |

#### Beslut: Konverteringsspårning

Hur mäts framgångarna i kampanjer utöver leverans- och engagemangsmått?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Ingen konverteringsspårning | Kampanjmålet är medvetenhet eller engagemang (öppningar, klick) utan någon specifik åtgärd längre fram i kedjan | Enklare; ingen ytterligare händelsespårning krävs |
| Webbkonverteringsspårning | Campaign CTA länkar till en webbsida där konverteringshändelser (inköp, registrering, formulärsändning) spåras | Kräver Web SDK- eller Analytics-taggning på målsidan. Händelser måste samlas in i AEP datamängder |
| Anpassad konverteringshändelse | Kampanjens framgång mäts av en affärsspecifik händelse som inte fångats in på webben (t.ex. köp i butiken, interaktion med callcenter) | Kräver att den anpassade händelsen hämtas till AEP och inkluderas i rapporteringsdatamängder |

#### Gränssnittsnavigering

- Live-rapporter: Kampanjer > Välj kampanj > Live-rapport (eller Resor > Välj resa > Live-rapport)
- Historiska rapporter: Kampanjer > Välj kampanj > Alla tidsrapporter (eller Resor > Välj resa > Alla tidsrapporter)

#### Information om nyckelkonfiguration

- Få tillgång till liverapporter under kampanjkörningen för att övervaka leveranser i realtid och engagemang
- Granska nyckeltal: Skickat, Levererat, studsar, Öppnar, klickar, Avbeställer (e-post); Skickat, Levererat, Klickningar, Fel (SMS); Skickat, Levererat, Öppnar, Åtgärder (push)
- Efter kampanjens slut kan du få tillgång till historiska rapporter (hela tiden) för en omfattande analys
- Analysera leveransen av funnel: Riktat > Skickat > Levererat > Öppnar > Klickningar
- Granska fel och uteslutningsorsaker för att identifiera leveransproblem
- Om innehållsexperimenterande har aktiverats kan du granska experimentresultatet och vänta på statistisk tillförsikt innan du deklarerar en vinnare
- För integrering med CJA kontrollerar du att AJO datavy innehåller relevanta AJO-datauppsättningar (händelsedatauppsättning för meddelandefeedback, händelsedatauppsättning för e-postspårning)

#### Experience League-dokumentation

- [Kampanjrapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Global kampanjrapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Rapport om livesändning på resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Global reserapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Rapport om innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Arbeta med Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Integreringsguide för AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

## Implementeringsöverväganden

Detta avsnitt behandlar skyddsförslag, vanliga fallgropar, bästa praxis och beslut om kompromisser.

### Gardrutor och begränsningar

- Max 500 aktiva live-kampanjer per sandlåda - [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Max 4 000 segmentdefinitioner per sandlåda - [Kundprofilsgardiner i realtid](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Högst 10 kanalytor per kanaltyp per sandlåda
- API-utlösta kampanjer har stöd för upp till 20 profilmottagare per utlösarbegäran
- Det går inte att redigera kampanjer när de har aktiverats - duplicera och ändra i stället
- Live-rapporter uppdateras var 60:e sekund och visar de senaste 24 timmarna med data
- Historikrapporter kan ta upp till två timmar att fylla i fullt ut efter att kampanjen har slutförts
- Maximalt 10 behandlingar (varianter) per innehållsexperiment
- Max 10 takkonfigurationer per sandlåda
- Högst 30 innehållsfragment per meddelande
- Maximal e-poststorlek på 100 kB rekommenderas för optimal leverans
- IP-uppvärmningsplaner bör öka volymen gradvis under 2-4 veckor för nya IP-adresser
- Poster i Suppression-listan sparas under en konfigurerbar period (14 dagar för mjuka studsar som standard)

### Vanliga fallgropar

- **Om du skickar innan IP-värmningen är klar:** Nya IP-adresser som skickar stora volymer omedelbart flaggas av Internet-leverantörer, vilket resulterar i dålig leveransförmåga och potentiell svartlistning. Slutför alltid en IP-värmare innan produktionen skickar nya IP-adresser.

- **Testar inte personalisering för flera profiler:** Personalization-tokens som fungerar för en testprofil kan misslyckas för andra om den refererade XDM-sökvägen inte finns eller är null för vissa profiler. Förhandsgranska alltid med flera testprofiler som representerar olika nivåer för datafullständighet.

- **Hoppar över granskning av undertryckningslista:** Inaktuella poster i undertryckningslistan kan blockera leverans till giltiga adresser, medan poster som saknas kan leda till leverans till ogiltiga adresser som genererar studsar. Granska och rensa suppressionslistan före större kampanjer.

- **Frekvensbegränsning för kampanjkampanjer ignoreras:** Om du skickar en kampanjkampanj utan frekvensbegränsning medan andra kampanjer också är aktiva kan det leda till att profiler får flera meddelanden under en kort period, vilket leder till att prenumerationer avbryts och skräppost besvaras.

- **Schemaläggning av kampanjer utan verifiering av målgruppspopulationen:** Om en kampanj aktiveras innan målgruppen bekräftas får målgruppen ett icke-nollutvärderat populationsresultat i nollmeddelanden. Kontrollera alltid målgruppens storlek före aktivering.

- **Använda batchutvärdering för målgruppsutlösta resor:** Om resan använder en Read Audience-post med batchutvärdering kommer profiler inte att anges i nästan realtid. Använd direktuppspelningsutvärdering för målgruppen när det krävs närapå-realtidsinträde.

- **Konfidentiellt samtycke inte konfigureras:** Att skicka meddelanden till profiler utan giltigt marknadsföringsmedgivande bryter mot reglerna och skadeståndsanseendet. Se till att godkännandefält fylls i och används på kanalytnivå.

### God praxis

- Börja med alternativ A (Scheduled Campaign) för enkla sändningsfall och ta examen i alternativ B (Audience-Triggered Journey) endast när förleveranslogik eller beteendestyrd timing behövs
- Inkludera alltid både en sida med en klickning och en länk för att avbryta prenumerationen i e-postmeddelandetexten för maximal kompatibilitet
- Skapa återanvändbara innehållsfragment för sidhuvuden, sidfötter och friskrivningsklausuler för att säkerställa enhetliga kampanjer
- Ange regler för frekvensbegränsning innan kampanjer aktiveras för att förhindra att meddelanden skickas samtidigt
- Använd innehållsexperimenterande för att optimera ämnesrader och CTA:er, börja med A/B-tester innan du går vidare till multivariata experiment
- Tilldela prioritetspoäng till alla aktiva kampanjer för att säkerställa en konsekvent konfliktlösning
- Schemalägg batchutvärdering som ska slutföras innan kampanjen körs för att säkerställa nya målgruppsdata
- Skicka korrekturmeddelanden och använd e-poståtergivningsfunktionen för att kontrollera att meddelandet visas korrekt i alla e-postklienter före aktivering
- Övervaka liverapporten omedelbart efter kampanjaktiveringen för att fånga upp leveransproblem tidigt
- Arkivera kampanjkonfigurationer och experimentera med resultat för framtida referens och kontinuerlig optimering

### Avvecklingsbeslut

Följande kompromisser bör utvärderas när du gör implementeringsval.

#### Enkelhet jämfört med flexibilitet

Schemalagda kampanjer (alternativ A) erbjuder den enklaste konfigurationen men ingen logik för förleverans. Målgruppsutlösta resor (alternativ B) ger logik före leverans men ökar komplexiteten i konfigurationen.

- **Alternativ A prioriterar:** Starthastighet, enkel drift, självbetjäning för marknadsförare
- **Alternativ B prioriterar:** Beteendeanpassning, villkorsstyrd nedtryckning, utbyggbarhet för flerstegsresor
- **Rekommendation:** Börja med alternativ A för enkla utskick. Byt bara till alternativ B när användningsfallet verkligen kräver väntetid, villkor eller förgreningslogik före leverans. Undvik att använda arbetsytan för enkla batchutskick som inte har någon nytta av orkestreringsfunktioner.

#### Målgruppens aktualitet kontra utvärderingskostnad

Direktuppspelningsutvärdering ger nästan realtidsuppdateringar men har begränsningar för segmentregler. Batchutvärderingen stöder alla segmentregelfunktioner men utvärderas enligt ett dagligt schema.

- **Direktuppspelning prioriterar:** Tidlighet, beteendestyrd precision, målgruppsinställd resepost
- **Batch-tjänster:** Komplex målgruppslogik, stora populationer, lägre omkostnader för utvärdering
- **Rekommendation:** Använd batchutvärdering för schemalagda kampanjer (alternativ A) där daglig aktualitet är tillräcklig. Använd direktuppspelningsutvärdering för målgruppsinlösta resor (alternativ B) där profilerna måste anges när de kvalificerar sig. Om målgruppssegmentregeluttrycket inte är direktuppspelningsbart strukturerar du om reglerna eller accepterar batchnivåfördröjning.

#### Personalization djupdesign jämfört med redigeringskomplexitet

Djupare personalisering (villkorsstyrt innehåll, dynamiska avsnitt) förbättrar engagemanget men ökar arbetet med att skapa och testa.

- **Djupa personaliseringsfördelar:** Högre engagemangsgrad, mer relevant kundupplevelse, bättre konvertering
- **Enkel personalisering prioriterar:** Snabbare start, lägre testningsbörda, minskad risk för återgivningsfel
- **Rekommendation:** Börja med grundläggande personalisering (förnamn, relevant produktkategori) och lager i villkorsstyrt innehåll som baseras på uppmätta prestandavinster. Testa alltid alla innehållsvariationer för flera testprofiler före aktivering.

#### Frekvenskontroll jämfört med meddelanderäckvidd

Strikta frekvensbegränsningar förhindrar att meddelanden skickas för mycket, men kan förhindra kampanjleverans till profiler som nyligen har tagit emot andra meddelanden.

- **Strikta capping-förmåner:** Kvalitet på kundupplevelsen, lägre avanmälningsfrekvens, varumärkets anseende
- **Avspänd begränsning:** Maximal räckvidd för meddelanden, högre totala visningar, kampanjtäckning
- **Rekommendation:** Aktivera alltid frekvensbegränsning för marknadsföringskampanjer. Ange kanalspecifika ändpunkter (t.ex. 3-5 e-postmeddelanden per vecka, 1-2 SMS per vecka). Undvik endast tidskritiska eller transaktionsstyrda meddelanden från regler om begränsning.

## Relaterad dokumentation

I det här avsnittet finns omfattande länkar till [!DNL Experience League]-dokumentation ordnade efter ämne.

### Kampanjer

- [Kom igång med kampanjer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Skapa en kampanj](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [API-utlösta kampanjer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/api-triggered-campaigns/api-triggered-campaigns)

### Resor

- [Kom igång med resor](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Läs målgruppsresan](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)

### Kanalkonfiguration

- [Kom igång med e-postkonfiguration](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegera underdomäner](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Skapa IP-pooler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [Planer för IP-värmare](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Inställningar för e-postyta](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Konfigurera SMS-kanal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Konfigurera kanal för push-meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [Hantera undertryckningslista](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Framtagning och personalisering av meddelanden

- [Skapa ett e-postmeddelande](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [Designa e-postinnehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Använda e-postinnehållskomponenter för Designer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/content-components)
- [Importera eller koda e-postinnehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/code-content)
- [Lägg till personalisering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization syntax](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Hjälpfunktioner](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Dynamiskt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)

### Innehållshantering

- [Arbeta med innehållsmallar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Arbeta med innehållsfragment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Förhandsgranska och testa ditt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [Skicka e-postkorrektur](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/proofs)
- [E-poståtergivning](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/email-rendering)

### Innehållsexperiment

- [Kom igång med innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Skapa ett innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Rapport om innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Statistikberäkningar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

### Hantering av frekvens och konflikter

- [Frekvensregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Översikt över affärsregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [Kom igång med konflikthantering och prioritetshantering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Prioritetspoäng](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Identifiera potentiella konflikter](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [Resegotypning och skiljeförfarande](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)

### Målgrupper och segmentering

- [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Direktuppspelningssegmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Edge segmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Målgruppssammansättning](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Profile Query Language referens](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### Rapporter

- [Kampanjrapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Global kampanjrapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Rapport om livesändning på resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Global reserapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Arbeta med Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Integreringsguide för AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

### Datastyrning och samtycke

- [Översikt över dataförvaltning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Översikt över etiketter för dataanvändning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/labels/overview)
- [Fältgruppen för samtycke och inställningar](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
- [Samtycke i Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### Datamodellering och identitet

- [XDM - systemöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Grundläggande om schemakomposition](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [Översikt över identitetstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Översikt över kopplingsprofiler](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### Skyddsräcken

- [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Garantier för kundprofiler i realtid](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Förvaringsskydd](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)

### Självstudiekurser och komma igång

- [Kom igång med Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/get-started)
- [Skapa din första kampanj](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Skapa den första resan](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
