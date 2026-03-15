---
source-git-commit: a632042b3a7434dd88f52804e15e30fa06057e3b
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---
# Experience League Agent-minne

## Nyckelreferensfiler i den här rapporten- `/Users/nick/Library/CloudStorage/OneDrive-Adobe/Documents/GitHub/blueprints-learn.en/metadata.md` - standardvärden för metadata på postnivå- `/Users/nick/Library/CloudStorage/OneDrive-Adobe/Documents/GitHub/blueprints-learn.en/help/blueprints/TOC.md` - metadata på stödlinjenivå- `/Users/nick/Library/CloudStorage/OneDrive-Adobe/Documents/GitHub/blueprints-learn.en/.cursor/skills/blueprint-document-reference/reference.md` - mönster för utkast

## Metadataregler (se metadata-fields.md för fullständig referens)- Artikelns främre del KRÄVS: `title`, `description`, `exl-id`- Artiklar på framsidan REKOMMENDERAS STARKT: `solution`- `exl-id` måste vara ett giltigt UUID. Ta bort/lämna tomt när du kopierar filer (automatiskt tilldelat av systemet)- `description` ska börja med &quot;Lär dig hur..&quot; eller&quot;Läs mer om..&quot; enligt Adobe riktlinjer- `title` max ~60 tecken för SEO; använd `[!DNL ProductName]` för produktnamn i titeln- `solution` värden är skiftlägeskänsliga och måste matcha godkända uppräkningar (se metadata-fields.md)- `thumbnail: null` eller `thumbnail:` (tom) används båda, tom accepteras- `kt:` är ett äldre fält (JIRA-nummer för kunskapsartikel); fortfarande i den här rapporten; tomt är godkänt- Innehållsförteckningsfiler använder: `user-guide-title`, `breadcrumb-title`, `user-guide-description`, `product`, `mini-toc-levels`, `role`- `metadata.md` använder: `cloud`, `solution`, `product`, `type`, `doc-type`, `mini-toc-levels`, `git-repo`, `index`

## Common Patterns in This Repo (blueprints-learn.en)- De flesta ritningsfiler har: `title`, `description`, `solution`, `exl-id`- Vissa äldre filer innehåller också: `kt`, `thumbnail`- Vissa filer använder `version` (Campaign v8-modeller)- Översikt använder `doc-type: overview-page`- `solution` innehåller ofta flera kommaavgränsade värden: t.ex. `Real-Time Customer Data Platform, Campaign`- Filer UTAN `solution` kan fortfarande valideras om `exl-id` finns

## Adobe Markdown Extensions som används i den här rapporten- `>[!NOTE]`, `>[!TIP]`, `>[!IMPORTANT]`, `>[!WARNING]`, `>[!CAUTION]`- `>[!BEGINTABS]` / `>[!TAB Name]` / `>[!ENDTABS]` för flikinnehåll- `[!DNL ProductName]` - lokalisera inte taggar för produktnamn- `[!UICONTROL Label]` - gränssnittskontrollreferenser- `&lbrace;zoomable="yes"&rbrace;` - bildens zoomattribut- `&lbrace;width="1000"&rbrace;` - bildbreddsattribut- `&lbrace;target="_blank"&rbrace;` - externt länkmål

## Detaljerade referenser- Fullständig metadatafältreferens: `metadata-fields.md`- En crawlad redigeringsguide: https://experienceleague.adobe.com/en/docs/authoring-guide-exl/using/home (februari 2026)
