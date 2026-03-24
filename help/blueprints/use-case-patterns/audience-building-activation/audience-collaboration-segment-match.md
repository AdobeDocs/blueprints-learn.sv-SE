---
title: Audience Collaboration
description: Lär dig hur du delar och matchar målgruppssegment i sandlådor eller organisationer med hjälp av segmentmatchning.
solution: Real-Time Customer Data Platform, Experience Platform
exl-id: 7014849c-5e32-4ec3-a531-c0e8ce896f44
source-git-commit: 27f7e230982807ec70ca96af7f737944a6588f27
workflow-type: tm+mt
source-wordcount: '6232'
ht-degree: 0%

---

# Audience Collaboration

Den här guiden innehåller en omfattande implementeringsreferens för målgruppssamarbete med hjälp av [!DNL Segment Match] i [!DNL Real-Time CDP] och [!DNL Adobe Experience Platform]. Det är utformat för lösningsarkitekter, marknadsföringsteknologer och implementeringstekniker som behöver dela och matcha målgruppssegment över sandlådor eller organisationer på ett sekretesssäkert sätt.

Använd den här planen för att förstå tillgängliga metoder, utvärdera avvägningar och navigera [!DNL Adobe Experience League] för detaljerade konfigurationsinstruktioner.

Med [!DNL Segment Match] kan två eller flera [!DNL Experience Platform]-organisationer (eller sandlådor i en organisation) samarbeta med målgruppsdata genom att dela information om segmentmedlemskap utan att visa underliggande PII. Deltagarna kan uppskatta överlappning, dela målgrupper och aktivera matchade profiler till efterföljande destinationer.

## Använd ärendeöversikt

Organisationer behöver i allt högre grad samarbeta om målgruppsdata med partners, dotterbolag eller andra affärsenheter, samtidigt som de har strikt sekretesskontroll. Målgruppssamarbete tillgodoser detta behov genom att aktivera säker segmentdelning via [!DNL Segment Match] - en funktion i [!DNL Real-Time CDP] som gör det möjligt för två eller flera [!DNL Experience Platform] organisationer (eller sandlådor) att utbyta information om målgruppsmedlemskap med hjälp av hashade, sekretesssäkra identifierare.

Affärsscenariot omfattar vanligtvis en organisation (avsändaren) som har skapat ett värdefullt målgruppssegment och vill dela det med en partnerorganisation (mottagaren) för gemensam målinriktning, undertryckning eller berikning. Före delning kan båda parter uppskatta målgruppsöverlappning för att bedöma värdet. När den delas kan den mottagande organisationen aktivera den matchade målgruppen via sina egna destinationer.

Det här mönstret skiljer sig från vanlig målgruppsaktivering eftersom det används mellan organisationer eller sandlådor i stället för till externa annons- eller marknadsföringsmål. Den skiljer sig också från dataröljen eller samarbetsplattformar från andra leverantörer, eftersom den fungerar internt i Adobe-ekosystemet med hjälp av identitetsinfrastrukturen [!DNL Experience Platform].

## Viktiga verksamhetsmål

Följande affärsmål stöds av det här användningsmönstret.

### Skaffa nya kunder

Utöka kundbasen med riktade kampanjer, lookalike-målgrupper och optimering av betalda medier. Målgruppssamarbete gör det möjligt för organisationer att hitta nya pooler för potentiella kunder genom att matcha deras segment mot målgrupper, identifiera högvärdesöverlappning och nå nya kunder genom gemensam aktivering.

