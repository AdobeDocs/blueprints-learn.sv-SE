---
title: B2B-analys
description: Lär dig hur du inkluderar information på B2B-kontonivå i kanalövergripande kundreseanalyser.
solution: Customer Journey Analytics, Real-Time Customer Data Platform
exl-id: 9d576e5c-cbd2-4c60-a6b0-88f8b8b963b4
source-git-commit: ccfd8c987a0090ca690e15a4bd89f4d96ec9c01f
workflow-type: tm+mt
source-wordcount: '7528'
ht-degree: 0%

---

# B2B-analys

Den här guiden innehåller en omfattande implementeringsreferens för B2B-kontoanalys med [!DNL Customer Journey Analytics] ([!DNL CJA]) B2B edition och [!DNL Real-Time Customer Data Platform] ([!DNL RT-CDP]) B2B edition. Det är utformat för lösningsarkitekter, marknadsföringsteknologer och implementeringstekniker som behöver införliva B2B-information på kontonivå i en flerkanalsanalys av kundresan.

Det täcker alla användbara metoder för kontobaserad analys, från platta kontostrukturer till komplexa globala kontohierarkier, med vägledning om när varje alternativ ska väljas. Planen omfattar dataanslutningar till B2B, konfiguration av kontodatavyn, analys av arbetsytan och publicering av instrumentpaneler.

B2B Analytics utökar de vanliga [!DNL CJA]-funktionerna med kontobaserade anslutningar, B2B-specifika behållare (konto, globalt konto, säljprojekt, inköpsgrupp) och kontonivårapportering. Tack vare den här funktionen kan organisationer analysera marknads- och säljengagemanget på kontonivå, spåra affärsmöjligheterna, mäta om köpgrupperna är fullständiga och attribuera intäkter till kontaktytor för marknadsföring över längre B2B-säljcykler.

## Använd ärendeöversikt

B2B-organisationer står inför en grundläggande utmaning när det gäller analys: deras kunder är inte enskilda personer utan konton som består av flera intressenter, inköpsgrupper och möjligheter. Vanliga personbaserade analyser kan inte besvara frågor som&quot;Vilka konton är mest engagerade?&quot;,&quot;Hur fullständiga är våra inköpsgrupper?&quot; eller&quot;Vilka kontaktytor för marknadsföring driver utvecklingen av affärsmöjligheterna?&quot;

B2B Analytics åtgärdar detta genom att utnyttja [!DNL CJA] B2B edition för att skapa kontobaserade analytiska vyer som kombinerar beteendedata på personnivå med konto, möjlighet och grupper. [!DNL RT-CDP] B2B edition tillhandahåller den underliggande kontouppställningen för enhetlighet och B2B-identitetsupplösning som matar analysskiktet. Tillsammans gör dessa lösningar det möjligt för organisationer att bygga flerkanalsanalyser på kontonivå, korrelera marknadsföringsinnehållet med pipeline-utvecklingen och leverera åtgärdbara insikter till både marknadsförings- och säljteam.

Målgruppen är bl.a. verksamhetsteam inom B2B-marknadsföring, chefer inom efterfrågegenerering, analytiker av intäktsverksamhet och säljchefer som behöver synlighet vad gäller engagemang på kontonivå och pipeline-hälsa.

## Viktiga verksamhetsmål

Följande affärsmål stöds av det här användningsmönstret.

### Förbättra analyser och rapporter

Förbättra rapporteringsmöjligheterna för snabbare och mer åtgärdbara marknadsföringsinsikter med hjälp av enhetliga instrumentpaneler och självbetjäningsverktyg. Med B2B-analys kan organisationer konsolidera interaktionsdata på kontonivå från flera källor till en enda analysmiljö, vilket ger en överblick över hur marknadsföringsprogram påverkar pipeline och intäkterna.

**KPI:er:** Effektivitet, produktivitet

[Läs mer om hur man förbättrar analyser och rapporter](/help/blueprints/business-objectives/analytics-insights/improve-analytics-reporting.md)

### Möjliggör datadrivet beslutsfattande

Ge teamen möjlighet att använda självbetjäningsanalyser, kundinsikter i realtid och AI-baserade prognoser som guidar strategin. Analysanalys på kontonivå ger marknadsförings- och säljteam de data som behövs för att prioritera konton, optimera engagemangsstrategier och anpassa sig till olika försäljningsmöjligheter.

**KPI:er:** Effektivitet, produktivitet

[Läs mer om att möjliggöra datadrivet beslutsfattande](/help/blueprints/business-objectives/analytics-insights/enable-data-driven-decision-making.md)

### Förbättra kvalificering och konvertering av leads

Öka ledningskvaliteten och snabba upp utvecklingen av pipeline genom poängsättning, vårdande och personaliserad uppföljning. CJA B2B edition har utökade 13-månaders kontosökningsfönster som är särskilt utformade för B2B-säljcykler, vilket möjliggör korrekt multitouch-attribuering under hela kundresan.

**KPI:er:** Effektivitet, Inkrementell intäkt

[Läs mer om hur du förbättrar kvalificering och konvertering av leads](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)

## Exempel på taktiska användningsfall

Följande scenarier visar hur mönstret kan användas i praktiken.

- **Analys av kontointeraktion** - Mät och rangordna konton utifrån deras samlade interaktion via webben, e-post, händelser och innehållsinteraktioner för att identifiera konton med hög återgivning för försäljningsuppföljning
- **Kontroll av kundgruppens fullständighet** - Analysera inköpsgruppdisposition mellan konton för att identifiera luckor i rolltäckning och prioritera lead-hämtning för ofullständiga inköpsgrupper
- **Försäljningsförmedlingens korrelation** - Korrelera marknadsföringsengagemangsdata med säljprojektsfasens förlopp för att förstå vilka kampanjer och kontaktytor som driver utvecklingen framåt
- **B2B-attribuering med flera beröringspunkter** - Använd attribueringsmodeller med 13 månaders svarstid för att attribuera kontaktytor för marknadsföring över hela B2B-köpresan från första beröring till sluten
- **Mappning av kontoresa** - Visualisera den flerkanaliga kontoresan från inledande medvetenhet till skapande och stängning av affärsmöjligheter, identifiera gemensamma vägar och friktionspunkter
- **Kampanjpåverkan på pipeline** - Mät hur specifika kampanjer påverkar genereringen av kontopipeline, möjligheterna och intäkterna
- **Förlopp för gruppengagemang** - Spåra hur poängen för gruppengagemang utvecklas över tid och korrelera tröskelvärdena för engagemang med affärsmöjligheterna
- **Kontobaserad innehållsprestanda** - Analysera vilka innehållsresurser och ämnen som fungerar med specifika kontosegment, branscher eller grupper för inköp
- **Kontrollpaneler för sälj- och marknadsföringsjustering** - Skapa delade instrumentpaneler som ger både marknadsförings- och säljteam en enhetlig vy över kontoengagemang, pipeline-hälsa och intäktsattribuering
- **Kontosegmentering för aktivering** - Skapa B2B-segment baserat på kontoanalys (till exempel&quot;mycket engagerade konton utan öppna möjligheter&quot;) och publicera dem för aktivering längre fram i kedjan

