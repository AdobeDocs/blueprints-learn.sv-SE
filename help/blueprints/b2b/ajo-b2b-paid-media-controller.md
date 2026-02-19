---
title: AJO B2B - betald mediestyrenhet
description: Prioritet för kampanjer och aktivering av konton för betalmediernas destinationer
solution: Journey Optimizer B2B Edition
source-git-commit: dff5608af92fa1140419d6834d8374df75de98d3
workflow-type: tm+mt
source-wordcount: '1392'
ht-degree: 0%

---

# Översikt

Marknadsföringsteam som kör betalda B2B-medier i stor skala stöter på ett återkommande problem: **kontona hamnar i flera kampanjer samtidigt** (persona, kategorimedvetenhet, lösningsstyrd, jakt), vilket späder ut meddelanden, utlöser målgruppströtthet och tvingar till manuellt listarbete - överföringar, uteslutningar och nedtryckning - i LinkedIn Account Match (kontomål). Utan **vattenfallsprioritering** och **automatiserad kampanjtilldelning** finns det ingen plats att bestämma vilket konto som ska få vilket meddelande, och åtgärderna skalas inte.

**Betalad mediestyrenhet** är en perfekt lösning på det här problemet. Den använder **Adobe Journey Optimizer B2B edition (AJO B2B)** och **Adobe Experience Platform (AEP)** tillsammans: en **kontoresa** läser en kvalificerad målgrupp från Real-Time CDP, tillämpar **logik med delade sökvägar (vattenfall)** för att tilldela varje konto till exakt en kampanjnivå och **aktiverar varje sökväg direkt** till betalda mediemål (**t.ex. kedIn Matched Audiences**) - utan manuell överlämning av listor. Resultatet är precisionskontroll, mindre överlappning och ett repeterbart mönster för multikanals B2B-betalda medier.

## Användningsfall: En marknadsförares berättelse: Varför en styrenhet är viktig

*Maya leder till betalmedier för ett globalt B2B-varumärke. Hennes team driver dussintals kampanjer - grundläggande medvetenhet, kategoriavsikt (resor, data, innehåll), lösningsledda program, personkampanjer och&quot;must-win&quot;-aktiviteter. Hon har ett problem.*

**Problemet:** Samma konton visas i flera kampanjer. Ett målgruppskonto finns också på en bred lista över medvetenheten. Ett efterföljarkonto får fortfarande persona annonser. Listöverföringar och undantag är manuella. Varje gång försäljningen uppdaterar en&quot;must-win&quot;-lista eller en ny personlig kampanj lanseras, exporterar hennes team om målgrupper, förenar överlappningar i kalkylblad och överför på nytt till LinkedIn och andra plattformar. Den är långsam, felbenägen och skalas inte.

**Vad hon vill ha:** En plats där varje kvalificerat konto utvärderas en gång, tilldelas den *mest relevanta* kampanjen med hjälp av tydliga prioritetsregler (vattenfall) och skickas till rätt betalmediemål automatiskt. Inga manuella överlämningar. När data eller strategi ändras utvärderas och flyttas kontona mellan olika kampanjer utan att deras team behöver ändra sina listor.

**Adobe-svar:** Med **AJO B2B och AEP i samarbete** kan Maya köra en enda **betald mediakontrollant**-resa: AEP och Real-Time CDP har data och en &quot;kvalificerad huvudkontors&quot; målgrupp. AJO B2B kör en kontoresa där **tvåvägslogik** (vattenfall) används för att dirigera varje konto till rätt nivå, t.ex. Utifrån → Lösningsrelaterad → Persona → Kategorimedvetenhet → Gränssnittsmedvetenhet - och **Aktivera till mål** skickar varje sökväg till rätt LinkedIn-kampanj (eller annan). En resa, en sanningskälla, ingen manuell listexport. Det är det Betalda mediestyrenhetsmönstret - och det är så Adobe möjliggör precision och skala för B2B-betalda medier.

## Varför det är viktigt för B2B-företag:

