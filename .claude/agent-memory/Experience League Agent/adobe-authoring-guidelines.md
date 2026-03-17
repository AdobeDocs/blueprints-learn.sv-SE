---
name: Adobe Experience League Authoring Guidelines
description: Fullständig referens för redigeringsreglerna för Adobe Experience League-markeringar, som crawlats från den officiella redigeringsguiden i mars 2026.
type: reference
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 0%

---


# Riktlinjer för redigering i Adobe Experience League

Source: https://experienceleague.adobe.com/en/docs/authoring-guide/using/home
Crawlade: 2026-03-15

---

## &#x200B;1. METADATA/FRAMFÖR-FRÅGAN

### Obligatoriska fält
| Fält | Krav | Regler |
|---|---|---|
| `title` | Obligatoriskt | Max 60 tecken (engelska). Versaler. Inga produktnamn om det inte behövs för tydlighet. Systemet lägger till &quot; | ProductName&quot; automatiskt. Radbryt inom citattecken om det innehåller kolon eller parenteser. |
| `description` | Obligatoriskt | Högst 150-160 tecken Kan inte vara tom/null. Koncepten börjar med &quot;Läs mer om..&quot; Aktiviteterna börjar med&quot;Lär dig hur..&quot; eller tvingande verb. |

### Valfria men ofta använda fält
| Fält | Giltiga värden | Anteckningar |
|---|---|---|
| `feature` | Måste matcha YAML-funktionens värden; versaler med blanksteg (t.ex. &quot;Content Fragment&quot;) | 1-2 per artikel; visas i avsnitt |
| `feature-set` | Måste valideras mot funktionen YAML | Överordnat program för funktionen |
| `role` | Användare, utvecklare, ledare, administratör, arkitekt, dataarkitekt, dataingenjör | Skiftlägeskänslig; visas som&quot;Skapad för&quot; |
| `level` | Nybörjare, medelhög, upplevelse | Standardvärdet är nybörjare om ospecificerat |
| `solution` | Måste matcha lösningen YAML (t.ex.&quot;Campaign, Campaign Standard v7&quot;) | Flera värden tillåts; används för sökfiltrering |
| `topic` | Måste matcha ämnet YAML; versaler för rubrik med blanksteg | För produktövergripande filtrering (t.ex.&quot;integreringar&quot;) |
| `type` | Dokumentation, självstudiekurs, felsökning | Repo-level; default to Documentation |
| `short-description` | En mening, max 20 ord | För ExL-landningssidor när beskrivningen är för lång |
| `badgePremium` | `label="Premium" type="Positive" url="..."` | Sidnivåmärke |
| `mini-toc-levels` | 1-6 (standard 2) | Kontrollerar visningsdjup för högerrubrik |
| `hidefromtoc` | true/false | Utesluter från vänster navigering men gör URL-adressen tillgänglig |

### Placering av metadata
- Artikelnivå: top of markdown file as YAML front matter
- innehållsförteckningsnivå: i filen TOC.md
- Repliknivå: i filen metadata.md

### Nyckelformateringsregler
- Radbryt värden som innehåller kommatecken eller parenteser inom citattecken
- Flera värden avgränsade med kommatecken
- Skiftlägeskänslig matchning mot YAML-definitioner
- Tomma/tomma taggvärden orsakar valideringsfel

### Föråldrade fält
seo-title, seo-description, målgrupp, svårighet, uuid (från migrationstidpunkten)

---

## &#x200B;2. MARKERAD SYNTAX (ADOBE-FLAVORED)

### Textformatering
- Fet: `**text**`
- Kursiv: `*text*`
- Fet + kursiv: `***text***`
- Escape-specialtecken: använd omvänt snedstreck `\` före `# { } [ ] * + - . !`
- HTML-entiteter: `&lt;` `&gt;` `&amp;` `&mdash;` `&ndash;`