## Nyckeltal för prestanda

Följande nyckeltal hjälper till att mäta hur bra det här användningsmönstret är.

| KPI | Beskrivning | Mätningsmetod |
| --- | --- | --- |
| Resultat för kontoengagemang | Sammanställd engagemangsmätning för alla kontakter i ett konto | Beräknade mätvärden som kombinerar webbbesök, e-postinteraktioner, närvaro vid händelse och innehållsnedladdningar på kontonivå |
| Slutlighet för inköpsgrupp | Procent av obligatoriska roller som fyllts i i en inköpsgrupp | Förhållandet mellan fyllda roller och totalt antal nödvändiga roller per inköpsgrupp, spårade över tid |
| Pipeline påverkad av marknadsföring | Intäkter i pipeline som har påverkats av marknadsföringsaktiviteter | Affärsmöjlighet där associerade kontokontakter har marknadsföringskontaktytor i attribueringsfönstret |
| Konverteringsgrad konto till affärsmöjlighet | Procent av engagerade konton som genererar kvalificerade möjligheter | Konton med affärsmöjligheter fördelade på totala konton under en angiven period |
| Genomsnittlig längd för avtalscykel | Tid från första marknadsföringsberöring till slutvunnen | Genomsnittlig varaktighet från första tilldelade kontaktyta till stängningsdatum för affärsmöjlighet |
| Marknadsattribueringsintäkt | Intäkter från kontaktytor på marknaden | Intäkter från slutna affärsmöjligheter med marknadsföringsåtgärder, fördelade på attribueringsmodell |
| Kontointervall och genomgång | Antal kontaktpersoner per målkonto | Unika kontakter med marknadsföringsinteraktioner per konto, jämfört med det totala antalet kända kontakter |
| Innehållsengagemang med inköpsroll | Engagemangsmått segmenterade efter inköpsgruppsroll | Sidvisningar, nedladdningar och tidsåtgång per person/roll inom inköpsgrupper |

## Använd skiftlägesmönster

**B2B-analys**

Inkludera information på B2B-kontonivå i kundreseanalys över flera kanaler.

**Funktionskedja:** B2B-dataanslutning > Kontodatavy Configuration > Workspace Analysis > Dashboard Publishing

## Tillämpningar

Följande program används för att implementera det här användningsmönstret.

- **[!DNL Customer Journey Analytics]B2B edition** - Tillhandahåller kontobaserade anslutningar, B2B-specifika datavybehållare, arbetsyteanalys på kontonivå, inköpsgruppsanalys, affärsmöjlighetsanalys, B2B-segmentering och B2B-attribuering med utökade sökningsfönster
- **[!DNL Real-Time CDP]B2B edition** - Tillhandahåller B2B-datamappningen inklusive enhetlig kontoprofil, B2B-identitetsupplösning, B2B-schemaklasser (konto, säljprojekt, inköpsgrupp) och [!DNL Marketo Engage]-integrering för inmatning av B2B-interaktionsdata

## Foundationsfunktioner

Följande grundläggande funktioner måste finnas för det här användningsmönstret. För varje funktion anger statusen om den vanligtvis är obligatorisk, antas vara förkonfigurerad eller inte tillämplig.

