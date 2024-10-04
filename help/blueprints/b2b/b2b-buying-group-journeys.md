---
title: Köpa en gruppbaserad plan för marknadsföring och resehantering
description: Lär dig att hitta, designa och bygga en resa som berättigar till köp i Adobe Journey Optimizer B2B edition.
solution: Journey Optimizer B2B Edition
source-git-commit: 5035c869aa5181fff66cbc20b03922f82832f126
workflow-type: tm+mt
source-wordcount: '2129'
ht-degree: 0%

---

# Köpa en koncernbaserad plan för marknadsföring och resehantering

Marknadsföringsteamen står inför många utmaningar när det gäller att ge säljarna kvalificerade leads. En av dessa utmaningar är att arbeta med rätt personer i organisationen, och de är vanligtvis uppenbara i arbete och precision. Med _lead-poäng_ är gruppen för smal och team kanske saknar rätt personer. Med _kontopoäng_ krävs större insatser för att identifiera rätt person med en så bred vy av ett konto.

Utmaningen är den plats där begreppet **_inköpsgrupp_** introduceras. En inköpsgrupp gör det möjligt för marknadsförare att hitta rätt grupp personer på kontot och att arbeta med dessa personer genom att kvalificera leads och identifiera deras roll i gruppen.

## Hur inköpsgrupper används för att kvalificera leads och konton

Att skapa och sträva efter att slutföra en inköpsgrupp ökar marknadsföringsaktivitetens effektivitet när det gäller att kvalificera leads till försäljningsmöjligheter. Köpgrupper kopplas till matchande leads till rollmallar som är länkade till lösningsmetoden.

Ett exempel på en inköpsgrupp kan vara _Acme Corp Seeds Buying Group_, som har ett lösningsintresse för _AI-drivna fraser_.

Köpgrupper representerar en grupp personer på företaget som är intresserade av en lösning i en lösningsmetod. Och en inköpsgrupp kunde identifieras för mer än ett lösningsintresse och de enskilda personerna finns i mer än en inköpsgrupp.

Tack vare de förbättrade B2B-funktionerna i Journey Optimizer B2B edition kan du nu ta itu med följande problem:

* Det saknas _marknadsföringskampanjer som sätter kunden först_.
* Inkonsekvent konvertering av marknadsföringskvalificerat lead (MQL) till säljkvalificerat lead (SQL), vilket kräver att initiativen anpassas till försäljningen för att vårda MQL
* Det saknas en säljbar mekanism för att identifiera och ha _fullständiga_-konton som mål.
* Koncentrationsrisk i intäkter och pipeline.

Följande nyckeltal är väl anpassade efter hur väl användningsexemplen fungerar:

* **Medvetenhet**: Är målkunderna intresserade av dina annonser och leder det dem till webbplatsen i högre frekvens än tidigare?
* **Engagemang**: Kommer målkunder till din webbplats och engagerar med innehåll?
* **Tid**: Hur lång tid tar det för säljteamet att hitta och lägga till kontakter från olika verktyg i affärsmöjligheten?
* **Kostnad**: Hur mycket kostar varje lead på varje plattform?

## Kontobaserad marknadsföring

Ett vanligt användningsexempel, och fokus i den här planen, är ett kontobaserat marknadsföringsinitiativ som utforskar den punkt där den inköpskoncern som skapats är ifylld med ett lead när de är kopplade till en roll och en lösning.

När du leder en individ under resan samlar du in mer information om leadet (Buying Group Workflow) via formulär, CRM Sync och LinkedIn-aktivering.

När ett lead tydligt visar lösningsintresset indikerar det en affärshändelse som definieras av ett företagslinje. I nuläget är företaget övertygat om att denna lead verkligen är intresserad av en produkt, och i Journey Optimizer B2B edition är ledaren kopplad till en inköpsgrupp för den lösningen i en rollmall (som påverkare, beslutsfattare, mästare och sponsorer).

Som framgår av bilden nedan kan du samla in uppgifter i formulär eller genom LinkedIn-aktivering och kvalificera en lösningsmetod när en chattrobot interagerar.

![Köper gruppresa](./assets/buying-group-journey-diagram.svg){zoomable="yes"}

När procentandelen för slutförda inköp är tillräckligt hög delar du gruppen med säljarna via SQL eller en SOL för att konvertera leads i kontot till en slutförd försäljning.

## Kontofokuserad lösning

Fokus på hantering av B2B-leads är konton och deras leads. Det tekniska skiktet är utformat för att stödja de data som representerar dessa egenskaper, vilket är ett krav för framgångsrik kontosegmentering och resehantering.

### Krav

Den kontofokuserade lösningen kräver följande program och tjänster:

* Adobe Journey Optimizer B2B edition
* Adobe Real-time Customer Data Platform (RTCDP) B2B edition
* Adobe Marketo Engage

