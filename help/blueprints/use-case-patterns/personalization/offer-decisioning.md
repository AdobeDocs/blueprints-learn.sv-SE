---
title: Offer Decisioning (erbjudandebeslut)
description: Lär dig hur du använder centraliserad beslutslogik för att välja nästa bästa erbjudande eller innehåll för en profil i olika kanaler.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 8fd511b3-0200-41bf-aff1-e3f2a00a578e
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '8026'
ht-degree: 1%

---

# Avtalsbeslut

Den här guiden innehåller en omfattande implementeringsreferens för offertbeslut med hjälp av [!DNL Adobe Journey Optimizer] (AJO) Decisioning och [!DNL Adobe Real-Time Customer Data Platform] (RT-CDP). Det är utformat för lösningsarkitekter, marknadsföringsteknologer och implementeringstekniker som behöver implementera en centraliserad logik för val av erbjudanden som bestämmer nästa bästa erbjudande för varje kundprofil i olika kanaler.

Använd den här guiden för att förstå vad som behöver konfigureras, var det finns val och vilka kompromisser som gäller för varje beslut.

Mönstret skiljer&quot;vad som ska visas&quot; från kanallogiken&quot;var det ska visas&quot;, vilket möjliggör ett enhetligt och optimerat urval av erbjudanden för e-post, webben, mobilappar och andra kontaktytor. AJO Decisioning hanterar hela erbjudandets livscykel: skapande och kataloghantering av erbjudanden, regler för behörighet (vem som kan se varje erbjudande), rangordningsstrategier (hur man väljer bland giltiga erbjudanden), placeringar (där erbjudanden visas) och beslutsstrategier (som knyter ihop allt).

## Använd ärendeöversikt

Organisationer måste ofta presentera det mest relevanta erbjudandet, erbjudandet eller incitamentet för varje kund vid interaktionen. Oavsett om interaktionen sker i en e-postkampanj, på en webbplatshem, i en mobilapp eller vid en beslutspunkt under en flerstegsresa är utmaningen densamma: välj det optimala erbjudandet från en katalog med tillgängliga alternativ baserat på vem kunden är, vad de är kvalificerade för och vilket erbjudande som mest troligt leder till önskat resultat.

Detta hanteras genom att all logik för val av erbjudanden centraliseras i AJO beslutsmotor. I stället för att hårdkoda tilldelningar av erbjudanden i enskilda kampanjer eller kanaler utvärderar beslutsmotorn varje profils attribut, målgruppsmedlemskap och sammanhangsberoende signaler för att avgöra vilket som är det bästa erbjudandet i realtid. Denna centralisering säkerställer att samma kund får enhetliga, optimerade erbjudanden oavsett vilken kanal de använder.

Det här mönstret skiljer sig från kända webb-/apppersonaliseringar i omfånget - offertbeslut är kanalbaserat och centraliserat, medan personalisering för kända besökare fokuserar på digital ytanpassning. Det skiljer sig från beteenderekommendationer i katalogmodell - beslut om erbjudanden när den stödberättigande artikeluppsättningen styrs av affärsregler, behörighetskrav eller lagstadgade krav (kampanjer, finansiella produkter, incitament). Använd beteenderekommendation när objektuppsättningen är stor, ändras kontinuerligt och markeringen styrs av beteendemässiga likhets- eller tillhörighetssignaler (produktkataloger, innehållsbibliotek).

## Viktiga verksamhetsmål

Följande affärsmål stöds av det här användningsmönstret.