### Rubriker
- Använd ATX-stil (`#` endast syntax, aldrig understrykning/textformat)
- En H1 per dokument (vanligtvis sidtiteln som matchar metadata `title`)
- Alla efterföljande rubriker H2 (`##`) eller lägre
- Tomma rader som krävs före och efter rubriker (utom den första rubriken)
- Max 69 characters (English) / 120 characters (localized)
- Max ~5 ord rekommenderas
- Inledande versal i mening för alla rubriker (endast inledande ord och avslutande nouns läggs till med versal)
- Endast versaler för metadatafältet `title`
- Inget slutskiljetecken (frågetecken tillåts för rubriker i vanliga frågor)
- Anpassade fästpunkts-ID: `## Title {#custom-id}` - använd bindestreck, inte punkter
- Inga duplicerade rubrikankar-ID:n i ett dokument
- Undvik reserverade ankarnamn: sök, resultat, ansikten, sidnumrering, sortering, fråga, sökruta, innehåll, sidhuvud, sidfot, huvud, navigering, sidospalt, sida, behållare, wrapper
- Följ varje rubrik med minst ett stycke brödtext (placera inte listor/tabeller direkt efter en rubrik)
- Konceptrubriker: substantiv/substantivfraser
- Uppgiftsrubriker: tvingande verb (NOT Ground -&quot;Skapa ett segment&quot;, inte&quot;Skapa ett segment&quot;)
- Parallell struktur över rubriknivåer

### Listor
- Bullet (unordered): `*`, `-` eller `+` - använd konsekvent i ett dokument
- Ordnad: `1.` för varje objekt (automatiska nummer)
- Tomma rader före och efter listor
- Indrag för kapslade numrerade objekt 3 blanksteg; kapslade punkter 2 blanksteg
- Punktskiljetecken: utelämna semikolon/kommatecken/sammansättningar i slutet; lägg endast till punkter för fullständiga meningar
- Lägg inte till punkter om alla objekt är ≤3 ord eller är gränssnittsetiketter/rubriker

### Länkar
- Extern: `[text](https://url.com)`
- Relativ (samma nivå): `[text](file.md)`
- Rotrelativ: `[text](/help/path/file.md)` - måste börja med `/`
- Djuplänkar (samma sida): `[text](#heading-anchor)`
- Djupa länkar mellan dokument: `[text](file.md#heading-id)`
- Tvinga ny flik: `[text](url){target="_blank"}`
- Bare URL:er: bryt i vinkelparenteser `<https://example.com>` för att göra klickbara
- Referenslänkar: endast absoluta länkar fungerar för referenslänkar
- Ta inte med samma fil på flera platser för innehållsförteckningar via relativa länkar
- Windows-användare: konvertera omvända snedstreck till snedstreck i banor

### Bilder
- Grundläggande: `![alt text](image.png "hover tooltip")`
- Ändra storlek: `{width="300"}`
- Justera: `{align="center"}` eller `{align="right"}`
- Zoomable: `{zoomable="yes"}` eller `{modal="regular"}`
- Maximal filstorlek: 100 MB (rekommenderas under 5 MB)
- Alt-text KRÄVS för alla bilder (för SEO och tillgänglighet)
- Bildfilnamn: gemener med bindestreck
- Lagra bilder i en särskild resursmapp

### Kodblock
- Textbunden: backticks `` `code` ``
- Använd för: filnamn, URL:er, användardefinierade termer, kommandon
- Träffade kodblock: trippelbakterier med språkidentifierare

  ```
  ```javascript
  code here
  ```

  ```
  
  
- Alternativ: `{line-numbers="true"}`, `{start-line="7"}`, `{highlight="11-13, 16"}`
- Inkludera alltid en språkidentifierare i avgränsade kodblock

