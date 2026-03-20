---
name: industry-use-case-builder
description: 'Guider för framtagning av nya användningsexempel för Adobe Experience Platform-databasen med utkast. Använd den här kompetensen när du lägger till ett nytt användningsexempel till en vertikal bransch (detaljhandel, bil, sjukvård, finansiella tjänster, försäkring, media och underhållning, telekommunikation, resor och turism, B2B), när användaren vill lägga till affärsscenarier till branschsidor eller när användaren uppdaterar fallkatalogen. Hanterar hela arbetsflödet: samla in information om användningsfall, bedöma mognadsnivå, generera innehåll, uppdatera sidan med branschöversikt och använd fallkatalog samt anropa färdigheter för att skapa ikoner med"use-case-icon".'
source-git-commit: ed8928687806b619e95d8d320478d27c13722a80
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 1%

---


# Bygg industrianvändningsfall

Denna kunskap vägleder framtagningen av nya användningsexempel för Adobe Experience Platform-databasen med utkast. Följ varje fas sekventiellt. Läs referensfilerna innan du börjar:

- `references/use-case-template.md` - exakt mall för fallavsnitt
- `references/catalog-row-template.md` - exakt format för katalogtabellrader
- `references/maturity-criteria.md` - detaljerad information för förfallobedömning

## Fas 1: Informationsinsamling

Intervjuera användaren för att samla in all nödvändig information innan något innehåll genereras.

### Obligatoriska fält

1. **Branschvertikal** - Måste vara något av:
   - bil
   - b2b
   - finansiella tjänster
   - hälsovård
   - försäkring
   - mediaunderhållning
   - butik
   - telekommunikation
   - resegästfrihet

2. **Använd ärendenamn** - En tydlig, beskrivande titel (t.ex. &quot;Avbruten återfinnande av kundvagn&quot;, &quot;Kampanjer för läkemedelsregistrering&quot;).

3. **Beskrivning** - 1-2 meningar som beskriver affärsscenariot och varför det gäller.

4. **Affärspåverkan** - kvantifierade resultat med specifika mått (t.ex.&quot;20-30 % ökning av klickfrekvensen&quot;,&quot;15-25 % förbättring av återfyllnadsgraden&quot;).

5. **Använd fallmönster** - Måste mappas till exakt ett av dessa befintliga mönster:
   - Audience Activation till mål
   - Målgrupps-Collaboration med segmentmatchning
   - Vidarebefordran av händelser
   - B2B Audience Activation
   - Anonym besökare på Personalization
   - Known-Visitor Web/App Personalization
   - Offer Decisioning (erbjudandebeslut)
   - Beteenderekommendation
   - Aktivering av utgående batchmeddelande
   - Händelseutlöst meddelanden
   - Flerstegsdirigerad resa
   - Flerkanalsresor med beslut
   - Köpa gruppbaserad marknadsföring och resehantering
   - Kundanalys och insiktsgenerering
   - B2B-analys
   - Brand Concierge Conversational Experience

6. **Tekniska överväganden** - 4-8 punkter som täcker datakrav, integreringar, krav på regelefterlevnad, prestanda och arkitektoniska anteckningar.

Fråga efter saknade fält innan du fortsätter. Ta inte på dig eller beskriv detaljer.

## Fas 2: Löptidsbedömning

Läs `references/maturity-criteria.md` om du vill se hela rubrikröningen. Tilldela en av tre mognadsnivåer:

- **Foundational** `[!BADGE Foundational]{type=Neutral}` - Ettstegs- eller händelseutlösta mönster (händelseutlösta meddelanden, utgående batchvis), enkla datakrav, minimal AI/ML, standardintegreringar.
- **Nya** `[!BADGE Emerging]{type=Informative}` - Flerstegsresor, beteendedata, rekommendationsmodeller, kända besökarpersonaliseringar, måttlig komplexitet i integreringen.
- **Avancerat** `[!BADGE Advanced]{type=Caution}` - Flerkanalsbeslut, AI-driven förutsägelse, offertbeslut, komplex orkestrering, flera systemintegreringar.

### Utvärderingsarbetsflöde

1. Identifiera vilket användningsmönster som användningsfallet mappas till.
2. Kontrollera listan&quot;Typiska mönster&quot; i mognadskriterierna för att få en snabb matchning.
3. Om mönstret inte tydligt visar mognad, utvärdera datakomplexitet, AI/ML-krav och integreringsomfång.
4. Presentera utvärderingen för användaren med en motivering: &quot;Baserat på mönstermappningen ({pattern}) och {key factors} klassificerar jag den som {level} eftersom {reasoning}.&quot;
5. Vänta tills användaren bekräftar eller åsidosätter innan du fortsätter med innehållsgenereringen.

