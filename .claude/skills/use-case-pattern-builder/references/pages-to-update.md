---
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---
# Sidor som ska uppdateras när ett användningsmönster läggs till

När ett nytt användningsmönster skapas måste följande sidor uppdateras för att mönstret ska kunna identifieras och länkas korrekt.

## Nödvändiga uppdateringar

### 1. TOC.md
- **Fil:** `/help/blueprints/TOC.md`
- **Åtgärd:** Lägg till en ny post i rätt kategoriavsnitt
- **Format:** `    + [{{Pattern Title}}](/help/blueprints/use-case-patterns/{{category}}/{{filename}}.md)`
- **Plats per kategori:**
   - Målgruppsbyggnad och -aktivering: efter rad ~47 (efter befintliga tävlingsbidrag i det avsnittet)
   - Personalization: efter rad ~52
   - Kampanjhantering och samordning: efter rad ~58
   - Analys: efter rad ~61
   - Conversational Experience: after line ~63

#### Mappning kategori-till-innehållsförteckning

| Kategoriinstruktionsmarginal | Avsnittsrubrik för innehållsförteckning | Ankarpunkt |
| --- | --- | --- |
| `audience-building-activation` | `+ Audience Building & Activation` | `{#audience-building-activation}` |
| `personalization` | `+ Personalization` | `{#personalization-patterns}` |
| `campaign-management-orchestration` | `+ Campaign Management & Orchestration` | `{#campaign-orchestration-patterns}` |
| `analysis` | `+ Analysis` | `{#analysis-patterns}` |
| `conversational-experience` | `+ Conversational Experience` | `{#conversational-experience-patterns}` |

#### Indragningsregler

- Kategorirubriker använder två mellanslag + `+` (t.ex. `  + Personalization{#personalization-patterns}`)
- Mönsterposter använder fyra mellanslag + `+` (t.ex. `    + [Pattern Title](path)`)

### &#x200B;2. Översikt över användningsfallsmönster
- **Fil:** `/help/blueprints/use-case-patterns/overview.md`
- **Åtgärd:** Lägg till en ny rad i rätt kategoritabell
- **Format:** `| [{{Pattern Title}}]({{category}}/{{filename}}.md) | {{Primary capability description}} | [!DNL {{Solution1}}], [!DNL {{Solution2}}] |`
- **Kategorier i översikt:**
   - Målgruppsuppbyggnad och -aktivering (rad ~18)
   - Personalization (rad ~29)
   - Kampanjhantering och samordning (rad ~40)
   - Analys (rad ~52)
   - Konversationsupplevelse (rad ~61)

#### Exempel på radformat

```
| [Event-Triggered Messaging](campaign-management-orchestration/event-triggered-messaging.md) | Listen for a real-time behavioral or system event, then deliver a contextual message to the triggering profile | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
```

## Checklista för validering

- [ ] Mönstermarkeringsfil har skapats i rätt kategorikatalog
- [ ] innehåller rubrik, beskrivning, lösning och exl-id
- [ ] TOC.md-post har lagts till under rätt kategori
- [ ] Översikt.md tabellrad har lagts till under rätt kategori
- [ ] Alla affärsmålslänkar pekar på befintliga filer
- [ ]-filen använder namnkonventionen kebab-case
- [ ] Alla Experience League-länkar är giltiga URL:er
- [ ] Adobe-produktnamn använder `[!DNL ...]`-syntax
- [ ] Funktionskedjan använder ` > ` avgränsarformat
- [ ] Mönsterfilen innehåller alla nödvändiga avsnitt (se pattern-template.md)
