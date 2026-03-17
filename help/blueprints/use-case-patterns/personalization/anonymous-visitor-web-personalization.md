---
title: Anonym besökare på Personalization
description: Lär dig hur du levererar personaliserat webbinnehåll till oidentifierade besökare baserat på sessionsbeteendesignaler.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: e2446801-ffce-40e6-bfe9-abec623c9201
source-git-commit: ccfd8c987a0090ca690e15a4bd89f4d96ec9c01f
workflow-type: tm+mt
source-wordcount: '8076'
ht-degree: 0%

---

# Webbanpassning för anonyma besökare

Denna referensplan ger implementeringsvägledning för att leverera personaliserat webbinnehåll till anonyma (oidentifierade) besökare baserat på sessionsbeteendesignaler. Den täcker hela implementeringens livscykel - från [!DNL Web SDK]-konfiguration och edge-målgruppsdefinition till innehållsleverans och resultatrapportering - och är utformad för lösningsarkitekter, marknadsföringsteknologer och implementeringstekniker som arbetar med [!DNL Adobe Journey Optimizer] (AJO), [!DNL Adobe Real-Time Customer Data Platform] (RT-CDP) och [!DNL Adobe Experience Platform] (AEP).

Använd den här planen för att förstå arkitekturen, utvärdera implementeringsalternativ, fatta välgrundade konfigurationsbeslut och hitta relevant Experience League-dokumentation för varje implementeringsfas.

Mönstret fungerar med begränsade data - bara det som kan observeras i den aktuella sessionen och alla anonyma kantprofiler som samlats in från tidigare besök på samma enhet eller cookie. Detta gör det lämpligt för personalisering på topp-of-funnel där besökaren inte har något konto eller inte har autentiserats.

## Använd ärendeöversikt

Ett anonymt besöks-Personalization på webben som tar upp behovet av att leverera relevant, personaliserat innehåll till besökare som ännu inte har identifierats - de har inte loggat in, saknar känd identitet och kan inte matchas mot en enhetlig kundprofil. Trots den här begränsningen kan meningsfull personalisering uppnås med beteendesignaler i sessioner: visade sidor, tid på plats, rullningsdjup, hänvisningskälla, geografisk plats, enhetstyp och UTM-kampanjparametrar.

Det här mönstret använder AJO webbkanalsytor och kodbaserade upplevelser för att ändra sidinnehåll i realtid. Edge segmentering är den primära utvärderingsmetoden eftersom beslut måste fattas med en mindre fördröjning när besökaren navigerar på webbplatsen. [!DNL Web SDK] samlar in beteendesignaler och skickar dem till [!DNL AEP Edge Network], där utvärderade målgruppsregler avgör vilken innehållsvariant som ska levereras.

Till skillnad från webbpersonalisering/appanpassning för kända besökare, som utnyttjar den fullständiga enhetliga profilen och segmentmedlemskapet, begränsas det här mönstret till data som kan observeras i den aktuella sessionen och alla anonyma kantprofiler som är kopplade till besökarens ECID ([!DNL Experience Cloud ID]). Den här skillnaden är viktig för implementeringsplanering: de beteendesignaler som är tillgängliga för personalisering är begränsade till vad [!DNL Web SDK] hämtar och vad som finns kvar i edge-profilarkivet för sessioner via den cookie-baserade ECID:t.

## Viktiga verksamhetsmål

Följande affärsmål stöds av det här användningsmönstret.

**[Öka webbplatsengagemanget](../../business-objectives/acquisition-growth/increase-website-engagement.md)**

Förbättra tiden på plats, sidor per session och interaktion med webbinnehåll genom relevanta upplevelser som är skräddarsydda för anonyma besökarsignaler.

| KPI:er |
| --- |
| Tid på (webb) sida |
| Engagemang |
| Konverteringsgrader |

**[Leverera personaliserade kundupplevelser](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**

Skräddarsy innehåll, erbjudanden och budskap efter individuella preferenser, beteenden och livscykelsteg - även för besökare som ännu inte har identifierat sig själva.

| KPI:er |
| --- |
| Engagemang |
| Konverteringsgrader |
| Nöjda kunder (CSAT) |

**[Öka konverteringsgraden](../../business-objectives/revenue-monetization/increase-conversion-rates.md)**

Förbättra andelen besökare och presumtiva som slutför önskade åtgärder som inköp, registreringar eller inskickade formulär genom att presentera det mest relevanta innehållet baserat på beteendesammanhang.

| KPI:er |
| --- |
| Konverteringsgrader |
| Leadkonvertering |
| Kostnad per lead |

## Exempel på taktiska användningsfall

I följande exempel visas specifika scenarier där mönstret kan användas.

- **A/B-test på landningssida baserat på hänvisningskälla** - Testa olika rubriker för besökare som kommer från Google, sociala medier eller direkttrafik för att optimera engagemanget genom förvärvskanalen
- **Rekommendationer för kategoritillhörighet baserade på webbläsarbeteende** - Visa rekommendationer för produkt eller innehåll baserat på sidor som visas i den aktuella sessionen för att öka identifiering och konvertering
- **Avsluta avsiktligt erbjudande för besökare som ska lämna** - Visa ett kampanjerbjudande eller lead-formulär när beteendesignaler indikerar att besökaren håller på att överge webbplatsen
- **Geografisk marknadsföringsbanderoll** - Visa platsspecifika kampanjer, butiksplaceringsinnehåll eller regionala erbjudanden baserat på besökarens geografiska plats
- **Enhetsspecifik innehållslayoutoptimering** - Anpassa innehållslayout, bildstorlekar och CTA-placering baserat på om besökaren befinner sig på skrivbordet, surfplattan eller mobilen
- **Nytt jämfört med att returnera besökarens välkomstmeddelande** - Differentiera upplevelsen för förstagångsbesökare jämfört med att returnera anonyma besökare med hjälp av ECID-beständighet mellan sessioner
- **Innehållsrekommendationer baserade på visade sidor i den aktuella sessionen** - Visa relaterade artiklar, produkter eller resurser dynamiskt baserat på de sidor som besökaren redan har visat
- **Dynamisk hjältebanderoll baserad på UTM-kampanjparametrar** - Anpassa hjältebanderollen så att den matchar meddelandet eller kreativiteten från den refererande kampanjen

## Nyckeltal för prestanda

Använd följande nyckeltal för att mäta effektiviteten för det här användningsmönstret.

| KPI | Beskrivning | Mätningsmetod |
| --- | --- | --- |
| Personalization Impression Rate | Procentandel av berättigade sidvisningar där personaliserat innehåll levererades | AJO kampanjrapport: antal visningar |
| Klickfrekvens (CTR) | Procentandel personaliserade visningar som resulterar i ett klick | AJO kampanjrapport: klickningar/visningar |
| Engagement Lift | Ökad tid på sidor, sidor per session eller rullningsdjup för anpassat innehåll jämfört med standardinnehåll | Jämförelse av CJA arbetsyta: personaliserad kohort jämfört med kontroll |
| Konverteringsgrad | Procentandel besökare som exponeras för personaliserat innehåll som slutför en önskad åtgärd | CJA funnel-analys: exponering > interaktion > konvertering |
| Studsfrekvens - reducering | Minska antalet personliga sessioner för besökare som tar emot personaliserat innehåll | CJA sessionsanalys: studsfrekvens delta för personaliserade kontra standardvärden |
| Experimentell Win-hastighet | Procentandel A/B-tester som ger en statistiskt signifikant vinnare | AJO-experimentrapport: experiment med tröskelvärde för konfidensgrad |

## Använd skiftlägesmönster

Nedan beskrivs kärnmönstret och funktionskedjan för det här användningsexemplet.

**Anonym besökare på Personalization**

Leverera personaliserat innehåll baserat på sessionsbeteendesignaler för oidentifierade besökare via AJO webbkanal.

**Funktionskedja:** Webbplatskonfiguration > Beteenderegelutvärdering > Innehållsleverans > Impression Tracking > Reporting

## Tillämpningar

Följande program används i det här fallmönstret.

- **[!DNL Adobe Journey Optimizer](AJO)** - Konfiguration av webbkanalsyta, innehållsutveckling (webb- och kodbaserade upplevelser), kampanjkörning, innehållsexperiment (A/B-testning), beslut (dynamiskt innehållsval) och rapportering
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)** - Edge-segmentering för målgruppsutvärdering i realtid baserad på beteendesignaler i sessioner; anonym hantering av kantprofiler
- **[!DNL Adobe Experience Platform](AEP)** - [!DNL Web SDK] för beteendesignalinsamling, [!DNL Edge Network] för dataroutning och personalisering i realtid, datastream-konfiguration

