---
title: Målgruppsaktivering
description: Lär dig hur du utvärderar och publicerar målgruppssegment till externa mål för målinriktning eller nedtryckning med Adobe Real-Time CDP.
solution: Real-Time Customer Data Platform, Experience Platform
exl-id: b0b9d937-45d2-48f9-ac4c-3611c6e35f58
source-git-commit: ccfd8c987a0090ca690e15a4bd89f4d96ec9c01f
workflow-type: tm+mt
source-wordcount: '7005'
ht-degree: 0%

---

# Målgruppsaktivering

Den här guiden innehåller en fullständig implementeringsreferens för aktivering av målgrupper från Adobe [!DNL Real-Time Customer Data Platform] (RT-CDP) till externa mål. Det är utformat för lösningsarkitekter, marknadsföringsteknologer och implementeringstekniker som behöver utvärdera målgruppssegment och publicera dem på annonsplattformar, molnlagring, CRM-system eller datapartners för målinriktning, undertryckande, lookalike-modellering eller analysberikning.

Den presenterar alla genomförbara implementeringsalternativ med en avbrottsanalys, beslutsvägledning, navigeringsvägar för användargränssnitt och referenser till Experience League-dokumentation.

Guiden täcker hela livscykeln för målgruppsaktivering - från att definiera och utvärdera målgruppssegment till att konfigurera målgruppsanslutningar och publicera målgrupper, till att övervaka aktiveringshälsokontroll och kontrollera att styrningen följs.

## Använd ärendeöversikt

Organisationer måste kunna leverera målgruppsdata till externa system för att kunna driva betalmediekampanjer, förbättra CRM-register, dela data med partners eller flöda analyser längre fram i kedjan. Audience Activation to Destinations är det grundläggande aktiveringsmönstret i RT-CDP: det utvärderar vilka profiler som kvalificerar sig för en målgrupp, ansluter till en eller flera externa destinationer, mappar profilattribut till målspecifika fält och publicerar målgruppen för nedladdning.

Det här mönstret används när målet är att hämta målgruppsdata till ett externt system i rätt format vid rätt tidpunkt. Det handlar inte om meddelandeleverans, anpassning av webbplatser eller analys. Det är den vanligaste utgångspunkten för RT-CDP-implementeringar och fungerar som en byggsten som andra mönster utgör ovanpå.

Typiska intressenter är bland annat digitala marknadsföringsteam som hanterar betalda medier, datateam som anrikar lagerställen, CRM-team som förbereder kontaktlistor för kampanjer och integritetsteam som ser till att företagsstyrningen följs när det gäller utgående dataflöden.

## Viktiga verksamhetsmål

Följande affärsmål behandlas i det här användningsmönstret.

### Skaffa nya kunder

Utöka kundbasen med riktade kampanjer, lookalike-målgrupper och optimering av betalda medier.

**KPI:er:** Nya kunder, Kundanskaffningskostnad, Prospekt/Leadkonvertering

