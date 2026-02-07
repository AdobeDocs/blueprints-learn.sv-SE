---
source-git-commit: dfa21942ecf2a1db06df6f6cc945f5572811ca93
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 1%

---
# Design Document Reference - Detailed Guide

## Dokumenttyper

| Typ | Syfte | Plats / Exempel |
|------|---------|--------------------|
| **Översikt/hubb** | En produkt eller ett område introduceras; länkar till scenarioutkast | t.ex. `overview.md`, `journey-optimizer-overview.md` |
| **Scenarioplan** | Enskilt fall: arkitektur, steg, skyddsräcken | t.ex. `real-time-lookup.md`, `journey-optimizer-journeys.md` |
| **Innehåll** | Navigering; använd inte som innehållsmall | `help/blueprints/TOC.md` |

&#x200B;---

## Full Section Reference

### Titel och beskrivning (förhandsgranskning)

- **title**: Kort, specifik. Använd `[!DNL Product Name]` som produktnamn (t.ex. `[!DNL Journey Optimizer]`).
- **description**: En mening. Beskriv vad ritningen visar och resultatet (t.ex.&quot;Kundprofilåtkomst i realtid vid sidan om för webb- och mobilpersonalisering&quot;).

### Brödavsnitt

| Avsnitt | Inkludera | Innehållsvägledning |
|---------|-----------------|-------------------|
| **Program** | Alltid för scenarioritningar | Punktlista över Adobe produkter/lösningar (t.ex. Customer Data Platform i realtid, Data Collection). |
| **Användningsexempel** | Alltid | Punktlista över affärsbruk och tekniska användningsområden som den här planen stöder. |
| **Förutsättningar** | När inställning krävs | Produkter, underdomäner, SDK:er, konfiguration som måste vara på plats. Länka till Experience League för steg i installationen. |
| **Arkitekturdiagram** | Alltid | Enkelt primärdiagram (SVG rekommenderas). Använd konsekvent formatering: `style="width:90%; border:1px solid #4a4a4a" class="modal-image"`. Ange meningsfull `alt`-text. |
| **Guardrails** | Alltid när produkten har skyddsräcken | Länka till Experience League brevpapper. Lägg till gränser för utkast (t.ex. TTL, hastighetsgränser) som punkter. |
| **Implementeringsmönster** | När flera metoder finns | Namnge varje mönster (t.ex. &quot;Mönster 1: Målgruppsmedlemskap som baseras på Web SDK&quot;); använd punktlistor för när de ska användas och kompromisser. |
| **Implementeringssteg** | För scenarioutkast med en definierad bana | Numrerad lista. Varje steg: åtgärd + länk till Experience League där proceduren finns. Kopiera inte fullständiga procedurer. |
| **Implementeringsöverväganden** | När det finns viktiga kavattar | Underavsnitt (t.ex. ID-överväganden, attributbaserad personalisering). Punkter eller korta stycken; länka för djup. |
| **Relaterad dokumentation** | Alltid | Grupperade länkar till Experience League (och eventuellt developer.adobe.com). Se Experience League länkgrupper nedan. |

### Översikt/navsidor

- Börja med 1-2 stycken på produkten/området och vad ritningarna omfattar.
- **Användningsfall**: Kan använda `>[!BEGINTABS]` / `>[!TAB ...]` / `>[!ENDTABS]` för flera kategorier.
- **Arkitektur**: Ett huvuddiagram.
- **Schemautskriftsscenarier** eller **Integreringsmönster**: Tabell med scenarionamn, kort beskrivning och länk till scenarioplanen.
- **Förutsättningar**, **Guardrails**, **Relaterad dokumentation**: Samma som ovan. Var kortfattad.

&#x200B;---

## Adobe Experience League - agentanvisningar

### När ska du hänvisa till Experience League

- **Produktdokumentation**: Så här fungerar en produkt, användargränssnitt, begrepp.
- **API:er**: slutpunkter, parametrar, exempel (Experience Platform, Edge osv.).
- **Garantier**: officiella skyddsutkast för produkten eller tjänsten.
- **Självstudiekurser**: Stegvisa guider (t.ex. skapa scheman, aktivera mål).
- **Konfiguration**: Datastreams, mål, sammanslagningsprinciper, identiteter osv.

