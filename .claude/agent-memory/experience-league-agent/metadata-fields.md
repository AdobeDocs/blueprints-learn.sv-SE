---
source-git-commit: a632042b3a7434dd88f52804e15e30fa06057e3b
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 1%

---
# Adobe Experience League - referens för godkända metadatafält

*Från Adobe ExL Authoring Guide (crawlad februari 2026) + repo analysis of blueprints-learn.en*

&#x200B;---

## Metadatahierarki

Metadataskader i den här ordningen (artikel åsidosätter innehållsförteckning, innehållsförteckning åsidosätter repo):
1. Artikel (högsta prioritet)
2. Innehållsförteckning i användarhandboken
3. metadata.md vid repo root (lägsta prioritet)

&#x200B;---

## Artikelnivåfält

### KRÄVS

| Fält | Beskrivning | Format / Begränsningar |
|-------|-------------|----------------------|
| `title` | SEO page title. Visas i sökresultat. | Max ~60 tecken; versaler; använd `[!DNL Product]` för produktnamn; duplicera INTE H1 exakt om det inte är tänkt |
| `description` | Meta description for search engines and ExL recommendations. | 150-160 tecken; idealiskt börjar du&quot;Lär dig hur...&quot; eller &quot;Läs mer om..&quot;; valideringen misslyckas om den saknas/är null |
| `exl-id` | Systemtilldelad unik identifierare. Används för innehållsspårning. | UUID-format (t.ex. `70573eb9-cd69-4fe6-b2ae-dae81665a308`); **ta bort vid kopiering av en fil** - det tilldelas automatiskt; aldrig dupliceras mellan filer |

### STARKT REKOMMENDERAD

| Fält | Beskrivning | Giltiga värden |
|-------|-------------|--------------|
| `solution` | Adobe-produkter som artikeln omfattar. Används för ExL-sökning/filtrering och innehållsrekommendationer. | Kommaavgränsad; skiftlägeskänslig; måste matcha godkänd uppräkning (se Giltiga lösningsvärden nedan) |

### VALFRITT - GEMENSAMT

| Fält | Beskrivning | Giltiga värden/anteckningar |
|-------|-------------|----------------------|
| `kt` | Äldre kunskapsbasartikel JIRA-nummer. Används för analysspårning. | Heltal (t.ex. `7207`); tomt godtagbart; `null` godtagbart |
| `thumbnail` | Miniatyrbildsreferens för rekommendationer/analyser. | Filnamnssträng eller `null` eller tom |
| `version` | Produktversionsfilter. Används främst för AEM och Campaign. | E.g. `Campaign v8`, `Campaign v8 Client Console`; måste matcha version.yml |
| `doc-type` | Innehållsklassificering som används i repo/analys. | `blueprint`, `overview-page`, `Video`, `Tutorial`, `Troubleshooting` (gemener rekommenderas) |
| `feature` | Ämnestaggar visas som&quot;Ämnen&quot; på ExL-sidor. | 1-2 per artikel; versaler; måste matcha feature.yml; kommaavgränsade |
| `feature-set` | Överordnat program för funktionsvalidering. | Måste matcha feature.yml-värden |
| `role` | Målgruppsroll. Visas som&quot;Skapad för&quot; på ExL. | `Admin`, `Architect`, `Data Architect`, `Data Engineer`, `Developer`, `Leader`, `User` |
| `level` | Användarupplevelsenivå. Visas som&quot;Skapad för&quot; på ExL. | `Beginner`, `Intermediate`, `Experienced` (versaler) |
| `topic` | Ämnen för sökning/filtrering i flera produkter. | Titelskiftläge; måste matcha topic.yml; kommaseparerad |
| `type` | Klassificering av stödlinjer. | `Documentation` (standard), `Tutorial`, `Troubleshooting` |
| `last-substantial-update` | Ytor i&quot;Nyheter&quot;-widgetar. | Format: `YYYY-MM-DD` |
| `hide` | Utesluter sidan från alla sökningar och rekommendationer. Anger även indexvärdet till nej. | `yes` eller `no` |
| `hidefromtoc` | Tar bort från innehållsförteckningens navigering, men sidan är fortfarande tillgänglig via direktlänk. | `yes` eller `no` |
| `index` | Styr om sidan ska visas i en extern sökning/platskarta. | `yes`/`no` eller `y`/`n`; standard: `no` (indexerad) |
| `recommendations` | Kontrollerar beteendet&quot;Mer hjälp om den här funktionen&quot; i widgeten. | `noDisplay` (förhindrar widgetvisning), `noCatalog` (utelämnar från rekommendationspoolen) |
| `internal` | Markerar sidan som Adobe internal-only. Förhindrar flaggning av interna länkar. | `yes` |
| `short-description` | Kondenserad beskrivning för ExL-landningssidor. Använder `description` om det utelämnas. | En mening; max ~20 ord |
| `activity` | Klassificering av sidanvändning. | `understand`, `implement`, `troubleshoot` (gemener) |
| `sub-product` | Produktdelkomponent. Samarbeta med lösningsteam för giltiga enum. | Gemener, t.ex. `search`, `assets`, `sites` |
| `team` | Teamtilldelning för analyser. | E.g. `TM` |
| `landing-page-name` | Länkar till landningssida för vägbeskrivningar. | E.g. `experience-manager` |
| `landing-page-breadcrumb-title` | Bröd text för landningssidans länk. | E.g. `AEM` |
| `auto-video-transcripts` | Aktiverar videotranskript som standard. | `true` |
| `badgeType` | Märk efter innehållsstatus. | Varierar, t.ex. `informative`, `positive` |
| `badgePremium` | Premium-märke. | Specifikation per Adobe-märke |
| `badgeLabel` | Etikettext för emblem. | Kort sträng |
| `source-git-url` | Source-databas-URL. | Fullständig GitHub-URL |
| `cloud` | Åsidosättning av molnkategori på artikelnivå. | Titelskiftläge; måste matcha cloud.yml |

