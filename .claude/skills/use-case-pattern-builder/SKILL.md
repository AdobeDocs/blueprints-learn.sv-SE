---
name: use-case-pattern-builder
description: 'Guider för att skapa nytt fallmönsterinnehåll för Adobe Experience Platform-databasen med utkast. Använd den här kompetensen när du lägger till ett nytt användningsmönster, skapar innehåll med vägledning för implementering eller när användaren talar om att mönster ska läggas till på webbplatsen med utkast. Hanterar hela arbetsflödet: samla in mönsterinformation, generera markeringsfilen med rätt mallstruktur och uppdatera alla korsreferenssidor (TOC.md, overview.md).'
source-git-commit: ed8928687806b619e95d8d320478d27c13722a80
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 0%

---


# Använd mönsterverktyget

Den här kunskapen hjälper dig att skapa ett nytt användningsmönster för Adobe Experience Platform ritningar. Den hanterar hela arbetsflödet: samla in mönsterinformation från användaren, generera filen med markerat innehåll med rätt mallstruktur och uppdatera alla korsreferenssidor så att det nya mönstret kan upptäckas.

Innan du startar läser du följande referensfiler för den fullständiga mallstrukturen och checklistan för de sidor som ska uppdateras:

- `references/pattern-template.md` - den fullständiga markeringsmallen med platshållarvärden
- `references/pages-to-update.md` - checklistan för sidor som måste uppdateras när ett mönster läggs till

## Fas 1: Informationsinsamling

Intervjuera användaren för att samla in all nödvändig information innan några filer genereras. Fråga efter följande och fortsätt inte med innehållsgenerering förrän varje objekt anges eller uttryckligen skjuts upp.

### Nödvändig information

1. **Mönsternamn** - Den läsbara titeln (t.ex. &quot;Event-Triggered Messaging&quot;).

2. **Kategori** - Exakt ett av följande:
   - `audience-building-activation`
   - `personalization`
   - `campaign-management-orchestration`
   - `analysis`
   - `conversational-experience`

3. **Beskrivning av primär funktion** - En enda mening som beskriver vad det här mönstret gör (används i översiktstabellen och i beskrivningen av frontmatet).

4. **Adobe kärnlösningar** - Adobe-produkterna är centrala för detta mönster. Välj mellan: Journey Optimizer, Real-Time Customer Data Platform, Experience Platform, Customer Journey Analytics, Brand Concierge, Journey Optimizer B2B edition, Real-Time CDP B2B edition eller andra.

5. **Steg i funktionskedjan** - 3-6 sekventiella faser som beskriver mönstrets körningsflöde, avgränsade med `>`. Exempel:&quot;Händelseinmatning > Reseanmälan > Villkorsutvärdering > Meddelandeleverans > Rapportering&quot;.

6. **Affärsmål som stöds** - Ett eller flera affärsmål från den befintliga uppsättningen under `/help/blueprints/business-objectives/`. Alla ska innehålla målnamnet, undermappen för kategorin och filnamnet. Kontrollera att de refererade filerna finns innan du genererar innehåll.

7. **Exempel på exempel på taktiska användningsområden** - 6-10 punktbaserade scenarier som beskriver hur mönstret kan användas i olika affärskontexter. Varje scenario ska ha ett fetstilt namn följt av en beskrivning.

8. **KPI:er** - En tabell med tre kolumner: KPI (namn), Beskrivning (mått), Mätning (formel eller metod).

9. **Implementeringsalternativ** - 2-4 implementeringsalternativ. För varje alternativ:
   - Alternativnamn
   - Bäst för (när detta alternativ ska användas)
   - Så här fungerar det (2-4 stycken)
   - Viktiga överväganden (punktlista)
   - Fördelar (punktlista)
   - Begränsningar (punktlista)
   - Experience League-länkar (URL:er till relevant dokumentation)

### Valfritt men rekommenderas

- Använd skiftlägesöversiktsstycken (3-5 stycken, om de inte anges, gör ett utkast från den andra informationen)
- Programlista med beskrivningar av varje Adobe-programs roll
- Foundational functions table (function, status, What Must be in Place, Experience League Reference)
- Tabell med stödfunktioner (Function, Status, Why It Matters, Experience League Reference)
- Programfunktionstabeller (en per program, med Function, Implementeringsfas, Description)
- Kontrollista för krav

Om användaren inte tillhandahåller de valfria objekten genererar du rimliga standardvärden baserat på mönsterkategorin, lösningarna och funktionskedjan.

## Fas 2: Generering av innehåll

Generera mönstermarkeringsfilen på följande sökväg:

```
/help/blueprints/use-case-patterns/{category}/{kebab-case-pattern-name}.md
```

Filnamnet måste innehålla&quot;kebab-case&quot; som härletts från mönsternamnet. Till exempel blir&quot;Händelseutlöst meddelande&quot; `event-triggered-messaging.md`.

Använd mallen från `references/pattern-template.md` och fyll i alla platshållarvärden med den insamlade informationen. Den genererade filen måste innehålla alla avsnitt i mallen:

1. **YAML-frontmateria** - titel, beskrivning, lösning (kommaseparerad), exl-id (generera en UUID-platshållare som `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx` - publiceringsteamet tilldelar den riktiga).

