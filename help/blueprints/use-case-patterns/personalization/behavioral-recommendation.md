---
title: Beteenderekommendation
description: Lär dig hur du genererar rekommendationer för objekt och innehåll med hjälp av markeringsstrategier och rankningsmodeller.
solution: Journey Optimizer, Real-Time Customer Data Platform
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '7626'
ht-degree: 0%

---


# Beteenderekommendation

Den här guiden beskriver hur du implementerar beteenderekommendationer för produkter och innehåll med hjälp av [!DNL Adobe Journey Optimizer] (AJO) Decisioning, [!DNL Real-Time Customer Data Platform] (RT-CDP) och [!DNL Adobe Experience Platform] (AEP). Det är utformat för lösningsarkitekter, marknadsföringsteknologer och implementeringstekniker som behöver kunna leverera personaliserade rekommendationsupplevelser via webben, mobilappar och e-postkanaler.

Den innehåller alla genomförbara implementeringsalternativ, beslutsöverväganden vid varje fas och länkar till [!DNL Adobe Experience League]-dokumentation. Beteenderekommendation genererar rekommendationer på objektnivå eller på innehållsnivå med hjälp av beteendesignaler - produktvyer, inköp, innehållsinteraktioner, sökfrågor - i kombination med urvalsstrategier och rangordningsmodeller för AJO Decisioning. Till skillnad från beslut om erbjudanden, som väljs ut från en välstrukturerad uppsättning marknadsföringserbjudanden med hjälp av explicita regler, fungerar det här mönstret på stora artikelkataloger (produkter, artiklar, videor) och använder beteendetillhörighetssignaler och XML-baserad rankning för att visa de mest relevanta objekten för varje besökare.

## Använd ärendeöversikt

Organisationer med produktkataloger, innehållsbibliotek eller mediebibliotek måste visa de mest relevanta objekten för varje besökare utifrån deras beteendehistorik och sessionsaktivitet. Oavsett om det är en karusell som&quot;rekommenderas för dig&quot; på en hemsida, en korsförsäljningswidget på en produktinformationssida eller produktrekommendationer som är inbäddade i en e-postkampanj är den underliggande utmaningen densamma: matcha varje besökares beteendeprofil mot de mest relevanta objekten från en katalog och leverera sedan dessa rekommendationer i rätt kanal vid rätt tillfälle.

Det här mönstret åtgärdar den utmaningen genom att inhämta beteendesignaler i realtid via [!DNL Web SDK] eller [!DNL Mobile SDK], bearbeta dem via AJO Decisioning-markeringsstrategier som kombinerar objektattribut med beteendekontext och levererar de rekommenderade objekten via webben, i appen eller via e-postkanaler. Rankningsmodeller kan vara formelbaserade (t.ex. sortera efter kategoritillhörighetspoäng) eller AI-rankade (t.ex. personaliserad rekommendationsmodell). Mönstret hanterar också kallstartsscenarier för nya besökare utan beteendehistorik genom att konfigurera reservrekommendationer.

Målgruppen för det här mönstret är bland annat e-handelsteamen, team för innehållspersonalisering och team för digitala upplevelser som vill förbättra engagemanget, konverteringen och det genomsnittliga ordervärdet genom personaliserade rekommendationer som bygger på verkliga användarbeteenden.

## Viktiga verksamhetsmål

Följande affärsmål stöds av det här användningsmönstret.

### [Öka korsförsäljning och merförsäljning](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)

Marknadsför kompletterande och premiumbaserade produkter eller tjänster till befintliga kunder baserat på beteenden och inköpshistorik.

| KPI | Beskrivning |
| --- | --- |
| Merförsäljning/korsförsäljning % | Procentandel kunder som köper rekommenderade kompletterande eller premiumartiklar |
| Inkrementell intäkt | Ytterligare intäkter som kan tillskrivas rekommendationsdrivna inköp |
| Kundens livstidsvärde | Långsiktig värdeökning från djupare produktengagemang |

### [Öka konverteringsgraden](../../business-objectives/revenue-monetization/increase-conversion-rates.md)

Förbättra andelen besökare och presumtiva som utför önskade åtgärder, t.ex. inköp, registreringar eller inskickade formulär.

| KPI | Beskrivning |
| --- | --- |
| Konverteringsgrader | Procentandel besökare som konverterar efter att ha engagerat sig i rekommendationerna |
| Leadkonvertering | Den hastighet med vilken besökare som engagerar sig i rekommendationer blir kunder |
| Kostnad per lead | Minskade anskaffningskostnader genom engagemang i organiska rekommendationer |

### [Leverera personaliserade kundupplevelser](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)

Skräddarsy innehåll, erbjudanden och budskap efter enskilda preferenser, beteenden och livscykelsteg.

| KPI | Beskrivning |
| --- | --- |
| Engagemang | Interaktionsfrekvens med rekommendationsytor (klickningar, vyer, tillägg till kundvagnen) |
| Konverteringsgrader | Ökad konverteringsgrad för besökare som engagerar sig i rekommendationer jämfört med kontroll |
| Nöjda kunder (CSAT) | Förbättrade kundnöjdheter från relevanta, personaliserade upplevelser |

## Exempel på taktiska användningsfall

Nedan följer några vanliga taktiska implementeringar av det här mönstret:

- Produktens korsförsäljningswidget på produktinformationssidan (&quot;kunder som också köpt&quot;)
- &quot;Recommended for you&quot;-karusell på hemsidan baserat på webbläsarhistorik
- Innehållsrekommendationer för mediewebbplats baserat på läsbeteende
- &quot;Nyligen visade&quot; i kombination med liknande objektwidget
- Kompletterande produktrekommendationer efter köp
- E-postproduktrekommendationer baserade på beteendetillhörighet
- Kategorispecifika rekommendationer baserade på webbläsarbeteende under session
- Sökresultat omrangordnas baserat på beteendesignaler

## Nyckeltal för prestanda

Följande nyckeltal hjälper till att mäta effekten av implementeringar av beteenderekommendationer.

| KPI | Mätningsmetod |
| --- | --- |
| Rekommendationsklickningshastighet (CTR) | Klicka på rekommenderade objekt delat med rekommendationsvisningar |
| Konverteringsgrad för rekommendation | Inköp eller önskade åtgärder från rekommendationsklickningar delat med totalt antal rekommendationsklickningar |
| Inkomster som påverkas av rekommendationer | Totala intäkter från order som innehöll minst en rekommendationsdriven produkt |
| Genomsnittligt ordervärde (AOV) Lyft | Ökning av AOV för sessioner som engagerar med rekommendationer jämfört med sessioner utan |
| Artiklar per order | Antal artiklar per order för sessioner som har engagerats av rekommendationer |
| Rekommendationstäckning | Procentandel av berättigade sidvisningar eller sessioner som har fått anpassade (ej reserv) rekommendationer |
| Fallback-frekvens vid kallstart | Procent av rekommendationsbegäranden som hanteras av reservlogik på grund av otillräcklig beteendehistorik |

## Använd skiftlägesmönster

**Beteenderekommendation**

Generera rekommendationer på objektnivå eller innehållsnivå baserade på beteendesignaler, med AJO Decisioning-markeringsstrategier och rankningsmodeller för att leverera kontextuellt innehåll.

**Funktionskedja:** Behavioral signalintag > Decisioning Strategy Evaluation > recommendation Delivery > Reporting

I avsnittet Mönsterkomposition under Implementeringsfrågor finns vägledning om hur du kombinerar mönster.