Organisationer som använder det här mönstret kan helt ta bort manuell inaktivering och exkluderingslogik (t.ex. 100 % av överlappningsupplösningen som hanteras under resan), skala till **tiotusentals konton** via en enda styrenhet och behålla en **enda källa till sanning** för vilket konto som ska användas. Systemet **anpassar automatiskt** när kampanjfokus, målgrupper och försäljningsmål ändras, utan att behöva exportera om listor eller överföra dem till varje plattform igen. För alla B2B-företag som kör flera betalda mediekampanjer ger mönstret Betald mediestyrenhet den tydlighet, kontroll och automatisering som manuella listarbetsflöden inte kan hantera.

Följande nyckeltal är väl anpassade efter mätningen:

- **Medvetenhet:** Ser målkontona rätt annonser och flyttar till rätt kampanjer i högre frekvens?
- **Engagemang:** Är engagemang och konvertering bättre när överlappning tas bort?
- **Effektivitet:** Hur mycket har det manuella listarbetet (överföringar, undantag, inaktivering) minskat?
- **Kostnad:** Hur ändras kostnaden per förvärvat konto eller affärsmöjlighet med automatisk samordning?

## Betald Media Journey-orkestrering

Ett vanligt användningsexempel, och fokus för den här planen, är **betald mediesändning från B2B**: att se till att varje kvalificerat konto tilldelas exakt en kampanjnivå och aktiveras till rätt betalmediemål, utan överlappning eller manuella överlämningar.

Kontrollenhetsresan **läser** en målgrupp med kvalificerade konton (inbyggt i Real-Time CDP från AEP-data), **utvärderar** varje konto genom villkor för delade sökvägar (vattenfall), t.ex. följande → lösningsledda → persona → kategorimetod → grundläggande, och **aktiverar** varje sökväg till motsvarande mål (t.ex. LinkedIn Matched Audiences för varje kampanj).

**Kontofokuserad lösning:** Fokus för den betalande mediestyrenheten är **konton** och deras **kampanjtilldelning**. Den tekniska konfigurationen stöder de data och målgrupper som representerar kvalificerade konton och deras attribut (t.ex. avsikt, segment, persona), vilket krävs för framgångsrik segmentering på kontonivå och resebaserad samordning.

## Krav

Den kontofokuserade lösningen kräver följande program och tjänster:

- **Adobe Journey Optimizer B2B edition** - Kontoresor, logik för delad sökväg (vattenfall), Aktivera till mål.
- **Adobe Customer Data Platform (RTCDP) B2B edition** i realtid - kontoprofiler, kontomålgrupper (t.ex. kvalificerade konton för betalda media).

## Arkitektur

Högnivåflöde:

1. **Data och målgrupper** - AEP innehåller profiler och evenemang; Real-Time CDP B2B skapar kontomålgrupper (t.ex.&quot;Betald medieberättigande konton&quot;) som används som målgrupp för reseanmälan.
2. **Orchestration** - AJO B2B-kontoresa: **Läsa målgrupp** (kvalificerade konton) → **Delad sökväg** (vattenfall: t.ex. Continit → Solution-Led → Persona → Category → Foundational) → **Aktivera till mål** (per sökväg till LinkedIn eller andra betalda medier).
3. **Destinationer** - Betalda mediekanaler (t.ex. LinkedIn Matched Audiences) får aktivering på kontonivå från varje resa; inga manuella listöverföringar.

## Arkitekturdiagram

<img src="assets/ajo-b2b-paid-media-activation-architecture.svg" alt="AJO B2B Betald Media Controller Architecture" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## Datamodellering i B2B AEP

Med all datadriven orkestrering är schemadesign viktigt. Konto- och personprofiler i AEP/RTCDP måste innehålla de attribut som används i **tvåvägsvillkor** (t.ex. uppföljningsflagga, lösningsintresse, persona, intent-kategori, engagemangspoäng). B2B-scheman (XDM Business Account, XDM Individual Profile, Relational) ska representera hierarkin och datakällorna. Mer information finns i [RTCDP B2B-scheman](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview) och [AJO B2B-dokumentation](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/home).

**Obs!** Logiken för delad sökväg i resan använder profiler och, om det stöds, relationsdata. Kontrollera att fälten som du behöver för logik för vattenfall är tillgängliga under resan.

### Skyddsräcken

