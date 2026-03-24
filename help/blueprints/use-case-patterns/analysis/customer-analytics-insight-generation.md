---
title: Kundanalys och insiktsgenerering
description: Lär dig hur du bygger arbetsytor för flerkanalsanalys, beräknade mätvärden och kontrollpaneler för beteende- och prestandaanalys.
solution: Customer Journey Analytics, Experience Platform
exl-id: 235a4eb0-91ae-4030-b90e-7eda08c67ae1
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '8947'
ht-degree: 0%

---

# Generering av kundanalyser och insikter

Den här guiden ger en komplett implementeringsreferens för kundanalys och generering av insikter. Det handlar om hur du ansluter [!DNL Adobe Experience Platform] datauppsättningar till [!DNL Customer Journey Analytics], konfigurerar datavyer, bygger arbetsytor för kostnadsfri analys, skapar beräknade mätvärden, publicerar instrumentpaneler och mobilstyrkort och eventuellt publicerar CJA-definierade målgrupper tillbaka till [!DNL Adobe Experience Platform] för aktivering.

Det är utformat för lösningsarkitekter, marknadsföringsteknologer och implementeringstekniker som behöver förstå alla genomförbara implementeringsvägar, kompromisserna mellan dem och de konfigurationsbeslut som krävs i varje fas.

Till skillnad från de andra mönstren i taxonomin, som fokuserar på aktivering och engagemang (skicka meddelanden, personalisera innehåll, aktivera målgrupper), fokuserar det här mönstret på förståelse - analysera kundbeteende, mäta kampanjresultat, identifiera trender och generera insikter som stöder strategi- och optimeringsbeslut. Det är det vanligaste mönstret och par med nästan varje aktiverings- eller personaliseringsmönster.

## Använd ärendeöversikt

Organisationer måste förstå hur kunderna beter sig i olika kanaler, hur kampanjer fungerar, var kunderna faller bort från sina resor, vilket innehåll som får genklang och hur olika segment behåller sig över tid. Kundanalys och insiktsgenerering tillgodoser detta behov genom att ansluta de omfattande flerkanalsdata som finns i [!DNL Adobe Experience Platform] till [!DNL Customer Journey Analytics], där analytiker kan skapa frihandsarbetsytor, skapa anpassade mätvärden, konfigurera attribueringsmodeller och publicera instrumentpaneler för intressenters behov.

Mönstret vänder sig till en mängd olika målgrupper: marknadsföringsanalytiker som behöver djupgående analyser, kampanjchefer som behöver prestandakontroller, produktchefer som behöver engagemangs- och kundlojalitetsinsikter samt chefer som behöver snabbgående KPI-styrkort. Implementeringsmetoden varierar beroende på det primära analytiska fokus - kampanjresultatmätning, flerkanalsanalys, analysdriven målgruppsaktivering eller guidade produktinsikter.

## Viktiga verksamhetsmål

Följande affärsmål stöds av det här användningsmönstret.

**Förbättra analyser och rapporter**

Förbättra rapporteringsmöjligheterna för snabbare och mer åtgärdbara marknadsföringsinsikter med hjälp av enhetliga instrumentpaneler och självbetjäningsverktyg.

- **KPI:er:** Effektivitet, produktivitet

Mer information om det här affärsmålet finns i [Förbättra analyser och rapporter](/help/blueprints/business-objectives/analytics-insights/improve-analytics-reporting.md).

**Aktivera datadrivet beslutsfattande**

Ge teamen möjlighet att använda självbetjäningsanalyser, kundinsikter i realtid och AI-baserade prognoser som guidar strategin.

- **KPI:er:** Effektivitet, produktivitet

Mer information om det här affärsmålet finns i [Aktivera datadriven beslutsfattande](/help/blueprints/business-objectives/analytics-insights/enable-data-driven-decision-making.md).

**Förbättra marknadsattribueringen**

Mätning av effekten av kontaktytor, kanaler och kampanjer för marknadsföring på konverterings- och intäktsresultaten.

- **KPI:er:** Effektivitet, Inkrementell intäkt

Mer information om det här affärsmålet finns i [Förbättra marknadsattribuering](/help/blueprints/business-objectives/analytics-insights/improve-marketing-attribution.md).

**Optimera marknadsföringsbudgeten och avkastningen**

Optimera allokeringen av marknadsföringsbudgeten genom att förstå vilka kanaler och kampanjer som ger störst avkastning.

- **KPI:er:** Effektivitet, Inkrementell intäkt

Mer information om det här affärsmålet finns i [Optimera marknadsföringsutgifter och avkastning](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md).

## Exempel på taktiska användningsfall

Nedan följer exempel på taktiska användningsområden som kan implementeras med det här mönstret.

- Instrumentpanel för kampanjresultat - leveransstatistik, engagemangsgrader, konvertering och intäktsattribuering för e-post, SMS, push och betalda mediekampanjer
- Utfallsanalys för kundresan - identifiera var kunderna faller bort från köp-, registrerings- eller introduktionskanaler
- Kohortanalyser av kvarhållningsförmåga - mät hur väl olika förvärvsmetoder bevarar över veckor, månader och kvartal
- Kanalattribueringsmodellering - jämför attribuering vid första beröringen, sista beröringen, linjär och tidsminskning för att förstå vilka kanaler som driver konverteringar
- Analys av innehållsprestanda - identifiera vilket innehåll som fungerar bäst efter segment, kanal och livscykelstadium
- Produktanvändning och implementeringsanalys - spåra användning av funktioner, interaktionsfrekvens och trender för användartillväxt
- Kundlivscykelstegsanalys - segmentera och analysera kunder efter livscykelstadium (ny, aktiv, i riskzonen, annullerad)
- Kontrollpanel för optimering av marknadsföringsmixer - jämför kanalinvesteringar med intäktsbidrag
- Poäng och rapportering för flerkanalsengagemang - skapa sammansatta engagemangspoäng utifrån interaktioner mellan webben, appar, e-post och kampanjer

## Nyckeltal för prestanda

Följande nyckeltal hjälper till att mäta hur bra det här användningsmönstret är.

| KPI | Beskrivning | Mätningsmetod |
| --- | --- | --- |
| Effektivitet | Minska tiden till insikt och manuell rapportering | Spåra analytikernas tid med att skapa rapporter före och efter CJA implementering |
| Produktivitet | Antal självbetjäningsanalyser som skapats av företagsanvändare | Övervaka användningen av Workspace-projekt och kontrollpaneler |
| Inkrementell intäkt | Intäkter som härrör från insiderdrivna optimeringsbeslut | Mät intäktsökning från kampanjer som optimerats baserat på CJA analys |
| Konverteringsgrader | Funnel slutförandegrad under alla viktiga kundresor | Spåra bortfallsfrekvenser vid varje kundresa med hjälp av CJA utfallsvisualisering |
| Engagemang | Djup och frekvens för kundinteraktion över olika kanaler | Skapa beräknade mätvärden för engagemangsbedömning i CJA |
| Kvarhållning | Kundens avkastningsnivåer under definierade tidsperioder | Använd CJA kohortanalys för att mäta kvarhållningskurvor |

## Använd skiftlägesmönster

**Generering av kundanalyser och insikter**

Bygg arbetsytor för flerkanalsanalys, beräknade mätvärden och kontrollpaneler för att förstå kundbeteende och kampanjresultat.

**Funktionskedja:** Dataanslutning > Datavy Configuration > Workspace Analysis > Computed Metric Creation > Dashboard Publishing

