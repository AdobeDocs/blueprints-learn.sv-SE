---
title: Händelseutlöst meddelanden
description: Lär dig hur du levererar sammanhangsbaserade meddelanden i realtid som svar på beteendehändelser eller systemhändelser.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 75137990-9848-40c0-abf3-adbd21d2de52
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '9040'
ht-degree: 1%

---

# Händelseutlösta meddelanden

Den här guiden innehåller en omfattande implementeringsplan för händelseutlösta meddelanden med [!DNL Adobe Journey Optimizer] (AJO), [!DNL Real-Time Customer Data Platform] (RT-CDP) och [!DNL Adobe Experience Platform] (AEP). Det är utformat för lösningsarkitekter, marknadsföringsteknologer och implementeringstekniker som behöver leverera sammanhangsbaserade meddelanden i realtid som svar på beteendeförändringar eller systemhändelser.

Använd den här vägledningen när du vill veta vad du ska konfigurera, var implementeringsalternativ finns och vilka kompromisser som styr varje beslut.

Guiden täcker hela livscykeln från händelsehantering och reseskapande till meddelandeleverans och resultatrapportering, med detaljerad beslutsvägledning för tre olika implementeringsalternativ.

## Använd ärendeöversikt

Händelseutlösta meddelanden levererar ett sammanhangsberoende meddelande som svar på en händelse i realtid som rör beteende eller system. Till skillnad från batchaktivering av utgående meddelanden, som skickar till en utvärderad målgrupp enligt ett schema, lyssnar mönstret efter en kvalificerande händelse - som att kunden överger en kundvagn, bläddrar, skickar in formulär eller ändrar systemstatusen - och registrerar omedelbart den utlösande profilen på en resa där villkoren utvärderas och ett meddelande skickas.

Mönstret bygger på händelseströmning i realtid till AEP (via Web SDK, Mobile SDK eller API:t på serversidan), en resa med en enda händelsepost i AJO, och logik för villkorsutvärdering som avgör om och vad som ska skickas. Meddelandet skickas vanligtvis inom några minuter efter den utlösande händelsen, vilket gör det här mönstret idealiskt för tidskänslig, sammanhangsberoende kommunikation.

Organisationer använder det här mönstret för att svara på kundåtgärder i realtid, vilket ökar relevansen och ökar engagemanget och konverteringsgraden jämfört med schemalagd batchkommunikation. Vanliga scenarier är bland annat övergiven kundvagnsåterställning, uppföljning efter inköp, välkomstmeddelanden efter registrering och tidskänsliga meddelanden som betalningsfel eller varningar om prisfall.

## Viktiga verksamhetsmål

Följande affärsmål stöds av det här användningsmönstret.

**[Återställ övergivna varukorgar och resor](../../business-objectives/customer-experience/recover-abandoned-carts-journeys.md)**

Engagera användare som slutade på grund av köp, ansökningar eller registreringar med skräddarsydda uppföljningar i rätt tid.

| KPI:er |
| --- |
| Konverteringsgrader, inkrementella intäkter, engagemang |

**[Öka konverteringsgraden](../../business-objectives/revenue-monetization/increase-conversion-rates.md)**

Förbättra andelen besökare och presumtiva som utför önskade åtgärder, t.ex. inköp, registreringar eller inskickade formulär.

| KPI:er |
| --- |
| Konverteringsgrader, leadkonvertering, kostnad per lead |

**[Leverera personaliserade kundupplevelser](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**

Skräddarsy innehåll, erbjudanden och budskap efter enskilda preferenser, beteenden och livscykelsteg.

| KPI:er |
| --- |
| Engagemang, konverteringsgrader, kundnöjdhet (CSAT) |

**[Förbättra kundintroduktionen](../../business-objectives/customer-experience/improve-customer-onboarding.md)**

Snabba upp time-to-value för nya kunder med smidiga, personaliserade välkomstupplevelser och aktiveringsresor.

| KPI:er |
| --- |
| Engagemang, lagring, konverteringsgrader |

## Exempel på taktiska användningsfall

Följande scenarier visar hur händelseutlösta meddelanden kan användas i olika affärskontexter.

- **E-post om att kunden överger kundvagnen eller SMS** - Skicka ett påminnelsemeddelande när kunden lägger till artiklar i kundvagnen men inte slutför köpet inom ett angivet tidsfönster
- **Bläddra bland övergivna uppföljningar** - Engagera besökare som visade produkter eller innehåll på nytt men inte vidtagit någon konverteringsåtgärd
- **Efterbeställning - tack eller korsförsäljning** - Leverera en bekräftelse och korsförsäljningsrekommendation omedelbart efter en köphändelse
- **Påminnelse om att utvärderingsversionen har gått ut** - Meddela användare att den kostnadsfria utvärderingsversionen snart har löpt ut med meddelanden om förnyelse eller konvertering
- **Välkomstmeddelande efter registrering** - Skicka ett meddelande om direkt introduktion när en ny användare registrerar eller skapar ett konto
- **Bekräftelse av inskickad blankett** - Bekräfta inskickade formulär (kontaktförfrågningar, ansökningar, registreringar) med en sammanhangsbaserad bekräftelse
- **Meddelande om betalningsfel** - Meddela kunder när en återkommande betalning misslyckas och uppmana dem att uppdatera betalningsinformationen
- **Push-meddelande för programavinstallation** - Utlös ett PIN-återkopplingsmeddelande när en användare avinstallerar ett mobilprogram
- **Bekräftelse av bokning eller avtalad tid** - Skicka direkt bekräftelse efter att en bokning, reservation eller avtalad tid har schemalagts
- **Varning om prisfall för önskelisteobjekt** - Meddela kunderna när en produkt i deras önskelista faller i pris

## Nyckeltal för prestanda

Följande nyckeltal hjälper till att mäta effektiviteten hos händelseutlösta meddelandeimplementeringar.

| KPI | Beskrivning | Mätningsmetod |
| --- | --- | --- |
| Konverteringsgrad | Procentandel utlösta meddelandemottagare som slutfört den önskade åtgärden (inköp, registrering, förnyelse) | Konverteringar/meddelanden* 100 |
| Inkrementell intäkt | Ytterligare intäkter som kan tillskrivas händelseutlösta meddelanden jämfört med kontrollgrupper som inte skickar | Intäkter från utlösta utskick - kontrollgruppens baslinje |
| Öppen kurs | Procentandel levererade meddelanden som öppnas av mottagarna | Öppnar/levereras * 100 |
| Klickfrekvens (CTR) | Procentandel levererade meddelanden som genererar minst ett klick | Klickningar/levererat * 100 |
| Tid till konvertering | Genomsnittlig förfluten tid mellan meddelandeleverans och konverteringshändelse | Genomsnittlig(tidsstämpel för konvertering - tidsstämpel för leverans) |
| Färdavslut | Procentandel profiler som går in på resan och når meddelandets leveranssteg (inte släppta av villkor eller utgångar) | Profiler som når leverans/profiler som tar sig in på resan * 100 |
| Undertryckningshastighet för meddelande | Procentandel av kvalificerade profiler som inaktiverats på grund av frekvensbegränsningar, samtycke eller villkorsutvärdering | Undertryckta profiler / Totalt antal kvalificerade profiler * 100 |
| Studsfrekvens | Procentandel meddelanden som inte kunde levereras på grund av hårda eller mjuka studsar | studsar/skickade * 100 |

## Använd skiftlägesmönster

I det här avsnittet beskrivs grundmönstret och funktionskedjan som driver händelseutlösta meddelanden.

**Meddelanden som utlösts av händelser**

Lyssna efter en händelse i realtid som rör beteende eller system och leverera sedan ett sammanhangsberoende meddelande till den utlösande profilen.

**Funktionskedja:** Händelseinmatning > Reseanmälan > Villkorsutvärdering > Meddelandeleverans > Rapportering

## Tillämpningar

Följande Adobe-program används i det här fallmönstret.

- **[!DNL Adobe Journey Optimizer](AJO)** - Resehantering med enhetlig händelseinmatning, villkorsutvärdering, väntesteg, meddelanderedigering, kanalkonfiguration, frekvensstyrning och leveransrapportering
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)** - Målgruppsutvärdering för villkorsbaserad filtrering inom resor, medgivande och styrning, profilanrikning
- **[!DNL Adobe Experience Platform](AEP)** - Inmatning av händelser i realtid via Web SDK, Mobile SDK eller API:t på serversidan; datamodellering; identitetsupplösning; Edge Network