## Foundationsfunktioner

Följande grundläggande funktioner måste finnas för det här användningsmönstret. För varje funktion anger statusen om den vanligtvis är obligatorisk, antas vara förkonfigurerad eller inte tillämplig.

| Funktionen Foundation | Status | Vad måste finnas på plats | Experience League referens |
| --- | --- | --- | --- |
| Administration och styrning | Antagen på plats | AJO-sandlåda med konfigurerad behörighet för webbkanal. [!DNL Web SDK] implementeringsbehörigheter och dataåtkomst som ges till implementeringsteamet. Användare med roller som tillåter konfiguration av webbkanaler, målgruppshantering och kampanjkörning. | [Översikt över åtkomstkontroll](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Datamodellering och förberedelse | Obligatoriskt | Experience Event-schema för att hämta webbbeteendesignaler (sidvyer, klickningar, rullningsdjup, hänvisningsdata, UTM-parametrar). Schemat måste innehålla standardfältgrupper för webbinteraktion och vara aktiverat för edge-profiler för att ge stöd för realtidsutvärdering. En motsvarande datauppsättning måste skapas och profilaktiveras. | [Översikt över XDM-systemet](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home) |
| Datakällor och samling | Obligatoriskt | [!DNL Web SDK] måste implementeras på alla målwebbegenskaper med en datastream konfigurerad att dirigera data till [!DNL AEP Edge Network]. Datastream måste ha tjänsterna [!DNL Adobe Experience Platform] och [!DNL Adobe Journey Optimizer] aktiverade. Detta är ett kritiskt beroende - utan [!DNL Web SDK] är det inte möjligt att samla in eller leverera beteendesignaler. | [SDK - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home) |
| Konfiguration av identitet och profil | Obligatoriskt | ECID ([!DNL Experience Cloud ID]) har konfigurerats som primär identitetsnamnrymd för anonyma besökare. Edge kopplingsprofil måste konfigureras med `isActiveOnEdge: true` för att anonyma profildata ska kunna matchas. Endast en sammanfogningsprincip kan vara aktiv för kant per sandlåda. | [Översikt över identitetstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home) |
| Målgruppsdefinition och segmentering | Obligatoriskt | Edge utvärderade målgruppssegment som definieras baserat på sessionsbeteendesignaler. Edge-segmentering är obligatoriskt för undersekundsutvärdering av fördröjning. Segmentregler får endast använda edge-eligibility segment rule expressions (enkla attributkontroller och segmentmedlemskap - inga tidsseriefrågor eller komplexa aggregeringar). | [Edge-segmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation) |

## Stödfunktioner

Följande funktioner förstärker det här användningsmönstret, men behövs inte för att köra kärnan.

| Stödfunktioner | Status | Varför det spelar någon roll | Experience League referens |
| --- | --- | --- | --- |
| Skapande av beräknat/härlett attribut | Ej tillämpligt | Begränsat värde för anonyma besökare eftersom det finns minimala historiska profildata att sammanställa. Kan bli tillämpligt om edge-profilen samlar in meningsfulla beteendedata från tidigare anonyma besök i flera sessioner. | [Översikt över beräknade attribut](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| Livscykelhantering för data | Rekommenderad | Pseudonym förfallotid för profiler med anonyma kanter bör konfigureras för att hantera lagring och uppfylla sekretesskrav. Profiler som bara innehåller ECID kan förfalla mellan 14 och 365 dagar. Cookie-medgivandeprinciper bör tillämpas för insamling av beteendedata. | [Översikt över livscykelhantering av avancerade data](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| Dataanvändningsetiketter och -tillämpning | Rekommenderad | Styrningsetiketter på beteendedata säkerställer efterlevnad, särskilt för geografisk anpassning (S2-känslig geografisk etikett) och enhetsbaserad personalisering. Etiketter förhindrar att begränsade beteendedata används i obehöriga personaliseringssammanhang. | [Datastyrningsöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home) |
| Övervakning och observerbarhet | Rekommenderad | Dataflödesövervakningen [!DNL Edge Network] och [!DNL Web SDK] hjälper till att identifiera leveransproblem med personalisering. Konfigurera varningar för dataströmsfel, intag-fel och avvikelser vid kantleverans. Viktigt för driftsättningar där personaliseringsfel försämrar besökarupplevelsen. | [Översikt över Insikter om observabilitet](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| Rapportering och analys | Ingår | Personalization resultatrapportering ingår i funktionskedjan (fas 5). CJA analys av anonyma besökares personalisering möjliggör djupgående funnel-analyser, kohortjämförelser och mätning av konverteringseffekt utöver vad AJO-rapporterna ger. | [CJA - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## Programfunktioner

I den här planen används följande funktioner från programfunktionskatalogen. Funktioner mappas till implementeringsfaser i stället för till numrerade steg.

### [!DNL Journey Optimizer] (AJO)

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Kanalkonfiguration | Fas 1: Konfiguration av webbyta | Konfigurera webbkanalsytor som definierar var personaliserat innehåll ska levereras på målwebbegenskaperna |
| Redigering av meddelanden | Fas 3: Skapa innehåll och skapa varianter | Ta fram skräddarsydda varianter för webbsidor med webbdesignern, den kodbaserade upplevelseredigeraren eller innehållsmallarna |
| Kampanjkörning | Fas 4: Kampanj- och leveranskonfiguration | Skapa och aktivera webbkampanjer som binder målgrupper, innehåll och leveranskonfiguration |
| Beslutsfattande | Fas 3: Skapa innehåll och skapa varianter (alternativ C) | Konfigurera beslutspolicyer, regler för behörighet och rankningsstrategier för dynamiskt innehållsval baserat på beteendesignaler |
| Experimentera med innehåll | Fas 3: Skapa innehåll och skapa varianter (alternativ B) | Konfigurera A/B-tester och multivariata innehållsexperiment med trafikallokering, framgångsmått och konfidensgränser |
| Rapportering och prestandaanalys | Fas 5: Rapportering och resultatanalys | övervaka mätvärden för personalisering, varianternas effektivitet, experimentera med resultat och konverteringseffekt |

### [!DNL Real-Time CDP] (RT-CDP)

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Målgruppsutvärdering | Fas 2: Beteende för målgruppsdefinition | Definiera och utvärdera kantbaserade målgruppssegment med beteendesignaler i realtid för personalisering |

## Förutsättningar

Slutför följande innan du börjar implementera.

- [ ] [!DNL Web SDK] implementeras på alla målwebbegenskaper med `sendEvent` anrop som fångar sidvyer, klick och relevanta beteendeinteraktioner
- [ ] Datastream har konfigurerats i användargränssnittet för datainsamling med [!DNL Adobe Experience Platform] och [!DNL Adobe Journey Optimizer] tjänster aktiverade
- [ ] Experience Event-schemat finns med fältgrupper för webbinteraktion (sidvisningar, referensdata, UTM-parametrar, enhetskontext) och är aktiverat för profil
- [ Namnområdet för ECID-identitet för ] har konfigurerats och angetts som primär identitet i webbbeteendehändelseschemat
- [ ] Edge-sammanslagningsprincip har konfigurerats med `isActiveOnEdge: true` i målsandlådan
- [ ] AJO webbkanal är etablerad och tillgänglig i målsandlådan
- [ ] Innehållsvarianter (kopiera, bilder, CTA:er) har utformats och godkänts för varje användningsfall för personalisering
- [ ] Framgångsmått har definierats (vad som utgör en konverterings- eller engagemangshändelse för mätning)
- [ Mekanismen för godkännande av cookies har implementerats på webbplatsen för att uppfylla sekretessreglerna innan beteendedata samlas in]

## Implementeringsalternativ

I det här avsnittet beskrivs tre implementeringsmetoder. Välj det alternativ som bäst passar dina personaliseringskrav.

### Alternativ A: Regelbaserad webbanpassning

**Passar bäst för:** Enkel, deterministisk personalisering - geomriktade banners, hänvisningsrubriker, enhetsspecifika layouter, nya jämfört med att returnera besökarmeddelanden. Välj det här alternativet när innehållsvarianten kan bestämmas av okomplicerad villkorlig logik (om villkor X, visa innehåll Y).

**Så här fungerar det:**

Regelbaserad personalisering använder kvalificerade målgruppssegment för att avgöra vilken innehållsvariant en besökare ser. Varje målgruppssegment mappas till en viss innehållsvariant via villkorsregler som definierats i kampanjen. När en besökare läser in en sida skickar [!DNL Web SDK] beteendesignaler till [!DNL Edge Network], som utvärderar besökarens kantprofil mot de definierade målgruppsreglerna i millisekunder. Den matchande innehållsvarianten returneras i svaret [!DNL Edge Network] och återges på sidan.

Strategin kräver att man definierar distinkta målgruppssegment i RT-CDP (t.ex.&quot;besökare från Google&quot;,&quot;besökare i Kalifornien&quot;,&quot;mobilbesökare&quot;) och skapar motsvarande innehållsvarianter i AJO. Kampanjen binder varje målgrupp till dess innehållsvariant med hjälp av regler för villkorat innehåll eller separata kampanjer per segment. Ingen AI-rankning eller trafikdelning är inblandad - relationen mellan målgrupp och innehåll är avgörande.

**Viktiga överväganden:**

- Kräver väldefinierade målgruppskriterier som kan uttryckas som edge-eligibility segment rule expressions
- Innehållsvarianter måste skrivas i förväg för varje målgruppssegment
- Nya personaliseringsregler kräver att nya målgruppssegment och innehållsvarianter skapas
- Tillhandahåller inte statistisk mätning av innehållsvariantens effektivitet

**Fördelar:**

- Lättaste att implementera och förstå - tydligt orsakssamband mellan målgrupp och innehåll
- Inga experimentella overhead- eller trafikdelningar krävs
- Deterministiskt beteende gör testning och kvalitetssäkring enkla
- Låg latens eftersom kantutvärdering är helt regelbaserad
- Fungerar bra när företaget redan vet vilket innehåll som fungerar bäst för varje segment

**Begränsningar:**

- Ingen inbyggd mekanism för att mäta om personalisering förbättrar resultatet jämfört med standardinnehåll
- Kräver manuellt beslutsfattande om vilket innehåll som ska visas för varje segment
- Anpassar eller optimerar inte över tid - statiska regler ändras först manuellt
- Om du skalar till många segment och varianter blir konfigurationen mer komplex

**Experience League:**

- [Kom igång med webbkanalen](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [Edge segmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### Alternativ B: Experimentationsbaserad webbanpassning

**Bäst för:** A/B-tester och multivariata tester - testa rubrikvarianter, CTA knappfärger, layoutalternativ, kampanjerbjudanden - med statistisk signifikansmätning. Välj det här alternativet när du behöver validera vilken innehållsvariant som fungerar bäst innan du implementerar en permanent personaliseringsregel.

**Så här fungerar det:**

Experimentationsbaserad personalisering använder AJO Content Experimentation för att slumpvis tilldela besökare till innehållsbehandlingsgrupper och mäta vilken variant som fungerar bäst i förhållande till ett definierat framgångsmått. Trafiken delas upp på olika varianter (t.ex. 50/50 för A/B, 33/33/34 för A/B/C) och prestanda spåras tills statistisk signifikans uppnås.

Experimentet är inbäddat i en webbkampanj från AJO. När en besökare läser in en sida tilldelar [!DNL Edge Network] dem till en behandlingsgrupp baserat på den konfigurerade trafikallokeringen. Besökaren får konsekvent samma behandling under hela försöket (sessionnivå eller besöksnivå beroende på konfiguration). Resultatstatistik (klickningar, konverteringar, engagemangshändelser) spåras via [!DNL Web SDK] och rapporteras i AJO experimentrapport.

Det här alternativet kräver inte fördefinierade målgruppssegment för målinriktning - alla besökare (eller en målinriktad delmängd) deltar i experimentet. Målet är att identifiera vilket innehåll som fungerar bäst, inte att inrikta sig på kända segment med fördefinierat innehåll.

**Viktiga överväganden:**

- Kräver tillräcklig trafikvolym för att uppnå statistisk signifikans inom en rimlig tidsram
- Experimentera använder en bayesisk statistisk modell med valfria tidsintervall
- En utelämningsgrupp (som inte tar emot personligt innehåll) rekommenderas för att mäta inkrementell lyft
- Endast ett experiment kan vara aktivt per kampanj i taget
- Experimentella ändringar kräver att kampanjen stoppas och startas om

**Fördelar:**

- Tillhandahåller statistiskt rigorös mätning av innehållsvariantens effektivitet
- Slipper gissningsarbete från personaliseringsbeslut - datadrivet innehållsval
- Stöder blockeringsgrupper för riktig stegvis höjning-mätning
- Inbyggda experimentrapporter med konfidensintervall och vinnardeklaration
- Resultat kan informera framtida regelbaserad personalisering (alternativ A) genom att identifiera vinnande varianter

**Begränsningar:**

- Kräver en meningsfull trafikvolym - det kan ta veckor innan lågtrafiksidor når sin betydelse
- Trafikdelning innebär att vissa besökare ser suboptimalt innehåll under testperioden
- Det går inte att anpassa efter segment under experimentet (alla besökare eller en delmängd deltar i lika stor utsträckning)
- Maximalt 10 behandlingsvarianter per experiment
- Ingen kontinuerlig optimering - experimenten är diskreta med start och slut

**Experience League:**

- [Kom igång med innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Skapa ett innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Rapport om innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)

### Alternativ C: Beslutsbaserad webbanpassning

**Passar bäst för:** Val av dynamiskt innehåll - kategoritillhörighetsrekommendationer, erbjudanden om avslutning, beteenderekommendationer - där en beslutsprincip utvärderar sessionssignaler och väljer det optimala innehållet från en katalog med valbara objekt. Välj det här alternativet när logiken för innehållsval är för komplex för enkla regler, när du vill ha AI-rankad optimering eller när uppsättningen av valbara innehållsobjekt är stor och dynamisk.

**Så här fungerar det:**

Beslutsbaserad personalisering använder AJO Decisioning för att utvärdera beteendesignaler och välja den bästa innehållsvarianten för varje besökare från en hanterad katalog med innehållsobjekt (erbjudanden). Varje innehållsobjekt har regler för behörighet (vem som kvalificerar), representationer (hur innehållet ser ut i varje placering) och valfria begränsningar för att sätta fast innehåll (hur ofta det kan visas). En beslutspolicy länkar placeringar (där innehåll visas på sidan) till samlingar av innehållsobjekt och tillämpar en rangordningsstrategi för att välja det bästa alternativet.

När en besökare läser in en sida skickar [!DNL Web SDK] en [!DNL Edge Network]-begäran som innehåller beslutsomfånget. Beslutsmotorn utvärderar besökarens edge-profil mot reglerna för berättigande av innehållsobjekt, tillämpar rangordningsstrategin (prioritetsbaserad, formelbaserad eller AI-rankad) och returnerar det vinnande innehållsobjektet. Detta sker vid kanten med en mindre fördröjning.

Rankningsstrategin avgör hur valbara innehållsobjekt beställs. Prioritetsbaserad rankning använder manuellt tilldelade prioritetsvärden. Formelbaserad rankning använder ett anpassat uttryck (t.ex. viktningsfrekvensen för sidvyer). AI-rankad rankning använder en maskininlärningsmodell som optimerar för det valda framgångsmåttet över tiden, men kräver minst 1 000 konverteringshändelser för utbildning.

**Viktiga överväganden:**

- Kräver att du ställer in beslutskomponenterna: placeringar, regler för behörighet, innehållsobjekt, reservposter, samlingar och beslutspolicyer
- AI-rankade strategier kräver tillräcklig konverteringsvolym (1 000+ händelser) för att utbilda modellen
- Edge beslut är begränsade till profilattribut som är tillgängliga i edge-profilarkivet
- Innehållsobjekt måste hanteras och underhållas i beslutsbiblioteket
- Reservinnehåll måste definieras för fall där inget anpassat objekt kvalificerar sig

**Fördelar:**

- Kan anpassas till stora innehållskataloger utan att behöva mappa målgrupp till innehåll individuellt
- AI-rankade strategier optimerar kontinuerligt innehållsurvalet baserat på observerade prestanda
- Reglerna för rätt till och begränsning av antalet licenser ger detaljerad kontroll över innehållsleveransen
- Stöder komplex affärslogik som skulle vara svår att uttrycka som målgruppssegment
- Kan återanvändas i alla kanaler - samma beslutspolicy kan styra webben, e-post och mobilpersonalisering

**Begränsningar:**

- Komplexare implementering - kräver att du ställer in den fullständiga beslutskomponentstacken
- AI-rankningen kräver stor konverteringsvolym och tid för effektiv utbildning
- Begränsningar av profildata i Edge begränsar komplexiteten i berättigandereglerna för anonyma besökare
- Objektivhantering - varje artikel behöver representationer, regler för behörighet och underhåll
- Felsökningslogiken för beslutsfattande är mer komplex än regelbaserade strategier

**Experience League:**

- [Beslutsledning - översikt](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Skapa placeringar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Skapa personaliserade erbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Skapa beslut](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)

### Jämförelse av alternativ

I följande tabell jämförs de tre implementeringsalternativen över de viktigaste kriterierna.

| Kriterier | Alternativ A: Regelbaserat | Alternativ B: Experimentation | Alternativ C: Beslut |
| --- | --- | --- | --- |
| Bäst för | Kända kopplingar mellan segment och innehåll | Identifiera vilket innehåll som fungerar bäst | Val av dynamiskt innehåll från stora kataloger |
| Komplex | Lågt | Medelsvåra: | Högt |
| Latens | Undersekund (kant) | Undersekund (kant) | Undersekund (kant) |
| Personalization precision | Segmentnivå (målgruppsregler) | Besökarnivå (slumpmässig tilldelning) | Besöksnivå (behörighet + rankning) |
| Innehållsoptimering | Manuell (ingen mätning) | Statistisk provning (A/B) | Kontinuerlig (AI-rankad) eller manuell (prioritet) |
| Kräver publiksegment | Ja (edge-evaluate) | Nej (trafikdelning) | Valfritt (för regler för behörighet) |
| Mätkapacitet | Ingen inbyggd (kräver CJA) | Inbyggda experimentrapporter | Inbyggda beslutsrapporter |
| Storlek på innehållskatalog | Liten (1:1 segment-till-innehåll) | Liten (2-10 varianter) | Stora (obegränsat antal berättigade artiklar) |
| Kräver | Edge målgrupper, innehållsvarianter | Kampanj med experimentellt aktiverat | Beslutskomponenter (praktik, erbjudanden, policyer) |

### Välj rätt alternativ

Använd följande beslutslogik för att välja lämpligt implementeringsalternativ:

1. **Vet du redan vilket innehåll som ska visas för varje besökarsegment?**
   - Ja: Börja med **alternativ A (regelbaserat)**. Ni har fastställt innehållsstrategier per segment och behöver deterministisk leverans.
   - Nej: fortsätt till fråga 2.

2. **Behöver du testa ett litet antal innehållsvarianter för att hitta den bästa utföraren?**
   - Ja: välj **Alternativ B (experimentering)**. Du vill ha statistisk validering innan du implementerar en innehållsstrategi.
   - Nej: fortsätt till fråga 3.

3. **Har du en stor katalog med innehållsobjekt med komplexa kvalificerings- och rankningskrav?**
   - Ja: välj **Alternativ C (beslut)**. Du behöver välja dynamiskt innehåll som kan skalas utöver enkla regler.
   - Nej: Börja med **alternativ A (regelbaserat)** för enkelhetens skull, och fortsätt sedan med alternativ B eller C när behoven växer.

**Kombinationsalternativ:** Dessa alternativ utesluter inte varandra. Ett vanligt framsteg är att börja med alternativ B (Experimentation) för att hitta vinnande innehåll och sedan distribuera vinnare med alternativ A (Regelbaserad) för kontinuerlig leverans. Alternativ C (beslut) kan placeras ovanpå om du vill använda dynamiska katalogbaserade markeringar, medan alternativ A hanterar enklare deterministiska regler.

## Implementeringsfaser

I följande faser beskrivs arbetsflödet för implementering från början till slut.

### Fas 1: Konfigurera webbytor

**Programfunktion:** AJO: Kanalkonfiguration

Definiera de webbkanalsytor som anger var på din webbplats personaliserat innehåll ska levereras. En webbyta identifierar ett specifikt sidans URL- eller URL-mönster och platsen på sidan (CSS-väljare eller kodbaserad upplevelseyta) där AJO kan mata in eller ersätta innehåll.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>**Beslut: Yttyp** - Hur ska personaliserat innehåll levereras till sidan?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Webbkanal (visuell redigerare) | Personaliseringen innebär att man ändrar synliga sidelement (banners, headlines, images, CTA) med en visuell redigerare med dra-och-släpp | Kräver webbläsartillägget för webbdesignern. Bäst för marknadsföringsdrivna innehållsändringar. Begränsat till visuella ändringar av befintliga sidelement. |
| Kodbaserad upplevelse | Personaliseringen kräver att strukturerade data (JSON) som webbplatsens programkod använder och återger matas in | Kräver att utvecklarimplementeringen förbrukar JSON-nyttolasten. Maximal flexibilitet för komplex personalisering. Bäst för SPA, dynamiska komponenter och programmatisk återgivning. |
| Båda (hybrid) | Olika personaliseringar på samma webbplats behöver olika leveransmekanismer | Använd webbkanalen för enkla visuella ändringar och kodbaserade upplevelser för programmatisk återgivning. Ökar komplexiteten i implementeringen men maximerar täckningen. |

>[!NOTE]
>**Beslut: Ytomfång** - Vilket URL-omfång ska webbytan omfatta?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Exakt URL-matchning | Personalization riktar in sig på en viss sida (t.ex. hemsida, landningssida) | Mest exakt målinriktning. Kräver separata ytor för varje sida. |
| URL-mönster med jokertecken | Personalization gäller för en sidkategori (t.ex. alla produktsidor, alla bloggartiklar) | Minskar overheadkostnaderna för ythantering. Innehållsvarianter måste utformas så att de fungerar på alla matchande sidor. |
| Enkelsidig applikation (SPA)-yta | Webbplatsen är en SPA där URL-ändringar inte aktiverar helsidesomladdning | Kräver SPA-medveten [!DNL Web SDK]-konfiguration med `sendEvent` anrop om visningsändringar. Ytdefinitioner använder SPA-vynamnet i stället för URL. |

**Gränssnittsnavigering:** [!DNL Journey Optimizer] > Administration > Kanaler > Webbkonfiguration

**Information om nyckelkonfiguration:**

- Definiera sidans URL eller URL-mönster för ytan
- Ange CSS-väljaren eller yt-URI för innehållsplacering
- För kodbaserade upplevelser definierar du det ytnamn som programkoden ska referera till
- Associera ytan med AJO-sandlådan där kampanjer ska skapas

**Experience League-dokumentation:**

- [Kom igång med webbkanalen](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [Skapa webbupplevelser](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [Kodbaserad upplevelsekanal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/get-started-code-based)
- [Kodbaserad upplevelsekonfiguration](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/code-based-configuration)

### Fas 2: Definiera beteendemässiga målgrupper

**Programfunktion:** RT-CDP: Målgruppsutvärdering

Definiera högkvalitativa målgruppssegment baserat på sessionsbeteendesignaler som driver personalisering. Dessa målgrupper avgör vilka besökare som kvalificerar sig för varje personaliserad upplevelse. Edge-utvärdering är obligatoriskt för det här mönstret eftersom personaliseringsbeslut måste fattas i delsekundersintervall när besökaren navigerar på webbplatsen.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>**Beslut: Beteendesignalval** - Vilka sessionssignaler ska leda till personalisering?

| Signal | När ska du använda | Edge-berättigande |
| --- | --- | --- |
| Referenskälla-/UTM-parametrar | Kampanjspecifik anpassning av landningssidor | Berättigad - enkel attributkontroll för den aktuella händelsen |
| Geografisk plats (land, region, stad) | Regionala kampanjer, språkspecifikt innehåll, butiksposition | Kvalificerad - kontroll av profilattribut |
| Enhetstyp (dator, mobil, surfplatta) | Enhetsoptimerade innehållslayouter och CTA:er | Kvalificerad - kontroll av profilattribut |
| Sidor som visas i sessionen | Kategoritillhörighet, innehållsrekommendationer | Berättigad med begränsningar - endast kontroll av antalet enkla händelser |
| Ny eller återkommande besökare | Välkomstmeddelanden, progressivt engagemang | Berättigad - ECID-beständighet indikerar återkommande besökare |
| Tid på plats/rullningsdjup | Avslutande, engagemangsbaserade erbjudanden | Kan kräva anpassad implementering - inte internt kvalificerade |

>[!NOTE]
>**Beslut: Målgruppsutvärderingsmetod** - Alla målgrupper för det här mönstret måste använda kantutvärdering. Bekräfta behörighet innan du definierar segment.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Edge-utvärdering | Krävs för det här mönstret | Segmentregeluttryck måste vara kanteliga: enkla attributjämförelser, segmentmedlemskapskontroller, inga tidsseriefrågor eller aggregeringsfunktioner. Utvärderingsfördröjning under andra sekund. |
| Utvärdering av direktuppspelning (reserv) | När segmentregeluttrycket inte är kantkvalificerat men nästan realtid är godtagbart | Fördröjning mellan sekunder och minuter. Stöder mer komplexa segmentregeluttryck. Kan leda till märkbar fördröjning i personaliseringen. |

**Gränssnittsnavigering:** Kund > Målgrupper > Skapa målgrupp > Skapa regel

**Information om nyckelkonfiguration:**

- Använd Segment Builder för att definiera målgruppsregler med beteendeattribut
- Verifiera att kanten är berättigad genom att bekräfta att segmentregeluttrycket endast använder funktioner som stöds (enkla attributjämförelser, segmentmedlemskap)
- Ställ in sammanfogningsprincipen på den edge-aktiva sammanfogningsprincip som konfigurerats i F4
- Förhandsgranska målgruppspopulationen för att validera segmentet returnerar förväntade resultat
- Använd händelsenivåattribut från den aktuella sessionen i stället för tidsseriefrågor för målgrupper som baseras på sidvisningar på sessionsnivå

**Var alternativen skiljer sig:**

**För alternativ A (regelbaserad):**
Skapa distinkta målgruppssegment för varje innehållsvariant. Varje segment representerar ett visst beteendeförhållande (t.ex. &quot;Referens = Google AND Geo = US&quot; mappar till innehållsvariant A). Antalet målgrupper är lika med antalet personaliseringsregler.

**För alternativ B (experimentering):**
Målgruppsdefinitionen är valfri. Om experimentet riktar sig till alla besökare krävs ingen målgrupp - trafikdelningen hanterar varianttilldelningen. Om experimentet avser en viss delmängd (t.ex. endast mobilbesökare), definierar du en målgrupp för att experimentera med rätt till det.

**För alternativ C (beslut):**
Definiera målgrupper som kan användas som regler för behörighet för innehållsobjekt. Dessa målgrupper avgör vilka besökare som är kvalificerade för vilka innehållsobjekt i beslutspolicyn. Beslutsmotorn hanterar val av innehåll bland valbara objekt.

**Experience League-dokumentation:**

- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Edge segmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Profile Query Language referens](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)
- [Direktuppspelningssegmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)

### Fas 3: Skapa innehåll och skapa varianter

**Programfunktion:** AJO: Message Authoring, AJO: Content Experimentation (Option B), AJO: Decisioning (Option C)

Skapa de anpassade varianter av innehåll som ska levereras till besökarna baserat på målgruppsmedlemskap (alternativ A), experimenttilldelning (alternativ B) eller beslutslogik (alternativ C). I den här fasen beskrivs hur du skapar innehåll med AJO webbdesigner eller kodsbaserade upplevelseredigerare, liksom hur du använder det experimentella gränssnittet eller den beslutskonfiguration som styr hur innehåll väljs.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>**Beslut: Metoden för innehållsredigering** - Hur ska webbinnehållsvarianter redigeras?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Webbvisuell redigerare | Marknadsförare kan ändra sidelement visuellt utan kod | Kräver webbläsartillägg. Passar bäst för text, bilder och CTA-ändringar. Begränsat till att ändra befintliga sidelement. |
| Kodbaserad upplevelseeditor | Innehållet kräver strukturerade data (JSON) som programkoden återger | Maximal flexibilitet. Kräver att utvecklarimplementeringen förbrukar nyttolasten. Passar bäst för dynamiska komponenter och SPA. |
| HTML/CSS-kodredigerare | Innehållsändringar kräver anpassad HTML eller CSS | Direkt kodkontroll. Kräver HTML/CSS-expertis. Passar bäst för komplexa layoutändringar. |

>[!NOTE]
>**Beslut: Personalization-tokens** - Ska innehåll innehålla dynamisk personalisering med hjälp av profil- eller kontextuella attribut?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Statiska innehållsvarianter | Varje variant är en fast del av innehållet utan dynamiska tokens | Det enklaste sättet. Innehållet är förutsägbart och enkelt att hantera på kvalitetsnivå. Ingen risk för att attributvärden saknas. |
| Dynamiskt innehåll med personaliseringsuttryck | Innehåll innehåller variabler av typen Handlebars som matchar profil- eller händelseattribut (t.ex. stadsnamn, hänvisningskälla) | Mer relevant innehåll. Kräver reservvärden för attribut som kan vara null i anonyma profiler. Använd syntaxen `{{profile.homeAddress.city}}` med hjälpredor. |
| Villkorliga innehållsblock | Olika innehållsblock återges baserat på attributvillkor i en enskild variant | Minskar antalet distinkta varianter som behövs. Ökar innehållets komplexitet. Bra för mindre variationer i en delad layout. |

**Gränssnittsnavigering:** [!DNL Journey Optimizer] > Kampanjer > Välj kampanj > Redigera innehåll

**Information om nyckelkonfiguration:**

- Skapa innehåll med webbdesignern (visuella ändringar) eller kodsbaserad Experience Editor (JSON-nyttolast)
- Använd redigeraren för anpassningsuttryck för att infoga dynamiska variabler från kantprofilattribut
- Konfigurera reservinnehåll för personaliseringstoken som kan vara tomt i anonyma profiler
- Förhandsgranska innehåll med testprofiler för att verifiera återgivning i olika scenarier

**Var alternativen skiljer sig:**

**För alternativ A (regelbaserad):**
Skapa en distinkt innehållsvariant för varje målgruppssegment som definieras i fas 2. Bind varje variant till målgruppen med hjälp av regler för villkorat innehåll i kampanjkonfigurationen. Kontrollera att det finns en standardvariant för innehåll för besökare som inte matchar någon målgruppsregel.

**För alternativ B (experimentering):**
Författarbehandlingsvarianter (A, B, C osv.) för experimentet. Aktivera innehållsexperimenterande i kampanjen, definiera behandlingsvarianter med deras innehåll, ange procentsatser för trafikallokering och konfigurera framgångsmåttet.

- Definiera 2-10 behandlingsvarianter med distinkt innehåll
- Ange trafikallokering (t.ex. 50/50 för A/B, eller viktad delning för lågrisktestning)
- Om du vill kan du inkludera en blockeringsgrupp (t.ex. får 10 % standardinnehåll) för att mäta stegvis lyft
- Välj framgångsmått: unika öppningar, unika klick, konverteringar eller anpassade mätvärden
- Ange ett tröskelvärde för tillförlitlighet: 95 % för standardtester, 99 % för beslut med högsta prioritet, 90 % för riktat lärande
- **Gränssnittsnavigering:** Kampanj > Innehållsexperiment > Lägg till behandling > Trafikallokering > Resultatmått

**För alternativ C (beslut):**
Konfigurera Beslutskomponentstacken och integrera den i kampanjen.

1. **Skapa placeringar** - Definiera var på sidan innehållsobjekten ska visas (webb-HTML, webb-JSON, webbild)
   - **Gränssnittsnavigering:** [!DNL Journey Optimizer] > Komponenter > Beslutshantering > Placeringar
2. **Definiera regler för behörighet** - Skapa regler baserat på attribut för kantprofil som avgör vilka besökare som är kvalificerade för varje innehållsobjekt
   - **Gränssnittsnavigering:** [!DNL Journey Optimizer] > Komponenter > Beslutshantering > Regler
3. **Skapa innehållsobjekt (erbjudanden)** - Skapa anpassade innehållsobjekt med representationer för varje placering, behörighetsregler, prioritet och valfri begränsning
   - **Gränssnittsnavigering:** [!DNL Journey Optimizer] > Komponenter > Beslutshantering > Erbjudanden > Skapa erbjudande
4. **Skapa reservinnehåll** - Definiera ett reservobjekt som returneras när inget anpassat objekt kvalificeras
   - **Gränssnittsnavigering:** [!DNL Journey Optimizer] > Komponenter > Beslutshantering > Erbjudanden > Skapa reserverbjudande
5. **Ordna i samlingar** - Gruppera innehållsobjekt med hjälp av samlingskvalificerare (taggar) och skapa samlingar
   - **Gränssnittsnavigering:** [!DNL Journey Optimizer] > Komponenter > Beslutshantering > Samlingskvalificerare / Samlingar
6. **Skapa beslutspolicy** - Länka ersättningar till samlingar och välj rangordningsstrategi (prioritetsbaserad, formelbaserad eller AI-rankad)
   - **Gränssnittsnavigering:** [!DNL Journey Optimizer] > Komponenter > Beslutshantering > Beslut > Skapa beslut

**Experience League-dokumentation:**

- [Skapa webbupplevelser](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [Kodbaserad upplevelsekanal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/get-started-code-based)
- [Lägg till personalisering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Dynamiskt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Skapa ett innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Skapa personaliserade erbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Skapa beslut](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Rankningsstrategier](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Fas 4: Konfigurera kampanj och leverans

**Programfunktion:** AJO: Kampanjkörning

Skapa och aktivera AJO webbkampanj som binder webbytan (fas 1), målgruppsanpassningen eller experimentkonfigurationen (fas 2-3) och innehållsvarianterna (fas 3) till en slutprodukt. Kampanjen styr när och hur personaliserat innehåll skickas till besökare.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>**Beslut: Kampanjtyp** - Hur ska kampanjen aktiveras?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Schemalagd kampanj (alltid aktiverad) | Personalization bör köras kontinuerligt för alla kvalificerade besökare | Ange startdatum utan slutdatum för personlig anpassning. Målgruppsutvärderingen görs i realtid. De vanligaste för webbpersonalisering. |
| Schemalagd kampanj (tidsbunden) | Personalization är knutet till en viss kampanjperiod eller säsongsevenemang | Ange explicit start- och slutdatum. Kampanjen inaktiveras automatiskt vid slutdatumet. Bra för kampanjkampanjer. |
| API-utlöst kampanj | Personalization-leverans måste utlösas av en extern systemhändelse | Kräver API-integrering. Mindre vanligt för anonym webbpersonalisering. Används när ett backend-system måste kontrollera när personalisering är aktivt. |

**Gränssnittsnavigering:** [!DNL Journey Optimizer] > Kampanjer > Skapa kampanj

**Information om nyckelkonfiguration:**

- Markera webbkanalen och webbytan som konfigurerats i fas 1
- Bind målgruppen (för alternativ A) eller konfigurera experimentinställningar (för alternativ B) eller bädda in beslutet (för alternativ C)
- Ange kampanjschemat (startdatum, slutdatum eller alltid aktiverat)
- Konfigurera frekvensbegränsning på kampanjnivå om tillämpligt
- Granska all konfiguration och aktivera kampanjen

**Var alternativen skiljer sig:**

**För alternativ A (regelbaserad):**
Skapa en kampanj per personaliseringsregel, som alla riktar sig till olika målgrupper med motsvarande innehållsvariant. Du kan också använda en enda kampanj med villkorsstyrda innehållsregler som mappar målgruppsmedlemskap till innehållsvarianter inom en kampanj.

**För alternativ B (experimentering):**
Skapa en enda kampanj med innehållsexperimenterande aktiverat. Experimentkonfigurationen (varianter, trafikallokering, framgångsmått) definierades i fas 3. Aktivera kampanjen för att starta experimentet.

**För alternativ C (beslut):**
Skapa en kampanj som bäddar in den beslutsprincip som konfigurerats i fas 3. Kampanjens innehållsåtgärd refererar till beslutsomfånget, som utlöser beslutsmotorn i förgrunden. Aktivera kampanjen för att påbörja beslutsbaserad innehållsleverans.

**Experience League-dokumentation:**

- [Skapa en kampanj](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Kom igång med kampanjer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Leverera erbjudanden i meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### Fas 5: Rapportera och analysera prestanda

**Programfunktion:** AJO: Rapporterings- och prestandaanalys

Övervaka personaliseringsprestanda med inbyggda rapporter från AJO och utöka analysen med CJA för djupare insikter över olika kanaler. Den här fasen handlar om att få tillgång till livesändningar och historiska kampanjrapporter, granska experimentresultat och bygga anpassade analysarbetsytor.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>**Beslut: Rapporteringsdjup** - Hur djupgående ska prestandaanalys gå?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Endast inbyggda AJO-rapporter | Grundläggande mått för leverans och engagemang är tillräckliga | Ger utskrift, klickning, CTR och konverteringsstatistik. Finns omedelbart i kampanjgränssnittet. Begränsad anpassning. |
| AJO-rapporter + CJA-analys | Det krävs djupgående analyser, kohortjämförelser eller mätningar av påverkan över flera kanaler från funnel | Kräver CJA-anslutning och datavy länkad till AJO datamängder. Möjliggör frihandsanalys, anpassade beräknade värden, attribueringsmodellering och målgruppspublicering. |

**Gränssnittsnavigering:** [!DNL Journey Optimizer] > Kampanjer > Välj kampanj > Visa rapport

**Information om nyckelkonfiguration:**

- Få tillgång till liverapporten under aktiva kampanjer för att övervaka leveransen i realtid (uppdateras var 60:e sekund, visar senaste dygnet)
- Få tillgång till den historiska rapporten (hela tiden) efter kampanjslutförandet för en omfattande analys (kan ta upp till två timmar att fylla i fullt ut)
- För alternativ B (Experimentation): se experimentrapporten för jämförelse av behandlingsresultat, konfidensintervall och vinnardeklaration
- För CJA-analys: kontrollera att en CJA-anslutning innehåller data om AJO Experience-händelser och att en datavy har konfigurerats med mått för webbpersonalisering

**Var alternativen skiljer sig:**

**För alternativ A (regelbaserad):**
Granska kampanjrapporter för varje målgruppssegment för att jämföra leverans- och engagemangsmått för personaliserade innehållsvarianter. Använd CJA för att skapa en jämförelsearbetsyta som mäter konverteringseffekten för personaliserat och standardinnehåll.

**För alternativ B (experimentering):**
Granska experimentrapporten för statistisk säkerhet, behandlingshöjning och identifiering av vinnare. Vänta på att tröskelvärdet för förtroende nås innan du deklarerar en vinnare. Använd vinnande innehåll som permanent variant (övergång till alternativ A för kontinuerlig leverans).

- **Gränssnittsnavigering:** Kampanj > Innehållsexperiment > Visa rapport
- **Experience League:** [Rapport om innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)

**För alternativ C (beslut):**
Granska resultatvärden för beslutsfattande, inklusive antal erbjudanden, urvalsfrekvens och konverteringsattribuering per innehållsobjekt. Analysera hur rangordningsstrategier fungerar och om reservinnehåll hanteras för ofta (vilket anger att reglerna för behörighet är för restriktiva).

**Experience League-dokumentation:**

- [Kampanjrapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Global kampanjrapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Arbeta med Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Analysis Workspace - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [Statistiska beräkningar i innehållsexperimentet](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

## Implementeringsöverväganden

I det här avsnittet beskrivs hur man kan lösa säkerhetsproblem, vanliga fallgropar, bästa praxis och beslut om avvägning för det här användningsmönstret.

### Gardrutor och begränsningar

Granska följande skyddsutkast före och under implementeringen.

- Edge-segment är begränsade till enkla attributkontroller och segmentmedlemskap - inga tidsseriefrågor eller komplexa aggregeringar - [Edge-segmenteringsberättigande](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- Endast en sammanfogningsprincip kan vara aktiv för kant per sandlåda: [Profilskyddsräcken](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Maximalt 4 000 segmentdefinitioner per sandlåda - [Segmenteringsskyddsräcken](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Max 500 aktiva live-kampanjer per sandlåda - [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Max 10 behandlingsvarianter per innehållsexperiment - [Begränsningar för innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Högst 10 000 godkända anpassade erbjudanden per sandlåda (alternativ C) - [Beslutshanteringsgarantier](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Max 30 placeringar per beslut (alternativ C) - [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- AI-rankningsmodeller kräver minst 1 000 konverteringshändelser för utbildning (alternativ C)
- Svarstid för [!DNL Edge Network] SLA: &lt; 200 ms för edge-utvärderade segment
- Förfallodatum för pseudonym profil: kan konfigureras mellan 14 och 365 dagar för profiler som endast är ECID
- Live-rapporter uppdateras var 60:e sekund och visar de senaste 24 timmarna med data
- Historikrapporter kan ta upp till två timmar att fylla i fullt ut efter att kampanjen har slutförts

### Vanliga fallgropar

Undvik följande vanliga implementeringsmisstag.

- **[!DNL Web SDK]skickar inte beteendesignaler till AEP:** Kontrollera att tjänsten [!DNL Adobe Experience Platform] är aktiverad för datastream och att händelsens datamängd är korrekt mappad. Utan detta fylls kantprofilerna inte i och målgruppsutvärderingen misslyckas utan att något märks - besökaren får standardinnehåll utan felindikering.
- **Edge-målgrupp som returnerar noll kvalifikationer:** Edge-segmentering har strikta behörighetskrav. Tidsseriefrågor, aggregeringsfunktioner och multientitetsfrågor är inte kantberättigande. Skriv om segmentregeluttrycket med enkla attributjämförelser eller segmentmedlemskapskontroller.
- **Sammanslagningsprincipen är inte aktiv för kant:** Om den sammanfogningsprincip som används av målgruppssegmentet inte har `isActiveOnEdge: true`, misslyckas kantprofilsökningarna och personaliseringen levereras inte. Endast en sammanfogningsprincip per sandlåda kan vara aktiv vid kant - kontrollera att det inte finns någon konflikt.
- **Personalization flimmer vid sidinläsning:** Anropet [!DNL Web SDK] `sendEvent` som hämtar personaliseringsförslag måste köras innan sidan återger målinnehållsområdet. Implementera fördolda fragment eller asynkron återgivning för att förhindra att standardinnehållet blinkar innan det anpassade innehållet läses in.
- **Innehåll som inte återges på SPA-vägändringar:** Single-page-program kräver explicita `sendEvent` anrop med uppdaterad visningsinformation när flödet ändras. Utan detta utvärderas inte personaliseringen för den nya vyn av [!DNL Edge Network].
- **Experimentera som inte uppnår statistisk signifikans:** Otillräcklig trafikvolym eller för många behandlingsvarianter späder samplingsstorleken per variant. Minska antalet varianter eller öka experimentets längd. Stoppa inte experimenten i förtid - resultaten kan vara vilseledande.
- **Beslut om att endast returnera reservinnehåll:** Kontrollera att anpassade innehållsobjekt har godkänts, inom giltighetsdatumintervallet, och att behörighetskraven matchar den anonyma besökarens kantprofilattribut. Kontrollera också att inga begränsningar har nåtts.

### God praxis

Följ dessa rekommendationer för en lyckad implementering.

- **Börja enkelt, iterera sedan:** Börja med alternativ A (regelbaserad) för inledande personalisering och använd sedan alternativ B (experimentering) för att validera antaganden och alternativ C (beslut) för avancerade användningsfall. Varje alternativ bygger på den grundläggande infrastrukturen.
- **Använd prehide för att förhindra flimmer:** Implementera AEP-preflight-utdrag på sidor där personalisering ska levereras. Detta döljer målinnehållsområdet tills det personaliserade innehållet är klart att återges, vilket förhindrar visuell flimmer.
- **Designa grundinnehåll avsiktligt:** Standardinnehållet (icke-personaliserat) ska vara en självständig upplevelse av hög kvalitet. Besökare som inte är kvalificerade för personalisering - eller när svaret på [!DNL Edge Network] är fördröjt - bör inte få en försämrad upplevelse.
- **Verifiera Edge-berättigande innan du skapar målgrupper:** Innan du investerar i utveckling av målgruppsregler bekräftar du att segmentregeluttrycket är edge-eligible genom att granska kriterierna i Experience League. Uttryck som inte är giltiga återgår i tysthet till batch- eller direktuppspelningsutvärdering med oacceptabel fördröjning för det här mönstret.
- **Övervaka kantleveransresultat:** Konfigurera övervakningsaviseringar för [!DNL Edge Network] svarstider och leveransfel för personalisering. Edge leveransproblem är osynliga för besökaren (de ser standardinnehåll) och kan gå förlorade utan proaktiv övervakning.
- **Konfigurera pseudonym förfallotid för profil:** Ange lämpliga förfalloperioder för anonyma kantprofiler för att balansera personalisering mellan sessioner (identifiera återkommande besökare) med sekretess- och lagringshantering.
- **Testa med representativa profiler:** När du förhandsgranskar anpassat innehåll ska du använda testprofiler som representerar de faktiska anonyma besökarscenarierna (inga CRM-data, begränsad beteendehistorik, olika geografiska platser och enheter).

### Avvecklingsbeslut

Tänk på följande när du planerar implementeringen.

>[!NOTE]
>**Avvikelse: Komplexitet för Personalization-bredd jämfört med implementering**
>
>Mer detaljerad personalisering (många målgrupper, många innehållsvarianter) ger mer relevanta upplevelser, men ökar komplexiteten i konfigurationen och kostnaderna för innehållsproduktion.
>
>- **Många personaliseringsfördelar:** Enkelhet, kortare time-to-market, lägre produktionskostnader för innehåll. Ett litet antal målgrupper och varianter täcker de flesta besökare med meningsfull personalisering.
>- **Detaljerad personalisering prioriterar:** Maximal relevans, högre engagemangsökning, bättre konverteringsgrader. Många målgrupper och varianter hanterar specifika beteendesignaler med skräddarsytt innehåll.
>- **Rekommendation:** Börja med 3-5 högeffektiva personaliseringsregler för de vanligaste besökarsegmenten (t.ex. hänvisningskälla, enhetstyp, geografisk region). Mät effekten och utöka sedan till mer detaljerade regler baserade på observerade prestanda och affärsvärden.

>[!NOTE]
>**Avvikelse: Regelbaserad determinism kontra AI-driven optimering**
>
>Regelbaserade metoder (alternativ A) ger företaget fullständig kontroll över vilket innehåll varje besökare ser. AI-rankade metoder (alternativ C) optimerar innehållsvalet över tid men minskar synligheten för varför specifikt innehåll har valts.
>
>- **Regelbaserade fördelar:** Förutsägbarhet, Granskningsbarhet, Affärskontroll. Marknadsföringsteamen vet exakt vilket innehåll varje segment tar emot och kan förklara logiken för intressenter.
>- **AI-drivna förmåner:** Prestandaoptimering, skalbarhet, kontinuerlig förbättring. AI-modellen upptäcker tillhörigheter för innehållsbesökare som mänsklig regelskrivning kanske saknar.
>- **Rekommendation:** Använd regelbaserad för innehållsbeslut med hög prioritet där varumärkets enhetlighet och intressenters transparens är av största vikt. Använd AI-rankad för stora innehållskataloger där manuell regelhantering blir ohanterlig och kontinuerlig optimering ger en mätbar lyft.

>[!NOTE]
>**Avvikelse: Anonym profilbeständighet jämfört med sekretessefterlevnad**
>
>Längre pseudonym förfallotid för profiler ger bättre personalisering över flera sessioner (identifierar återkommande besökare, skapar beteendesammanhang över tid). Kortare utgångsdatum förbättrar sekretessen och minskar lagringskostnaderna.
>
>- **Längre förfallodatum prioriterar:** Mer anonyma profiler, bättre återgång till besöksigenkänning, fler data för personaliseringsbeslut. Ange utgångsdatum till 90-365 dagar.
>- **Kortare förfallotider:** Integritetsefterlevnad (GDPR, CCPA), minskade lagringskostnader, minimerad risk för inaktuella profildata. Ange utgångsdatum till 14-30 dagar.
>- **Rekommendation:** Justera förfallodatum med din organisations policy för godkännande av cookies och sekretess. För de flesta implementeringar ger 30-90 dagar en rimlig balans mellan personaliseringsvärde och efterlevnad av sekretesskrav.

## Relaterad dokumentation

Följande Experience League-resurser innehåller ytterligare information om de funktioner som används i det här användningsmönstret.

**Webbkanal och kodbaserade upplevelser**

- [Kom igång med webbkanalen](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [Skapa webbupplevelser](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [Kodbaserad upplevelsekanal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/get-started-code-based)
- [Kodbaserad upplevelsekonfiguration](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/code-based-configuration)

**Målgrupper och segmentering**

- [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Edge segmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Direktuppspelningssegmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Profile Query Language referens](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

**Personalization och innehåll**

- [Lägg till personalisering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization syntax](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Dynamiskt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Arbeta med innehållsmallar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Arbeta med innehållsfragment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)

**Experimentera med innehåll**

- [Kom igång med innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Skapa ett innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Rapport om innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Statistikberäkningar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

**Beslutshantering**

- [Beslutsledning - översikt](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Skapa placeringar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Skapa beslutsregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Skapa personaliserade erbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Skapa reserverbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Skapa samlingar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Skapa beslut](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Rankningsstrategier](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [Leverera erbjudanden i meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

**Kampanjer**

- [Kom igång med kampanjer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Skapa en kampanj](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)

**[!DNL Web SDK]och datainsamling**

- [SDK - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Installera SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
- [Konfigurera datastreams](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Översikt över taggar](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)

**Identitet och profil**

- [Översikt över identitetstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Översikt över namnutrymmen för identiteter](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/namespaces)
- [Översikt över kopplingsprofiler](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [Översikt över kundprofiler i realtid](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)

**Datamodellering**

- [XDM - systemöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Grundläggande om schemakomposition](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)

**Rapportering och analys**

- [Kampanjrapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [Global kampanjrapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Arbeta med Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Analysis Workspace - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [CJA - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)

**Datastyrning och sekretess**

- [Översikt över dataförvaltning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Översikt över livscykelhantering av avancerade data](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)
- [Fältgruppen för samtycke och inställningar](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)

**Guardrails**

- [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Garantier för kundprofiler i realtid](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [Garantier för identitetstjänst](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)