[Läs mer om hur man skaffar nya kunder](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

### Minska anskaffningskostnaden

Förbättra målinriktningens effektivitet, hindra befintliga kunder från att värva kampanjer och optimera medieinvesteringarna.

**KPI:er:** Kundanskaffningskostnad, kostnad per lead, effektivitet

[Läs mer om hur man minskar kundvärvningskostnaderna](/help/blueprints/business-objectives/cost-efficiency/reduce-customer-acquisition-cost.md)

### Optimera marknadsföringsbudgeten och avkastningen

Förbättra avkastningen på marknadsföringsinvesteringar genom bättre målgruppsanpassning, attribuering, dämpande av målgrupper och budgettilldelning.

**KPI:er:** Kostnadsbesparingar, Kundanskaffningskostnad, Inkrementella intäkter

[Läs mer om optimering av marknadsföringsutgifter och avkastning](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)

## Exempel på taktiska användningsfall

- **Målgruppsanpassning för annonsplattformar** - Lyft kvalificerade segment till betalda medieplattformar för kampanjmålinriktning
- **Betalande mediaundertryckning av befintliga kunder** - Uteslut kända kunder från värvningskampanjer på annonsplattformar för att slippa slösa utgifter
- **Lookalike-målgrupper** - Lyft värdefulla kundsegment till Facebook, Google Ads eller The Trade Desk som dirigerade målgrupper för lookalike-expansion
- **CRM-synkronisering för försäljningsaktivering** - Aktivera målgrupper med hög återgivning eller högt värde så att säljarna kan prioritera utåtriktade aktiviteter
- **Målgruppsdelning** - Dela kvalificerade målgruppssegment med datapartners för målinriktning eller mätning genom samarbete
- **Export av molnlagring för datalagerberikning** - Exportera målgruppsmedlemskap och profilattribut till Amazon S3, Azure Blob, Google Cloud Storage eller SFTP för analyser längre fram i kedjan
- **Återmarknadsföring av målgruppen** - Aktivera webbplatsbesökare som inte konverterade till återmarknadsföringsplattformar
- **Synkronisering av kontaktlistor med e-postleverantörer** - Överför målgruppsmedlemskap till e-postplattformar från tredje part för koordinerad utåtriktad marknadsföring

## Nyckeltal för prestanda

| KPI | Beskrivning | Riktlinjer för mätning |
| --- | --- | --- |
| Kundanskaffningskostnad | Kostnader för att köpa en ny kund via aktiverade målgrupper | Medieutgifter totalt/nya kunder som tillskrivs aktiverade målgrupper |
| Matchningsfrekvens för målgrupp | Procentandel aktiverade profiler som matchats mot målet | Profiler som matchar målet/profiler som exporteras från RT-CDP |
| Undertrycksbesparingar | Medieutgifter som undviks genom att befintliga kunder hindras från att köpa kampanjer | Uppskattad storlek på ignorerad målgrupp i CPM x |
| Aktiveringsleveranshastighet | Procentandel profiler som levererats till målet | Levererade profiler/profiler i källgruppen |
| Aktiveringstid | Förfluten tid från målgruppsdefinition till första leverans på målet | Mät från segmentskapande till första bekräftade dataflödeskörning |
| Målgruppsanpassning | Justering mellan förväntad och faktisk målgruppsstorlek på målet | Antal målgrupper/RT-CDP antal målgrupper |

## Använd skiftlägesmönster

**Audience Activation till mål** - Utvärdera och publicera ett målgruppssegment till externa mål för målgruppsanpassning eller inaktivering.

**Funktionskedja:** Målutvärdering > Målkonfiguration > Audience Activation > Övervakning

## Tillämpningar

- **Adobe [!DNL Real-Time Customer Data Platform] (RT-CDP)** - Målgruppsutvärdering, målgruppshantering, målgruppsaktivering, samtycke och styrning
- **Adobe [!DNL Experience Platform] (AEP)** - Profilarkiv, identitetstjänst, segmenteringsmotor, datastyrning

## Foundationsfunktioner

Följande grundläggande funktioner måste finnas för det här användningsmönstret. För varje funktion anger statusen om den vanligtvis är obligatorisk, antas vara förkonfigurerad eller inte tillämplig.

| Funktionen Foundation | Status | Vad måste finnas på plats | Experience League referens |
| --- | --- | --- | --- |
| Administration och styrning | Antagen på plats | RT-CDP-sandlådan har etablerats och är aktiv. Målhanterings- och aktiveringsbehörigheter som tilldelats implementeringsroller. Referenser till målkontot som är tillgängliga för målplattformarna. | [Översikt över sandlådor](https://experienceleague.adobe.com/sv/docs/experience-platform/sandbox/home), [Översikt över åtkomstkontroll](https://experienceleague.adobe.com/sv/docs/experience-platform/access-control/home) |
| Datamodellering och förberedelse | Obligatoriskt | Profilschemat måste innehålla attribut som mappas till målfält (t.ex. e-post, telefon, hash-kodade identifierare, demografiska attribut). Schemat måste vara profilaktiverat med datauppsättningar som aktivt tar emot data. | [Systemöversikt för XDM](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/home), [Grundläggande om schemakomposition](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/schema/composition) |
| Datakällor och samling | Antagen på plats | Profildata som ligger till grund för målgruppsutvärderingen måste vara inkapslade och aktuella. Inmatningsledningar för batchströmning och/eller strömning i drift. Web SDK, källanslutningar eller batchimport som levererar data till profilaktiverade datauppsättningar. | [Källor - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/home), [Web SDK - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/web-sdk/home) |
| Konfiguration av identitet och profil | Obligatoriskt | Identitetsnamnutrymmen för målmatchning måste konfigureras (t.ex. hashas email for Facebook Custom Audiences, Google Ads Customer Match). Sammanslagningspolicyer måste producera enhetliga profiler med alla attribut som krävs för aktivering. | [Översikt över identitetstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/home), [Översikt över sammanslagningsprinciper](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/merge-policies/overview) |
| Målgruppsdefinition och segmentering | Obligatoriskt | Målgrupper som definierats med Segment Builder, Audience Composition eller Federated Audience Composition. Utvärderingsmetod (batch, strömning eller kant) som väljs baserat på latensbehov vid aktivering. Denna funktion utövas i fas 1 av denna plan. | [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/home), [Användargränssnittsguide för segmentbyggaren](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/ui/segment-builder) |

## Stödfunktioner

Följande funktioner förstärker det här användningsmönstret, men behövs inte för att köra kärnan.

| Stödfunktioner | Status | Varför det spelar någon roll | Experience League referens |
| --- | --- | --- | --- |
| Skapande av beräknat/härlett attribut | Rekommenderad | Beräknade attribut som livstidsvärde, engagemangsmusik eller benägenhetspoäng förbättrar målgruppens precision och ger berikande attribut att mappa till mål. Särskilt värdefullt när destinationerna drar nytta av värdebaserad eller poängbaserad målgruppssegmentering. | [Översikt över beräknade attribut](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/computed-attributes/overview) |
| Livscykelhantering för data | Rekommenderad | Datauppsättnings- och profilförfallopolicyer säkerställer att data är aktuella och att de följs. Konfiguration av samtycke garanterar att endast godkända profiler aktiveras. Viktigt för regelefterlevnad vid export av data till externa system. | [Översikt över livscykelhantering av avancerade data](https://experienceleague.adobe.com/sv/docs/experience-platform/data-lifecycle/home) |
| Dataanvändningsetiketter och -tillämpning | Rekommenderad | Etiketter och policyer för styrning förhindrar aktivering av begränsade data till obehöriga destinationer (t.ex. PII till annonsnätverk, känsliga segment till datapartners). Särskilt viktigt för målgruppsaktivering i externa tredjepartssystem. | [Översikt över datastyrning](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/home), [Översikt över etiketter för dataanvändning](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/labels/overview) |
| Övervakning och observerbarhet | Ingår | Aktiveringsövervakning ingår i funktionskedjan (fas 5). Omfattar övervakning av dataflöde, leveransstatusaviseringar, spårning av målgruppspopulationer och synlighet för licensanvändning. | [Övervaka måldataflöden](https://experienceleague.adobe.com/sv/docs/experience-platform/dataflows/ui/monitor-destinations), [Översikt över aviseringar](https://experienceleague.adobe.com/sv/docs/experience-platform/observability/alerts/overview) |
| Rapportering och analys | Rekommenderad | CJA analys av målgruppens aktiveringseffektivitet möjliggör mätning av prestanda för aktiverade målgrupper (t.ex. konverteringshöjning från nedtryckning, ROAS från lookalike-målgrupper). | [CJA - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-overview/cja-overview) |

## Programfunktioner

I den här planen används följande funktioner från programfunktionskatalogen. Funktioner mappas till implementeringsfaser i stället för till numrerade steg.

### [!DNL Real-Time CDP] (RT-CDP)

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Målgruppsutvärdering | Fas 1: Målgruppsutvärdering | Definiera målgruppsregler och utvärdera segmentmedlemskapet med hjälp av metoder för batchvis, direktuppspelning eller edge-utvärdering |
| Målgruppssammansättning | Fas 1: Målgruppsutvärdering | Möjlighet att sätta ihop härledda målgrupper via funktioner för berikning, rankning, delning, uteslutning och sammanslagning för komplex målgruppslogik |
| Målkonfiguration | Fas 2: Målkonfiguration | Konfigurera autentiserade anslutningar till externa mål med fältmappning och schemaläggningsparametrar |
| Audience Activation | Fas 3: Audience Activation | Publicera utvärderade målgrupper till konfigurerade mål med attributmappning och exportplanering |
| Verkställande av samtycke och styrning | Fas 4: Styrningsvalidering | Använd samtyckesinställningar och dataanvändningspolicyer före och under målgruppsaktivering i externa system |

## Förutsättningar

- [ ] RT-CDP-licens är aktiv med målgruppsaktiveringsrättigheter
- [ ] Målsandlådan är etablerad och tillgänglig för implementeringsteamet
- [ ] Användarroller innehåller behörigheter för målhantering och målgruppsaktivering
- [ Autentiseringsuppgifter för ] för varje målmål är tillgängliga (OAuth-tokens, API-nycklar, S3-åtkomstnycklar eller autentiseringsuppgifter för tjänstkonto)
- [ ] Profilschemat innehåller alla attribut som måste mappas till målfält
- [ ] Identitetsnamnutrymmen som krävs för målmatchning är konfigurerade (t.ex. hashad e-post, telefon, enhets-ID)
- [ ] pipelines för dataöverföring är i drift och profilerna fyller i profilarkivet
- [ ] Etiketter och principer för datastyrning granskas för de attribut som aktiveras (särskilt för externa mål)
- [ ] Godkännandefält fylls i med profiler om medgivande-baserad filtrering krävs

## Implementeringsalternativ

Följande implementeringsalternativ är tillgängliga för det här användningsmönstret. Granska varje alternativ och jämförelsetabellen för att avgöra vilken metod som passar bäst för dina behov.

### Alternativ A: Aktivering av direktuppspelningsmål

**Passar bäst för:** Uppdateringar av målgruppsmedlemskap i realtid på annonsplattformar eller partnersystem - anpassade målgrupper på Facebook, kundmatchning för Google Ads, matchade målgrupper med LinkedIn, Trade Desk och liknande API-baserade mål för direktuppspelning.

**Så här fungerar det:**

Aktivering av direktuppspelning ger förändringar av målgruppsmedlemskapet i nära realtid när profilerna kvalificerar sig eller diskvalificerar från segmentet. När ett profilattribut ändras eller en beteendehändelse inträffar som får en profil att ange eller avsluta en målgrupp, direktuppspelas medlemskapsuppdateringen till målet inom några minuter.

Strategin kräver en målanslutning för direktuppspelning (de flesta annonsplattformar stöder detta) och en metod för utvärdering av direktuppspelnings- eller edge-målgrupper. Publiken utvärderas kontinuerligt för att se om det finns några kvalificerande profiländringar och aktiveringsdataflödet uppdaterar allt eftersom de inträffar. Målet får stegvisa medlemsändringar i stället för fullständiga ögonblicksbilder av målgruppen.

Direktuppspelningsaktivering är standard för de flesta annonsplattformsmål i RT-CDP-katalogen. Målkopplingen hanterar API-autentisering, hastighetsbegränsning och återförsökslogik automatiskt.

**Viktiga överväganden:**

- Målgruppsutvärderingen måste använda direktuppspelning eller kantutvärdering (målgrupper som bara har grupper kan inte mata in direktuppspelningsdestinationer i realtid)
- Inte alla segmentuttryck är kvalificerade för direktuppspelningsutvärdering - komplexa aggregeringar, multientitetsfrågor och vissa tidsbaserade funktioner kräver batchbearbetning
- Gränserna för målpartners API-frekvens kan påverka genomströmningen under stora kvalificeringshändelser
- Profilattributsuppdateringar skickas tillsammans med medlemsändringar, vilket håller måldata aktuella

**Fördelar:**

- Nära målgruppsfärdighet i realtid på målet (minuter, inte timmar)
- Inkrementella uppdateringar minskar dataöverföringsvolymen jämfört med fullständig export
- Automatisk hantering av både kvalificerings- och diskvalificeringshändelser
- De flesta destinationer för annonsplattformar stöder strömning

**Begränsningar:**

- Kräver definitioner av segment som kan direktuppspelas (begränsad segmentfunktionsuppsättning)
- Ingen kontroll över filformat eller exportstruktur - dataformatet bestäms av målkopplingen
- Det går inte att exportera till filbaserade lagringsplatser (S3, Azure Blob, SFTP)
- Gränserna för målets API-frekvens kan begränsa förändringar i stora volymer

**Experience League:**

- [Aktivera målgrupper för direktuppspelningsmål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Målkatalog för direktuppspelning](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/overview)

### Alternativ B: Aktivering av batchmål (filexport)

**Passar bäst för:** Den schemalagda målgruppen exporterar till molnlagring, datalager eller system som använder filbaserad import: Amazon S3, Azure Blob Storage, Google Cloud Storage, SFTP, Data Landing Zone.

**Så här fungerar det:**

Aktivering av batchmål utvärderar målgrupper på en schemalagd gräns och exporterar resultaten som filer (CSV, JSON eller Parquet) till det konfigurerade lagringsmålet. Exporten kan innehålla foton med en fullständig målgrupp eller inkrementella förändringar (nya kvalifikationer och diskvalifikationer sedan den senaste exporten).

Implementeringen innefattar att konfigurera en filbaserad målanslutning med lagringsuppgifter, inställningar för filformat (avgränsare, komprimering, namnkonvention) och ett exportschema (varje dag, var tredje timme, var sjätte timme osv.). Varje exportkörning genererar filer som innehåller målgruppsmedlemskapet och eventuella mappade profilattribut.

Detta arbetssätt stöder ett brett urval av kunder längre fram i kedjan eftersom filbaserat datautbyte stöds av alla. Det är också det enda alternativet för användning av molnlagring och datalagerberikning.

**Viktiga överväganden:**

- Målgruppsutvärderingen kan använda vilken metod som helst (batch, direktuppspelning eller kant) - själva exporten körs enligt ett schema oavsett vilket
- Filformat, komprimering och namnkonventioner kan konfigureras per mål
- Stöder både inkrementell export (endast ändringar) och fullständig export (ögonblicksbild av hela målgruppen)
- Exportera schemalagda granularitetsintervall från var 3:e timme till dagen

**Fördelar:**

- Full kontroll över exportfilformat (CSV, JSON, Parquet), komprimering och namngivning
- Kompatibel med alla underordnade system som kan förbruka filer
- Stöder både inkrementellt och fullständigt exportläge
- Kan exportera målgrupper med valfri utvärderingsmetod (inklusive segment som bara innehåller grupper med komplex segmenteringslogik)
- Stöder ad hoc-export (on demand) utanför det vanliga schemat

**Begränsningar:**

- Latensen är i sig högre - målgruppsdata når målet enligt ett schema, inte i realtid
- Filbaserad export kräver att målsystemet bearbetar och importerar filerna
- Lagringskostnader vid destinationen för exporterade filer
- Större datavolymer per export jämfört med inkrementella uppdateringar

**Experience League:**

- [Aktivera målgrupper för att batchprofilera exportmål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Filbaserad målkatalog](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/cloud-storage)

### Alternativ C: Aktivera flera destinationer

**Passar bäst för:** Aktivera samma målgrupp för flera destinationer samtidigt - till exempel för att skicka en inaktiveringslista till alla annonsplattformar, synkronisera ett högvärdessegment till både CRM- och annonsplattformar eller samordna målgruppernas räckvidd med flera mediapartners.

**Så här fungerar det:**

Flerdestinationsaktivering är inte en separat teknisk mekanism utan en sammansättning av alternativ A och B som tillämpas på samma målgrupp över flera destinationsanslutningar. Samma målgrupp aktiveras för två eller flera mål, var och en med sin egen anslutningskonfiguration, fältmappning och schemaläggning.

Varje målanslutning fungerar oberoende av varandra - en direktuppspelningsaktivering till Facebook och en batchexport till S3 kan köras samtidigt från samma källmålgrupp. Fältmappningar konfigureras per mål, så olika attribut kan skickas till olika system baserat på vad varje mål kräver och vilka styrningsprinciper som tillåter.

Detta är ett vanligt produktionsmönster för organisationer som arbetar på flera annonsplattformar, upprätthåller CRM-synkronisering tillsammans med mediaaktivering eller behöver distribuera målgruppsdata till både operativa och analytiska system.

**Viktiga överväganden:**

- Varje mål har oberoende fältmappning, schemaläggning och styrningsutvärdering
- Styrningsprinciper tillämpas per mål - olika attribut kan tillåtas för olika måltyper
- En och samma målgrupp kan aktiveras till en blandning av direktuppspelning och batchmål samtidigt
- Om du lägger till ett nytt mål behöver du inte ändra befintliga aktiveringar

**Fördelar:**

- Samordnad målgruppsdistribution över alla externa system från en enda målgruppsdefinition
- Oberoende konfiguration per mål tillåter optimerade mappningar och scheman
- Tillämpning av styrning per mål säkerställer efterlevnad mellan olika måltyper
- Centraliserar målgruppshanteringen och stöder distribuerad aktivering

**Begränsningar:**

- Fler målanslutningar för att konfigurera, autentisera och underhålla
- Övervaka komplexiteten ökar med varje mål - aktiveringsfel måste spåras per mål
- Licensanvändningen (aktiverade profiler) kan räkna per mål beroende på berättiganden
- Underhåll av fältmappning mellan flera destinationer kräver samordning

**Experience League:**

- [Översikt över destinationer](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/home)
- [Målkatalog](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/overview)

### Jämförelse av alternativ

| Kriterier | Alternativ A: Direktuppspelning | Alternativ B: Gruppera (filexport) | Alternativ C: Flera destinationer |
| --- | --- | --- | --- |
| Bäst för | Målgruppsanpassning och undertryckande annonsplattform i realtid | Berikning av datalager, filbaserad systemintegration | Samordnad plattformsoberoende målgruppsdistribution |
| Komplex | Lågt | Medelsvåra: | Högt |
| Latens | Minuter (nästan i realtid) | Timmar (schemalagda) | Blandning av minuter och timmar per mål |
| Filformatskontroll | Ingen (mål bestämmer format) | Fullständig (CSV, JSON, Parquet, komprimering, namngivning) | Per mål |
| Målgruppsutvärdering | Strömning eller kant krävs | Alla metoder (batch, streaming, edge) | Krav per mål |
| Kräver | Strömmande målanslutning, strömningsbart segment | Filbaserad målanslutning, lagringsuppgifter | Flera målanslutningar och autentiseringsuppgifter |
| Styrning | Utvärdering av enstaka mål | Utvärdering av enstaka mål | Utvärdering per mål |

### Välj rätt alternativ

Använd följande beslutslogik för att välja rätt implementeringsmetod:

1. **Hur många mål behöver du?** Om du behöver aktivera samma målgrupp för två eller flera destinationer implementerar du alternativ C (som består av alternativ A och B per mål). Gå vidare till frågorna 2 och 3 för varje mål.

2. **Stöder målet strömning?** Om målet är en annonsplattform (Facebook, Google Ads, LinkedIn, The Trade Desk) eller partnerintegrering med ett API för direktuppspelning använder du alternativ A för det målet. Om målet är molnlagring (S3, Azure Blob, GCS, SFTP) eller ett system som använder filer använder du alternativ B.

3. **Hur snabbt måste målgruppen komma fram till målet?** Om målgruppsmedlemskapet måste spegla på målet inom några minuter (t.ex. nedtryckning i realtid under aktiva kampanjer) använder du alternativ A. Om leverans per dag eller flera timmar är tillräcklig (t.ex. uppdatering av datalagret varje vecka, batchsynkronisering av CRM) använder du alternativ B.

4. **Använder målgruppen komplex segmenteringslogik?** Om målgruppsdefinitionen innehåller sammanställningar av flera händelser, stora tidsfönster eller funktioner som inte uppfyller kraven för direktuppspelningsutvärdering, ska du använda alternativ B (gruppdestinationer) eller se till att alternativ A-destinationer också får grupputvärderade målgrupper enligt ett schema.

## Implementeringsfaser

Implementeringen följer dessa faser. Varje fas innehåller konfigurationsinformation, beslutsunderlag och länkar till Experience League-dokumentation.

### Fas 1: Målgruppsutvärdering

**Programfunktion:** RT-CDP: Audience Evaluation, RT-CDP: Audience Composition

**Det här konfigurerar du:** Definiera målgruppen som ska aktiveras för mål. Detta innefattar att specificera målgruppskriterier (vilka profiler som är kvalificerade), välja utvärderingsmetod (hur snabbt medlemskapet uppdateras) och validera målgruppspopulationen. Detta är startpunkten för all aktivering - utan en definierad och utvärderad målgrupp finns det inget att aktivera.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>
>**Beslut: Målgruppsskapandemetod**
>
>Hur ska målgruppen definieras?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Segment Builder (regelbaserad) | Standardmålgruppsdefinition med hjälp av profilattribut, beteendehändelser och villkor för segmentmedlemskap | Den mest flexibla regeldefinitionen; stöder strömning och kantutvärdering för berättigade uttryck; idealisk för en eller medelkomplex målgrupp |
>| Målgruppssammansättning | Målgruppen kräver att befintliga målgrupper kombineras, rangordnas, delas upp eller utesluts | Visuell arbetsyta för sekventiella åtgärder; resultaten utvärderas endast i grupp; max 10 kompositionsblock per arbetsyta |
>| Sammansatt målgrupp | Målgruppskriterier måste utvärderas mot data i externa datalager utan att man behöver hämta in dem i AEP | Frågar externa databaser direkt; undviker datadubbletter; kräver licens för federerad målgruppskomposition |

>[!NOTE]
>
>**Beslut: Utvärderingsmetod**
>
>Hur snabbt måste profiler gå in och lämna målgruppen?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Grupp | Schemalagda kampanjer, dagliga målgruppsuppdateringar eller komplex segmenteringslogik som inte kvalificerar för strömning | Bearbetar upp till 24 miljoner profiler per jobb; alla segmenteringsfunktioner stöds; körs enligt ett schema (dagligt standardschema eller anpassat kundschema) |
>| Direktuppspelning | Ändringar av målgruppsmedlemskap i realtid krävs för aktivering av direktuppspelningsmål eller händelseutlösta användningsfall | Nästan i realtid (sekunder till minuter), begränsad segmenteringsfunktionsuppsättning - enkla händelser, attributjämförelser och begränsade tidsfönster - inga multientitetsfrågor |
>| Edge | Personalisering av samma sida eller omedelbar målgruppskompetens krävs i toppen | Millisekundsfördröjning; den mest restriktiva regeluppsättningen - endast profilattribut och enkel kontroll av medlemskap i segment; används främst för anpassning på plats (mindre vanligt för målaktivering) |

>[!NOTE]
>
>**Beslut: Sammanslagningspolicy**
>
>Vilken sammanslagningspolicy ska målgruppsutvärderingen använda?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Tidsstämpeln har ordnats (standard) | De flesta användningsfall - senaste data bör prioriteras när profilfragment hamnar i konflikt | Mest vanligt; använder det senast uppdaterade attributvärdet |
>| Datauppsättningsprioritet | Specifika datakällor bör åsidosätta andra oavsett tidsstämpel | Kräver att en prioritetsordning för en datauppsättning definieras. Detta är användbart när ett CRM-system för en post alltid ska åsidosätta webbinsamlade data |

**Gränssnittsnavigering:** Kund > Publiker > Skapa målgrupp > Skapa regel (för Segment Builder) eller Disponera målgrupp (för Audience Composition)

**Information om nyckelkonfiguration:**

- Definiera målgruppskriterier baserat på användningsfall - profilattribut, beteendehändelser, segmentmedlemskap eller tidsbaserade villkor
- Använd undertryckningsregler för att exkludera profiler som inte ska aktiveras (t.ex. nyligen konverterade, globalt avbrutna)
- Validera målgruppens populationsstorlek innan du fortsätter med aktiveringen
- Bekräfta att utvärderingsmetoden är anpassad till den måltyp som valts i fas 2

**Var alternativen skiljer sig:**

**För alternativ A (aktivering av direktuppspelningsmål):**
Publiken måste använda direktuppspelning eller edge-utvärdering för att kunna leverera uppdateringar för medlemskap i realtid. Verifiera att segmentregeluttrycket kvalificerar sig för utvärdering av direktuppspelning - undvik tidsbaserade aggregeringsfunktioner, multientitetsfrågor och `inSegment()` referenser till segment med endast gruppbearbetning.

**För alternativ B (aktivering av gruppmål):**
Alla utvärderingsmetoder fungerar. Batchutvärdering är det vanligaste alternativet eftersom själva exporten körs enligt ett schema. Bekräfta att det finns ett batchutvärderingsschema i sandlådan, eller skapa ett.

**För alternativ C (aktivering med flera mål):**
Utvärderingsmetoden bör ge plats för den mest krävande destinationen. Om något mål kräver direktuppspelning bör målgruppen använda utvärdering av direktuppspelning. Om alla mål är batchvis räcker det med batchutvärdering.

**Experience League-dokumentation:**

- [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/home)
- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/ui/segment-builder)
- [Profile Query Language referens](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/pql/overview)
- [Direktuppspelningssegmentering](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Edge segmentering](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Översikt över Audience Composition](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/ui/audience-composition)
- [Utvärderingsmetoder](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/home#evaluation-methods)


### Fas 2: Målkonfiguration

**Programfunktion:** RT-CDP: Målkonfiguration

**Det här konfigurerar du:** Upprätta autentiserade anslutningar till de externa destinationer där målgrupper ska publiceras. Detta inkluderar att välja mål från katalogen, ange autentiseringsuppgifter och konfigurera målspecifika parametrar som filformat, lagringsplats och exportplanering. Varje mål kräver en egen anslutningskonfiguration.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>
>**Beslut: Måltyp**
>
>Var ska målgrupperna levereras?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Advertising-mål (direktuppspelning) | Målinriktning eller nedtryckning på annonsplattformar (Facebook, Google Ads, LinkedIn, The Trade Desk, osv.) | Direktuppspelningskontakter, medlemskapsuppdateringar i nära realtid, identitetsmatchning via hashad-e-post, telefon eller enhets-ID |
>| Lagringsmål för molnet (batch) | Exportera till S3, Azure Blob, GCS, SFTP eller Data Landing Zone för datalagerberikning | Filbaserad export; konfigurerbart format (CSV, JSON, Parquet); schemalagd stängning |
>| CRM-mål | Synkronisera målgrupper med Salesforce, Microsoft Dynamics eller HubSpot för säljaktivering | Vanligtvis direktuppspelning; kräver CRM-specifik fältmappning; kan behöva administratörsbehörighet för CRM |
>| Dataparameterns mål | Dela målgruppsdata med partners för mätning och målinriktning | Varierar efter partner; granska hur datautbyte påverkar styrningen externt |
>| Anpassat mål (Destination SDK) | Målsystemet är inte tillgängligt i katalogen | Kräver att du skapar ett anpassat mål med hjälp av Destination SDK; högre implementeringsinsats |

>[!NOTE]
>
>**Beslut: Autentiseringsmetod**
>
>Vilka autentiseringsuppgifter krävs för målet?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| OAuth 2.0 | Annonsplattformar och SaaS-mål (Facebook, Google, Salesforce) | Kräver initialt auktoriseringsflöde, tokens uppdateras automatiskt, vanligaste för direktuppspelningsmål |
>| Åtkomstnyckel/hemlig nyckel | molnlagring (S3, Azure Blob) | Statiska referenser; rotation ska planeras; lämpligt för filbaserade mål |
>| Tjänstkonto/API-nyckel | Partner-API:er och anpassade integreringar | Kräver etablering av autentiseringsuppgifter från målpartnern |
>| Anslutningssträng | Azure-baserade destinationer | En sträng som innehåller alla anslutningsparametrar |

>[!NOTE]
>
>**Beslut: Exporttyp (endast gruppmål)**
>
>Hur ska målgruppsdata paketeras för export?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Stegvis export | Endast nya kvalifikationer och diskvalifikationer sedan senaste exporten | Mindre filstorlekar; snabbare bearbetning på målet; målsystemet måste behålla läget |
>| Fullständig export | En fullständig målgruppsbild av varje körning | Större filer; målet får en komplett bild varje gång; enklare för system som utför en fullständig ersättning |

**Gränssnittsnavigering:** Anslutningar > Destinationer > Katalog > [Välj mål] > Konfigurera

**Information om nyckelkonfiguration:**

- Bläddra i målkatalogen och välj måldestinationen
- Ange autentiseringsuppgifter och testa anslutningen
- För gruppmål: konfigurera filformat (CSV, JSON, Parquet), komprimering, filnamnsmall och exportschema
- För direktuppspelningsmål: anslutningen upprättas vanligtvis via OAuth-auktoriseringsflödet
- Kontrollera att målanslutningsstatusen är aktiv innan du fortsätter med aktiveringen

**Var alternativen skiljer sig:**

**För alternativ A (aktivering av direktuppspelningsmål):**
Välj ett mål för direktuppspelning i katalogen (Advertising eller Sociala kategorier). Slutför OAuth-auktoriseringsflödet. Anslutningen är klar för aktivering när auktoriseringen har bekräftats.

**För alternativ B (aktivering av gruppmål):**
Välj ett filbaserat mål i katalogen (molnlagringskategorin). Konfigurera lagringssökväg, filformat, komprimering, namnkonvention och exportschema. Testa anslutningen genom att verifiera skrivåtkomst till lagringsplatsen.

**För alternativ C (aktivering med flera mål):**
Upprepa den här fasen för varje mål. Varje anslutning är oberoende - du kan ha en blandning av direktuppspelning och batchmål. Dokumentera varje anslutnings autentisering och konfiguration för driftsreferens.

**Experience League-dokumentation:**

- [Målkatalog](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/overview)
- [Översikt över destinationer](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/home)
- [Aktivera målgrupper för att batchprofilera exportmål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Aktivera målgrupper för direktuppspelningsmål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Destination SDK - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/destination-sdk/overview)
- [Konfigurationsalternativ för Destination SDK](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/destination-sdk/functionality/configuration-options)


### Fas 3: Målgruppsaktivering

**Programfunktion:** RT-CDP: Audience Activation

**Så här konfigurerar du:** Publicera den utvärderade målgruppen till det konfigurerade målet genom att skapa aktiveringsdataflödet. Detta innebär att välja vilka målgrupper som ska aktiveras, mappa profilattribut till målfält och konfigurera exportschemat. Aktiveringsdataflödet kopplar målgruppen till måldestinationen och hanterar kontinuerlig dataleverans.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>
>**Beslut: Attributmappning**
>
>Vilka profilattribut ska tas med i aktiveringen?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Endast identitetsfält | Målet behöver bara matcha profiler (t.ex. målgruppsmedlemskap i annonsplattformar) | Minimal dataöverföring, mest sekretesssäker, typisk för annonsplattformar med målinriktning och inaktivering |
>| Identitet + profilattribut | Målgruppen behöver anrikningsattribut för personalisering eller segmentering (t.ex. CRM-synkronisering, partnerdelning) | Fler data har överförts; kräver granskning av styrningen för varje attribut; kontrollera dataanvändningsetiketter mot målmarknadsföringsåtgärd |
>| Identitet + beräknade attribut | Destinationsfördelar från härledda poäng eller aggregeringar (t.ex. livstidsvärdesnivå, benägenhetspoäng för partnermål) | Kräver att beräknade attribut konfigureras; värdefull anrikning för system längre fram i kedjan |

>[!NOTE]
>
>**Beslut: Exportplanering (endast gruppmål)**
>
>Hur ofta ska målgruppsdata exporteras?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Dagligen | Standardcadence för uppdatering, de flesta användningsfall för grupp | Balanserar nyhet med bearbetningskostnad; vanligaste standardinställning |
>| Var 3-6:e timme | Användare med högre frekvens, till exempel kampanjoptimering under en dag | Oftare filgenerering, högre lagringsutrymme och högre bearbetningskapacitet vid destinationen |
>| On-demand (ad hoc) | Engångsexport eller omedelbar slutaktivering | Manuell utlösaråsidosättning av schema, användbart för testning eller brådskande kampanjbehov |

**Gränssnittsnavigering:** Anslutningar > Destinationer > Bläddra > [Välj mål] > Aktivera målgrupper

**Information om nyckelkonfiguration:**

- Markera en eller flera målgrupper som ska aktiveras för målet
- Mappa profilattribut och identitetsfält till målspecifika fält
- För direktuppspelningsmål: bekräfta mappning av identitetsnamn (t.ex. hashad e-post till Facebooks externa_id)
- För batchmål: konfigurera exportschema, välj inkrementellt eller fullständigt exportläge och ange det första exportdatumet
- Granska aktiveringssammanfattningen för att bekräfta alla mappningar och scheman innan publicering

**Var alternativen skiljer sig:**

**För alternativ A (aktivering av direktuppspelningsmål):**
Välj målgrupper och mappa ID-namnutrymmen till mål-ID-fält. Aktiveringen börjar omedelbart efter publiceringen - målgruppsmedlemskapet ändrar strömmen till destinationen i nära realtid. Inget exportschema behövs; aktiveringen är kontinuerlig.

**För alternativ B (aktivering av gruppmål):**
Välj målgrupper, mappa profilattribut och konfigurera exportschemat. Välj mellan inkrementellt och fullständigt exportläge. Om du vill kan du aktivera en ad hoc-export för omedelbar leverans utanför det vanliga schemat.

**För alternativ C (aktivering med flera mål):**
Upprepa aktiveringsarbetsflödet för varje mål. Samma målgrupp kan aktiveras för flera mål med olika attributmappningar per mål. Du kan till exempel skicka enbart hashad e-post till annonsplattformar, men inkludera demografiska attribut till CRM.

**Experience League-dokumentation:**

- [Aktivera målgrupper för direktuppspelningsmål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Aktivera målgrupper för att batchprofilera exportmål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Aktivera målgrupper on demand till batchmål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/api/ad-hoc-activation-api)
- [Övervaka dataflöden för mål](https://experienceleague.adobe.com/sv/docs/experience-platform/dataflows/ui/monitor-destinations)


### Fas 4: Validering av styrformerna

**Programfunktion:** RT-CDP: Tvingande av samtycke och styrning

**Vad du ska konfigurera:** Verifiera att styrningsprinciper och medgivandeinställningar används korrekt före och under aktivering. Denna fas säkerställer att begränsade data (PII, känsliga attribut) inte skickas till obehöriga mottagare och att profiler utan giltigt samtycke utesluts från aktivering. Styrningen verkställs automatiskt vid aktiveringen, men proaktiv validering förhindrar blockerade aktiveringar och överträdelser av regelefterlevnaden.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>
>**Beslut: Styrningens tvångsmetod**
>
>När ska myndighetsefterlevnad valideras?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Förebyggande (föraktivering) | Rekommenderas för alla implementeringar, särskilt vid aktivering till externa tredjepartssystem | Granska etiketter och principer för användning av data innan du konfigurerar fältmappningar; förhindrar aktiveringsfel och säkerställer regelefterlevnaden från början |
>| Reaktiv (vid aktivering) | När styrningspolicyer redan är väletablerade och teamet är övertygat om att de uppfyller kraven | Plattformen framtvingar principer automatiskt vid aktiveringen; brott blockerar aktiveringen eller utesluter begränsade attribut; kan orsaka oväntade fel om reglerna inte är välkända |

>[!NOTE]
>
>**Beslut: Samtyckesfiltrering**
>
>Hur ska medgivandeinställningarna påverka aktiveringen?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Verkställighet av samtycke aktiverat | Krävs vid aktivering av reklam- eller marknadsföringsdestinationer där samtycke krävs enligt lag | Profiler utan giltigt samtycke (consents.marketing.{channel}.val = &#39;y&#39;) exkluderas automatiskt från aktiveringen; data för samtycke måste hämtas |
>| Ingen medgivandefiltrering | Destinationer för intern användning eller export av analyser där samtycke inte gäller för dataöverföringen | Endast lämpligt när dataanvändningen inte utgör en marknadsföringsåtgärd som kräver samtycke, rådfråga jurister/sekretessteam |

**Gränssnittsnavigering:** Integritet > Profiler > Samtyckesprinciper (för granskning av samtycke); Datastyrning > Profiler (för granskning av dataanvändningspolicy)

**Information om nyckelkonfiguration:**

- Granska dataanvändningsetiketter som används på datauppsättningar och schemafält som aktiveras
- Verifiera att styrningsprinciper är aktiva för marknadsföringsåtgärden som är kopplad till målet (t.ex. &quot;Exportera till tredje part&quot; för annonsplattformar)
- Bekräfta att godkännandefält fylls i på profiler och att medgivande har aktiverats för relevanta kanaler
- Om principfel upptäcks kan du lösa problemet genom att ta bort begränsade fält från målmappningen eller välja ett annat mål

**Experience League-dokumentation:**

- [Översikt över dataförvaltning](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/home)
- [Politiska åtgärder](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/enforcement/overview)
- [Översikt över etiketter för dataanvändning](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/labels/overview)
- [Samtycke och inställningar](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)
- [Bekräftelsepolicytillämpning](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/policies/user-guide)


### Fas 5: Övervakning och validering

**Programfunktion:** Övervakning och observerbarhet

**Vad du ska konfigurera:** Konfigurera kontinuerlig övervakning för aktiveringsdataflöden, konfigurera varningar för fel, validera målgruppspopulationen på destinationer och spåra licensanvändning. Övervakning är viktigt för produktionsaktiveringar där leveransfel direkt påverkar kampanjens prestanda och medieleveranser.

**Information om nyckelkonfiguration:**

- Granska körningsstatus för dataflöde för varje aktivt mål för att bekräfta att målgrupperna har levererats
- Konfigurera aviseringar om fel vid målaktivering, dataflödesfördröjningar och målgruppens populationsavvikelser
- Spåra profiler som exporterats jämfört med profiler som misslyckats per körning av dataflöde
- Övervaka målgruppsmatchningar vid destinationen (där målrapportering är tillgänglig)
- Granska licensanvändning för att spåra aktiverad profilvolym mot berättiganden

**Gränssnittsnavigering:** Anslutningar > Destinationer > Bläddra > [Välj mål] > Dataflöd (för aktiveringsövervakning); Varningar > Varningsregler > Prenumerera (för aviseringskonfiguration); Administration > Licensieringsanvändning (för licensspårning)

**Experience League-dokumentation:**

- [Övervaka dataflöden för mål](https://experienceleague.adobe.com/sv/docs/experience-platform/dataflows/ui/monitor-destinations)
- [Översikt över aviseringar](https://experienceleague.adobe.com/sv/docs/experience-platform/observability/alerts/overview)
- [Översikt över Insikter i observationer](https://experienceleague.adobe.com/sv/docs/experience-platform/observability/home)
- [Kontrollpanel för licensanvändning](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/license-usage-dashboard)

## Implementeringsöverväganden

Granska följande överväganden före och under implementeringen.

### Gardrutor och begränsningar

- **Segmentdefinitionsgräns:** Maximalt antal 4 000 segmentdefinitioner per sandlåda - [Skyddsritningar för segment](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/guardrails)
- **Dataflöden per mål:** Maximalt 100 dataflöden per målanslutning - [Målskyddsutkast](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/guardrails)
- **Storlek på batchexportfil:** Filbaserade mål har maximala storleksgränser för exportfiler; stora målgrupper delas automatiskt över flera filer
- **Direktuppspelning av målgenomströmning:** Genomströmningsgränser per sekund anges av varje målpartner, ändringar av stora volymer kan begränsas
- **Batchutvärderingskapacitet:** Upp till 24 miljoner profiler per segmentutvärderingsjobb som standard
- **Målgruppskomposition:** Maximalt 10 kompositionsblock per arbetsyta; sammansatta målgrupper utvärderas endast gruppvis
- **Identitetsdiagram:** Max 50 identiteter per diagram - [Identitetstjänstens skyddsprofiler](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/guardrails)
- **Beräknade attribut:** Högst 25 beräknade attribut per sandlåda - [Beräknade attributskyddsräcken](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/computed-attributes/overview#guardrails)
- **Översikt över aktiveringsskyddsutkast:** [Aktiveringsskyddsutkast](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/guardrails)

### Vanliga fallgropar

- **Direktuppspelningssegment med ogiltig regellogik:** Definierar en målgrupp med komplexa aggregeringsfunktioner eller multientitetsfrågor och förväntar sig utvärdering av direktuppspelning. Dessa segment går i tysthet tillbaka till grupputvärdering, vilket orsakar oväntad fördröjning. Förebyggande: kontrollera kraven för direktuppspelning innan du definierar målgruppen.

- **Nollprofiler som exporterats på grund av medgivandefiltrering:** Alla profiler i målgruppen saknar giltiga medgivandevärden, vilket gör att hela målgruppen filtreras bort vid aktiveringen. Förebygga: kontrollera att inmatning av data om samtycke är operativt och att fält för medgivande fylls i innan de aktiveras.

- **Styrningsprincip blockerar oväntat aktivering:** Dataanvändningsetiketter i schemafält utlöser principöverträdelser som förhindrar aktivering. Förebyggande: utvärdera efterlevnadskontroll proaktivt (fas 4) innan fältmappningar konfigureras. Granska vilka etiketter som ärvs från schemat.

- **Förfallotid för målautentiseringsuppgifter:** OAuth-tokens eller API-nycklar förfaller, vilket orsakar aktiveringsfel utan någon omedelbar varning. Förebyggande: konfigurera aviseringar för misslyckade målaktiveringar och upprätta ett rotationsschema för autentiseringsuppgifter.

- **Identitetsnamnutrymmen som inte matchar:** Identitetsnamnområdet som konfigurerats i aktiveringsmappningen matchar inte vad målet förväntar sig (t.ex. att skicka e-post med oformaterad text när målet kräver SHA-256-hashade e-post). Förebyggande: Granska måldokumentationen för att se om det finns nödvändiga identitetsformat innan du konfigurerar mappningen.

- **Fältmappningsfel som orsakar exportfel:** Mappa ett profilattribut till ett målfält med en inkompatibel datatyp eller ett inkompatibelt format. Förebyggande: testa aktiveringen med en liten publik först och se hur dataflödet kan mappa fel innan det skalas till produktionspubliken.

- **Målgruppspopulation mellan RT-CDP och mål:** Målgruppsantalet i RT-CDP matchar inte antalet vid målet på grund av skillnader i identitetsmatchning, logik för måldeduplicering eller timing. Detta är förväntat beteende - förebyggande: dokumentets förväntade referensvärden för matchningsfrekvens per mål och övervaka för signifikanta avvikelser.

### God praxis

- **Börja med en testmålgrupp:** Aktivera en liten, välkänd testmålgrupp för varje nytt mål innan du aktiverar produktionspubliken. Validera fältmappningar, identitetsmatchning och leveransstatistik med testmålgruppen.

- **Lagerstyrning tidigt:** Tillämpa dataanvändningsetiketter och konfigurera styrningsprinciper innan målaktiveringar konfigureras. Detta förhindrar blockerade aktiveringar och säkerställer överensstämmelse från början.

- **Använd inkrementell export för gruppmål:** Inkrementell export minskar filstorleken, snabbar upp bearbetningen på målet och minimerar lagringskostnaderna. Använd endast fullständig export när målsystemet kräver ett fullständigt målgruppsersättning.

- **Standardisera namnkonventioner:** Upprätta konsekventa namn för målgrupper, målanslutningar och dataflöden i hela organisationen. Inkludera användningsfall, mål och utvärderingsmetod i namn (t.ex. &quot;Suppression_ExistingCustomers_Facebook_Streaming&quot;).

- **Övervaka matchningsfrekvenser:** Spåra förhållandet mellan profiler som exporteras från RT-CDP och profiler som matchas vid varje mål. Betydande fall av matchningsfrekvens kan tyda på problem med identitetsupplösning, problem med autentiseringsuppgifter eller ändringar i mål-API.

- **Koordinera undertryckning mellan destinationer:** När du använder undertryckande målgrupper (t.ex. utelämnar befintliga kunder från värvningskampanjer) ska du aktivera undertryckande målgrupper för alla relevanta annonsplattformar samtidigt för att upprätthålla enhetligheten.

- **Granska och rensa inaktiva aktiveringar:** Granska måldataflöden regelbundet och inaktivera målgrupper som inte längre behövs. Inaktiva aktiveringar förbrukar licenskapacitet och lägger till övervakningskostnader.

### Avvecklingsbeslut

>[!NOTE]
>
>**Brytfrekvens: Målgruppens aktualitet kontra segmenteringsflexibilitet**
>
>Direktuppspelningsutvärdering ger nästan hela tiden målgruppsuppdateringar, men begränsar de segmentregelfunktioner du kan använda. Batchutvärderingen har stöd för hela segmentregelfunktionsuppsättningen men introducerar fördröjning (timmar i stället för minuter).
>
>- **Direktuppspelning prioriterar:** Fall av användning i realtid där målgruppsmedlemskapet måste spegla på målet inom några minuter (aktiv inaktivering av kampanjer, återmarknadsföring i realtid)
>- **Batch prioriterar:** Komplex målgruppslogik som kräver aggregeringsfunktioner, multientitetsfrågor eller stora tidsfönsterförhållanden (livstidsvärden, flerberöringsbeteendesegment)
>- **Rekommendation:** Använd direktuppspelningsutvärdering för målgrupper som har aktiverats för direktuppspelningsmål där aktualitet i realtid driver affärsvärdet. Använd batchutvärdering för komplexa målgrupper som aktiveras för filbaserade mål eller när daglig uppdatering är tillräckligt. För målgrupper som behöver båda bör du överväga att skapa två versioner: ett förenklat direktuppspelningssegment för aktivering i realtid och ett omfattande batchsegment för periodisk berikning.

>[!NOTE]
>
>**Avvikelse: Minimal dataexport jämfört med attributmappning med rich**
>
>Genom att endast exportera identitetsfält (hashad e-post, enhets-ID) minimeras dataexponeringen och förenklar styrningen. Om du exporterar ytterligare profilattribut (demografi, värdenivå, engagemangsmoment) blir målet bättre, men det ökar komplexiteten i styrningen och gör data mer tillförlitliga.
>
>- **Minimal export prioriterar:** Sekretess först-metod, lägre styrningsrisk, enklare fältmappning, tillräckligt för de flesta användningsfall för annonsplattform och undertryckning
>- **Omfattande exportförmåner:** Skräddarsydd anpassning i efterföljande led på målet; CRM-anrikning; delning av partnerdata som kräver detaljnivå på attributnivå
>- **Rekommendation:** Standardinställningen är minimal identitetsexport för annonsmål. Lägg bara till profilattribut när målanvändningsexemplet uttryckligen kräver det och styrningsgranskningen bekräftar regelefterlevnaden. Använd beräknade attribut för att tillhandahålla aggregerade, mindre känsliga anrikningsvärden i stället för obearbetad PII.

>[!NOTE]
>
>**Avvikelse: Enstaka målgrupp per mål kontra konsoliderade dataflöden för flera målgrupper**
>
>Genom att aktivera varje målgrupp som ett separat dataflöde får du isolering och detaljerad övervakning. Genom att aktivera flera målgrupper via ett enda dataflöde till ett mål blir hanteringen enklare, men isoleringen minskar.
>
>- **Separata dataflöden ger följande fördelar:** Oberoende övervakning, enklare felsökning, möjlighet att pausa enskilda målgruppsaktiviteter utan att påverka andra
>- **Konsoliderade dataflöden ger en förmån:** Färre anslutningar att underhålla, förenklad autentiseringshantering, minskad operativ overhead
>- **Rekommendation:** Använd konsoliderade dataflöden när flera relaterade målgrupper aktiveras till samma mål (t.ex. alla undertryckningssegment till Facebook). Använd separata dataflöden när målgrupper har olika SLA-avtal, olika attributmappningar eller när det är viktigt med felisolering.

## Relaterad dokumentation

**Destinationer**

- [Översikt över destinationer](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/home)
- [Målkatalog](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/overview)
- [Aktivera målgrupper för direktuppspelningsmål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Aktivera målgrupper för att batchprofilera exportmål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Aktivera målgrupper on demand till batchmål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/api/ad-hoc-activation-api)
- [Skyddsräcken för destinationer](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/guardrails)
- [Destination SDK - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/destination-sdk/overview)

**Målgrupper och segmentering**

- [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/home)
- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/ui/segment-builder)
- [Profile Query Language referens](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/pql/overview)
- [Direktuppspelningssegmentering](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Edge segmentering](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Översikt över Audience Composition](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/ui/audience-composition)
- [Skyddsritningar för segmentering](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/guardrails)

**Identitet och profil**

- [Översikt över identitetstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/home)
- [Översikt över namnutrymmen för identiteter](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/features/namespaces)
- [Länkningsregler för identitetsdiagram](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/features/identity-linking-logic)
- [Profilöversikt](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/home)
- [Översikt över kopplingsprofiler](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/merge-policies/overview)

**Datamodellering och scheman**

- [XDM - systemöversikt](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/home)
- [Grundläggande om schemakomposition](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/schema/composition)

**Datastyrning**

- [Översikt över dataförvaltning](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/home)
- [Översikt över etiketter för dataanvändning](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/labels/overview)
- [Datastyrningspolicyer](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/policies/overview)
- [Politiska åtgärder](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/enforcement/overview)
- [Samtycke och inställningar](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)

**Övervakning och observerbarhet**

- [Övervaka dataflöden för mål](https://experienceleague.adobe.com/sv/docs/experience-platform/dataflows/ui/monitor-destinations)
- [Översikt över aviseringar](https://experienceleague.adobe.com/sv/docs/experience-platform/observability/alerts/overview)
- [Översikt över Insikter i observationer](https://experienceleague.adobe.com/sv/docs/experience-platform/observability/home)
- [Kontrollpanel för licensanvändning](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/license-usage-dashboard)

**Beräknade attribut**

- [Översikt över beräknade attribut](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/computed-attributes/overview)
- [Användargränssnittshandbok för beräknade attribut](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/computed-attributes/ui)

**Datainsamling och källor**

- [Översikt över källor](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/home)
- [SDK - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/web-sdk/home)
- [Konfigurera datastreams](https://experienceleague.adobe.com/sv/docs/experience-platform/datastreams/configure)

**Administration**

- [Översikt över sandlådor](https://experienceleague.adobe.com/sv/docs/experience-platform/sandbox/home)
- [Översikt över åtkomstkontroll](https://experienceleague.adobe.com/sv/docs/experience-platform/access-control/home)
- [Attributbaserad åtkomstkontroll](https://experienceleague.adobe.com/sv/docs/experience-platform/access-control/abac/overview)

**Guardrails**

- [Garantier för kundprofiler i realtid](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/guardrails)
- [Garantier för identitetstjänst](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/guardrails)
- [Aktiveringsskydd](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/guardrails)
- [Förvaringsskydd](https://experienceleague.adobe.com/sv/docs/experience-platform/ingestion/guardrails)