2. **Öppnar avsnitt** — `# {Pattern name}` följt av ett inledande stycke och&quot;Använd den här guiden för att förstå..&quot; mening.

3. **Använd fallöversikt** - 3-5 stycken som beskriver mönsteromfånget, när det är tillämpligt, vad det gör och inte gör samt vilka som är de vanliga intressenterna.

4. **Viktiga affärsmål** - Varje mål som en länkad rubrik med en kort beskrivning och en sammanfattningsrad för nyckeltal.

5. **Exempel på exempel på taktiska användningsområden** - punktlista över 6-10 scenarier.

6. **Nyckeltal för prestandaindikatorer** - Tabell med KPI, Beskrivning, Mätningskolumner.

7. **Använd fallmönster** - Beskriv stycket och funktionskedjan.

8. **Program** - Lista över Adobe-program med `[!DNL ...]` formatering och beskrivningar.

9. **Foundationsfunktioner** - Tabell med kolumner: Foundational Function, Status, What Must be in Place, Experience League Reference. Statusvärden: Obligatoriskt, antaget på plats, ej tillämpligt.

10. **Stödfunktioner** - Tabell med kolumner: Stödfunktioner, Status, Varför det är viktigt, Experience League-referens. Statusvärden: Rekommenderat, Inkluderat, Ej tillämpligt.

11. **Programfunktioner** - En tabell per program med kolumner: Function, Implementation Phase, Description.

12. **Förutsättningar** - Checklista med syntax `- [ ]`.

13. **Implementeringsalternativ** - 2-4 detaljerade alternativ, var och en med Bästa för, Hur det fungerar, Viktiga överväganden, Fördelar, Begränsningar och Experience League-länkar.

14. **Alternativjämförelse** - Jämförelsetabell i slutet.

## Fas 3: Korsreferensuppdateringar

Uppdatera följande filer när du har genererat mönsterfilen. Läs `references/pages-to-update.md` för den detaljerade checklistan.

### TOC.md

**Fil:** `/help/blueprints/TOC.md`

Lägg till en ny post under rätt kategoriavsnitt. Kategorierna mappas till följande avsnitt i innehållsförteckningen:

| Kategoriinstruktionsmarginal | Avsnittsrubrik för innehållsförteckning |
| --- | --- |
| `audience-building-activation` | `+ Audience Building & Activation{#audience-building-activation}` |
| `personalization` | `+ Personalization{#personalization-patterns}` |
| `campaign-management-orchestration` | `+ Campaign Management & Orchestration{#campaign-orchestration-patterns}` |
| `analysis` | `+ Analysis{#analysis-patterns}` |
| `conversational-experience` | `+ Conversational Experience{#conversational-experience-patterns}` |

Postformatet är:

```
    + [{{Pattern Title}}](/help/blueprints/use-case-patterns/{{category}}/{{filename}}.md)
```

Lägg till den nya posten efter den sista befintliga posten i det matchande avsnittet. Bevara det exakta indraget (fyra blanksteg före `+`).

### Översiktssida

**Fil:** `/help/blueprints/use-case-patterns/overview.md`

Lägg till en ny rad i rätt kategoritabell. Formatet är

```
| [{{Pattern Title}}]({{category}}/{{filename}}.md) | {{Primary capability description}} | [!DNL {{Solution1}}], [!DNL {{Solution2}}] |
```

Lägg till den nya raden efter den sista befintliga raden i den matchande kategoritabellen.

## Fas 4: Validering

När alla filer har skapats och uppdaterats kontrollerar du följande:

1. **Affärsmållänkar** - Varje affärsmålslänk i mönsterfilen pekar på en befintlig fil under `/help/blueprints/business-objectives/`. Använd glob eller läs för att bekräfta att respektive målfil finns.

2. **Placering av innehållsförteckningspost** - Den nya innehållsförteckningsposten finns i rätt kategoriavsnitt och använder rätt indrag och sökvägsformat.

3. **Översikt över tabellrad** - Den nya översiktsraden finns i rätt kategoritabell och har samma kolumnformat som befintliga rader.

4. **Filnamngivning** - Mönsterfilnamnet använder kebab-case och matchar sökvägen som refereras i både TOC.md och overview.md.

5. **Slutlighet för främmande objekt** - Mönsterfilen innehåller titel, beskrivning, lösning och exl-id i YAML-förhandsgranskningen.

6. **Experience League-länkar** - Kontrollera att alla Experience League-URL:er är tillförlitliga (börja med `https://experienceleague.adobe.com/sv`).

Rapportera eventuella valideringsfel till användaren och åtgärda dem innan uppgiften slutförs.

## Anteckningar

- Använd alltid syntaxen `[!DNL ...]` för Adobe-produktnamn i tabeller och brödtext, enligt vedertagen standard för befintliga mönsterfiler.
- `exl-id` i den främsta komponenten ska vara en platshållare för UUID. Publiceringsflödet tilldelar det verkliga värdet.
- Om användaren vill skapa flera mönster samtidigt upprepar du Fas 2-4 för varje mönster, men samlar in all information i Fas 1.
- Om det behövs en ny kategori som inte finns med i listan ovan varnar du användaren om att TOC.md och overview.md kommer att behöva skapa nya avsnitt och hanterar det som ett separat steg.