### Tabeller
- Separatorraden kräver minst 3 bindestreck per kolumn: `|---|---|---|`
- Justering: vänster `|---|`, mitten `|:---:|`, höger `|---:|`
- Escape-literalrör: `\|` eller använd `&vert;`
- HTML-tabeller tillåts; använd `<table style="table-layout:auto">` eller `table-layout:fixed`
- Justering av HTML-tabell: `<td align="left|center|right">`
- Undvik markeringssyntax i HTML-tabeller (t.ex. fungerar `[!NOTE]` inte i HTML-tabeller)
- Ta bort kantlinjer: `<tr style="border: 0;">`
- Layoutalternativ för markeringsregister: lägg till `{style="table-layout:auto"}` efter tabell med tomma rader
- Undvik mycket breda/höga tabeller på grund av problem med synlighet i vågrät rullningslist

---

## &#x200B;3. SPECIALTILLÄGG FÖR ADOBE SYNTAX

### Kommentarer/tillägg

```
>[!NOTE]
>
>Text here.

>[!TIP]
>
>Text here.

>[!IMPORTANT]
>
>Text here.

>[!WARNING]
>
>Text here.

>[!CAUTION]
>
>Text here.

>[!ADMIN]
>[!AVAILABILITY]
>[!PREREQUISITES]
>[!INFO]
>[!ERROR]
>[!SUCCESS]
```
- ALLVARLIGT: Inget utrymme mellan `>` och `[!` - använd `>[!NOTE]` NOT `> [!NOTE]`
- Lägg till en tom rad mellan `>[!NOTE]` och brödtextraden

### Tabbar

```
>[!BEGINTABS]

>[!TAB iOS]
Content here

>[!TAB Android]
Content here

>[!ENDTABS]
```

### Komprimerbara avsnitt (dragspel)

```
+++Click to expand
Content inside
+++
```
Obs! Kapslade komprimerbara avsnitt stöds INTE.

### Skuggningsrutor

```
>[!BEGINSHADEBOX "Optional Title"]
Content here
>[!ENDSHADEBOX]
```

### Videor

```
>[!VIDEO](https://video.tv.adobe.com/v/ID/?quality=12&learn=on)
```
Lägg till `{transcript=true}` för transkript.

### Mer som detta

```
>[!MORELIKETHIS]
>* [Article 1](url)
>* [Article 2](url)
```

### Sammanhangsberoende hjälp

```
>[!CONTEXTUALHELP]
>id="..."
>title="..."
>abstract="..."
>additional-url="..."
```

### Badges (Inline)

```
[!BADGE Label]{type=Informative url="https://example.com" tooltip="text"}
```
Typer: `Informative` (blå), `Positive` (grön), `Negative` (röd), `Neutral` (grå), `Caution` (gul)

### Textmarkering (förhandsvisning)

```html
<span class="preview">highlighted text</span>
```

### Innehåller och fragment
- Inkludera hela filen: `{{$include /help/_includes/legal-blurb.md}}`
- Fragment (inga rubriker): `{{snippet-id}}`
- Lagra återanvändbara filer i mappen `help > _includes/`
- Fragment lagrade i `help > _includes/snippets.md`
- Inkluderingar kan ha rubriker; textutdrag KAN INTE
- Fungerar endast inom samma databas (inte korsrepo)
- Escape-tecken `{{` eller `}}` i filer som inte refererar

### DNL-tagg (Do Not Localize)
- `[!DNL ProductName]` - kapslar in produkt-/varumärkesnamn som inte ska översättas
- Används vid första eller väl synliga omnämnanden på en sida

### UICONTROL-tagg
- `[!UICONTROL Button Label]` - kapslar in UI-elementtext (knappar, menyer, fältnamn)
- Ser till att gränssnittssträngar dras från produktdatabaser i stället för maskinöversättning
- Inga apostrofer, citattecken eller skiljetecken i UICONTROL-taggar
- Använd fet formatering för gränssnittselement som refereras i steg

### Funktioner som inte stöds
- Uppgiftslistor (kryssrutor)
- Emoji
- Vågräta linjer
- Kapslade komprimerbara avsnitt

---

## &#x200B;4. FILNAMN OCH MAPPSTRUKTUR

