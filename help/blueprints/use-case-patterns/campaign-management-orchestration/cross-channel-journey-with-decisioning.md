---
title: Flerkanalsresor med beslut
description: Lär dig att samordna en flerstegsresa som innefattar realtidsbeslut för att välja optimala kanaler, innehåll eller erbjudanden.
solution: Journey Optimizer, Real-Time Customer Data Platform
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '8992'
ht-degree: 0%

---


# Flerkanalsresor med beslutsfattande

Den här guiden ger en fullständig implementeringsreferens för flerkanalsresor med beslutsfattande. Det är utformat för lösningsarkitekter, marknadsföringsteknologer och implementeringstekniker som behöver samordna flerstegsresor i flera kanaler med realtidsbeslut på en eller flera resedaggar.

Använd den här vägledningen när du vill veta mer om implementeringsalternativ, utvärdera avvägningar och navigera till relevant Experience League-dokumentation för detaljerade konfigurationsinstruktioner.

Flerkanalsresor med beslutsfattande är det mest sofistikerade kampanjkoordineringsmönstret i ekosystemet [!DNL Adobe Experience Platform]. Den utökar flerstegsdirigerade resor genom att införliva realtidsbeslut, med [!DNL AJO]-beslut om att utvärdera en profils aktuella kontext och dynamiskt välja den optimala kanalen, innehållet eller erbjudandet vid en eller flera beslutspunkter på arbetsytan.

## Använd ärendeöversikt

Organisationer behöver i allt högre grad kunna leverera anpassningsbara, personaliserade kundresor som dynamiskt motsvarar varje enskild individs realtidskontext i stället för att följa en fast, förutbestämd sekvens. En kunds föredragna kanal, deras engagemangshistorik, deras lojalitetsnivå, deras förväntade livstidsvärde och deras nuvarande produktintressen är avgörande för vad den näst bästa åtgärden bör vara vid varje kontaktyta.

Flerkanalsresan med beslutsfattande tillgodoser detta behov genom att kombinera två kraftfulla [!DNL AJO]-funktioner: resesamordning (som hanterar flerstegsflödet, timing, villkor och kanalleverans) och beslut (som utvärderar behörighetsregler, tillämpar rangordningsstrategier och väljer den optimala erbjudandet eller innehållsvarianten vid varje beslutspunkt).

Det här mönstret passar bäst när:

- Färden måste anpassas dynamiskt till varje profils realtidstillstånd i stället för att följa en fast kanal eller innehållssekvens
- Flera erbjudanden, innehållsvarianter eller kanaler är kandidater på en eller flera reseddelanden, och det bästa alternativet bör väljas baserat på profilkontext
- AI-assisterad eller formelbaserad rankning krävs för att optimera urvalet av erbjudanden under hela kundresan
- Organisationen vill konsolidera logiken för kanalval och erbjuda hantering i ett centraliserat beslutsramverk istället för att underhålla komplex förgrenade logik

Målgruppen är bland annat marknadsförare som hanterar livscykelprogram, lojalitetsresor, återvinningssekvenser och introduktionsflöden där personalisering i stor skala kräver automatiskt beslutsfattande vid varje kontaktyta.

## Viktiga verksamhetsmål

Följande affärsmål behandlas i det här användningsmönstret.