Se avsnittet [Implementeringsalternativ](#implementation-options) för dispositionsvägledning.

## Tillämpningar

Följande program används i det här fallmönstret.

- **[!DNL Customer Journey Analytics] (CJA)** - Anslutningar, datavyer, arbetsyteanalys, guidad analys, beräknade mätvärden, instrumentpaneler, målgruppspublicering och innehållsanalys
- **[!DNL Adobe Experience Platform] (AEP)** - Datasjön, datauppsättningar, XDM-scheman, profil- och händelsedata som matar in CJA-anslutningar

## Foundationsfunktioner

Följande grundläggande funktioner måste finnas för det här användningsmönstret. För varje funktion anger statusen om den vanligtvis är obligatorisk, antas vara förkonfigurerad eller inte tillämplig.

| Funktionen Foundation | Status | Vad måste finnas på plats | Experience League referens |
| --- | --- | --- | --- |
| Administration och styrning | Antagen på plats | CJA produktprofil har etablerats med behörighet att skapa arbetsytor och datavyåtkomst. AEP datauppsättningar som är tillgängliga för CJA-anslutningen. Användare som tilldelats lämpliga CJA-roller. | [Översikt över åtkomstkontroll](https://experienceleague.adobe.com/sv/docs/experience-platform/access-control/home) |
| Datamodellering och förberedelse | Obligatoriskt | XDM-scheman och datauppsättningar som ska anslutas till CJA måste finnas i AEP. Schemadesign påverkar direkt vilka dimensioner och mätvärden som är tillgängliga i CJA datavyer. Händelsescheman behöver tidsstämpelfält, uppslagsscheman behöver nyckelfält. | [Översikt över XDM-systemet](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/home) |
| Datakällor och samling | Obligatoriskt | Data måste flöda in i AEP datamängder - webbevent via Web SDK, appevent via Mobile SDK, AJO kampanjevent och CRM-data via källanslutningar. Analysens komplexitet beror på den insamlade datans bredd. | [Källor - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/home) |
| Konfiguration av identitet och profil | Obligatoriskt | Personens ID-konfiguration i CJA-anslutningen avgör hur händelser sammanfogas över datauppsättningar. Enhetsidentitetssammanfogning i AEP förbättrar CJA förmåga att skapa fullständiga kundresor. Identitetsnamnrymden måste konfigureras för fältet Person-ID. | [Översikt över identitetstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/home) |
| Målgruppsdefinition och segmentering | Ej tillämpligt | CJA bygger sina egna filter och målgrupper i analyskontexten. RT-CDP-målgrupper är inte en förutsättning, men CJA kan publicera målgrupper tillbaka till AEP via publikation (Option C). | [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/home) |

## Stödfunktioner

Följande funktioner förstärker det här användningsmönstret, men behövs inte för att köra kärnan.

| Stödfunktioner | Status | Varför det spelar någon roll | Experience League referens |
| --- | --- | --- | --- |
| Skapande av beräknat/härlett attribut | Rekommenderad | AEP beräknade attribut kan berika datauppsättningarna som är kopplade till CJA och ge ytterligare mått och mätvärden för analys (t.ex. antal livstidsköp, dagar sedan senaste aktivitet). Dessa aggregeringar på profilnivå blir tillgängliga som dimensioner i CJA datavyer. | [Översikt över beräknade attribut](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/computed-attributes/overview) |
| Livscykelhantering för data | Rekommenderad | Principer för datalagring påverkar vilka historiska data som är tillgängliga i CJA. Långvarig lagring är vanligtvis önskvärd för analyser för att möjliggöra årliga jämförelser och långsiktig trendanalys. Konfigurera TTL:er för datamängd för att säkerställa lämpligt historiskt djup. | [Översikt över livscykelhantering av avancerade data](https://experienceleague.adobe.com/sv/docs/experience-platform/data-lifecycle/home) |
| Dataanvändningsetiketter och -tillämpning | Rekommenderad | Etiketter för styrning av känsliga fält kan begränsa vad som visas i CJA datavyer. Om PII eller känsliga data ingår i CJA-anslutningen säkerställer datastyrningsetiketterna att åtkomsten är korrekt och förhindrar obehörig exponering i delade instrumentpaneler. | [Datastyrningsöversikt](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/home) |
| Övervakning och observerbarhet | Rekommenderad | CJA anslutningshälsa och dataaktualitet bör övervakas. Konfigurera varningar för fel i källdataflödet och problem med förtäring för att säkerställa att dataflödet i CJA är tillförlitligt och aktuellt. | [Översikt över Insikter om observabilitet](https://experienceleague.adobe.com/sv/docs/experience-platform/observability/home) |
| Rapportering och analys | Ingår | Detta är implementeringen av rapportering och analys. När en referensplan för ett annat mönster innehåller S5 ska du använda den här kundanalysen och insikterna för att generera analyser för analysimplementeringen. | [CJA - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-overview/cja-overview) |

## Programfunktioner

I den här planen används följande funktioner från programfunktionskatalogen. Funktioner mappas till implementeringsfaser i stället för till numrerade steg.

### [!DNL Customer Journey Analytics] (CJA)

I följande tabell visas de CJA-programfunktioner som används i det här mönstret.

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Dataanslutning | Fas 1: Dataanslutning | Bind AEP-datauppsättningar till en CJA-anslutning för flerkanalsanalys, konfigurera datauppsättningstyper och Person-ID för sammanfogning av datauppsättningar |
| Datavy-konfiguration | Fas 2: Konfiguration av datavy | Definiera mått, mätvärden, attribueringsmodeller, beständighetsinställningar, sessionsparametrar och härledda fält som formger det analytiska perspektivet |
| Workspace Analysis | Fas 3: Skapa analyser och mätvärden | Skapa frihandsanalyser med tabeller, visualiseringar, filter, anteckningar och dimensionsuppdelningar (alternativ A, B, C) |
| Guidad analys | Fas 3: Skapa analyser och mätvärden | Använd strukturerade guidade arbetsflöden för funnel, trender, lojalitet, användartillväxt och interaktionsanalys (alternativ D) |
| Skapande av beräknade mått | Fas 3: Skapa analyser och mätvärden | Definiera beräknade mätvärden med hjälp av formler, filter och funktioner för återanvändbara nyckeltal som konverteringsgrad, engagemangspoäng och intäkter per besök |
| Dashboard &amp; Scorecard Publishing | Fas 4: Dashboard Publishing | Skapa och dela interaktiva instrumentpaneler och mobilstyrkort för intressentrapportering |
| Audience Publishing | Fas 5: Audience Publishing (endast alternativ C) | Publicera CJA-definierade målgrupper tillbaka till AEP kundprofil i realtid för aktivering längre fram i kedjan |
| Innehållsanalys | Fas 3: Skapa analyser och mätvärden | Analysera trender, avvikelser och utmattning för innehållsprestanda i digitala resurser (när innehållsanalys är i fokus) |

### [!DNL Adobe Experience Platform] (AEP)

I följande tabell visas de AEP-programfunktioner som används i det här mönstret.

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Datasjön och datauppsättningar | Krav (F2, F3) | Ange källhändelser, profil och uppslagsdatauppsättningar som matar in CJA-anslutningen |
| Identitetstjänst | Förutsättning (F4) | Ange konfiguration av identitetsnamnrymd för sammanfogning av person-ID mellan datauppsättningar i CJA-anslutningen |

## Förutsättningar

Följande villkor måste vara uppfyllda innan du implementerar det här användningsfallsmönstret.

- [ ] CJA produktberättigande har etablerats för organisationen
- [ ] CJA produktprofiler har konfigurerats med lämplig användaråtkomst (arbetsytan skapas, datavyåtkomst)
- [ ] AEP-sandlådan innehåller måldatauppsättningar med dataflöde (webbhändelser, apphändelser, kampanjdata, CRM-poster)
- [ ] XDM-scheman definieras för alla källdatamängder med lämpliga fältgrupper
- [ Fältet ] för person-ID identifieras och är konsekvent tillgängligt för alla datauppsättningar som ska anslutas
- [ ] Identitetsnamnutrymmen är konfigurerade i AEP för det person-ID som används i CJA anslutningssammanfogning
- [ ] Krav på intressenter har dokumenterats - vilket nyckeltal, vilka målgrupper som kommer att förbruka instrumentpaneler, vilken detaljnivå
- [ ] För mobilstyrkort: intressenter har mobilappen [!DNL Adobe Analytics] för instrumentpaneler installerad
- [ ] för alternativ C (Audience Publishing): AEP kundprofil i realtid är aktiverad i målsandlådan
- [ ] för alternativ D (guidad analys): CJA SKU innehåller funktioner för guidad analys

## Implementeringsalternativ

I det här avsnittet beskrivs de tillgängliga implementeringsalternativen för det här användningsmönstret.

### Alternativ A: Kampanjresultatanalys

**Passar bäst för:** Mäta och optimera kampanjer och resereffektivitet - instrumentpaneler för e-postkampanjer, funnel-analys, kanalresultatjämförelse och rapportering av marknadsföringsavkastning.

**Så här fungerar det:**

Det här alternativet kopplar samman AJO kampanj- och resedatamängder med CJA, konfigurerar datavyer med leverans- och engagemangsmått (skicka, leverans, öppning, klick, studsar, avabonnemang), skapar instrumentpaneler för kampanjresultat och publicerar styrkort för marknadsföringsintressenter. Fokus ligger på att förstå hur marknadsföringskampanjer fungerar över flera kanaler och över tid.

Datavyn är konfigurerad med kampanjspecifika dimensioner (kampanjnamn, resenamn, kanaltyp, meddelandevariant) och leveransmått. Beräknade mått skapas för härledda mått som öppningskurs, klickfrekvens, konverteringsgrad och intäkter per meddelande. Kontrollpaneler presenterar dessa nyckeltal med jämförelseperioder för trendanalys.

**Viktiga överväganden:**

- Kräver AJO data om kampanj- och resehändelser i AEP
- Attributionsmodeller bör överensstämma med organisationens kampanjmätningsfilosofi
- Överväg att inkludera både AJO-rapporter (för mätvärden för operativ leverans) och CJA (för påverkan av flerkanalsverksamhet)

**Fördelar:**

- Specialbyggd för kampanjmätning och optimering
- Möjliggör jämförelse mellan kampanjer och analys av kanalmixning
- Beräknade mätvärden ger standardiserade KPI-definitioner för alla kampanjer
- Mobilstyrkort ger överskådliga resultat för marknadsledare

**Begränsningar:**

- Begränsad till kampanjdata och resedata; ger inte en fullständig kontext för kundresan
- Omfattar inte kundresa, bortfall eller kohortanalys
- Attributionen omfattar kampanjkontaktytor i stället för hela kundresan

**Experience League:**

- [Integreringsguide för AJO + CJA](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Workspace - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/home)

### Alternativ B: Analys av kundresan

**Passar bäst för:** Förstå kundresor över flera kanaler - bortfallsanalys, sökvägsanalys, kvarhållande av kohort, attribueringsmodellering och livscykelfasanalys över kontaktpunkter för webb, app, e-post, CRM och offline.

**Så här fungerar det:**

Det här alternativet kopplar samman flera datauppsättningar från AEP (webbhändelser, apphändelser, CRM-data, kampanjinteraktioner, transaktionsposter) för att skapa en enhetlig flerkanalsvy över kundresan. Datavyn är konfigurerad med mått och mätvärden som sträcker sig över alla kanaler. CJA visualiseringar av flöden, bortfall, kohort och attribuering används för att analysera hur kunderna rör sig genom resor, var de faller bort, hur olika segment behåller och vilka kanaler som förtjänar erkännande för konverteringar.

Det här är det mest omfattande analytiska alternativet som ger djupgående insikter i hela kundupplevelsen. Det är också det mest komplicerade att implementera, vilket kräver noggrann konfiguration av person-ID för sammanfogning av datauppsättningar och genomtänkt design av datavyer för att visa rätt dimensioner och mätvärden.

**Viktiga överväganden:**

- Kräver ett konsekvent person-ID för alla anslutna datauppsättningar för korrekt flerkanalsanalys
- Schemadesign i AEP påverkar direkt kvaliteten och djupet i CJA analys
- Fler datauppsättningar i anslutningen innebär djupare analyser men längre efterfyllnadstider
- Attributmodellering kräver tydliga definitioner av konverteringshändelser

**Fördelar:**

- Komplett synlighet för flerkanalskundens resa
- CJA hela serie visualiseringar: flöde, bortfall, kohort, attribuering, frihandstabeller
- Möjliggör upptäckt av insikter som är osynliga i enkanalsrapportering
- Stöder komplexa analytiska frågor om kundbeteende och livscykel

**Begränsningar:**

- Komplexa implementeringar på grund av anslutningar med flera datauppsättningar och sammanfogning över flera kanaler
- Kräver mer planering i förväg för datavykonfiguration och härledda fält
- Backfill för stora anslutningar med flera datauppsättningar kan ta dagar
- Analyskvaliteten beror på de underliggande uppgifternas fullständighet och konsekvens

**Experience League:**

- [Anslutningar - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-connections/overview)
- [Flödesvisualisering](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [Utfallsvisualisering](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [Kohortabell](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [Attributionspanelen](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/panels/attribution)

### Alternativ C: Analyser med målgruppspublicering

**Bäst för:** Analysdriven aktivering - Upptäck intressanta segment genom CJA-analys och publicera dem sedan till AEP för aktivering via RT-CDP-destinationer, AJO-kampanjer eller AJO-resor.

**Så här fungerar det:**

Med det här alternativet utökas alternativ A eller Alternativ B med målgruppspublicering från CJA. Analytikerna bygger segment i CJA med hjälp av flerkanaliga beteendedata och den fulla analyskraften hos CJA filter, och publicerar sedan dessa målgrupper i AEP Real-Time Customer Profile för aktivering nedströms. Detta överbryggar klyftan mellan insikter och åtgärder - segment som upptäcks under undersökande analyser blir åtgärdbara målgrupper utan manuell återskapning i AEP Segment Builder.

Publicerade målgrupper visas i AEP Audience Portal med ursprung&quot;CJA&quot; och kan aktiveras för alla RT-CDP-destinationer, användas som kampanjmål i AJO eller användas som villkor för deltagande i resor.

**Viktiga överväganden:**

- Kräver att AEP kundprofil för realtid är aktiverad i målsandlådan
- CJA-anslutningen måste ha ett giltigt person-ID som matchar ett AEP-identitetsnamnutrymme
- Publicerade målgrupper räknas in i organisationens AEP-målgruppsberättigande
- Uppdateringsperioden måste konfigureras baserat på aktiveringskrav (en gång, var fjärde timme, varje dag, varje vecka)

**Fördelar:**

- Stänger slingan mellan analys och aktivering
- Gör det möjligt att identifiera högvärdessegment med hjälp av CJA flerkanalsbeteendedata
- Målgrupper som definieras i CJA kan utnyttja de dimensioner och filter som inte finns i AEP Segment Builder
- Stöder iterativ förbättring av målgruppskriterier baserat på analytiska insikter

**Begränsningar:**

- Max 75 publicerade målgrupper per CJA-kund
- Den inledande målgruppsutvärderingen kan ta upp till 24 timmar för stora datamängder
- Målgrupper som publicerats av CJA kan inte redigeras i AEP - ändringar måste göras i CJA
- Kräver ytterligare konfiguration av identitetsnamnområde och profil utöver grundläggande analys

**Experience League:**

- [Översikt över målgrupper](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [Skapa och publicera målgrupper](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/audiences/publish)

### Alternativ D: Guidad analys för produktteam

**Passar bäst för:** Produktupplevelser - anpassning av funktioner, användarinteraktionstrender, kundlojalitetsanalys, funnel-konvertering och släppeffektsanalys med CJA guidade analysarbetsflöden utan att det krävs komplexa Workspace-projektinställningar på fri hand.

**Så här fungerar det:**

Det här alternativet använder CJA Guidad analys för att generera strukturerade, mallbaserade insikter. Med guidad analys får du färdiga analystyper - funnel, trender, lojalitet, användartillväxt, engagemangsfrekvens, publiceringseffekt, första användning och tidslinje - som gör att analytiker går igenom ett strukturerat arbetsflöde för att besvara specifika produkt- och upplevelsefrågor. Det är idealiskt för produktchefer och analytiker som behöver snabba, fokuserade insikter utan att behöva skapa frihandsprojekt från grunden.

Implementeringen kopplar AEP datauppsättningar till CJA, konfigurerar en datavy med mått och mätvärden på händelsenivå och använder sedan guidade analysarbetsflöden för att generera insikter. Resultaten kan sparas som paneler i Workspace-projekt för ytterligare anpassning.

**Viktiga överväganden:**

- För guidad analys krävs CJA produktberättigande som inkluderar guidade analysfunktioner
- Passar bäst för produkt- och upplevelseanalyser i stället för kampanjresultatmätning
- Tillhandahåller strukturerade arbetsflöden som är mer tillgängliga för icke-analytikeranvändare
- Kan kombineras med kostnadsfri Workspace-analys för djupare utforskande

**Fördelar:**

- Lägre inträdeshinder - strukturerade arbetsflöden vägleder användarna genom analysen
- Specialbyggd för frågor om produktupplevelser (funnel, lojalitet, tillväxt, påverkan)
- Snabbare insikt i vanliga analysfrågor
- Sparade analyser kan bäddas in i Workspace-projekt tillsammans med frihandsanalyser

**Begränsningar:**

- Mindre flexibelt än Workspace-analys på frihand
- Begränsat till de färdiga analystyperna (funnel, trender, lojalitet, tillväxt, frekvens, påverkan, tidslinje)
- Segmentjämförelser stöder upp till tre segment samtidigt
- Funnel analys stöder maximalt 15 steg

**Experience League:**

- [Översikt över guidad analys](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/guided-analysis/overview)
- [Funnel view](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [Bevarandevy](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/guided-analysis/retention/retention-rates)

### Jämförelse av alternativ

I följande tabell jämförs de tillgängliga implementeringsalternativen.

| Kriterier | Alternativ A: Kampanjresultat | Alternativ B: Kundresa | Alternativ C: Analys + aktivering | Alternativ D: Guidad analys |
| --- | --- | --- | --- | --- |
| Bäst för | Kampanjmätning och optimering | Förståelse av flerkanalsresor | Insiktsdriven målgruppsaktivering | Produktupplevelser |
| Komplex | Låg-Medium | Högt | Högt | Lågt |
| Datamängder krävs | AJO kampanj-/reseevent | Flera flerkanalsdatauppsättningar | Samma som A eller B, plus profilidentitet | Händelsedatauppsättningar med produktinteraktioner |
| Viktiga visualiseringar | Frihandstabeller, sammanfattningsnummer, trendlinjer | Flöde, utfall, kohort, attribuering | Samma som A eller B, plus målgruppspublicering | Funnel, trender, lojalitet, tillväxt |
| Aktiveringsfunktion | Nej (endast rapportering) | Nej (endast rapportering) | Ja (publicerar målgrupper till AEP) | Nej (endast rapportering) |
| Målgrupp krävs | Marknadsföringsanalytiker, kampanjchefer | Dataanalytiker, researkitekter | Analytiker + aktiveringsteam | Produktledare, tillväxtanalytiker |
| CJA-funktioner som används | Connection, Data View, Workspace, Computed Metrics, Dashboard | Connection, Data View, Workspace, Computed Metrics, Dashboard | Samma som A eller B, plus Audience Publishing | Anslutning, datavy, guidad analys, instrumentpanel |
| Dags att få första insikten | Dagar | Veckor | Veckor | Timmar-dagar |

### Välj rätt alternativ

Använd följande vägledning för att välja det implementeringsalternativ som bäst passar dina behov.

- **Om ditt primära mål är att mäta kampanjeffektivitet** och du har AJO kampanjdata som flödar till AEP börjar du med **Alternativ A**. Det ger snabbast time-to-value för rapportering av marknadsföringsprestanda.

- **Om du behöver förstå hela kundresan** på webben, i appar, via e-post och offline, och du har flera datauppsättningar med ett konsekvent person-ID, väljer du **Alternativ B**. Den ger de djupaste analysfunktionerna men kräver mer direkta investeringar i datavykonfiguration.

- **Om du vill agera utifrån insikter** genom att publicera segment som identifierats av CJA tillbaka till AEP för aktivering i RT-CDP eller AJO väljer du **Alternativ C**. Detta utökar alternativ A eller B med målgruppspublicering och kräver AEP kundprofilskonfiguration i realtid.

- **Om ditt team behöver snabba, strukturerade produktinsikter** utan att behöva bekymra sig om Workspace-projekt på fri hand, och din CJA SKU innehåller guidade analyser, väljer du **Alternativ D**. Det är den snabbaste vägen till att besvara specifika frågor om produktupplevelser.

- **Många organisationer implementerar flera alternativ**: Alternativ A för kontrollpaneler för marknadsföringsteam, alternativ B för analysteam:s flerkanalsanalys och alternativ D för självbetjäningsinsikter för produktteam. Dessa alternativ har samma CJA-anslutning och datavyinfrastruktur.

## Implementeringsfaser

I det här avsnittet beskrivs de stegvisa implementeringsfaserna för det här användningsmönstret.

### Fas 1: Dataanslutning

**Programfunktion:** CJA: Dataanslutning

Den här fasen konfigurerar en CJA-anslutning som binder en eller flera AEP-datauppsättningar till CJA för analys. Anslutningen definierar vilka datauppsättningar som flödar in i CJA, hur händelser sammanfogas över datauppsättningar via person-ID samt hur historiska data och strömmande data importeras. Detta är grundlänken mellan AEP datasjön och CJA.

#### Beslutspunkter

Följande beslut måste fattas under denna fas.

>[!NOTE]
>**Beslut: Val av AEP-sandlåda**
>
>Vilken AEP-sandlåda innehåller källdatauppsättningarna?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Produktionssandlåda | Live-kunddata för produktionsrapporter | Använd för produktionspaneler och rapporter från intressenter |
>| Utvecklingssandlåda | Testning och upprepning före driftsättning | Använd för inledande konfiguration och validering innan du befordrar till produktion |

>[!NOTE]
>**Beslut: Val av datauppsättning och typbeteckning**
>
>Vilka AEP-datauppsättningar ska ingå i anslutningen och vilken typ ska tilldelas?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Händelsedatamängder | Tidsstämplade beteendedata (webbinteraktioner, apphändelser, kampanjinteraktioner, transaktioner) | Kräv ett tidsstämpelfält, från kärnan i de flesta analyser |
>| Sök datauppsättningar | Referensdata för nyckelvärde (produktkatalog, kampanjmetadata, butiksplatser) | Ansluten till händelsedata via en delad nyckel; endast det senaste läget används |
>| Profildatamängder | Personnivåattribut (lojalitetsnivå, livstidsvärde, CRM-attribut) | Tillhandahåll anrikning på personnivå; endast det senaste tillståndet används |

>[!NOTE]
>**Beslut: Konfiguration av person-ID**
>
>Vilket fält fungerar som Person-ID för sammanfogning av korsdatauppsättningar?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| CRM-ID | Organisationen har en konsekvent CRM-identifierare i alla kanaler | Ger de mest korrekta funktionerna för sammanfogning över flera kanaler för kända kunder |
>| ECID (Experience Cloud-ID) | Analysera huvudsakligen anonyma webb-/appbeteenden | Enhetsomfattad; sammanfogar inte enheter utan identitetsupplösning |
>| E-post (hash) | E-post är den vanliga identifieraren för datauppsättningar | Fungerar bra när e-post samlas in på olika kontaktytor |
>| Anpassat namnutrymme | Organisationen använder en egen identifierare | Måste matcha ett AEP-identitetsnamnutrymme för publikation (alternativ C) |

>[!NOTE]
>**Beslut: Omfånget för bakgrundsfyllning**
>
>Hur mycket historiska data ska importeras till anslutningen?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Alla befintliga data | Maximalt historiskt djup krävs för årsjämförelser och långsiktiga trender | Det kan ta dagar att fylla i stora datauppsättningar (miljarder poster) |
>| Anpassat datumintervall | Bara den senaste historiken är relevant, eller så är lagringsoptimering ett bekymmer | Begränsar det historiska djup som är tillgängligt för analys |
>| Ingen bakgrundsfyllning | Endast framåtblickande analyser behövs | Snabbaste anslutningsinställning: inga historiska data är tillgängliga förrän nya data flödar i |

>[!NOTE]
>**Beslut: Direktuppspelningsaktivering**
>
>Bör nya data flöda in i CJA i nära realtid?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Aktivera direktuppspelning | Nära realtidsrapportering behövs (data är tillgängliga inom cirka 90 minuter efter AEP intag) | Det vanligaste för produktionsanslutningar; möjliggör snabb analys |
>| Endast batch | Periodisk uppdatering är tillräckligt och direktuppspelning behövs inte | Enklare konfiguration; data är tillgängliga efter gruppbearbetning |

#### Konfigurera dataanslutning

**Gränssnittsnavigering:** CJA > Anslutningar > Skapa ny anslutning

Information om nyckelkonfiguration:

- Anslutningens namn och beskrivning ska följa organisationens namnkonventioner
- Genomsnittligt antal dagliga händelser används för CJA kapacitetsplanering
- Alla datauppsättningar i en enda anslutning måste komma från samma AEP-sandlåda
- Personens ID-fält måste vara konsekventa i alla datauppsättningar för korrekt sammanfogning av datauppsättningar
- Kontrollera att fältet för person-ID finns och fylls i i varje datauppsättning innan du lägger till det i anslutningen

**Experience League-dokumentation:**

- [Anslutningar - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-connections/overview)
- [Skapa eller redigera en anslutning](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-connections/create-connection)
- [Hantera anslutningar](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-connections/manage-connections)
- [CJA skyddsräcken](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-admin/guardrails)

### Fas 2: Datavy configuration

**Programfunktion:** CJA: Datavy Configuration

Den här fasen konfigurerar en datavy som definierar hur anslutningsdata visas i analysen. Datavyn avgör vilka schemafält som exponeras som mått och mätvärden, hur värden tilldelas och bevaras, hur sessioner definieras och vilka härledda fält som omvandlar rådata till analysklara komponenter. Flera datavyer kan skapas från en enda anslutning för olika analytiska perspektiv.

#### Beslutspunkter

Följande beslut måste fattas under denna fas.

>[!NOTE]
>**Beslut: Namn på behållare**
>
>Vilken terminologi ska behållarna använda för att matcha affärsdomänen?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Standard (person/session/händelse) | Standardanalysterminologi förstås av teamet | Fungerar för de flesta implementeringar |
>| Egna namn (t.ex. Shopper/Besök/Interaktion) | Affärsdomänspecifik terminologi förbättrar användarens acceptans | Hjälper icke-tekniska intressenter att förstå analysomfånget |
>| B2B-namn (t.ex. konto/engagemang/kontaktyta) | B2B-analys där kontonivåanalys är fokus | Justerar behållaromfånget med B2B-affärskoncept |

>[!NOTE]
>**Beslut: Tidsgräns för session**
>
>Hur lång tid av inaktivitet definierar en sessionsgräns?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| 30 minuter (standard) | Sessionsdefinition för standardwebbanalys | Branschstandard; följer de flesta analysriktmärken |
>| 15 minuter | Korta formulär eller transaktionssajter där användarna snabbt utför uppgifter | Skapar fler sessioner; kan bättre fånga upp olika användaråtergivningar |
>| 60 minuter eller längre | Innehåll i lång form, komplexa B2B-interaktioner eller forskningskrävande resor | Färre sessioner; samlar in utökad forskning som enstaka sessioner |
>| Anpassad med nya sessionshändelser | Vissa händelser (t.ex. programstart, klickfrekvens för kampanj) ska alltid starta en ny session | Ger affärslogikdrivna sessionsgränser |

>[!NOTE]
>**Beslut: Standardvärden för attribueringsmodell**
>
>Vilken standardattribueringsmodell ska användas för konverteringsmått?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Senaste beröring (standard) | Krediten bör gå till den senaste kontaktytan före konvertering | Enkel och intuitiv; kan undervärdera informationskanaler |
>| Första beröringen | Förstå vilka kanaler som driver inledande medvetenhet och värvning | Användbar för förvärvsanalys; ignorerar kontaktytor |
>| Linjär | Alla kontaktytor ska ha samma kredit | Rättvis fördelning - kan påverka viktiga kontaktytor negativt |
>| Tidsminskning | Senaste kontaktytor bör få mer kredit än avlägsna | Återkommande saldon med historiskt bidrag |
>| U-formad | De första och sista kontaktytorna förtjänar störst kredit | Bra för att förstå både inköps- och slutkanaler |
>| Algoritmisk | Datadriven attribuering med CJA AI-modeller | Mest korrekt men kräver tillräcklig datavolym för konvertering |

>[!NOTE]
>**Beslut: Härledd fältlogik**
>
>Behövs anpassade affärsregler för att omvandla rådata till analysfärdiga dimensioner?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Klassificering av marknadsföringskanal (fall när) | Råspårningskoder måste klassificeras i kanalgrupper | Det vanligaste sättet att använda härledda fält; kritiskt för kanalanalys |
>| Värdebuckning | Kontinuerliga värden måste grupperas i intervall (t.ex. ordningsvärdenivåer) | Förenklar analys av kontinuerliga mätvärden |
>| Sammanfoga fält | Flera källfält ska kombineras till en enda dimension | Användbart när samma koncept finns i olika schemasökvägar för olika datauppsättningar |
>| Regex-baserad extraktion | Strukturerade värden måste tolkas (t.ex. extrahera kampanjtypen från kampanjkoden) | Kraftfull men kräver noggrann regex-mönsterdesign |

#### Konfigurera datavy

**Gränssnittsnavigering:** CJA > Datavyer > Skapa ny datavy

Information om nyckelkonfiguration:

- Välj den överordnade anslutningen som skapades i fas 1
- Konfigurera tidszon och kalendertyp för att matcha rapporteringskrav
- Mappa XDM-schemafält till dimensioner med lämpliga inställningar för beständighet (allokering och förfallodatum)
- Mappa XDM-schemafält till mått med format (decimal, heltal, valuta, procent, tid) och attribueringsinställningar
- Konfigurera inkluderings-/exkluderingsregler för dimensioner för att filtrera bort irrelevanta värden
- Aktivera vid behov avduplicering av mätvärden för att förhindra dubbelräkning
- Skapa härledda fält för klassificering av marknadsföringskanal, värdebuggning eller fältsammanslagning
- Maximalt 5 000 dimensioner och 5 000 mätvärden per datavy
- Max 100 härledda fält per datavy

#### Var alternativen skiljer sig

**För alternativ A (Kampanjresultatanalys):**

Mappa kampanjspecifika dimensioner: kampanjnamn, resenamn, kanaltyp, meddelandevariant, ämnesrad. Kartleveransstatistik: skicka, leverera, öppna, klicka, studsa, avsluta abonnemang. Konfigurera attribuering utifrån konverteringsstatistik baserat på kampanjmätningsfilosofi.

**För alternativ B (kundreseanalys):**

Mappa flerkanalsdimensioner: sidnamn, appskärm, kanal, kampanj, produkt, innehållstyp. Kartlägg engagemangs- och konverteringsstatistik över alla kanaler. Konfigurera flera attribueringsmodeller för jämförelseanalys. Skapa härledda fält för kanalklassificering och identifiering av resefas.

**För alternativ D (guidad analys):**

Mappa dimensioner och mått på händelsenivå som är relevanta för produktupplevelseanalys: funktionsnamn, användaråtgärd, typ av engagemang. Fokusera på händelser som definierar funnel steg, kvarhållningskriterier och tillväxtsignaler.

**Experience League-dokumentation:**

- [Översikt över datavyer](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/data-views)
- [Skapa eller redigera en datavy](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Översikt över komponentinställningar](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [Inställningar för beständighet](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [Attributinställningar](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [Formatinställningar](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/component-settings/format)
- [Metrisk deduplicering](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication)
- [Inkludera/exkludera värden](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/component-settings/include-exclude-values)
- [Sessionsinställningar](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/session-settings)
- [Härledda fält](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/derived-fields)

### Fas 3: Analys och metrisk framtagning

**Programfunktion:** CJA: Workspace Analysis, CJA: Guided Analysis, CJA: Computed Metric Creation

I den här fasen byggs arbetsytorna för analys (frihandsprojekt eller guidad analys), beräknade värden för härledda KPI:er, filter för segmenterad analys och anteckningar för viktiga händelser. Det är här som analysvärdet realiseras - skapa tabeller, visualiseringar och mätvärden som besvarar affärsfrågor.

#### Beslutspunkter

Följande beslut måste fattas under denna fas.

>[!NOTE]
>**Beslut: Analysmetod**
>
>Ska den här analysen använda frihandsprojekt från Workspace eller arbetsflöden för guidad analys?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Frihandsfigur Workspace (Alternativ A, B, C) | Djupgående undersökande analys, anpassade layouter, komplexa uppdelningar, avancerade visualiseringar | Maximal flexibilitet; kräver kunskaper från analytiker; stöder alla visualiseringstyper |
>| Guidad analys (alternativ D) | Strukturerade produktinsikter, snabba svar på specifika frågor, mindre tekniska användare | Snabbare insikt; begränsat till färdiga analystyper; sparar Workspace för ytterligare anpassning |
>| Båda | Organisationen behöver både djupgående analyser och snabbt strukturerade insikter | Använd guidad analys för vanliga frågor; Workspace för grundlig utforskning |

>[!NOTE]
>**Beslut: Visualiseringstyper**
>
>Vilka visualiseringar förmedlar bäst insikterna om detta användningsfall?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Frihandsregister | Detaljerad datautforskning med dimensionsanalyser | Grundläggande av de flesta analyser; stöder upp till 10 uppdelningsnivåer |
>| Flödesvisualisering | Förstå målningsbeteende (sidflöde, kanalövergångar) | Utmärkt för kartläggning av resevägar; kan vara komplicerat med hög kardinalitet |
>| Utfallsvisualisering | Mäta konvertering genom en definierad sekvens av kontaktytor | Bäst för funnel-analyser; visar tydligt hur mycket som faller bort i varje steg |
>| Kohortabell | Kvarhållningsanalys över tid genom förvärvskohort | Visar hur väl olika grupper behåller, vilket är viktigt för livscykelanalys |
>| Attributionspanelen | Jämföra attribueringsmodeller för konverteringsmått | Jämförelse av modell sida vid sida; kräver definition av en klar konverteringshändelse |
>| Sammanfattningsnummer/ändring | Executive KPI display with period-over-period comparison | Ren, snabb visning, idealisk för instrumentpanelsrubriker |

>[!NOTE]
>**Beslut: Beräknade måttformler**
>
>Vilka nyckeltal för företag kräver beräknade värden utöver de grundläggande datavyvärdena?
>
>| Mätmönster | Exempel på formel | När ska du använda |
>| --- | --- | --- |
>| Ratio / Hastighet | Beställningar/besök | Konverteringsgrad, klickfrekvens, studsfrekvens |
>| Filtrerade mått | Intäkter (där kanal = &quot;e-post&quot;) | Kanalspecifika eller segmentspecifika åtgärder |
>| Genomsnittligt per artikel | Intäkter/beställningar | Genomsnittligt ordervärde, intäkt per besök |
>| Sammansatt formel | (Inkomster - kostnad) / Inkomster | Marginalprocent, ROI-beräkningar |
>| Engagement score | Viktad summa av interaktioner | Sammansatt poängsättning av engagemang i alla kanaler |

#### Konfigurera analys och mätvärden

**Gränssnittsnavigering:**

- Workspace: CJA > Workspace > Projekt > Skapa projekt > Tomt projekt
- Guidad analys: CJA > Hem > Guidad analys (eller Workspace > Skapa > Guidad analys)
- Beräknade mått: CJA > Komponenter > Beräknade mått > Skapa
- Filter: CJA > Komponenter > Filter > Skapa filter

Information om nyckelkonfiguration:

- Välj datavyn som skapades i fas 2 som projektdatavy
- Ange lämpliga datumintervall och jämförelseperioder för analysen
- Bygg frihandstabeller genom att dra mått till rader och mätvärden till kolumner
- Lägg till dimensionsfördelningar för att utforska data på djupare nivåer (t.ex. kanal för kampanj, sida för produkt)
- Skapa återanvändbara filter (segment) för målgruppsspecifik analys (personnivå, sessionsnivå eller händelsenivå)
- Lägg till anteckningar för att markera viktiga affärshändelser (produktlanseringar, kampanjer, incidenter)
- Ange beräknat måttformat (decimal, percent, currency, time) och polarity (up is good / up is bad)
- Dela arbetsyteprojekt med CJA-användare som visar eller redigerar behörigheter

#### Var alternativen skiljer sig

**För alternativ A (Kampanjresultatanalys):**

Bygg frihandstabeller med kampanjdimensioner uppdelade efter leverans- och engagemangsmått. Skapa beräknade mätvärden för öppen ränta, klickfrekvens, konverteringsgrad, intäkt per meddelande och kampanjens avkastning. Lägg till trendvisualiseringar för att följa upp kampanjresultat över tid. Jämför kampanjvarianter med segmentjämförelse.

**För alternativ B (kundreseanalys):**

Skapa visualiseringar av bortfall för att identifiera bortfallspunkter för resan. Skapa flödesvisualiseringar för att identifiera navigeringsmönster över olika kanaler. Bygg kohorttabeller för att mäta kundlojalitet genom förvärvskohort. Konfigurera attribueringspanelen för att jämföra attribueringsmodeller för konverteringsmått. Skapa beräknade mätvärden för slutförandegrad av kundresor, poäng för flerkanalsengagemang och konvertering av livscykelstadium.

**För alternativ C (Analys med målgruppspublicering):**

Bygg analysarbetsytorna från alternativ A eller B och identifiera sedan segment med högt värde eller underpresterande under analysen. Skapa CJA-filter som fångar upp dessa segment för publicering i fas 5.

**För alternativ D (guidad analys):**

Välj lämplig analystyp baserad på affärsfrågan. Konfigurera nyckelhändelser, datumintervall, beräkningsmetoder och segmentjämförelser. Spara färdiga analyser som paneler i Workspace-projekt för ytterligare anpassning.

**Experience League-dokumentation:**

- [Workspace - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/home)
- [Skapa ett projekt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [Frihandsregister](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [Flödesvisualisering](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [Utfallsvisualisering](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [Kohortabell](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [Attributionspanelen](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [Uppdelningsdimensioner](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)
- [Översikt över filter](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [Skapa filter](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/cja-filters/create-filters)
- [Översikt över anteckningar](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/annotations/overview)
- [Översikt över beräknade mätvärden](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [Skapa beräknade mått](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [Beräknade mätfunktioner](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-functions)
- [Översikt över guidad analys](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/guided-analysis/overview)
- [Funnel view](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [Trendvyn](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/guided-analysis/trends/usage)
- [Bevarandevy](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/guided-analysis/retention/retention-rates)
- [Aktiv tillväxtvy](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/guided-analysis/user-growth/active)
- [Vy över engagemangsfrekvens](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/guided-analysis/trends/frequency)
- [Visa diseffekt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/guided-analysis/impact/release)
- [Innehållsanalys](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/content-analytics/content-analytics)

### Fas 4: Dashboard publishing

**Programfunktion:** CJA: Dashboard &amp; Scorecard Publishing

I den här fasen skapas interaktiva instrumentpaneler (Workspace-projekt) och mobilstyrkort som ger intressenterna transparens i nyckeltal. Instrumentpanelerna ger chefer och operativ insyn genom sammanfattningar, trendlinjer, delningar och anteckningar. Mobilstyrkort ger överskådliga prestandadata via mobilappen [!DNL Adobe Analytics] dashboards.

#### Beslutspunkter

Följande beslut måste fattas under denna fas.

>[!NOTE]
>**Beslut: Instrumentpanelstyp**
>
>Är detta en Workspace kontrollpanel, ett mobilstyrkort eller båda?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Workspace-projekt (skrivbord) | Detaljerade interaktiva paneler för analytiker och marknadsförare | Komplett visualisering med stöd för paneler, tabeller och komplexa layouter |
>| Mobil styrkort | En snabbtitt på nyckeltal för chefer och intressenter på mobila enheter | Begränsat till 16 rutor; sammanfattande siffror med trendminiatyrbilder; kräver mobilapp |
>| Båda | Organisationen behöver både detaljerad analys och mobilrapportering på ledningsnivå | Separata artefakter men kan dela samma datavy och beräknade värden |

>[!NOTE]
>**Beslut: Delningsmodell**
>
>Vem ska ta emot kontrollpanelen och hur?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Dela med specifika användare | Begränsad publik med specifika åtkomstbehov | Mest detaljstyrd; kräver individuell användarhantering |
>| Dela med produktprofilgrupp | Åtkomst på teamnivå justerad mot organisationsroller | Effektiv för hela teamet; hanteras via CJA produktprofiler |
>| Schemalägg e-postleverans | Återkommande PDF-/CSV-rapporter för intressenter som inte loggar in i CJA | Automatiserad leverans, maxfrekvens är timme; PDF- och CSV-format |

>[!NOTE]
>**Beslut: Synlighet för anteckning**
>
>Ska nyckelhändelser kommenteras på kontrollpanelens trendlinjer?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Ja - skapa anteckningar | Större kampanjer, produktlanseringar, webbplatsincidenter eller säsongshändelser kan förklara datatrender | Anteckningar visas som markörer på linjediagram och styrkortstrender. Ange kontext för dataroppar eller dips |
>| Nej | Instrumentpanelens målgrupp är bekant med företagskontext och kommentarer skulle göra arbetet tydligare | Enklare visuell presentation |

#### Konfigurera instrumentpaneler

**Gränssnittsnavigering:**

- Workspace kontrollpaneler: CJA > Workspace > Skapa projekt
- Mobil styrkort: CJA > Projekt > Skapa > Mobil styrkort
- Dela: CJA > Workspace > Dela > Dela med Workspace-användare
- Schemalagd leverans: CJA > Workspace > Dela > Schemalägg projekt

Information om nyckelkonfiguration:

- För mobilstyrkort skapar du plattor som visar ett enda mätvärde med ett summeringsnummer och glitteral-trend
- Konfigurera standarddatumintervall och jämförelseperioder (t.ex. de senaste 30 dagarna jämfört med föregående period eller månadsvis)
- Lägg till målgruppsfilter som cheferna kan växla mellan på mobila styrkort
- Konfigurera schemalagd e-postleverans för återkommande PDF- eller CSV-rapporter
- Max 16 paneler per mobilstyrkort; max 15 paneler per Workspace-projekt
- Anteckningar är begränsade till 100 per datavy

**Experience League-dokumentation:**

- [Skapa ett mobilstyrkort](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [Konfigurera och strukturera styrkort](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Adobe Analytics Dashboards - Executive Guide](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dashboards/set-up-execs)
- [Dela projekt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [Schemalägg projekt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [Visualisering av sammanfattningsnummer](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/visualizations/summary-number-change)
- [Datumintervall](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/date-ranges/overview)

### Fas 5: Målgruppspublicering (endast alternativ C)

**Programfunktion:** CJA: Audience Publishing

I den här fasen konfigureras CJA målgruppspublicering för att överföra analysidentifierade segment tillbaka till AEP kundprofil i realtid för aktivering nedströms i RT-CDP-destinationer, AJO-kampanjer eller AJO resor.

#### Beslutspunkter

Följande beslut måste fattas under denna fas.

>[!NOTE]
>**Beslut: Uppdatera cadence**
>
>Hur ofta ska målgruppsmedlemskapet uppdateras?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Engångsbild (ögonblicksbild) | Kampanjspecifik målgrupp som inte behöver uppdateras kontinuerligt | Ingen pågående bearbetning; måste publicera om för uppdateringar |
>| Var 4:e timme | Aktiveringskrav i nära realtid | Högre bearbetningskostnad - bäst för tidskänsliga målgrupper |
>| Dagligen | Standard marketing activation cadence | Balanserad färskhet och kostnad; det vanligaste alternativet |
>| Vecka | Stabila och långsamma målgrupper | Minimal bearbetning, lämplig för långfristiga segment |

>[!NOTE]
>**Beslut: Identitetsnamnområde**
>
>Vilket ID-namnutrymme ska CJA använda för målgruppsmedlemmens upplösning?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| CRM-ID | Organisationens primära kundidentifierare | Bästa noggrannhet för känd kundmatchning |
>| ECID | Primärt webb-/appbaserade målgrupper | Enhetsomfattad; kanske inte kan matchas till alla profilposter |
>| E-post (hash) | E-post är den vanliga identifieraren för aktivering | Måste matcha namnutrymmet som används i AEP-identitetskonfigurationen |
>| Anpassat namnutrymme | Egen identifierare som används i hela organisationen | Måste konfigureras i AEP Identity Service |

#### Konfigurera publikpublicering

**Gränssnittsnavigering:** CJA > Komponenter > Publiker > Publicera målgrupp

Information om nyckelkonfiguration:

- Definiera målgruppskriterier med CJA-filter (omfång för person, session eller händelsebehållare)
- Markera datavyn och filtret som ska publiceras
- Konfigurera identitetsnamnområdet för AEP-profilmatchning
- Ställa in cadence för uppdatering baserat på aktiveringsbehov
- Övervaka publiceringsstatus i listan CJA-publiker (Komponenter > Publiker > Statuskolumnen)
- Kontrollera att målgruppen visas i AEP Audience Portal (Publiker > Bläddra > Filtrera efter ursprung &quot;CJA&quot;)
- Max 75 publicerade målgrupper per CJA-kund (över alla sandlådor)
- Den inledande målgruppsutvärderingen kan ta upp till 24 timmar för stora datamängder

**Experience League-dokumentation:**

- [Översikt över målgrupper](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [Skapa och publicera målgrupper](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/audiences/publish)
- [Hantera målgrupper](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/audiences/manage)
- [Översikt över målgruppsportalen](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/ui/audience-portal)

## Implementeringsöverväganden

I det här avsnittet beskrivs hur man kan lösa säkerhetsproblem, vanliga fallgropar, bästa praxis och beslut om avvägning för det här användningsmönstret.

### Skyddsritningar och begränsningar

Följande skyddsförslag och begränsningar gäller för den här implementeringen.

- **Anslutningsgränser:** Det maximala antalet anslutningar per organisation begränsas av CJA SKU-berättigandet. En enda anslutning kan innehålla datauppsättningar från endast en AEP-sandlåda. — [CJA skyddsräcken](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-admin/guardrails)
- **Begränsningar i datavyn:** Maximalt 5 000 dimensioner och 5 000 mått per datavy. Max 100 härledda fält per datavy med upp till 5 nivåer av kapslade funktioner.
- **Begränsningar för Workspace:** Maximalt 40 paneler per projekt. Frihandsregister har stöd för upp till 10 dimensionsfördelningar på djupet. Högst 50 000 rader per rapportbegäran.
- **Styrkortsgränser:** Högst 16 plattor per mobilstyrkort.
- **Fördröjning vid direktuppspelning:** Direktuppspelningsdata är vanligtvis tillgängliga i CJA inom 90 minuter efter att AEP har tagit emot data.
- **Gränser för publikpublicering:** Maximalt 75 publicerade målgrupper per CJA-kund. Minsta uppdateringsgräns är var fjärde timme.
- **Begränsningar för guidad analys:** Funnel-analys stöder maximalt 15 steg. Segmentjämförelser har stöd för upp till tre segment samtidigt.

### Vanliga fallgropar

Tänk på följande vanliga problem när du implementerar det här mönstret.

- **Person-ID matchar inte i datauppsättningar:** Alla datauppsättningar i en anslutning måste använda ett konsekvent Person-ID-fält för korsdatauppsättningsanalys. Omatchade person-ID:n resulterar i fragmenterade kundvyer där samma person visas som flera personer. Verifiera enhetlighet för person-ID innan anslutningen skapas.

- **Backfill tar oväntat lång tid:** Stora datauppsättningar med miljarder poster kan ta dagar att fylla på nytt. Planera för detta under tidslinjer för implementering och börja fylla på igen tidigt. Övervaka förloppet i vyn för anslutningsinformation.

- **Datavy som visar &quot;Ospecificerad&quot; för de flesta dimensionsvärden:** Det mappade schemafältet kan vara glest ifyllt i källdata. Kontrollera om källdatauppsättningen har datakvalitet innan du antar ett konfigurationsfel. Använd ett härlett fält för att hantera null-värden.

- **Antalet sessioner verkar vara felaktigt:** Sessionens timeoutinställningar påverkar sessionsomfångets mått dramatiskt. En mycket kort timeout skapar fler sessioner och en mycket lång timeout skapar färre. Nya starthändelser för sessioner kan även fragmentera sessioner oväntat. Granska och testa sessionsinställningarna mot kända beteendemönster.

- **Attributionsmodellen används inte som förväntat:** Attributionsmodeller gäller bara för mått, inte dimensioner. Kontrollera att uppslagsfönstret är rätt inställt för affärscykeln. Kortare fönster kanske saknar tidiga kontaktpunkter från funnel.

- **Beräknade mått returnerar nollor eller oväntade värden:** Kontrollera att basmåtten som refereras i formeln har data i måldatavyn för det valda datumintervallet. Kontrollera om det finns division med noll i ratio-mått. Hämta måttdefinitionen och verifiera formelstrukturen.

- **Målgruppspubliceringen misslyckas (alternativ C):** CJA-anslutningen måste ha ett giltigt person-ID som matchar ett AEP ID-namnområde. Verifiera konfigurationen av identitetsnamnrymden och att AEP Real-Time Customer Profile är aktiverad i målsandlådan.

### God praxis

Följ dessa metodtips för en lyckad implementering.

- **Börja med en enda omfattande anslutning:** Skapa en anslutning som innehåller alla relevanta datauppsättningar och skapa sedan flera datavyer för olika analytiska perspektiv. Detta förhindrar att anslutningen sprider sig och förenklar hanteringen.

- **Använd härledda fält för klassificering av marknadsföringskanal:** Skapa härledda fält med alternativet Fall när logik används för att klassificera trafik i marknadsföringskanaler i stället för att förlita sig på spårningskoder för Raw. Detta garanterar en enhetlig kanalrapportering för alla analyser.

- **Skapa en måttordlista:** Dokumentera alla beräknade mätvärden med deras formler, avsedda användning och förväntade värdeintervall. Dela den här ordlistan med analysteamet för att säkerställa att mätvärdena används på ett konsekvent sätt i alla projekt.

- **Designa datavyer för er målgrupp:** Skapa separata datavyer för olika intressenter - en marknadsföringsdatavy med kampanjfokuserade mått och mätvärden, och en produktdatavy med funktioner och engagemangsdimensioner. Detta förenklar komponentlistorna för varje användargrupp.

- **Kommentera allt:** Skapa anteckningar för kampanjlanseringar, webbplatsändringar, tekniska incidenter, säsongsvariationer och alla händelser som kan förklara datatrender. Anteckningar ger ett viktigt sammanhang när du granskar instrumentpaneler flera månader senare.

- **Testa beräknade mätvärden mot manuella beräkningar:** Innan du förlitar dig på ett beräknat mätvärde för instrumentpaneler kör du en rapport med det beräknade mätvärdet och dess baskomponenter sida vid sida. Kontrollera att de beräknade värdena matchar en manuell beräkning.

- **Använd filter strategiskt:** Skapa återanvändbara filter för vanliga segmenteringsmönster (nya jämfört med att returnera, mobila jämfört med stationära datorer, baserat på geografisk plats). Använd dessa som panelnivåfilter i stället för att bädda in dem i alla frihandstabeller.

- **Övervaka anslutningshälsan regelbundet:** Kontrollera om det finns överhoppade poster, misslyckade batchar och fördröjda direktuppspelningar i vyn med anslutningsinformation. Datakvalitetsproblem på anslutningsnivå påverkar alla analyser i senare led.

### Avvecklingsbeslut

Tänk på följande när du planerar implementeringen.

>[!NOTE]
>**Avvikelse: Analysdjup kontra time-to-insight**
>
>Alternativ B (kundreseanalys) ger de djupaste flerkanalsinsikterna men kräver en betydande investering i anslutningskonfigurationen, datavydesign och härledd fältgenerering. Alternativ D (Guidad analys) ger snabbare insikt med strukturerade arbetsflöden men ger mindre analysflexibilitet.
>
>- **Alternativ B prioriterar:** Omfattande förståelse, komplex flerkanalsanalys, attribueringsmodellering, anpassad KPI-utveckling
>- **Alternativ D prioriterar:** Hastighet, tillgänglighet för icke-analytikeranvändare, frågor om strukturerade produktupplevelser
>- **Rekommendation:** Börja med alternativ D om du vill ha omedelbar produktinformation när du skapar alternativ B-infrastrukturen parallellt. Många organisationer kör båda samtidigt för olika team.

>[!NOTE]
>**Avvikelse: Fullständighet för bakgrundsfyllning kontra anslutningsberedskap**
>
>Import av alla historiska data ger maximalt analytiskt djup för årsjämförelser och långsiktig trendanalys, men efterfyllnad för stora datauppsättningar kan ta dagar. Om du begränsar bakåtfyllnaden till en nyligen använd period blir anslutningen klar snabbare, men historikanalysen begränsas.
>
>- **Alla data gynnar:** Långsiktig trendanalys, årsvisa jämförelser, kohortanalys med utökad historik
>- **Begränsad underfyllning prioriterar:** Snabbare anslutningsberedskap, kortare tid till första instrumentpanelen, lagringsoptimering
>- **Rekommendation:** Fyll i alla data för produktionsanslutningar som stöder strategisk analys. Använd begränsad backfill för utvecklingsanslutningar och koncepttestimplementeringar.

>[!NOTE]
>**Kompromiss: En heltäckande datavy jämfört med flera datavyer med fokus**
>
>En enda datavy med alla dimensioner och mått ger en enhetlig analytisk arbetsyta, men kan överbelasta användare med komponentlistor. Flera fokuserade datavyer (en per team eller användningsfall) förenklar komponentupplevelsen, men kräver att du underhåller flera konfigurationer.
>
>- **Vyn Enstaka data prioriterar:** Enhetlig analys, domänövergripande uppdelning, enklare hantering
>- **Flera datavyer prioriterar:** Renare komponentlistor, gruppspecifik terminologi, olika sessionsdefinitioner per användningsfall
>- **Rekommendation:** Börja med en primär datavy och skapa sedan ytterligare fokuserade datavyer om komplexiteten i komponentlistan blir ett hinder för implementering. Alla datavyer kan referera till samma anslutning.

>[!NOTE]
>**Brytning: Direktuppspelning i realtid kontra endast gruppinmatning**
>
>Om du aktiverar direktuppspelning på CJA-anslutningen får du nästan realtidsdata (inom cirka 90 minuter efter att AEP har tagit emot dem), men mer data bearbetas kontinuerligt. Intag av data endast i batch bearbetar regelbundet data och kan leda till förseningar.
>
>- **Direktuppspelning prioriterar:** Snabb rapportering, övervakning av aktiva kampanjer, instrumentpaneler i nära realtid
>- **Endast grupper:** Enklare konfiguration, förutsägbara bearbetningsfönster, tillräckligt för vecko- eller månadsrapportering
>- **Rekommendation:** Aktivera strömning för produktionsanslutningar. Kostnaden för inkrementell bearbetning är minimal jämfört med värdet av aktuella data för aktiv kampanjövervakning och kontrollpaneler för drift.

## Relaterad dokumentation

Följande resurser innehåller ytterligare information om det här användningsmönstret.

### [!DNL Customer Journey Analytics] - Komma igång

- [CJA - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-overview/cja-overview)
- [CJA skyddsräcken](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-admin/guardrails)

### Anslutningar

- [Anslutningar - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-connections/overview)
- [Skapa eller redigera en anslutning](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-connections/create-connection)
- [Hantera anslutningar](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-connections/manage-connections)

### Datavyer

- [Översikt över datavyer](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/data-views)
- [Skapa eller redigera en datavy](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Översikt över komponentinställningar](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [Inställningar för beständighet](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [Attributinställningar](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [Formatinställningar](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/component-settings/format)
- [Metrisk deduplicering](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication)
- [Inkludera/exkludera värden](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/component-settings/include-exclude-values)
- [Sessionsinställningar](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/session-settings)
- [Härledda fält](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/derived-fields)

### Workspace &amp; analys

- [Workspace - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/home)
- [Skapa ett projekt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [Frihandsregister](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [Flödesvisualisering](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [Utfallsvisualisering](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [Kohortabell](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [Attributionspanelen](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [Uppdelningsdimensioner](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)
- [Dela projekt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [Schemalägg projekt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [Exportera översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/export/export-cloud)

### Guidad analys

- [Översikt över guidad analys](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/guided-analysis/overview)
- [Funnel view](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [Trendvyn](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/guided-analysis/trends/usage)
- [Vy över engagemangsfrekvens](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/guided-analysis/trends/frequency)
- [Bevarandevy](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/guided-analysis/retention/retention-rates)
- [Aktiv tillväxtvy](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/guided-analysis/user-growth/active)
- [Visa diseffekt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/guided-analysis/impact/release)
- [Inslagsvy för första användning](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/guided-analysis/impact/first-use)
- [Tidslinjevy](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/guided-analysis/streams/timeline)

### Komponenter

- [Översikt över filter](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [Skapa filter](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/cja-filters/create-filters)
- [Översikt över beräknade mätvärden](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [Skapa beräknade mått](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [Beräknade mätfunktioner](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-functions)
- [Översikt över anteckningar](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/annotations/overview)
- [Datumintervall](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/date-ranges/overview)
- [Mätningskomponent](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/apply-create-metrics)

### Målgruppspublicering

- [Översikt över målgrupper](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [Skapa och publicera målgrupper](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/audiences/publish)
- [Hantera målgrupper](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-components/audiences/manage)

### Innehållsanalys

- [Innehållsanalys](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/content-analytics/content-analytics)
- [Content Analytics-konfiguration](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/config/configuration)

### Instrumentpaneler och styrkort

- [Skapa ett mobilstyrkort](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [Konfigurera och strukturera styrkort](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Adobe Analytics Dashboards - Executive Guide](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dashboards/set-up-execs)
- [Visualisering av sammanfattningsnummer](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/visualizations/summary-number-change)

### AEP Foundation

- [Datauppsättningar - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/catalog/datasets/overview)
- [XDM - systemöversikt](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/home)
- [Översikt över källor](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/home)
- [Översikt över identitetstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/home)
- [Översikt över målgruppsportalen](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/ui/audience-portal)

### Integrering med AJO

- [Integreringsguide för AJO + CJA](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [E-postrapport för kampanj](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/reporting/campaign-global-report-cja-email)
- [E-postrapport om resan](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/reporting/journey-global-report-cja-email)

### Självstudiekurser och guider

- [Grundläggande om schemakomposition](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [SDK - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/web-sdk/home)
- [Konfigurera datastreams](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