### Namngivningsregler
- Filnamn med gemener och endast bindestreck
- Inga versaler, understreck, punkter eller blanksteg
- Beskrivande SEO-vänliga namn (t.ex. `calculated-metric-overview.md` inte `cmo.md`)
- Undvik siffror i filnamn. Använd beskrivande ord
- Undvik reserverade/motstridiga namn: `metadata.md`, `search.md`
- Byte av namn på live-filer kräver omdirigeringshantering (URL-ändringar)

### Mappstruktur
- Katalog-/mappnamn påverkar INTE URL-adresser (endast reponamn och filnamn påverkar URL-adresser)
- TOC.md styr navigeringshierarkin, inte platsen för Git-mappen
- Lagra bilder/resurser i en särskild resursmapp
- Återanvändbara inkluderar lagrade i `help/_includes/`
- Fragment lagrade i `help/_includes/snippets.md`

### TOC.md Rules
- Alla artiklar måste listas i TOC.md för att kunna återges i Experience League
- H1-format: `# Guide Title {#anchor-id}` - ankaret genererar bas-URL-sökväg
- Avsnittsrubriker måste ha ankar-ID: `+ Section Name {#section-id}`
- Avsnittsrubriker (överordnade objekt) kan inte vara länkar i sig
- Artikellänkar: `+ [Title](path/file.md)`
- Om du ändrar sektionsankare-ID ändras alla kapslade artikel-URL:er (omdirigeringar krävs)
- Använd konsekvent punktformat genomgående (`+`, `*` eller `-`)
- Metadata för innehållsförteckning: `user-guide-description`, eventuellt `breadcrumb-title`
- `mini-toc-levels`: styr visning av rubrik till höger (1-6, standard 2)

---

## &#x200B;5. INNEHÅLLSKVALITET OCH REDAKTIONSSTANDARDER

### Röst och ton
- Aktiv röst framför passiv
- Presentera spänning över framtida spänningar
- Andra person (&quot;du&quot;) för undervisningsmaterial
- Meningar under 35 ord
- Starka, exakta verb - undvik svaga reklamfilmer (&quot;very&quot;,&quot;extreme&quot;)

### Steg/procedurer
- Varje steg är ett enda kortfattat kommando (en mening)
- Ytterligare information läggs in på nästa rad (indragen under steget)
- Starta varje steg med ett obligatoriskt verb
- Begränsa procedurerna till ca 7 steg (max ~10 innan du bryter in i underaktiviteter)
- Placera konceptuell information FÖRE steg
- Placera skärmbilder EFTER relevant steg
- Upprepa sid-/tabbnamn för läsarorientering
- Fet UICONTROL-formatering för gränssnittselement i steg

### Gränssnittsterminologi
- **Öppna/stäng**: program och program
- **Gå till**: menyer, flikar eller gränssnittsplatser
- **Markera**: text, celler eller alternativ från listor
- **Klicka**: musåtgärder (undvik att ange kontrolltyp om det inte är nödvändigt)
- **Listruta** (inte &quot;listruta&quot;)

### Produktnamn
- Lägg inte till produktnamn i rubriker om inte klarheten kräver det
- Uteslut&quot;the&quot; före produktnamn
- Inkludera&quot;Adobe&quot; vid första omnämnandet på konturnivå (varumärkeskrav)
- Släpp&quot;Adobe&quot; på sekundära omnämnanden om det inte är obligatoriskt enligt lag
- Använd DNL-taggar för produktnamn för att förhindra felöversättning

### Betoning och formatering
- Fetstil: gränssnittselement och tangentbordsåtgärder
- Kursiv: Felmeddelanden, främmande ord, betoning
- Kod (backticks): Filnamn, URL:er, användardefinierade termer
- Inga citattecken runt gränssnittselement (använd taggen UICONTROL i stället)

### Versaler
- Meningsfall för rubriker, navigering, underrubriker
- Endast versaler för `title`-metadatafält
- Korrekta substantiv alltid med versaler

---

## 6. SEO BEST PRACTICES