| Funktionen Foundation | Status | Vad måste finnas på plats | Experience League referens |
| --- | --- | --- | --- |
| Administration och styrning | Obligatoriskt | Sandlådan har konfigurerats med [!DNL CJA] B2B edition- och [!DNL RT-CDP] B2B edition-berättiganden. Roller har etablerats för datatekniker, analytiker och användare av marknadsföringsåtgärder med tillgång till [!DNL CJA] och B2B-datamodellen. | [Översikt över sandlådor](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/home) |
| Datamodellering och förberedelse | Obligatoriskt | B2B XDM-scheman konfigurerade med B2B-klasser: XDM Business Account, XDM Business Opportunity, XDM Business Account Person Relation, XDM Business Opportunity Person Relation och XDM Business Marketing List-medlemmar. Fältgrupper för kontoattribut, affärsmöjlighetsfaser och inköpsgruppsroller måste definieras. Datauppsättningar skapade och aktiverade för profil. | [Systemöversikt för XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [B2B edition scheman](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b) |
| Datakällor och samling | Obligatoriskt | B2B-datakällor är anslutna, vanligtvis via [!DNL Marketo Engage]-källkopplingen eller [!DNL Salesforce] CRM-källkopplingen. Kontoposter, poster för affärstillfällen, relationer mellan människor och konton samt beteendehändelser måste flöda in i AEP datamängder. [!DNL Web SDK] eller [!DNL Marketo]-integrering måste hämta beteendehändelser med kontoassociationen. | [Källor - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home), [Marketo Engage Connector](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) |
| Konfiguration av identitet och profil | Obligatoriskt | B2B-identitetsmatchning konfigurerad för att matcha relationer från människa till konto. Konto-ID, ID för person ([!DNL Marketo] lead-ID eller CRM-kontakt-ID) och identiteter mellan enheter (ECID, e-post) måste vara länkade. Identitetsdiagrammet måste ha stöd för många-till-många-mappning från människa till konto som är inbyggd i B2B-datamodeller. | [Översikt över identitetstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [B2B-identitetsupplösning](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b) |
| Målgruppsdefinition och segmentering | Antagen på plats | Målgruppsdefinitioner på kontonivå bör vara tillgängliga om B2B-segment publiceras från [!DNL CJA] tillbaka till AEP för aktivering. I fall där bara analyser används är detta inte en strikt förutsättning, men rekommenderas för segmentbaserad analys. | [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home) |

## Stödfunktioner

Följande funktioner förstärker det här användningsmönstret, men behövs inte för att köra kärnan.

| Stödfunktioner | Status | Varför det spelar någon roll | Experience League referens |
| --- | --- | --- | --- |
| Skapande av beräknat/härlett attribut | Rekommenderad | Beräknade attribut för kontoprofiler (t.ex. totalpoäng, dagar sedan senaste aktivitet, antal affärstillfällen) förbättrar de analytiska dimensioner som är tillgängliga i [!DNL CJA] för kontonivåanalys. | [Översikt över beräknade attribut](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| Livscykelhantering för data | Rekommenderad | B2B-datauppsättningar, särskilt beteendehändelsedata från [!DNL Marketo Engage], kan växa snabbt. Förfallotidsprinciper för datauppsättningar hjälper till att hantera lagring och säkerställa att kraven på datalagring uppfylls. | [Avancerad livscykelhantering för data](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| Dataanvändningsetiketter och -tillämpning | Rekommenderad | B2B-data innehåller ofta känslig affärsinformation (kontraktsvärden, konkurrensinformation). Dataanvändningsetiketter och styrningsprinciper säkerställer att dessa data används på rätt sätt i arbetsflödena för analys och aktivering. | [Datastyrningsöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home) |
| Övervakning och observerbarhet | Rekommenderad | B2B-källanslutningar ([!DNL Marketo], [!DNL Salesforce]) kräver övervakning för matningshälsa. Övervakning av anslutningshälsa i [!DNL CJA] säkerställer dataaktualitet för analyser. Varningsregler för misslyckade inmatningar förhindrar inaktuella instrumentpaneler. | [Översikt över Insikter om observabilitet](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| Rapportering och analys | Ingår | Mönstret är i sig självt ett analysmönster. Den här funktionen är till sin natur inkluderad eftersom kärnfunktionskedjan tillhandahåller rapporterings- och analysfunktioner. | [CJA - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## Programfunktioner

I den här planen används följande funktioner från programfunktionskatalogen. Funktioner mappas till implementeringsfaser i stället för till numrerade steg.

### [!DNL Customer Journey Analytics] B2B edition

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Kontobaserad anslutning | Fas 1: B2B-dataanslutning | Konfigurera anslutningar med Konto eller Global Account som primär identifierare för analys på organisationsnivå |
| Konfiguration av B2B-datavy | Fas 2: Konfiguration av kontodatavy | Definiera datavyer med B2B-specifika behållare (konto, globalt konto, möjlighet, inköpsgrupp) tillsammans med vanliga person-, session- och händelsebehållare |
| Workspace-analys på kontonivå | Fas 3: Workspace Analysis | Bygg frihandsanalyser med kontonivådimensioner, mätvärden och B2B-behållare för insikter om kundresan på organisationsnivå |
| Köpgruppsanalys | Fas 3: Workspace Analysis | Analysera inköpsgruppens sammansättning, engagemang och framsteg genom inköpsbeslutsprocessen |
| Affärsmöjlighetsanalys | Fas 3: Workspace Analysis | Spåra affärsmöjligheterna genom säljfaser i funnel och korrelera med data om marknadsföringsengagemang |
| B2B-segmentering | Fas 3: Workspace Analysis | Skapa segment med B2B-behållare för filtrerad analys på kontonivå |
| B2B Attribution | Fas 3: Workspace Analysis | Använd attribueringsmodeller med utökade 13-månaders kontosökningsfönster för analys av B2B-säljcykel |
| Skapande av beräknade mått | Fas 3: Workspace Analysis | Definiera beräknade mätvärden för nyckeltal inom B2B, t.ex. kontointeraktion, fullständighet för köpgrupper och påverkan på försäljningsförloppet |
| Dashboard &amp; Scorecard Publishing | Fas 4: Dashboard Publishing | Skapa och dela instrumentpaneler och mobilstyrkort för ledande marknads- och säljchefer |
| Audience Publishing | Fas 4: Dashboard Publishing | Publicera [!DNL CJA]-definierade kontobaserade målgrupper tillbaka till AEP för aktivering nedströms |

### [!DNL Customer Journey Analytics] - standardfunktioner

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Dataanslutning | Fas 1: B2B-dataanslutning | Bind AEP B2B-datauppsättningar till [!DNL CJA] anslutningar för flerkanalsanalys |
| Datavy-konfiguration | Fas 2: Konfiguration av kontodatavy | Konfigurera standardmått, mått, attribuering och beständighetsinställningar i B2B-datavyn |
| Workspace Analysis | Fas 3: Workspace Analysis | Bygg friformsanalyser med tabeller, utfall, flöden, kohort och attribuering |
| Guidad analys | Fas 3: Workspace Analysis | Använd guidade arbetsflöden för funnel, trender och kundlojalitetsanalys på kontonivå |

### [!DNL Real-Time CDP] B2B edition

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Enhetlig kontoprofil | Krav (F2/F4) | Konsolidera B2B-data från olika källor i enhetliga kontoprofiler med hjälp av specialiserade XDM B2B-schemaklasser |
| B2B-identitetsupplösning | Förutsättning (F4) | Lös relationer från människa till konto med stöd för kontohierarkier på flera nivåer och många-till-många-mappningar |
| Integrering av [!DNL Marketo Engage] | Förutsättning (F3) | Ingest behavioral engagement data and account/lead records from [!DNL Marketo Engage] via native B2B source connectors |

## Förutsättningar

Följande objekt måste finnas innan implementeringen börjar.

- [!DNL CJA] B2B edition-licensen är aktiv och har etablerats för organisationen
- [!DNL RT-CDP] B2B edition-licens är aktiv med B2B-scheman och kontoprofiler konfigurerade
- B2B XDM-scheman har definierats (konto, säljprojekt, kundrelation, säljprojektspersonsrelation, marknadsföringslistmedlemmar)
- [!DNL Marketo Engage] och/eller CRM-källanslutningar är konfigurerade och inhämtar data aktivt
- Data om beteendehändelser på kontonivå (webbbesök, e-postinteraktioner, inskickade formulär) flödar in i AEP med kontoassociation
- Relationer från människa till konto har upprättats i identitetsdiagrammet
- Minst 30 dagars historisk B2B-engagemangsdata finns tillgängliga för meningsfull analys
- Intresseförklaringar för inköp av grupproller och intressemappningar för lösningar har fastställts
- [!DNL CJA] användarkonton har tilldelats lämpliga produktprofiler för B2B edition-funktioner
- Mål-KPI:er och rapporteringskrav har definierats av marknads- och säljledningen

## Implementeringsalternativ

I följande avsnitt beskrivs olika sätt att implementera det här användningsmönstret.

### Alternativ A: Kontocentrerad analys

**Passar bäst för:** Organisationer som vill analysera alla engagemangs- och pipeline-data via kontots objektiv. I den här metoden används kontobehållaren som primär analysenhet, vilket ger en översikt över hur konton utvecklas under köpresan.

**Så här fungerar det:**

Konfigurera en [!DNL CJA] B2B-anslutning med Konto som primär identifierare. Alla beteendehändelser, möjligheter och köpgruppsdata samlas på kontonivån. I datavyn används Konto som behållare på den högsta nivån med kapslad person, session och händelse. Detta gör att man kan göra en analys som&quot;Hur många konton har besökt prissidan och sedan skapat en möjlighet inom 30 dagar?&quot;

Kontobaserad analys ger den mest naturliga bilden för B2B-organisationer där kontot är inköpsenheten. Dimensioner som bransch, företagsstorlek, kontonivå och kontoägare kan användas för att bryta ner engagemangsmönster och försäljningsstatistik. Attribuering tillämpas på kontonivån med 13-månaders uppslagsfönster som rymmer långa B2B-säljcykler.

**Viktiga överväganden:**

- Kräver att konto-till-person-mappas i identitetsdiagrammet
- Alla händelser på personnivå måste tillskrivas ett konto
- Anonym webbtrafik som inte kan kopplas till ett konto visas inte i kontonivåanalysen

**Fördelar:**

- Ger en korrekt översikt på kontonivå över hela köpresan
- Aktiverar kontobaserad attribuering som matchar hur B2B-intäkter genereras
- Stöder analys av inköpsgrupper och affärsmöjligheter som kapslade behållare i kontot
- Justerar analyser med kontobaserad marknadsföringsstrategi (ABM)

**Begränsningar:**

- Kräver robust identitetsmatchning från människa till konto
- Anonyma eller omatchade engagemangsdata exkluderas från analysen
- Mer komplex att konfigurera än personcentrerad analys

**Experience League:**

- [CJA B2B edition - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)
- [B2B edition schemas](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)

### Alternativ B: Global kontobaserad analys

**Passar bäst för:** Företagsorganisationer med komplexa kontohierarkier där ett överordnat företag har flera dotterkonton. I den här metoden används Global Account som primär identifierare, vilket innebär att all dotterkontoaktivitet samlas på den överordnade organisationsnivån.

**Så här fungerar det:**

Konfigurera B2B-anslutningen [!DNL CJA] med det globala kontot som primär identifierare i stället för konto. Detta aggregerar interaktionsdata från alla dotterföretag under deras överordnade organisation. Om&quot;Acme Corp&quot; till exempel har regionala dotterbolag&quot;Acme EMEA&quot; och&quot;Acme APAC&quot;, konsoliderar en Global Account-anslutning alla engagemang från alla tre enheter till en enda analysvy.

Datavyn innehåller ett globalt konto som den översta behållaren, med Konto, Person, Session och Händelse som kapslade behållare. Detta möjliggör analys på både global och underordnad kontonivå inom samma arbetsyteprojekt. Attributsökningsfönster gäller på global kontonivå och fångar in alla kontaktytor i hela företagshierarkin.

**Viktiga överväganden:**

- Kräver kontohierarkidata med överordnade och underordnade relationer definierade i B2B-datamodellen
- Det globala konto-ID:t måste fyllas i och vara korrekt för alla kontoposter
- Dotterkonton måste mappas korrekt till sina överordnade konton

**Fördelar:**

- Ger samlad synlighet över komplexa företagsstrukturer
- Förhindrar fragmenterad analys när en enda företagskund har flera kontoposter
- Möjliggör jämförelse mellan regionala dotterbolag på ett enda globalt konto
- Stöd för pipeline och intäktsrapportering på företagsnivå

**Begränsningar:**

- Kräver korrekta kontohierarkidata, som många organisationer har svårt att underhålla
- Kan skymma mönster på underordnad nivå endast när de visas på global nivå
- Ytterligare datamodelleringsinsatser för att upprätta och underhålla hierarkiska relationer

**Experience League:**

- [CJA B2B edition - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

### Alternativ C: Hybrid person + kontoanalys

**Passar bäst för:** Organisationer som övergår från personbaserad analys till kontobaserad analys eller de som behöver både person- och kontonivåvyer. Med den här metoden skapas två datavyer från samma anslutning - en personcentrerad och en kontocentrerad.

**Så här fungerar det:**

Konfigurera en enskild [!DNL CJA] B2B-anslutning som innehåller alla B2B-datauppsättningar (händelse, konto, affärsmöjlighet, inköpsgrupp, person-kontorelationer). Skapa sedan två datavyer: en med Person som primär behållare (som liknar standard [!DNL CJA]) och en med Konto som primär behållare. Analytikerna kan växla mellan olika datavyer beroende på vilken fråga som ställs.

Den personcentrerade datavyn ger en traditionell reseanalys på individnivå (t.ex.&quot;Vilken konverteringsväg för leads som blir möjligheter?&quot;), medan den kontobaserade datavyn ger en analys på organisationsnivå (t.ex.&quot;Vilka konton har den högsta konverteringsgraden från ärende till pipeline?&quot;). Båda vyerna använder samma underliggande data, vilket ger enhetlighet.

**Viktiga överväganden:**

- Kräver två datavyer med potentiellt olika dimensioner och mätkonfigurationer
- Analytikerna behöver utbildning i när de ska använda respektive vy
- Beräknade mätvärden kan behöva skapas separat för varje datavy

**Fördelar:**

- Ger flexibilitet att analysera data både på person- och kontonivå
- Enklare acceptansväg för team som är vana vid analys på personnivå
- Möjliggör jämförelse mellan personnivå och kontonivå
- Stödjer både lead-baserade och kontobaserade marknadsföringsstrategier

**Begränsningar:**

- Två datavyer att underhålla och synkronisera
- Potentiell förvirring för analytiker om vilken vy som ska användas
- Beräknade mätvärden och filter kan kräva duplicering över olika vyer

**Experience League:**

- [Skapa eller redigera en datavy](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Översikt över datavyer](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)

### Jämförelse av alternativ

| Kriterier | Alternativ A: Kontocentrerat | Alternativ B: Global kontocentrerad | Alternativ C: Hybrid-person + konto |
| --- | --- | --- | --- |
| Bäst för | Standard B2B med platt kontostruktur | Företag med överordnade-underordnade hierarkier | Övergångsorganisationer eller dubbla behov |
| Komplex | Medelsvåra: | Högt | Medium-High |
| Datakrav | Mappning av kontoperson | Kontohierarki + mappning | Mappning av kontoperson |
| Attributionsomfång | Kontonivå (13-månaders uppslag) | Global kontonivå (13-månaders uppslag) | Både person- och kontonivå |
| Anonyma data | Exkluderad från kontovy | Exkluderad från global vy | Inkluderad i personvyn, exkluderad från kontovyn |
| Kräver | [!DNL RT-CDP] B2B edition, [!DNL CJA] B2B edition | [!DNL RT-CDP] B2B edition, [!DNL CJA] B2B edition, hierarkidata | [!DNL RT-CDP] B2B edition, [!DNL CJA] B2B edition |
| Underhållsarbete | Vyn Enstaka data | Vyn Enstaka data | Två datavyer |

### Välj rätt alternativ

- **Välj alternativ A** om din organisation har en platt kontostruktur (inga hierarkier för överordnade och underordnade), din ABM-strategi fungerar på den enskilda kontonivån och du vill ha den enklaste vägen till kontoanalys.
- **Välj alternativ B** om målkontona är stora företag med dotterkonton mellan regioner eller divisioner och du behöver konsoliderad rapportering på företagsmodernivå. Det här alternativet kräver kontohierarkidata av hög kvalitet.
- **Välj alternativ C** om din organisation går över från lead-baserad till kontobaserad marknadsföring, dina analytiker behöver både funnel-analyser på personnivå och interaktionsanalyser på kontonivå, eller så har du en blandning av B2B- och B2C-affärsområden.

## Implementeringsfaser

I följande faser beskrivs den rekommenderade implementeringssekvensen.

### Fas 1: B2B-dataanslutning

**Programfunktion:** [!DNL CJA] B2B: Kontobaserad anslutning, [!DNL CJA]: Dataanslutning

Konfigurera anslutningen [!DNL CJA] som binder dina AEP B2B-datauppsättningar till [!DNL CJA] för analys. Den här anslutningen definierar vilka datauppsättningar som flödar in i [!DNL CJA], den primära identifierartypen (konto eller globalt konto) samt hur historiska data och strömmande data importeras. Kopplingen utgör grunden för alla efterföljande analyser.

#### Beslut: Primär identifierartyp

Avgör om anslutningen ska använda konto-ID eller globalt konto-ID som primär identifierare.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Konto-ID | Platt kontostruktur, inga överordnade-underordnade hierarkier | Enklare konfiguration - varje konto analyseras separat. Det vanligaste alternativet för små och medelstora B2B-företag. |
| ID för globalt konto | Företagskonton med underordnade hierarkier | Kräver hierarkidata, aggregerar alla underordnade under överordnade. Bäst för ABM-program för företag. |

#### Beslut: Val av datauppsättning och typbeteckning

Bestäm vilka B2B-datauppsättningar som ska inkluderas och hur de ska anges.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Händelsedatauppsättningar (beteenden) | Inkludera alltid | Webbinteraktioner, e-postevent, formulärinlämning, nedladdning av innehåll. Måste ha ett tidsstämpelfält. Det här är engagemangssignalerna. |
| Datamängder för kontopost (profil) | Inkludera alltid | Kontoattribut som bransch, storlek, nivå, ägare. Anger den dimensionella kontexten för kontoanalys. |
| Datauppsättningar för affärsmöjligheter (sökning/profil) | Inkludera för pipeline-analys | Affärsmöjlighetens fas, värde, stängningsdatum. Krävs för pipeline- och intäktsattribueringsanalys. |
| Köpa gruppdatauppsättningar (sökning/profil) | Inkludera för inköpsgruppsanalys | Köpa grupproller, engagemangspoäng, fullständighet. Krävs för analys av inköpsgruppdisposition. |
| Relationsdatauppsättningar för person-konto (sökning) | Inkludera alltid | Mappar personer till konton. Kritiskt för att associera händelser på personnivå med analys på kontonivå. |
| Kampanj-/programdatauppsättningar (sökning) | Inkludera för attribuering | Kampanjmetadata, programtyper, kanaler. Aktiverar analys av kampanjpåverkan. |

#### Beslut: Område för bakgrundsfyllning

Avgör hur mycket historiska data som ska importeras till anslutningen.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Alla befintliga data | B2B-säljcyklerna är långa (6-18 månader) och du behöver en komplett historik | Rekommenderas för B2B. Backfill kan ta dagar för stora datauppsättningar men ger fullständiga attribueringsdata. |
| Anpassat datumintervall (senaste 2-3 åren) | Datakvaliteten försämras mer än en viss punkt | Balanserar fullständighet med datakvalitet. Vanligt när CRM-data har historiska inkonsekvenser. |
| Ingen bakgrundsfyllning | Endast testning eller utveckling | Endast nya data flödar i. Passar inte för B2B-analyser. |

#### Konfigurera B2B-dataanslutningen

**Gränssnittsnavigering:** [!DNL Customer Journey Analytics] > Anslutningar > Skapa ny anslutning

Information om nyckelkonfiguration:

- Markera AEP-sandlådan som innehåller B2B-datauppsättningar
- Ange genomsnittligt antal dagliga händelser för kapacitetsplanering
- Lägg till varje datauppsättning och ange dess typ (händelse, sökning eller profil)
- Konfigurera person-ID-fältet så att konto-ID eller globalt konto-ID används för B2B-anslutningar
- Aktivera direktuppspelning för datauppsättningar som kräver nästan realtidsuppdateringar
- Aktivera&quot;Importera alla befintliga data&quot; för historik med bakåtfyllnad

**Var alternativen skiljer sig:**

**För alternativ A (kontocentrerat):**
Ange den primära identifieraren som konto-ID. Lägg till kontopost, affärsmöjlighet, inköpsgrupp och relationsdatauppsättningar för personkonton. Konfigurera händelsedatamängder på personnivå med konto-ID-fältet för koppling av korsdatamängd.

**För alternativ B (globalt kontobaserat):**
Ange den primära identifieraren som globalt konto-ID. Kontrollera att kontohierarkidata innehåller fältet för globalt konto-ID. Alla datauppsättningar måste innehålla eller kunna kopplas till det globala konto-ID:t för att kunna samlas in korrekt.

**För alternativ C (hybrid):**
Skapa en enda anslutning med alla B2B-datauppsättningar. Använd konto-ID som primär identifierare. Den personcentrerade vyn skapas i fas 2 med en annan datavykonfiguration för samma anslutning.

**Experience League-dokumentation:**

- [Anslutningar - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [Skapa eller redigera en anslutning](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [Hantera anslutningar](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/manage-connections)
- [CJA B2B edition - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

### Fas 2: Konfiguration av kontodatavy

**Programfunktion:** [!DNL CJA] B2B: Konfiguration av B2B-datavy, [!DNL CJA]: Datavykonfiguration

Konfigurera datavyn som definierar hur anslutningsdata visas i analysen. För B2B-analyser innebär detta bland annat att konfigurera B2B-specifika behållare (konto, säljprojekt, inköpsgrupp), mappa B2B-schemafält till dimensioner och mått, ställa in attribueringsmodeller med B2B-lämpliga lookback-fönster och skapa härledda fält för B2B-affärslogik.

#### Beslut: Konfiguration av behållare

Avgör vilka B2B-behållare som ska aktiveras och hur de ska namnges.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Konto + person + session + händelse | Standard B2B utan köp- eller säljgruppsanalys | Den enklaste B2B-behållarhierarkin. Konto är behållaren på den översta nivån. |
| Konto + säljprojekt + person + session + händelse | Rörledning och intäktsanalys krävs | Lägger till affärsmöjligheten som behållarnivå, vilket möjliggör analys av affärsmöjligheter. |
| Konto + inköpsgrupp + säljprojekt + person + session + händelse | Fullständig B2B-analys inklusive inköpsgruppens sammansättning | Mest omfattande. Möjliggör analys på alla nivåer i B2B-datamodellen. |
| Global account + account + Person + Session + Event | Analys av global kontohierarki | Lägger till ett globalt konto som den högsta behållaren ovanför Konto. |

#### Beslut: Attributmodell för B2B-mått

Avgör vilken attribueringsmodell som ska vara standard för konverteringsmått.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Linjär attribuering (13-månaders uppslag) | Alla kontaktytor i B2B-resan får samma erkännande | Bäst för att förstå den fullständiga mixen av marknadsföringsaktiviteter. Rekommenderad startpunkt för B2B. |
| U-formad attribuering (13-månaders uppslag) | Framhäv första och sista kontakten med kredit till mitten | Framhäv leadframtagning och tillfällen till konvertering. Vanligt inom analys av efterfrågegenerering. |
| Tidsminskning (13-månaders uppslag) | Fler senaste kontaktytor bör få mer kredit | Bäst när senaste nytt engagemang är en viktig signal för säljberedskapen. |
| Senaste beröring | Enkel rapportering av den slutliga kontaktytan före konvertering | Lätt att förstå men undervärderar tidig marknadsföring. Används endast för snabb operativ rapportering. |

#### Beslut: Sessionsdefinition för B2B

Bestäm hur sessioner ska definieras för B2B-engagemang.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| 30-minuters timeout (standard) | Sessionsbeteende för standardwebbanalys | Standard för analys av webbengagemang. Må fragmentera sessioner med lång innehållsförbrukning. |
| Utökad tidsgräns (60-120 minuter) | B2B-användare deltar i längre forskningssessioner | B2B-köpare ägnar ofta längre tid åt att granska tekniskt innehåll, prissättning och dokumentation. |
| Händelsebaserad ny session | Specifika händelser ska alltid starta en ny session | Används när kampanjklickningar eller demonstrationsförfrågningar alltid ska starta en ny analyssession. |

#### Konfigurera kontodatavyn

**Gränssnittsnavigering:** [!DNL Customer Journey Analytics] > Datavyer > Skapa ny datavy

Information om nyckelkonfiguration:

- Välj anslutningen som skapades i fas 1
- Konfigurera tidszon och kalendertyp som passar organisationen
- Byt namn på behållare till B2B-relevant terminologi (till exempel Account/Engagement/Touchpoint)
- Mappa B2B-schemafält till dimensioner: kontonamn, konto-ID, bransch, företagsstorlek, kontonivå, kontoägare, affärsmöjlighetsstadium, affärsmöjlighetsvärde, inköpsgruppsroll, lösningsränta
- Mappa interaktionsmått: händelser (förekomster), människor, sessioner, sidvisningar, formulärinskick, e-postöppningar, e-postklick
- Konfigurera beständighet för nyckeldimensioner (t.ex. kontoindustrin kvarstår på kontonivå)
- Ange attribuering till linjär med 13-månaders uppslag som standard för konverteringsmått
- Skapa härledda fält för klassificering av marknadsföringskanaler, poängnivåer för engagemang och gruppering av affärsmöjlighetsfaser

**Var alternativen skiljer sig:**

**För alternativ A (kontocentrerat):**
Konfigurera en enskild datavy med Konto som behållare på den översta nivån. Inkludera behållare för säljprojekt och inköpsgrupp om analys av försäljningsförlopp och inköpsgrupp behövs.

**För alternativ B (globalt kontobaserat):**
Konfigurera globalt konto som behållare på den översta nivån. Inkludera konto som underbehållare för att aktivera både global och underordnad analys.

**För alternativ C (hybrid):**
Skapa två datavyer från samma anslutning. I datavy 1 används person som primär behållare (standardbeteende [!DNL CJA]). I datavy 2 används Account som primär behållare med B2B-behållare. Mappa identiska mått till båda vyerna där det är tillämpligt.

**Experience League-dokumentation:**

- [Översikt över datavyer](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)
- [Skapa eller redigera en datavy](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Översikt över komponentinställningar](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [Inställningar för beständighet](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [Attributinställningar](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [Härledda fält](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/derived-fields)
- [Sessionsinställningar](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/session-settings)

### Fas 3: Workspace-analys

**Programfunktion:** [!DNL CJA] B2B: Workspace-analys på kontonivå, Köpgruppsanalys, säljprojektsanalys, B2B-segmentering, B2B-attribuering, [!DNL CJA]: Workspace-analys, framtagning av beräknade mätvärden, guidad analys

Skapa arbetsyteprojekt som ger de analytiska insikter som definieras i nyckeltal. I den här fasen ingår att skapa frihandstabeller med B2B-dimensioner och mätvärden, skapa beräknade mätvärden för B2B KPI:er, konfigurera B2B-specifika visualiseringar (kontoflöde, möjlighet-funnel, köpa gruppengagemang), skapa filter/segment med B2B-behållare och tillämpa B2B-attribueringsmodeller.

#### Beslut: Arbetsytestrukturen för analyser

Bestäm hur arbetsytans projekt ska ordnas.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Ett omfattande projekt med flera paneler | Små team, alla intressenter ser samma rapporter | Underlätta underhåll. Använd paneler för att skilja ämnen åt (engagemang, pipeline, attribuering). Upp till 40 paneler per projekt. |
| Flera fokuserade projekt efter målgrupp | Olika intressenter behöver olika vyer | Marknadsföring får engagemang och attribuering. Försäljningen hämtar hälsotillstånd för pipeline/konto. Åtgärder ger datakvalitet. Mer underhåll men bättre målinriktad. |
| Mallbaserade projekt med guidad analys | Självbetjäningsanalys för icke-expertanvändare | Använd guidad analys för funnel och trendvyer. Spara som mallar för upprepningsbar analys. Bäst för bred användning. |

#### Beslut: B2B-beräknade värden

Avgör vilka beräknade värden som behövs för B2B KPI:er.

| Mått | Formel | När ska du skapa |
| --- | --- | --- |
| Ansvarsfrekvens för konto | (Totalt antal kontohändelser/totalt konto) | Alltid - B2B-kärnmått |
| Slutlighet för inköpsgrupp % | (Fyllda roller/obligatoriska roller) * 100 | När inköpsgruppsanalys är i omfånget |
| Konto-till-säljprojekt-konvertering | Konton med affärsmöjligheter/engagerade konton | När pipeline-analys behövs |
| Influensa i rörledning i % | Berört rörledningsvärde/totalt rörledningsvärde | När marknadsattribuering krävs |
| Genomsnittligt engagemang per kontakt | Händelser/unika personer per konto | När analys av kontopenetration krävs |
| Innehållsengagemang efter roll | Händelser som filtrerats efter Buying Group-roll | När innehållsoptimering för B2B krävs |

#### Beslut: B2B-filter/segmentområde

Avgör vid vilken behållarnivå filter ska skapas.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Filter på kontonivå | Analys som omfattar kriterier för kontomatchning (t.ex. företagskonton, specifika branscher) | Inkluderar alla händelser från kvalificerade konton. De vanligaste för B2B. |
| Filter på affärsmöjlighetsnivå | Analys som omfattar specifika typer eller faser av affärsmöjlighet | Inkluderar alla händelser som är associerade med kvalificerade affärsmöjligheter. |
| Köpa filter på gruppnivå | Analys som omfattar specifika köpgruppstillstånd | Inkluderar händelser från personer i kvalificerade inköpsgrupper. |
| Filter på personnivå | Analysomfång för individer som matchar villkor (t.ex. specifika roller, titlar) | Standardfilterbeteende. Använd det här när du analyserar enskilt engagemang i B2B-sammanhang. |

#### Bygg analysen av arbetsytan

**Gränssnittsnavigering:** [!DNL Customer Journey Analytics] > Workspace > Projekt > Skapa projekt

Information om nyckelkonfiguration:

- Markera B2B-datavyn som skapades i fas 2
- Bygg frihandstabeller med kontonivådimensioner (kontonamn, bransch, nivå) uppdelade efter interaktionsstatistik
- Skapa funnel-visualiseringar som visar hur affärsmöjligheterna utvecklas stegvis
- Skapa sammansättningstabeller för inköpsgrupper som visar rollfyllnadsnivåer och engagemang per roll
- Konfigurera B2B-attribueringspaneler som jämför attribueringsmodeller (linjär, U-formad, tidsminskning) med 13 månaders uppslag
- Skapa visualiseringar av kontoflöden som visar vanliga vägar genom köpresan
- Skapa kohorttabeller som analyserar kontokvarhållande och återengagemang över tid
- Använd B2B-filter för segmentanalys efter kontonivå, bransch eller engagemangsnivå
- Skapa anteckningar för viktiga händelser (kampanjer, produktreleaser, prisändringar)

**Experience League-dokumentation:**

- [Workspace - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Skapa ett projekt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [Frihandsregister](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [Attributionspanelen](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [Flödesvisualisering](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [Utfallsvisualisering](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [Kohortabell](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [Översikt över filter](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [Översikt över beräknade mätvärden](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [Skapa beräknade mått](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [Översikt över anteckningar](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/annotations/overview)
- [Översikt över guidad analys](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/overview)
- [Uppdelningsdimensioner](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)

### Fas 4: Dashboard publishing

**Programfunktion:** [!DNL CJA]: Dashboard- och styrkortspublicering, [!DNL CJA]: Audience Publishing

Skapa delningsbara instrumentpaneler och mobilstyrkort som levererar B2B-analyser till intressenter. Denna fas omfattar även publicering av [!DNL CJA]-definierade B2B-målgrupper tillbaka till AEP för aktivering i senare led, t.ex. B2B-målgruppsaktivering.

#### Beslut: Instrumentpanelens leveransmetod

Fastställ hur B2B-analyser ska levereras till intressenter.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Workspace-projekt (skrivbord) | Analytiker och marknadsföringsaktiviteter som behöver interaktiv utforskning | Full interaktivitet, detaljgranskning, filterväxling. Kräver [!DNL CJA] åtkomst. |
| Mobil styrkort | Chefer och säljare som behöver nyckeltal | Sammanfattning av tal med trendlinjer. Tillgängligt via [!DNL Adobe Analytics]-instrumentpanelsappen. Begränsad interaktivitet. |
| Schemalagd PDF/CSV-export | intressenter utan [!DNL CJA] åtkomst som behöver regelbundna uppdateringar | Automatiserad leverans enligt ett schema. Ingen interaktivitet. Bäst för varje vecka/månad. |
| Allt det ovanstående | Stora organisationer med olika intressenter | Maximal räckvidd. Högre underhållsarbete. Rekommenderas för mogna B2B-analysprogram. |

#### Beslut: Målgruppspublicering från [!DNL CJA]

Bestäm om B2B-segment ska publiceras tillbaka till AEP för aktivering.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Publicera kontobaserade målgrupper | Analysinsikter bör utgöra underlag för målgruppsanpassning och undertryckning | Aktiverar aktivering av [!DNL CJA] definierade segment (till exempel &quot;mycket engagerade konton utan öppna möjligheter&quot;) via [!DNL RT-CDP]. Uppdateringsgräns: 4 timmar till varje vecka. |
| Publicera inte | Analysen är enbart till för rapportering, inte aktivering | Enklare konfiguration. Aktiveringen hanteras separat i [!DNL RT-CDP]. |

#### Publicera paneler och målgrupper

**Gränssnittsnavigering:** [!DNL Customer Journey Analytics] > Projekt > Dela (för Workspace), Projekt > Skapa > Mobile-styrkort (för styrkort), Komponenter > Publiker > Publicera (för publikation)

Information om nyckelkonfiguration:

- Bygg chefsstatuspaneler med sammanfattningsnummer för viktiga nyckeltal för B2B (totala engagerade konton, pipeline-värde, hela inköpsgruppen)
- Konfigurera jämförelseperioder (månad för månad, kvartal för kvartal) för trendindikatorer
- Skapa mobilstyrkort med paneler för kontoengagemang, pipeline-hälsa och attribueringsstatistik
- Lägg till filter för chefer för att växla mellan vyer per region, bransch eller kontonivå
- Konfigurera schemalagd projektleverans för Veckorapporter
- För målgruppspublicering: välj B2B-filtret, konfigurera identitetsnamnutrymmet (konto-ID) och ange uppdateringsgräns

**Experience League-dokumentation:**

- [Skapa ett mobilstyrkort](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [Dela projekt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [Schemalägg projekt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [Konfigurera och strukturera styrkort](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Adobe Analytics Dashboards - Executive Guide](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/set-up-execs)
- [Översikt över målgrupper](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [Skapa och publicera målgrupper](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/publish)

## Implementeringsöverväganden

Följande avsnitt behandlar skyddsförslag, vanliga fallgropar, bästa praxis och avbrottsbeslut som ska beaktas vid implementeringen.

### Gardrutor och begränsningar

- [!DNL CJA] anslutningar kan innehålla datauppsättningar från endast en AEP-sandlåda - [CJA skyddsräcken](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-admin/guardrails)
- Maximalt 5 000 dimensioner och 5 000 mätvärden per datavy
- Max 100 härledda fält per datavy
- B2B-attribuering stöder uppslagsfönster upp till 13 månader för kontonivåanalys
- Maximalt 75 publicerade målgrupper per [!DNL CJA] kund över alla sandlådor
- Publicering av målgrupper har minst en uppdateringskurs var fjärde timme
- Tidsfördröjning för direktuppspelning från AEP till [!DNL CJA] är vanligtvis under 90 minuter
- Frihandsregister har stöd för upp till 10 dimensionsfördelningar, djup
- Mobil styrkort har stöd för upp till 16 plattor per styrkort
- Workspace-projekt har stöd för upp till 40 paneler per projekt
- Backfill för stora B2B-datauppsättningar (miljarder poster) kan ta dagar att slutföra

### Vanliga fallgropar

- **Ofullständig mappning från människa till konto:** Om händelser på personnivå inte kan associeras med ett konto visas de inte i kontonivåanalysen. Se till att alla händelsedatamängder innehåller ett fält som kan anslutas till konto-ID, antingen direkt eller via en datauppsättning för person-kontorelationssökning. Granska procentandelen händelser som saknar kontoassociation innan analys byggs.
- **Felaktig typbeteckning för datauppsättningen:** B2B-sökdatauppsättningar (affärsmöjlighet, inköpsgrupp, person-konto-relationer) måste vara korrekt angivna som uppslag eller profiltyp i anslutningen [!DNL CJA]. Om en uppslagsdatauppsättning skrivs som en händelsedatamängd skapas felaktiga resultat eftersom [!DNL CJA] försöker att behandla varje post som en tidsstämplad händelse.
- **Attributionsfönstret är för kort för B2B:** Om du använder 30-dagars standardattribueringsfönster missas tidiga kontaktytor på B2B-resor som vanligtvis sträcker sig över 6-18 månader. Konfigurera alltid 13-månaders uppslagsfönster för B2B-attribueringsstatistik.
- **Felaktig blandning av kontonivåvärden och personnivåstatistik:** Att räkna &quot;personer&quot; i en kontonivåanalys kan vara vilseledande. Kontrollera att beräknade värden har definierats på lämplig behållarnivå. En kontointeraktionsfrekvens ska använda händelser på kontonivå som delas med konton, inte med människor.
- **Inaktuella inköpsgruppdata:** Köpgruppens komposition och rolltilldelningar ändras över tid. Om inköp av gruppdatauppsättningar inte uppdateras regelbundet kommer fullständighetsmått att vara felaktiga. Kontrollera att källsystemet ([!DNL Marketo Engage] eller [!DNL AJO] B2B edition) aktivt synkroniserar köpgruppsdata.
- **Överlagring av ett enskilt arbetsyteprojekt:** B2B-analyser sträcker sig över engagemang, pipeline, attribuering och inköpsgrupper. Att försöka placera allt i ett projekt leder till långsam inläsning och förvirrande navigering. Använd flera fokuserade projekt eller tydligt märkta paneler.

### God praxis

- Börja med alternativ A (Kontocentrerat) även om du tänker använda alternativ B (Global Account) senare. Kontocentrerad analys är enklare och validerar datamodellen innan du lägger till hierarkisk komplexitet.
- Skapa ett dedikerat&quot;B2B Data Quality&quot;-arbetsyteprojekt som spårar andelen händelser med kontoassociering, antalet överblivna konton och hur många som köpt grupper. Kör den här veckan för att fånga upp dataproblem tidigt.
- Använd härledda fält för att skapa poängnivåer för engagemang (hög/Medium/låg) baserat på antalet händelser på kontonivå. Detta förenklar analysen och gör det enklare för andra intressenter än tekniska.
- När B2B-attribuering konfigureras börjar du med linjär attribuering som baslinje och jämför sedan med U-formade modeller och tidsminskningsmodeller. Skillnaderna mellan modellerna visar ofta om er marknadsföringsmix är inriktad på medvetenhet eller konverteringsaktiviteter.
- Publicera ett&quot;B2B Executive Summary&quot;-mobilstyrkort med högst åtta paneler som täcker de nyckeltal som är viktigast för ledningen. Fokusera på saken - chefsstyrkorten ska svara&quot;Hur gör vi?&quot; inte &quot;Varför?&quot;
- Anteckna viktiga händelser (produktlanseringar, större lanseringar av kampanjer, prisförändringar, förändringar av försäljningsprocesser) för att skapa kontext för datatrender. B2B-data visar ofta toppar och dalar som är oförklarliga utan händelsetyp.
- När du publicerar B2B-målgrupper från [!DNL CJA] ska du använda daglig uppdatering för standardaktiveringssegment och 4-timmars uppdatering endast för tidskänsliga segment. Vanliga uppdateringar använder bearbetningsresurser.

### Avvecklingsbeslut

>[!NOTE]
>Följande beslut om avräkning bör utvärderas baserat på organisationens specifika krav och begränsningar.

**Datakompatibilitet jämfört med analysnoggrannhet**

Om alla händelser på personnivå inkluderas i kontoanalysen (även de med svag kontokoppling) blir uppgifterna mer fullständiga, men noggrannheten kan minskas om kontomappningen inte är tillförlitlig.

- **Inkludera alla händelser:** Omfattande engagemangsmätning, poäng för högre kontoengagemang, bredare synlighet
- **Exkludera ej matchade händelser:** Korrekta kontonivåvärden, tillförlitlig attribuering och tillförlitlig pipeline-korrelation
- **Rekommendation:** Uteslut omatchade händelser från kontonivåanalys men inkludera dem i en separat datavy på personnivå (alternativ C) för att förstå hela bilden. Prioritera förbättring av datakvaliteten för kontoassociationer som en parallell arbetsström.

**Fönsterlängd för B2B-attribueringssökning**

Längre uppslagsfönster (13 månader) fångar upp fler kontaktytor men kan inkludera marknadsföringsaktiviteter som inte längre är relevanta för det aktuella köpbeslutet.

- **Långvarig återblick (13 månader) prioriterar:** Hämtning av hela B2B-resan, kreditering av aktiviteter på kundinformationsstadiet, hantering av långa säljcykler
- **Kortare uppslag (6 månader) prioriterar:** Fokusera på nyligen genomförda aktiviteter, minska bruset från gamla kontaktytor, bättre återgivning av nuvarande inköpsmetod
- **Rekommendation:** Använd 13-månaders uppslag för företagskonton med långa säljcykler (12+ månader). Använd 6-månaders uppslag för medelstora konton med kortare cykler. Skapa separata beräknade mätvärden för varje fönster som ska jämföras.

**En heltäckande datavy jämfört med datavyer med flera fokus**

En datavy med alla B2B-behållare och dimensioner är enklare att underhålla men kan överbelasta analytiker med komplexitet. Flera fokuserade datavyer (engagemang, pipeline, attribuering) är enklare att använda men svårare att underhålla.

- **Enstaka vy prioriterar:** Konsekvens, enklare underhåll, domänövergripande analys inom ett enskilt projekt
- **Flera vyer prioriterar:** Analytikernas tydlighet, snabbare inläsningstider, anpassade komponentlistor per användningsfall
- **Rekommendation:** Börja med en enda heltäckande datavy. Om analytiker rapporterar svårigheter att hitta rätt dimensioner och mätvärden, kan du skapa välstrukturerade komponentgrupper i samma vy innan du delar upp dem i flera vyer. Använd arbetsytemallar för att vägleda analytikerna till rätt komponenter.

## Relaterad dokumentation

Följande resurser innehåller ytterligare information för implementering av det här användningsmönstret.

**[!DNL CJA]B2B edition**

- [CJA B2B edition - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)
- [CJA - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [CJA skyddsräcken](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-admin/guardrails)

**Anslutningar**

- [Anslutningar - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [Skapa eller redigera en anslutning](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [Hantera anslutningar](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/manage-connections)

**Datavyer**

- [Översikt över datavyer](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)
- [Skapa eller redigera en datavy](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Översikt över komponentinställningar](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [Inställningar för beständighet](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [Attributinställningar](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [Formatinställningar](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/format)
- [Härledda fält](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/derived-fields)
- [Sessionsinställningar](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/session-settings)

**Workspace och analys**

- [Workspace - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Skapa ett projekt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [Frihandsregister](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [Flödesvisualisering](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [Utfallsvisualisering](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [Kohortabell](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [Attributionspanelen](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [Dela projekt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [Schemalägg projekt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [Uppdelningsdimensioner](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)

**Komponenter**

- [Översikt över filter](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [Skapa filter](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/create-filters)
- [Översikt över beräknade mätvärden](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [Skapa beräknade mått](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [Översikt över anteckningar](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/annotations/overview)
- [Datumintervall](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/date-ranges/overview)

**Publiker**

- [Översikt över målgrupper](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [Skapa och publicera målgrupper](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/publish)
- [Hantera målgrupper](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/manage)

**Kontrollpaneler och styrkort**

- [Skapa ett mobilstyrkort](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [Konfigurera och strukturera styrkort](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Adobe Analytics Dashboards - Executive Guide](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/set-up-execs)

**Guidad analys**

- [Översikt över guidad analys](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/overview)
- [Funnel view](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [Trendvyn](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/trends/usage)
- [Bevarandevy](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/retention/retention-rates)

**[!DNL RT-CDP]B2B edition**

- [RT-CDP B2B edition - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#702702)
- [B2B edition schemas](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Översikt över B2B-källor](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/sources/b2b)

**AEP Data Foundation**

- [XDM - systemöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Översikt över källor](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [Marketo Engage Connector](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Översikt över identitetstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Översikt över sandlådor](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/home)

**Datastyrning och livscykel**

- [Översikt över dataförvaltning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Avancerad livscykelhantering av data](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)

**Självstudiekurser och guider**

- [Grundläggande om schemakomposition](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [Översikt över beräknade attribut](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Översikt över Insikter i observationer](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)