## Foundationsfunktioner

Följande grundläggande funktioner måste finnas för det här användningsmönstret. För varje funktion anger statusen om den vanligtvis är obligatorisk, antas vara förkonfigurerad eller inte tillämplig.

| Foundational Function | Status | Vad måste finnas på plats | Experience League Reference |
| --- | --- | --- | --- |
| Administration och styrning | Antagen på plats | AJO-sandlådan har etablerats med konfiguration för aktiv kanal. Skapa och publicera behörigheter som tilldelats implementeringsteamet. Användarroller konfigurerade för resehantering, innehållsutveckling och kanaladministration. | [Översikt över sandlådor](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/home), [Översikt över åtkomstkontroll](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Datamodellering och förberedelse | Obligatoriskt | Ett XDM ExperienceEvent-schema måste fånga in den utlösande händelsen med alla kontextuella fält som behövs för villkorsutvärdering och meddelandepersonalisering (t.ex. `commerce.productListAdds` för kundvagnshändelser, produktinformation, kundvagnsvärde). Schemat måste aktiveras för kundprofil i realtid. En motsvarande datauppsättning måste skapas och profilaktiveras. | [Systemöversikt för XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [Grundläggande om schemakomposition](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| Datakällor och samling | Obligatoriskt | Händelseströmning i realtid måste konfigureras - Web SDK för webbhändelser, Mobile SDK för apphändelser eller Edge Network Server API för systemhändelser. En datastream måste konfigureras med AEP- och AJO-tjänster aktiverade, och händelser dirigeras till rätt datauppsättning. Detta är ett kritiskt beroende eftersom mönstret är beroende av händelseinmatning i realtid. | [Webböversikt för SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home), [Konfigurera dataströmmar](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure) |
| Konfiguration av identitet och profil | Obligatoriskt | Den utlösande händelsen måste associeras med en känd identitet (e-post, CRM-ID eller autentiserad session) så att resan kan matcha profilen och leverera meddelandet. Identitetsnamnutrymmen måste finnas för de identifierare som används av den utlösande händelsen. Anonyma händelser kräver identitetssammanfogning via identitetsdiagrammet innan ett meddelande kan levereras. En sammanfogningsprincip måste konfigureras. | [Översikt över identitetstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [Översikt över sammanslagningsprinciper](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| Målgruppsdefinition och segmentering | Rekommenderad | Även om det inte är absolut nödvändigt för händelseutlösta resor (bidraget är händelsebaserat, inte målgruppsbaserat), kan målgruppssegment användas för villkorsutvärdering under resan (t.ex. bara skicka om profilen finns i ett&quot;högt värde kund&quot;-segment, eller utelämna om profilen finns i ett&quot;nyligen kontaktat&quot; segment). Direktuppspelningsutvärdering rekommenderas för segmentmedlemskapskontroller i realtid under resor. | [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [Direktuppspelningssegmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation) |

## Stödfunktioner

Följande funktioner förstärker det här användningsmönstret, men behövs inte för att köra kärnan.

| Stödfunktioner | Status | Varför det spelar någon roll | Experience League Reference |
| --- | --- | --- | --- |
| Skapande av beräknat/härlett attribut | Rekommenderad | Beräknade attribut som antal kundavhopp, dagar sedan senaste köp, genomsnittligt ordervärde och total livstid förbättrar villkorsutvärderingen och personaliseringen inom triggade resor. Dessa beteendeaggregat möjliggör exaktare beslut om målinriktning (t.ex. att särskilja förstagångsövergivna personer från upprepade övergivna). | [Översikt över beräknade attribut](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| Livscykelhantering för data | Rekommenderad | Förfallodatum för händelsedata bör konfigureras för tillfälliga beteendehändelser (sidvisningar, sökningar, klickningar) för att hantera lagringskostnader och efterlevnad. Schemafält för samtycke måste finnas för kanalspecifik tvång för deltagande/avanmälan vid meddelandeleverans. | [Översikt över livscykelhantering av avancerade data](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home), [Giltighetsperioder för datauppsättningar](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration) |
| Dataanvändningsetiketter och -tillämpning | Rekommenderad | Myndighetsetiketter på händelse- och profilfält säkerställer korrekt personalisering. Om utlösta meddelanden innehåller personaliserat innehåll med hjälp av PII-data eller beteendedata bör dataanvändningsetiketter och styrningsprinciper granskas för att förhindra obehörig dataanvändning i meddelandeinnehåll. | [Översikt över datastyrning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [Översikt över etiketter för dataanvändning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/labels/overview) |
| Övervakning och observerbarhet | Ingår | Övervakning av körning på resa ingår i rapporteringsfasen. Konfigurera dessutom varningar för misslyckade händelseinmatningar eller fördröjningar av resebearbetningen för att upptäcka pipeline-problem som skulle förhindra att utlösta meddelanden skickas. | [Aviseringsöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview), [Översikt över Insikter i observabilitet](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| Rapportering och analys | Ingår | Rapporter om reseprestanda ingår i rapporteringsfasen. Om du vill få en djupare analys av hur väl utlösta meddelanden fungerar i olika kanaler och över tid kan du konfigurera CJA-anslutningar och arbetsytor för att analysera konverteringsattribuering, time-to-conversion och kanalprestanda. | [CJA - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [AJO + CJA - integreringsguide](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo) |

## Programfunktioner

I den här planen används följande funktioner från programfunktionskatalogen. Funktioner mappas till implementeringsfaser i stället för till numrerade steg.

### [!DNL Journey Optimizer] (AJO)

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Journey Orchestration | Reseskapande och konfiguration | Skapa en resa med Unitary Events-post, konfigurera kvalificerande händelse, lägg till villkorsnoder, väntesteg, meddelandeåtgärder, avslutsvillkor och regler för återinträde |
| Kanalkonfiguration | Kanalytinställningar | Konfigurera eller validera kanalytor (e-post, SMS, push) inklusive delegering av underdomäner, IP-pooler, avsändarinställningar och hantering av undertryckningslistor |
| Redigering av meddelanden | Skapa meddelandeinnehåll | Skapa sammanhangsbaserat meddelandeinnehåll med händelsestyrd personalisering, villkorsstyrt innehåll och återanvändbara fragment |
| Frekvens och affärsregler | Reseskapande och konfiguration (alternativ C) | Konfigurera regler för frekvensbegränsning och borttagning av dubbletter för att förhindra övermeddelanden från händelsekällor med hög frekvens |
| Konflikt- och prioritetshantering | Reseskapande och konfiguration | Tilldela prioritetspoäng och konfigurera konfliktidentifiering för resor som konkurrerar om samma profiler |
| Rapportering och prestandaanalys | Rapportering och övervakning | övervaka leveransstatistik för resan via live- och historiska rapporter; få tillgång till programmatiska prestandadata via CJA |

### [!DNL Real-Time CDP] (RT-CDP)

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Målgruppsutvärdering | Foundational Setup (F5) | Utvärdera målgruppssegment som används för villkorsbaserad filtrering inom resan (t.ex. värdefulla kundsegment, undertryckningssegment) |
| Verkställande av samtycke och styrning | Foundational Setup (S2/S3) | Använd samtyckesinställningar och styrningsprinciper för dataanvändning vid leverans av meddelanden för att säkerställa att kommunikationen blir korrekt |

## Förutsättningar

Slutför följande innan du påbörjar implementeringen.

- [ ] AJO-sandlådan har etablerats med behörighet att skapa och publicera resor (F1)
- [ ] XDM ExperienceEvent-schema som fångar in den utlösande händelsen med sammanhangsberoende fält, aktiverat för kundprofil i realtid (F2)
- [ ] Händelseströmning i realtid konfigurerad via Web SDK, Mobile SDK eller Edge Network Server API med datastream-routningshändelser till rätt AEP-datauppsättning (F3)
- [ ] Identitetsnamnutrymmen har konfigurerats för identifierarna för den utlösande händelsen; regler för identitetslänkning finns på plats (F4)
- [ Kanalytan ] (e-post, SMS eller push) har konfigurerats och validerats med en lyckad testsändning
- [ ] Meddelandeinnehåll som har skapats, granskats och testats med exempelprofiler
- [ ] Samtyckesfält ifyllda i profiler för målkanalen (t.ex. `consents.marketing.email.val`)
- [ ] Om villkorsbaserad målgruppsfiltrering (alternativ B/C) används, har direktuppspelade målgruppssegment definierats och utvärderas aktivt

## Implementeringsalternativ

I det här avsnittet beskrivs tre implementeringsalternativ för händelseutlösta meddelanden. Varje alternativ bygger på det föregående och lägger till ytterligare funktioner.

### Alternativ A: Enkelt händelseutlöst meddelande

**Passar bäst för:** Omedelbara svar med ett meddelande där ingen fördröjning eller villkorlig logik krävs - orderbekräftelse, välkomstmeddelande, bekräftelse av formulärsändning, bokningsbekräftelse.

**Så här fungerar det:**

Resan lyssnar efter en kvalificerande händelse via en händelsetod. När händelsen tas emot tar profilen sig in på resan, passerar genom minimal villkorsutvärdering (samtyckeskontroll, kontroll av profilexistens) och får omedelbart ett enda meddelande via den konfigurerade kanalåtgärdsnoden.

Detta är den enklaste implementeringsvarianten. Arbetsytan för resan innehåller en nod för händelseinmatning, en valfri nod för grundläggande behörighetskontroller, en enda nod för meddelandeåtgärder och en slutnod. Det finns inga väntesteg, ingen komplex förgrening och inga konverteringskontroller. Meddelandet levereras vanligtvis inom några sekunder till minuter efter den utlösande händelsen.

Händelsedata från den utlösande händelsen (produktnamn, ordersumma, formulärinformation) kan användas för meddelandeanpassning via sammanhangsbaserade attribut i personaliseringsredigeraren. Detta tillvägagångssätt maximerar hastigheten till leveransen och minimerar kundens komplexitet.

**Viktiga överväganden:**

- Meddelandet skickas oavsett om kunden själv konverterar efter händelsen (ingen konverteringskontroll)
- Passar bäst för händelser som kräver ett omedelbart svar (bekräftelser, erkännanden)
- Regler för återinträde bör konfigureras noggrant - för bekräftelsemeddelanden tillåter du återinträde så att varje händelse genererar ett meddelande; för välkomstmeddelanden förhindrar du återinträde

**Fördelar:**

- Snabbaste tid till leverans (sekunder till minuter efter händelsen)
- Enklare konfiguration av resan med minimalt antal rörliga delar
- Låg risk för fel på resan eller fastnade profiler
- Enkelt att testa och underhålla

**Begränsningar:**

- Ingen möjlighet att kontrollera om kunden är självkonverterad innan den skickar
- Det går inte att inkludera villkorslogik som är fördröjd
- Kan generera onödiga meddelanden om händelsen inträffar ofta utan frekvensstyrning

**Experience League:**

- [Skapa en resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Allmänna händelser](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)

### Alternativ B: Villkorligt meddelande som utlöses av en händelse och väntar

**Bäst för:** Fördröjda, villkorliga svar där kunden måste ha tid att konvertera sig själv innan meddelandet tas emot: kundvagn har övergivits (vänta 1-4 timmar, kontrollera om kundvagnen fortfarande är övergiven), bläddra bland övergivna (vänta 24 timmar, kontrollera om köpet har gjorts), testperioden har gått ut (vänta tills förfallodatumet närmar sig).

**Så här fungerar det:**

Resan lyssnar efter en kvalificerande händelse, anger profilen och introducerar en vänteperiod innan villkoren utvärderas. Efter väntetiden kontrollerar en villkorsnod om kunden har självkonverterat (t.ex. slutfört köpet, förnyat prenumerationen) eller om den ursprungliga kontexten fortfarande är giltig. Endast om villkoret är uppfyllt (t.ex. vagnen fortfarande är övergiven) fortsätter resan till meddelandeleveransen.

Arbetsytan för resan innehåller en nod för händelseinmatning, en väntenod (konfigurerbar varaktighet eller specifikt datum/tid), en villkorsnod som söker efter en konverteringshändelse eller ändring av profiltillstånd, förgreningssökvägar (skicka meddelande kontra avsluta utan att skicka), en meddelandeåtgärdsnod på den kvalificerande sökvägen och en slutnod på varje gren. Avslutningskriterier kan konfigureras så att profiler automatiskt tas bort från resan om konverteringshändelsen inträffar under vänteperioden, vilket eliminerar behovet av den explicita villkorskontrollen.

Detta minskar behovet av meddelanden genom att ge kunderna tid att själva konvertera, förbättra kundupplevelsen och öka den uppfattade relevansen i de meddelanden som skickas.

**Viktiga överväganden:**

- Väntetiden påverkar konverteringsgraden avsevärt - kortare väntetider (1-2 timmar) ger större brådska men fler onödiga utskick; längre väntetider (24-48 timmar) minskar volymen men kan missa relevansfönstret
- Villkorsutvärderingen kräver att konverteringshändelsen hämtas i AEP och kopplas till samma profilidentitet
- Avslutsvillkor är ett renare alternativ till explicita villkorsnoder för konverteringskontroll
- Regler för återinträde måste ta hänsyn till vänteperioden - en profil får inte återinträda i resan medan den redan väntar

**Fördelar:**

- Minskar antalet onödiga meddelanden genom att kontrollera självkonvertering
- Ger mer relevant kommunikation av högre kvalitet
- Stöder tidskänsliga användningsfall med konfigurerbara fördröjningsfönster
- Avslutningskriterier möjliggör automatisk borttagning av resan vid konvertering

**Begränsningar:**

- Ökad komplexitet i resan med väntetider och villkorsnoder
- Profilerna upptar restider under vänteperioder (med 91 dagars tidsgräns för resa)
- Kräver att konverteringshändelsen infogas i AEP i väntefönstret för korrekt villkorsutvärdering
- Längre leveranstid jämfört med alternativ A

**Experience League:**

- [Vänta på aktivitet](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Villkorsaktivitet](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Avslutningskriterier](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)

### Alternativ C: Händelse som utlöses med frekvensstyrning

**Bäst för:** Högfrekventa händelsekällor där meddelandetrötthet är ett problem - sidvisningar, produktvyer, sökfrågor, upprepade varukorgstillägg. Kan användas som en övertäckning ovanpå alternativ A eller B.

**Så här fungerar det:**

Det här alternativet lägger till frekvensstyrning till antingen alternativ A eller alternativ B för att förhindra övermeddelanden. Beteendehändelser med hög frekvens (t.ex. produktvisningar eller upprepade kundvagnstillägg) kan utlösa resan flera gånger inom en kort period. Utan frekvensstyrning kan en profil ta emot dubbletter eller överdrivet många meddelanden.

Frekvensstyrningen genomförs med två kompletterande mekanismer: AJO affärsregler (frekvensgränser) som begränsar hur många meddelanden en profil tar emot per kanal per tidsperiod och regler för återinträde på resenivå som definierar en nedladdningsperiod innan en profil kan återkomma till samma resa. Affärsreglerna fungerar på organisationsnivå och sätter gränser för alla kampanjer och resor (t.ex. max 3 e-postmeddelanden per vecka), medan återinträde i bostaden sker på den enskilda resan (en profil kan t.ex. inte återkomma till den här resan inom 72 timmar efter det sista inträdet).

Dessutom kan hantering av konflikter och prioriteter konfigureras för att tilldela prioritetspoäng till den utlösta resan, så att kommunikationen får högsta prioritet när flera resor eller kampanjer tävlar om samma profil.

**Viktiga överväganden:**

- Frekvensgränser måste balansera mellan att förhindra trötthet och säkerställa att viktiga utlösta meddelanden levereras
- Kanalspecifika gränser rekommenderas - e-post, SMS och push har olika trösklar för utmattning
- Kartläggning av återinträde på resan och frekvensband på organisationsnivå fungerar tillsammans. Båda bör konfigureras
- Prioriterade poäng avgör vilka kommunikationsmöjligheter som vinner när tak uppnås - högprioriterade resor bör tilldelas högre poäng

**Fördelar:**

- Förhindrar meddelandetrötthet från händelsekällor med hög frekvens
- Upprätthåller varumärkets anseende och abonnemangsnöjdhet
- Skyddstak på organisationsnivå ger ett säkerhetsnät för alla kampanjer och resor
- Prioriterad poängsättning säkerställer att de viktigaste budskapen levereras när versaler nås

**Begränsningar:**

- Vissa kvalificerande profiler kommer att ignoreras och relevanta meddelanden kan saknas
- Konfigurationen av frekvensbegränsningen ger administrativ komplexitet
- Caps kan oväntat interagera med andra aktiva kampanjer och resor som delar samma kanal
- Kräver kontinuerlig övervakning och justering när meddelandeportföljen ändras

**Experience League:**

- [Frekvensregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Översikt över affärsregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [Prioritetspoäng](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Anställningshantering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)

### Jämförelse av alternativ

I följande tabell jämförs de tre implementeringsalternativen över de viktigaste kriterierna.

| Kriterier | Alternativ A: Enkel händelseutlöst | Alternativ B: Villkorligt med Vänta | Alternativ C: Frekvensstyrning |
| --- | --- | --- | --- |
| Bäst för | Omedelbara bekräftelser, bekräftelser | Återställning av övergivna, fördröjda villkorliga svar | Händelsekällor med hög frekvens, miljöer med flera resor |
| Komplex | Lågt | Medelsvåra: | Medium-Hög (tillägg till A eller B) |
| Svarstid för meddelande | Sekunder till minuter | Minuter till timmar/dagar (konfigurerbar väntetid) | Samma som underliggande option (A eller B) |
| Självkonverteringskontroll | Nej | Ja (via villkor eller avslutningskriterier) | Beroende på underliggande alternativ |
| Frekvensskydd | Ingen (om inte kombinerat med C) | Ingen (om inte kombinerat med C) | Ja - kanaländpunkter och återinträde i jordatmosfären |
| Noder på arbetsytan på resan | 3-4 (händelse, valfritt villkor, åtgärd, slut) | 5-7 (event, wait, condition, branch, action, ends) | Samma som A eller B, plus konfiguration av affärsregler |
| Kräver | Händelseschema, kanalyta, meddelandeinnehåll | Alla alternativ A + konverteringshändelseinmatning | Konfiguration av alla alternativ A eller B + frekvensregel |

### Välj rätt alternativ

Använd följande riktlinjer för beslut för att välja rätt implementeringsalternativ.

1. **Måste meddelandet skickas omedelbart utan dröjsmål?** Om ja, börja med **alternativ A**. Bekräftelsemeddelanden, välkomstmeddelanden och bekräftelser kräver vanligtvis ingen vänteperiod.

2. **Ska kunden ha tid att konvertera sig själv innan meddelandet tas emot?** Om ja, välj **Alternativ B**. Att kunden överger en varukorg, överger en webbsida och använder testversioner vid en viss tidpunkt.

3. **Är den utlösande händelsen hög (inträffar flera gånger per session eller per dag för samma profil)?** Om ja, lägg till **alternativ C** som en övertäckning ovanpå alternativ A eller B. Produktvyer, sidvyer och sökruthändelser kan generera stora volymer utlösare som kräver frekvensskydd.

4. **Är flera utlösta resor och kampanjer aktiva i sandlådan?** Om ja, lägg till **alternativ C** oavsett händelsfrekvens för att hantera kommunikationsbelastning för flera resor och förhindra kanalutmattning.

I praktiken använder de flesta produktionsimplementeringar alternativ B + C för användningsområden av typen övergivna (villkorlig väntan med frekvensstyrning) och alternativ A + C för bekräftelseliknande användningsfall (omedelbar sändning med frekvensstyrning som ett säkerhetsnät).

## Implementeringsfaser

Följande faser går igenom den kompletta implementeringen av händelseutlösta meddelanden.

### Fas 1: Konfigurera händelseschema och datainsamling

**Programfunktion:** AEP: Datamodellering (F2), AEP: Datakällor och samling (F3)

**Så här konfigurerar du:** XDM ExperienceEvent-schemat som fångar den utlösande händelsen, datauppsättningen som lagrar de här händelserna samt realtidsflödet för datainsamling (Web SDK, Mobile SDK eller Server API) som strömmar händelser till AEP. Denna fas utgör grunden för de data som resan kommer att lyssna på.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>
>**Beslut: Utlöser händelsetyp**
>
>Vilken händelse utlöser meddelandet? Händelsetypen avgör vilka schemafält som krävs och samlingsmetoden.
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Commerce event (cart add, purchase, checkout) | Användningsexempel inom e-handel - övergivna varukorgar, efter köp | Kräver Commerce-fältgrupp med `productListItems`, `cart`, `order` fält |
>| Webbinteraktionshändelse (sidvy, produktvy) | Bläddra bland övergivna webbplatser, triggers av engagemang i innehållet | Kräver fältgrupp för webbinformation med `webPageDetails`, `webInteraction` fält |
>| Programhändelse (programinstallation, avinstallation, åtgärd i appen) | Mobil engagemangsutlösare | Kräver Mobile SDK-implementering och programfältgrupp |
>| Systemhändelse (betalningsfel, prenumerationsändring, statusuppdatering) | Driftsmeddelanden | Kräver serversidans API eller källanslutning för att importera systemhändelser |
>| Formuläröverföringshändelse | Leadgenerering, registreringsbekräftelse | Kräver anpassad fältgrupp som hämtar formulärdatafält |

>[!NOTE]
>
>**Beslut: Samlingsmetod**
>
>Hur spelas den utlösande händelsen in och strömmas till AEP?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Web SDK | Webbaserade beteendehändelser (kundvagn tillagd, sidvisning, inskickad blankett) | Kräver installation av Web SDK på webbplatsen; händelserna strömmas i realtid via Edge Network |
>| Mobile SDK | Mobilappshändelser (appöppning, åtgärder i appen, registrering av push-token) | Kräver integrering av Mobile SDK i det inbyggda programmet eller React Native wrapper |
>| Edge Network Server-API | Systemhändelser på serversidan (betalningshantering, prenumerationshantering, backend-utlösare) | Inget beroende på klientsidan - händelser skickas från organisationens serversystem |
>| Source Connector | Händelser från externa system (CRM, automatiserad marknadsföring, äldre plattformar) | Vanligtvis batchbaserad; har inte stöd för realtidsutlösande såvida inte direktuppspelningskapacitet |

**Gränssnittsnavigering:** Datainsamling > Datastreams > New Datastream (for datastream setup); Scheman > Create schema (for event schema); Datasets > Create dataset from schema (for dataset creation)

**Information om nyckelkonfiguration:**

- Händelseschemat måste innehålla alla fält som behövs för utvärdering av resevillkor och meddelandepersonalisering
- Datastream måste ha både [!DNL Adobe Experience Platform] och [!DNL Adobe Journey Optimizer] tjänster aktiverade
- Datauppsättningen måste aktiveras för kundprofilen i realtid så att händelser associeras med enhetliga profiler
- Händelsedata måste innehålla ett identitetsfält (e-post, CRM-ID, ECID) som kan evalueras till en känd profil

**Experience League-dokumentation:**

- [XDM - systemöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Konfigurera datastreams](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [SDK - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Edge Network Server API - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)
- [Översikt över direktuppspelning](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/streaming/overview)

### Fas 2: Konfigurera identitet och profil

**Programfunktion:** AEP: Identity &amp; Profile Configuration (F4)

**Så här konfigurerar du:** Identitetsnamnutrymmen för identifierarna för den utlösande händelsen, primär identitetsbeteckning för händelseschemat, regler för identitetslänkning för enhetsupplösning och en sammanfogningsprincip för profilenhetliga. Detta garanterar att den utlösande händelsen är kopplad till en enhetlig kundprofil så att resan kan matcha kontaktinformationen och leverera meddelandet.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>
>**Beslut: Primär identitet för händelseschema**
>
>Vilket identitetsfält i den utlösande händelsen ska fungera som primär identitet för profilmatchning?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| E-postadress | Händelser från autentiserade webbsessioner eller formulär där e-post hämtas | Direktupplösning till en kontaktbar identitet; enklaste väg till e-postleverans |
>| CRM-ID | Händelser från autentiserade system där CRM-ID är den primära identifieraren | Kräver att CRM ID-namnområde skapas. Profilen måste ha ett länkat e-postmeddelande eller en länkad telefon för att kunna levereras |
>| ECID (Experience Cloud-ID) | Anonyma webb- eller apphändelser där ingen autentiserad identitet är tillgänglig | Kräver identitetssammanfogning för att länka ECID till en känd identitet; meddelanden kan inte skickas enbart till ECID |
>| Telefonnummer | Händelser från interaktioner mellan mobiler och callcenter | Stöder SMS-leverans; kräver Phone namespace |

**Gränssnittsnavigering:** Identiteter > Skapa identitetsnamnrymd; Scheman > Välj schema > Välj fält > Identitet > Ange som primär identitet; Profiler > Sammanfoga principer

**Information om nyckelkonfiguration:**

- Anonyma händelser (endast ECID) kan inte utlösa meddelandeleverans förrän ECID är länkat till en känd kontaktbar identitet (e-post, telefon) via identitetsdiagrammet
- Den sammanslagningsprincip som används av AJO måste vara konsekvent med den som används för målgruppsutvärdering
- För webbaserade utlösta meddelanden ska du kontrollera att identitetsdiagrammet länkar ECID till autentiserade identiteter via inloggningshändelser

**Experience League-dokumentation:**

- [Översikt över namnutrymmen för identiteter](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/namespaces)
- [Länkningsregler för identitetsdiagram](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)
- [Översikt över kopplingsprofiler](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### Fas 3: Konfigurera kanalytor

**Programfunktion:** AJO: Kanalkonfiguration

**Så här konfigurerar du:** Kanalytan (förinställning) som definierar den sändande infrastrukturen för det utlösta meddelandet: underdomänsdelegering, IP-pool, avsändaridentitet, svarsadress, hantering av avanmälan och kanalspecifika autentiseringsuppgifter (SMS-provider, push-certifikat). Det måste finnas en giltig kanalyta innan meddelandeinnehållet kan skapas eller resor kan publiceras.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>
>**Beslut: Meddelandekanal**
>
>Vilken kanal kommer det utlösta meddelandet att använda?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| E-post | De flesta utlösta användningsområdena för meddelanden - återställning efter avhopp, bekräftelser, introduktion | Kräver delegering av underdomän, IP-pool, konfiguration av avsändare; stöder omfattande HTML-innehåll och -personalisering |
>| SMS | Tidskänsliga meddelanden, kortfattade aviseringar, målgrupper med högt SMS-engagemang | Kräver integrering med SMS-leverantörer (Sinch, Twilio, Infobip); omfattas av teckenbegränsningar och striktare krav på medgivande |
>| Push-meddelande | Mobilappsengagemang, appanvändares återengagemang | Kräver konfiguration av push-autentiseringsuppgifter (APN för iOS, FCM för Android); användaren måste ha appen installerad med push aktiverad |
>| Flera kanaler | Omfattande engagemangsstrategi med kanalpreferenser eller reservlogik | Kräver flera kanalytor; kanalval kan hanteras via noder för resevillkor |

>[!NOTE]
>
>**Beslut: Delegeringsmetod för underdomän (e-post)**
>
>Hur ska den e-postsändande underdomänen delegeras till Adobe?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Fullständig delegering | Organisationen vill att Adobe ska hantera alla DNS-poster för den sändande underdomänen | Enklast installation; Adobe hanterar SPF-, DKIM-, DMARC-poster automatiskt |
>| CNAME-delegering | Organisationen vill behålla DNS-kontrollen samtidigt som den pekar på Adobe infrastruktur | Kräver manuell DNS-posthantering; ger mer organisatorisk kontroll över DNS |

**Gränssnittsnavigering:** Administration > Kanaler > Underdomäner (för underdomänsinställningar); Administration > Kanaler > IP-pooler (för IP-poolkonfiguration); Administration > Kanaler > Kanalytor > Skapa yta (för att skapa yta)

**Information om nyckelkonfiguration:**

- Underdomänsverifiering och DNS-spridning kan ta upp till 48 timmar
- Nya IP-pooler kräver en värmeplan (2-4 veckors gradvis ökning av volymen)
- Konfigurera rubriker för att avbeställa e-postmeddelanden med ett klick
- Konfigurera autentiseringsuppgifterna för leverantören för SMS innan du skapar SMS-kanalsytan
- Konfigurera APN:er och FCM-autentiseringsuppgifter för push-kanaler innan du skapar push-kanalsytan

**Experience League-dokumentation:**

- [Kom igång med e-postkonfiguration](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegera underdomäner](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Skapa IP-pooler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [Konfigurera kanalytor](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Konfigurera SMS-kanal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Konfigurera kanal för push-meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Fas 4: Skapa meddelandeinnehåll

**Programfunktion:** AJO: Meddelanderedigering

**Det här konfigurerar du:** Det meddelandeinnehåll som levereras under resan, inklusive layoutdesign, personaliseringstoken med hjälp av profil- och händelseattribut, villkorsstyrda innehållsblock, återanvändbara fragment (sidhuvuden, sidfötter, juridisk ansvarsfriskrivning) samt förhandsgranskning och testning av innehåll.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>
>**Beslut: Innehållsstrategi**
>
>Hur ska meddelandeinnehållet skapas?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Starta från en befintlig mall | Organisationsmallar finns och varumärkets enhetlighet krävs | Den snabbaste vägen till framtagning av innehåll; säkerställer varumärkesefterlevnad; malländringar sprids till nya meddelanden |
>| Designa från scratch i e-postprogrammet Designer | Anpassad layout krävs för det här specifika utlösta meddelandet | Full kreativ kontroll; dra-och-släpp-redigerare; långsammare men mer flexibel |
>| Importera HTML | Innehållet är utformat av ett externt team eller en extern byrå och tillhandahålls som HTML | Kräver HTML expertis inom kodning; kanske inte stöder alla funktioner i e-post-Designer fullt ut |

>[!NOTE]
>
>**Beslut: Händelseanpassning**
>
>Vilka händelsedata ska användas i meddelandeinnehållet?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Kontextattribut för händelse | Meddelandet ska innehålla information från den utlösande händelsen (produktnamn, kundvagnsvärde, formulärfält) | Använd kontextuella händelseattribut i personaliseringsredigeraren; data kommer från den utlösande händelsenyttolasten |
>| Profilattribut | Meddelandet ska innehålla data på profilnivå (förnamn, lojalitetsnivå, plats) | Använd profilattribut via XDM-sökvägar (t.ex. `profile.person.name.firstName`); data kommer från den enhetliga profilen |
>| Attributen för både händelse och profil | Meddelandet ska kombinera händelsekontext med profilanpassning | Det vanligaste sättet för utlösta meddelanden; garanterar både relevans (händelse) och personalisering (profil) |

**Gränssnittsnavigering:** Innehållshantering > Innehållsmallar > Bläddra (för mallval); Kampanj- eller reseåtgärd > Redigera innehåll > E-posta Designer (för innehållsdesign); Välj textkomponent > Personalization-ikon (för att lägga till personalisering)

**Information om nyckelkonfiguration:**

- Använd kontextuella attribut för att anpassa data från den utlösande händelsen (t.ex. produktnamn, kundvagnsvärde)
- Använd profilattribut för namn, inställningar och lojalitetsdata
- Konfigurera villkorliga innehållsblock för att variera innehåll efter profilsegment eller attribut (t.ex. olika CTA för lojalitetsmedlemmar)
- Skapa återanvändbara fragment för sidhuvuden, sidfötter och friskrivningsklausuler som delas mellan utlösta meddelanden
- Förhandsgranska med flera testprofiler för att verifiera personaliseringsrenderingar korrekt
- Skicka korrektur till interna intressenter innan resan publiceras

**Experience League-dokumentation:**

- [Designa e-postinnehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Lägg till personalisering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization syntax](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Dynamiskt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Arbeta med innehållsmallar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Arbeta med innehållsfragment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Förhandsgranska och testa ditt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### Fas 5: Skapa och konfigurera resan

**Programfunktion:** AJO: Journey Orchestration, AJO: Täthet och affärsregler (alternativ C), AJO: Hantering av konflikter och prioritet

**Så här konfigurerar du:** Den resa som lyssnar efter den utlösande händelsen och ordnar meddelandeleveransen. Detta är den huvudsakliga implementeringsfasen där arbetsytan för resan är utformad med noden för händelsetabell, villkorsnoder, väntesteg (för alternativ B), noder för meddelandeåtgärd och avslutningskriterier. Denna fas omfattar även frekvensstyrning (alternativ C) och konfiguration av konflikt/prioritet.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>
>**Beslut: Regler för återinträde**
>
>Kan en profil återansluta till den här resan om utlösarhändelsen inträffar igen?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Tillåt återinträde (med nedstämning) | Evenemanget kan återkomma på ett legitimt sätt och varje förekomst motiverar ett meddelande (t.ex. ska varje kundvagnsöverlämnande utlösa ett meddelande om återkrav) | Ställ in en nedkylningsperiod (minst 5 minuter) för att förhindra snabb återinträde från dubbletthändelser. Normal nedkylning varierar från 1 timme till 72 timmar |
>| Ingen återregistrering | Meddelandet ska bara skickas en gång per profil, oavsett om en händelse återkommer (t.ex. välkomstmeddelande efter första registreringen) | Profilen tas inte bort permanent när den första resan har slutförts, vilket är lämpligt för engångs-livscykelmeddelanden |

>[!NOTE]
>
>**Beslut: Väntetid (endast alternativ B)**
>
>Hur länge ska resan vänta innan villkoren utvärderas och meddelandet skickas?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Vänta kort (1-4 timmar) | Snabb användning, t.ex. övergivna varukorgar, där en omedelbar uppföljning är effektiv | Högre meddelandevolym; kan fånga upp vissa självkonverterare; bäst för kundvagnsåterställning med högt värde |
>| Medium, vänta (12-24 timmar) | Användningsexempel med medelhög snabbhet, som surfning eller engagemang för innehåll | Balanserad strategi; minskar onödiga utskick samtidigt som relevansen bibehålls |
>| Lång väntan (2-7 dagar) | Låga brådskande användningsfall som påminnelser om att testperioden är slut eller periodiska incheckningar | Lägre meddelandevolym, högre risk för att förlora sammanhangsberoende relevans |
>| Anpassat datum/tid | Användningsfall som är knutna till ett visst datum (t.ex. 3 dagar före testperiodens förfallodatum) | Vänta tills ett beräknat datum/tid; använder den anpassade uttrycksredigeraren |

>[!NOTE]
>
>**Beslut: Avslutningskriterier**
>
>Under vilka villkor ska en profil tas bort från resan innan meddelandeåtgärden nås?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Konverteringshändelse (t.ex. slutfört köp) | Kundvagn eller bläddra efter övergivna kunder där målet är konvertering | Profilen avslutas automatiskt när konverteringshändelsen upptäcks. Renast inställning för alternativ B |
>| Ändring av målgruppsmedlemskap | Profilen bör avslutas om de lämnar ett kvalificerande segment | Kräver direktuppspelad publik som uppdateras i nästan realtid |
>| Resetimeout (max 91 dagar) | Standardbeteende - profilen avslutas efter den maximala resans varaktighet | Säkerhetsnät; bör inte vara den primära exitmekanismen för kortlivade utlösta resor |
>| Inga explicita avslutningskriterier | Enkla bekräftelser (alternativ A) där alla kvalificerande profiler ska få meddelandet | Profilen avslutas naturligt efter meddelandeåtgärden och slutnoden |

>[!NOTE]
>
>**Beslut: Frekvensstyrning (alternativ C)**
>
>Hur många utlösta meddelanden ska en profil ta emot per tidsperiod?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Kanalspecifika ändpunkter (t.ex. 3 e-postmeddelanden/vecka, 1 SMS/dag) | Olika kanaler har olika trötthetströsklar | Rekommenderad strategi: respekterar varje kanals nivå för intrång |
>| Globalt tak (t.ex. 5 meddelanden/vecka över alla kanaler) | Förenklad styrning över alla kommunikationstyper | Enklare att hantera men mindre nyansrika; kan begränsa mindre invecklade kanaler |
>| Endast återinträde på resenivå | Frekvensstyrning krävs för den här specifika resan men inte för hela organisationen | Enklast implementering; skyddar inte mot utmattning under resan |

**Gränssnittsnavigering:** Resor > Skapa resa (för att skapa resa); Researbetsyta > Dra händelseaktivitet (för händelseinmatning); Researbetsyta > Dra aktiviteten Vänta (för väntekonfiguration); Researbetsyta > Dra aktiviteten Villkor (för villkorsförgreningar); Resegenskaper > Utträdeskriterier (för avslutningskonfiguration); Administration > Affärsregler > Skapa regel (regel) för frekvensändar)

**Information om nyckelkonfiguration:**

- Konfigurera resehändelsen genom att välja händelseschemat och definiera kvalificeringsvillkoren
- För alternativ B lägger du till väntenoden omedelbart efter händelseposten och före villkorsutvärderingen
- Konfigurera villkorsnoder med hjälp av profilattribut, händelsedata eller medlemskontroller för målgrupper
- Länka meddelandeåtgärdsnoden till kanalytan och det redigerade innehållet från fas 3 och 4
- Ställ in resans tidsgräns till en lämplig längd (kortare än 91 dagar för utlösta resor)
- För alternativ C skapar du frekvensregler via Administration > Affärsregler innan resan publiceras
- Tilldela resepoäng om andra kampanjer eller resor riktar sig till överlappande målgrupper

**Var alternativen skiljer sig:**

**För alternativ A (enkel händelse utlöst):**
Resans arbetsyta är minimal: anmälan till händelsen > villkor för medgivande/behörighet > meddelandeåtgärd > slut. Inga väntesteg eller konverteringskontroller. Ange regler för återinträde baserat på om händelsen ska generera ett meddelande varje gång det inträffar.

**För alternativ B (villkorligt med väntan):**
Lägg till en väntenod efter händelsepost. Efter väntetiden lägger du till en villkorsnod för att kontrollera konverteringen (t.ex. kontrollera om händelsen `commerce.purchases` inträffade efter resans inträde) eller använder avslutsvillkor för att automatiskt ta bort konverterade profiler. Fördela till meddelandeåtgärden på sökvägen&quot;inte konverterad&quot; och till en slutnod på den konverterade sökvägen.

**För alternativ C (frekvensstyrning):**
Konfigurera frekvensbegränsningar på organisationsnivå via Administration > Affärsregler före publicering. Ställ in återinträde på resenivå i färdegenskaperna. Om du vill kan du tilldela en prioritetspoäng via reseegenskaper för att kontrollera vilken kommunikation som vinner när gränsen nås. Detta kan tillämpas ovanpå antingen alternativ A eller alternativ B.

**Experience League-dokumentation:**

- [Skapa en resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Resans egenskaper](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Allmänna händelser](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Villkorsaktivitet](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Vänta på aktivitet](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Lägg till ett meddelande i en resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Avslutningskriterier](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [Anställningshantering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Frekvensregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Prioritetspoäng](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Identifiera potentiella konflikter](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)

### Fas 6: Testa och driftsätt resan

**Programfunktion:** AJO: Journey Orchestration

**Så här konfigurerar du:** Testlägesvalidering för att verifiera att resan fungerar som förväntat med testprofiler, följt av resepublikation för att göra den offentlig.

**Gränssnittsnavigering:** Researbetsyta > Växla testläge (för testning); Researbetsyta > Publicera (för distribution)

**Information om nyckelkonfiguration:**

- Aktivera testläge på arbetsytan för att simulera händelseutlösare med testprofiler
- Välj testprofiler som har giltig kanalkontaktinformation (e-postadress, telefonnummer)
- Utlös testhändelsen och verifiera att testprofilen går igenom den förväntade sökvägen
- För alternativ B kontrollerar du att väntesteget fungerar korrekt och att villkorsutvärderingen ger förväntad förgrening
- Kontrollera att personaliseringstoken återges korrekt i testmeddelandet
- Publicera resan för att göra den levande efter lyckade tester
- Övervaka resestatus och inledande profilanmälningsmått efter publicering

**Experience League-dokumentation:**

- [Testa din resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [Publicera resan](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)

### Fas 7: Övervaka och rapportera om prestanda

**Programfunktion:** AJO: Rapporterings- och prestandaanalys, S4: Övervakning och observerbarhet, S5: Rapportering och analys

**Vad du kommer att konfigurera:** Live- och historikrapporter för leverans- och engagemangsövervakning, plattformsaviseringar för misslyckad händelsehantering och resehantering samt (valfritt) CJA-arbetsytor för mer djupgående flerkanalsanalys av händelseutlösande meddelandeeffektivitet.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>
>**Beslut: Rapporteringsdjup**
>
>Hur mycket rapportanalys behövs för det här användningsfallet?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Endast inbyggda AJO-rapporter | Operativ övervakning av leveransstatistik är tillräcklig | Tillgänglig omedelbart; täcker skickade, levererade, studsade, öppnade, klickade; ingen ytterligare konfiguration behövs |
>| Integrering med AJO och CJA | Flerkanalsanalys, konverteringsattribuering och trendanalys behövs | Kräver CJA anslutning och datavy länkad till AJO datamängder; ger djupare analysfunktioner |

**Gränssnittsnavigering:** Resor > Välj resa > Live-rapport (för direktövervakning); Resor > Välj resa > All time-rapport (för historikanalys); Varningar > Varningsregler > Prenumerera (för aviseringskonfiguration)

**Information om nyckelkonfiguration:**

- Få åtkomst till resans liverapport under aktiv körning för att övervaka profilposter, utträden och leveransstatistik
- Granska den historiska rapporten efter att resan har varit aktiv tillräckligt länge för att samla in meningsfulla data
- Konfigurera varningar för fel vid körning av källflöde (händelseinmatning) och fördröjningar vid bearbetning av resan
- För integrering med CJA ska du kontrollera att CJA-anslutningen innehåller data om AJO-upplevelsehändelser (händelsedatauppsättning för meddelandefeedback, händelsedatauppsättning för e-postspårning)

**Experience League-dokumentation:**

- [Rapport om livesändning på resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Global reserapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Arbeta med Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Översikt över aviseringar](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Integreringsguide för AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

## Implementeringsöverväganden

Det här avsnittet handlar om säkerhetsutkast, vanliga fallgropar, bästa praxis och beslut om kompromisser vid händelseutlösta meddelandeimplementeringar.

### Gardrutor och begränsningar

Följande plattformsskydd och -begränsningar gäller för händelseutlösta meddelandeimplementeringar.

- **Enhetlig händelsegenomströmning:** Maximalt 5 000 händelser per sekund och sandlåda för enhetsbaserade händelseresor - [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- **Gräns för direktresa:** Maximalt 500 direktresor per sandlåda - [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- **Gräns för arbetsyta i resan:** Maximalt 50 aktiviteter per arbetsyta i resan
- **Tidsgräns för resa:** Den maximala transporttiden är 91 dagar (global tidsgräns)
- **Kylning av ny post:** Minsta nedladdning av ny post är 5 minuter
- **Konfigurationer av frekvensbegränsning:** Maximalt antal 10 takkonfigurationer per sandlåda
- **Kanalytor:** Högst 10 kanalytor per kanaltyp och sandlåda
- **Direktuppspelande inmatning:** Maximalt 20 000 poster per sekund per HTTP-anslutning — [Inmatningsskydd](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
- **Beräknade attribut:** Maximalt 25 beräknade attribut per sandlåda - [Beräknade attributskyddsdetaljer](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview#guardrails)
- **Innehållsfragment:** Högst 30 innehållsfragment per meddelande
- **Uppdatering av Live-rapport:** Live-rapporter uppdateras var 60:e sekund och visar de senaste 24 timmarna med data
- **Fördröjning för historikrapport:** Det kan ta upp till två timmar innan historiska rapporter (hela tiden) har fyllts i fullständigt när körningen har avslutats

### Vanliga fallgropar

Tänk på följande vanliga problem när du implementerar händelseutlösta meddelanden.

- **Anonyma händelser utan identitetsupplösning:** Utlösande händelser som bara innehåller ett ECID (anonymt cookie ID) kan inte matchas till en kontaktbar profil för meddelandeleverans. Kontrollera att den utlösande händelsen innehåller en autentiserad identitet eller att identitetsdiagrammet länkar ECID till en känd kontakt. Utan identitetsupplösning kommer profiler in på resan men misslyckas vid meddelandeleveransen.

- **Konverteringshändelse saknas för alternativ B-villkorskontroller:** Om konverteringshändelsen (t.ex. köp) inte har importerats till AEP eller inte är associerad med samma profilidentitet som den utlösande händelsen, utvärderas villkorskontrollen felaktigt som&quot;inte konverterad&quot; och onödiga meddelanden skickas. Verifiera att konverteringshändelser strömmar in i AEP i realtid och dela en identitet med den utlösande händelsen.

- **Överflödiga regler för återinträde:** Om du tillåter återinträde utan en nedladdningsperiod på händelsekällor med hög frekvens kan samma profil ta emot flera meddelanden inom några minuter. Ställ alltid in en postnedladdning som matchar affärskontexten (t.ex. 4-timmars nedkylning för kundvagnsövergivande, 24-timmars nedladdning för övergivna webbläsare).

- **Tidszonsfel i väntesteg:** Vänta tills processen i UTC är som standard. Om resan avser profiler över flera tidszoner och väntetiden ska anpassas till mottagarens lokala tid, konfigurerar du inställningarna för tidszonen på resan i enlighet med detta.

- **Frekvensbegränsningar som står i konflikt med andra kampanjer:** Frekvensgränser på organisationsnivå gäller för alla kampanjer och resor. En ny utlöst resa kan undertryckas om profiler redan har nått sin övre gräns för andra aktiva kampanjer. Övervaka dämpningsfrekvensen och justera prioritetspoäng för att säkerställa att viktiga utlösta meddelanden prioriteras.

- **Det gick inte att publicera på resa på grund av saknade beroenden:** Alla grenar på arbetsytan måste avslutas med en slutaktivitet. Alla åtgärdsnoder måste referera till giltiga kanalytor med aktivt meddelandeinnehåll. Kontrollera alla beroenden före publicering.

### God praxis

Följ dessa rekommendationer för lyckade händelseutlösta meddelandeimplementeringar.

- **Börja enkelt och iterera sedan:** Börja med alternativ A för nya utlösta meddelandeanvändningsfall. Lägg till logik för väntetid och villkor (alternativ B) först efter att händelseförloppet och meddelandeleveransen har validerats. Lägg till frekvensstyrning (alternativ C) när flera utlösta resor är aktiva.

- **Använd avslutningskriterier i stället för villkorsnoder för konverteringskontroller:** Utgångskriterier tar automatiskt bort profiler från resan när en kvalificerande händelse (t.ex. köp) inträffar, vilket eliminerar behovet av en explicit villkorsnod efter väntesteget. Detta ger en renare arbetsyta och mer responsiv konverteringsidentifiering.

- **Testa med verkliga händelsedata i en utvecklingssandlåda:** Använd testläge med faktiska händelsenyttolaster (inte bara testprofiler) för att validera att händelseschemafält, personaliseringstoken och villkorsuttryck fungerar korrekt med produktionsliknande data.

- **Ange händelsespecifika återinmatningshämtningar:** Matcha nedladdningsperioden med affärskontexten för utlösarhändelsen. Vid avbrutna kundresor används vanligtvis en 4-24-timmarssummering, bekräftelseresor kan möjliggöra omedelbar återinträde, och ombordstigningsresor bör förhindra återinträde helt.

- **Övervaka undertryckningshastigheten som ett hälsomått:** Om undertryckningshastigheten (profiler som kvalificerar men inte tar emot meddelanden på grund av frekvensbegränsningar eller villkor) överstiger 30-40 %, kontrollerar du om ändpunkterna är för restriktiva eller om den utlösande händelsen är för bred.

- **Versionsresor i stället för att redigera levande:** En direktresa kan inte redigeras direkt. Skapa en ny version genom att duplicera resan, göra ändringar och sedan stoppa den gamla versionen och publicera den nya. På så sätt undviker du att störa de profiler som för närvarande finns på resan.

- **Ta med en reservsökväg/standardsökväg i villkorsnoder:** Konfigurera alltid en standardsökväg (else) i villkorsnoder för att hantera oväntade profiltillstånd. Profiler som inte matchar någon villkorsgren bör avslutas på ett smidigt sätt i stället för att förbli fastnade.

### Avvecklingsbeslut

Tänk på följande när du utformar en händelseutlöst meddelandeimplementering.

>[!NOTE]
>
>**Avvikelse: Meddelandehastighet kontra relevans för meddelande**
>
>Omedelbar meddelandeleverans (alternativ A) maximerar hastigheten men kan skicka meddelanden till kunder som skulle ha konverterat sig själva. Försenad villkorlig leverans (alternativ B) ökar relevansen genom att självkonverterare filtreras bort, men ger en fördröjning som kan minska behovet.
>
>- **Alternativ A prioriterar:** Hastighet, enkelhet och bekräftelseliknande användning där varje händelse kräver ett meddelande
>- **Alternativ B prioriterar:** Relevans, reducerad meddelandetrötthet, användningsområden av typen övergivna där självkonvertering är vanlig
>- **Rekommendation:** Använd alternativ A för transaktions- och bekräftelsemeddelanden där hastighet är det primära värdet. Använd alternativ B för meddelanden om återställning och återengagemang där relevansen är större än hastigheten. Experimentera med väntetider för att hitta den optimala balansen för varje användningsfall.

>[!NOTE]
>
>**Avvikelse: Frekvensskydd jämfört med meddelandetäckning**
>
>Strikta anfanger (alternativ C) förhindrar trötthet men kan förhindra viktiga utlösta meddelanden när profilerna är nära sin övre gräns. Tillåtna eller inga gränser maximerar täckningen men riskerar överbudstänkande och kanalutmattning.
>
>- **Strikta anspråk till förmån:** Kundens upplevelse, varumärkets anseende, leveransförmåga (färre skräppostklagomål)
>- **Tillåtna ändar ger:** Meddelandetäckning, konverteringsmöjligheter, undvika missade utlösare
>- **Rekommendation:** Börja med att ange branschstandard (3-5 e-postmeddelanden/vecka, 1-2 SMS/vecka, 2-3 push/dag) och justera baserat på interaktionsstatistik och avbeställningsfrekvens. Tilldela högre prioritetspoäng till utlösta meddelanden så att de vinner över batchkampanjer när gränsen nås.

>[!NOTE]
>
>**Avvikelse: Enkelhet i resan jämfört med avancerad resa**
>
>Enkla resor (få noder, ingen förgrening) är enklare att bygga, testa och underhålla, men erbjuder begränsad sammanhangsbaserad anpassning. Avancerade resor (olika villkor, förgrenade banor, segmentkontroller) ger fler nyanserade svar men ökar komplexiteten och risken för fel.
>
>- **Enkla resor gynnar:** Snabbare implementering, enklare felsökning, lägre underhållsbörda
>- **Avancerade resor gynnar:** Mer exakt målinriktning, bättre personalisering, färre onödiga utskick
>- **Rekommendation:** Börja med den enklaste resa som uppfyller verksamhetskraven. Öka komplexiteten stegvis baserat på prestandadata. En enkel, tillförlitlig resa är mer värdefull än en komplex resa med fel som inte upptäckts.

## Relaterad dokumentation

Följande resurser ger mer information om de funktioner som används i den här implementeringen.

### Resesamordning

- [Kom igång med resor](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Skapa en resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Resans egenskaper](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Allmänna händelser](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Elevkvalificeringshändelser](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [Villkorsaktivitet](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Vänta på aktivitet](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Lägg till ett meddelande i en resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Avslutningskriterier](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [Anställningshantering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Testa din resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [Publicera resan](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)

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
- [Lägg till personalisering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization syntax](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Hjälpfunktioner](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Dynamiskt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Arbeta med innehållsmallar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Arbeta med innehållsfragment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Förhandsgranska och testa ditt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [Skapa ett SMS-meddelande](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/create-sms)
- [Utforma ett push-meddelande](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/design-push)

### Regler för frekvens och verksamhet

- [Frekvensregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Översikt över affärsregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [API för begränsning](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/channel-surfaces/capping)

### Hantering av konflikter och prioriteringar

- [Kom igång med konflikthantering och prioritetshantering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Identifiera potentiella konflikter](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [Prioritetspoäng](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Resegotypning och skiljeförfarande](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)

### Rapportering och prestanda

- [Rapport om livesändning på resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Global reserapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Integreringsguide för AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

### Datainsamling och -förtäring

- [SDK - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Mobile SDK - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Edge Network Server API - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)
- [Konfigurera datastreams](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Översikt över direktuppspelning](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/streaming/overview)

### Datamodellering och scheman

- [XDM - systemöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Grundläggande om schemakomposition](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)

### Identitet och profil

- [Översikt över identitetstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Översikt över namnutrymmen för identiteter](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/namespaces)
- [Länkningsregler för identitetsdiagram](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)
- [Profilöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [Översikt över kopplingsprofiler](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### Segmentering och målgrupper

- [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Direktuppspelningssegmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)

### Datastyrning och samtycke

- [Översikt över dataförvaltning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Översikt över etiketter för dataanvändning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/labels/overview)
- [Fältgruppen för samtycke och inställningar](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
- [Samtycke i Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### Beräknade attribut

- [Översikt över beräknade attribut](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Användargränssnittshandbok för beräknade attribut](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)

### Övervakning och iakttagbarhet

- [Översikt över aviseringar](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Översikt över Insikter i observationer](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)

### Skyddsräcken

- [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Garantier för kundprofiler i realtid](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Förvaringsskydd](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)

### Självstudiekurser och guider

- [Skapa en självstudiekurs om resan](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Installera SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