- **KPI:er:** Nya kunder, Kundanskaffningskostnad, Prospekt/Leadkonvertering
- [Skaffa nya kunder](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

### Minska anskaffningskostnaden

Förbättra målinriktningens effektivitet, hindra befintliga kunder från att värva kampanjer och optimera medieinvesteringarna. Genom att dela motsatssegment mellan organisationer och affärsenheter kan team undvika slöseri med utgifter för redan konverterade kunder och fokusera budgeten på verkligt nya potentiella kunder.

- **KPI:er:** Kundanskaffningskostnad, kostnad per lead, effektivitet
- [Minska anskaffningskostnaden](/help/blueprints/business-objectives/cost-efficiency/reduce-customer-acquisition-cost.md)

### Optimera marknadsföringsbudgeten och avkastningen

Förbättra avkastningen på marknadsföringsinvesteringar genom bättre målgruppsanpassning, attribuering, dämpande av målgrupper och budgettilldelning. [!DNL Segment Match] gör det möjligt att undertrycka målgrupper över flera organisationer och att målinrikta flera personer samtidigt, vilket minskar antalet dubbletter och förbättrar precisionen.

- **KPI:er:** Kostnadsbesparingar, Kundanskaffningskostnad, Inkrementella intäkter
- [Optimera marknadsföringsbudgeten och avkastningen](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)

## Exempel på taktiska användningsfall

- **Målgruppsmatchning för utgivare/annonsörer** - Ett varumärke delar sitt värdefulla kundsegment med en medieutgivare för att beräkna överlappning och rikta in matchade användare med personaliserade annonser, vilket förbättrar kampanjrelevansen utan att visa PII.
- **Undertryckande av flera varumärken inom ett holdingföretag** - Flera varumärken inom en överordnad organisation delar kundsegment för att hindra befintliga kunder hos systervarumärken från att värva kampanjer, vilket minskar bortslösade annonskostnader.
- **Målgruppsanpassning i detaljhandelsnätverk** - En återförsäljare delar inköpsbaserade segment med CPG:s varumärkespartners, vilket gör det möjligt för varumärkena att inrikta sig på beprövade köpare i återförsäljarens medienätverk med högre konverteringsgrad.
- **Identifiering av målgrupper för samarbetspartners** - Två icke-konkurrerande varumärken utvärderar målgruppsöverlappning för att utvärdera partnerpotential innan en gemensam kampanj startas, och använder överlappningsberäkning för att validera målgruppsjustering.
- **Segmentdelning för datasamarbete** - Organisationer i ett datakoncernsegment hashas för att utöka målgruppsanpassningen samtidigt som de upprätthåller integritetsefterlevnad och datastyrning.
- **Målgruppsfederation med flera sandlådor** - Ett globalt företag delar målgruppssegment över regionala sandlådor för att möjliggöra enhetlig kundanpassning över flera marknader samtidigt som regionala krav på dataresistens respekteras.
- **Lojalitetsprogram - partneraktivering** - En lojalitetskoalition delar lojalitetsskiktsegment med deltagande handlare så att varje partner kan erbjuda nivåanpassade kampanjer till den delade kundbasen.
- **Mätnings- och attribueringssamarbete** - En annonsörer delar ett konverteringssegment med en mediepartner så att partnern kan mäta kampanjens effektivitet genom att matcha exponerade användare mot konverterare.

## Nyckeltal för prestanda

Följande nyckeltal hjälper till att mäta framgången i implementeringar av målgruppssamarbete.

| KPI | Beskrivning | Mätningsmetod |
| --- | --- | --- |
| Överlappningsfrekvens för målgrupp | Procentandel profiler i det delade segmentet som matchar mellan avsändare och mottagare | [!DNL Segment Match] - rapport för överlappningsberäkning |
| Matchad målgruppsstorlek | Antal profiler som matchats och är tillgängliga för aktivering | [!DNL Segment Match] resursstatus och antal målgrupper |
| Nytt kundförvärv från matchade målgrupper | Net-new-kunder förvärvade genom kampanjer med matchade segment | Konverteringsspårning för kampanjer med matchade målgrupper |
| Kundvärvningskostnadsminskning | Minska kostnaden per förvärv när ni använder matchade målgrupper jämfört med bred målinriktning | Kampanjkostnadsanalys som jämför matchade och oöverträffade målgruppsprestanda |
| Undertrycksbesparingar | Medieutgifter som sparats genom att undertrycka kända kunder från värvningskampanjer | Jämförelse av utgifter för media för förhands-/efterhandsundertryckning |
| Kampanjprestanda - lyft | Förbättrad konverteringsgrad, klickfrekvens eller engagemang för kampanjer med matchade målgrupper | A/B-test som jämför matchade målgruppskampanjer jämfört med kontroll |
| Time to Collaboration | Förfluten tid från start av segmentdelning till aktiveringsberedskap | [!DNL Segment Match] tidsstämplar för arbetsflöde |

## Använd skiftlägesmönster

Det här användningsexemplet följer målgruppsmönstret Collaboration.

Dela och matcha målgruppssegment över sandlådor eller organisationer med hjälp av [!DNL Segment Match].

**Funktionskedja:** Segmentmarkering > Matcha konfiguration > Överlappningsberäkning > Målgruppsdelning > Aktivering

## Tillämpningar

Följande program används i det här fallmönstret.

- **[!DNL Real-Time CDP]** - Tillhandahåller funktionen [!DNL Segment Match] för sekretesssäker målgruppsdelning, målgruppsutvärdering för att skapa segment och målaktivering för nedladdning av matchade målgrupper.
- **[!DNL Adobe Experience Platform]** - Tillhandahåller den grundläggande datainfrastrukturen, inklusive identitetsmatchning, profilunifiering, datastyrning och medgivande som [!DNL Segment Match] är beroende av.

## Foundationsfunktioner

Följande grundläggande funktioner måste finnas för det här användningsmönstret. För varje funktion anger statusen om den vanligtvis är obligatorisk, antas vara förkonfigurerad eller inte tillämplig.

| Funktionen Foundation | Status | Vad måste finnas på plats | Experience League referens |
| --- | --- | --- | --- |
| Administration och styrning | Obligatoriskt | Både avsändar- och mottagarorganisationer måste ha sandlådor med lämpliga roller och behörigheter. Användare som hanterar [!DNL Segment Match] måste ha behörighet att visa och dela segment, konfigurera anslutningar och hantera partnerflöden. ABAC-principer ska konfigureras för att styra vilka användare som kan initiera och acceptera segmentresurser. | [Översikt över åtkomstkontroll](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Datamodellering och förberedelse | Antagen på plats | XDM-scheman för profiler och händelser måste finnas med de obligatoriska fältgrupperna. Profil- och händelsedatamängder måste skapas och aktiveras för [!DNL Real-Time Customer Profile]. Datamodellen måste ha stöd för de identitetsnamnutrymmen som används för segmentmatchning (vanligen hashad-e-post eller hashad-telefon). | [Översikt över XDM-systemet](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home) |
| Datakällor och samling | Antagen på plats | Kunddata måste aktivt flöda in i [!DNL Experience Platform] via konfigurerade datakällor (SDK, källanslutningar, batchintag). Profiler måste fyllas i med de identitetstyper som används för [!DNL Segment Match] (t.ex. hashad e-post). | [Källor - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home) |
| Konfiguration av identitet och profil | Obligatoriskt | Identitetsnamnutrymmen måste konfigureras för de identifierare som används vid segmentmatchning. Både avsändaren och mottagaren måste använda kompatibla ID-namnutrymmen. Sammanfogningsprinciper måste konfigureras för att profilerna ska kunna sammanfogas korrekt. Regler för identitetslänkning bör fastställas för att säkerställa korrekt profilupplösning. | [Översikt över identitetstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home) |
| Målgruppsdefinition och segmentering | Obligatoriskt | Source-målgrupper måste definieras och utvärderas innan de kan delas via [!DNL Segment Match]. Målgrupper ska skapas med [!DNL Segment Builder] eller [!DNL Audience Composition] där grupputvärderingen är slutförd. Endast grupputvärderade målgrupper är berättigade till delning av [!DNL Segment Match]. | [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home) |

## Stödfunktioner

Följande funktioner förstärker det här användningsmönstret, men behövs inte för att köra kärnan.

| Stödfunktioner | Status | Varför det spelar någon roll | Experience League referens |
| --- | --- | --- | --- |
| Skapande av beräknat/härlett attribut | Rekommenderad | Beräknade attribut, som livstidsvärde, poängpoäng eller produkttillhörighet, kan skapa mer exakta segment för delning. Högkvalitativa indatasegment leder till mer värdefullt målgruppssamarbete. | [Översikt över beräknade attribut](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| Livscykelhantering för data | Rekommenderad | Regler för samtycke och datalagring säkerställer att delade segment följer sekretesslagstiftningen. Datauppsättningens förfalloprinciper hjälper till att hantera livscykeln för mottagna målgruppsdata. Medgivandetvång förhindrar delning av profiler som har avanmält sig. | [Översikt över livscykelhantering av avancerade data](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| Dataanvändningsetiketter och -tillämpning | Ingår | Datastyrningsprinciper måste utvärderas innan segment delas för att säkerställa regelefterlevnad. Etiketter för identitetsfält och profilattribut avgör vad som kan delas. Styrning förhindrar att oauktoriserade data inkluderas i segmentaktier. | [Datastyrningsöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home) |
| Övervakning och observerbarhet | Rekommenderad | Genom att övervaka [!DNL Segment Match]-delningsprocessen, överlappa uppskattningsjobb och aktiveringsdataflöden kan du upptäcka fel tidigt. Aviseringar kan konfigureras för resursfel eller oväntat låga matchningsfrekvenser. | [Översikt över Insikter om observabilitet](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| Rapportering och analys | Rekommenderad | Genom att mäta resultatet för kampanjer som använder matchade målgrupper valideras värdet av samarbetet. [!DNL Customer Journey Analytics] kan analysera matchande målgruppskampanjresultat jämfört med kontrollgrupper. | [CJA - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## Programfunktioner

I den här planen används följande funktioner från programfunktionskatalogen. Funktioner mappas till implementeringsfaser i stället för till numrerade steg.

### [!DNL Real-Time CDP]

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Målgruppsutvärdering | Fas 1: Val och förberedelse av segment | Utvärdera segmentmedlemskap med batchutvärdering för att skapa målgrupper som ska delas via [!DNL Segment Match] |
| Målgruppssammansättning | Fas 1: Val och förberedelse av segment | Du kan också komponera härledda målgrupper (rankning, delning, exkludering, berika) för att skapa mer målinriktade segment för delning |
| Verkställande av samtycke och styrning | Fas 2: Matcha konfiguration och styrning | Använd policyer för dataanvändning och samtyckesinställningar innan ni delar segment för att säkerställa regelefterlevnad |
| Audience Activation | Fas 5: Matchad Audience Activation | Publicera matchade målgrupper som tagits emot via [!DNL Segment Match] till externa mål för mål eller undertryckning |
| Målkonfiguration | Fas 5: Matchad Audience Activation | Konfigurera anslutningar till externa destinationer där matchade målgrupper ska aktiveras |

## Förutsättningar

- Både avsändar- och mottagarorganisationer har [!DNL Real-Time CDP] etablerat med [!DNL Segment Match]-berättigande
- [!DNL Segment Match] har aktiverats för de organisationer eller sandlådor som deltar i samarbetet
- Partneranslutningen har upprättats mellan avsändaren och mottagarorganisationerna i användargränssnittet för [!DNL Segment Match]
- Båda organisationerna använder kompatibla ID-namnutrymmen (t.ex. har båda e-postmeddelanden konfigurerade)
- Source målgrupper har definierats och utvärderats med populationer som inte är noll
- Datastyrningsprinciper konfigureras och dataanvändningsetiketter tillämpas på relevanta datauppsättningar och fält
- Användare på båda sidor har de behörigheter som krävs för att hantera [!DNL Segment Match] anslutningar, resurser och feeds
- Samtyckesfält fylls i med profiler för att möjliggöra samtyckesbaserad filtrering före delning

## Implementeringsalternativ

Följande alternativ beskriver olika strategier för att implementera målgruppssamarbete med [!DNL Segment Match]. Välj det alternativ som bäst passar er organisationsstruktur och era samarbetskrav.

### Alternativ A: Direktsegmentdelning (en-till-en)

Det här alternativet passar bäst för bilaterala partnerskap mellan två specifika organisationer, som en annonsörer och en utgivare, eller två varumärken i ett sammarknadsföringsavtal.

**Så här fungerar det:**

I en direkt 1:1-segmentdelning väljer avsändarorganisationen en eller flera utvärderade målgrupper, initierar en delning med en viss partnerorganisation och mottagaren accepterar delningen. Överlappningsberäkningen körs automatiskt för att visa båda parter procentandelen och volymen för matchade profiler innan delningen är klar.

Avsändaren definierar vilka ID-namnutrymmen som ska användas för matchning och markerar de segment som ska delas. Mottagaren granskar den inkommande resursen, godkänner den och den matchade målgruppen blir tillgänglig i sin målgruppslista för aktivering nedströms. Endast hash-kodad identitetsöverlappning byts ut - inga underliggande PII- eller profilattributdata överskrider organisatoriska gränser.

Detta tillvägagångssätt är okomplicerat och ger båda parter full kontroll. Avsändaren väljer exakt vad som ska delas och med vem, och mottagaren kan välja att acceptera eller avvisa varje resurs.

**Viktiga överväganden:**

- Kräver explicit konfiguration av partneranslutning mellan de två organisationerna
- Båda organisationerna måste komma överens om identitetsnamnutrymmen för matchning
- Överlappningsberäkning ger transparens före åtagande
- Varje resurs måste hanteras och övervakas individuellt

**Fördelar:**

- Enkelt, välförstått bilateralt arbetsflöde
- Fullständig transparens genom överlappningsberäkning före delning
- Detaljkontroll - avsändaren väljer exakt vilka segment som ska delas
- Sekretesssäker - endast hash-kodade identifierare används för matchning
- Mottagaren kan välja att acceptera eller avvisa delningar

**Begränsningar:**

- Kan inte skalas upp effektivt när man samarbetar med många partners samtidigt
- Varje koppling kräver separat konfiguration och hantering av anslutningen
- Resurskonfigurationen måste upprepas för varje nytt segment

**Experience League:**

- [Översikt över segmentmatchning](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/overview)
- [Felsökning av segmentmatchning](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/troubleshooting)

### Alternativ B: Segmentdistribution med flera partner (ett till många)

Det här alternativet passar bäst för organisationer som behöver dela segment med flera partners samtidigt, t.ex. ett nätverk för att dela inköpsbaserade segment med flera varumärkesannonsörer eller ett holdingbolag som distribuerar segment till dotterbolag.

**Så här fungerar det:**

I en 1:N-distributionsmodell upprättar avsändarorganisationen [!DNL Segment Match] anslutningar med flera partnerorganisationer och delar samma eller olika segment med var och en. Avsändaren hanterar en portfölj med partneranslutningar och kan selektivt dela olika målgruppssegment med olika partner baserat på relation och användningsfall.

Varje partneranslutning fungerar oberoende av varandra - uppskattningar av överlappning, godkännande av delning och aktivering hanteras per partner. Avsändaren kan styra vilka segment som varje partner får, vilket möjliggör olika samarbetsstrategier (t.ex. får premiumpartners mer detaljerade segment, standardpartner får bredare).

Den här metoden använder samma underliggande [!DNL Segment Match]-mekanism som alternativ A, men använder den i stor skala med ett operativt ramverk för hantering av flera samtidiga partnerskap.

**Viktiga överväganden:**

- Kräver robusta operativa processer för hantering av flera partnerskap
- Styrningspolicyn måste ta hänsyn till att samma segment ska delas med flera externa parter
- Varje partner kan använda olika identitetsnamnutrymmen, vilket kräver flexibel konfiguration
- Överlappningsfrekvensen varierar beroende på partner, vilket kräver utvärdering per partner

**Fördelar:**

- Skalar målgruppssamarbetet över ett ekosystem av partners
- Differentierade delningsstrategier per partner
- Centraliserad hantering av alla utgående segmentaktier från en organisation
- Varje partnerskap upprätthåller oberoende styrning och medgivande

**Begränsningar:**

- Driftskomplexiteten ökar för varje ytterligare partner
- Övervakning och felsökning måste göras per partner
- Styrningsgranskning krävs för varje ny partneranslutning
- Partners kan inte se varandras data eller dela status

**Experience League:**

- [Översikt över segmentmatchning](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/overview)

### Alternativ C: Förening av målgrupper över sandlådor

Det här alternativet passar bäst för stora företag med flera [!DNL Experience Platform] sandlådor (t.ex. regionala sandlådor, varumärkesspecifika sandlådor eller miljöspecifika sandlådor) som måste dela målgruppssegment över interna gränser utan att flytta rådata.

**Så här fungerar det:**

I stället för att dela mellan olika organisationer används [!DNL Segment Match] för att dela målgruppssegment mellan sandlådor inom samma organisation. Detta gör att ett globalt marknadsföringsteam kan bygga upp ett segment i en central sandlåda och dela det med regionala sandlådor, eller tillåter varumärkesspecifika sandlådor att dela undertryckningslistor med varandra.

Arbetsflödet speglar den direkta segmentdelningen (alternativ A) men arbetar inom organisationsgränsen. Anslutningar från sandlåda till sandlåda upprättas via [!DNL Segment Match], och segment delas med samma sekretesssäkra matchningsprocess. Den mottagande sandlådan hämtar den matchande målgruppen som en ny målgrupp som kan aktiveras via sina egna lokalt konfigurerade mål.

Det här tillvägagångssättet är särskilt värdefullt när krav på dataresistens förhindrar att rådata flyttas mellan regioner, men målgruppssamarbete är tillåtet.

**Viktiga överväganden:**

- Kräver [!DNL Segment Match]-berättigande som stöder delning över sandlådor
- Identitetsnamnutrymmen måste vara konsekventa över sandlådor
- Sammanslagningsprinciper i varje sandlåda kan lösa profiler på olika sätt, vilket kan påverka matchningsfrekvenser
- Styrningsprinciper tillämpas oberoende per sandlåda

**Fördelar:**

- Möjliggör samarbete utan att rådata flyttas över sandlådegränserna
- Stöder krav på datamedstånd och regional efterlevnad
- Utnyttjar befintlig infrastruktur för organisationsidentitet
- Enklare granskning av styrning eftersom delning sker inom samma organisation

**Begränsningar:**

- Kräver konsekvent konfiguration av identitetsnamnrymd i alla sandlådor
- Matchningsfrekvenser beror på sammanslagningsprincipens konsekvens mellan sandlådor
- Avgör inte behovet av samarbete mellan olika organisationer
- Sandbox Tooling kan behövas för att synkronisera schema och konfiguration

**Experience League:**

- [Översikt över segmentmatchning](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/overview)
- [Översikt över sandlådor](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/home)

### Jämförelse av alternativ

I följande tabell jämförs de tre implementeringsalternativen över de viktigaste kriterierna.

| Kriterier | Alternativ A: Direkt segmentdelning | Alternativ B: Distribution för flera partner | Alternativ C: Cross-Sandbox Federation |
| --- | --- | --- | --- |
| Bäst för | Bilaterala partnerskap | Samarbete i ekosystem | Intern delning över sandlådor |
| Komplex | Lågt | Högt | Medelsvåra: |
| Antal partners | 1 | Många | Interna sandlådor |
| Styrning | Lågt | Hög (granskning per partner) | Medium (inom organisationen) |
| Operativ förvaltning | Enkel | Kräver partnerhanteringsramverk | Måttlig |
| Stöd för datalagring | Ej tillämpligt | Beroende på partnerplats | Stark |
| Kräver | Inställningar för partneranslutning | Flera partneranslutningar | Korssandlåda [!DNL Segment Match] |

### Välj rätt alternativ

Använd följande riktlinjer för beslut för att välja lämplig implementeringsmetod:

1. **Samarbetar du med en extern organisation eller inom din egen organisation?**
   - Extern organisation: fortsätt till fråga 2.
   - Inom din egen organisation (över alla sandlådor): välj **Alternativ C** (Cross-Sandbox Federation).

2. **Hur många externa partner samarbetar du med?**
   - En partner: välj **Alternativ A** (direktsegmentdelning).
   - Flera partners: välj **Alternativ B** (Distribution av flera partner).

3. **Har du begränsningar för datastorlek som förhindrar att rådata flyttas mellan regioner?**
   - Ja: välj **Alternativ C** oavsett om partners är interna eller externa - använd delning mellan sandlådor för att behålla dataplatsen.

## Implementeringsfaser

I följande faser beskrivs den kompletta implementeringsprocessen för målgruppssamarbete med [!DNL Segment Match].

### Fas 1: Markera och förbered segment

**Programfunktion:** [!DNL Real-Time CDP]: Målgruppsutvärdering, [!DNL Real-Time CDP]: Målgruppssammansättning

I den här fasen definieras och utvärderas målgruppssegment som delas via [!DNL Segment Match]. Källsegmenten måste utvärderas fullständigt med populationer som inte är noll innan de kan väljas för delning. Den här fasen omfattar även tillvalssammansättning för att förfina segment innan de delas.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>
>**Beslut: Målgruppsdefinitionsmetod**
>
>Hur ska källmålgrupperna för delning skapas?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Segment Builder (segmentregler) | Standardmålgruppsdefinitioner baserade på profilattribut, händelser eller segmentmedlemskap | Stöder batch-, streaming- och edge-utvärdering; flexibelt för att definiera kriterier |
>| Målgruppssammansättning | Härledda målgrupper som behöver rangordnas, delas upp, exkluderas eller berika operationer i befintliga segment | Stöder endast grupputvärdering; begränsat till 10 kompositionskanvaser per sandlåda |
>| Sammansatt målgrupp | Målgrupper som skapats från externa datalagerfrågor utan inmatning av data till [!DNL Experience Platform] | Kräver [!DNL Federated Audience Composition] tillstånd; data finns kvar på lagerstället |

>[!NOTE]
>
>**Beslut: Målgruppsutvärderingsmetod**
>
>[!DNL Segment Match] kräver grupputvärderade målgrupper. Hur ska utvärderingen schemaläggas?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Schemalagd batch (dag) | Standardfall där det räcker med daglig målgruppsuppdatering | Standardutvärderingsschema, enklast att hantera |
>| On demand-batch | Ad-hoc-delning där ni omedelbart vill dela den senaste målgruppen | Kräver manuell utlösare, användbart för tidskänsliga samarbeten |
>| Anpassat schema | Specifika timingkrav som är anpassade efter partneraktiveringsfönster | Konfigurera ett anpassat kroniskt schema, mer komplext men exakt |

**Gränssnittsnavigering:** Kund > Publiker > Skapa målgrupp > Skapa regel (för [!DNL Segment Builder]) eller Disponera målgrupp (för [!DNL Audience Composition])

**Information om nyckelkonfiguration:**

- Definiera målgruppskriterier med hjälp av profilattribut, beteendehändelser och/eller segmentmedlemskap
- Kontrollera att målgruppen använder en sammanfogningsprincip som är kompatibel med de identitetsnamnutrymmen som används för [!DNL Segment Match]
- Verifiera att målgruppspopulationen inte är noll efter utvärdering
- Använd undertryckningsregler för att exkludera profiler som inte ska delas (t.ex. profiler som har avanmält sig från datadelning)

**Var alternativen skiljer sig:**

**För alternativ A (direktsegmentsresurs):**
Förbered de specifika segment som du tänker dela med din partner. Fokusera på kvalitet framför kvantitet - strukturera segment som ger ett tydligt värde till partnerskapet.

**För alternativ B (Multi-Partner Distribution):**
Skapa en segmentportfölj som kan delas med olika partner. Överväg att skapa partnerspecifika segment om olika partners behöver olika målgruppsdefinitioner. Använd konsekventa namnkonventioner för att hantera segment mellan partnerskap.

**För alternativ C (federering mellan sandlådor):**
Kontrollera att källmålgrupperna i den sändande sandlådan använder identitetsnamnutrymmen som finns i den mottagande sandlådan. Kontrollera att sammanfogningsprinciper är justerade i sandlådor.

**Experience League-dokumentation:**

- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Översikt över Audience Composition](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Utvärderingsmetoder](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home#evaluation-methods)
- [Profile Query Language referens](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### Fas 2: Konfigurera matchning och styrning

**Programfunktion:** [!DNL Real-Time CDP]: Kräver samtycke och styrning

Den här fasen upprättar anslutningen [!DNL Segment Match] mellan organisationer eller sandlådor, konfigurerar de identitetsnamnutrymmen som används för matchning och ser till att datastyrningsprinciper tillåter delning. Myndighetskontrollen fungerar som en policyport som måste rensas innan segmentdata delas.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>
>**Beslut: Identitetsnamnrymd för matchning**
>
>Vilket ID-namnutrymme ska användas för att matcha profiler mellan avsändare och mottagare?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Hash-kodad e-post (SHA-256) | Båda organisationerna samlar in e-postadresser och kan hacka dem konsekvent | Den vanligaste matchningsnyckeln; höga matchningsfrekvenser för konsumentbruk; båda sidorna måste använda samma hash-algoritm |
>| Hash-kodat telefonnummer | E-post är inte alltid tillgängligt, men telefonnummer är | Lägre täckning än e-post på många marknader; användbart för målgrupper som sätter mobilen först |
>| Anpassat namnutrymme (t.ex. hash-kodat lojalitets-ID) | Organisationer delar ett gemensamt ID för lojalitet eller medlemsprogram | Högsta matchningsfrekvens för kända delade kundbaser; kräver befintlig infrastruktur för delade ID |
>| Flera namnutrymmen | Det är viktigt att maximera matchningsfrekvensen och båda organisationerna har flera konsekventa identifierare | Ökar matchningsfrekvenser men ökar komplexiteten. Varje namnutrymme måste konfigureras separat |

>[!NOTE]
>
>**Beslut: Granskning av datastyrning**
>
>Vilka kontroller av företagsstyrning måste slutföras innan delning?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Utvärdering av standardstyrning | Vanligt användningsexempel med standardetiketter och standardpolicyer för dataanvändning | Utvärdera marknadsföringsåtgärden &quot;Export to Third Party&quot; (Exportera till tredje part) mot datauppsättningsetiketter; åtgärda eventuella överträdelser innan delning |
>| Bättre styrning med samtyckesfiltrering | Delning med externa partner där samtycke måste verifieras uttryckligen | Lägg till samtyckesbaserad filtrering för att exkludera profiler utan medgivande (t.ex. samtycke.share.val = &#39;n&#39;); striktare men säkrare |
>| Intern styrningsgranskning | Delning mellan sandlådor inom samma organisation | Lägre krav på styrning eftersom data ligger inom organisatoriska gränser, men ändå verifiera etiketter för dataanvändning |

**Gränssnittsnavigering:** Kund > Målgrupper > Segmentmatchning > Partneranslutningar

**Information om nyckelkonfiguration:**

- Upprätta en partneranslutning genom att utbyta anslutningsidentifierare mellan avsändar- och mottagarorganisationer
- Konfigurera de identitetsnamnutrymmen som ska användas för matchning på båda sidor
- Kör utvärdering av datahanteringsprincip mot marknadsföringsåtgärden som är kopplad till segmentdelning
- Verifiera att fält för samtycke fylls i i på profiler och att profiler utan medgivande är uteslutna
- Granska dataanvändningsetiketter på datauppsättningar och schemafält som ingår i resursen

**Var alternativen skiljer sig:**

**För alternativ A (direktsegmentsresurs):**
Upprätta en enda partneranslutning. Konfigurera identitetsnamnutrymmen med din specifika partner. Översynen av styrformerna fokuserar på de bilaterala förbindelserna.

**För alternativ B (Multi-Partner Distribution):**
Upprätta och hantera flera partneranslutningar. Varje partner kan kräva en separat granskning av styrningen. Dokumentera styrningens godkännande för varje partnerskap. Överväg att skapa en checklista för styrning som effektiviserar partnerintroduktionen.

**För alternativ C (federering mellan sandlådor):**
Upprätta sandbox-to-sandbox-anslutningar inom organisationen. Styrningen är vanligtvis enklare eftersom delning sker internt. Kontrollera att identitetsnamnutrymmen är konsekventa över sandlådor.

**Experience League-dokumentation:**

- [Översikt över segmentmatchning](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/overview)
- [Översikt över dataförvaltning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Politiska åtgärder](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/enforcement/overview)
- [Samtycke och inställningar](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)

### Fas 3: Uppskattningsöverlappning

**Programfunktion:** [!DNL Real-Time CDP]: Målgruppsutvärdering (för beräkning av överlappning)

Den här fasen kör överlappningsberäkningen mellan avsändarens segment och mottagarens profilbas. Överlappningsberäkning ger båda parter den förväntade matchningsvolymen och procentandelen innan de förbinder sig till hela segmentresursen, vilket möjliggör välgrundade beslut om värdet av samarbetet.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>
>**Beslut: Överlappningströskel för att fortsätta**
>
>Vilken miniminivå för överlappning motiverar att du fortsätter med hela segmentresursen?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Ingen minimitröskel | Förberedande partnerskap eller när någon överlappning ger värde | Passar för inledande samarbete där du testar relationen |
>| Lågt tröskelvärde (1-5 %) | Storskalig målgruppssamverkan där även små överlappningar representerar stora volymer | Gemensamt för relationer mellan förläggare och annonsörer med stora målgruppsbaser |
>| Medium-tröskel (5-20 %) | Standardpartnerskap där meningsfull överlappning förväntas | Normalt för sammarknadsföring eller samarbete inom samma bransch |
>| Högt tröskelvärde (20 %+) | Partnerskap där stark målgruppsanpassning är en förutsättning | Gemensamt för lojalitetskoalitioner eller nära integrerade varumärkespartnerskap |

**Gränssnittsnavigering:** Kund > Publiker > Segmentmatchning > Delar > Uppskattningsöverlappning

**Information om nyckelkonfiguration:**

- Markera de segment som ska ingå i överlappningsberäkningen
- Granska överlappningsrapporten med matchat profilantal och procent
- Dela resultaten av överlappningsberäkningen med intressenter på båda sidor för godkännande
- Dokumentera överlappningsstatistik som en grund för mätning av samarbetets effektivitet
- Om överlappningen ligger under det tillåtna tröskelvärdet bör du överväga att justera segmentdefinitioner eller konfigurationen för identitetsmatchning innan du fortsätter

**Experience League-dokumentation:**

- [Översikt över segmentmatchning](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/overview)

### Fas 4: Dela målgrupper

**Programfunktion:** [!DNL Real-Time CDP]: Målgruppsutvärdering (för delningskörning)

Den här fasen kör den faktiska segmentresursen från avsändare till mottagare. Avsändaren initierar delningen för de valda segmenten och mottagaren accepterar den inkommande resursen. När den matchade målgruppen godkänts visas den i mottagarens målgruppslista som en ny målgrupp tillgänglig för aktivering längre fram i kedjan.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>
>**Beslut: Dela riktning**
>
>Vilken är delningsmodellen för det här samarbetet?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Envägsdelning (avsändare till mottagare) | Asymmetriskt partnerskap där endast en part tillhandahåller målgruppsdata | Den enklaste modellen; avsändarresurser, mottagaraktiveringar; gemensamma i relationer mellan annonsörer och utgivare |
>| Dubbelriktad resurs | Båda parter kan dra nytta av att dela målgrupper med varandra | Båda organisationerna fungerar som avsändare och mottagare samtidigt; kräver två delade konfigurationer; gemensamma i partnerskap för sammarknadsföring |

>[!NOTE]
>
>**Beslut: Dela uppdateringsgräns**
>
>Hur ofta ska den delade målgruppen uppdateras med det uppdaterade segmentmedlemskapet?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Engångsdelning | Testa samarbetet eller för en viss kampanj med en fast målgrupp | Enklast; inget löpande underhåll; publiken blir stulen över tiden |
>| Återkommande resurs (justerad mot batchutvärdering) | Pågående partnerskap där målgruppsmedlemskapet ändras och behöver hållas uppdaterat | Kräver övervakning av uppdateringsstatus, vilket är vanligast för produktionssamarbete |

**Gränssnittsnavigering:** Kund > Publiker > Segmentmatchning > Delningar > Skapa resurs (avsändare) eller Acceptera resurs (mottagare)

**Information om nyckelkonfiguration:**

- Avsändaren markerar de segment som ska delas och initierar delningen med den konfigurerade partnern
- Mottagaren granskar informationen om den inkommande resursen (segmentnamn, beräknad storlek, identitetsnamnutrymmen som används)
- Mottagaren accepterar delningen för att skapa den matchande målgruppen i sandlådan
- Verifiera att den matchande målgruppen visas i mottagarens målgruppslista med den förväntade populationen
- Bekräfta att den matchade målgruppen har rätt etikett för styrningsspårning

**Var alternativen skiljer sig:**

**För alternativ A (direktsegmentsresurs):**
Utför en enda delning med din partner. Övervaka delningens status och verifiera den matchande målgruppen på mottagarsidan.

**För alternativ B (Multi-Partner Distribution):**
Utför delningar för varje partner oberoende av varandra. Spåra delningsstatus i alla partnerskap. Överväg att starta en mellanlagringsresurs för att hantera bearbetningsbelastningen.

**För alternativ C (federering mellan sandlådor):**
Utför resursen mellan sandlådor. Den matchande målgruppen visas i den mottagande sandlådans målgruppslista. Kontrollera att den mottagande sandlådan har de målkonfigurationer som krävs för aktivering nedströms.

**Experience League-dokumentation:**

- [Översikt över segmentmatchning](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/overview)
- [Felsökning av segmentmatchning](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/troubleshooting)

### Fas 5: Aktivera matchande målgrupper

**Programfunktion:** [!DNL Real-Time CDP]: Målkonfiguration, [!DNL Real-Time CDP]: Audience Activation

Den här fasen aktiverar den matchande målgruppen (på mottagarsidan) till externa mål för målgruppsanpassning, inaktivering eller nedströms användning. Den matchande målgruppen behandlas som vilken annan målgrupp som helst i mottagarens sandlåda och kan aktiveras via standardarbetsflödet för målaktivering.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>
>**Beslut: Måltyp för matchad målgrupp**
>
>Var ska den matchande publiken aktiveras?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Advertising destinationer (Google, Meta, Trade Desk) | Använda matchande målgrupper för målinriktning och undertryckande av annonser | Kräver målanslutning och autentisering, enligt målspecifika hastighetsbegränsningar och formatkrav |
>| Lagringsmål för molnet (S3, Azure, GCS) | Exportera matchade målgrupper som filer för användning i externa system | Stöder anpassning av filformat; batchexportschema krävs; flexibelt för nedladdning |
>| Mål för CRM/marknadsföring och automatisering | Förbättra CRM-poster eller skapa automatiserade arbetsflöden för marknadsföring med matchande målgruppsdata | Kräver fältmappning till CRM-schema, vilket är användbart för sälj- och marknadsföringsjustering |
>| Personalization destinationer (webb, app) | Använda matchande målgruppsmedlemskap för anpassning av webbplatser | Kräver kantutvärdering av den matchande målgruppen eller aktiveringen av direktuppspelning. Latensen varierar beroende på mål |

>[!NOTE]
>
>**Beslut: Aktiveringsschema**
>
>Hur ofta ska den matchade målgruppen exporteras till målet?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Inkrementell export varje dag | Standardaktivering med regelbundna uppdateringar | Exportera endast ändrade profiler, lägre datavolym, vanligaste för pågående kampanjer |
>| Fullständig export varje dag | Destinationer som kräver en komplett målgruppsfil varje gång | Högre datavolym; säkerställer att destinationen har fullständig målgruppsstatus; vissa destinationer kräver full export |
>| On-demand-aktivering | Ad-hoc-kampanjer startar eller tidsberoende aktiveringar | Manuell utlösare; kringgår schemalagd gräns; endast tillgängligt för batchdestinationer |

**Gränssnittsnavigering:** Anslutningar > Destinationer > Katalog (för målkonfiguration) eller Bläddra > Välj mål > Aktivera målgrupper (för aktivering)

**Information om nyckelkonfiguration:**

- Konfigurera målanslutningen med lämpliga autentiseringsuppgifter
- Mappa profilattribut från den matchade målgruppen till målfält (identitetsfält, profilattribut, segmentmedlemskap)
- Konfigurera exportschemat (inkrementellt kontra fullständigt, dagligen kontra anpassat)
- Övervaka aktiveringsdataflödet för att bekräfta att matchade målgruppsprofiler har exporterats
- Verifiera aktiveringsmått (exporterade profiler, poster misslyckades) i målövervakningsvyn

**Var alternativen skiljer sig:**

**För alternativ A (direktsegmentsresurs):**
Mottagaren aktiverar den matchande målgruppen genom sitt standardarbetsflöde för destinationer. Ingen specialkonfiguration behövs utöver den normala målaktiveringen.

**För alternativ B (Multi-Partner Distribution):**
Varje mottagarorganisation aktiverar matchade målgrupper oberoende av varandra via sina egna destinationer. Avsändaren kan inte se aktiveringen på mottagarsidan.

**För alternativ C (federering mellan sandlådor):**
Den mottagande sandlådan måste ha egna målkonfigurationer. Destinationer kan inte delas mellan sandlådor. Kontrollera att den mottagande sandlådan har upprättat nödvändiga målanslutningar.

**Experience League-dokumentation:**

- [Översikt över destinationer](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [Målkatalog](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [Övervaka dataflöden för mål](https://experienceleague.adobe.com/en/docs/experience-platform/dataflows/ui/monitor-destinations)
- [Aktiveringsskydd](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)

## Implementeringsöverväganden

Granska följande överväganden före och under implementeringen för att undvika vanliga problem och optimera målgruppssamarbetet.

### Gardrutor och begränsningar

- [!DNL Segment Match] använder hash-kodade identifierare för matchning - ingen PII överskrider organisationsgränserna. Se [Översikt över segmentmatchning](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/overview).
- Endast grupputvärderade målgrupper kan delas via [!DNL Segment Match]. Strömmande och kantutvärderade segment måste konverteras till grupputvärdering innan de kan delas.
- Max 4 000 segmentdefinitioner per sandlåda gäller både käll- och mottagningssegment. Se [Segmenteringsskyddsutkast](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails).
- Exaktheten för överlappningsberäkning beror på volymen för matchade identifierare. Små målgrupper kan visa mindre exakta uppskattningar.
- Aktiveringsskydd gäller för matchade målgrupper på samma sätt som andra målgrupper - maximalt 100 dataflöden per mål. Se [Aktiveringsskyddsutkast](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails).
- Sammansatta målgrupper utvärderas enligt ett batchschema och är begränsade till 10 kompositionscanvases per sandbox. Se [Målgruppsprofiler](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/guardrails).

### Vanliga fallgropar

- **Inkonsekvent ID-hashning mellan avsändare och mottagare:** Om båda organisationerna hash-kodar e-postadresser men använder olika hash-algoritmer, normaliseringsregler eller salt-värden kommer matchningsfrekvenserna att ligga nära noll. Båda sidor måste komma överens om den exakta hash-specifikationen (t.ex. SHA-256 om nedsänkt, trimmad e-post) innan anslutningen upprättas.
- **Delning av målgrupper utan styrningsgranskning:** Om du initierar en segmentresurs utan att utvärdera dataanvändningsprinciper kan det leda till efterlevnadsöverträdelser. Utvärdera alltid styrningspolicyn mot marknadsföringsåtgärden&quot;Exportera till tredje part&quot; innan segment delas med externa organisationer.
- **Låga matchningsfrekvenser p.g.a. öppningar i identitetstäckningen:** Om avsändarens målgrupp primärt identifieras av ECID (anonym cookie) men det matchande namnområdet hashas-e-post, kommer matchningsfrekvensen att vara mycket låg eftersom anonyma profiler inte har e-postadresser. Kontrollera att källmålgrupperna har tillräcklig täckning för det konfigurerade matchande identitetsnamnområdet.
- **Förlorar att acceptera resursen på mottagarsidan:** Den delade målgruppen visas inte i mottagarens målgruppslista förrän delningen accepteras explicit. Koordinera med mottagaren för att säkerställa att materialet accepteras i tid, särskilt för tidskänsliga kampanjer.
- **Inaktuella matchade målgrupper på grund av felaktig matchning av utvärderingsschema:** Om avsändarens källmålgrupp utvärderas dagligen men uppdateringen [!DNL Segment Match] körs varje vecka, kanske den matchade målgruppen på mottagarsidan inte speglar det senaste medlemskapet. Justera utvärderingen och dela uppdateringskoder.

### God praxis

- Upprätta ett formellt datadelningsavtal mellan organisationer innan du konfigurerar [!DNL Segment Match]. Detta bör omfatta tillåtna användningsfall, krav på datastyrning, medgivandeskyldigheter och avslutningsförfaranden.
- Använd överlappningsberäkning som ett valideringsverktyg före varje större kampanj - kör uppskattningar innan du förbinder dig att se till att den matchade målgruppen uppfyller minimikraven för storlek och kvalitet.
- Använd beskrivande namnkonventioner på delade segment som innehåller partnernamnet, användningsfallet och datumet (t.ex.&quot;PartnerX_HighValue_Suppression_2026Q1&quot;) för att behålla tydligheten i olika organisationer.
- Övervaka matchningsfrekvenser över tid. Minskade matchningsfrekvenser kan tyda på minskad identitetstäckning, problem med datakvaliteten eller förändringar i partnerns kundbas.
- Segmentera målgrupper som ska exkludera profiler utan att matchande ID-namnutrymme har fyllts i. Detta förbättrar procentsatserna för matchningsfrekvensen och ger exaktare uppskattningar av överlappning.
- För dubbelriktade partnerskap anger du tydligt ägarskap för segmentunderhåll och uppdateringsscheman för att undvika förvirring om vilken organisation som ansvarar för uppdateringarna.

### Avvecklingsbeslut

>[!NOTE]
>
>**Avvikelse: Matchningsfrekvens jämfört med sekretesskontroll**
>
>Om du använder fler identitetsnamnutrymmen (hashad e-post, hash-kodad telefon, enhets-ID) för att matcha ökar matchningsfrekvensen, men utökar ytan för eventuell omidentifiering. Om du använder färre namnutrymmen (endast hash-kodad e-post) får du ett starkare sekretesskydd, men det kan minska den matchande målgruppens storlek.
>
>- **Flera namnutrymmen gynnar:** Högre matchningsfrekvens, större matchade målgrupper, mer värdefullt för kampanjanpassning
>- **Enkelt namnutrymme prioriterar:** Starkare sekretessposition, enklare granskning av styrning, lägre efterlevnadsrisk
>- **Rekommendation:** Börja med ett enda namnutrymme (hash-kodad e-post är det vanligaste) och lägg bara till ytterligare namnutrymmen om matchningsfrekvensen inte räcker till för användningsfallet. Dokumentera bedömningen av integritetseffekten för varje namnområde som läggs till.

>[!NOTE]
>
>**Avvikelse: Segmentgranularitet jämfört med operativ enkelhet**
>
>Genom att dela många detaljerade, extremt målinriktade segment med en partner blir det mer flexibelt att rikta kampanjer, men det ökar komplexiteten för både avsändare och mottagare. Delning av färre, bredare segment förenklar hanteringen men minskar precisionen för målinriktning.
>
>- **Detaljerade segment gynnar:** Exakt målinriktning, differentierade kampanjer, högre relevans
>- **Stora segment gynnar:** Enklare hantering, färre resurser att övervaka, lägre operativ overhead
>- **Rekommendation:** Börja med ett litet antal värdefulla segment (2-5) för ett nytt partnerskap. Öka granulariteten i takt med att partnerskap och operativa processer inrättas. Använd namnkonventioner och dokumentation för att hantera komplexiteten allt eftersom antalet segment ökar.

>[!NOTE]
>
>**Avvikelse: Uppdatera frekvens jämfört med bearbetningskostnad**
>
>Att uppdatera delade målgrupper oftare håller den matchande målgruppen aktuell men ökar belastningen på behandlingen och kan konsumera mer licenskapacitet. Mindre vanliga uppdateringar minskar kostnaderna men gör att den matchande publiken blir stulen.
>
>- **Vanliga uppdateringsfavoriter:** Aktuellt målgruppsmedlemskap, större kampanjrelevans, bättre undertryckningskvalitet
>- **Ovanliga uppdateringar prioriterar:** Lägre bearbetningskostnader, enklare övervakning, minskad licensförbrukning
>- **Rekommendation:** Daglig uppdatering passar för de flesta samarbete i produktionen. För tidskänsliga användningsfall (t.ex. blixtförsäljning, händelsebaserade kampanjer) bör du överväga en ny utvärdering och delning omedelbart innan kampanjen lanseras.

## Relaterad dokumentation

Följande resurser innehåller ytterligare information om de funktioner som används i det här användningsmönstret.

### [!DNL Segment Match]

- [Översikt över segmentmatchning](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/overview)
- [Felsökning av segmentmatchning](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/troubleshooting)

### Segmentering och målgrupper

- [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Översikt över Audience Composition](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Profile Query Language referens](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)
- [Direktuppspelningssegmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Edge segmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### Identitet och profil

- [Översikt över identitetstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Översikt över namnutrymmen för identiteter](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/namespaces)
- [Översikt över kopplingsprofiler](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [Översikt över kundprofiler i realtid](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)

### Datastyrning och samtycke

- [Översikt över dataförvaltning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Översikt över etiketter för dataanvändning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/labels/overview)
- [Politiska åtgärder](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/enforcement/overview)
- [Samtycke och inställningar](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)
- [Fältgruppen för samtycke och inställningar](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)

### Destinationer och aktivering

- [Översikt över destinationer](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [Målkatalog](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [Övervaka dataflöden för mål](https://experienceleague.adobe.com/en/docs/experience-platform/dataflows/ui/monitor-destinations)

### Datamodellering och schema

- [XDM - systemöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Grundläggande om schemakomposition](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)

### Administration och åtkomstkontroll

- [Översikt över åtkomstkontroll](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home)
- [Översikt över sandlådor](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/home)

### Övervakning och iakttagbarhet

- [Översikt över aviseringar](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Översikt över Insikter i observationer](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)

### Skyddsräcken

- [Garantier för kundprofiler i realtid](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Skyddsritningar för segmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/guardrails)
- [Aktiveringsskydd](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)

### Självstudiekurser

- [Skapa ett schema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/union-schema)
- [Aktivera en datauppsättning för profil](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/enable-for-profile)
