---
title: Known-Visitor Web/App Personalization
description: Lär dig leverera personaliserat innehåll, erbjudanden eller kampanjer till identifierade besökare baserat på realtidsprofil och segmentmedlemskap.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 585adc0e-f528-4a09-b931-ef6b45fa8ec8
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '7968'
ht-degree: 1%

---

# Webbadress-/apppersonalisering för kända besökare

Den här referensplanen innehåller en fullständig implementeringshandbok för att leverera personaliserat innehåll till identifierade besökare över digitala ytor med [!DNL Adobe Journey Optimizer] (AJO) och [!DNL Adobe Real-Time Customer Data Platform] (RT-CDP). Det är utformat för lösningsarkitekter, marknadsföringsteknologer och implementeringstekniker som behöver förstå alla genomförbara implementeringsstrategier, de beslut som måste fattas i varje fas och den Experience League-dokumentation som stöder konfiguration.

Personalisering av webben/appar som är kända besökare är det primära personaliseringsmönstret för autentiserade digitala upplevelser. Till skillnad från anonym besökspersonalisering, som endast bygger på sessionsbeteendesignaler, utnyttjar det här mönstret den fullständiga enhetliga profilen: historiska beteendedata, segmentmedlemskap, lojalitetsnivå, inköpshistorik, livscykelstadium, beräknade attribut och benägenhetspoäng. Det har stöd för personalisering på webbsidor (via AJO webbkanal), mobilmeddelanden i appen och innehållskort.

I den här handboken presenteras alla genomförbara implementeringsalternativ - segmentbaserade, beslutsbaserade och flerytor - med kompromisser, beslutsvägledning och referenser till [!DNL Adobe Experience League]-dokumentation.

## Använd ärendeöversikt

Organisationer med autentiserade digitala resurser - e-handelsplatser, bankportaler, prenumerationstjänster, lojalitetsprogram, mobilappar - måste leverera personaliserade upplevelser som speglar varje kunds relation till varumärket. När en besökare loggar in eller identifieras via identitetsupplösning kan plattformen få tillgång till sin fullständiga enhetliga profil och leverera innehåll som är anpassat till deras specifika attribut, beteenden och inställningar.

Det här mönstret åtgärdar det scenario där en identifierad besökare kommer till en webbegenskap eller öppnar en mobilapp, och systemet måste avgöra vilket innehåll, erbjudande eller erbjudande som ska visas baserat på realtidsprofildata och målgruppsmedlemskap. Personaliseringsbeslutet fattas i kanten i millisekunder, vilket möjliggör leverans av underordnat innehåll utan märkbar fördröjning.

Mönstret stöder både deterministisk personalisering (där specifikt innehåll mappas till specifika målgruppssegment) och dynamisk beslutsfattande (där AJO Decisioning utvärderar behörighetsregler och rankningsstrategier för att välja det optimala innehållet per profil). Det omfattar flera digitala ytor - webbsidor, mobilmeddelanden i appen och innehållskort - vilket möjliggör enhetlig personalisering i hela kundens digitala resa.

## Viktiga verksamhetsmål

Följande affärsmål stöds av det här användningsmönstret.

### Leverera personaliserade kundupplevelser

Skräddarsy innehåll, erbjudanden och budskap efter enskilda preferenser, beteenden och livscykelsteg. Mer information finns i [Leverera personaliserade kundupplevelser](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md).

**KPI:er:** engagemang, konverteringsgrader, kundnöjdhet (CSAT)

### Öka webbplatsengagemanget

Förbättra tiden på webbplatsen, sidor per session och interaktion med webbinnehåll genom relevanta upplevelser. Mer information finns i [Öka webbplatsengagemanget](../../business-objectives/acquisition-growth/increase-website-engagement.md).

**KPI:er:** Tid på (webb) sida, engagemang, konverteringsgrader

### Öka mobilappsengagemanget

Öka den dagliga användningen, användningen av funktioner och konverteringar i appar genom personaliserade upplevelser i appen.

**KPI:er:** engagemang, lagring, konverteringsgrader

## Exempel på taktiska användningsfall

Nedan följer några vanliga taktiska implementeringar av det här mönstret:

- Personalisering av hemsidans hjälte efter lojalitetsskikt eller livscykelstadium - visa olika hjältebanners baserat på om kunden är ny, aktiv, i farozonen eller VIP
- Produktrekommendationsrapport baserad på inköpshistorik - ta fram relevanta produktförslag med hjälp av tidigare inköpsuppgifter och produkttillhörighetspoäng
- Personlig reklambanner per kundsegment - visa olika kampanjer för högvärdessegment, risksegment och nya kundsegment
- Meddelande i appen för mobilanvändare baserat på vilka funktioner som används - vägleder användarna till underutnyttjade funktioner baserat på deras användningsmönster
- Innehållskort med skräddarsytt erbjudande på kontouppsättningen - beständiga, diskreta erbjudanden skräddarsydda efter kundens profil
- Personaliserade priser eller rabatter baserade på kundnivå - visa nivåspecifika priser eller exklusiva rabatter för medlemmar i lojalitetsprogram
- Widget för korsförsäljningsrekommendation baserad på ägda produkter - föreslå kompletterande produkter eller tjänster baserat på den aktuella portföljen
- Anpassad navigering eller innehållsordning utifrån intressen - ändra ordning på innehållsmoduler eller navigeringselement baserat på dokumenterade inställningar

## Nyckeltal för prestanda

Följande nyckeltal hjälper till att mäta effekten av det här användningsmönstret.

| KPI | Mätningsmetod | Riktlinjer för prestandatester |
| --- | --- | --- |
| Personalization Engagement Rate | Klickningar och interaktioner med personaliserade element i innehållet delat med intryck | Personaliserat innehåll bör överträffa standardinnehållet med 20-50 % |
| Lyft konverteringsgrad | Konverteringsgrad för personaliserade upplevelser jämfört med kontroll-/standardupplevelser | Rikta 10-30 % högre kvalitet än icke-personaliserade upplevelser |
| Klickfrekvens (CTR) | Klicka på personaliserade CTA:er, erbjudanden och rekommendationer dividerat med intryck | Bildskärm per yta (webb, app, innehållskort) och per segment |
| Intäkter per besök | Intäkter från sessioner med personaliserade upplevelser | Jämför personaliserade kontra icke-personaliserade besökarkohorter |
| Interaktionshastighet för innehållskort | Innehållskortsklickningar och avaktiveringar i förhållande till visningar | Spåra per korttyp och målgruppssegment |
| Meddelandeengagemang i appar | Meddelandeinteraktioner i appen (CTA-klickningar, uppsägningar) i förhållande till visningar | Jämför målgruppssegment och meddelandetyper |
| Tid på sidan | Genomsnittlig tid för sidor med personaliserat innehåll jämfört med standard | Personaliserade sidor ska visa längre tid |
| Ansvarsfrekvens för erbjudande | Procent av beslutsvalda erbjudanden som resulterar i en konverteringshändelse | Spåra per erbjudande, per placering och per rankningsstrategi |

## Använd skiftlägesmönster