## Fas 3: Generering av innehåll

Generera eller uppdatera innehåll i två filer.

### A. Branschöversikt

**Filsökväg:** `/help/blueprints/industry-use-cases/{industry}/{industry}-overview.md`

Läs den befintliga filen först för att få en förståelse för den aktuella strukturen och innehållet. Lägg sedan till ett nytt avsnitt som följer den exakta mallen från `references/use-case-template.md`:

```markdown
## {Use Case Title}

{1-2 sentence description of the business scenario and why it matters}

### Business impact

{Quantified business outcomes, e.g., "Retailers typically see a 20-30% increase in click-through rates..."}

### How to implement

Use the [{Pattern Name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md) pattern. {1-2 sentence explanation of why this pattern applies}

### Technical considerations

- {4-8 bullet points covering data integration, regulatory, performance, or architectural considerations}
```

Placera det nya avsnittet efter befintliga användningsfallsavsnitt, med konsekvent formatering.

### B. Använd fallkatalog

**Filsökväg:** `/help/blueprints/industry-use-cases/use-case-catalog.md`

Läs den befintliga katalogfilen först. Lägg till en ny rad på rätt flik. Katalogen använder en flikstruktur med `>[!TAB {Industry}]` markörer. Varje flik innehåller en tabell med följande kolumner:

| Kolumn | Innehåll |
| --- | --- |
| Ikon | `<img src="assets/use-case-icons/{industry}/icon-{kebab-name}.png" alt="{Alt Text}" width="40">` (lämna tomt om ingen ikon ännu) |
| Användningsfall | `[{Use Case Title}]({industry}/{industry}-overview.md#{anchor})` där ankarpunkt är rubriken i nyckelrutor |
| Beskrivning | Sammanfattning av en mening |
| Löptid | Syntax för märke för tilldelad nivå |
| Mönster | `[{Pattern Name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md)` |

**Placeringsregel:** Inom varje flik i branschen grupperas rader efter mognad i den här ordningen: först Foundational, sedan Emerging och sedan Advanced. Placera den nya raden i slutet av rätt löptidsgrupp.

Mönsterfilsökvägarna är:
- `audience-building-activation/audience-activation-to-destinations.md`
- `audience-building-activation/audience-collaboration-segment-match.md`
- `audience-building-activation/event-forwarding.md`
- `audience-building-activation/b2b-audience-activation.md`
- `personalization/anonymous-visitor-web-personalization.md`
- `personalization/known-visitor-web-app-personalization.md`
- `personalization/offer-decisioning.md`
- `personalization/behavioral-recommendation.md`
- `campaign-management-orchestration/batch-outbound-message-activation.md`
- `campaign-management-orchestration/event-triggered-messaging.md`
- `campaign-management-orchestration/multi-step-orchestrated-journey.md`
- `campaign-management-orchestration/cross-channel-journey-with-decisioning.md`
- `campaign-management-orchestration/buying-group-based-marketing.md`
- `analysis/customer-analytics-insight-generation.md`
- `analysis/b2b-analytics.md`
- `conversational-experience/brand-concierge-conversational-experience.md`

## Fas 4: Ikongenerering

När innehållet har skapats anropar du `use-case-icon-generator`-kompetensen för att generera en ikonspecifikation för det nya användningsfallet. Förverkliga dina kunskaper med:
- Namn på användningsfall
- Branschvertikalt
- En kort beskrivning av användningsfallet

När användaren har skapat ikonfilen uppdaterar du katalograden så att den innehåller ikonreferensen:

```
<img src="assets/use-case-icons/{industry}/icon-{kebab-name}.png" alt="{Alt Text}" width="40">
```

## Fas 5: Validering

Kontrollera följande innan du slutför:

1. **Mallkompatibilitet** - Branschöversiktsavsnittet följer mallen exakt (# heading, description, ### Business impact, ### How to implement, ### Technical Consights).
2. **Katalogplacering** - Katalograden finns på rätt branschflik och i rätt mognadsgrupp (Foundation, Emerging, sedan Advanced).
3. **Mönsterlänkens giltighet** - Mönsterlänken i både översikten och katalogen använder en giltig mönsterfilssökväg från listan ovan.
4. **Ankarkonsekvens** - Ankaret i kataloglänken (t.ex. `#abandoned-cart-email-recovery`) matchar rubriken `##` i översiktsfilen konverterad till&quot;kebabcase&quot;.
5. **Konventioner för ikonsökväg** - Ikonens sökväg följer `assets/use-case-icons/{industry}/icon-{kebab-name}.png`.

Rapportera eventuella problem som uppstår under valideringen och åtgärda dem innan du slutför.