>[!NOTE]
>
>Licenser för Journey Optimizer B2B edition ska omfatta följande:
><ul><li>Journey Optimizer B2B edition-instans som är ansluten till Experience Platform B2B</li><li>Marketo Engage-instans som synkroniseras till RTCDP</li></ul>
&gt;<br/>
&gt;För befintliga Marketo Engage-kunder rekommenderas en anslutning till den befintliga instansen.
&gt;<br/><br/>
&gt;Det finns ytterligare tillägg för lösningen för att förbättra profilrikedomen:
&gt;<ul><li>Ytterligare källor till RTCDP för att utöka profilen</li><li>RTCDP-mål till Marketo Engage</li></ul>

Implementeringen av den här lösningen kräver också en tydlig förståelse för konceptet _Konto_ och _Köpgrupp_ och hur de förstärker och snabbar upp kvalificeringen av säljleads. Med den här förståelsen måste du också identifiera önskat poängvärde för slutförande av inköpsgrupper.

### Arkitektur

![Lösningsarkitektur för inköp av gruppbaserad marknadsföring och resehantering](./assets/ajo-b2b-architecture.png){zoomable="yes"}

### Datamodell

Vid varje implementering av datadriven automatisering av marknadsföringen är utformningen av scheman avgörande för att implementeringen ska lyckas. Innan du utformar ditt schema bör du granska [B2B-namnutrymmen och scheman](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo-namespaces) och se till att du förstår vilket verktyg för automatisk generering som är tillgängligt för att skapa ett nytt schema i ett nytt implementeringsscenario.

Scheman har berikats specifikt med B2B-dataelement för att ge stöd åt den omfattande relationen i profiler och inkludera kontoperspektivet via `sourceKey` för att koppla händelser och profiler till kontoschemat. Scheman är en representation av organisationens krav och insamlade och profilerade data. För att tillgodose dessa behov är B2B-scheman flexibla och är en förlängning av de B2B-element som krävs.

När du utformar dataschemat för din organisation är det en god vana att representera och etikettera huvudentiteterna i din ERD med högnivåentiteter i det första diagrammet i [RTCDP B2B-schemadokumentationen](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/relationship-b2b). Den här processen är mycket användbar för att förstå de dataelement som krävs och som du måste definiera i varje schema.

I det här skedet kan Experience Events ännu inte påverka resorna. Förutom Experience Event-scheman rekommenderar vi att du lägger till egenskaper i kontot som representerar viktiga beslut baserade på användaraktiviteter. De här egenskaperna används för delade banelement i resedesignern.

>[!NOTE]
>
>För närvarande är den enda relation som stöds av Journey Optimizer B2B edition direktrelationer via attributet `personComponents[0].sourceAccountKey.sourceKey` i entiteten `Person`. Framtida expansion planeras för att passa relationsobjektet konto-person i B2b-schemat.

### Marketo Engage-källanslutning

Om du vill utöka kontodataelementen kan du använda Marketo Engage och dess B2B-data för att utöka RTCDP- och Journey Optimizer B2B edition-kontovyn. Genom att ställa in Marketo Engage Source Connector och mappa Marketo Engage data till RTCDP-schemaattribut kan data flöda från Marketo Engage till RTCDP, och om så anges, till profilen.

Mer information om anslutningskonfigurationen och den obligatoriska fältmappningen finns i [Marketo Engage-anslutningsdokumentationen](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) till det schema som definierades i föregående steg.

### Skyddsräcken

Journey Optimizer B2B edition-skyddsutkast finns på [produktbeskrivningssidan](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer-b2b.html).

Implementeringsrelaterade skyddsräcken

