---
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 2%

---
# Använd stil på fallikon

## Översikt

Använd skiftlägesikoner fungerar som visuella identifierare i användningsfallkatalogtabellen. De måste vara omedelbart igenkännbara vid en visningsbredd på 40px samtidigt som de bibehåller sin kvalitet vid sin ursprungliga upplösning på 1 024 x 1 024.

## Tekniska specifikationer

| Egenskap | Värde |
| --- | --- |
| Mått | 1 024 x 1 024 pixlar |
| Format | PNG (8-bitars RGB eller RGBA) |
| Filstorlek | 900 kB - 1,4 MB normalt |
| Visningsstorlek | Bredd 40 px i katalogtabeller |
| Namngivning | `icon-{kebab-case-name}.png` |
| Lagringssökväg | `/help/blueprints/industry-use-cases/assets/use-case-icons/{industry}/` |

## Riktlinjer för visuell stil

### Disposition
- **Ett centralt motiv** - Varje ikon ska innehålla en tydlig visuell metafor som representerar konceptet för användningsfall
- **Centrerad komposition** - Huvudmotivet ska centreras med balanserat tomt utrymme
- **Ingen text** - texten är oläslig vid 40px. Förlita dig helt på visuell metafor
- **Inga komplexa scener** - Undvik kompositioner med flera element, bakgrunder med många objekt eller berättande scener
- **Fet silhuetter** - Ikonens form bör kunna identifieras även som en liten silhuett

### Färg och ton
- **Ren, modern palett** - Använd proffsiga, företagsanpassade färger
- **Branschsammanhållning** - ikoner inom samma bransch bör kännas som om de hör ihop
- **Hög kontrast** - Se till att huvudmotivet sticker ut tydligt från bakgrunden
- **Undvik neonfärger och för mättade färger** - Behåll paletten förfinad och professionell

### Stil
- **Modern och professionell** - rena linjer, polerad finish
- **Enhetlig återgivning** - Alla ikoner ska se ut att komma från samma designsystem
- **3D eller flat är acceptabel** - men måste vara konsekvent inom en vertikal bransch
- **Undvik fotorealism** - Illustrerad eller renderad stil ger enhetlighet
- **Inga logotyper eller varumärkesskyddade bilder** - Använd generiska visuella metaforer

### Liten Legibilitetstest
Före slutförandet: Skala bilden mentalt till 40px:
- Kan du identifiera huvudmotivet?
- Finns det tillräckligt med kontrast mellan förgrund och bakgrund?
- Finns det några fina detaljer som kan förvandlas till visuellt brus?
- Läser formen tydligt utan färg (om den är tillgänglig)?

## Exempel på visuell metafor per bransch

### Detaljhandel
| Användningsfall | Visual Metaphor |
| --- | --- |
| Övergiven kundvagn | Kundvagn med artiklar |
| Produktrekommendationer | Presentlåda eller kuraterade produkter |
| Merförsäljning | Kopplade shoppingartiklar |
| Välkomstserie | Välkomstkort eller present |
| Prisfall | Pris-tagg med nedpil |

### Bilar
| Användningsfall | Visual Metaphor |
| --- | --- |
| Tjänstpåminnelser | Tur- eller servicekalender |
| Fordonsköp | Bil med nycklar |
| Inbyte | Pilar för bilutbyte |
| Ansluten bil | Bil med digital anslutning |

### Hälso- och sjukvård
| Användningsfall | Visual Metaphor |
| --- | --- |
| Påminnelse om avtalad tid | Kalender med stetoskop |
| Läkemedelsöverensstämmelse | Vänligen flaska eller recept |
| Förebyggande vård | Sköld med hälsosymbol |

### Finansiella tjänster
| Användningsfall | Visual Metaphor |
| --- | --- |
| Lead texturering | Tillväxtsdiagram eller inredning |
| Förebyggande av könskörning | Sköld- eller kvarhållningssymbol |
| Livslängd | Tidslinje för milstolpar för liv |

### B2B
| Användningsfall | Visual Metaphor |
| --- | --- |
| ABM | Målet med byggandet |
| Betyg för lead | Mätare eller termometer |
| Förnyelse av kontrakt | Dokument med uppdateringssymbol |