- **Journey Optimizer B2B edition** - I [produktbeskrivningen](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer-b2b.html) finns information om resebegränsningar, nodbegränsningar och stöd för destinationer.
- **Real-Time CDP** - Se [RTCDP skyddsutkast](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/guardrails/overview) för information om begränsningar för segmentering och aktivering.

## Implementering

I följande steg beskrivs hur du implementerar den betalande mediestyrenheten med AJO B2B och AEP.

### Krav-steg

1. **Definiera kontomålgrupper och datamodell i Real-Time CDP B2B.**

   Skapa den **kvalificerade målgruppen** (t.ex. &quot;Betald medieberättigande konton&quot;) som kommer att gå in på styrenhetens resa. Använd Segment Builder och de konto-/personattribut som definierar behörighet (t.ex. geografi, segment, MQA-status). Den här målgruppen är den enda ingångspunkten för resan.

2. **Definiera kampanjhierarki och delningslogik.**

   Dokumentera vattenfallsordningen (t.ex. Pursu→ Solution-Led → Persona → Kategori → Foundational) och villkoren för varje bana (vilka attribut eller målgrupper kvalificerar ett konto). Se till att villkoren **utesluter varandra i ordningen** (nedrullningsbar): ett konto bör matcha högst en sökväg, den första som utvärderas som sann.

3. **Konfigurera mål.**

   Ställ in betalmediemål (t.ex. LinkedIn Matched Audiences) i AEP/RTCDP och se till att de är tillgängliga för aktivering från AJO B2B. Mappa kontoidentifierare och eventuella obligatoriska attribut för varje mål.

### Konfiguration av betald mediestyrenhet

1. **Skapa kontrollenhetsresan i AJO B2B.**

   - **Läs målgrupp:** Välj den kvalificerade kontomubliken från Real-Time CDP.
   - **Delad sökväg:** Lägg till noder i vattenfallsordning. Varje nod utvärderar villkor (t.ex. &quot;in Pursuit publik&quot;, &quot;solution interest = X&quot;, &quot;persona = Y&quot;, &quot;intent category = Z&quot;). Konton som matchar avslut till motsvarande aktivering, andra fortsätter till nästa delning.
   - **Aktivera till mål:** För varje sökväg lägger du till en Aktivera till målnod i rätt LinkedIn-kampanj/mål (eller annan).

2. **Validera ömsesidig exklusivitet.**

   - Bekräfta att varje konto bara anger en sökväg (det första matchande villkoret).
   - Verifiera aktivering: konton visas på rätt plats och är exkluderade från kampanjer med låg prioritet enligt vad som är avsett.

## Implementeringsdiagram

<img src="assets/ajo-b2b-paid-media-controller-canvas.svg" alt="AJO B2B - betald mediestyrenhet - arbetsyta" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

### 4.2.3. Målgruppsaktivering

1. **Aktivera till LinkedIn (och andra mål).**

   Använd&quot;Aktivera till mål&quot; under resan för att skicka varje väg till rätt betald mediepublik. Ingen manuell export eller överföring av listor; resan driver aktiveringen när kontona löper genom sökvägar.

2. **Övervaka och justera.**

   Använd reserapportering för att övervaka volymer per sökväg.

## Sammanfattning

I den **betalda mediekontrollantens**-översikten visas hur **AJO B2B och AEP** samverkar för att ge B2B-marknadsförare ett enda automatiserat sätt att tilldela konton till kampanjer och aktivera för betalda medier: en huvudmålgrupp, en resa, vattenfallslogik och direktaktivering till destinationer - ingen manuell överlämning av listor. Det skapar ett repeterbart mönster för multichannel B2B-baserad mediehantering och hjälper till att minska överlappning, förbättra relevansen och skalningsåtgärder.

## Relaterad dokumentation

- [Köper en koncernbaserad plan för marknadsföring och resehantering](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/b2b-activation/b2b-buying-group-journeys) - Konto- och inköpsgruppresor i AJO B2B.
- [Adobe Journey Optimizer B2B edition](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b) - produktdokumentation.
- [Kunddataplattform B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview) i realtid - målgrupper och aktivering av konton.