**[Leverera personaliserade kundupplevelser](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**
Skräddarsy innehåll, erbjudanden och budskap efter enskilda preferenser, beteenden och livscykelsteg.
**KPI:er:** engagemang, konverteringsgrader, kundnöjdhet (CSAT)

**[Öka korsförsäljning och merförsäljning](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)**
Marknadsför kompletterande och premiumbaserade produkter eller tjänster till befintliga kunder baserat på beteenden och inköpshistorik.
**KPI:er:**, merförsäljning/korsförsäljning %, inkrementell intäkt, kundens livstidsvärde

**[Öka kundlojalitet och livstidsvärde](../../business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)**
Fördjupa kundrelationerna och maximera det långsiktiga värdet genom lojalitetsprogram, belöningar och personaliserat engagemang.
**KPI:er:** Kundens livstidsvärde, kvarhållning, merförsäljning/korsförsäljning %

## Exempel på taktiska användningsfall

Följande scenarier visar hur offertbeslut kan tillämpas i praktiken.

- Nästa bästa erbjudande i e-postkampanjer - välj den mest relevanta kampanjen per mottagare vid sändning
- Realtidskampanjbanderoll på webbplats - beslut väljer erbjudandet vid sidladdning baserat på besökarens profil
- Personligt anpassat appkort med de bästa incitamenten för användarens livscykelstadium
- Enhetliga erbjudanden i flera kanaler - samma beslutslogik används för e-post, webben och push så att kunderna får en enhetlig upplevelse
- Dynamiskt kupong- eller rabattval baserat på kundvärdesnivå (t.ex. värdefulla kunder får ett premiumerbjudande)
- Produktuppgradering eller merförsäljning baserat på den aktuella prenumerationsnivån
- Personalisering av lojalitetserbjudanden baserat på nivå- och aktivitetshistorik

## Nyckeltal för prestanda

Följande nyckeltal hjälper till att mäta effektiviteten i en implementering av offertbeslut.

| KPI | Beskrivning | Mätningsmetod |
| --- | --- | --- |
| Ansvarsfrekvens för erbjudande | Andel levererade erbjudanden som resulterar i ett klick, inlösen eller konvertering | Erbjud klick eller inlösen/Totalt antal erbjudanden |
| Distribuera erbjudandeval | Andel av varje erbjudande som valts ut för alla beslut | Antal per erbjudande / Totalt antal utförda beslut |
| Reservfrekvens | Procent av beslut där inga personliga erbjudanden kvalificerades och reservlösningar användes | Reservvisningar/Totalt antal beslut |
| Konverteringsgrad | Procentandel av erbjudandemottagare som slutförde den önskade åtgärden (köp, registrering, inlösen) | Konvertering/Erbjud avtryck |
| Inkrementell intäkt | Intäkter som kan tillskrivas valda erbjudanden jämfört med en kontrollgrupp eller reserv | Inkomster från personaliserade erbjudanden - Inkomster från reserv/kontroll |
| Konsekvensresultat över flera kanaler | Procentandel profiler som tar emot samma erbjudande i flera kanaler i ett definierat fönster | Enhetliga erbjudanden / Totalt antal flerkanalsvisningar |
| Erbjud genomklickningshastighet | Procentandel erbjudandevisningar som resulterar i ett klick | Erbjud klickningar/Erbjud avtryck |

## Använd skiftlägesmönster

I det här avsnittet beskrivs funktionskedjan och mönsterdefinitionen för offertbeslut.

**Erbjudandebeslut**

Använd centraliserad beslutslogik för att välja nästa bästa erbjudande eller innehåll för en profil över alla kanaler.

**Funktionskedja:** Målgruppsutvärdering > Erbjudandebehörighet > Rankningsstrategi > Beslutskörning > Leverans > Rapportering

Se avsnittet [Implementeringsalternativ](#implementation-options) för hur varje disposition visas.

## Tillämpningar

Följande Adobe-program används i det här fallmönstret.

- **[!DNL Adobe Journey Optimizer](AJO)** - Beslutshanteringsmotor för att skapa erbjudanden, regler för kvalificering, rangordningsstrategier, praktik och beslutspolicyer; kanalkonfiguration och meddelandeskapande för erbjudanden; kampanj- och resekörning
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)** - Målgruppsutvärdering för erbjudandeberättigandesegment, profildata och beräknade attribut som används för kvalificering och rankning
- **[!DNL Adobe Experience Platform](AEP)** - Enhetligt profilarkiv, identitetsupplösning och datamängd som stöder både AJO och RT-CDP

## Foundationsfunktioner

Följande grundläggande funktioner måste finnas för det här användningsmönstret. För varje funktion anger statusen om den vanligtvis är obligatorisk, antas vara förkonfigurerad eller inte tillämplig.

| Funktionen Foundation | Status | Vad måste finnas på plats | Experience League referens |
| --- | --- | --- | --- |
| Administration och styrning | Antagen på plats | AJO-sandlåda med beslutsbehörighet aktiverat. Erbjudandehanteringsroller (Beslutsfattare, Erbjudandegodkännare) som tilldelats implementeringsteamet. | [Översikt över sandlådor](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/home), [Översikt över åtkomstkontroll](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Datamodellering och förberedelse | Obligatoriskt | Profilschemat måste innehålla attribut som används för regler för kvalificering av erbjudanden (t.ex. lojalitetsnivå, inköpshistorik, prenumerationstyp). Det bör finnas ett svars-/interaktionsschema för att spåra erbjudandevisningar, klickningar och konverteringar. | [Systemöversikt för XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [Grundläggande om schemakomposition](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| Datakällor och samling | Antagen på plats | Profilattribut som används i regler för behörighet måste vara aktuella. För webbleverans (alternativ B) måste Web SDK implementeras med AJO-tjänsten aktiverad på datastream. För e-postleverans måste profilattributen kunna matchas vid sändning. | [Webböversikt för SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home), [Konfigurera dataströmmar](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure) |
| Konfiguration av identitet och profil | Antagen på plats | Profilerna måste kunna lösas i alla kanaler där erbjudandena levereras. För enhetlighet i flerkanalserbjudandena är enhetlig identitet avgörande - samma profil måste kännas igen i e-post-, webb- och mobilsammanhang. Det krävs en edge-active merge-policy för att leverera webb/app i realtid. | [Översikt över identitetstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [Översikt över sammanslagningsprinciper](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| Målgruppsdefinition och segmentering | Obligatoriskt | Målgrupper som används som kriterier för att erbjuda kvalificering måste definieras och utvärderas (t.ex.&quot;värdefulla kunder&quot;,&quot;provanvändare&quot;,&quot;lojalitetsguldnivå&quot;). Utvärderingsmetoden måste matcha leveransfördröjningen - edge-utvärdering för webb/app, batch eller strömning i realtid för e-postkampanjer. | [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [Användargränssnittsguide för segmentbyggaren](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder) |

## Stödfunktioner

Följande funktioner förstärker det här användningsmönstret, men behövs inte för att köra kärnan.

| Stödfunktioner | Status | Varför det spelar någon roll | Experience League referens |
| --- | --- | --- | --- |
| Skapande av beräknat/härlett attribut | Rekommenderad | Kundens AI-benägenhetspoäng, beräkningar av livstidsvärden och engagemangsmått förbättrar effektiviteten i rankningsstrategin avsevärt. Beräknade attribut som&quot;dagar sedan senaste köp&quot; eller&quot;totala utgifter på 90 dagar&quot; ger exaktare regler för berättigande och formelbaserad rankning. | [Översikt över beräknade attribut](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview), [Översikt över AI för kunder](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview) |
| Livscykelhantering för data | Rekommenderad | Erbjud historik- och beslutsdata ackumuleras över tid. Lagringsprinciper (förfallodatum) bör konfigureras för händelsedatamängder för interaktion för att hantera lagring och uppfylla datalagringskrav. | [Översikt över livscykelhantering av avancerade data](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home), [Giltighetsperioder för datauppsättningar](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration) |
| Dataanvändningsetiketter och -tillämpning | Rekommenderad | Styrningsetiketter säkerställer att erbjudanden med känsliga målinriktningskriterier (t.ex. ekonomisk status, hälsovillkor) följer policyer för dataanvändning. Etiketter på fält som används i regler för behörighet förhindrar att erbjudandet riktas mot annat än regelefterlevnad. | [Översikt över datastyrning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [Översikt över etiketter för dataanvändning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/labels/overview) |
| Övervakning och observerbarhet | Rekommenderad | Beslutsmotorernas prestanda, reservfrekvenser och leveranshälsa för erbjudanden bör övervakas. Varningar för höga reservfrekvenser kan tyda på problem med felkonfigurering av berättiganderegler eller dataaktualitet. | [Aviseringsöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview), [Översikt över Insikter i observabilitet](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| Rapportering och analys | Ingår | Resultatrapportering av erbjudanden ingår i funktionskedjan (fas 7). Med CJA-analys kan ni mäta effektiviteten i olika kanaler, attribuera intäkter och identifiera optimeringsmöjligheter. | [CJA - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [Analysis Workspace - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home) |

## Programfunktioner

I den här planen används följande funktioner från programfunktionskatalogen. Funktioner mappas till implementeringsfaser i stället för till numrerade steg.

### [!DNL Journey Optimizer] (AJO)

I följande tabell visas AJO-funktioner och de implementeringsfaser där de är konfigurerade.

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Beslutsfattande | Fas 3: Beslutsinställningar | Skapa erbjudandeartiklar, definiera regler för behörighet, konfigurera rangordningsstrategier, skapa reserverbjudanden, definiera praktik och utforma beslutsstrategier |
| Kanalkonfiguration | Fas 4: Konfiguration av kanal och yta | Konfigurera e-post-, webb-, app- eller kodbaserade kanalytor för leverans av erbjudanden |
| Redigering av meddelanden | Fas 5: Konfiguration av innehåll och leverans | Designa meddelandemallar med placeringszoner; konfigurera kodbaserade upplevelser för leverans via webben/appar |
| Kampanjkörning | Fas 5: Konfiguration av innehåll och leverans | Kör schemalagda eller API-utlösta kampanjer som anropar beslutsprinciper (alternativ A) |
| Experimentera med innehåll | Fas 5: Konfiguration av innehåll och leverans | Valfritt A/B-testa olika rankningsstrategier eller erbjud kreativa varianter |
| Rapportering och prestandaanalys | Fas 7: Rapportering och prestandaövervakning | Övervaka fördelningen av erbjudanden, acceptansnivåer, reservnivåer och prestanda på kanalnivå |

### [!DNL Real-Time CDP] (RT-CDP)

I följande tabell visas RT-CDP-funktioner och de implementeringsfaser där de är konfigurerade.

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Målgruppsutvärdering | Fas 2: Målgruppsutvärdering | Definiera och utvärdera målgrupper som används för att uppfylla kraven för erbjudanden. Välj lämplig utvärderingsmetod (batch, streaming eller edge) |
| Profilberikning | Fas 1 (stöd): Beräknade attribut | Förbättra profiler med beräknade attribut och benägenhetspoäng som förbättrar effektiviteten i rankningsstrategin |

## Förutsättningar

Slutför följande krav innan du börjar implementera.

- [ ] AJO-sandlåda med funktioner för beslutshantering aktiverat
- [ ] användarroller med beslutsbehörigheter (skapa/redigera erbjudanden, ersättningar, beslut)
- [ ] Profilschemat innehåller attribut som krävs för att erbjuda behörighet (t.ex. lojalitetsnivå, kundsegment, prenumerationsnivå)
- [ ] Profildata är aktuella och har aktivt importerats för aktualitet av berättigandeattribut
- [ ] för alternativ A (e-post): Ytan på e-postkanalen har konfigurerats med verifierad underdomän och en värmad IP-pool
- [ ] för alternativ B (Web/App): Web SDK som implementerats med AJO-tjänsten aktiverad på datastream; edge-active merge policy konfigurerad
- [ ] för alternativ C (Resa): Researbetsytebehörigheter och minst en resestarthändelse eller konfigurerad målgrupp
- [ ] Erbjud kreativa resurser (bilder, kopia, CTA:er) som förberetts för varje erbjudande och monteringskombination
- [ ] Reserverbjudandeinnehåll har förberetts för varje placering
- [ ] målgrupper för regler för anbudsbehörighet som definieras och utvärderas i RT-CDP

## Implementeringsalternativ

I det här avsnittet beskrivs de tillgängliga implementeringsalternativen för offertbeslut. Varje alternativ har olika leveranskanaler och har olika skiftlägeskontext.

### Alternativ A: Beslut om e-posterbjudande

Det här alternativet är bäst om du väljer det bästa erbjudandet som ska ingå i utgående e-postkampanjer - kampanjmeddelanden, personalisering av nyhetsbrev, e-postmeddelanden i livscykeln med dynamiskt erbjudandeinnehåll. Beslutet fattas vid meddelanderenderingstid för varje mottagare.

#### Så här fungerar det

Beslutsprinciper anropas vid återgivning av e-postmeddelanden för att välja det bästa erbjudandet för varje mottagare. E-postmallen innehåller en offertplaceringszon där beslutsmotorn infogar det valda erbjudandets innehållsbeteckning (bild, HTML eller text). Vid sändning utvärderar motorn varje mottagares profil mot reglerna för anbudsbehörighet, tillämpar rangordningsstrategin och bäddar in innehållet i det vinnande erbjudandet i e-postmeddelandet.

Den här metoden fungerar med både schemalagda kampanjer (utvärderade vid körning av kampanjer) och reseinbäddade e-postmeddelanden (utvärderade när profilen når noden för meddelandeåtgärder). Innehållet i erbjudandet - bild, rubrik, brödtext och CTA - personaliseras per mottagare baserat på beslutsresultatet.

#### Viktiga överväganden

- Erbjudandets berättigande utvärderas vid sändning med hjälp av profilens aktuella tillstånd
- Det räcker med att utvärdera grupper eftersom beslut fattas vid meddelandeåtergivning
- Varje erbjudande behöver en HTML- eller bildåtergivning för e-postplacering
- Reserverbjudandet måste ha innehåll för varje e-postplacering som används

#### Fördelar

- Enklare implementeringsväg - använder standardkampanjer eller e-postleverans via resan
- Inga krav från SDK på klientsidan
- Fungerar med befintlig e-postinfrastruktur och kanalytor
- Stöd för stora målgruppsvolymer genom batchkampanjkörning

#### Begränsningar

- Beslut fattas vid sändning; det går inte att anpassa sig till beteendet efter sändning
- Erbjudandet är statiskt när e-postmeddelandet har skickats (inga uppdateringar i realtid)
- Begränsad till profilattribut som är tillgängliga i navprofilarkivet (inte kant)

#### Experience League-resurser

- [Leverera erbjudanden i meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Skapa en kampanj](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)

### Alternativ B: Beslut om erbjudande i realtid för webb/app

Det här alternativet passar bäst för val av erbjudanden i realtid på webbsidor eller mobilappar - kampanjbanners för hemsidor, widgetar för kontoinstrumentpanel, erbjudandekort i appen eller någon annan digital yta där erbjudandet ska väljas när sidan läses in eller skärmåtergivningen.

#### Så här fungerar det

Beslutsprinciper anropas vid sidinläsning eller appskärmsåtergivning via Edge Decisioning-nätverket eller kodbaserade upplevelser. När en besökare läser in en sida skickar Web SDK en förfrågan till Edge Network, som utvärderar besökarens edge-profil mot reglerna för erbjudandebehörighet och rankningsstrategier. Det valda erbjudandet returneras som svar och återges i den konfigurerade placeringen på den digitala ytan.

För kodbaserade upplevelser hämtar programmet beslutssvaret och återger erbjudandeinnehållet med hjälp av anpassad logik. För webbkanalsupplevelser kan AJO webbkanal mata in erbjudandeinnehållet direkt på sidan med visuell eller kodbaserad redigering.

#### Viktiga överväganden

- Kräver att SDK eller SDK för mobiler implementeras med AJO-tjänsten aktiverad på datastream
- Edge-aktiv kopplingsregel krävs för profilsökningar i realtid
- Målgrupper som används för kvalificering måste stödja edge-utvärdering (enkla attributkontroller och segmentmedlemskap)
- Erbjudanderepresentationer bör använda JSON- eller bild-URL-format för återgivning på klientsidan
- Tryckspårning måste implementeras för att hämta in offertvisningar och klickningar

#### Fördelar

- Val av sessionsrelaterade erbjudanden i realtid baserat på besökarens aktuella profiltillstånd
- Beslutsfördröjning under andra fasen via Edge Network
- Erbjudandena anpassar sig till de mest aktuella profildata som finns i kanten
- Stöd för A/B-testning av erbjudandestrategier via innehållsexperiment

#### Begränsningar

- Kräver implementering av SDK på klientsidan (Web SDK eller Mobile SDK)
- Edge-profilen har en delmängd av fullständiga attribut för hubbprofiler - komplexa regler för behörighet kanske inte utvärderas korrekt
- Edge-segment har begränsningar för segmentregelkomplexitet (inga tidsseriefrågor)
- Kräver frontendutveckling för anpassad återgivning i kodbaserade upplevelser

#### Experience League-resurser

- [Leverera erbjudanden med Edge Decisioning API](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [Kodbaserad upplevelsekanal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based-experience/get-started-code-based)

**Hur detta skiljer sig från anpassningsalternativ B för webbbesökare/appar:**

Infrastrukturen är identisk - båda använder AJO Decisioning i toppklass med Web SDK och en fullödig kopplingsstrategi. Skillnaden är katalogstyrningsmodellen. Det här alternativet styr en avgränsad erbjudandekatalog med regler för behörighet, spärrräknare och giltighetsdatum - använd den när affärsbegränsningar eller lagstadgade begränsningar avgör vilka erbjudanden som kan visas och hur ofta. [Känd besökares anpassning av webb/app ](known-visitor-web-app-personalization.md) Alternativ B väljer bland innehållsobjekt med hjälp av segmentmedlemskap eller rankningsstrategier utan livscykelhantering. Om objektuppsättningen är stor, ändras kontinuerligt och inte kräver begränsning eller behörighetskontroll ska du använda alternativet Känd besökare B i stället.

### Alternativ C: Vägbeslutsnod

Det här alternativet är bäst för att välja ett erbjudande inom en resa i flera steg - välj det bästa erbjudandet vid en beslutspunkt i en kundresa och leverera det sedan via nästa åtgärdsnod. Använd detta när erbjudandebeslutet ingår i ett större orkestreringsflöde med väntetider, villkor och flera meddelandeåtgärder.

#### Så här fungerar det

Beslutspolicyer anropas från en beslutsnod inom en arbetsyta i AJO. När en profil når beslutsnoden utvärderar motorn om erbjudandet är giltigt och rangordnas för att välja det optimala erbjudandet. Det valda erbjudandet informerar nästa meddelandeåtgärd - som erbjuder innehåll som ska inkluderas, vilken kanal som ska användas eller vilken kundgren som ska vidtas baserat på erbjudandets resultat.

Detta tillvägagångssätt möjliggör anpassningsbara resor där offertbeslutet påverkar efterföljande kundsteg. En resa kan till exempel välja det bästa erbjudandet, leverera det via e-post, vänta på engagemang och sedan följa upp med ett push-meddelande om erbjudandet inte öppnats.

#### Viktiga överväganden

- Resan måste utformas med en beslutsnod följt av en eller flera meddelandeåtgärdsnoder
- Erbjudandets berättigande utvärderas med hjälp av profilens tillstånd när profilen når beslutsnoden
- Väntestegen mellan beslut och leverans kan göra att profilens tillstånd ändras
- Kan kombineras med förgreningar av resan för att ta olika vägar baserat på vilket erbjudande som valts

#### Fördelar

- Integrerar urval av erbjudanden i flerstegsflöden
- Möjliggör anpassningsbara resor där erbjudandet påverkar efterföljande steg
- Stöd för flerkanalsleverans inom samma resa (e-post, push, SMS)
- Kan kombineras med resevillkor för uppföljning av anställningar efter erbjudande

#### Begränsningar

- Mer komplex att konfigurera än fristående kampanjbeslut
- Gränser för genomströmning på resa gäller (5 000 profiler per sekund för inträde)
- Beslutet är knutet till resesammanhanget - ändringar kräver att en ny version av resan görs
- Resan måste publiceras på nytt för att uppdateringar av erbjudandekatalogen eller beslutspolicyn ska börja gälla

#### Experience League-resurser

- [Leverera erbjudanden i meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Kom igång med resor](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)

### Jämförelse av alternativ

I följande tabell jämförs de tre implementeringsalternativen över de viktigaste kriterierna.

| Kriterier | Alternativ A: E-postbeslut | Alternativ B: Webb/app i realtid | Alternativ C: Vägbeslutsnod |
| --- | --- | --- | --- |
| Bäst för | E-postkampanjer i grupp med val av erbjudanden per mottagare | Erbjudandebanners i realtid på webb-/appytor | Erbjud urval i flerstegssamordnade resor |
| Beslutsfördröjning | Vid sändning (sekunder per mottagare vid batchåtergivning) | Undersekund (Edge Network) | Vid körning av kundnod (sekunder) |
| Kanal | E-post | Webb, mobilapp, kodbaserade ytor | Alla kanaler (e-post, push, SMS) under resan |
| SDK krävs | Nej | Ja (SDK eller SDK för mobiler) | Nej (för e-post/push); Ja (om webbkanalen är en reseåtgärd) |
| Målgruppsutvärdering | Batch- eller direktuppspelning | Edge | Batch, direktuppspelning eller kant (beroende på reseinmatning) |
| Profildatatyp | Fullständig navprofil | Edge-profil (delmängd) | Fullständig navprofil |
| Komplex | Lågt | Medium-High | Medelsvåra: |
| Genomflöde | Hög (kampanjvolymer) | Hög (Edge Network scale) | Medium (begränsningar för genomströmning av resor gäller) |

### Välj rätt alternativ

Använd följande vägledning för att välja det bästa implementeringsalternativet för ditt användningsfall.

- **Välj alternativ A** om det primära användningsexemplet är att välja det bästa erbjudandet per mottagare i utgående e-postkampanjer och ingen SDK på klientsidan är tillgänglig. Detta är den enklaste implementeringsvägen och fungerar bra för e-postreklam, nyhetsbrev och livscykelkampanjer.
- **Välj alternativ B** om erbjudanden måste väljas i realtid när en besökare läser in en webbsida eller öppnar en mobilapp. För detta krävs Web SDK eller Mobile SDK och en effektiv kopplingsregel, men det snabbaste och mest kontextuella valet av erbjudande.
- **Välj alternativ C** om erbjudandebeslutet är en del av en större kundresa med flera steg, väntan och villkorlig förgrening. Det här är det rätta valet när det valda erbjudandet ska påverka åtgärder för efterföljande kundresor eller när uppföljning i flera kanaler baserat på anställningserbjudandet behövs.
- **Kombinera alternativ** när erbjudanden måste levereras på ett enhetligt sätt i alla kanaler. Använd samma policy för alla tre alternativen för att se till att kunden ser samma erbjudande via e-post (alternativ A), på webbplatsen (alternativ B) och inom en uppföljning av resan (alternativ C).

## Implementeringsfaser

I följande faser beskrivs den kompletta implementeringssekvensen för anbudsbeslut.

### Fas 1: Validera grundläggande krav

**Programfunktion:** AEP: Datamodellering och förberedelser, AEP: Identitet- och profilkonfiguration

Den här fasen kontrollerar att det grundläggande datalagret stöder offertbeslut. Profilscheman måste innehålla de attribut som används i reglerna för behörighet, och identitetskonfigurationen måste aktivera matchning av flerkanalsprofiler.

#### Beslut: Profilattribut för behörighet

Bestäm vilka profilattribut som ska användas i reglerna för erbjudande.

>[!NOTE]
>Valet av profilattribut påverkar både utformningen av berättiganderegler och effektiviteten i rankningsstrategin. Ta hänsyn till beräknade attribut och benägenhetspoäng för att förbättra beslutskvaliteten.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Standardprofilattribut (förmånsnivå, inköpshistorik) | Attribut finns redan i profilschemat | Inga schemaändringar behövs. Verifiera dataaktualitet |
| Beräknade attribut (livstidsvärde, poäng för engagemang) | Kvalificering eller rankning beror på aggregerade beteendedata | Kräver S1-konfiguration, lägger till ett beroende av den beräknade uppdateringsreferensen för attribut |
| Kundens AI-benägenhetspoäng | Rankningen bör utnyttja ML-baserade prognoser | Kräver tillräckligt med utbildningsdata (10 000+ profiler med målhändelse), modellutbildning |

#### Information om nyckelkonfiguration

- Verifiera att profilschemat innehåller fält som det refereras till i regler för behörighet (t.ex. `_tenantId.loyaltyTier`, `_tenantId.subscriptionType`)
- Bekräfta att det finns ett schema för uppföljning av interaktion för att upptäcka, klicka och konvertera erbjudanden
- För alternativ B: Verifiera att en edge-active-sammanslagningsprincip är konfigurerad och att tjänsten AJO är aktiverad för Web SDK-datastream

#### Experience League-dokumentation

- [XDM - systemöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Aktivera ett schema för profil](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/union-schema)
- [Översikt över kopplingsprofiler](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### Fas 2: Konfigurera målgruppsutvärdering

**Programfunktion:** RT-CDP: Målgruppsutvärdering

I den här fasen definieras och utvärderas de målgrupper som används som kriterier för att erbjuda rätt till uppgradering. Dessa målgrupper avgör vilka kundsegment som kvalificerar sig för specifika erbjudanden (t.ex.&quot;värdefulla kunder&quot; kvalificerar sig för premiumerbjudanden,&quot;testanvändare&quot; kvalificerar sig för konverteringserbjudanden).

#### Beslut: Metod för utvärdering av målgrupper

Bestäm hur snabbt målgruppsmedlemskapet måste uppdateras för att vara kvalificerat för erbjudanden.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Batchutvärdering | Alternativ A (e-postkampanjer) där berättigandet utvärderas vid sändningstid | Enklast; alla segmentregeluttryck stöds; daglig uppdatering eller uppdatering på begäran |
| Utvärdering av strömning | Alternativ A eller C när det behövs nära realtidsuppdateringar mellan grupper | Automatiskt för berättigade segment; stöd för begränsade segmentregler (enstaka händelser, attributjämförelser) |
| Edge-utvärdering | Alternativ B (web/app real-time) där behörigheten måste utvärderas vid sidinläsning | Undersekund; krävs för webb-/apperbjudanden i realtid; begränsas till enkla attributkontroller och segmentmedlemskap |

**Gränssnittsnavigering:** Kund > Målgrupper > Skapa målgrupp > Skapa regel

#### Information om nyckelkonfiguration

- Definiera målgrupper för rätt att köpa (t.ex.&quot;Loyalty Gold Tier&quot;,&quot;High-Value Customers&quot;,&quot;Trial Users&quot;)
- Definiera undertryckande målgrupper om det behövs (t.ex.&quot;Nyligen mottaget erbjudande X&quot;)
- För alternativ B: Verifiera att berättigade målgrupper är kvalificerade för edge-utvärdering - undvik tidsseriefrågor och komplexa aggregeringar i segmentregeluttryck

#### Var alternativen skiljer sig

**För alternativ A (E-postbeslut):**
Utvärderingen av batchströmning eller strömning räcker. Publiken utvärderas före eller under kampanjkörningen. Komplexa segmentregeluttryck, inklusive tidsbaserade villkor och händelseaggregeringar, stöds fullt ut.

**För alternativ B (realtid för webb/app):**
Edge måste utvärderas. Publiken måste använda enkla attributkontroller eller villkor för segmentmedlemskap. Testa om kanten är berättigad genom att verifiera att segmentregeluttrycket är kvalificerat för kantsegmentering.

**För alternativ C (resebeslutsnod):**
Alla bedömningsmetoder fungerar beroende på vilka kriterier för reseanmälan som gäller. Om resan använder målgruppsbaserad anmälan matchar metoden för målgruppsbedömning kundens krav.

#### Experience League-dokumentation

- [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Direktuppspelningssegmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Edge segmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### Fas 3: Ange beslutsinställningar

**Programfunktion:** AJO: Bestämning

Detta är den centrala fasen där erbjudandekatalogen, reglerna för behörighet, rankningsstrategier och beslutspolicyer byggs. I den här fasen skapas den beslutsmotorkonfiguration som alla leveransalternativ (A, B, C) delar.

#### Beslut: Placeringskanal och innehållsformat

Bestäm var erbjudandena ska visas och i vilket format.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| E-post (HTML) | Alternativ A - Erbjud innehåll som återges som HTML i e-postbrödtexten | Stöder formatering; måste vara kompatibelt med e-postklienter |
| E-post (bild-URL) | Alternativ A - Erbjudandet återges som en värdbild i ett e-postmeddelande | Enklare; bilden måste finnas på webben och vara åtkomlig; ingen dynamisk text |
| Webb (HTML) | Alternativ B - Erbjudandet återges som HTML på en webbsida | Full layoutkontroll; stöder interaktiva element |
| Webb/mobil (JSON) | Alternativ B - Erbjud data som returneras som JSON för anpassad återgivning | Maximal flexibilitet; kräver framtagningsutveckling för att rendera |
| Kodbaserad (JSON) | Alternativ B - erbjuda data för kodbaserade upplevelseytor | Programkontroller återgivning; mest flexibel |

#### Beslut: Rankningsstrategi

Bestäm hur det bästa erbjudandet ska väljas bland giltiga erbjudanden.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Prioritetsbaserad (manuell) | Små erbjudandekataloger; explicita affärsregler för erbjudandebeställning | Lättaste att konfigurera; tilldela prioritetsvärde manuellt per erbjudande; deterministisk |
| Formelbaserat (anpassat uttryck) | Rankningen ska ta hänsyn till profilattribut (t.ex. lojalitetsnivå, senaste tid) | Flexibelt; använder profildata för att beräkna ett rangordningsresultat; kräver segmentregeluttryck |
| AI-rankad (automatisk optimering) | Kataloger med stora erbjudanden; vi vill att HTML ska optimera markeringen över tid | Kräver minst 1 000 konverteringshändelser för modellutbildning; lär sig av erbjudandeprestandadata |

#### Beslut: Erbjudandebegränsning

Bestäm om det ska finnas gränser för hur många gånger ett erbjudande visas.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Anfang per profil | Förhindra att samma erbjudande visas för många gånger för en kund | Undvik trötthet och få en fördröjning på några sekunder i högflödesscenarier |
| Global ändpunkt | Begränsa det totala antalet visningar för ett erbjudande för alla profiler (t.ex. begränsat lager) | Kontrollerar utbudet. När gränsen har nåtts utesluts erbjudandet från beslut |
| Ingen ände | Erbjudandena är obegränsade | Lättaste; lämpligt för alltid aktiverade kampanjer |

**Gränssnittsnavigering:** Komponenter > Beslutshantering > Placeringar/Regler/Erbjudanden/Beslut

#### Information om nyckelkonfiguration

1. **Skapa placeringar** - Definiera var erbjudandena visas genom att ange kanaltyp och innehållsformat för varje placering.
   - Gränssnitt: Komponenter > Beslutshantering > Placeringar
   - Skapa en placering per kanal/formatkombination (t.ex. &quot;Email Hero Banner - HTML&quot;, &quot;Web Homepage - JSON&quot;, &quot;Mobile App Card - JSON&quot;)

2. **Definiera regler för behörighet** - Skapa regler med hjälp av segmentregeluttryck som refererar till profilattribut eller målgruppsmedlemskap.
   - Gränssnitt: Komponenter > Beslutshantering > Regler
   - Regler kan referera till målgruppsmedlemskap, profilattribut (lojalitetsnivå, prenumerationstyp), datumbegränsningar eller sammanhangsberoende data

3. **Skapa personaliserade erbjudanden** - Bygg varje erbjudande med innehållsrepresentationer för varje placering, tilldela regler för behörighet, ange prioritet och konfigurera valfri begränsning.
   - Gränssnitt: Komponenter > Beslutshantering > Erbjudanden > Skapa erbjudande
   - Varje erbjudande måste innehålla en representation per placering (t.ex. HTML för e-post, JSON för webben)
   - Tilldela regler för behörighet för att styra vilka profiler som kan se varje erbjudande
   - Ange giltighetsdatum för erbjudandet (start/slut) och valfri frekvensbegränsning
   - Godkänn varje erbjudande för att få delta i beslut

4. **Skapa reserverbjudanden** - Skapa ett standarderbjudande för varje placering som visas när inget anpassat erbjudande kvalificerar sig.
   - Gränssnitt: Komponenter > Beslutshantering > Erbjudanden > Skapa reserverbjudande
   - Reservationen måste ha representationer för varje placering som används i beslutet

5. **Skapa samlingskvalificerare och samlingar** - Ordna erbjudanden i samlingar med kvalificeringstaggar.
   - UI: Komponenter > Beslutshantering > Samlingskvalificerare
   - Grupprelaterade erbjudanden (t.ex. &quot;Sommarkampanjer&quot;, &quot;Loyalty Rewards&quot;) för användning i beslutsomfattningar

6. **Skapa beslutsprinciper** - Bind placeringar, samlingar, rankningsstrategier och reserverbjudanden till körbara beslut.
   - Gränssnitt: Komponenter > Beslutshantering > Beslut > Skapa beslut
   - Varje beslutsomfattning länkar en placering till en samling och anger rangordningsmetoden

#### Experience League-dokumentation

- [Beslutsledning - översikt](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Skapa placeringar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Skapa beslutsregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Skapa personaliserade erbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Skapa reserverbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Skapa samlingar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Skapa samlingskvalificerare](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [Skapa beslut](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Rankningsstrategier](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Fas 4: Konfigurera kanal och yta

**Programfunktion:** AJO: Kanalkonfiguration

Den här fasen konfigurerar kanalytorna som erbjudandena kommer att levereras via. Konfigurationen beror på vilka implementeringsalternativ som används.

#### Beslut: Kanaltyp

Avgör vilken meddelandekanal som användningsfallet kräver.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| E-post | Alternativ A eller Alternativ C med e-postleverans | Kräver delegering av underdomän, IP-pool, avsändarinställningar |
| Webb | Alternativ B för leverans av webbsidor | Kräver Web SDK och datastream-konfiguration |
| I appen | Alternativ B för mobilappsleverans | Kräver Mobile SDK och push-autentiseringsuppgifter |
| Kodbaserad upplevelse | Alternativ B för anpassade återgivningsytor | Mest flexibel; återgivning hanteras i programmet |

#### Var alternativen skiljer sig

**För alternativ A (E-postbeslut):**
- Gränssnitt: Administration > Kanaler > Kanalytor > Skapa yta (e-post)
- Konfigurera underdomän, IP-pool, avsändarens namn/e-postadress, svar, inställningar för att avbryta prenumeration
- Verifiera SPF-, DKIM- och DMARC-poster för den sändande underdomänen

**För alternativ B (realtid för webb/app):**
- Gränssnitt: Administration > Kanaler > Kanalytor > Skapa yta (webb eller app)
- För webben: Konfigurera webbytans URL-mönster
- För kodbaserade upplevelser: Definiera yta-URI för programmet
- Kontrollera att AJO-tjänsten är aktiverad för datastream

**För alternativ C (resebeslutsnod):**
- Konfigurera kanalytor för varje kanal som används i resan (e-post, push, SMS eller webb)
- Varje åtgärd för att skicka ett meddelande kräver en motsvarande aktiv kanalyta

#### Experience League-dokumentation

- [Kom igång med e-postkonfiguration](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Inställningar för e-postyta](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Delegera underdomäner](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Konfigurera kanal för push-meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Fas 5: Konfigurera innehåll och leverans

**Programfunktion:** AJO: Meddelanderedigering, AJO: Kampanjkörning

Den här fasen utformar meddelandemallar eller upplevelseytor som visar det valda erbjudandet och konfigurerar sedan leveransmekanismen (kampanj, resa eller kodbaserad upplevelse).

#### Beslut: Innehållsstrategi för anbudsåtergivning

Bestäm hur erbjudandeinnehållet ska integreras i meddelandet eller upplevelsen.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Avtalskomponent i e-post-Designer | Alternativ A - Bädda in erbjudandeplacering i e-postmall | Dra-och-släpp; erbjud innehållsåtergivning automatiskt baserat på beslutsresultatet |
| Kodbaserad erfarenhet av beslutspolitik | Alternativ B - data hämtas och återges | Maximal kontroll över återgivning; kräver framtagning |
| Resemeddelandeåtgärd med inbäddat beslut | Alternativ C - Nodmatningar för beslut erbjuder innehåll i kundresan | Val och leverans av erbjudanden är samordnade inom reseflödet |

#### Beslut: Kampanjtyp (endast alternativ A)

Bestäm om detta är en schemalagd marknadsföringskampanj eller en API-utlöst kampanj.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Schemalagd kampanj | Engångs- eller återkommande batchutskick till en angiven målgrupp | Målgruppen utvärderades vid körningstid; ange datum/tid eller upprepning |
| API-utlöst kampanj | Händelsedrivna eller systemutlösta meddelanden skickas till angivna profiler | Profiler angivna i utlösarnyttolast; stöder upp till 20 mottagare per begäran |

#### Var alternativen skiljer sig

**För alternativ A (E-postbeslut):**

1. Skriv e-postmeddelandet med e-post-Designer
   - Gränssnitt: Kampanjer > Skapa kampanj > Välj e-post > Redigera innehåll
   - Infoga en komponent för anbudsbeslut i e-postlayouten för att definiera placeringszonen
   - Lägg till personaliseringstoken för innehåll på profilnivå (namn, lojalitetsnivå)
   - Konfigurera ämnesrad och preheader med personlig anpassning (tillval)
2. Skapa och konfigurera kampanjen
   - Gränssnitt: Kampanjer > Skapa kampanj > Schemalagd eller API-utlöst
   - Bind målgruppen och välj kanalyta
   - Ange körningsschema eller API-utlösarkonfiguration
   - Granska och aktivera kampanjen

**För alternativ B (realtid för webb/app):**

1. Konfigurera kodbaserad upplevelse eller webbkanal
   - Gränssnitt: Kampanjer > Skapa kampanj > Kodbaserad upplevelse (eller webben)
   - Länka beslutspolicyn till upplevelsen
   - Definiera återgivningsformatet (JSON-svar för kodbaserad, visuell redigerare för webbkanal)
2. Implementera rendering på klientsidan
   - Använd Web SDK `sendEvent`-svaret för att hämta det valda erbjudandet
   - Rendera erbjudandeinnehållet på den avsedda placeringen på sidan
   - Implementera intryck och klickspårning

**För alternativ C (resebeslutsnod):**

1. Designa resan med en beslutsnod
   - Användargränssnitt: Resor > Skapa resa > Lägg till beslutsnod
   - Konfigurera beslutsnoden för att anropa beslutsprincipen från fas 3
2. Lägg till meddelandeåtgärdsnoder efter beslutet
   - Konfigurera e-post-, push- eller SMS-åtgärder som refererar till det valda erbjudandet
   - Lägg till väntesteg, villkor eller förgreningar baserat på offertengagemang
3. Publicera resan

#### Experience League-dokumentation

- [Leverera erbjudanden i meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Designa e-postinnehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Lägg till personalisering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Skapa en kampanj](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Kom igång med resor](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Förhandsgranska och testa ditt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### Fas 6: Testa och validera

**Programfunktion:** AJO: Beslutsfattare, AJO: Meddelanderedigering

Denna fas kontrollerar att beslutsmotorn returnerar rätt erbjudanden för testprofiler och att erbjudandeinnehållet återges korrekt i varje leveranskanal.

#### Testa beslutslogik

Använd testprofiler med kända attribut för att verifiera att rätt erbjudanden har valts ut baserat på behörighet och rankning.

- Skapa testprofiler som matchar olika behörighetskriterier (t.ex. Gold-nivå, Silver-nivå, Trial-användare)
- Verifiera att varje testprofil tar emot det förväntade erbjudandet
- Verifiera att profiler som inte matchar några regler för behörighet får reserverbjudandet

#### Testa innehållsåtergivning

Förhandsgranska innehållet i varje leveranskanal.

- För alternativ A: Använd e-postförhandsgranskning med testprofiler för att verifiera att erbjudandeinnehållet återges korrekt
- Alternativ B: Testa Edge Decisionings-svaret i en testmiljö
- Alternativ C: Använd testläge för resan för att verifiera att beslutsnoden väljs korrekt

#### Validera visningsspårning

Bekräfta att visningar, klickningar och konverteringar spåras.

- Verifiera att interaktionshändelser för erbjudanden visas i spårningsdatauppsättningarna
- Bekräfta attribuering mellan offertvisningar och konverteringar i efterföljande led

#### Experience League-dokumentation

- [Förhandsgranska och testa ditt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [Skicka e-postkorrektur](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/proofs)

### Fas 7: Konfigurera rapportering och prestandaövervakning

**Programfunktion:** AJO: Rapporterings- och prestandaanalys

I den här fasen skapas rapporter för att spåra fördelningen av erbjudanden, acceptansgrader, konverteringseffekt och reservfrekvenser. Denna fas omfattar både AJO-rapporter och CJA-baserad flerkanalsanalys.

#### Beslut: Rapporteringsmetod

Fastställ vilka rapporteringsverktyg som behövs för att analysera resultatet.

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Endast inbyggda AJO-rapporter | Operativ övervakning av enskilda kampanjer eller resor | Snabb åtkomst, inbyggda mått för leverans och engagemang, begränsad entitetsanalys |
| Analys av arbetsytan i CJA | Erbjudandeeffektivitet i flera kanaler, intäktsattribuering, funnel-analys | Kräver CJA anslutning och datavy; djupare analysfunktioner |
| Både AJO och CJA | Full operativ och analytisk täckning | Rekommenderas för produktionsimplementationer; AJO för realtidsövervakning, CJA för strategisk analys |

#### Information om nyckelkonfiguration

1. **Inbyggd AJO-rapportering** - Övervaka kampanjer eller resan med hjälp av inbyggda rapporter.
   - Gränssnitt: Campaigns > Select campaign > All time report (eller Live report)
   - Granska de erbjudandespecifika mätvärdena: antal visningar per erbjudande, klickfrekvens per erbjudande, reservfrekvens
   - Monitor delivery funnel: Targeted > Skickat > Delired > Open > Click

2. **CJA-analys (rekommenderas)** - Skapa instrumentpaneler för kanalövergripande erbjudanden.
   - Konfigurera en CJA-anslutning med AJO-datauppsättningar för interaktion
   - Skapa en datavy med erbjudandespecifika dimensioner (erbjudandenamn, placering, beslut) och mätvärden (visningar, klick, konverteringar)
   - Bygg en analys av arbetsytan för: distribution av erbjudanden, acceptansgrad per segment, intäktspåverkan, enhetlighet i flerkanalserbjudanden

#### Experience League-dokumentation

- [Global kampanjrapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Global reserapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Arbeta med Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Analysis Workspace - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

## Implementeringsöverväganden

Det här avsnittet handlar om säkerhetsutkast, vanliga fallgropar, bästa praxis och avräkningsbeslut för implementering av offertbeslut.

### Gardrutor och begränsningar

Tänk på följande plattformsskydd och -begränsningar när du planerar implementeringen.

- Högst 10 000 godkända anpassade erbjudanden per sandlåda - [Beslutshanteringssystem](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- Högst 30 praktik per beslut
- Maximalt 30 samlingsomfång per beslutsbegäran
- AI-rankningsmodeller kräver minst 1 000 konverteringshändelser för utbildning
- Räknare för buffertbegränsning kan ha en fördröjning på upp till några sekunder i högflödesscenarier
- Edge beslut är begränsade till profilattribut som är tillgängliga i edge-profilarkivet
- Maximalt 4 000 segmentdefinitioner per sandlåda - [Plattformsskydd](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Endast en sammanfogningsprincip kan vara aktiv i Edge per sandlåda
- Max 500 aktiva livekampanjer per sandlåda
- Gräns för antal resenärer: 5 000 profiler per sekund
- Högst 10 kanalytor per kanaltyp per sandlåda

### Vanliga fallgropar

Undvik problem som ofta uppstår under implementeringen.

- **Beslut returnerar alltid reserverbjudande:** Detta innebär vanligtvis att personaliserade erbjudanden inte godkänns, ligger utanför giltighetsdatumintervallet eller att reglerna för behörighet inte matchar testprofilens attribut. Verifiera varje villkor: godkännandestatus, datumintervall och exakthet för segmentregeluttryck. Kontrollera också att begränsningen inte har nåtts.
- **Erbjudandet visas inte i samlingen:** Kontrollera att erbjudandet har taggats med rätt samlingskvalificerare och att samlingsfiltret matchar. Erbjudandena måste vara både taggade och godkända för att kunna förekomma i de samlingsbaserade beslutsomfången.
- **Rankningsformeln används inte:** Kontrollera att formeln är syntaktiskt giltig och refererar till tillgängliga profilattribut. Formelfel återgår i tysthet till prioritetsbaserad rankning utan synligt fel.
- **Edge-leverans returnerar tom personalisering:** Kontrollera att datastream har konfigurerats med tjänsten [!DNL Adobe Journey Optimizer] aktiverad och att beslutsomfånget är korrekt formaterat. Kontrollera att den edge-active-sammanslagningsprincipen finns.
- **Inkonsekventa erbjudanden över olika kanaler:** Om olika beslutsprinciper används per kanal kan samma profil ta emot olika erbjudanden. Använd en enda beslutspolicy i alla kanaler för enhetlighet, eller acceptera avsiktliga skillnader baserat på kanalspecifika placeringar.
- **Erbjud innehåll som inte återges i e-post:** Kontrollera att erbjudandet har en innehållsrepresentation som matchar e-postplaceringsformatet (HTML eller bild-URL). Saknade representationer resulterar i tomma placeringszoner.

### God praxis

Följ de här rekommendationerna för en lyckad implementering av offertbeslut.

- **Börja med en liten erbjudandekatalog och iterera** - Börja med 5-10 erbjudanden och utöka allt eftersom beslutsramverket valideras. Detta förenklar felsökning och säkerställer att reglerna för behörighet fungerar korrekt före skalning.
- **Använd samlingskvalificerare strategiskt** - Tagga erbjudanden per kategori (t.ex. &quot;Anskaffning&quot;, &quot;Kvarhållning&quot;, &quot;merförsäljning&quot;) för att möjliggöra flexibla samlingsbaserade beslutsomfattningar som kan återanvändas mellan kampanjer och resor.
- **Skapa alltid meningsfulla reserverbjudanden** - Reserverbjudanden är inte bara ett säkerhetsnät. De är standardupplevelsen för profiler som inte matchar någon behörighetsregel. Investera i reservinnehåll som ger värde även utan personalisering.
- **Behörighetsreglerna för design utesluter varandra där det är möjligt** - När flera erbjudanden överlappar varandra blir rankningsstrategin avgörande. Om det i affärskraven fastställs ett specifikt erbjudande för ett visst segment, kan du göra reglerna för behörighet ömsesidigt uteslutande i stället för att enbart förlita dig på rangordningen.
- **Testa med kantrepresentativa profiler för alternativ B** - Edge-profiler innehåller en delmängd av hubbprofilattribut. Testa med profiler som har edge-available-attribut för att säkerställa att kvalificeringen utvärderas korrekt i produktionen.
- **Övervaka reservfrekvenser som ett hälsomått** - en hög reservfrekvens (över 20-30 %) anger att erbjudandekatalogen inte täcker tillräckligt många kundsegment. Utöka erbjudandekatalogen eller bredda reglerna för behörighet.
- **Versionsbeslutsprinciper i stället för att redigera live-principer** - Skapa en ny version av beslutspolicyn i stället för att ändra en aktiv. Detta förhindrar avbrott i livekampanjer och möjliggör A/B-jämförelse av beslutsstrategier.

### Avvecklingsbeslut

Tänk på följande när du ska fatta beslut om arkitektur och konfiguration.

#### Kvalificeringsprecision jämfört med täckning

Nära regler för behörighet säkerställer att varje erbjudande endast når de mest relevanta profilerna, men kan resultera i höga reservpriser när profilerna inte matchar något erbjudande. Många regler för berättigande maximerar täckningen för erbjudandet men minskar precisionen för personalisering.

- **Nära berättigandeförmåner:** Högre acceptansgrad, bättre personalisering, lägre utmattning
- **Höga berättigandeförmåner:** Lägre reservfrekvenser, fler profiler tar emot personaliserade erbjudanden, enklare regelhantering
- **Rekommendation:** Börja med bredare regler för behörighet och tätare dem baserat på prestandadata. Övervaka reservfrekvenser och acceptansfrekvenser för att hitta rätt balans. Använd rankningsstrategier för att skilja mellan allmänt berättigade erbjudanden.

#### Prioritetsbaserad eller AI-rankad rankning

Prioritetsbaserad rankning ger företaget full kontroll över vilka erbjudanden som visas, medan AI-rankad optimerar konverteringen men minskar den mänskliga kontrollen över valet av erbjudanden.

- **Prioritetsbaserade fördelar:** Affärskontroll, förutsägbarhet, inga krav på utbildningsdata, omedelbar driftsättning
- **AI-rankade tjänster:** Konverteringsoptimering, upptäckt av oväntade mönster, automatisk anpassning till förändrade kundbeteenden
- **Rekommendation:** Använd prioritetsbaserad rankning för inledande lanseringar och myndighetskänsliga erbjudanden där affärskontroll är av största vikt. Övergång till AI-rankad för högvolymsoptimerade användningsfall när det finns tillräckligt med konverteringsdata (1 000+ händelser).

#### Policyer för ett enda beslut jämfört med riktlinjer för beslut per kanal

En enda beslutspolicy säkerställer enhetlighet i alla kanaler, men begränsar optimeringen per kanal. Policyer per kanal möjliggör kanalspecifik rankning och kvalificering, men riskerar inkonsekventa kundupplevelser.

- **Enkel princip prioriterar:** Konsekvens över flera kanaler, enklare hantering, enhetlig rapportering
- **Policyer per kanal ger följande fördelar:** Kanaloptimerad rankning, kanalspecifik behörighet (t.ex. webbaserade erbjudanden), oberoende iteration
- **Rekommendation:** Börja med en enda beslutsprincip för enhetlighet mellan kanaler. Skapa profiler per kanal endast när affärsbehoven kräver kanalspecifika strategier (t.ex. webbexklusiv Flash-försäljning).

#### Hubbbeslut (alternativ A/C) jämfört med kantbeslut (alternativ B)

Hubbbeslut har åtkomst till den fullständiga profilen men fungerar vid sändning. Edge-beslut körs i realtid med delsekundsfördröjning, men är begränsat till profilattribut som är tillgängliga på kanten.

- **Navet för beslut:** Åtkomst till fullständiga profildata, komplexa regler för behörighet, gruppkampanjvolymer
- **Edge-beslutsstöd prioriterar:** Realtidskontext, sessionsanpassning, subsekundssvar
- **Rekommendation:** Använd navbeslut för utgående kanaler (e-post, push) där fullständiga profildata förbättrar erbjudanderelevansen. Använd edge-decimering för inkommande kanaler (webb, app) där realtidsrespons är avgörande. Se till att reglerna för behörighet endast används för Edge-attribut.

## Relaterad dokumentation

Följande resurser innehåller ytterligare information om komponenterna som används i det här användningsmönstret.

### Beslutshantering

- [Beslutsledning - översikt](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [Skapa placeringar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [Skapa beslutsregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [Skapa personaliserade erbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [Skapa reserverbjudanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [Skapa samlingar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [Skapa samlingskvalificerare](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [Skapa beslut](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [Rankningsstrategier](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### Erbjudandeleverans

- [Leverera erbjudanden i meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Leverera erbjudanden med Edge Decisioning API](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [Leverera erbjudanden med hjälp av besluts-API](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/decisioning-api)

### Kanalkonfiguration

- [Kom igång med e-postkonfiguration](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Inställningar för e-postyta](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Delegera underdomäner](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Konfigurera kanal för push-meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [Konfigurera SMS-kanal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)

### Framtagning och personalisering av meddelanden

- [Designa e-postinnehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Lägg till personalisering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization syntax](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Dynamiskt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Arbeta med innehållsmallar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Förhandsgranska och testa ditt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### Kampanjer och resor

- [Kom igång med kampanjer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [Skapa en kampanj](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [Kom igång med resor](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)

### Innehållsexperiment

- [Kom igång med innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Skapa ett innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)

### Målgrupper och segmentering

- [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Direktuppspelningssegmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Edge segmentering](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### Profil och identitet

- [Översikt över identitetstjänsten](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [Översikt över kopplingsprofiler](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [Översikt över beräknade attribut](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Översikt över AI för kunder](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### Datamodellering och insamling

- [XDM - systemöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [SDK - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Konfigurera datastreams](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)

### Rapportering och analys

- [Global kampanjrapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Global reserapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Arbeta med Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [CJA - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Analysis Workspace - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

### Datastyrning och livscykel

- [Översikt över dataförvaltning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Översikt över etiketter för dataanvändning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/labels/overview)
- [Översikt över livscykelhantering av avancerade data](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)
- [Samtycke i Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### Skyddsräcken

- [Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [Garantier för kundprofiler i realtid](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)

### Självstudiekurser

- [API för beslutshantering - komma igång](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/getting-started)