Klistra inte in långa procedurer från Experience League i ritningen. Sammanfatta och länka.

### URL-mönster

| Innehållstyp | Bas-URL | Exempel på sökväg |
|--------------|----------|--------------|
| Experience Platform docs | `https://experienceleague.adobe.com/docs/experience-platform/` | `.../profile/home.html`, `.../destinations/catalog/...` |
| Experience League (en) | `https://experienceleague.adobe.com/sv/docs/` | Samma struktur som ovan med `/en/`. |
| Journey Optimizer | `https://experienceleague.adobe.com/docs/journey-optimizer/` | `.../using/get-started/guardrails.html` |
| Web SDK | `https://experienceleague.adobe.com/docs/experience-platform/web-sdk/` | `.../home.html`, `.../commands/command-responses.html` |
| Edge Network Server-API | `https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/` | `.../overview.html`, `.../guardrails.html` |
| Mobile SDK | `https://developer.adobe.com/client-sdks/` | `.../home/`, `.../edge/adobe-journey-optimizer-decisioning/` |
| Taggar | `https://experienceleague.adobe.com/docs/experience-platform/tags/` | `.../home.html` |
| Självstudiekurser för plattformar | `https://experienceleague.adobe.com/docs/platform-learn/tutorials/` | `.../profiles/create-merge-policies.html` |

Använd den kanoniska sökvägen som matchar den aktuella Experience League-webbplatsen (använd `/en/docs/` när den engelska sökvägen är känd).

### Länka formatering i markering

- **Beskrivande länktext**: `[Create schemas](https://experienceleague.adobe.com/sv...)` inte&quot;klicka här&quot;.
- **Produktnamn i text**: Använd `[!DNL Product Name]` per Adobe-format (t.ex. `[!DNL Real-time Customer Profile]`).
- **Externa länkar**: Lägg bara till `{target="_blank"}` när mallen eller pipelinen kräver det (kontrollera befintliga utkast i svaret).

### Relaterad dokumentation - föreslagna grupper

Använd de här grupperna när de används:

1. **Målkonfigurationer** (för aktiverings-/kantanpassningsplaner)
2. **SDK-dokumentation** (Web SDK, Mobile SDK, Edge Network Server API, taggar)
3. **Profil och segmentering** (kundprofil i realtid, sammanfogningsprinciper, segmentering)
4. **Självstudiekurser** (plattformsinlärning eller produktspecifika steg-för-steg-guider)
5. **Produktdokumentation** (startsida för huvudproduktdokumentet eller viktiga underavsnitt)
6. **Guardrails** (om inte redan finns i avsnittet Guardrails)

Exempel:

```markdown
## Related documentation

### Destination configurations
* [Custom Personalization Connection](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/personalization/custom-personalization)
* [Activate audiences to edge personalization destinations](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations)

### SDK documentation
* [Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html?lang=sv-SE)
* [Edge Network Server API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=sv-SE)

### Profile and segmentation
* [Real-time Customer Profile](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=sv-SE)
* [Profile Guardrails](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=sv-SE)
```

&#x200B;---

## Repo och innehållsförteckning

- **Innehållssökväg för utkast**: `help/blueprints/` (med undermappar efter område, t.ex. `audience-activation/`, `customer-journeys/journey-optimizer/`).
- **Assets**: Samarbeta med planen (t.ex. `assets/`, `images/`) eller i en delad mapp (t.ex. `experience-platform/assets/`).
- **Innehållsförteckning**: Redigera `help/blueprints/TOC.md` när du lägger till, byter namn på eller flyttar ritningssidor. Bevara frontalformen (`user-guide-title`, `breadcrumb-title`, `user-guide-description`, `product`, `mini-toc-levels`, `role`) och hierarkin `+`.

&#x200B;---

## Exempelreferenser i den här rapporten

- **Scenarioplan (lång form)**: `help/blueprints/audience-activation/real-time-lookup.md`
- **Översikt/nav med flikar och tabeller**: `help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-overview.md`
- **Fästpaneler-fokuserade**: `help/blueprints/experience-platform/guardrails.md`
- **Navigering**: `help/blueprints/TOC.md`, `help/blueprints/overview.md`

Använd dessa som mönster för sektionordning, frontalspunkt, diagramplacering och länkanvändning i Experience League.