**[Leverera personaliserade kundupplevelser](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**
Skräddarsy innehåll, erbjudanden och budskap efter enskilda preferenser, beteenden och livscykelsteg.
**KPI:er:** engagemang, konverteringsgrader, kundnöjdhet (CSAT)

**[Öka kundlojalitet och livstidsvärde](../../business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)**
Fördjupa kundrelationerna och maximera det långsiktiga värdet genom lojalitetsprogram, belöningar och personaliserat engagemang.
**KPI:er:** Kundens livstidsvärde, kvarhållning, merförsäljning/korsförsäljning %

**[Förbättra kundlojaliteten](../../business-objectives/customer-experience/improve-customer-retention.md)**
Håll befintliga kunder engagerade och förnyade genom värdestyrda upplevelser och kontinuerlig relationshantering.
**KPI:er:**-lagring, kundens livstidsvärde, engagemang

**[Öka korsförsäljning och merförsäljning](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)**
Marknadsför kompletterande och premiumbaserade produkter eller tjänster till befintliga kunder baserat på beteenden och inköpshistorik.
**KPI:er:**, merförsäljning/korsförsäljning %, inkrementell intäkt, kundens livstidsvärde

## Exempel på taktiska användningsfall

Följande scenarier visar hur flerkanalsresor med beslutsfattande kan tillämpas i praktiken.

- **Adaptiv återvinnande resa** - En resa i flera steg där beslut väljer kanal (e-post, push eller SMS) baserat på varje profils interaktionshistorik och dynamiskt väljer det bästa incitamentserbjudandet baserat på förväntat livstidsvärde
- **Livscykeln för nästa bästa åtgärd** - Beslut avgör vad som ska kommuniceras i varje fas av kundlivscykeln, utifrån startinnehåll, korsförsäljningserbjudanden, förmånserbjudanden eller kundlojalitetsincitament
- **Personaliserad introduktion med dynamiskt innehållsval** - Ny kundintroduktionsresa där varje kontaktyta väljer det mest relevanta produktutbildningsmaterialet, tips eller aktiveringserbjudandet
- **Flerkanals lojalitetsprogramresa med personaliserade belöningar** - Lojalitetsmedlemmar går igenom en resa där beslut väljer personaliserade belöningserbjudanden baserat på nivå, inköpshistorik och kategoritillhörighet
- **Dynamiskt återengagemang med optimering av kanaler och incitament** - Dåligt återengagemang från kunder där både den utåtriktade kanalen och incitamentet väljs dynamiskt för att maximera sannolikheten för svar
- **Kundens livscykler med AI-rankade innehållsrekommendationer** - Pågående vårdresa där AI-rankade beslut väljer det mest relevanta innehållet eller produktrekommendationerna vid varje kontaktyta

## Nyckeltal för prestanda

Använd följande nyckeltal för att mäta effektiviteten för det här användningsmönstret.

| KPI | Beskrivning | Mätningsmetod |
| --- | --- | --- |
| Färdavslut | Procentandel profiler som slutför hela resan | Reserapport: ifylld/inskriven |
| Ansvarsfrekvens för erbjudande | Procentandel av valda beslutsalternativ som är engagerade med (klickade, lösta) | Beslutsrapport: erbjudandeklickningar/erbjudandevisningar |
| Kanalengagemang | Öppna och klicka på frekvenser i alla kanaler som används under resan | Resultatstatistik per kanal i reserapport |
| Konverteringsgrad | Procent av resedeltagare som slutför målkonverteringsåtgärden | Händelsespårning vid avresa eller CJA funnel-analys |
| Reserverbjudande | Procent av beslutsbegäranden som returnerar reserverbjudandet i stället för ett personaliserat erbjudande | Beslutsrapport: reservval/totalt urval |
| Värdepåverkan för kundens livstid | Förändring i CLV för resedeltagare jämfört med kontrollgrupp | CJA cohort analysis with holdout comparison |
| Merförsäljning/merförsäljning | Ökad intäkt som tillskrivs valda erbjudanden | CJA attribueringsanalys av anbudsdrivna konverteringar |
| Effektivitet vid bedömning av rangordning | Resultatskillnad mellan AI-rankade erbjudanden och slumpmässigt/prioritetsbaserat urval | A/B-experiment där rankningsstrategier jämförs |

## Använd skiftlägesmönster

**Flerkanalsresa med beslut**

Samordna en flerstegs flerkanalsresa som innefattar realtidsbeslut på en eller flera noder för att välja den optimala kanalen, innehållet eller erbjudandet.

**Funktionskedja:** Målgruppsutvärdering > Resekörning > Beslutsnod > Kanalval > Meddelandeleverans > Rapportering

## Tillämpningar

Följande program används för att implementera det här användningsmönstret.

- **[!DNL Adobe Journey Optimizer]([!DNL AJO])** - Resesamordning (design av arbetsyta i flera steg, startvillkor, väntevillkor, avslutsvillkor), meddelandeskapande över flera kanaler, kanalytkonfiguration, hantering av konflikter och prioriteter
- **[!DNL Adobe Journey Optimizer]Beslut** - Hantering av erbjudanden och innehållsobjekt, regler för behörighet, rangordningsstrategier (prioritet, formel, AI), beslutsprinciper, ersättningar, reserverbjudanden
- **[!DNL Adobe Real-Time Customer Data Platform]([!DNL RT-CDP])** - Målgruppsutvärdering för registrering av resor och segment för erbjudandekvalificering, profilanrikning med beräknade attribut och benägenhetspoäng, samtycke och efterlevnadskontroll
- **[!DNL Adobe Experience Platform]([!DNL AEP])** - Kundprofilarkiv i realtid, identitetstjänst för flerkanalsupplösning, datamodellering och inmatningsinfrastruktur i realtid

## Foundationsfunktioner

Följande grundläggande funktioner måste finnas för det här användningsmönstret. För varje funktion anger statusen om den vanligtvis är obligatorisk, antas vara förkonfigurerad eller inte tillämplig.

| Funktionen Foundation | Status | Vad måste finnas på plats | Experience League referens |
| --- | --- | --- | --- |
| Administration och styrning | Antagen på plats | [!DNL AJO]-sandlådan med konfigurerade behörigheter för resa, kampanj och beslut. Kanalytor för alla möjliga leveranskanaler. Användarroller för resedesigners, beslutsfattare och innehållsförfattare. | [Översikt över sandlådor](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/home), [Översikt över åtkomstkontroll](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Datamodellering och förberedelse | Obligatoriskt | Profilschemat måste innehålla attribut som används för beslut (till exempel lojalitetsnivå, inköpshistorik, kanalinställningar, engagemangspoäng). Erbjudandekatalog och beslutsscheman måste konfigureras. ExperienceEvent-scheman måste fånga upp beteendesignaler som används av regler för behörighet och rankningsformler. | [Systemöversikt för XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [Grundläggande om schemakomposition](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| Datakällor och samling | Antagen på plats | Profilattribut och beteendesignaler som används vid beslut måste vara aktuella. Händelseströmning i realtid behövs om resan använder händelseutlösta kriterier för inträde eller utträde. Web SDK, Mobile SDK eller serversidessamling måste vara aktiva för kanaler som har feed-beslutssammanhang. | [Översikt över Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home), [Översikt över källor](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home) |
| Konfiguration av identitet och profil | Obligatoriskt | Identitetsupplösning för flera kanaler är avgörande - resan måste matcha profiler via e-post, push, SMS och webben. Sammanslagningsprinciper måste skapa en enhetlig profil för beslut. Identitetsnamnutrymmen för alla kundidentifierare (CRM-ID, e-post, ECID, telefon) måste konfigureras. | [Översikt över identitetstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [Översikt över sammanslagningsprinciper](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| Målgruppsdefinition och segmentering | Obligatoriskt | Målgruppsdefinition för resan. Ytterligare segment som används för att erbjuda regler för kvalificering och villkorsförgreningar under resan. Utvärderingsmetoden måste matcha latenskraven (direktuppspelning för registrering i realtid, batch för schemalagd). | [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [Användargränssnittsguide för segmentbyggaren](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder) |

## Stödfunktioner

Följande funktioner förstärker det här användningsmönstret, men behövs inte för att köra kärnan.

| Stödfunktioner | Status | Varför det spelar någon roll | Experience League referens |
| --- | --- | --- | --- |
| Skapande av beräknat/härlett attribut | Rekommenderad | Beräknade attribut som till exempel kundernas AI-poängtal, engagemangsmätningar, kanalpreferenser och beräkningar av livstidsvärden förbättrar beslutskvaliteten avsevärt. Dessa förhöjda profilattribut möjliggör mer sofistikerade regler för behörighet och rankningsformler. | [Översikt över beräknade attribut](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview), [Översikt över AI för kunder](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview) |
| Livscykelhantering för data | Rekommenderad | Erbjud historik- och beslutshändelsedata ackumuleras över tid och bör ha lagringspolicyer. Det är viktigt att kunna genomdriva samtycke över flera kanaler - profiler utan giltigt samtycke för en kanal måste uteslutas från den kanalens leveransväg. | [Översikt över livscykelhantering av avancerade data](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home), [Medgivande i Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted) |
| Dataanvändningsetiketter och -tillämpning | Rekommenderad | Styrning över flera kanaler och erbjudandetyper är viktigt när beslut kan dirigera profiler till olika kanaler med olika begränsningar för dataanvändning. Ser till att erbjudandet levereras korrekt över alla kanaler. | [Översikt över datastyrning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [Krävande av principer](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/enforcement/overview) |
| Övervakning och observerbarhet | Ingår | Resekontroll och beslutsövervakning är av största vikt för produktionsverksamheten. Varningar vid fel vid registrering av resor, beslut om reservtoppar och leveransfel möjliggör snabb problemlösning. | [Aviseringsöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview), [Översikt över Insikter i observabilitet](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| Rapportering och analys | Ingår | Reserapporter och beslutsrapporter ingår i rapporteringsfasen. CJA analys av beslutseffektivitet, optimering av kanalmixning, resultat och avkastning på kundresan ger de insikter som behövs för att förfina rangordningsstrategier och optimera kundresan över tid. | [CJA - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [AJO + CJA - integreringsguide](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo) |

## Programfunktioner

I den här planen används följande funktioner från programfunktionskatalogen. Funktioner mappas till implementeringsfaser i stället för till numrerade steg.

### [!DNL Journey Optimizer] ([!DNL AJO])

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Kanalkonfiguration | Fas 2: Kanalkonfiguration | Konfigurera kanalytor för alla kanaler som kan väljas eller som resan använder (e-post, SMS, push, i appen) |
| Redigering av meddelanden | Fas 4: Meddelanderedigering | Skapa meddelandeinnehåll för varje kanal och integrera beslutsunderlag - erbjudandeplaceringar, dynamiska innehållsblock, personaliseringstoken från utvalda erbjudanden |
| Beslutsfattande | Fas 3: Beslutsinställningar | Konfigurera erbjudandeartiklar, regler för behörighet, rankningsstrategier, beslutspolicyer och reserverbjudanden för varje beslutspunkt under resan |
| Journey Orchestration | Fas 5: Resedesign och aktivering | Utforma arbetsytan för flerstegsresor med startvillkor, beslutsnoder, kanalroutning, väntesteg, meddelandeåtgärder och avslutskriterier |
| Konflikt- och prioritetshantering | Fas 5: Resedesign och aktivering | Konfigurera prioritetspoäng och konfliktidentifiering om flera resor kan ha samma profiler som mål samtidigt |
| Frekvens och affärsregler | Fas 5: Resedesign och aktivering | Tvinga frekvensgränser för meddelanden över flera kanaler för att förhindra att meddelanden skickas över flera kanaler |
| Rapportering och prestandaanalys | Fas 6: Rapportering och övervakning | Övervaka kundens resa och leveransstatistik per nod, beslutsresultat och kanalengagemang |

### [!DNL Real-Time CDP] ([!DNL RT-CDP])

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Målgruppsutvärdering | Fas 1: Målgruppsutvärdering | Definiera och utvärdera tävlingsdeltagare eller kvalificerande anmälningshändelse; skapa berättigandesegment som används genom beslut |
| Profilberikning | Krav/stöd | Förbättra profiler med beräknade attribut och benägenhetspoäng som förbättrar beslutskvaliteten |
| Verkställande av samtycke och styrning | Fas 2: Kanalkonfiguration | Använd medgivandeinställningar i alla kanaler; säkerställ att erbjudandet levereras enligt gällande regler |

## Förutsättningar

Slutför följande innan du börjar implementera.

- [ ] [!DNL AJO]-sandlådan har etablerats med funktioner för resesamordning och beslutsfattande aktiverade
- [ ] Alla målkanaler (e-post, SMS, push) har aktiva, verifierade kanalytor
- [ ] Profilschemat innehåller attribut som krävs för beslut (lojalitetsnivå, inköpshistorik, kanalinställningar, engagemangspoäng)
- [ ] Identitetsupplösning för flera kanaler har konfigurerats - profiler kan matchas via e-post, push-token, telefonnummer och webbidentifierare
- [ ]-målgruppen definieras och utvärderas med en population som inte är noll
- [ ] Erbjud kataloginnehåll (kreativa resurser, kopia, juridisk ansvarsfriskrivning) är godkänt och klart för konfiguration
- [ ] data för samtycke hämtas och krav på samtycke är aktiva för alla målkanaler
- [ ] Innehållsmallar och fragment för varje kanal har utformats och godkänts
- [ Regler för frekvensbegränsning för ] definieras och distribueras om organisationen har frekvensregler för flera kampanjer
- [ ] Om AI-rankat beslut används finns det minst 1 000 konverteringshändelser för modellutbildning

## Implementeringsalternativ

Granska följande alternativ och välj den metod som passar dina behov bäst.

### Alternativ A: Resa med offertbeslut (fast kanal, dynamiskt innehåll)

**Bäst för:** Resor där kanalsekvensen är förbestämd men innehållet eller erbjudandet vid varje kontaktyta ska väljas dynamiskt - lojalitetsresor med personaliserade belöningar, återengagemang med dynamiska incitament, livscykelnäring med rekommendationer för AI-rankat innehåll.

#### Så här fungerar det

Färdens arbetsyta definierar den fasta sekvensen av kanaler och tidpunkter (till exempel Dag 0: E-post, Dag 3: Tryck, Dag 7: SMS). Vid varje nod för meddelandeåtgärd väljer en beslutsprincip det bästa erbjudandet eller det bästa innehållet som ska ingå i meddelandet från en konfigurerad katalog med kvalificerade artiklar. Erbjudandena hanteras i [!DNL AJO]-beslutskatalogen med berättiganderegler som filtrerar efter en profil och rangordningsstrategier som avgör vilket kvalificerat erbjudande som passar bäst.

Detta tillvägagångssätt skiljer&quot;när och var&quot; (resesamordning) från&quot;vad&quot; (beslut). Resedesignern styr kanalflödet medan beslutsfattaren styr erbjudandekatalogen, reglerna för behörighet och rangordningslogiken oberoende av varandra. Detta innebär att implementeringen blir enklare och att erbjudandekatalogen kan utvecklas utan att arbetsytan ändras.

Erbjudandeplaceringar bäddas in direkt i meddelandeinnehållet med e-post-Designer eller andra kanalredigerare. När meddelandet återges vid leveranstillfället utvärderar beslutsmotorn profilens behörighet och rankning för att välja det optimala erbjudandet för varje placering i meddelandet.

#### Viktiga överväganden

- Kanalsekvensen är statisk - alla profiler följer samma kanalsökväg oavsett deras inställningar
- Beslutsfattningens komplexitet är mindre eftersom det bara väljer innehåll/erbjudanden, inte kanaler
- Erbjudandekatalogen kan hanteras oberoende av resan
- Reserverbjudanden måste konfigureras för varje placering för att hantera profiler utan personliga erbjudanden som är berättigade

#### Fördelar

- Enklare arbetsyta - ingen förgrenade logik för kanalval
- Tydlig åtskillnad mellan resedesign och hantering av erbjudanden
- Enklare att testa och validera - varje kanalsökväg är deterministisk
- Mindre komplex implementering och kortare time-to-market
- Katalogändringarna träder i kraft omedelbart utan reseändringar

#### Begränsningar

- Det går inte att anpassa kanalen baserat på beteende eller inställningar för enskilda profiler
- Profiler som föredrar en kanal framför en annan får fortfarande meddelanden på de förbestämda kanalerna
- Optimerar inte för engagemangsnivåer på kanalnivå

#### Experience League-referenser

- [Leverera erbjudanden i meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Beslutsledning - översikt](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)

### Alternativ B: Resa med dynamiskt kanalval (fast innehåll, dynamisk kanal)

**Bäst för:** Resor där innehållet vid varje kontaktyta är liknande men kanalen ska väljas dynamiskt baserat på profilkontext - adaptiv förstärkning (e-post kontra SMS baserat på engagemang), näst bästa åtgärdsprogram där kanaloptimering är det primära målet.

#### Så här fungerar det

Under resan används villkorsnoder som bygger på profilattribut (t.ex. kanalpreferenser, senaste engagemangskanal eller medgivandestatus) eller som beslutsutdata för att dirigera profiler till olika kanalsökvägar. Varje sökväg levererar kanalspecifikt innehåll via en egen meddelanderefod. Beslutslogiken avgör vilken kanal som är mest sannolik att utlösa engagemang baserat på profilens beteendehistorik.

Kanalval kan implementeras med noder för resevillkor med profilattributsutvärderingar (till exempel om `channelPreference = "push"` dirigerar till push-banan), eller genom att använda beslut med kanalspecifika objekt där varje erbjudande representerar en kanal och rankningsstrategin avgör den bästa kanalen.

Med den här metoden optimeras leveranskanalen samtidigt som innehållet är relativt enhetligt i alla kanaler. Det kräver att meddelandeinnehåll skapas för varje möjlig kanal, och kanalytor måste konfigureras för alla kanaler.

#### Viktiga överväganden

- Kräver meddelandeinnehållsvarianter för varje kandidatkanal
- Kanalytorna måste vara aktiva för alla möjliga kanaler
- Villkorslogik eller beslutskonfiguration måste ta hänsyn till samtycke - profiler utan SMS-medgivande kan inte dirigeras till SMS-sökvägen
- Resans arbetsyta är mer komplex med förgreningsbanor för varje kanal

#### Fördelar

- Optimerar kanalval för varje enskild profil
- Ökar det övergripande engagemanget genom att nå ut till profiler via den kanal de föredrar
- Respekterar kanalspecifikt samtycke automatiskt genom tillståndsmedveten dirigering
- Kan införliva engagemangshistorik och kanalpreferenser i beslut om att slussa runt ärendet

#### Begränsningar

- Mer komplex arbetsyta med flera kanaler
- Innehållet måste skapas separat för varje kanal (även om meddelandemetoden är densamma)
- Svårare att testa - måste validera alla möjliga kanalsökvägar
- Innehållspersonalisering inom varje kanal är statisk (inget beslut om erbjudande)

#### Experience League-referenser

- [Villkorsaktivitet](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Skapa en resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)

### Alternativ C: En helt anpassningsbar resa (dynamisk kanal + dynamiskt innehåll)

**Bäst för:** Maximal personalisering - både kanalen och innehållet/erbjudandet väljs dynamiskt på varje nod. Lämpligt för värdefulla kundsegment, avancerade lojalitetsprogram och organisationer med väl fungerande beslutsrutiner och omfattande profildata.

#### Så här fungerar det

Det här alternativet kombinerar alternativen A och B. För resan används beslut på två nivåer: för det första för att avgöra vilken kanal som ska användas för varje kontaktyta och för det andra för att avgöra vilket innehåll eller erbjudande som ska levereras i den valda kanalen. Varje beslutspunkt i resan utvärderar profilens aktuella kontext för att göra både kanal- och innehållsval.

Implementeringen kräver omfattande beslutsunderlag med beslutsregler för både val av kanal och val av innehåll/erbjudande. Kanalvalet kan använda en beslutspolicy där varje objekt representerar en kanal med berättiganderegler som baseras på samtycke och engagemang, medan innehållsvalet använder en separat beslutspolicy med offertobjekt rankade efter relevans.

Detta är den mest komplexa varianten och kräver den djupaste integrationen mellan resesamordning och beslutsfattande. Det ger högsta grad av personalisering men kräver också den mest konfigurering, testning och kontinuerlig hantering.

#### Viktiga överväganden

- Kräver två skikt för beslutsfattande - kanalval och innehållsval
- Arbetsytans komplexitet är som störst med kapslad förgrening och beslut vid varje nod
- Omfattande testning krävs för alla möjliga kombinationer av kanaler och innehåll
- Kräver omfattande profildata (engagemangshistorik, kanalpreferenser, produkttillhörighet, benägenhetspoäng) för effektivt beslutsfattande
- AI-rankad beslutsfördel ger avsevärda fördelar av beräknade attribut

#### Fördelar

- Maximal personalisering - alla kontaktytor är optimerade för kanaler och innehåll
- Bästa engagemang och konverteringspotential för välkonfigurerade implementeringar
- Centraliserar all personaliseringslogik i stället för statiska kundresor
- Kan kontinuerligt förbättras genom inlärning av AI-rankningsmodell

#### Begränsningar

- Högsta komplexitet i implementeringen och längsta time to market
- Kräver omfattande katalog- och kanalinnehållsförberedelser
- Svårt att felsöka när leveransproblem uppstår
- Kräver en mogen datainfrastruktur med avancerade profilattribut
- AI-rankningen kräver en tillräcklig volym för konverteringshändelser för modellutbildning

#### Experience League-referenser

- [Beslutsledning - översikt](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Rankningsstrategier](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Jämförelse av alternativ

Använd följande tabell för att snabbt jämföra de tre implementeringsalternativen.

| Kriterier | Alternativ A: Beslut om erbjudande | Alternativ B: Dynamisk kanal | Alternativ C: Fullständig adaptiv |
| --- | --- | --- | --- |
| Bäst för | Fast kanalsekvens, dynamiskt innehåll | Kanaloptimering, enhetligt innehåll | Maximal personalisering i båda dimensionerna |
| Komplex | Medelsvåra: | Medium-High | Högt |
| Reseduk | Enkel (linjär med beslut vid actionnoder) | Måttlig (förgreningar för kanalsökvägar) | Komplex (kapslad förgrening med beslut på flera nivåer) |
| Beslutsfattningens omfattning | Endast innehåll/erbjudande | Endast kanalval | Markering av både kanal och innehåll |
| Innehållskrav | En uppsättning innehåll per kanal (med erbjudanden) | Innehåll för varje kandidatkanal | Innehåll med erbjudandeplaceringar för varje kanal |
| Profildatabehov | Måttligt (attribut för erbjudande) | Måttlig (kanalpreferens, engagemang) | Hög (både kanal och attribut) |
| time to market | Snabbare | Måttlig | Längst |
| Löpande hantering | Kataloghantering | Hantering av logik för kanalroutning | Både katalog- och kanalroutning |
| Personalization - djup | Innehållet varierar, kanalen är fast | Kanalen varierar, innehållet liknar | Både kanal och innehåll varierar |

### Välj rätt alternativ

Använd följande riktlinjer för att fastställa det bästa alternativet för din situation.

- **Börja med alternativ A** om din kanalstrategi redan är definierad (till exempel&quot;vi skickar alltid e-post först, sedan push, sedan SMS&quot;) och det primära personaliseringsbehovet är att välja rätt erbjudande eller innehåll vid varje kontaktyta. Det här är den vanligaste utgångspunkten för organisationer som inte är beslutsamma.

- **Välj alternativ B** om kanaloptimering är det primära målet - du vill nå varje kund i den kanal som de troligast interagerar med, men meddelandeinnehållet är relativt konsekvent över alla kanaler. Detta kräver kanalinställningsdata för profiler.

- **Välj bara alternativ C** när du har en väl fungerande beslutsinfrastruktur, omfattande profildata (inklusive beräknade attribut och benägenhetspoäng), en väl ifylld erbjudandekatalog och organisationskapaciteten för att hantera komplexiteten. Många organisationer börjar med alternativ A eller B och utvecklas till alternativ C allt eftersom deras beslutslösning ökar.

- **Om du är osäker** börjar du med alternativ A. Den ger en meningsfull personalisering med minsta möjliga komplexitet, och den erbjudandekatalog du bygger för alternativ A kan återanvändas direkt om du senare går över till alternativ C.

## Implementeringsfaser

Följande faser går igenom hela implementeringen av det här fallmönstret.

### Fas 1: Målgruppsutvärdering

**Programfunktion:** [!DNL RT-CDP]: Målgruppsutvärdering

Den här fasen konfigurerar den målgrupp som bestämmer vilka profiler som kommer in på resan och eventuella ytterligare segment som används för att erbjuda regler för kvalificering eller villkorsförgreningar under resan. Målgruppsdefinitionen är grunden för all efterföljande resa och beslutslogik.

#### Beslut: Typ av bidrag

Hur ska profiler ta sig in på resan - via en schemalagd läsning eller en händelseutlösare i realtid?

>[!NOTE]
>Välj en typ av inträde baserat på resans timing och triggerbehov.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Läs målgrupp (gruppinmatning) | Livscykelprogram, lojalitetsresor, schemalagda återengagemangskampanjer | Profilerna anges i grupper vid schemalagda tidpunkter, målgruppen utvärderas vid läsning, stöder stora målgruppsstorlekar |
| Målgruppskvalifikation (direktuppspelning) | Beteendeutlösta resor där inträde ska ske när en profil går in i eller ut ur ett segment | Nära inträde i realtid; kräver en definition av segment som kan strömmas, bra för milstolpe-baserade resor |
| Unitary Event (händelseutlösare) | En specifik händelse bör utlösa resan (t.ex. köp, övergivna varukorgar, registrering) | Real-time entry on event; requires event schema configuration; limited to 5 000 events/second |

#### Beslut: Metod för utvärdering av målgrupper

Hur snabbt måste målgruppen kvalificera sig för profiler?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Grupp | Dagliga eller periodiska målgruppsuppdateringar är tillräckliga; schemalagda kampanjliknande resor | Bearbetar upp till 24 MB profiler per jobb, schemabaserade, de flesta segmentregeluttryck stöds |
| Direktuppspelning | Målgruppsmedlemskap i realtid krävs för händelseutlösta eller kvalificeringsbaserade bidrag | Närliggande realtid; begränsad segmentregelfunktionsuppsättning; ingen tidsbaserad aggregering |
| Edge | Samsessionskvalifikation krävs | Millisekundsfördröjning; endast enkla attributkontroller; begränsat till kantprofilattribut |

#### Information om nyckelkonfiguration

**Gränssnittsnavigering:** Kund > Målgrupper > Skapa målgrupp > Skapa regel

- Definiera målgruppen med hjälp av Segment Builder med segmentregeluttryck som riktar sig till relevanta profilattribut och beteendehändelser
- Skapa ytterligare berättigandesegment om reglerna för erbjudandebehörighet ska referera till segmentmedlemskap (t.ex.&quot;Högvärdeskunder&quot;,&quot;Lojalitetsnivå&quot;)
- Kontrollera att målgruppspopulationen inte är noll innan du fortsätter till resekonfigurationen
- Välj den sammanfogningsprincip som skapar den enhetliga profilvy som krävs för beslut

#### Experience League-dokumentation

- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Direktuppspelningssegmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Edge segmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Profile Query Language referens](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### Fas 2: Kanalkonfiguration

**Programfunktion:** [!DNL AJO]: Kanalkonfiguration

Den här fasen konfigurerar kanalytor för varje kanal som resan kan använda för att leverera meddelanden. Alla kanaler måste ha aktiva, verifierade ytor innan meddelanden kan skapas eller resan kan publiceras. För det här mönstret konfigurerar du vanligtvis ytor för e-post, SMS och push i minsta möjliga mån - och eventuellt i appen eller på webben om beslut kan välja dessa kanaler.

#### Beslut: Vilka kanaler ska konfigureras

Vilka kanaler är kandidater för resan - antingen som fasta resesteg (alternativ A/B) eller som valbara kanaler (alternativ B/C)?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Endast e-post | Enkelkanalig resa med offertbeslut (alternativ A, endast e-post) | Enklast konfiguration; kräver delegering av underdomän och IP-värmare |
| E-post + push | Tvåkanalig resa; vanlig för engagemangsinriktade resor | Push kräver APN/FCM-inloggningsuppgifter; mobilappen måste ha SDK integrerat |
| E-post + SMS + push | Fullständig flerkanalsresa, vanligaste för alternativ B och C | SMS kräver autentiseringsuppgifter för leverantörer (Sinch, Twilio, Infobip); varje kanal behöver sin egen yta |
| Email + SMS + Push + In-App | Maximal kanaltäckning inklusive sessionsytor | Konfiguration av mobilappen kräver SDK och appytan |

#### Beslut: Delegeringsmetod för underdomän (e-post)

Hur ska den sändande underdomänen delegeras till Adobe?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Fullständig delegering | Organisationen vill att Adobe ska hantera alla DNS-poster för den sändande underdomänen | Enklast installation; Adobe hanterar SPF, DKIM, DMARC; mindre kontroll över DNS |
| CNAME-delegering | Organisationen måste behålla kontrollen över DNS-poster | Komplexare konfiguration; kunden hanterar DNS; ger större flexibilitet |

#### Information om nyckelkonfiguration

**Gränssnittsnavigering:** Administration > Kanaler > Kanalytor > Skapa yta

- För e-post: konfigurera underdomän, IP-pool, avsändarnamn, svarsadress och hantering av avanmälan
- För SMS: konfigurera autentiseringsuppgifter för SMS-provider och avsändarnummer
- För push: konfigurera APN och FCM-referenser för iOS och Android
- Kontrollera att alla ytor har statusen Aktiv innan du fortsätter
- Bekräfta att IP-värmerappningen har slutförts för e-postsändning av IP-adresser

#### Experience League-dokumentation

- [Kom igång med e-postkonfiguration](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegera underdomäner](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Skapa IP-pooler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [Konfigurera SMS-kanal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Konfigurera kanal för push-meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Fas 3: Beslutsinställningar

**Programfunktion:** [!DNL AJO]: Bestämning

I den här fasen konfigureras det fullständiga beslutsramverket, inklusive praktik, regler för behörighet, personaliserade erbjudanden, reserverbjudanden, insamlingskvalificerare, samlingar, rankningsstrategier och beslutspolicyer. I den här fasen skapas den beslutslogik som ska anropas vid beslutsunderlag för resan.

#### Beslut: Beslutets tillämpningsområde

Vad ska jag välja mellan - erbjudanden/innehåll (alternativ A), kanaler (alternativ B) eller båda (alternativ C)?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Endast erbjudande/innehåll | Kanalsekvensen är fast; personalisering finns i innehållet | Beslutspolicyer har erbjudandeobjekt med innehåll som representeras per placering |
| Endast kanalval | Innehållet är enhetligt. Optimeringen görs i leveranskanalen | Beslutsobjekten representerar kanaler, behörigheten omfattar samtyckeskontroller, rankningen använder engagemangsdata |
| Både kanal och innehåll | Fullständig, anpassningsbar personalisering över alla kanaler och innehåll | Kräver två skikt av beslutsprinciper; den mest komplexa men högsta personaliseringen |

#### Beslut: Rankningsstrategi

Hur ska berättigade erbjudanden rangordnas för att kunna välja den bästa?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Prioritetsbaserad (manuell) | Enkel rankning där affärsregler avgör erbjudandeprioritet | Varje erbjudande får högsta prioritet, högsta prioritet vinner, är deterministiskt och lätt att förstå |
| Formelbaserat (anpassat uttryck) | Rankningen bör ta hänsyn till profilattribut (t.ex. CLV, tier, affinity score)) | Anpassad rankningsformel utvärderar profilkontext; mer dynamisk än prioritet; ingen ML krävs |
| AI-rankad (automatisk optimering) | Rankningen bör optimeras automatiskt baserat på historiska konverteringsdata | AI-modellen lär sig av konverteringshändelser; kräver minst 1 000 event för utbildning; förbättras kontinuerligt |

#### Beslut: Erbjudandebegränsning

Bör det finnas begränsningar för hur många gånger ett erbjudande visas?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Anfang per profil | Förhindra att samma erbjudande visas upprepade gånger i samma profil | Skyddar mot utmattning av erbjudanden. Motsvarande fördröjning kan inträffa under hög genomströmning |
| Global ändpunkt | Begränsa totala visningar för alla profiler (t.ex. begränsade lagerkampanjer) | Styr den totala exponeringen; användbart för leveransbegränsade erbjudanden |
| Ingen ände | Alla berättigade intryck bör visa erbjudandet | Lättaste; lämpligt för helgrönt innehåll eller obegränsat erbjudande |

#### Information om nyckelkonfiguration

**Gränssnittsnavigering:** Komponenter > Beslutshantering > Placeringar/erbjudanden/beslut

- Skapa placeringar för varje kombination av kanal och innehållstyp (t.ex. e-postbanderoll, push JSON, SMS)
- Definiera berättiganderegler med hjälp av segmentregeluttryck som refererar till profilattribut eller målgruppsmedlemskap
- Skapa personaliserade erbjudanden med representationer för varje placering, tilldela regler för behörighet och ange prioritet
- Skapa ett reserverbjudande som täcker alla placeringar - detta returneras när inget personligt erbjudande kvalificerar sig
- Organisera erbjudanden i samlingar med hjälp av samlingskvalificerare (taggar)
- Konfigurera rankningsstrategi - prioritetsbaserad, formelbaserad eller AI-rankad
- Skapa beslutspolicyer som binder placeringar, samlingar, rankningsstrategier och reserverbjudanden
- Godkänn alla erbjudanden innan de kan väljas genom beslut

#### Var alternativen skiljer sig

**För alternativ A (Offer Decisioning):**
Skapa placeringar och erbjudanden som fokuserar på innehållspersonalisering inom varje kanal (t.ex. bannererbjudande för e-posthjälte, sidfotserbjudande för e-post, brödmeddelandeerbjudande). Beslutsprinciper väljer det bästa innehållet för varje placering i meddelandet.

**För alternativ B (Dynamic Channel Selection):**
Skapa beslutsobjekt som representerar varje kanal. Behörighetsreglerna omfattar godkännandekontroller (en profil måste till exempel ha SMS-medgivande för att vara berättigad till SMS-objektet). Rankningen använder kanalinteraktionspoäng eller formelbaserade uttryck.

**För alternativ C (fullständig anpassad):**
Konfigurera två beslutsskikt: en uppsättning beslutsprofiler för kanalval och en separat uppsättning för val av innehåll/erbjudande i den valda kanalen. Båda skikten kräver praktik, erbjudanden, regler för behörighet och rankningsstrategier.

#### Experience League-dokumentation

- [Beslutsledning - översikt](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Skapa placeringar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Skapa beslutsregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Skapa personaliserade erbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Skapa reserverbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Skapa samlingar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Skapa beslut](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Rankningsstrategier](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Fas 4: Utveckla meddelanden

**Programfunktion:** [!DNL AJO]: Meddelanderedigering

I den här fasen konfigureras meddelandeinnehåll för varje kanal och kontaktyta i resan, vilket integrerar beslutsutdata (valt erbjudandeinnehåll) i meddelandemallarna. Varje meddelandeåtgärdsnod på resan kräver redigerat innehåll med rätt kanalyta, personaliseringstoken och erbjuder placeringsintegreringar.

#### Beslut: Innehållsstrategi

Hur ska meddelandeinnehåll skapas för varje kanal?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Mallbaserad | Organisationen har etablerat märkesmallar; enhetlighet är viktigt | Snabbare framtagning, säkerställer enhetlig varumärkeshantering och kan begränsa designflexibiliteten |
| Designa från grunden | Unik kreativ frihet för den här resan - inga befintliga mallar | Full kontroll över designen, längre redigeringstid; använd dra-och-släpp-funktionen i e-post för Designer |
| Importera HTML | Creative-teamet producerar HTML externt. Importera till [!DNL AJO] | Bevarar externt designarbetsflöde; kräver HTML-kompatibilitet med e-post Designer |

#### Beslut: Personalization tillämpningsområde

Vilken nivå av personalisering ska meddelanden omfatta utöver att bestämma utdata?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Grundläggande personalisering (namn, hälsning) | Minimala personaliseringsbehov utöver vad som erbjuds | Simple Handlebars expressions; låg komplexitet |
| Villkorliga innehållsblock | Olika innehållsavsnitt för olika segment eller attribut | Använder regler för dynamiskt innehåll; innehållet varierar beroende på profilattribut eller segmentmedlemskap |
| Komplett personalisering med beslutsintegration | Erbjud placeringar inbäddade i meddelandet i kombination med profilbaserad personalisering | Kombinerar beslutsunderlag med anpassningstoken för verktygsfält; en rikare upplevelse |

#### Information om nyckelkonfiguration

**Gränssnittsnavigering:** Välj kampanj- eller reseåtgärd > Redigera innehåll > Skicka e-post till Designer/kanalredigerare

- Skapa meddelandeinnehåll för varje kanal som används i resan (e-post, SMS, push, i appen)
- Bädda in beslutsunderlag för erbjudanden i meddelandeinnehåll där beslutsvalda erbjudanden ska visas
- Lägg till anpassningsuttryck med hjälp av Handlebars-syntax för profilattribut (till exempel `{{profile.person.name.firstName}}`)
- Konfigurera villkorsstyrt innehåll för segmentspecifika meddelanden
- Skapa återanvändbara innehållsfragment för delade element (sidhuvuden, sidfötter, friskrivningsklausuler)
- Förhandsgranska och testa med exempelprofiler för att verifiera personaliseringsrenderingar korrekt
- Skicka korrekturmeddelanden för granskning av intressenter

#### Var alternativen skiljer sig

**För alternativ A (Offer Decisioning):**
Varje meddelande innehåller placeringar där det valda beslutsinnehållet visas. Meddelandelayouten är konsekvent, men erbjudandeområdet visar dynamiskt det bästa erbjudandet för varje profil.

**För alternativ B (Dynamic Channel Selection):**
Varje kanal har ett eget meddelandeinnehåll som skapas separat. Innehållet är likartat i alla kanaler men anpassat till kanalbegränsningar (e-post, HTML och SMS jämfört med push-meddelandeformat).

**För alternativ C (fullständig anpassad):**
Varje kanal har sitt eget meddelandeinnehåll med inbäddade erbjudandeplaceringar. Både kanalen och erbjudandeinnehållet i den kanalen väljs dynamiskt.

#### Experience League-dokumentation

- [Designa e-postinnehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Lägg till personalisering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Dynamiskt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Leverera erbjudanden i meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Arbeta med innehållsmallar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Arbeta med innehållsfragment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Skapa ett SMS-meddelande](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/create-sms)
- [Utforma ett push-meddelande](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/design-push)

### Fas 5: Resedesign och aktivering

**Programfunktion:** [!DNL AJO]: Journey Orchestration, [!DNL AJO]: Konflikt- och prioritetshantering, [!DNL AJO]: Frekvens- och affärsregler

Den här fasen konfigurerar hela arbetsytan för resan, inklusive startkonfiguration, beslutsnoder som är länkade till konfigurerade beslutsprinciper, villkorsdelningar för kanalroutning (alternativ B/C), meddelandeåtgärdsnoder för varje kanalsökväg, väntenoder mellan kontaktytor, avslutsvillkor, inställningar för konflikt/prioritet och regler för frekvensbegränsning. Denna fas sätter ihop alla tidigare konfigurerade komponenter i det samordnade reseflödet och aktiverar det.

#### Beslut: Återinträdespolicy

Kan profiler återinträda på resan när de har slutförts eller avslutats?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Tillåt återinträde (med nedkylning) | Återkommande resor där profiler kan kvalificeras igen (t.ex. kvartalsvis lojalitetsförnyelse) | Ställ in en nedkylningsperiod (minst 5 minuter) för att förhindra direkt återinträde; profilomstarter från början |
| Ingen återinträde | Engångsresor där varje profil endast ska gå igenom en gång (till exempel introduktion) | Det går inte att ange profilen igen när den har slutförts eller avslutats, vilket är enklare |

#### Beslut: Avslutningskriterier

Under vilka villkor ska en profil tas bort från resan innan den slutförs?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Ändring av målgruppsmedlemskap | Profilen ska avslutas när de lämnar tävlingsgruppen eller anger en nedtryckande målgrupp | Avsluta i realtid vid segmentändring, användbart för &quot;konverterad&quot; eller &quot;avanmäld&quot; |
| Händelseförekomst | En specifik händelse (till exempel köp, avbeställning) ska utlösa avslutning | Avsluta i realtid vid händelse; kräver konfiguration av händelseschema |
| Timeout | Den längsta tiden för resan har gått ut | Standardvärdet är 91 dagar; förhindrar profiler från att finnas oändligt |

#### Beslut: Tidsgräns för resa

Hur lång tid har en profil kvar på resan?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| 91 dagar (max) | Långvariga livscykelresor med utökade vårdsekvenser | Maximal tillåten varaktighet; profiler avslutas efter 91 dagar oavsett |
| Kortare längd | Tidsbundna kampanjer eller säsongsresor | Ange baserat på kundlogik; kortare tidsgräns minskar inaktuella profiler |

#### Beslut: Konflikt- och prioriteringsinställningar

Ska den här resan prioriteras för konfliktlösning med andra resor/kampanjer?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Hög prioritet (70-100) | Kritiska kundresor (kundlojalitet, lojalitet) som ska ha företräde | Högre prioritet vinner när flera kommunikationsformer konkurrerar, använd sparsamt |
| Medium prioritet (30-69) | Standardlivscykelresor | Balanserad prioritet; kan undertryckas av kommunikation med högre prioritet |
| Låg prioritet (0-29) | Kompletterande resor eller informationsresor | Kommer att undertryckas när ni konkurrerar med mer viktig kommunikation |

#### Information om nyckelkonfiguration

**Gränssnittsnavigering:** Resor > Skapa resa

- Skapa resan och konfigurera egenskaper (namn, beskrivning, tidszon, timeout)
- Konfigurera post: Läs målgrupp (för batch) eller händelseutlösare (för realtid)
- Lägg till beslutsnoder som är länkade till konfigurerade beslutspolicyer från fas 3
- Lägg till villkorsdelningar för kanalroutning baserat på beslutsutdata eller profilattribut (alternativ B/C)
- Lägg till meddelandeåtgärdsnoder för varje kanalsökväg som länkar till det redigerade innehållet från fas 4
- Lägg till väntenoder mellan kontaktytor (minst 1 timme för målgruppsläsare)
- Definiera slutkriterier (målgruppsändring, händelse, timeout)
- Tilldela prioritetspoäng för konfliktlösning
- Konfigurera frekvensbegränsning om frekvensbegränsningar för korsningar gäller
- Testa resan i testläge med testprofiler före publicering
- Publicera resan så att den blir levande

#### Var alternativen skiljer sig

**För alternativ A (Offer Decisioning):**
Resans arbetsyta är linjär med beslutsprofiler inbäddade i varje meddelandeåtgärdsnod. Ingen förgrening för kanalval. Erbjudandebeslutet fattas vid meddelanderenderingstid i åtgärdsnoden.

**För alternativ B (Dynamic Channel Selection):**
Efter varje väntesteg lägger du till en villkorsnod som utvärderar kanalurvalskriterier (profilattribut, beslutsutdata eller godkännandestatus). Varje villkorsgren leder till en kanalspecifik meddelanderefod. Inkludera en standardsökväg/en annan sökväg för profiler som inte matchar något villkor.

**För alternativ C (fullständig anpassad):**
Kombinera villkorsnoder för val av kanaler med åtgärdsnoder för beslutsmeddelanden. Vid varje kontaktyta: först avgör ett villkor eller beslut kanalen, och sedan, inom den valda kanalens meddelandeåtgärd, väljer en beslutspolicy det optimala erbjudandet/innehållet.

#### Experience League-dokumentation

- [Skapa en resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Resans egenskaper](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Läs målgruppsaktivitet](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Villkorsaktivitet](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Vänta på aktivitet](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Lägg till ett meddelande i en resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Avslutningskriterier](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [Anställningshantering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Testa din resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [Publicera resan](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)
- [Prioritetspoäng](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Översikt över hantering av konflikter och prioritet](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Frekvensregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)

### Fas 6: Rapportering och övervakning

**Programfunktion:** [!DNL AJO]: Rapportering och prestandaanalys

Denna fas konfigurerar övervakning av rese- och beslutsprestanda genom live-rapporter (under körning) och historiska rapporter (efter slutförande). Beslutsspecifika mätvärden, inklusive fördelning av erbjudanden, reservnivåer och rankningseffektivitet. CJA arbetsyteanalys för djupgående flerkanalsresor och beslutsfattande av ROI-analys kan också användas.

#### Beslut: Rapporteringsdjup

Vilken nivå av rapportanalys krävs?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Endast [!DNL AJO] inbyggda rapporter | Operativ övervakning av leverans- och engagemangsmått | Inbyggda live- och historiska rapporter, ingen ytterligare konfiguration, begränsad till [!DNL AJO]-värden |
| [!DNL AJO] + CJA-analys | Djupgående flerkanalsanalys, beslutseffektivitet, avkastning på resan, kohortanalys | Kräver CJA anslutning och datavy; ger funktioner för attribuering, funnel och kohortanalys |

#### Information om nyckelkonfiguration

**Gränssnittsnavigering:** Resor > Välj resa > Live-rapport / Heltidsrapport

- Övervaka resans liverapport under den inledande körningen för värden för inträde, avslut och per nod
- Prestanda för granskningsbeslut: fördelning av erbjudanden, offertfrekvens, rankningseffektivitet
- När kundresan är klar kan du ta del av historiska rapporter för en komplett analys av funnel
- För CJA-analys: kontrollera att CJA-anslutningen innehåller [!DNL AJO] datauppsättningar (meddelandefeedbackhändelse, e-postspårningshändelse)
- Bygg en CJA-arbetsyta med paneler för kanalblandningsanalys, jämförelse av erbjudanden och konverteringsmöjligheter för resor
- Skapa anteckningar för startdatum för resan och viktiga konfigurationsändringar

#### Experience League-dokumentation

- [Rapport om livesändning på resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Global reserapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Arbeta med Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Analysis Workspace - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Integreringsguide för AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

## Implementeringsöverväganden

Granska följande utkast, vanliga fallgropar, bästa praxis och beslut om kompromisser före och under implementeringen.

### Gardrutor och begränsningar

- Maximalt 500 live-resor per sandlåda - [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Den maximala transporttiden är 91 dagar (global tidsgräns)
- Max 50 aktiviteter per arbetsyta
- Läs målgruppsresor kan bearbeta upp till 20 000 profiler per sekund
- Unitära eventresor stöder upp till 5 000 händelser per sekund per sandlåda
- Max 10 000 godkända anpassade erbjudanden per sandlåda
- Högst 30 praktik per beslut
- Erbjud svarstid för leverans SLA: mindre än 500 ms vid P95 för förfrågningar med en enda omfattning
- AI-rankningsmodeller kräver minst 1 000 konverteringshändelser för utbildning
- Högst 10 kanalytor per kanaltyp per sandlåda
- Väntestegen har en minsta varaktighet på 1 timme för målgruppsläsningar
- Minsta antal återinträde på resan är 5 minuter
- Maximalt 4 000 segmentdefinitioner per sandlåda - [Plattformsskydd](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)

### Vanliga fallgropar

**Beslut returnerar alltid reserverbjudande:** Kontrollera att anpassade erbjudanden har godkänts (inte utkasttillstånd), inom giltighetsdatumintervallet och att berättigandereglerna matchar målprofilernas attribut. Kontrollera att gränsen för erbjudandet inte har nåtts. Testa med en profil som tydligt ska kvalificera sig för ett personaliserat erbjudande.

**Reseutgivare men profiler anges inte:** För målgruppsresor måste du kontrollera att målgruppen har en utvärderad population som är större än noll. För händelseutlösta resor ska du kontrollera händelseschemat, utlösa villkor och att händelser skickas. Kontrollera att målgruppspolicyn för målgruppssammanfogning matchar kundens förväntade sammanfogningspolicy.

**Rankningsformeln används inte korrekt:** Kontrollera att formelsyntaxen är giltig och refererar till tillgängliga profilattribut. Formelfel återgår i tysthet till prioritetsbaserad rankning utan förvarning. Testrankning med profiler som har olika attributvärden för att bekräfta formeln ger den förväntade ordningen.

**Kanalroutning ignorerar samtycke:** Villkorsnoder för kanalval måste innehålla godkännandekontroller. En profil utan SMS-medgivande får inte dirigeras till SMS-sökvägen. Bygg in samtycke i regler för behörighet när du använder beslut för kanalval (alternativ B/C).

**Erbjudandet om räknare för begränsning av antalet tillåtna fel ligger under hög genomströmning:** Erbjudandet om räknare kan ha en fördröjning på några sekunder i scenarier med hög genomströmning. Om det är viktigt med exakt capping ska du använda globala versaler med en buffert eller kombinera med frekvensregler.

**Researbetsytan överskrider 50-aktivitetsgränsen:** Komplexa alternativ C-resor med många kanalgrenar och beslutsnoder kan närma sig 50-aktivitetsgränsen. Förenkla genom att konsolidera villkorslogiken, minska antalet kontaktytor eller dela upp i flera sekventiella resor.

**Edge-beslut returnerar tom personalisering:** Om edge-beslut används för realtidsbeslut kontrollerar du att datastream har tjänsten [!DNL Adobe Journey Optimizer] aktiverad och att beslutsomfånget är korrekt formaterat. Edge beslut är begränsade till profilattribut som är tillgängliga i edge-profilbutiken.

### God praxis

**Börja enkelt och utvecklas:** Börja med alternativ A (fast kanal, dynamiska erbjudanden) för att validera beslutsramverket och gå sedan vidare till Alternativ B eller C när datamängden och organisationens kapacitet ökar.

**Investera i profilberikning:** Beräknade attribut som interaktionspoäng, kanalinställningsindex och AI-benägenhetspoäng för kunder förbättrar beslutskvaliteten dramatiskt. Bygg upp dessa anrikningsattribut innan du konfigurerar komplexa rankningsstrategier.

**Konfigurera alltid reserverbjudanden:** Alla beslutsprinciper måste ha ett reserverbjudande. Utforma reservlösningar som verkligt värdefullt innehåll (inte tomma platshållare) eftersom de betjänar profiler som inte är kvalificerade för något personaliserat erbjudande.

**Testa med olika profiler:** Använd testläge med profiler som representerar olika berättigandesökvägar, kanalinställningar och attributkombinationer. Kontrollera att alla möjliga vägar och beslut fungerar korrekt före publicering.

**Övervaka reservfrekvenser som hälsomått:** Ett högt reserverbjudande indikerar att reglerna för behörighet är för restriktiva eller att erbjudandekatalogen inte täcker tillräckligt många profilsegment. Ange en reservfrekvens under 20 % för välkonfigurerad beslutsfattande.

**Använd innehållsfragment för enhetlighet över flera kanaler:** Skapa delade innehållsfragment (sidhuvuden, sidfötter, friskrivningsklausuler, blockering av prenumerationer) för att upprätthålla varumärkets enhetlighet i e-post, SMS och push-meddelanden under resan.

**Konfigurera avslutningskriterier proaktivt:** Definiera avslutningskriterier för konverteringshändelser (till exempel köp, registrering) så att profiler som slutför den önskade åtgärden tas bort från resan omedelbart i stället för att fortsätta att ta emot meddelanden.

**Tilldela meningsfulla prioritetspoäng:** Tilldela prioritetspoäng baserat på affärsmässiga konsekvenser när du kör flera resor och kampanjer. Resor med högt värde för lagring bör ha högre prioritet än informationskommunikation.

### Avvecklingsbeslut

Se följande kompromisser för att få information om implementeringsalternativen.

#### Besluta komplexitet jämfört med time to market

Mer sofistikerad beslutsfattande (alternativ C med AI-rankning) ger högre personalisering men kräver betydligt mer konfiguration, datainställning och testningstid.

- **Alternativ A/B prioriterar:** Snabbare driftsättning, enklare testning, lägre löpande hanteringskostnader
- **Alternativ C prioriterar:** Maximal personalisering, kontinuerlig AI-driven optimering, högsta möjliga engagemang
- **Rekommendation:** Börja med alternativ A eller B för inledande start. Samla in prestandadata och bygg profilanrikningsattribut parallellt. Växla till alternativ C när du har minst 1 000 konverteringshändelser för AI-rankningsutbildning och en välfylld erbjudandekatalog.

#### Statisk förgrening jämfört med beslut för kanalval

Kanalval kan genomföras med enkla noder för resevillkor (utvärdering av profilattribut direkt) eller via beslutsramen (där kanalerna modelleras som beslutsposter med behörighet och rankning).

- **Statiska villkorsnoder ger fördelar:** Enkelhet, genomskinlighet, enkel felsökning. Bäst när logiken för kanalval är okomplicerad (om det till exempel finns en push-token och den senaste push-funktionen öppnas inom 30 dagar, använd push, annars e-post).
- **Beslutsbaserat kanalval prioriterar:** Centraliserad hantering, AI-optimeringspotential, möjlighet att utveckla rangordningslogik utan att ändra arbetsytan. Bäst när kanalvalet är komplext och bör förbättras över tid.
- **Rekommendation:** Använd statiska villkorsnoder för alternativ B när kanalurvalskriterierna är enkla och väldefinierade. Använd beslutsbaserat kanalval när du vill att AI ska optimera kanalvalet över tid eller när logiken för kanalval är tillräckligt komplex för att dra nytta av centraliserad hantering av kvalificering och rankning.

#### Erbjud detaljrikedom jämfört med kataloghantering

En stor, detaljerad erbjudandekatalog med många målinriktade erbjudanden ger en mer exakt personalisering, men kräver mer hantering. En mindre katalog med större behörighet är enklare att hantera men mindre personaliserad.

- **Stor katalog (många specifika erbjudanden) prioriterar:** Högre precision för personalisering, mer relevanta markeringar för olika målgrupper, lägre reservfrekvenser
- **Små kataloger (färre breda erbjudanden) prioriterar:** Enklare hantering, snabbare konfiguration, enklare testning, lägre risk för överblivna erbjudanden
- **Rekommendation:** Börja med 5-15 personaliserade erbjudanden plus ett reserv per beslut. Lägg till fler erbjudanden samtidigt som du observerar vilka segment som får de vanligaste reserverbjudandena. Använd samlingskvalificerare för att ordna erbjudanden efter kategori, nivå eller produktlinje för hanterbar tillväxt.

#### Prioritetsbaserad eller AI-rankad beslutsfattande

Prioritetsbaserad rankning är deterministisk och transparent. AI-rankad beslutsfattande optimeras automatiskt men kräver utbildningsdata och är mindre transparent.

- **Prioritetsbaserad rankning prioriterar:** Förutsägbarhet, genomskinlighet, omedelbar driftsättning, inga krav på utbildningsdata
- **AI-rankade beslutsfavoriter:** Kontinuerlig optimering, datadriven markering, möjlighet att upptäcka icke-uppenbara tillhörigheter mellan erbjudande och profil
- **Rekommendation:** Använd prioritetsbaserad eller formelbaserad rankning för inledande distribution. Övergå till AI-rankat beslutsfattande när du har samlat in minst 1 000 konverteringshändelser och vill gå från regelbaserad till modellbaserad optimering.

## Relaterad dokumentation

Följande resurser innehåller ytterligare information om de funktioner som används i det här användningsmönstret.

### Resesamordning

- [Kom igång med resor](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Skapa en resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Resans egenskaper](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Läs målgruppsaktivitet](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Allmänna händelser](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Elevkvalificeringshändelser](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [Villkorsaktivitet](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Vänta på aktivitet](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Lägg till ett meddelande i en resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Avslutningskriterier](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [Anställningshantering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Testa din resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [Publicera resan](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)

### Beslutsledning

- [Beslutsledning - översikt](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Skapa placeringar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Skapa beslutsregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Skapa personaliserade erbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Skapa reserverbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Skapa samlingar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Skapa samlingskvalificerare](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [Skapa beslut](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Rankningsstrategier](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [Leverera erbjudanden i meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### Kanalkonfiguration

- [Kom igång med e-postkonfiguration](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Delegera underdomäner](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Skapa IP-pooler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [Planer för IP-värmare](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Inställningar för e-postyta](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Konfigurera SMS-kanal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Konfigurera kanal för push-meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Framtagning och personalisering av meddelanden

- [Skapa ett e-postmeddelande](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [Designa e-postinnehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Lägg till personalisering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization syntax](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Dynamiskt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Arbeta med innehållsmallar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Arbeta med innehållsfragment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Förhandsgranska och testa ditt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### Hantering av konflikter, prioritet och frekvens

- [Översikt över hantering av konflikter och prioritet](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Prioritetspoäng](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Identifiera potentiella konflikter](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [Resegotypning och skiljeförfarande](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)
- [Frekvensregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)

### Målgrupper och segmentering

- [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Direktuppspelningssegmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Edge segmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Målgruppssammansättning](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Profile Query Language referens](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### Rapportering och analys

- [Rapport om livesändning på resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Global reserapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Arbeta med Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Integreringsguide för AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [CJA - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Analysis Workspace - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

### Profil och identitet

- [Översikt över kundprofiler i realtid](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [Översikt över identitetstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Översikt över kopplingsprofiler](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [Översikt över beräknade attribut](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Översikt över AI för kunder](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### Datastyrning och samtycke

- [Översikt över dataförvaltning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Samtycke i Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [Hantera undertryckningslista](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Skyddsräcken

- [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Garantier för kundprofiler i realtid](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Garantier för identitetstjänst](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)