* Alla B2B-målgruppsprofiler beskrivs i [B2B Audience and Profile Activation Plan](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails) som direkt införlivas i Journey Optimizer B2B edition.
* Om aktivering krävs via Marketo Engage-kanaler på kontoresan eller om CRM Sync används för att berika kontot, är de [Marketo Engage-relaterade skyddsprofilerna](https://helpx.adobe.com/legal/product-descriptions/adobe-marketo-engage---product-description.html#performance-guardrails) relevanta.

Läs dokumentationen för [Real-Time CDP GuarDRAils](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/guardrails/overview) om du vill ha mer information om RTCDP GuarDRAils.

### Etablering

* Alla instanser måste finnas i samma IMS-organisation.
* Endast en Journey Optimizer B2B edition-instans kan länkas till en Experience Platform-sandlåda.
* Vi rekommenderar att du implementerar [Marketo Source Connector till Real-time Customer Data Platform](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo).

## Implementering

Följande steg ger vägledning för att aktivera funktionen Buying Group i din Journey Optimizer B2B edition-instans och inkluderar ytterligare aktivering för att stödja utökning av din kontobas med fokus på att köpa rollmallar som saknas i grupper.

### Krav-steg

1. Definiera XDM-schemat som ska representera din företagsvy över konton och leads.

   Som ett första steg definierar och skapar ni ett upplevelseschema som är utformat för att passa B2B-användningsbehoven och som täcker datakällorna, både batch- och realtidsdata. Denna design bör representera hur företaget tänker på konto- och personenheter och vilka användningsområden du vill stödja. För att schemat ska kunna vara ett B2B-schema bör schemat följa de strukturer som finns i [dokumentationen för RTCDP B2B-schemat](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/relationship-b2b).

   En användbar metod är att ta enhetsnamnen från diagrammet och identifiera dessa enheter i ditt schema genom att märka dem på samma sätt. Observera att vissa scheman kräver specifika nycklar, som `sourceKey`, för att fungera i RTCDP B2B. På kort sikt stöds inte relationen _Många-till-Många_ mellan konto och person via Kontopersonsrelation i Journey Optimizer B2B. Använd acceleratorskripten som den bästa startpunkten:

   * Använd det [RTCDP B2B-schemaskapandeskriptet](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility) för att generera det inledande schemat
   * Lägg till ärendespecifika fält i scheman som genereras för att slutföra schemat så att det passar organisationens behov.

   I det här skedet har du anslutningen mellan Marketo Engage och RTCDP och schemastrukturen för att acceptera konto- och persondata för att fylla i dataset för kontosegmenten. Nästa steg är att ansluta RTCDP till Marketo Engage och Journey Optimizer B2B edition.

1. Konfigurera Marketo Engage-anslutningen, inklusive mappningen av Marketo Engage till XDM-strukturen.

   När XDM-strukturen och -fälten är på plats fortsätter du att ansluta Marketo Engage till RTCDP med hjälp av kopplingen, som matar datauppsättningarna med data från Marketo Engage och Journey Optimizer B2B. Börja med att ordna mappningen för fälten från Marketo Engage till RTCDP-klasser. Använd informationen i [anslutningsdokumentationen](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo#field-mapping-from-marketo-engage-to-xdm) för att identifiera fälten som du vill ta med från implementeringen av Marketo Engage.

### Konfiguration av inköpsgrupp

1. Skapa kontomålgrupper i Journey Optimizer B2B edition eller RTCDP.

   Aktivera alternativet Schemalägga alla målgrupper på sidan Customer → Audiences → Browse för att aktivera Account Audiences. (Om detta inte fungerar måste du skapa ett kundprofilsegment för att kunna skapa kontomåldrar)

   Om du vill skapa ett segment följer du stegen i [målgruppsdokumentationen](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-audiences/account-audience-overview). Användningen av Segment Builder tillsammans med de datafält som du har identifierat som nyckel för din kontopublik är nyckelaktiviteten när du definierar målgruppen.

   I det här skedet vet du att kontot leder till fokus via RTCDP och att det används för inköpsgruppens byggstenar.

1. Definiera rollmallen.

   Identifiera de roller som representerar den roll som enskilda personer spelar i gruppen som du vill ta emot i varje inköpsgrupp. Du kan till exempel använda _beslutsfattare_, _påverkare_ och _mästare_. Definiera också vikt och villkor för den här rollen i inköpsgruppen.

   [rollmallens dokumentation](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-role-templates) beskriver den här processen och hur du definierar särskilda villkor.

1. Definiera lösningsintresset.

   Intresset hos en lösning är ett sätt att visa vilka inköpsgrupper som fokuserar på era marknadsföringsaktiviteter och er strategi.

   Om du vill definiera ett intresse för en lösning följer du stegen i [dokumentationen om lösningsintresse](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/solution-interests). Kom ihåg att du använder den för att matcha inköpsgruppen med ett säljinitiativ i organisationen.

1. Konfigurera inköpsgruppen.

   Med byggstenarna för inköpsgruppen redo konfigurerar du inköpsgruppen för lösningsintresse och kontomålgrupp med ett mål för att slutföra rollmallen med rätt kontomedlemmar. Med den här konfigurationen tilldelar du ett lösningsintresse till den rollmall som du har identifierat och du ger varje roll en viktig roll i säljframgången för den specifika produkten.

   Följ stegen i dokumentationen för [inköpsgrupper](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-create) när du vill skapa inköpsgruppen.

   I det här skedet är du redo att [skapa en resa](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-overview#get-started-with-a-journey) och börja arbeta med den kontobaserade målgruppen för att bygga upp inköpsgruppen och kvalificera dem för lösningsintresset.

### Målgruppsaktivering

Öka kundgruppens fullständighet genom målgruppsaktivering.

1. Definiera en målgrupp för ett LinkedIn Ad Matched Account.

   Förutom e-post- och formulärfyllnadsaktiviteter erbjuder Journey Optimizer B2B edition en LinkedIn Ad-funktion för att öka bredden på ditt konto och stödja arbetet med att slutföra en inköpsgrupp genom att utöka antalet leads för kontot och öka marknadsföringsaktiviteternas räckvidd.

   Om du vill använda LinkedIn Paid-medier för att kommunicera med konton där inköpsgrupperna inte är tillräckligt kompletta eller engagerade, expanderar eller interagerar med den kontobaserade målgruppen, använder du funktionen [LinkedIn Account Matched Audiences](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-audiences/linkedin-account-matched-audiences) för att generera LinkedIn Ad-målgrupper via Kontomatchade målgrupper.

1. Aktivera målgruppen för inköpsgrupper.

>[!TIP]
>
>Några tips om framgångsrika kampanjer:
>
>* En kampanj bör ha rollfilter för att passa inköpsgrupper med saknade roller för att öka avkastningen.
>* Om du vill hämta leads leder det till att formulär fylls i (LinkedIn eller Marketo Engage) och att formulärfelen återannonseras.
