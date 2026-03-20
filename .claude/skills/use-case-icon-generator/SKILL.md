---
name: use-case-icon-generator
description: Generera ikonspecifikationer och bildgenereringsprompter för ikoner i Adobe Experience Platform-databasen med utkast. Använd den här färdigheten när du skapar ikoner för nya användningsområden i branschen, när en ikon behövs för att skapa eller uppdatera en användares färdigheter eller när användaren frågar om att skapa eller uppdatera en ärendeikon. Visar en detaljerad uppmaning om att skapa bilder som användaren kan använda tillsammans med Midjourney, DALL-E, Adobe Firefly eller liknande verktyg, tillsammans med rätt filnamngivning och placering.
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---


# Använd ikongenerator för ärende

Generera detaljerade ikonspecifikationer och AI-bildgenereringstexter för fallsymboler i databasen med utkast.

## När ska denna kompetens användas

- Skapa ett nytt användningsfall som behöver en ikon
- Anropas av branschens Fallbyggarskicklighet för att generera en ikonspecifikation
- Användaren frågar om du vill skapa, uppdatera eller ersätta en skiftlägesikon
- Användaren vill generera en grupp ikoner för en ny vertikal bransch

## Steg 1: Samla in indata

Samla in följande information från användaren eller från den anropande kompetensen:

**Obligatoriskt:**
- **Använd fallnamn** - Det läsbara namnet på användningsfallet (t.ex. &quot;Övergiven kundvagn&quot;, &quot;Blypoäng&quot;)
- **Branschvertikal** - En av: bil, b2b, finansiella tjänster, hälso- och sjukvård, försäkring, mediaunderhållning, detaljhandel, telekommunikation, resegästfrihet
- **Kort beskrivning** - 1-2 meningar som beskriver vad användningsfallet gör

**Valfritt:**
- **Önskad visuell metafor eller ämne** - Om användaren har en viss idé om vad ikonen ska visa

Om några nödvändiga indata saknas frågar du användaren innan du fortsätter.

## Steg 2: Läs stilguiden

Läs filen `references/icon-style-guide.md` (i förhållande till den här färdighetens katalog) för att läsa in den fullständiga formatguiden, inklusive:

- Tekniska specifikationer
- Riktlinjer för visuell stil
- Exempel på visuell metafor per bransch
- Uppmaningsmallen
- Det befintliga ikonlagret

Använd stilguiden för att säkerställa enhetlighet med befintliga ikoner.

## Steg 3: Generera ikonspecifikationen

Skapa alla tre delarna av ikonspecifikationen:

### A. Filspecifikation

Ta fram filnamnet och sökvägen från ärendets namn och bransch:

- **Filnamn:** `icon-{kebab-case-name}.png`
   - Konvertera användningsfallnamnet till&quot;kebabcase&quot; (gemener, bindestreck för blanksteg)
   - Exempel: &quot;Övergiven kundvagn&quot; blir `icon-abandoned-cart.png`, &quot;Korsförsäljning&quot; blir `icon-cross-sell-upsell.png`
- **Sökväg:** `/help/blueprints/industry-use-cases/assets/use-case-icons/{industry}/`
- **Dimensioner:** 1 024 x 1 024 pixlar
- **Format:** PNG, 8-bitars RGB eller RGBA
- **Målfilstorlek:** 900 kB - 1,4 MB

### B. Fråga om bildgenerering

Skapa en detaljerad, kopieringsfärdig fråga för generering av AI-bilder. Uppmaningen måste:

1. **Beskriv en tydlig visuell metafor** - Välj en enda stark visuell metafor som omedelbart förmedlar konceptet med användningsfall. Om användaren har angett en metafor ska du använda den. I annat fall väljer du en som baseras på exempelformatguiden och fallbeskrivningen.

2. **Ange det konstnärliga formatet** - Inkludera följande formatdirektiv:
   - Ren, modern ikonillustration
   - Professionell design, estetisk
   - Fet form och rena linjer
   - Snygg, återgiven finish (ej fotorealistisk)
   - Enhetligt med ett enhetligt designsystem