### Resor och turism
| Användningsfall | Visual Metaphor |
| --- | --- |
| Cart Abandonment | Suitcase eller bokning |
| Lojalitetsprogram | Förmånskort eller stjärnmärke |
| Bokningspåminnelser | Kalender med plan/hotell |

### Försäkring
| Användningsfall | Visual Metaphor |
| --- | --- |
| Förnyelse av policy | Dokument med förnyelsepilar |
| Anspråksprocess | Urklipp med bock |
| Korsförsäljning | Anslutna principdokument |

### Media och underhållning
| Användningsfall | Visual Metaphor |
| --- | --- |
| Nytt innehåll | Uppspelningsknapp eller spotlight |
| Innehållsrekommendationer | Aktuell spelningslista eller startat innehåll |
| Prenumerationskanal | Skadat prenumerationskort |

### Telekommunikation
| Användningsfall | Visual Metaphor |
| --- | --- |
| Planoptimering | Signalstreck med växel |
| Uppgradering av enhet | Telefon med uppil |
| Förebyggande av könskörning | Sköld med signal |

## Uppmaningsmall för bildgenerering

Använd den här mallen som utgångspunkt och anpassa ämnet och informationen för varje användningsfall:

```
A clean, modern icon illustration of {visual metaphor} representing {use case concept}. Professional corporate design style with bold shapes and clean lines. Single centered subject on a {solid/gradient} background. High contrast, vibrant but refined color palette. No text, no fine details, no complex backgrounds. The icon must be clearly recognizable when scaled down to 40 pixels. Square format, 1024x1024 pixels.
```

### Tips för anpassning av fråga

- **Var tydlig med ämnet** -&quot;En ljusröd kundvagn med två färgglada presentlådor inuti&quot; är bättre än&quot;en kundvagn&quot;
- **Ange bakgrundsbehandling** -&quot;på en mjuk blå övertoningsbakgrund&quot; eller&quot;på en ren vit bakgrund med subtil skugga&quot;
- **Omnämnande av ljussättning** - &quot;mjuk studiobelysning&quot; eller &quot;mjuk omgivningsglöd&quot; ger enhetlighet
- **Lägg till formatmodifierare** -&quot;minimalist&quot;,&quot;geometric&quot;,&quot;isometric&quot; eller&quot;flat design&quot; för att styra den estetiska
- **Inkludera negativa frågor om det stöds** -&quot;ingen text, inga vattenstämplar, inga kanter, inga fotorealistiska element&quot;

## Befintligt ikonlager

### Per bransch

**Detaljhandel (9 ikoner):**
ikonövergiven varukorg, ikon-lager-trängning, ikon-pris-drop, icon-product-recommendations, icon-category-pages, icon-welcome-series, icon-refillement, icon-post-purchase, icon-cross-sell-upsell

**Automatisering (12 ikoner):**
icon-service-reminders, icon-revoss-notifications, icon-test-drive, icon-model-launch, icon-trade-in, icon-parts-components, icon-warranty, icon-connected-car, icon-dealer-network, icon-Vehicle-purchase, icon-finansiering, icon-owner-loyalty

**Finansiella tjänster (6 ikoner):**
icon-lead-plantturing, icon-account-dashboard, icon-product-recommendation, icon-churn-Prevention, icon-life-stage

**Hälsovård (4 ikoner):**
icon-avtalad tid-påminnelse, ikon-post-besök, icon-Prevention-care, icon-medicination-adherence

**Försäkring (3 ikoner):**
icon-policy-förnyelse, icon-claim-process, icon-cross-sell

**Media och underhållning (3 ikoner):**
icon-new-content, icon-content-recommendations, icon-subscription-churn

**Telekommunikation (3 ikoner):**
icon-plan-optimization, icon-device-upgrade, icon-churn-prevent

**Resor och turism (12 ikoner):**
icon-cart-abonment, icon-booking-reminders, icon-säsongsrelaterade kampanjer, icon-personalized-homepage, icon-high-intent, icon-post-booking-upsell, icon-win-back, icon-dynamic-interary, icon-recently-browsed, icon-group-booking, icon-exit-intent, icon-loyalty-program

**B2B (11 ikoner):**
icon-webinar-demo, icon-abm, icon-lead-scoring, icon-content-personalization, icon-event-registration, icon-trial-conversion, icon-customer-onboarding, icon-Competi-replace, icon-case-study, icon-contract-conversion, icon-upsell-expansion