- En H1 per sida - måste vara kortfattad, beskrivande, informera användarna om vad sidan handlar om
- Sekventiell rubrikhierarki (h1 → h2 → h3, aldrig hoppnivåer)
- Inkludera nyckelord i H1, brödtext och metadata (inte meta-taggen `keywords` - Google ignorerar den)
- Undvik problem med nyckelord (återgivning > frekvens)
- Titel: max. 50-60 tecken; systemet lägger till &quot;| Adobe ProductName&quot; automatiskt
- Beskrivning: 150-160 tecken; ska vara en call to action, inte en upprepning av innehåll
- Lägg till beskrivande alternativ text i alla bilder
- Inkludera videomaterial (sökmotorer kan bara läsa text)
- Länka strategiskt till relaterade sidor (undvik överblivna sidor)
- Inkludera strukturerade element: numrerade listor, underrubriker, kodblock
- Använd verktyg som AnswerThePublic, Google Trends to research keywords
- Innehållet ska visa E-E-A-T (erfarenhet, expertis, auktoritativitet, tillförlitlighet)

---

## &#x200B;7. LOKALISERING

### Maskinöversättning först
- Innehåll i engelsk källa genererar automatiskt lokaliserade versioner
- Språk som stöds: tyska, franska, japanska, italienska, spanska, brasiliansk portugisiska, förenklad kinesiska, traditionell kinesiska, koreanska, nederländska, svenska

### Skriva för lokalisering
- Enhetlig terminologi genom hela
- Korta meningar och aktiv röst
- Engelsk standardordordning (ämne → verb → objekt)
- Använd relativa uttal (&quot;that&quot;,&quot;which&quot;)
- Undvik: humor, idiom, jargon, regionala fraser, metaforer, onödiga ord

### Lokaliseringstaggar
- `[!UICONTROL Label]` - garanterar att gränssnittssträngar hämtas från produktdatabasen, inte maskinöversätts
- `[!DNL ProductName]` - förhindrar att produkt-/varumärkesnamn översätts
- Bilder i en&quot;do-not-localize&quot;-mapp undantas från lokalisering

---

## &#x200B;8. INNEHÅLLSTYPER

- **Guide**: Onlinesamling med sidor som refereras i en innehållsförteckning, innehåller bästa praxis
- **Självstudiekurs**: Instruktionsinnehåll (video eller text) för specifika användningsfall, publicerat i utbildningsrapporter
- **Referenshandbok**: Utvecklar-API:er/SDK:er, vanligtvis tabellformat; publiceras på developer.adobe.com
- **Kurs**: Expertstrukturerad samling lektioner för specifika användarroller
- **Kunskapsbasartiklar**: Kortfattad, tillfälligt relevant felsökningsinnehåll
- **Landningssida/startsida**: Hanteras separat (SCCM)

---

## &#x200B;9. VANLIGA VALIDERINGSFEL SOM SKA UNDVIKAS

- `title`- eller `description`-metadata saknas
- `description` börjar inte med &quot;Läs om..&quot; eller&quot;Lär dig mer..&quot;
- Avstånd mellan `>` och `[!` i bildtextens syntax (`> [!NOTE]` i stället för `>[!NOTE]`)
- Blanksteg i fetstil: `**text **` (avslutande blanksteg bryts i fet stil)
- Markeringssyntax i HTML-tabeller (t.ex. pratbubblor fungerar inte där)
- Duplicera rubrikankar-ID:n i ett dokument
- Ankarpunkts-ID:n som innehåller punkter (använd bindestreck i stället)
- Använda reserverade ankarnamn (sökning, resultat, sidhuvud, sidfot osv.)
- `role`, `level`, `feature`, `topic` värden som inte matchar YAML-definitioner
- Staplade rubriker utan brödtext mellan dem
- H1 används mer än en gång per dokument
- Överhoppade rubriknivåer (t.ex. H1 → H3)
- Namnge filer med versaler, understreck eller mellanslag
- Alt-text saknas i bilder
- Rubriker för bakgrundsuppgifter (&quot;Skapar..&quot;) i stället för&quot;Skapa..&quot;)