3. **Inkludera tekniska specifikationer:**
   - Fyrkantigt format, 1024x1024 pixlar
   - Enstaka centrerat motiv
   - Heldragen eller subtil övertoningsbakgrund
   - Hög kontrast mellan motiv och bakgrund

4. **Använd läsbarhet i liten storlek:**
   - Ingen text eller text av något slag
   - Inga fina detaljer eller komplicerade mönster
   - Inga komplexa bakgrunder eller scener med flera element
   - Fet silhuett som är tydligt 40px
   - Stark formigenkänning även utan färg

5. **Stödja färgpaletten:**
   - Professionella, företagsanpassade färger
   - Vibrant men raffinerad (ej neon eller alltför mättad)
   - Hög kontrast för tillgänglighet
   - Cohesive with other icons in the same industry vertical

Strukturera prompten som ett enda stycke, redo att klistras in i vilket bildgenereringsverktyg som helst.

### C. Katalogreferensfragment

Generera HTML-kodutdraget som ska användas i katalogtabellen:

```
<img src="assets/use-case-icons/{industry}/icon-{name}.png" alt="{Alt Text}" width="40">
```

Där `{Alt Text}` är ett användardefinierat ärendenamn.

## Steg 4: Ange befintliga ikoner i samma bransch

Kontrollera den befintliga ikoninventeringssektionen i stilguiden och visa alla aktuella ikoner för samma bransch. Detta hjälper användaren att:
- Säkerställ visuell enhetlighet när du genererar den nya ikonen
- Undvik att duplicera en ikon som redan finns
- Referera befintliga ikoner som formatexempel

## Steg 5: Visa utdata

Formatera utdata tydligt med följande avsnitt:

---

### Ikonspecifikation: {Use Case Name}

**Bransch:** {Industry}

**Filinformation:**
- Filnamn: `icon-{kebab-case-name}.png`
- Sökväg: `/help/blueprints/industry-use-cases/assets/use-case-icons/{industry}/`
- Mått: 1 024 x 1 024 pixlar
- Format: PNG (8-bitars RGB/RGBA)

**Fråga om bildgenerering:**

> {Den fullständiga, detaljerade uppmaningen - formaterad som ett blockcitat så att det är enkelt att kopiera}

**Katalog-HTML:**

```html
<img src="assets/use-case-icons/{industry}/icon-{name}.png" alt="{Use Case Name}" width="40">
```

**Befintliga ikoner i {Industry}:**
- {list of existing icon names}

**Nästa steg:**
1. Kopiera uppmaningen om att skapa bilder ovan.
2. Klistra in den i det bildgenereringsverktyg du föredrar (Adobe Firefly, Midjourney, DALL-E eller liknande).
3. Generera bilden och välj det bästa resultatet.
4. Ändra storlek/exportera till exakt 1024x1024 pixlar vid behov.
5. Spara som `{filename}` i sökvägen ovan.
6. Kontrollera att ikonen ser tydlig och identifierbar ut vid visningsstorleken 40px.
7. Använd HTML-kodutdraget för katalogen när du lägger till det här användningsfallet i katalogtabellen.

---

## Riktlinjer

- **Generera aldrig den faktiska bilden** - Den här kompetensen ger bara specifikationen och uppmaningen. Användaren måste använda ett externt bildgenereringsverktyg.
- **En ikon per användningsfall** - Varje användningsfall får exakt en ikon.
- **Kontrollera om det finns dubbletter** - Om det redan finns en ikon med samma eller mycket liknande namn i lagret varnar du användaren.
- **Prioritera läsbarhet** - Om det finns tvivel mellan en detaljerad metafor och en enkel bör du alltid välja det enklare alternativet som är bra vid 40px.
- **Var specifik i uppmaningar** - Vag-uppmaningar ger inkonsekventa resultat. Inkludera konkreta visuella detaljer (t.ex.&quot;en varukorg med två färgglada rutor inuti&quot; istället för&quot;ett shoppingkoncept&quot;).
- **Undvik klickningar när det är möjligt** - Försök att hitta nya, men fortfarande omedelbart identifierbara, visuella metaforer. En glödlampa för varje&quot;smart&quot; användning blir repetitiv.
