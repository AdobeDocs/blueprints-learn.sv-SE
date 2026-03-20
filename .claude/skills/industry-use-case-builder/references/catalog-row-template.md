---
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---
# Använd mall för ärendekatalograd

## Radformat

Varje rad i katalogen use case har följande exakta format:

```
| <img src="assets/use-case-icons/{industry}/icon-{kebab-name}.png" alt="{Alt Text}" width="40"> | [{Use Case Title}]({industry}/{industry}-overview.md#{heading-anchor}) | {One-sentence description} | [!BADGE {Maturity}]{type={Type}} | [{Pattern Name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md) |
```

### Rad utan ikon (använd när ikonen inte är tillgänglig än)

```
| | [{Use Case Title}]({industry}/{industry}-overview.md#{heading-anchor}) | {One-sentence description} | [!BADGE {Maturity}]{type={Type}} | [{Pattern Name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md) |
```

## Fältreferens

| Fält | Format | Exempel |
| --- | --- | --- |
| bransch | namn på katalogen kebab-case | detaljhandel, finansiella tjänster, resegästfrihet |
| kebabnamn | kebab-case use case name for icon | övergiven varukorg, ledande vårdsverksamhet |
| Alt-text | Versaler, kort | Övergiven kundvagn, ledande tillverkning |
| heading-anchor | kebab-case för rubriken ## i översikt | serverövergiven-kundvagn-e-poståterställning |
| Löptid + Typ | Syntax för badge | `[!BADGE Foundational]{type=Neutral}`, `[!BADGE Emerging]{type=Informative}`, `[!BADGE Advanced]{type=Caution}` |

## Flikmarkörer i branschen i katalogen

Katalogfilen använder den här flikstrukturen:

- `>[!TAB Retail]`
- `>[!TAB Automotive]`
- `>[!TAB Financial Services]`
- `>[!TAB Healthcare]`
- `>[!TAB Insurance]`
- `>[!TAB Media & Entertainment]`
- `>[!TAB Telecommunications]`
- `>[!TAB Travel & Hospitality]`
- `>[!TAB B2B]`

## Ordna på flikar

Rader ordnas efter mognadsnivå:

1. **Foundational** rader först (type=Neutral)
2. **Nya** rader, andra (typ=Informativ)
3. **Avancerat** rader sist (type=Varning)

Lägg till nya rader i slutet av gruppen inom samma mognadsnivå.