## Tillämpningar

Följande program används i det här fallmönstret.

- **[!DNL Adobe Journey Optimizer] (AJO) Beslut** - Urvalsstrategier, rangordningsmodeller, objektkataloger och beslutsprofiler som utvärderar beteendesignaler och returnerar de mest relevanta objekten för varje besökare
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** - ackumulering av beteendeprofildata, målgruppsutvärdering för rekommendationsomfattning och beräknade attribut för beteendeaffinitetsklassificering
- **[!DNL Adobe Experience Platform] (AEP)** - Inmatning av beteendehändelser via [!DNL Web SDK] och [!DNL Mobile SDK], [!DNL Edge Network] bearbetning, XDM-schemahantering för händelse- och katalogdata

## Foundationsfunktioner

Följande grundläggande funktioner måste finnas för det här användningsmönstret. För varje funktion anger statusen om den vanligtvis är obligatorisk, antas vara förkonfigurerad eller inte tillämplig.

| Foundational Function | Status | Vad måste finnas på plats | Experience League Reference |
| --- | --- | --- | --- |
| Administration och styrning | Antagen på plats | AJO-sandlåda med beslutsbehörighet aktiverat. Användarroller som tillhandahålls med tillgång till hantering av artikelkataloger, konfiguration av urvalsstrategier och kanalytadministration. | [Översikt över sandlådor](https://experienceleague.adobe.com/sv/docs/experience-platform/sandbox/home), [Översikt över åtkomstkontroll](https://experienceleague.adobe.com/sv/docs/experience-platform/access-control/home) |
| Datamodellering och förberedelse | Obligatoriskt | Upplev hur händelseschemat fångar in beteendesignaler (produktvyer, tillägg till kundvagnen, inköp, innehållsinteraktioner) med artikel-/produktidentifierare. Artikelkatalogschema (produktattribut, kategorier, bilder, priser) för rekommendationsobjektsuppsättningen. Profilschema med identitetsfält. Alla scheman har aktiverats för [!DNL Real-Time Customer Profile]. | [Systemöversikt för XDM](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/home), [Grundläggande om schemakomposition](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/schema/composition), [Skapa en datauppsättning](https://experienceleague.adobe.com/sv/docs/experience-platform/catalog/datasets/create) |
| Datakällor och samling | Obligatoriskt | Beteendeströmning i realtid via [!DNL Web SDK] eller [!DNL Mobile SDK] är avgörande - rekommendationskvaliteten beror på nya beteendesignaler. Objektkatalogdata måste importeras (batch- eller direktuppspelning). Datastölar som konfigurerats med AJO-tjänsten aktiverad för Edge-beslut. | [SDK-webböversikt](https://experienceleague.adobe.com/sv/docs/experience-platform/web-sdk/home), [SDK-översikt för mobiler](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview), [Konfigurera datastreams](https://experienceleague.adobe.com/sv/docs/experience-platform/datastreams/configure) |
| Konfiguration av identitet och profil | Obligatoriskt | Beteendesignaler måste kopplas till en identitet (känd eller anonym via ECID) för att kunna skapa beteendeprofiler. Autentiserad identitet (CRM-ID, e-post) måste konfigureras för rekommendationer för kända besökare. Lägg samman en aktiv policy i Edge för rekommendationsleverans i realtid. | [Översikt över identitetstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/home), [Översikt över sammanslagningsprinciper](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/merge-policies/overview) |
| Målgruppsdefinition och segmentering | Rekommenderad | Målgrupper kan användas för att definiera rekommendationer (t.ex. endast rekommendera premiumprodukter till premiummedlemmar) eller för filtrering. Detta är inte absolut nödvändigt om rekommendationerna endast är beteendemässiga. Krävs för e-postbaserade rekommendationer (alternativ C) för att definiera målgruppen. | [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/home), [Användargränssnittsguide för segmentbyggaren](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/ui/segment-builder) |

## Stödfunktioner

Följande funktioner förstärker det här användningsmönstret, men behövs inte för att köra kärnan.

| Stödfunktioner | Status | Varför det spelar någon roll | Experience League Reference |
| --- | --- | --- | --- |
| Skapande av beräknat/härlett attribut | Rekommenderad | Beräknade attribut som kategoritillhörighetspoäng, produktinteraktionsfrekvens, inköpsrekordtid och totala utgifter förbättrar rekommendationskvaliteten. [!DNL Customer AI] Propensitetsmätningar kan öka relevansen ytterligare genom att förutsäga sannolikheten för inköp. | [Översikt över beräknade attribut](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/computed-attributes/overview), [Översikt över AI för kunder](https://experienceleague.adobe.com/sv/docs/experience-platform/intelligent-services/customer-ai/overview) |
| Livscykelhantering för data | Rekommenderad | Data för beteendehändelser bör ha lämpliga utgångsprofiler - rekommendationsrelevansen försämras med inaktuella data. Genom att ange förfalloprinciper för datauppsättningar för beteendehändelsedatamängder kan du säkerställa aktualitet och hantera lagring. Samtycksreglerna säkerställer att beteendedata används på ett korrekt sätt. | [Datauppsättningens förfallodatum](https://experienceleague.adobe.com/sv/docs/experience-platform/data-lifecycle/ui/dataset-expiration), [Översikt över livscykelhantering för avancerade data](https://experienceleague.adobe.com/sv/docs/experience-platform/data-lifecycle/home) |
| Dataanvändningsetiketter och -tillämpning | Rekommenderad | Styrningsetiketter på beteendedata säkerställer att interaktionshistorik används korrekt för rekommendationer. Detta är särskilt viktigt när beteendedata omfattar webbläsarmönster, inköpshistorik eller intressesignaler för hälsa/finansiella produkter. | [Översikt över datastyrning](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/home), [Översikt över etiketter för dataanvändning](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/labels/overview) |
| Övervakning och observerbarhet | Rekommenderad | Leveransfördröjning, reservfrekvenser och hälsotillstånd för artikelkataloger bör övervakas. Varningar om beteendefel vid förtäring av händelser och beslutsfel hjälper till att upprätthålla rekommendationskvaliteten. | [Översikt över Insikter i observabilitet](https://experienceleague.adobe.com/sv/docs/experience-platform/observability/home), [Översikt över aviseringar](https://experienceleague.adobe.com/sv/docs/experience-platform/observability/alerts/overview) |
| Rapportering och analys | Ingår | Rekommendationsprestandarapportering ingår i Function Chain Step 4. [!DNL Customer Journey Analytics] analys av rekommendationseffektivitet, intäktseffekt och prestanda på objektnivå för olika ytor och segment ger optimeringsinsikter. | [CJA - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-overview/cja-overview), [Analysis Workspace - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/home) |

## Programfunktioner

I den här planen används följande funktioner från programfunktionskatalogen. Funktioner mappas till implementeringsfaser i stället för till numrerade steg.

### [!DNL Journey Optimizer] (AJO)

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Beslutsfattande | Inställningar för artikelkatalog och urvalsstrategi | Konfigurera artikelkataloger (beslutsobjekt), urvalsstrategier med beteendemodeller, filtreringsregler och reservrekommendationer |
| Kanalkonfiguration | Konfiguration för kanal och yta | Konfigurera leveransytor för webben (kodbaserade upplevelser), appar, innehållskort eller e-postkanaler där rekommendationer återges |
| Redigering av meddelanden | Konfiguration av innehåll och leverans | Designa rekommendationsåtergivningsmallar, objektvisningslayouter och personaliseringsuttryck för rekommenderade objekt |
| Rapportering och prestandaanalys | Rapportering och optimering | Övervaka rekommendationer, klickfrekvens, konvertering och intäktsmått genom AJO-rapporter och integrering med [!DNL Customer Journey Analytics] |

### [!DNL Real-Time CDP] (RT-CDP)

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Målgruppsutvärdering | Målgruppsomfång (alternativ C) | Utvärdera målgruppssegment som används för att definiera rekommendationer eller definiera målpopulationen för e-postrekommendationskampanjer |
| Profilberikning | Behavioral signalberikning | Förbättra profiler med beräknade attribut (kategoritillhörighetspoäng, interaktionsfrekvens) som förbättrar rekommendationsrankningen |

## Förutsättningar

Slutför följande innan du börjar implementera:

- AJO Decisioning har etablerats och aktiverats i målsandlådan
- [!DNL Web SDK] eller [!DNL Mobile SDK] distribueras och samlar in beteendehändelser med produkt-/innehållsidentifierare
- Produkt- eller innehållskatalogdata är tillgängliga för konsumtion (produktnamn, kategori, pris, bild-URL, tillgänglighet)
- Beteendehändelsescheman innehåller objekt-/produktidentifierare som länkar till katalogobjekt
- Datastream har konfigurerats med tjänsten [!DNL Adobe Journey Optimizer] aktiverad (krävs för Edge-beslut)
- Sammanslagningsprincip med `isActiveOnEdge: true` har konfigurerats (krävs för webb-/apprekommendationer i realtid)
- För e-postrekommendationer (alternativ C): e-postkanalens yta är konfigurerad och validerad
- För e-postrekommendationer (alternativ C): målgruppen definieras och utvärderas

## Implementeringsalternativ

Följande alternativ beskriver olika strategier för att implementera beteenderekommendationer. Välj det alternativ som bäst passar dina kanalbehov och tekniska begränsningar.

### Alternativ A: Realtidsrekommendationer för webben

**Passar bäst för:** Rekommendationer för produkter eller innehåll på webbsidor - korsförsäljningswidgetar för produktinformation, rekommenderad hemsida, personaliserade listor för kategorisidor och personalisering av sökresultat.

**Så här fungerar det:**

Beteendesignaler samlas in i realtid via [!DNL Web SDK] när besökare surfar på webbplatsen. Varje sidvy, produktinteraktion eller sökfråga direktuppspelas till AEP och kopplas till besökarens profil (via ECID för anonyma besökare eller autentiserad identitet för kända besökare). När en sida som innehåller en rekommendationsyta läses in, begär [!DNL Web SDK] en beslutsutvärdering från AJO via [!DNL Edge Network]. Beslutsmotorn utvärderar besökarens beteendeprofil mot urvalsstrategin, tillämpar rangordningslogik, filtrerar bort icke-berättigade objekt (som redan har köpts, ej i lager) och returnerar de rekommenderade objekten.

Rekommendationer återges på sidan med kodbaserade upplevelser eller webbkanalsytor. Återgivningen kan vara en karusell, ett rutnät, widget för ett objekt eller en anpassad layout som definieras i rekommendationsmallen. Impression- och klickningshändelser spåras automatiskt tillbaka till AEP för prestandarapportering.

**Viktiga överväganden:**

- Edge-beslut kräver att kopplingsregeln är aktiv i Edge
- Rekommendationsfördröjning beror på svarstiden [!DNL Edge Network] (under 500 ms SLA för begäranden med en omfattning)
- Anonyma besökare får rekommendationer baserade på sessionsbeteenden; kända besökare drar nytta av beteendemönster mellan sessioner
- Rivstarta besökare utan beteendehistorik som får tillbaka sina rekommendationer

**Fördelar:**

- Realtidspersonalisering baserad på sessionsbeteende
- Leverans av undersekundära rekommendationer via [!DNL Edge Network]
- Fungerar för både anonyma och kända besökare
- Automatiskt intryck och klickning
- Ingen sidomladdning krävs för nya rekommendationer

**Begränsningar:**

- Edge profilarkiv innehåller en delmängd av fullständiga profilattribut
- Komplexa rangordningsmodeller med många profilattribut kan kräva utvärdering på navsidan
- Kräver [!DNL Web SDK]-distribution med beteendehändelsespårning

**Experience League:**

- [Leverera erbjudanden med Edge Decisioning API](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [SDK - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/web-sdk/home)

### Alternativ B: Rekommendationer för mobilappar

**Passar bäst för:** Produktrekommendationer i appen, personliga innehållsflöden, aviseringsdrivna rekommendationer och mobilhandelsupplevelser.

**Så här fungerar det:**

Beteendesignaler samlas in via [!DNL Mobile SDK] när användarna interagerar med appen. Produktvyer, innehållsinteraktioner, sökningar och inköp strömmas till AEP. När en skärm som innehåller en rekommendationsyta läses in, begär [!DNL Mobile SDK] en beslutsutvärdering. Rekommendationer levereras via meddelanden i appen, innehållskort eller kodbaserade upplevelser i mobilappen.

Innehållskort är särskilt väl lämpade att användas som rekommendationer i mobilappar eftersom de finns kvar i en upplevelse som ser ut ungefär som när användaren vill. Meddelanden i appen kan användas för sammanhangsbaserade rekommendationer som utlöses av specifika beteenden (t.ex. för att visa kompletterande produkter efter att en artikel har lagts till i kundvagnen).

**Viktiga överväganden:**

- [!DNL Mobile SDK] måste konfigureras med beteendehändelsespårning för relevanta interaktioner
- Innehållskort ger en beständig rekommendationsyta, meddelanden i appen är tillfälliga
- Spårning av offlinebeteende kräver SDK-köhantering för överföring av fördröjda händelser
- Uppdateringscyklerna i App Store påverkar hur snabbt ändringar av rekommendationsrendering kan distribueras

**Fördelar:**

- Inbyggd mobilupplevelse med smidig, appintegrerad rekommendationsrendering
- Innehållskort är en beständig, läsbar rekommendationsfeed
- Meddelanden i appen aktiverar sammanhangsberoende, beteendestyrda rekommendationer
- Utnyttjar signaler på enhetsnivå (plats, appanvändningsmönster) för ökad relevans

**Begränsningar:**

- Kräver integrerings- och apputvecklingsresurser för [!DNL Mobile SDK]
- Återgivningsändringar kräver appuppdateringar (såvida inte kodbaserade upplevelser med serverdrivna layouter används)
- Offlineperioder skapar luckor i beteendesignalinsamling

**Experience League:**

- [Mobile SDK - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Konfigurera kanal för push-meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Alternativ C: Rekommendationer för e-postbeteende

**Passar bäst för:** Produktrekommendationer i e-postkampanjer - övergivna bläddringsmeddelanden med visade produktrekommendationer, korsförsäljningsmeddelanden efter köp, periodiska&quot;val för dig&quot;-sammanfattningar och e-postmeddelanden med anpassade produktförslag.

**Så här fungerar det:**

Behaviorala profildata som samlats in från tidigare sessioner informerar rekommendationsvalet vid e-postsändningstid eller återgivningstid. En målgrupp definieras för att rikta sig till rätt mottagare (t.ex. besökare som surfar men inte köpte, kunder som nyligen köpt något). En kampanj eller resa är konfigurerad att skicka ett e-postmeddelande som innehåller rekommendationer. Vid sändning utvärderar AJO Decisioning varje mottagares beteendeprofil mot urvalsstrategin och injicerar de rekommenderade objekten i e-postinnehållet.

Det här alternativet bygger på ackumulerad beteendehistorik i stället för sessionssignaler. Beräknade attribut (kategoritillhörighetsgrad, senaste produktvisningar, inköpsfrekvens) förbättrar rekommendationskvaliteten avsevärt för e-post eftersom de bearbetar beteendehistorik till profilnivåsignaler som urvalsstrategin kan utvärdera effektivt.

**Viktiga överväganden:**

- E-postrekommendationer utvärderas vid sändning, inte vid öppning - beteendeprofilläget vid tidpunkten för sändning avgör rekommendationerna
- Beräknade attribut rekommenderas starkt för att förbättra rangordningskvaliteten
- Begränsningar för e-poståtergivning (ingen JavaScript, begränsad CSS) begränsar visningsformat för rekommendationer
- Kräver en konfigurerad och validerad e-postkanal

**Fördelar:**

- Utnyttjar fullständig beteendehistorik för sessioner för djupare personalisering
- Integreras med befintliga arbetsflöden för kampanjer och resor
- Gäller för återanvändning och återvinningsscenarier där webb-/appkontaktytor inte är tillgängliga
- Kan innehålla flera rekommendationsplaceringar i ett enda e-postmeddelande

**Begränsningar:**

- Rekommendationer är statiska vid sändning - de uppdateras inte när e-postmeddelandet öppnas
- Begränsningar för e-poståtergivning begränsar visningsformat för rekommendationer
- Kräver utvärdering av målgruppen och infrastruktur för samordning av kampanjer och resor
- Komplexa implementeringar på grund av ytterligare beroenden (kanalkonfiguration, målgruppsdefinition, kampanjkörning)

**Experience League:**

- [Skapa ett e-postmeddelande](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/channels/email/create-email)
- [Leverera erbjudanden i meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### Jämförelse av alternativ

I följande tabell sammanfattas de viktigaste skillnaderna mellan implementeringsalternativen.

| Kriterier | Alternativ A: Webbrealtid | Alternativ B: Mobilapp | Alternativ C: E-postbeteende |
| --- | --- | --- | --- |
| Bäst för | Rekommendationer för webbsidor (PDP, hemsida, kategori) | Rekommendationer och innehållsflöden i appen | E-postkampanjer med produktrekommendationer |
| Beteendesignalkälla | In-session + korssession ([!DNL Web SDK]) | Interaktioner i appen ([!DNL Mobile SDK]) | Ackumulerad beteendehistorik (profil) |
| Rekommendationsfördröjning | Undersekund ([!DNL Edge Network]) | Undersekund ([!DNL Edge Network]) | Vid sändning (utvärdering på navsidan) |
| Typ av besökare | Anonym och känd | Kända (appanvändare) | Kända (e-postmottagare) |
| Komplex | Medelsvåra: | Medium-High | Högt |
| Kanalberoende | [!DNL Web SDK], kodbaserad upplevelseyta | [!DNL Mobile SDK], yta på innehållskort i appen/i appen | E-postkanalens yta, målgrupp, kampanj/resa |
| Kräver | [!DNL Web SDK]-distribution, Edge kopplingsprofil | [!DNL Mobile SDK]-distribution, Edge kopplingsprofil | E-postyta, målgruppsdefinition, kampanjinställning |

### Välj rätt alternativ

Använd följande vägledning för att välja det bästa alternativet för din situation:

- **Börja med alternativ A** om ditt primära mål är produktrekommendationer i realtid på din webbplats. Detta är den vanligaste utgångspunkten och ger omedelbart värde med den lägsta komplexiteten i implementeringen.
- **Välj alternativ B** om din mobilapp är en primär engagemangskanal och rekommendationer i appen skulle leda till meningsfull konverteringshöjning. Alternativ B kan köras parallellt med alternativ A med samma urvalsstrategier och artikelkataloger.
- **Lägg till alternativ C** när du vill utöka beteenderekommendationer till e-postkampanjer. Detta ligger vanligen i lager ovanpå alternativ A eller B, med samma objektkataloger och urvalsstrategier, men med e-postspecifika återgivningsmallar och målgruppsbaserad målinriktning.
- **Kombinera alternativ A + C** för ett gemensamt mönster: webrekommendationer i realtid för aktiva besökare, plus övergivna e-postrekommendationer för bläddring eller efter köp för besökare som inte konverterar.

## Implementeringsfaser

I följande faser får du hjälp med att implementera beteenderekommendationer från början till slut.

### Fas 1: Konfigurera beteendehändelseschema och datainsamling

**Programfunktion:** AEP: Datamodellering och förberedelse (F2), AEP: Datakällor och samling (F3)

I den här fasen fastställs XDM-scheman, datamängder och datainsamlingsmekanismer som samlar in beteendesignaler och artikelkatalogdata. Den här datamängden är vad all rekommendationslogik bygger på.

#### Beslut: Design av beteendestyrt händelseschema

Vilka beteendesignaler ska leda till rekommendationer?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Endast produktvyer | Enkla rekommendationer för korsförsäljning/merförsäljning | Lägsta implementeringsinsats, begränsat signaldjup |
| Produktvisningar + inköp | Rekommendationer med undantag för inköp och korsförsäljningslogik | Måttlig insats; möjliggör filtrering av Exkludera redan köpt |
| Full beteendeserie (vyer, inköp, tillägg i varukorgen, sökningar, innehållsinteraktioner) | Avancerade rekommendationer med flersignalsrankning | Högsta signalkvalitet; kräver omfattande [!DNL Web SDK]/[!DNL Mobile SDK]-instrumentering |

#### Beslut: Inmatningsmetod för artikelkatalog

Hur kommer produkten eller innehållskatalogen att importeras till AEP?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Batchförbrukning via källanslutning | Kataloguppdateringar är periodiska (varje dag/vecka) | Enklare konfiguration - katalogändringarna återspeglas inte i realtid |
| Direktinmatning | Katalogen kräver nästan realtidsuppdateringar (prisändringar, tillgänglighet) | Mer komplicerad - ger rekommendationer som återspeglar aktuellt lager |
| Manuell överföring/API-överföring | Liten katalog med ovanliga ändringar | Enklast konfiguration, inte skalbar för stora eller dynamiska kataloger |

**Gränssnittsnavigering:** Datahantering > Scheman > Skapa schema; Datasamling > Datastreams > Ny datastream

**Information om nyckelkonfiguration:**

- Experience Event-schemat måste innehålla produkt-/artikelidentifierare (SKU, produkt-ID, innehålls-ID) i händelsens nyttolast
- Artikelkatalogschemat ska innehålla attribut för filtrering och rankning: kategori, pris, bild-URL, tillgänglighetsstatus, taggar
- Tjänsten [!DNL Adobe Journey Optimizer] måste vara aktiverad för Edge-beslut
- [!DNL Web SDK] `sendEvent` anrop måste innehålla produktinteraktionsdata mappade till XDM-e-handelsfält

**Experience League-dokumentation:**

- [XDM - systemöversikt](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/home)
- [Grundläggande om schemakomposition](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/schema/composition)
- [SDK - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/web-sdk/home)
- [Konfigurera datastreams](https://experienceleague.adobe.com/sv/docs/experience-platform/datastreams/configure)
- [Definiera en relation mellan två scheman](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/tutorials/relationship-api)

### Fas 2: Konfigurera identitet och profil

**Programfunktion:** AEP: Identity &amp; Profile Configuration (F4)

I den här fasen anges identitetsnamnutrymmen, primära identitetsbeteckningar och sammanfogningsprinciper som säkerställer att beteendesignaler kopplas korrekt till besökarprofiler och är tillgängliga för rekommendationsleverans i realtid.

#### Beslut: Sammanslagningspolicy för Edge-beslut

Kräver rekommendationens exempel Edge utvärdering i realtid?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Aktiv på Edge kopplingsprofil | Alternativ A och B (webb- och mobilrealtidsrekommendationer) | Krävs för undersekundsleverans av rekommendation; endast en Edge-sammanslagningsprincip per sandlåda |
| Standardprincip för sammanslagning (inte på Edge) | Endast alternativ C (e-postrekommendationer utvärderas vid sändning) | Tillräckligt för utvärdering på navsidan; använder inte Edge-sammanslagningspolicyplats |

#### Beslut: Anonym kontra känd besöksidentitet

Hur ska beteendesignaler från anonyma besökare hanteras?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Endast ECID (anonym) | Rekommendationer främst för anonyma besökare baserade på sessionsbeteenden | Enklare installation; ingen kontinuitet mellan sessionerna såvida inte besökaren autentiserar |
| ECID + autentiserad identitet (CRM-ID, e-post) | Sessionsrekommendationer för kända besökare med identitetssammanfogning | Mer beteendeprofiler; kräver autentiseringsflöde |
| Båda med länkning av identitetsdiagram | Fullständig anonym till känd resa med identitetssammanfogning | Mest omfattande; kräver konfigurering av regler för identitetslänkning |

**Gränssnittsnavigering:** Identiteter > Identitetsnamnutrymmen; Profiler > Sammanfoga profiler

**Information om nyckelkonfiguration:**

- ECID-namnområdet är förkonfigurerat och används automatiskt av [!DNL Web SDK] och [!DNL Mobile SDK]
- Anpassade identitetsnamnutrymmen (CRM-ID, lojalitets-ID) måste skapas för autentiserad identitet
- Primär identitet i Experience Event-schemat ska vara ECID för webb-/mobilbeteendehändelser
- Sammanslagningsprincipen måste använda privat enhetsdiagram för identitetssammanfogning mellan enheter

**Experience League-dokumentation:**

- [Översikt över identitetstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/home)
- [Översikt över namnutrymmen för identiteter](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/features/namespaces)
- [Översikt över kopplingsprofiler](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/merge-policies/overview)
- [Länkningsregler för identitetsdiagram](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/features/identity-linking-logic)

### Fas 3: Ställ in artikelkatalog och urvalsstrategi

**Programfunktion:** AJO: Bestämning

I den här fasen konfigureras objektkatalogen (beslutsobjekt), urvalsstrategier som kombinerar beteendesignaler med objektattribut för rankning, filtreringsregler för att exkludera icke-berättigade objekt och reservrekommendationer för kallstartsprofiler.

#### Beslut: Artikelkatalogområde

Vilka artiklar finns tillgängliga för rekommendation?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Produktkatalog (e-handel) | Rekommendera fysiska eller digitala produkter att köpa | Artikelattribut inkluderar pris, kategori, tillgänglighet, bilder |
| Innehållskatalog (media/publishing) | Rekommendera artiklar, videor eller utbildningsmaterial | Objektattribut inkluderar ämne, författare, publiceringsdatum, innehållstyp |
| Hybridkatalog | Rekommendera både produkter och innehåll | Kräver att båda typerna har ett enhetligt objektschema |

#### Beslut: rangordningsmetod

Hur ska kvalificerade artiklar rangordnas för att fastställa de bästa rekommendationerna?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Formelbaserad rankning | Rensa affärslogik för rankning (t.ex. sortera efter kategoritillhörighetsmoment multiplicerat med artikelpopularitet) | Genomskinlig, ändringsbar rankning; kräver en definierad rankningsformel |
| AI-rankad (automatisk optimering) | Maskinininlärning bör fastställa optimal rankning baserat på konverteringsdata | Kräver minst 1 000 konverteringshändelser för modellutbildning; mindre genomskinlig |
| Prioritetsbaserad (manuell) | Enkel, manuellt strukturerad rekommendationsbeställning | Enklast att konfigurera; anpassar sig inte till individuella beteenden |

#### Beslut: Filtreringsregler

Vilka objekt ska uteslutas från rekommendationerna?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Exkludera redan köpta artiklar | Korsförsäljning och identifieringsrekommendationer | Kräver inköpshistorik i beteendeprofil |
| Exkludera ej lagerförda artiklar | E-handel med dynamiskt lager | Kräver kataloguppdateringar i realtid eller nästan i realtid |
| Uteslut tidigare ignorerade objekt | Innehållsrekommendationer där användare kan stänga förslag | Kräver spårning av uppsägning vid beteendehändelser |
| Filtrering inom kategori | Rekommendationer som är begränsade till särskilda kategorier | Använder objektattribut för filtrering |

#### Beslut: Strategi för kallstart

Vad ska visas för nya besökare utan beteendebakgrund?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Populära objekt (globala bestsellers) | Allmän reserv | Enkel att underhålla, inte personaliserad |
| Kategorispecifika populära objekt | Besökaren har kommit till en kategorisida | Sammanhangsberoende reserv; kräver sidsammanhang |
| Valda redaktionella val | Varumärket vill ha redaktionell kontroll över upplevelsen vid kallstart | Kräver manuell kurering och uppdateringar |
| Trendartiklar (tidsviktad popularitet) | Dynamisk återgång som speglar aktuella trender | Kräver beräkning av trendsignal |

**Gränssnittsnavigering:** [!DNL Journey Optimizer] > Komponenter > Beslutshantering > Beslut; [!DNL Journey Optimizer] > Komponenter > Beslutshantering > Erbjudanden; [!DNL Journey Optimizer] > Komponenter > Beslutshantering > Placeringar

**Information om nyckelkonfiguration:**

- Skapa beslutsobjekt som representerar varje produkt eller innehållsobjekt i katalogen, med attribut (kategori, pris, bild-URL, taggar)
- Definiera urvalsstrategier som kombinerar objektkatalogfiltrering med beteendelogik
- Konfigurera rangordningsmodeller - formelbaserade uttryck kan referera till profilattribut (t.ex. kategoritillhörighetspoäng från beräknade attribut)
- Skapa reserverbjudanden/artiklar som fungerar som standardrekommendationer för kallstartsprofiler
- Ordna objekten i samlingar med hjälp av samlingskvalificerare (taggar) för logisk gruppering
- Ställ in filtreringsregler i urvalsstrategier för att tillämpa affärsregler (exkludera inköpt, endast inköpt)

**Experience League-dokumentation:**

- [Beslutsledning - översikt](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Skapa placeringar](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Skapa beslutsregler](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Skapa personaliserade erbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Skapa reserverbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Skapa samlingar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Skapa beslut](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Rankningsstrategier](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Fas 4: Konfigurera kanal och yta

**Programfunktion:** AJO: Kanalkonfiguration

Den här fasen konfigurerar de leveransytor där rekommendationer ska återges. Konfigurationen varierar avsevärt beroende på implementeringsalternativ.

#### Beslut: Typ av leveransyta

Var kommer rekommendationer att visas?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Kodbaserad upplevelse (webb) | Rekommendationswidget på webbsidor med anpassad återgivning | Maximal flexibilitet för återgivning; kräver framtagning |
| Webbkanalsyta | Standardyta för webbpersonalisering | Använder AJO webbdesigner; mindre flexibelt än kodbaserad |
| Meddelande i appen | Sammanhangsberoende rekommendationer som utlöses av appbeteende | Epidemiologi; försvinner efter interaktion eller avskedande |
| Innehållskort (mobilt) | Beständig rekommendationsfeed i mobilapp | Bevaras tills användaren agerar; användarvänligt flöde |
| E-post | Produktrekommendationer är inbäddade i e-postkampanjer | Statisk vid sändning; reservation för återgivningsbegränsningar via e-post |

**Var alternativen skiljer sig:**

**För alternativ A (Web Real-Time Recommendations):**
Konfigurera en kodbaserad upplevelseyta eller webbkanalsyta. Kodbaserade upplevelser ger den flexibilitet som krävs för anpassad rekommendationsåtergivning (karuseller, rutnät, artikelkort). Yt-URI:n identifierar var på sidan rekommendationerna visas.

**För alternativ B (mobilappsrekommendationer):**
Konfigurera ytor för meddelanden eller innehållskort i appen. Innehållskort rekommenderas för beständiga rekommendationsflöden. Meddelanden i appen fungerar bra för sammanhangsbaserade, beteendestyrda rekommendationer.

**För alternativ C (E-postbeteenderekommendationer):**
Konfigurera en e-postkanal med underdomänsdelegering, IP-pooltilldelning och avsändarinställningar. Kontrollera att ytan är godkänd för leverans.

**Gränssnittsnavigering:** Administration > Kanaler > Kanalytor > Skapa yta

**Experience League-dokumentation:**

- [Konfigurera kanalytor](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Kom igång med e-postkonfiguration](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Konfigurera SMS-kanal](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Konfigurera kanal för push-meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Fas 5: Konfigurera innehåll och leverans

**Programfunktion:** AJO: Meddelanderedigering

Den här fasen definierar rekommendationsåtergivningsmallarna som styr hur rekommenderade objekt visas för besökaren. Detta inkluderar layoutdesign av objekt, anpassningsuttryck som drar in objektattribut (namn, bild, pris, länk) och den övergripande utformningen av rekommendationsupplevelsen.

#### Beslut: Rekommendationens visningsformat

Hur ska rekommenderade objekt återges?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Carousel (vågrät rullning) | Hemsida eller kategorisida med begränsat vertikalt utrymme | Välbekant UX-mönster; visar flera objekt i kompakt utrymme |
| Stödraster (flera rader) | Dedikerat rekommendationsavsnitt med gott om utrymme | Visar fler objekt samtidigt. Fungerar bra för avsnitt som&quot;rekommenderas för dig&quot; |
| Widget för enstaka objekt | Sammanhangsberoende rekommendation på en specifik sidplats (t.ex. sidospalt) | Minimalt fotavtryck, högeffektsplacering |
| Textbundet e-postblock | Rekommendationer som är inbäddade i e-postbrödtexten | Reservation för HTML/CSS-begränsningar via e-post; vanligtvis 2-4 objekt |

#### Beslut: Antal rekommendationer som ska visas

Hur många artiklar ska beslutet returnera per placering?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| 3-4 objekt | Standardrekommendationswidget | Balanserar relevans med visuell densitet |
| 6-8 objekt | Carousel med rullning eller stödrasterlayout | Fler alternativ för besökaren; kräver tillräckligt katalogdjup |
| 1 objekt | Sammanhangsbaserad rekommendation för en produkt | Största relevanseffekt; enklaste återgivning |
| 10+ objekt | Feed-liknande rekommendationer | Användningsexempel (media, publicering) |

**Var alternativen skiljer sig:**

**För alternativ A (Web Real-Time Recommendations):**
Designa rekommendationsrenderingen med kodbaserade upplevelsemallar. Använd HTML/CSS/JavaScript för att skapa karusellen, rutnätet eller widgetlayouten. Personalization-uttryck refererar till beslutssvarsattributen (objektnamn, bild-URL, pris, produkt-URL). Impression och klickspårning hanteras automatiskt av [!DNL Web SDK].

**För alternativ B (mobilappsrekommendationer):**
Konfigurera innehållskortsmallar eller meddelandemallar i appen med artikelvisningslogik. Använd JSON-baserade innehållsstrukturer som mobilappen återger internt. Inkludera djuplänkar för varje rekommenderat objekt.

**För alternativ C (E-postbeteenderekommendationer):**
Designa e-postinnehåll med e-post-Designer. Infoga rekommendationsplaceringar med beslutsstyrda innehållsblock. Konfigurera anpassningsuttryck för objektattribut i e-postmallen. Personalisering av ämnesrader kan referera till de vanligaste rekommenderade objekten.

**Gränssnittsnavigering:** Innehållshantering > Innehållsmallar; Campaign/Journey > Redigera innehåll > E-posta Designer

**Information om nyckelkonfiguration:**

- Varje rekommendationsplacering måste hänvisa till det beslut som skapats i fas 3
- Personalization-uttryck använder Handlebars-syntax för att återge objektattribut
- För webben: konfigurera den kodbaserade upplevelsen så att den anropar beslutet och återger svaret
- För e-post: bädda in beslutet i e-poståtgärden i kampanjen eller resan
- Förhandsgranska rekommendationer med testprofiler med känd beteendehistorik

**Experience League-dokumentation:**

- [Designa e-postinnehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Lägg till personalisering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization syntax](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Dynamiskt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Leverera erbjudanden i meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Förhandsgranska och testa ditt innehåll](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [Arbeta med innehållsmallar](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/content-management/content-templates/content-templates)

### Fas 6: Ställa in målgruppsomfattning och kampanj/resa (endast alternativ C)

**Programfunktion:** RT-CDP: Målgruppsutvärdering, AJO: Kampanjkörning eller Journey Orchestration

För e-postbaserade rekommendationer (alternativ C) definierar den här fasen målgruppen och konfigurerar den kampanj eller resa som levererar rekommendationsmeddelandet. Alternativen A och B hoppar över den här fasen eftersom rekommendationer levereras i realtid vid sidinläsning/skärminläsning.

#### Beslut: Metod för utvärdering av målgrupper

Hur ska målgruppen för rekommendationsmeddelanden utvärderas?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Batchutvärdering | E-postkampanjer med schemalagda rekommendationer (daglig, veckovis sammanfattning) | Förutsägbar sändningstid; målgruppen utvärderades före sändning |
| Utvärdering av strömning | E-postmeddelanden om händelseutlösta rekommendationer (övergiven surfning, efter köp) | Publiken är nära realtid; par med resesamordning |

#### Beslut: Leveransmekanism

Ska e-postmeddelandet levereras via en kampanj eller en resa?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Schemalagd kampanj | E-postmeddelanden med enstaka eller återkommande rekommendationer till en viss målgrupp | Enklare konfiguration; utvärdering och sändning av batchmålgrupper |
| Resa med målgruppsinlägg | Pågående rekommendationer via e-post som triggas av målgruppskvalifikation | Aktiverar flerstegsflöden (t.ex. e-postrekommendation följt av påminnelse) |
| Händelseutlöst resa | Rekommendationsmeddelande som utlöses av en viss händelse (bläddringsavhopp, köp) | Realtidsutlösande; kräver händelsebaserad reseregistrering |

**Gränssnittsnavigering:** Kund > Publiker > Skapa målgrupp > Skapa regel; Kampanjer > Skapa kampanj; Resor > Skapa resa

**Information om nyckelkonfiguration:**

- Definiera målgruppen med segmentregeluttryck som refererar till beteendehistorik (t.ex.&quot;visade produkter under de senaste 7 dagarna men inte köpt&quot;)
- Konfigurera kampanjen eller resan med e-poståtgärden som refererar till kanalytan från fas 4
- Bädda in beslutet från fas 3 i e-postinnehållet
- Ange schemaläggnings- och frekvensregler för att undvika övermeddelanden

**Experience League-dokumentation:**

- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/ui/segment-builder)
- [Direktuppspelningssegmentering](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Kampanjrapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)

### Fas 7: Konfigurera rapportering och optimering

**Programfunktion:** AJO: Rapportering och prestandaanalys, CS5: Rapportering och analys

I den här fasen fastställs prestandaövervakning för rekommendationer klickfrekvens, konvertering och intäktsmått. Den skapar en rapportinfrastruktur för att mäta rekommendationseffektivitet och identifiera optimeringsmöjligheter.

#### Beslut: Rapporteringsdjup

Vilken nivå av rapportanalys krävs?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Endast inbyggda AJO-rapporter | Prestandaövervakning för grundläggande rekommendationer | Snabbredigering; begränsat till AJO-spårade mätvärden |
| Integrering med AJO + [!DNL Customer Journey Analytics] | Effektanalys av flerkanalsrekommendationer och intäktsattribuering | Kräver [!DNL Customer Journey Analytics] anslutning och datavy; ger djupare insikter |
| Fullständig [!DNL Customer Journey Analytics]-arbetsyta med anpassade instrumentpaneler | Pågående optimeringsprogram med analys på objektnivå, segmentnivå och ytnivå | Mest omfattande; kräver [!DNL Customer Journey Analytics] expertis och konfiguration |

**Gränssnittsnavigering:** Kampanjer > Välj kampanj > Alla tidsrapporter; Resurser > Välj resa > Alla tidsrapporter; [!DNL Customer Journey Analytics] > Projekt > Skapa nytt projekt

**Information om nyckelkonfiguration:**

- Granska AJO kampanjrapporter och reserapporter för leverans- och engagemangsmått
- För integrering med [!DNL Customer Journey Analytics] skapar du en anslutning med händelsedatamängder för AJO-upplevelser (meddelandefeedback, e-postspårning, beslutsfattande)
- Skapa en [!DNL Customer Journey Analytics]-datavy med rekommendationsspecifika dimensioner (artikelnamn, artikelkategori, rekommendationsyta) och mått (visningar, klick, konverteringar, intäkter)
- Skapa beräknade värden för rekommendation CTR, konverteringsgrad och intäkt per intryck
- Skapa [!DNL Customer Journey Analytics] arbetsytepaneler som jämför rekommendationsprestanda för ytor, segment och tidsperioder

**Experience League-dokumentation:**

- [Global kampanjrapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Global reserapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Arbeta med Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Skapa eller redigera en anslutning](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-connections/create-connection)
- [Skapa eller redigera en datavy](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Analysis Workspace - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/home)
- [Översikt över beräknade mätvärden](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)

## Implementeringsöverväganden

Granska följande utkast, fallgropar, bästa praxis och kompromisser före och under implementeringen.

### Gardrutor och begränsningar

- Högst 10 000 godkända anpassade erbjudanden (beslutsobjekt) per sandlåda - [Beslutsfattare](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/get-started/guardrails)
- Högst 30 praktik per beslut
- Maximalt 30 samlingsomfång per beslutsbegäran
- Erbjud leveranssvarstid SLA: mindre än 500 ms vid P95 för Edge-förfrågningar med en enda omfattning
- AI-rankningsmodeller kräver minst 1 000 konverteringshändelser för utbildning
- Räknare för buffertbegränsning kan ha en fördröjning på upp till några sekunder i högflödesscenarier
- Edge beslut är begränsade till profilattribut som är tillgängliga i edge-profilarkivet
- Endast en sammanslagningsprincip kan vara aktiv på Edge per sandlåda: [Profilskyddsutkast](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/guardrails)
- Högst 25 aktiva beräknade attribut per sandlåda - [Beräknade attributskyddsräcken](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/computed-attributes/overview)
- Maximalt 4 000 segmentdefinitioner per sandlåda - [Segmenteringsskyddsräcken](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/guardrails)
- Direktuppspelningsinmatning: högst 20 000 poster per sekund per HTTP-anslutning — [Inmatningsskydd](https://experienceleague.adobe.com/sv/docs/experience-platform/ingestion/guardrails)

### Vanliga fallgropar

- **Beslutet returnerar endast reservobjekt:** Kontrollera att anpassade beslutsobjekt har godkänts, inom giltighetsdatumintervallet och att berättigandereglerna matchar besökarens profilattribut. Kontrollera att begränsningen inte har nåtts.
- **Edge-leverans returnerar tom personalisering:** Kontrollera att datastream har konfigurerats med tjänsten [!DNL Adobe Journey Optimizer] aktiverad och att beslutsomfånget är korrekt formaterat i [!DNL Web SDK]-begäran.
- **Rankningsformeln används inte:** Kontrollera att formeln är syntaktiskt giltig och refererar till tillgängliga profilattribut. Formelfel återgår i tysthet till prioritetsbaserad rankning.
- **Gamla rekommendationer:** Om beteendehändelsedata inte flödar i realtid kommer rekommendationerna att baseras på föråldrade beteendeprofiler. Verifiera att [!DNL Web SDK] eller [!DNL Mobile SDK] aktivt direktuppspelar händelser.
- **Återgångsfrekvensen för kallstart är för hög:** Om en stor andel av besökarna får återgångsrekommendationer bör du överväga att initiera kallstartsstrategin med sammanhangsberoende signaler (aktuell sidkategori, hänvisningskälla) i stället för att enbart förlita dig på beteendehistorik.
- **Rekommendationer som inte återges på sidan:** Kontrollera att den kodbaserade URI:n för upplevelseyta matchar sidans URL-mönster och att [!DNL Web SDK] begär och återger beslutssvaret korrekt.
- **Katalogobjekt saknas i rekommendationer:** Kontrollera att alla katalogobjekt har importerats som beslutsobjekt, taggats med rätt samlingskvalificerare och inkluderats i rätt samlingar som markeringsstrategin refererar till.

### God praxis

- Börja med en formelbaserad rankningsmodell som använder beräknade attribut (kategoritillhörighet, interaktionsnyhet) innan du investerar i AI-rankade modeller. Formbaserade modeller är genomskinliga, ändringsbara och ger en solid baslinje för jämförelse.
- Gör intryck och klicka på spärra/knip från dag ett. Utan interaktionsdata kan AI-rankningsmodeller inte träna och du kan inte mäta rekommendationens effektivitet.
- Skapa separata urvalsstrategier för olika rekommendationsytor (hemsida, PDP, e-post) i stället för att återanvända en enda strategi överallt. Olika ytor har olika användaravsikter.
- Använd beräknade attribut för att bearbeta beteendehistorik till rankningssignaler. Raw-händelsedata är för detaljerade för effektiv formelbaserad rankning; aggregerade signaler som&quot;kategoritillhörighetspoäng&quot; och&quot;dagar sedan senaste köp&quot; är mer effektiva.
- Testa reservrekommendationer separat från personaliserade rekommendationer. Se till att reservdelar är varumärkesanpassade standardinställningar av hög kvalitet som ger en bra upplevelse för nya besökare.
- Övervaka återfallsfrekvensen vid kallstart som ett viktigt hälsomått. En minskande fallfrekvens över tiden tyder på ökad beteendetäckning.
- För e-postrekommendationer skickas schemat när beteendeprofilen är mest komplett (t.ex. efter de bästa surftimmarna, inte under dem).

### Avvecklingsbeslut

Följande kompromisser bör utvärderas utifrån dina specifika behov.

#### Realtidssignaler jämfört med ackumulerad historik

Beteendesignaler under session ger omedelbar relevans men begränsat djup. Ackumulerad beteendehistorik ger djup men kan vara inaktuell. Balansen mellan dessa källor påverkar rekommendationskvaliteten.

- **Alternativ A prioriterar:** Realtidssignaler för omedelbar relevans, kompletterat med historik för kända besökare
- **Alternativ C prioriterar:** Endast ackumulerad historik, eftersom e-postmeddelanden skickas asynkront
- **Rekommendation:** För webb och mobiler (Alternativ A, B) kombinerar sessionssignaler med beräknade attribut som härletts från historiskt beteende. För e-post (alternativ C) investerar du mycket i beräknade attribut som sammanfattar beteendehistorik i användbara profilnivåsignaler.

#### Formelbaserade eller AI-rankade modeller

Formelbaserad rankning är transparent och omedelbar. AI-rankade modeller anpassar sig automatiskt men kräver utbildningsdata och ger mindre insyn i rangordningsbesluten.

- **Formelbaserade fördelar:** Genomskinlighet, hörbarhet, omedelbar driftsättning och detaljerad affärskontroll över rankningslogik
- **AI-rankade favoriter:** Automatiserad optimering, identifiering av icke-uppenbara mönster och reducerad manuell justeringsinsats
- **Rekommendation:** Börja med formelbaserad rankning för att etablera en resultatbaslinje och samla in konverteringsdata. Gå över till AI-rankade modeller när du har tillräckligt med utbildningsdata (över 1 000 konverteringshändelser) och vill optimera bortom vad manuell formeljustering kan göra.

#### Rekommendationstäckning kontra relevans

Om du breddar artikelkatalogen och avspänningsfilterreglerna ökar procentandelen förfrågningar som får personaliserade rekommendationer, men det kan minska relevansen per rekommendation.

- **Hög täckning prioriterar:** Maximera antalet besökare som ser personaliserade rekommendationer, användbart när det primära målet är engagemang
- **Hög relevans:** Visar endast mycket relevanta objekt, även om det innebär att fler besökare ser reservrekommendationer. Användbart när det primära målet är konvertering
- **Rekommendation:** Starta med måttlig filtrering (exkludera köpta artiklar, ej lagerförda artiklar) och övervaka både reservfrekvensen och konverteringsgraden. Förbättra filtreringsreglerna endast om konverteringsdata har stöd för det.

#### Personalization djupdesign jämfört med implementeringskomplexitet

Mer omfattande beteendesignaler och mer sofistikerade rankningsmodeller förbättrar rekommendationskvaliteten men ökar komplexiteten i implementeringen och belastningen på underhållet.

- **Förenklad implementering prioriterar:** Snabbare värdeskapande, lägre underhållsbehov, enklare felsökning och upprepning
- **Djupare personalisering prioriterar:** Högre konverteringshöjning, bättre kundupplevelse, konkurrensdifferentiering
- **Rekommendation:** Implementera i faser. Börja med produktvysignaler och receptbaserad rankning (fas 1). Lägg till beräknade attribut för beteendeberikning (fas 2). Utvärdera AI-rankade modeller när grunden är mogen och det finns tillräckligt med utbildningsdata (fas 3).

## Relaterad dokumentation

Följande resurser innehåller ytterligare information om de tekniker och funktioner som används i det här mönstret.

### Beslutsledning

- [Beslutsledning - översikt](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Skapa placeringar](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Skapa beslutsregler](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Skapa personaliserade erbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Skapa reserverbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Skapa samlingar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Skapa samlingskvalificerare](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [Skapa beslut](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Rankningsstrategier](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [Leverera erbjudanden i meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Leverera erbjudanden med Edge Decisioning API](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)

### Datainsamling och webb/mobil-SDK

- [SDK - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/web-sdk/home)
- [Installera SDK](https://experienceleague.adobe.com/sv/docs/experience-platform/web-sdk/install/overview)
- [Mobile SDK - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Konfigurera datastreams](https://experienceleague.adobe.com/sv/docs/experience-platform/datastreams/configure)
- [Edge Network Server API - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/edge-network-server-api/overview)

### XDM och datamodellering

- [XDM - systemöversikt](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/home)
- [Grundläggande om schemakomposition](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/schema/composition)
- [Skapa en datauppsättning](https://experienceleague.adobe.com/sv/docs/experience-platform/catalog/datasets/create)
- [Definiera en relation mellan två scheman](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/tutorials/relationship-api)

### Identitet och profil

- [Översikt över identitetstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/home)
- [Översikt över namnutrymmen för identiteter](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/features/namespaces)
- [Översikt över kopplingsprofiler](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/merge-policies/overview)
- [Översikt över kundprofiler i realtid](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/home)

### Målgrupper och segmentering

- [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/home)
- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/ui/segment-builder)
- [Direktuppspelningssegmentering](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Edge segmentering](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/methods/edge-segmentation)

### Beräknade attribut och profilberikning

- [Översikt över beräknade attribut](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/computed-attributes/overview)
- [Användargränssnittshandbok för beräknade attribut](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/computed-attributes/ui)
- [Översikt över AI för kunder](https://experienceleague.adobe.com/sv/docs/experience-platform/intelligent-services/customer-ai/overview)

### Kanalkonfiguration

- [Kom igång med e-postkonfiguration](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Konfigurera kanalytor](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Delegera underdomäner](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)

### Framtagning och personalisering av meddelanden

- [Designa e-postinnehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Lägg till personalisering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization syntax](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Dynamiskt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Arbeta med innehållsmallar](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/content-management/content-templates/content-templates)

### Rapportering och analys

- [Global kampanjrapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Global reserapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Arbeta med Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [CJA - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-overview/cja-overview)
- [Analysis Workspace - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/home)
- [Översikt över beräknade mätvärden](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)

### Datastyrning och livscykel

- [Översikt över dataförvaltning](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/home)
- [Översikt över etiketter för dataanvändning](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/labels/overview)
- [Översikt över livscykelhantering av avancerade data](https://experienceleague.adobe.com/sv/docs/experience-platform/data-lifecycle/home)
- [Utgångsdatum för datauppsättning](https://experienceleague.adobe.com/sv/docs/experience-platform/data-lifecycle/ui/dataset-expiration)

### Övervakning och iakttagbarhet

- [Översikt över Insikter i observationer](https://experienceleague.adobe.com/sv/docs/experience-platform/observability/home)
- [Översikt över aviseringar](https://experienceleague.adobe.com/sv/docs/experience-platform/observability/alerts/overview)

### Skyddsräcken

- [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/get-started/guardrails)
- [Garantier för kundprofiler i realtid](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/guardrails)
- [Förvaringsskydd](https://experienceleague.adobe.com/sv/docs/experience-platform/ingestion/guardrails)
- [Garantier för identitetstjänst](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/guardrails)

### Självstudiekurser och guider

- [Översikt över källor](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/home)
- [Översikt över taggar](https://experienceleague.adobe.com/sv/docs/experience-platform/tags/home)
- [Fältgruppen för samtycke och inställningar](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/field-groups/profile/consents)