&#x200B;---

## Innehållsförteckningsfält

| Fält | Beskrivning | Anteckningar |
|-------|-------------|-------|
| `user-guide-title` | Stödlinjenamn som visas i ExL-vägbeskrivningar och på landningssidor. | Krävs för innehållsförteckningsfiler |
| `breadcrumb-title` | Kortare namn på stödlinjer för vägbeskrivningar när användaren-guide-title är för lång. | Valfritt |
| `user-guide-description` | Guide summary for ExL landing page. | En mening; max ~20 ord rekommenderas |
| `product` | Analysspårning för guiden. Endast ett värde. | Måste matcha product.yml (se Giltiga produktvärden) |
| `mini-toc-levels` | Antal rubriknivåer som visas i höger-nav mini-TOC. | Heltal 1-6; standard 2 |
| `role` | Guidens standardroll. | Samma värden som artikeln `role`; kommaavgränsade |
| `index` | Om stödlinjen är indexerad. | `yes`/`no` |

&#x200B;---

## Metadata.md-fält på upprepningsnivå

| Fält | Anteckningar |
|-------|-------|
| `cloud` | Standardmolnkategori för alla artiklar i repo |
| `solution` | Standardlösning för alla artiklar |
| `product` | Standardprodukt för analysspårning |
| `type` | Standardstödlinjetyp |
| `doc-type` | Standarddokumenttyp |
| `mini-toc-levels` | Standardnivåer för miniTOC |
| `git-repo` | GitHub-repo-URL; aktiverar knapparna Redigera den här sidan och Loggproblem |
| `index` | Standardindexinställning |

&#x200B;---

## Giltiga lösningsvärden (skiftlägeskänsliga)

Gemensamma värden som används i den här rapporten:
- `Experience Platform`
- `Real-Time Customer Data Platform`
- `Journey Optimizer`
- `Journey Optimizer B2B Edition`
- `Customer Journey Analytics`
- `Campaign`
- `Campaign v8`
- `Campaign Classic v7`
- `Campaign Standard`
- `Audience Manager`
- `Target`
- `Analytics`
- `Data Collection`
- `Commerce`
- `Marketo Engage`
- `Experience Cloud`
- `Journey Orchestration`

Flera värden: kommaavgränsade, t.ex. `Real-Time Customer Data Platform, Campaign`

&#x200B;---

## Giltiga produktvärden (för fältet `product` - analysspårning)

En fullständig lista finns i systemprompten. Nyckelvärden:
- `adobe experience platform` / `experience platform` / `aem`
- `adobe analytics` / `analytics` / `aa`
- `adobe journey optimizer` / `journey optimizer` / `jo`
- `adobe customer journey analytics` / `customer journey analytics` / `cja`
- `adobe real time customer data platform` / `real time cdp` / `rtcdp`
- `adobe marketo` / `marketo` / `amk`
- `adobe campaign` / `campaign` / `ac`
- `adobe target` / `target` / `at`

&#x200B;---

## Giltiga rollvärden

- `Admin`
- `Architect`
- `Data Architect`
- `Data Engineer`
- `Developer`
- `Leader`
- `User`

&#x200B;---

## Nyckelverifieringsregler

1. Lämna aldrig `exl-id` med samma UUID i en kopierad fil - ta bort den och låt systemet tilldela en ny.
2. Tomt/null `thumbnail` och `kt` är godtagbara. Dessa är äldre fält.
3. `solution` värden måste exakt matcha den godkända uppräkningen - skiftlägeskänslig.
4. `description`-valideringen misslyckas om den saknas eller är null. Ange alltid ett meningsfullt värde.
5. Radbryt `title`-värden inom citattecken om de innehåller kolon, hakparenteser eller inledande specialtecken.
6. Flera `solution`-värden är kommaavgränsade i ett enda strängvärde.
7. `product` är endast ett värde (för analysspårning); använd inte kommaseparerade värden.
8. Om du vill begära nya uppräkningsvärden skickar du en UGP JIRA-biljett med komponenten &quot;Content Tagging&quot;.