I det här avsnittet beskrivs kärnmönstret och dess funktionskedja.

**Webbadress-/apppersonalisering för kända besökare**

Leverera personaliserat innehåll, erbjudanden eller kampanjer till en identifierad besökare baserat på realtidsprofil och segmentmedlemskap på webben, mobiler i appen och innehållskortsytor.

**Funktionskedja:** Målgruppsutvärdering > Personalization Decisioning > Konfiguration av yta/kanal > Innehållsleverans > Impression Tracking > Reporting

## Tillämpningar

Följande program används i det här fallmönstret.

- **[!DNL Adobe Journey Optimizer](AJO)** - Konfiguration av webbkanal, konfiguration i appkanal, konfiguration av innehållskortskanal, beslut (urval och rankning av erbjudanden), meddelandeframställning (skräddarsytt innehåll), kampanjkörning, innehållsexperimenterande och rapportering
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)** - Målgruppsutvärdering (kant, direktuppspelning och batch), profilsökning via Edge Network i realtid, profilberikning med beräknade attribut och benägenhetspoäng
- **[!DNL Adobe Experience Platform](AEP)** - Profilarkiv, identitetstjänst, Web SDK, Mobile SDK, datastream-konfiguration, edge network delivery

## Foundationsfunktioner

Följande grundläggande funktioner måste finnas för det här användningsmönstret. För varje funktion anger statusen om den vanligtvis är obligatorisk, antas vara förkonfigurerad eller inte tillämplig.

| Foundational Function | Status | Vad måste finnas på plats | Experience League Reference |
| --- | --- | --- | --- |
| Administration och styrning | Antagen på plats | AJO sandlåda med konfigurerad webbkanal, in-app-kanal och beslutsbehörighet. Användare som etablerats med marknadsförings- och innehållsförfattarroller. | [Översikt över sandlådor](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/home), [Översikt över åtkomstkontroll](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Datamodellering och förberedelse | Obligatoriskt | Profilschemat måste innehålla attribut för personalisering och segmentering (t.ex. lojalitetsnivå, inköpshistorik, produktintressen, livscykelstadium). Experience Event-schema för interaktionsspårning och konverteringshändelser för webb/app. Datauppsättningar har aktiverats för [!DNL Real-Time Customer Profile]. | [Systemöversikt för XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [Grundläggande om schemakomposition](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| Datakällor och samling | Obligatoriskt | Web SDK implementeras på webbegenskaper för upplevelseleverans och visningsspårning. Mobile SDK implementeras i mobilappar för leverans av mediekort i appen. Datastream har konfigurerats med AJO-tjänst aktiverad för kantanpassning. Profildata i realtid som är tillgängliga vid sidan om för personalisering i undersekund. | [SDK-webböversikt](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home), [SDK-översikt för mobiler](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview), [Konfigurera datastreams](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure) |
| Konfiguration av identitet och profil | Obligatoriskt | Kända ID-namnutrymmen (CRM-ID, e-post, autentiserat användar-ID) har konfigurerats. Identitetssammanfogning mellan anonyma och autentiserade sessioner i drift för smidig övergång från anonym till personalisering av kända besökare. Edge kopplingsprofil konfigurerad med `isActiveOnEdge: true` för att matcha den autentiserade profilen vid kanten. | [Översikt över identitetstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [Översikt över sammanslagningsprinciper](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| Målgruppsdefinition och segmentering | Obligatoriskt | Målgrupper definierade med profilattribut, beteendedata och beräknade attribut. Utvärdering av Edge eller direktuppspelning har aktiverats för personalisering i realtid. Målgrupper som används för segmentbaserad personalisering måste vara kvalificerade för kantutvärdering. | [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [Edge-segmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation) |

## Stödfunktioner

Följande funktioner förstärker det här användningsmönstret, men behövs inte för att köra kärnan.

| Stödfunktioner | Status | Varför det spelar någon roll | Experience League Reference |
| --- | --- | --- | --- |
| Skapande av beräknat/härlett attribut | Rekommenderad | Beräknade attribut (t.ex. [!DNL Customer AI] benägenhetspoäng, livstidsvärde, engagemangspoäng, produkttillhörighet, dagar sedan senaste köpet) förbättrar personaliseringskvaliteten avsevärt genom att ge djupare signaler för målgruppsdefinition och innehållsval. | [Översikt över beräknade attribut](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview), [Översikt över AI för kunder](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview) |
| Livscykelhantering för data | Rekommenderad | Profil- och händelsedatalagringspolicyer säkerställer nya, relevanta data som ligger till grund för personaliseringsbeslut. Reglering av samtycke säkerställer att personaliseringen respekterar användarnas preferenser. | [Översikt över livscykelhantering av avancerade data](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home), [Medgivande i Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted) |
| Dataanvändningsetiketter och -tillämpning | Rekommenderad | Myndighetsetiketter på profilattribut som används för personalisering (särskilt PII-närliggande attribut som inköpshistorik, plats, finansiella data) säkerställer att dataanvändningsprinciperna följs. | [Översikt över datastyrning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [Översikt över etiketter för dataanvändning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/labels/overview) |
| Övervakning och observerbarhet | Rekommenderad | Prestandaövervakning för leverans och personalisering av Edge hjälper till att upptäcka latensproblem, leveransfel eller dataaktualitetsproblem som försämrar den personaliserade upplevelsen. | [Översikt över Insikter i observabilitet](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home), [Översikt över aviseringar](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview) |
| Rapportering och analys | Ingår | Personalization prestandarapportering ingår i Function Chain Step 6. [!DNL Customer Journey Analytics] Med hjälp av analys kan man göra djupgående utredningar om personaliseringens påverkan på konvertering, engagemang och intäkter mellan besökarsegment. | [CJA - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [AJO + CJA - integreringsguide](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo) |

## Programfunktioner

I den här planen används följande funktioner från programfunktionskatalogen. Funktioner mappas till implementeringsfaser i stället för till numrerade steg.

### [!DNL Journey Optimizer] (AJO)

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Kanalkonfiguration | Surface &amp; Channel Configuration | Konfigurera kanalytor för webben, appar och innehållskort för personalisering |
| Redigering av meddelanden | Innehållsutveckling | Skapa personaliserade varianter med dynamiskt innehåll, personaliseringsuttryck och villkorsstyrda block för varje yta |
| Kampanjkörning | Kampanjinställningar och aktivering | Skapa och aktivera webbkampanjer (schemalagda eller API-utlösta) som binder målgrupper, ytor och innehåll |
| Beslutsfattande | Beslutsinställningar (alternativ B/C) | Konfigurera beslutspolicyer med regler för behörighet, rankningsstrategier och erbjudanden/innehållsposter för dynamisk personalisering |
| Experimentera med innehåll | Optimering (valfritt) | Kör A/B-tester på personaliserade innehållsvarianter för att optimera prestandan |
| Frekvens och affärsregler | Kampanjinställningar och aktivering | Tvinga tryckfrekvenser för att förhindra överpersonalisering av trötthet |
| Rapportering och prestandaanalys | Rapportering och optimering | Övervaka personalisering, engagemang och konverteringsstatistik per yta och segment |

### [!DNL Real-Time CDP] (RT-CDP)

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Målgruppsutvärdering | Målgruppsdefinition och utvärdering | Definiera och utvärdera målgrupper med profilattribut, beteendedata och beräknade attribut med edge- eller streaming-utvärdering |
| Profilsökning i realtid | Content Delivery (runtime) | Få åtkomst till profilattribut och segmentmedlemskap i realtid via Edge Network för personaliseringsbeslut i mindre delar |
| Profilberikning | Före implementering (stöd) | Förbättra profiler med beräknade attribut, [!DNL Customer AI] poäng och aggregerade beteendesignaler som förbättrar personaliseringskvaliteten |

## Förutsättningar

Kontrollera följande innan du implementerar det här användningsmönstret:

- [ ] Web SDK implementerat på målwebbegenskaper med `alloy("sendEvent")` konfigurerat för sidvisningar och interaktionsspårning
- [ ] Mobile SDK implementerat i målmobilappar (om ytor i appen eller innehållskortet används)
- [ ] Datastream har konfigurerats med tjänsten [!DNL Adobe Journey Optimizer] aktiverad
- [ ] Profilschemat innehåller attribut som används för personalisering (kundlojalitetsnivå, inköpshistorik, produktintressen, livscykelstadium)
- [ ] Experience Event-schemat har konfigurerats för intrycks- och konverteringsspårning
- [ ] kända identitetsnamnutrymmen har skapats och identitetskoppling fungerar mellan anonyma (ECID) och autentiserade identiteter
- [ ] Edge-sammanslagningsprincip konfigurerad med `isActiveOnEdge: true`
- [ ] målgrupper definierade med kvalificerade bedömningar för personalisering i realtid
- [ ] Innehållsresurser (bilder, kopia, CTA) förberedda för varje personaliseringsvariant
- [ ] Personalization strategi dokumenterad: vilka attribut styr vilket innehåll, för vilka ytor

## Implementeringsalternativ

I det här avsnittet beskrivs de tillgängliga implementeringsmetoderna för det här användningsmönstret.

### Alternativ A: Segmentbaserad webbanpassning

**Bäst för:** Deterministisk personalisering där specifika innehållsvarianter mappas direkt till målgruppssegment - lojalitetsskiktsspecifika hjältebanners, livscykelfasmeddelanden, kampanjinnehåll för kundsegment. Idealiskt när mappningen av innehåll till segment är väldefinierad och inte kräver dynamisk rankning eller optimering.

**Så här fungerar det:**

Segmentbaserad personalisering mappar innehållsvarianter direkt till målgruppssegment. När en känd besökares profil utvärderas mot kanter som är kvalificerade vid sidinläsning avgör systemet vilka segment besökaren tillhör och visar motsvarande innehållsvariant. Markeringen baseras på segmentmedlemsprioritet - om en besökare kvalificerar sig för flera segment visas det högprioriterade segmentets innehåll.

Den här metoden använder AJO webbkanalskampanjer (eller kampanjer i appen/innehållskortet) med regler för villkorat innehåll eller flera målinriktningskonfigurationer. Varje målgruppssegment är kopplat till en viss innehållsupplevelse. Ingen beslutsmotor är inblandad - logiken för innehållsval är helt segmentstyrd.

Innehåll skapas med hjälp av AJO gränssnitt för meddelandeframställning med dynamiska innehållsblock som återger olika innehåll baserat på målgruppsmedlemskap eller profilattribut. Web SDK eller Mobile SDK levererar personaliserade upplevelser i realtid via Edge Network.

**Viktiga överväganden:**

- Innehållsvarianter måste skrivas i förväg för varje segment
- Segmentdefinitioner måste vara kvalificerade för att kvalificera sig i realtid
- Om du lägger till nya segment eller innehållsvarianter måste kampanjkonfigurationen uppdateras
- Innehållsvalet är deterministiskt - samma segment ser alltid samma innehåll

**Fördelar:**

- Enkelt att implementera och underhålla med tydlig mappning av innehåll till segment
- Enkelt att förstå och förklara personaliseringslogiken för intressenter
- Ingen decimaloverhead - snabbare innehållsupplösning
- Full kontroll över vilket innehåll varje segment får

**Begränsningar:**

- Begränsad flexibilitet när antalet segment och innehållsvarianter ökar
- Det går inte att dynamiskt optimera innehållsvalet baserat på profilnivåsignaler utanför segmentmedlemskapet
- För att lägga till nya innehållsvarianter krävs manuella kampanjuppdateringar
- Stöder inte scenarier där flera erbjudanden konkurrerar om samma placering

**Experience League:**

- [Kom igång med webbkanalen](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [Skapa webbupplevelser](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [Dynamiskt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)

### Alternativ B: Beslutsbaserad personalisering

**Passar bäst för:** Dynamisk personalisering där det optimala innehållet eller erbjudandet måste väljas per profil med hjälp av regler för behörighet och rangordningsstrategier - näst bästa erbjudandet om hemsida, personaliserade produktrekommendationer, dynamiskt val av kampanjbanderoll. Idealiskt när flera erbjudanden eller innehållsobjekt konkurrerar om samma placering och systemet måste välja den bästa.

**Så här fungerar det:**

Beslutsbaserad personalisering använder AJO Decisioning för att utvärdera varje besökares profil mot en katalog med innehållsobjekt eller erbjudanden, tillämpa regler för behörighet för att avgöra vilka artiklar som är kvalificerade och sedan tillämpa en rangordningsstrategi (prioritetsbaserad, formelbaserad eller AI-rankad) för att välja den optimala posten för varje placering.

Implementeringen innefattar att skapa placeringar (där innehåll visas), definiera erbjudanden med regler för behörighet och innehållsangivelser, ordna erbjudanden i samlingar och skapa beslutspolicyer som knyter placeringar till samlingar med rankningsstrategier. När en besökare läser in en sida under körningen utvärderar Edge Network beslutspolicyn mot besökarens profil och returnerar det valda erbjudandeinnehållet.

Detta tillvägagångssätt stöder sofistikerade personaliseringsscenarier, inklusive nästa bästa erbjudande, personaliserade kampanjer med capping och AI-optimerat innehållsval. Erbjudandena kan ha begränsningar per profil och global begränsning, giltighetsdatumintervall och komplexa behörighetskriterier som kombinerar profilattribut och målgruppsmedlemskap.

**Viktiga överväganden:**

- Kräver en bättre konfiguration (praktik, erbjudanden, regler för behörighet, samlingar, beslut)
- Rankningsstrategier kan vara prioritetsbaserade (manuella), formelbaserade (anpassade uttryck) eller AI-rankade (automatisk optimering)
- AI-rankning kräver minst 1 000 konverteringshändelser för modellutbildning
- Räknare för buffertbegränsning kan ha en viss fördröjning under scenarier med hög genomströmning
- Ett reserverbjudande måste konfigureras för fall där inget personligt erbjudande kvalificerar sig

**Fördelar:**

- Dynamiskt val av innehåll per profil utan hårdkodad mappning av segment till innehåll
- Stöder komplexa kriterier för behörighet och rankningslogik
- AI-rankat alternativ möjliggör automatisk optimering utan manuell åtgärd
- Erbjudandebegränsning förhindrar överexponering av visst innehåll
- Centraliserad hantering av erbjudanden - erbjudandena kan återanvändas i kampanjer och kanaler

**Begränsningar:**

- Komplexare implementering än segmentbaserad personalisering
- AI-rankningen kräver en tillräcklig volym för konverteringshändelser för utbildning
- Bedömningen av beslut lägger till marginell fördröjning jämfört med direktleverans av segmentbaserat innehåll
- Formelbaserad rankning kräver noggrann design för att undvika oavsiktlig prioritering

**Experience League:**

- [Beslutsledning - översikt](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Skapa personaliserade erbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Skapa beslut](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Rankningsstrategier](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

**Hur detta skiljer sig från offertbeslutsalternativ B:**

Infrastrukturen är identisk - båda använder AJO Decisioning i toppklass med Web SDK och en fullödig kopplingsstrategi. Skillnaden är vad som markeras. Det här alternativet hanterar innehållsobjekt där urvalskriterierna är anpassning (segmentmedlemskap, beteenderangordning). [Erbjudandebeslut för ](offer-decisioning.md) Alternativ B hanterar en styrd erbjudandekatalog där berättiganderegler, begränsningar och giltighetsfönster är affärskrav. Om din objektuppsättning kräver att man får ett visst antal bilder per profil, begränsningar av behörigheten enligt gällande bestämmelser eller livscykelhantering, ska du använda Offer Decision Option B i stället.

### Alternativ C: Flersidig anpassning (webb + i-app + innehållskort)

**Passar bäst för:** Enhetlig personalisering på flera digitala ytor - leverera samordnade personaliserade upplevelser på webbsidor, mobilmeddelanden i appen och innehållskort. Idealiskt när organisationen har både webb- och mobilappsegenskaper och vill ha en enhetlig personaliseringslogik över alla digitala kontaktytor.

**Så här fungerar det:**

Flersidig personalisering innebär att antingen Alternativ A (segmentbaserad) eller Alternativ B (beslutsbaserad) kan användas för att leverera personaliserat innehåll över flera AJO-ytor. Varje yttyp - webb, i appen, innehållskort - kan ha olika innehållsformat och leveransmekanismer, men den underliggande personaliseringslogiken (målgruppsmedlemskap eller -beslut) delas.

Implementeringen innefattar att konfigurera kanalytor för varje yttyp, skapa ytspecifikt innehåll (HTML/CSS för webbytor, strukturerade meddelanden för applayouter, kortlayouter för innehållskort) och skapa kampanjer som riktar sig mot rätt yta. Web SDK hanterar webbpublicering medan Mobile SDK hanterar distribution av appar och innehållskort.

Innehållskort är särskilt användbara för beständiga, icke-reflekterade meddelanden på kontomontroller eller apphemskärmar. Meddelanden i appen är idealiska för sammanhangsberoende, sessionsspecifik kommunikation. Webbpersonalisering hanterar hjältebanners, rekommendationswidgetar och marknadsföringsmaterial.

**Viktiga överväganden:**

- Varje yttyp kräver en egen kanalytkonfiguration och egen innehållsredigering
- SDK och Mobile SDK måste implementeras och konfigureras
- Innehållet måste utformas för varje ytformat (olika dimensioner, layouter, interaktionsmönster)
- Delade målgrupper och beslutslogik säkerställer enhetlighet mellan olika ytor
- Testningen måste omfatta alla yttyper över olika enheter

**Fördelar:**

- Enhetlig personaliseringsupplevelse över alla digitala kontaktytor
- Delad målgrupp och beslutslogik minskar behovet av duplicering
- Innehållskort ger en bestående, icke-påträngande personaliseringsyta
- Meddelanden i appen möjliggör sammanhangsbaserad, sessionsspecifik personalisering på mobilen

**Begränsningar:**

- Högsta komplexitet vid implementering - kräver konfiguration för varje yttyp
- Kräver både Web SDK och Mobile SDK
- Innehållet måste utformas och underhållas för varje ytformat
- Testningen ökar med varje ytterligare yttyp

**Experience League:**

- [Översikt över kanaler i appen](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/get-started-in-app)
- [Innehållskortskanal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/get-started-content-card)
- [Kom igång med webbkanalen](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)

### Jämförelse av alternativ

I följande tabell jämförs de tre implementeringsalternativen.

| Kriterier | Alternativ A: Segmentbaserad | Alternativ B: Beslutsbaserad | Alternativ C: Flera ytor |
| --- | --- | --- | --- |
| Bäst för | Känd segmentering-till-innehåll-mappning | Dynamiskt val av innehåll per profil | Enhetlig personalisering över webben + mobiler |
| Komplex | Lågt | Medium-High | Hög (bygger på A eller B) |
| Latens | Snabbaste (direkt segmentupplösning) | Något högre (bedömning av beslut) | Beroende på underliggande alternativ (A eller B) |
| Flexibilitet | Begränsat till fördefinierade segmentinnehållspar | Hög - dynamisk rankning och behörighet | Högsta - flera ytor med delad logik |
| Innehållshantering | Manuell mappning av segment till innehåll | Centraliserat offertbibliotek med regler för behörighet | Innehåll per yta med delad personaliseringslogik |
| Optimering | Manuell A/B-testning | AI-rankad automatisk optimering tillgänglig | Optimering per yta |
| Kräver | Edge-berättigade målgrupper, Web SDK | Placeringar, erbjudanden, regler för behörighet, beslut | SDK + Mobile SDK, flera ytkonfigurationer |
| Ytor som stöds | Webb (primär) | Webb (primär) | Webb + In-App + Innehållskort |

### Välj rätt alternativ

Börja med följande frågor för att välja rätt implementeringsmetod:

1. **Hur många ytor?** Om du behöver personalisering på både webben och i mobilappar väljer du alternativ C (som bygger på antingen A eller B för den underliggande logiken). Om du bara använder webben väljer du mellan A och B.

2. **Hur dynamiskt är ditt innehållsval?** Om du har en väldefinierad mappning av segment till innehållsvarianter (t.ex. 3-5 lojalitetsnivåer, var och en med en viss hjältebanderoll), väljer du alternativ A. Välj Alternativ B om du behöver välja från en katalog med erbjudanden med komplex behörighet och rangordning.

3. **Behöver du AI-optimerad markering?** Om du vill att systemet automatiskt ska lära sig och optimera vilket innehåll som fungerar bäst för varje profil väljer du Alternativ B med AI-rankat beslut.

4. **Hur många innehållsvarianter?** Om du har färre än 10 innehållsvarianter med tydliga segmentmappningar är alternativ A enklare. Om du har dussintals erbjudanden som behöver filtrering och rankning för behörighet, kan alternativ B skalas bättre.

5. **Planerar du att utöka till andra kanaler?** Om er beslutslogik så småningom ska kunna leverera erbjudanden via e-post, webben och andra kanaler, utgör alternativ B den centraliserade beslutsgrunden som beslutsprocessen för flerkanalserbjudanden sträcker sig över.

## Implementeringsfaser

I det här avsnittet går vi igenom varje fas av implementeringen i detalj.

### Fas 1: Definiera målgrupper och konfigurera utvärdering

**Programfunktion:** RT-CDP: Målgruppsutvärdering

**Vad du ska konfigurera:** Definiera de målgrupper som driver val av innehåll för personalisering. Dessa målgrupper representerar de besökarsegment som kommer att få personaliserade upplevelser - lojalitetsnivåer, livscykelstadier, beteendekohorter eller produkttillhörighetsgrupper.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>**Beslut: Målgruppsutvärderingsmetod**
>
>Hur snabbt måste målgruppsmedlemskapet lösas för personalisering? Detta påverkar direkt om personalisering kan ske vid sidinläsning eller kräver en fördröjning.
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Edge-utvärdering | Webb-/apppersonalisering i realtid som kräver subsekundskvalificering | Begränsat till enkel kontroll av profilattribut och segmentmedlemskap. Inga tidsseriefrågor eller komplexa aggregeringar. Krävs för personalisering av kända besökare. |
>| Utvärdering av strömning | Nära realtidskvalifikationer när profiler når/avslutar målgrupper baserat på beteendehändelser | Stöder enstaka händelser och tidsbegränsade fönsterfrågor. Målgruppsförändringarna återspeglas på bara några minuter. Passar för ytor i appen och på innehållskortet där en viss fördröjning är acceptabel. |
>| Batchutvärdering | Dagens målgrupp uppdateras för segment baserat på komplexa aggregeringar eller historiska mönster | Funktioner för helsegmentsregler. Passar inte för personalisering i realtid, men kan komplettera gränspubliken med komplexa, förberäknade segment. |

>[!NOTE]
>**Beslut: Personalization-attribut**
>
>Vilka profilattribut ska leda till målgruppsdefinition och innehållsval?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Profilattribut (lojalitetsnivå, livscykelstadium) | Deterministisk personalisering baserad på kända kundegenskaper | stabila, väldefinierade attribut. Enkelt att mappa till innehållsvarianter. Tillgängligt vid kanten om profilen är korrekt konfigurerad. |
>| Beteendesignaler (inköpshistorik, surfmönster) | Personalization baserat på nyligen använda beteenden och engagemangsmönster | Kräver beräknade attribut eller direktuppspelningssegment. Mer dynamiskt men mer komplext att underhålla. |
>| Propensitetspoäng ([!DNL Customer AI]) | Prediktiv personalisering baserad på sannolikhet för konvertering, bortfall eller inköp | Kräver beräknade attribut. Möjliggör sofistikerad personalisering men kräver utbildningsdata för ML-modeller. |
>| Kombinerad metod | De flesta produktionsimplementationer | Använder profilattribut för primär segmentering med beteendesignaler och benägenhetspoäng för förfining. |

**Gränssnittsnavigering:** Kund > Målgrupper > Skapa målgrupp > Skapa regel

**Information om nyckelkonfiguration:**

- Definiera målgrupper med hjälp av Segment Builder med segmentregeluttryck som refererar till profilattribut
- Se till att uttryck för segmentregler är kvalificerade för kantutvärdering (enkla attributkontroller, segmentmedlemskap)
- Konfigurera kvalificerade målgrupper för personalisering i realtid
- Överväg att hindra målgrupper att utesluta nyligen konverterade eller avanvisade besökare

**Experience League-dokumentation:**

- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Edge segmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Direktuppspelningssegmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Profile Query Language referens](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### Fas 2: Ställ in beslut (endast alternativ B och C)

**Programfunktion:** AJO: Bestämning

**Vad du ska konfigurera:** Konfigurera beslutsstrukturen som dynamiskt väljer det optimala innehållet eller erbjudandet för varje besökare. Detta omfattar praktik (där erbjudanden visas), erbjudanden (vilket innehåll som är tillgängligt), regler för behörighet (vem som kvalificerar), rangordningsstrategier (hur man väljer det bästa) och beslutsstrategier (hur allt hänger samman).

**Beslutspunkter i den här fasen:**

>[!NOTE]
>**Beslut: Rankningsstrategi**
>
>Hur ska berättigade erbjudanden rangordnas för att välja den bästa för varje besökare?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Prioritetsbaserad (manuell) | Enkla användningsfall med tydlig erbjudandehierarki | Varje erbjudande har ett manuellt prioritetsvärde. Erbjudandet om högsta prioritet vinner. Lätt att förstå och kontrollera. |
>| Formelbaserat (anpassat uttryck) | Vid rankning bör profilattribut beaktas | Anpassade rankningsformler, referensprofildata (t.ex. poäng per lojalitetsnivå + senaste). Flexibelt men kräver formeldesign och testning. |
>| AI-rankad (automatisk optimering) | När du vill att systemet automatiskt ska optimera urvalet av erbjudanden | ML-modellen lär sig vilka erbjudanden som fungerar bäst för vilka profiler. Kräver minst 1 000 konverteringshändelser för utbildning. Passar bäst för utplaceringar med hög trafik. |

>[!NOTE]
>**Beslut: Erbjudandet gäller endast**
>
>Bör det finnas begränsningar för hur många gånger ett erbjudande visas för en besökare eller för alla besökare?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Anfang per profil | Förhindra att trötthet ser samma erbjudande upprepade gånger | Begränsar intryck per besökare under en tidsperiod. Garanterar variation i den personaliserade upplevelsen. |
>| Global ändpunkt | Begränsa antalet visningar för ett erbjudande eller erbjudande med begränsad tillgänglighet | Förser alla besökare med summor. Användbart för kampanjer i begränsat antal. |
>| Ingen ände | Löpande innehåll eller alltid relevanta erbjudanden | Inga gränser för intryck. Passar för beständigt innehåll som banners för lojalitetsnivåer. |

**Gränssnittsnavigering:** [!DNL Journey Optimizer] > Komponenter > Beslutshantering

**Information om nyckelkonfiguration:**

- Skapa placeringar för varje yta där erbjudanden visas (webbanderoll, meddelandeområde i appen, innehållskortplats)
- Definiera regler för behörighet med hjälp av segmentregeluttryck som refererar till profilattribut och målgruppsmedlemskap
- Skapa personaliserade erbjudanden med innehållsrepresentationer för varje placering
- Skapa ett reserverbjudande som omfattar alla placeringar (visas när inget anpassat erbjudande kvalificerar sig)
- Organisera erbjudanden med samlingskvalificerare (taggar) och gruppera i samlingar
- Skapa en bindningsplacering för beslutspolicy för samlingar med den valda rankningsstrategin

**Experience League-dokumentation:**

- [Skapa placeringar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Skapa beslutsregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Skapa personaliserade erbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Skapa reserverbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Skapa samlingar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Skapa beslut](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Rankningsstrategier](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Fas 3: Konfigurera ytor och kanaler

**Programfunktion:** AJO: Kanalkonfiguration

**Så här konfigurerar du:** Konfigurera de kanalytor som definierar var personaliserat innehåll ska levereras. För varje yttyp (webb, i appen, innehållskort) krävs en egen konfiguration som anger parametrarna för yt-URI, innehållsformat och leverans.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>**Beslut: Målytor**
>
>Vilka digitala ytor får personaliserat innehåll?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Endast webbkanal | Personalization fokuserar på webbegenskaper | Kräver Web SDK. Enklast implementering. Omfattar hjältebanners, reklamområden, rekommendationswidgetar. |
>| Endast i appkanalen | Personalization fokuserar på mobilappsupplevelser | Kräver Mobile SDK. Täcker sammanhangsbaserade, sessionsspecifika meddelanden i programmet. |
>| Endast mediekortkanal | Beständiga, avfärdade personaliserade meddelanden | Kräver Mobile SDK eller Web SDK. Korten behålls tills de stängs. Idealiskt för instrumentpaneler och hemskärmar. |
>| Flera ytor (alternativ C) | Enhetlig personalisering på webben och i mobilen | Kräver både Web SDK och Mobile SDK. Varje yta behöver separat konfiguration och innehåll. |

>[!NOTE]
>**Beslut: Konfigurationsmetod för webbyta**
>
>Hur ska webbytan konfigureras för innehållsleverans?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Single-page application (SPA) | Moderna webbappar med routning på klientsidan | Använd `renderDecisions: true` i Web SDK `sendEvent`-anrop. Innehåll som återges automatiskt av SDK. |
>| Flersidigt program (MPA) | Traditionella serveråtergivna webbsidor | Innehåll som levereras på sidan läses in via Edge Network svar. Kan kräva ytans URI-konfiguration på sidnivå. |

**Gränssnittsnavigering:** [!DNL Journey Optimizer] > Administration > Kanaler > Kanalytor

**Information om nyckelkonfiguration:**

- För webbytor: konfigurera webbytans URI som matchar målsidan/målsidorna
- För ytor i appen: konfigurera mobilappsytan med program-ID och yttyp
- För innehållskortsytor: konfigurera innehållskortsytan med program-ID eller webbkontext
- Kontrollera att datastream har AJO-tjänsten aktiverad för kantanpassning

**Experience League-dokumentation:**

- [Kom igång med webbkanalen](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [Webbkanalskonfiguration](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/web-configuration)
- [Krav för kanaler i appen](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/inapp-configuration)
- [Konfiguration av innehållskort](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/content-card-configuration)

### Fas 4: Skapa innehåll

**Programfunktion:** AJO: Meddelanderedigering

**Så här konfigurerar du:** Skapa anpassade innehållsvarianter för varje yta och segment eller erbjudande. Detta innefattar att utforma den visuella layouten, lägga till anpassningsuttryck som refererar till profilattribut, konfigurera villkorliga innehållsblock och skapa återanvändbara innehållsfragment.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>**Beslut: Innehållsstrategi**
>
>Hur ska personaliserat innehåll struktureras för det här användningsfallet?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Villkorliga innehållsblock | Olika innehållsavsnitt i samma layout varierar beroende på målgrupp | Enskilt innehåll med villkorliga regler. Effektivt för mindre variationer (rubrik, CTA-text, bildbyte). |
>| Separata innehållsvarianter per behandling | I grund och botten olika layouter och designer per publik | Flera kompletta innehållsresurser. Mer flexibel men mer att underhålla. Krävs för innehållsexperimenterande. |
>| Beslutsstyrt innehåll | Innehåll som väljs dynamiskt från en erbjudandekatalog | Erbjud representationer som definierar innehållet. Innehållshanteringen är centraliserad i erbjudandebiblioteket. |

>[!NOTE]
>**Beslut: Personalization-djup**
>
>Hur mycket av innehållet ska personaliseras?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Personalisering på Surface-nivå | Endast specifika element är personaliserade (hjältebild, CTA, banner) | Lägre komplexitet. Fokuserad personalisering på områden med stor effekt. Den vanligaste startpunkten. |
>| Helsidesanpassning | Hela sidlayouten eller innehållsordningen är personaliserad | Högre komplexitet. Kräver omfattande innehållsskapande. Ger den mest skräddarsydda upplevelsen. |
>| Personalisering på tokennivå | Inline-personaliseringstoken (namn, nivå, poängbalans) | Enklast form. Infogar profilattributvärden i annars statiskt innehåll. |

**Gränssnittsnavigering:** [!DNL Journey Optimizer] > Kampanjer > Skapa kampanj > Redigera innehåll

**Var alternativen skiljer sig:**

**För alternativ A (segmentbaserad):**

- Skapa innehållsvarianter för varje målgruppssegment med webbdesignern eller kodredigeraren
- Använd dynamiska innehållsblock med villkor som bygger på målgruppsmedlemskap
- Konfigurera anpassningsuttryck som refererar till profilattribut (t.ex. `{{profile.person.name.firstName}}`, `{{profile.loyalty.tier}}`)
- Ställ in villkorsregler för att visa olika innehåll baserat på segmentmedlemskap

**För alternativ B (beslutsbaserat):**

- Författare erbjuder innehållsrepresentationer för varje placering som definieras i fas 2
- Varje erbjudande har en eller flera representationer (HTML, image, JSON) som matchar placeringar
- Integrera beslutsmaterial på webbsidan eller i appen genom att bädda in beslutsunderlag
- Innehållet väljs dynamiskt vid körning - redigeringen fokuserar på individuella erbjudanden

**För alternativ C (flera ytor):**

- Skapa ytspecifikt innehåll för varje målyta (webb-HTML/CSS, strukturerat meddelande i appen, innehållskortslayout)
- Bibehåll en konsekvent personaliseringslogik på alla ytor samtidigt som den anpassar sig till varje ytas formatbegränsningar
- Testa innehållsåtergivning för varje yttyp

**Experience League-dokumentation:**

- [Skapa webbupplevelser](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [Lägg till personalisering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization syntax](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Dynamiskt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Hjälpfunktioner](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Leverera erbjudanden i meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Skapa meddelanden i appen](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/create-in-app)
- [Skapa innehållskort](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/create-content-card)

### Fas 5: Konfigurera och aktivera kampanjer

**Programfunktion:** AJO: Kampanjkörning

**Vad du ska konfigurera:** Skapa och aktivera AJO-kampanjen som binder målgruppen, ytan och innehållet tillsammans för leverans. För webbpersonalisering är kampanjer vanligtvis konfigurerade för omedelbar eller kontinuerlig aktivering i stället för att skickas en gång.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>**Beslut: Kampanjtyp**
>
>Hur ska personaliseringskampanjen aktiveras?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Schemalagd kampanj (alltid aktiverad) | Kontinuerlig personalisering som fungerar kontinuerligt för alla kvalificerade besökare | Ange startdatum som omedelbart och inget slutdatum. Kampanjen är aktiv tills den stoppas manuellt. De vanligaste för webbpersonalisering. |
>| Schemalagd kampanj (tidsbunden) | Personalization knutet till en viss kampanjperiod | Ange start- och slutdatum. Kampanjen stoppas automatiskt efter slutdatumet. Passar för säsongskampanjer eller tidsbegränsade erbjudanden. |
>| API-utlöst kampanj | Personalization utlöses av en specifik programhändelse | Utlöses programmatiskt. Användbart när personalisering endast ska visas som svar på specifika systemhändelser. |

>[!NOTE]
>**Beslut: Frekvensbegränsning**
>
>Ska visningsfrekvensen begränsas för den här personaliseringen?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Använd frekvensregler | Kampanjbaserad eller erbjudandebaserad personalisering som skulle kunna trösta besökarna | Förhindrar att samma personalisering visas för många gånger. Konfigureras via AJO affärsregler. |
>| Ingen frekvens | Löpande innehållspersonalisering (lojalitetsskiktsbanderoll, dashboard-innehåll) | Alltid relevant innehåll som inte orsakar trötthet. Inga gränser för intryck behövs. |

**Gränssnittsnavigering:** [!DNL Journey Optimizer] > Kampanjer > Skapa kampanj

**Information om nyckelkonfiguration:**

- Välj webbkanalen, appkanalen eller innehållskortkanalen och den yta som konfigurerats i fas 3
- Bind målgruppen som definieras i fas 1
- Länka innehållet som skapats i fas 4
- Konfigurera kampanjschemat (omedelbart, datumintervall eller API-utlöst)
- Granska och aktivera kampanjen
- För innehållsexperimenterande: aktivera experimentell växling, definiera behandlingar, ange trafikallokering och framgångsmått innan aktivering

**Experience League-dokumentation:**

- [Skapa en kampanj](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Kom igång med kampanjer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Frekvensregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Kom igång med innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Skapa ett innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)

### Fas 6: Spåra visningar och samla in data

**Programfunktion:** AEP: Datakällor och samling

**Vad du ska konfigurera:** Se till att visningar, interaktioner och konverteringar från personaliserade upplevelser spåras tillbaka till plattformen för rapportering, omvärdering av målgrupper och optimering av beslut.

**Information om nyckelkonfiguration:**

- Verifiera att Web SDK skickar `decisioning.propositionDisplay` händelser när anpassat innehåll återges
- Verifiera att Web SDK skickar `decisioning.propositionInteract` händelser när besökare interagerar med personaliserat innehåll (klickningar, uppsägningar)
- För Mobile SDK: verifiera att interaktionshändelser för meddelanden och innehållskort fångas in i appen
- Konfigurera spårning av konverteringshändelser för framgångsmått (inköp, registreringar, användning av funktioner)
- Se till att händelser innehåller ett förslag-ID för attribuering till specifika personaliseringsbeslut

**Experience League-dokumentation:**

- [SDK - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Spåra händelser med Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/sendevent/overview)
- [Mobile SDK - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)

### Fas 7: Rapportera och optimera

**Programfunktion:** AJO: Rapportering och prestandaanalys, rapportering och analys

**Vad du ska konfigurera:** Konfigurera prestandaövervakning och analys för att mäta personaliseringseffektivitet över ytor, segment och innehållsvarianter. Använd AJO-inbyggda rapporter för driftsstatistik och [!DNL Customer Journey Analytics] för flerkanalsanalyser av affärsmässiga konsekvenser.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>**Beslut: Rapporteringsomfattning**
>
>Vilken analysnivå krävs för det här personaliseringsfallet?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Endast inbyggda AJO-rapporter | Operativ övervakning av leverans- och engagemangsmått | Inbyggda kampanjrapporter med bild-, klicknings- och konverteringsdata. Snabbast att konfigurera. |
>| CJA flerkanalsanalys | Djupanalys av personaliseringens påverkan på affärsresultatet | Kräver CJA-anslutning och datavy. Möjliggör funnel-analys, kohortjämförelser och attribueringsmodellering i alla kanaler. |
>| Både AJO och CJA | Fullständig operativ och analytisk synlighet | Använd AJO för den dagliga övervakningen och CJA för strategisk analys. Rekommenderas för produktionsimplementationer. |

**Gränssnittsnavigering:**

- AJO-rapporter: Kampanjer > Välj kampanj > Visa rapport
- CJA: Projekt > Skapa nytt projekt

**Information om nyckelkonfiguration:**

- Få tillgång till kampanjliverapporter under aktiv personalisering
- Granska historiska rapporter för slutförda kampanjer eller periodisk analys
- För CJA: konfigurera en anslutning med AJO Experience Event-datauppsättningar och skapa en datavy med personaliseringsstatistik
- Bygg kontrollpaneler för att spåra personalisering, konverteringshöjning, acceptansgrad för erbjudanden och intäkter per besök
- För beslutsbaserad personalisering (alternativ B): övervaka resultatet genom placering och rankningsstrategi

**Experience League-dokumentation:**

- [Kampanjrapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Global kampanjrapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Rapport om innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Analysis Workspace - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Integreringsguide för AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

## Implementeringsöverväganden

Detta avsnitt behandlar skyddsförslag, vanliga fallgropar, bästa praxis och beslut om avräkning som är relevanta för detta användningsmönster.

### Gardrutor och begränsningar

- Edge Network-sökningar har en svarstid på mindre än 200 ms för edge-evaluate-segment - [Kundprofilsgardiner i realtid](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Maximalt 4 000 segmentdefinitioner per sandlåda - [Segmenteringsskyddsräcken](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Edge-segment är begränsade till enkla attributkontroller och segmentmedlemsfrågor - inga tidsseriefrågor — [Edge-segmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- Endast en sammanslagningsprincip kan vara aktiv i Edge per sandlåda: [Sammanfoga principer](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- Högst 10 000 godkända anpassade erbjudanden per sandlåda - [Beslutshanteringssystem](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Max 30 placeringar per beslut - [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- AI-rankningsmodeller kräver minst 1 000 konverteringshändelser för utbildning
- Erbjud svarstid för leverans SLA är mindre än 500 ms vid P95 för förfrågningar med en enda omfattning
- Max 500 aktiva live-kampanjer per sandlåda - [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Högst 25 aktiva beräknade attribut per sandlåda - [Beräknade attributskyddsräcken](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)

### Vanliga fallgropar

- **Edge-sammanslagningsprincip har inte konfigurerats:** Utan en edge-active-sammanslagningsprincip kan inte Edge Network matcha den autentiserade profilen, vilket gör att personaliseringen misslyckas eller återgår till anonymt beteende. Kontrollera att exakt en sammanfogningsprincip har `isActiveOnEdge: true` i sandlådan.
- **Målgruppen är inte kantberättigad:** Om målgruppsregeluttryck använder tidsseriefrågor, komplexa aggregeringar eller `inSegment()` referenser till endast gruppsegment kvalificerar de sig inte för kantutvärdering och kan inte driva realtidspersonalisering. Validera kantens behörighet under målgruppsdefinitionen.
- **Gapet för identitetsmatchning vid autentisering:** När en besökare övergår från anonym till autentiserad kan det vara en kort stund då profilen ännu inte har åtgärdats. Kontrollera att identitetssammanfogningen är korrekt konfigurerad och att webb-SDK skickar den autentiserade identiteten via `identityMap` omedelbart vid inloggning.
- **Saknat reserverbjudande vid beslut:** Om inget reserverbjudande har konfigurerats och inget anpassat erbjudande kvalificerar för en besökare returneras tomt innehåll, vilket skapar en skadad upplevelse. Konfigurera alltid ett reserverbjudande som omfattar alla placeringar.
- **SDK för webben skickar inte förslagsvisningshändelser:** Om `renderDecisions` är inställt på `true` men visningshändelser inte skickas, kommer rapporteringen inte att återspegla faktiska visningar. Verifiera händelsespårning genom att granska nätverksbegäranden i webbläsarutvecklingsverktyg.
- **Innehållsflimmer vid sidinläsning:** Om anpassat innehåll inte är fördolt under beslutsanropet kan besökarna se standardinnehåll kort innan det ersätts. Använd det fördolda fragmentet eller CSS-baserad fördöljning för att eliminera flimmer.

### God praxis

- Börja med segmentbaserad personalisering (alternativ A) för den första implementeringen och gå sedan vidare till beslutsbaserad (alternativ B) i takt med att erbjudandekatalogen växer och optimeringsbehovet ökar
- Använd topprankade målgrupper när det är möjligt för personalisering i realtid; reservera strömnings- och batchmålgrupper för kompletterande ändamål
- Implementera innehållsexperiment på personaliserade upplevelser för att validera att personalisering ger mätbar lyft över standardinnehåll
- Designa personalisering med en graciös strategi för nedgradering - om profilen inte kan lösas i full skala visar du väldesignat standardinnehåll istället för en trasig upplevelse
- Använd beräknade attribut för att skapa personaliseringssignaler med högt värde som engagemangsmusik, produkttillhörighet och dagar sedan det senaste köpet, vilket förbättrar både segmentbaserad och beslutsbaserad personaliseringskvalitet
- upprätthålla en innehållsstyrningsprocess för att säkerställa att personaliserat innehåll hålls aktuellt, varumärkesanpassat och följer alla typer av gränssnitt
- Övervaka personalisering efter segment för att identifiera vilka målgrupper som drar störst nytta av personalisering och var lyften är som störst

### Avvecklingsbeslut

>[!NOTE]
>**Avvikelse: Personalization granularitet jämfört med komplexitet i innehållshantering**
>
>Mer detaljerad personalisering (fler segment, fler innehållsvarianter, fler ytor) ger allt mer skräddarsydda upplevelser, men kräver proportionellt mer arbete med att skapa, underhålla och styra innehåll.
>
>- **Högre detaljrikedom:** Bättre kundupplevelse, högre engagemang, starkare konverteringslyft
>- **Lägre granularitet prioriterar:** Snabbare implementering, lägre underhållsbörda, enklare styrning
>- **Rekommendation:** Börja med 3-5 segment med stor effekt (t.ex. lojalitetsnivåer eller livscykelfaser) med tydlig innehållsdifferentiering. Expandera granulariteten baserat på uppmätt prestandaökning. Använd decimering (alternativ B) för att skala granulariteten utan proportionell ökning av innehållshanteringen.

>[!NOTE]
>**Brytning: Realtidsbeslut kontra deterministisk innehållskontroll**
>
>Beslutsbaserad personalisering (alternativ B) ger dynamisk optimering men minskar den direkta kontrollen över vilket innehåll varje besökare ser. Segmentbaserad personalisering (alternativ A) ger full deterministisk kontroll men begränsar dynamisk optimering.
>
>- **Beslutsfattare:** Skalbarhet, automatisk optimering, komplexa berättigandescenarier
>- **Segmentbaserade fördelar:** Förutsägbarhet, efterlevnadskontroll, intressentgenomskinlighet
>- **Rekommendation:** Använd segmentbaserad personalisering för kompatibilitetskänsligt innehåll (regelmeddelanden, nivåspecifik prissättning) där exakt kontroll krävs. Använd beslut för kampanjinnehåll, erbjudanden och rekommendationer där dynamisk optimering ger mervärde.

>[!NOTE]
>**Avvikelse: Edge datatillgänglighet jämfört med personaliseringsrikedom**
>
>Personalisering som utvärderas av Edge begränsas till attribut som är tillgängliga i edge-profilbutiken. Mer omfattande personaliseringssignaler (fullständig beteendehistorik, komplexa beräknade attribut) kan kräva sökning på serversidan eller förberäkning.
>
>- **Endast Edge prioriterar:** Undersekund latens, enklast arkitektur
>- **Förberäknad berikning prioriterar:** Detaljerade personaliseringssignaler, mer avancerade målgruppsdefinitioner
>- **Rekommendation:** Använd beräknade attribut för att i förväg samla in avancerade beteendesignaler till profilattribut som är tillgängliga på kanten. Detta ger en mängd beteendedata med hastigheten på kantutvärderingen.

## Relaterad dokumentation

Följande resurser innehåller ytterligare information om de tekniker och konfigurationer som det hänvisas till i den här handboken.

### Webbkanalspersonalisering

- [Kom igång med webbkanalen](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [Skapa webbupplevelser](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [Webbkanalskonfiguration](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/web-configuration)

### Kanaler i appen och innehållskortet

- [Översikt över kanaler i appen](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/get-started-in-app)
- [Krav för kanaler i appen](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/inapp-configuration)
- [Skapa meddelanden i appen](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/create-in-app)
- [Innehållskortskanal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/get-started-content-card)
- [Konfiguration av innehållskort](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/content-card-configuration)
- [Skapa innehållskort](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/create-content-card)

### Beslutsledning

- [Beslutsledning - översikt](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Skapa placeringar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Skapa beslutsregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Skapa personaliserade erbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Skapa reserverbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Skapa samlingar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Skapa beslut](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Rankningsstrategier](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [Leverera erbjudanden i meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### Personalization och innehåll

- [Lägg till personalisering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization syntax](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Hjälpfunktioner](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Dynamiskt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Arbeta med innehållsmallar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Arbeta med innehållsfragment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)

### Målgrupper och segmentering

- [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Edge segmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Direktuppspelningssegmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Profile Query Language referens](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### Identitet och profil

- [Översikt över identitetstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Översikt över namnutrymmen för identiteter](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/namespaces)
- [Länkningsregler för identitetsdiagram](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)
- [Profilöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [Översikt över kopplingsprofiler](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### Datainsamling och SDK

- [SDK - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Installera SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
- [Mobile SDK - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Konfigurera datastreams](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Edge Network Server API - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)

### Kampanjer och experiment

- [Kom igång med kampanjer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Skapa en kampanj](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Kom igång med innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Skapa ett innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Rapport om innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)

### Beräknade attribut och anrikning

- [Översikt över beräknade attribut](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Användargränssnittshandbok för beräknade attribut](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)
- [Översikt över AI för kunder](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### Rapportering och analys

- [Kampanjrapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Global kampanjrapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Integreringsguide för AJO + CJA](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [CJA - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Analysis Workspace - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

### Styrning och integritet

- [Översikt över dataförvaltning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Samtycke i Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [Översikt över livscykelhantering av avancerade data](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)

### Skyddsräcken

- [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Garantier för kundprofiler i realtid](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Garantier för identitetstjänst](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)
