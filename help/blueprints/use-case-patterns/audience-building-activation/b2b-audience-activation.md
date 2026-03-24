---
title: B2B Audience Activation
description: Lär dig hur du aktiverar kontobaserade B2B-målgrupper över webb-, e-post- och reklamkanaler.
solution: Real-Time Customer Data Platform
exl-id: 2b979159-37aa-41d4-a6b4-1105538f6546
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '7611'
ht-degree: 0%

---

# B2B-målgruppsaktivering

Den här guiden innehåller en omfattande implementeringsreferens för aktivering av kontobaserade B2B-målgrupper med [!DNL Adobe Real-Time Customer Data Platform] ([!DNL RT-CDP]) B2B edition. Det är utformat för lösningsarkitekter, marknadsföringsteknologer och implementeringstekniker som behöver skapa, utvärdera och aktivera målgrupper på kontonivå via webben, e-post, annonsering och CRM-kanaler.

Den täcker hela livscykeln från en enhetlig kontoprofil till målgruppsbedömning och aktivering till B2B-specifika mål som [!DNL Marketo Engage], [!DNL LinkedIn] och CRM-system. Alla genomförbara implementeringsstrategier presenteras med kompromisser och beslutsvägledning som hjälper dig att välja rätt väg för din organisation.

## Använd ärendeöversikt

B2B-marknadsföringsteam måste inrikta sig på och aktivera målgrupper på kontonivå snarare än på individnivå. Till skillnad från B2C-målgruppsaktivering, där målgruppsenheten är en enda konsumentprofil, kräver B2B-målgruppsaktivering förståelse för relationen mellan människor och de konton de tillhör, utvärdering av målgruppsmedlemskap baserat på kontoattribut kombinerat med engagemangssignaler på personnivå och leverans av dessa målgrupper till destinationer som stöder kontobaserad målgruppsanpassning.

[!DNL RT-CDP] B2B edition utökar standarden [!DNL Real-Time Customer Data Platform] med specialiserade XDM-klasser för konton, affärsmöjligheter och kampanjer, samt B2B-identitetsmatchning som mappar relationer mellan människor och konton. Detta gör att marknadsförarna kan skapa kontoramar som kombinerar firmmografiska data (bransch, intäkter, antal anställda), teknikdata (teknikstack, produktanvändning) och beteendedata (webbbesök, e-postinteraktion, eventnärvaro) från de personer som är kopplade till dessa konton.

De aktiverade målgrupperna på kontot har olika strömanvändningsfall för efterfrågegenerationen funnel: kampanjer för att öka medvetenheten hos funnel på [!DNL LinkedIn] och displayannonsering, program för modernt funnel i [!DNL Marketo Engage] samt säljaktivering för nedre funnel via CRM-integrering. Genom att utesluta konton kan målgrupper förhindra slöseriet med utgifter genom att utesluta befintliga kunder, stängda konton eller konton som redan är aktiva säljcykler.

>[!NOTE]
>Om du aktiverar målgrupper på personnivå (B2C) i stället för på kontonivå läser du [Målgruppsaktivering](audience-activation-to-destinations.md). Det mönstret använder standarddatamodellen RT-CDP och kräver inte B2B edition.

## Viktiga verksamhetsmål

Följande affärsmål stöds av det här användningsmönstret.

### Öka lead-generering

Generera mer kvalificerade leads för säljflödet via formulär, event, innehåll och flerkanalsengagemang.

**KPI:er:** Prospekt, Kostnad per lead, Leadkonvertering

[Läs mer om hur ni kan öka antalet leads](/help/blueprints/business-objectives/acquisition-growth/increase-lead-generation.md)

### Förbättra kvalificering och konvertering av leads

Öka ledningskvaliteten och snabba upp utvecklingen av pipeline genom poängsättning, vårdande och personaliserad uppföljning.

**KPI:er:** Leadkonvertering, konvertering av potentiell kund/lead, effektivitet

[Läs mer om hur du förbättrar kvalificering och konvertering av leads](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)

### Skaffa nya kunder

Utöka kundbasen med riktade kampanjer, lookalike-målgrupper och optimering av betalda medier.

**KPI:er:** Nya kunder, Kundanskaffningskostnad, Prospekt/Leadkonvertering

[Läs mer om hur man skaffar nya kunder](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

### Optimera marknadsföringsbudgeten och avkastningen

Förbättra avkastningen på marknadsföringsinvesteringar genom bättre målgruppsanpassning, attribuering, dämpande av målgrupper och budgettilldelning.

**KPI:er:** Kostnadsbesparingar, Kundanskaffningskostnad, Inkrementella intäkter

[Läs mer om optimering av marknadsföringsutgifter och avkastning](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)

## Exempel på taktiska användningsfall

Följande scenarier visar hur mönstret kan användas i praktiken.

- **Kontobaserad annonsering på[!DNL LinkedIn]** - Målkonton som matchar din idealiska kundprofil (ICP) med sponsrat innehåll och InMail-kampanjer på [!DNL LinkedIn], med kontolistor aktiverade från [!DNL RT-CDP] B2B edition
- **[!DNL Marketo Engage]vårdprogram med målinriktning** - Aktivera kontomålgrupper för att [!DNL Marketo Engage] ska registrera associerade leads och kontakter i riktade vårdströmmar baserat på kvalifikationskriterier på kontonivå
- **Synkronisering av CRM-kontolista** - Överför kvalificerade kontolistor till [!DNL Salesforce] eller [!DNL Microsoft Dynamics] för säljteamets synlighet, områdestilldelning och arbetsflöden för utgående prospektering
- **Inaktivering av konto för betalda media** - Utelämna befintliga kunder, avslutade konton eller konton i aktiva säljcykler från betalda anskaffningskampanjer för att minska bortslösade utgifter
- **Återgivningsbaserad kontoanpassning** - Kombinera tredjepartsavsiktssignaler med förstapartsdata på kontonivå för att identifiera och aktivera målgrupper för marknadskonton
- **Produktkorsförsäljning till befintliga konton** - Skapa målgrupper med konton med en produktlinje men inte en annan, aktivera sedan för e-post- och annonskanaler för korsförsäljningskampanjer
- **Aktivering av händelser och webbinarier** - Aktivera målgrupper för konton för reklam och e-postkanaler för att driva händelseregistrering från målkonton
- **Konkurrenskraftiga förskjutningskampanjer** - Rikta konton med konkurrentprodukter med anpassade meddelanden aktiverade via reklam- och e-postkanaler
- **Höjd nivå för kontoengagemang** - Segmentera konton i engagemangsnivåer (hög, medel, låg) baserat på aggregerad aktivitet på personnivå och aktivera differentierade kampanjer för varje nivå
- **Målgrupper för sammarknadsföring** - Dela målgruppssegment med kanalpartners eller program för sammarknadsföring via molnlagring

## Nyckeltal för prestanda

Följande nyckeltal hjälper till att mäta hur bra det här användningsmönstret är.

| KPI | Beskrivning | Mätningsmetod |
| --- | --- | --- |
| Kontointervall | Antal målkonton som uppnåtts över aktiveringskanalerna | Spåra unika konton som aktiveras per mål |
| Ansvarsfrekvens för konto | Procentandel aktiverade konton som visar engagemangssignaler | Mät aggregerade kundnivååtaganden |
| Influensa i rörledning | Intäktspipeline för kontobaserade aktiveringskampanjer | Spåra möjligheter som skapats från aktiverade kontomålgrupper |
| Kostnad per engagerat konto | Marknadsföringsutgifter delat med antalet konton som visar engagemang | Beräkna kostnaderna för annonsering och e-postkanal |
| Konverteringsgrad för lead | Procentandel leads från aktiverade konton som konverteras till affärsmöjligheter | Spåra konvertering mellan leads och säljtillfällen för aktiverade målgrupper |
| Besparing av målgruppsinstötning | Kostnad som undviks genom att inaktivera icke-berättigade konton från betalda kampanjer | Mät utgiftsreduktion från dämpade målgrupper |
| Kontotäckning | Procentandel av den totala adresserbara marknaden (TAM) som omfattas av aktiverade målgrupper | Jämför aktiverade konton mot det totala ICP-universum |

## Använd skiftlägesmönster

**B2B-målgruppsaktivering**

Aktivera kontobaserade B2B-målgrupper över webb-, e-post- och reklamkanaler.

**Funktionskedja:** Uppgradering av kontoprofil > Utvärdering av målpublik > Audience Activation > Övervakning

## Tillämpningar

Följande program används för att implementera det här användningsmönstret.

- **[!DNL Real-Time CDP]B2B edition** - Kärnplattform för enhetlig kontoprofil, B2B-identitetsupplösning, utvärdering av kontomottagare, B2B-specifik destinationskonfiguration och aktivering av kontomottagare
- **[!DNL Adobe Experience Platform] (AEP)** - Foundationsinfrastruktur för B2B XDM-datamodellering, datainhämtning från CRM och källor för automatiserad marknadsföring, identitetstjänst och styrning
- **[!DNL Marketo Engage]** - Primär automatiserad B2B-marknadsföring som mål för leadplantningsprogram, poängsättning och kampanjutförande som tillhandahålls av aktiverade kontomålgrupper

## Foundationsfunktioner

Följande grundläggande funktioner måste finnas för det här användningsmönstret. För varje funktion anger statusen om den vanligtvis är obligatorisk, antas vara förkonfigurerad eller inte tillämplig.

| Funktionen Foundation | Status | Vad måste finnas på plats | Experience League referens |
| --- | --- | --- | --- |
| Administration och styrning | Obligatoriskt | Sandlådan har etablerats med [!DNL RT-CDP] B2B edition aktiverat. Roller konfigurerade för datahantering B2B, målgruppsgenerering och målaktivering. ABAC-principer används om kontodata innehåller begränsade fält. | [Översikt över sandlådor](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/home), [Översikt över åtkomstkontroll](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Datamodellering och förberedelse | Obligatoriskt | B2B XDM-scheman konfigurerade med XDM Business Account, XDM Business Opportunity, XDM Business Campaign och XDM Individual Profile-klasser. B2B-fältgrupper som används för kontoattribut, person-kontouppgifter och affärsmöjlighetsdata. Datauppsättningar som skapats och profilaktiverade för varje B2B-enhet. Schemarelationer definierade mellan konto-, person-, affärsmöjlighets- och kampanjentiteter. | [XDM-systemöversikt](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/home), [B2B-scheman i Real-Time CDP](https://experienceleague.adobe.com/sv/docs/experience-platform/rtcdp/schemas/b2b) |
| Datakällor och samling | Obligatoriskt | Source-anslutningar har konfigurerats för CRM ([!DNL Salesforce], [!DNL Microsoft Dynamics]) och marknadsföringsautomatisering ([!DNL Marketo Engage]) för import av konto-, person-, affärsmöjlighets- och kampanjdata. Inmatningsledningar för batchströmning eller direktuppspelning är aktiva. Dataprep-mappningar har konfigurerats för att omvandla källdata till B2B XDM-scheman. | [Källor - översikt](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/home), [Marketo Engage Connector](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) |
| Konfiguration av identitet och profil | Obligatoriskt | B2B-identitetsnamnutrymmen har konfigurerats för kontoidentifierare (konto-ID, CRM-konto-ID) och personidentifierare (e-post, CRM-kontakt-ID, Marketo lead-ID). Relationer från människa till konto löses genom upplösning av B2B-identitet. Sammanfogningsprinciper har konfigurerats för enhetlig kontoprofil. | [Översikt över identitetstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/home), [B2B edition för Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#rtcdp-b2b) |
| Målgruppsdefinition och segmentering | Obligatoriskt | Målgruppsdefinitioner på kontonivå som skapats med kontoattribut, personattribut och aktivitetsdata. Utvärderingsscheman har konfigurerats för kontomålgrupper. Undertryckande målgrupper definierade för att utesluta icke-berättigade konton. | [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/home), [Kontomålgrupper](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/types/account-audiences) |

## Stödfunktioner

Följande funktioner förstärker det här användningsmönstret, men behövs inte för att köra kärnan.

| Stödfunktioner | Status | Varför det spelar någon roll | Experience League referens |
| --- | --- | --- | --- |
| Skapande av beräknat/härlett attribut | Rekommenderad | Aggregerade engagemangsmusik, livstidsvärde och aktivitetsmått på kontonivån förbättrar målgruppens precision. Beräknade attribut kan sammanfoga händelser på personnivå (e-postöppningar, webbbesök, nedladdningar av innehåll) till kontonivån för användning vid segmentering. | [Översikt över beräknade attribut](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| Livscykelhantering för data | Rekommenderad | B2B-datalagringsprinciper säkerställer att inaktuella konto- och affärsmöjlighetsdata rensas bort. Samtalshantering för B2B-kontakter säkerställer efterlevnad av regler för e-postmarknadsföring. Förfallotidsprinciper förhindrar ackumulering av föråldrade CRM-synkroniseringsdata. | [Översikt över livscykelhantering av avancerade data](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| Dataanvändningsetiketter och -tillämpning | Ingår | B2B-kontodata innehåller ofta avtalsbegränsningar (intäktssiffror, antal anställda från tredjepartsleverantörer). Dataanvändningsetiketter förhindrar att begränsade kontoattribut aktiveras till obehöriga destinationer. Styrningsprinciper säkerställer att PII-fält från kontaktuppgifter hanteras på rätt sätt under aktiveringen. | [Datastyrningsöversikt](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/home) |
| Övervakning och observerbarhet | Ingår | Övervakning av CRM- och [!DNL Marketo Engage]-källanslutningsdataflöden säkerställer att kontodata hålls aktuella. Målaktiveringsövervakning bekräftar att målgrupperna har levererats till [!DNL LinkedIn], [!DNL Marketo] och CRM-mål. Varningsregler fångar upp misslyckade inmatningar som skulle orsaka inaktuella kontodata. | [Aviseringsöversikt](https://experienceleague.adobe.com/sv/docs/experience-platform/observability/alerts/overview), [Övervaka måldataflöden](https://experienceleague.adobe.com/sv/docs/experience-platform/dataflows/ui/monitor-destinations) |
| Rapportering och analys | Rekommenderad | [!DNL CJA] B2B edition tillhandahåller kontonivåanalyser som omfattar målgruppens räckvidd, engagemang och pipeline-påverkan. Kontobaserad attribuering hjälper till att mäta effekten av aktiveringskampanjer på möjligheterna och intäkterna. | [CJA - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-overview/cja-overview) |

## Programfunktioner

I den här planen används följande funktioner från programfunktionskatalogen. Funktioner mappas till implementeringsfaser i stället för till numrerade steg.

### [!DNL Real-Time CDP] B2B edition ([!DNL RT-CDP] B2B)

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Enhetlig kontoprofil | Fas 1: Berikning av kontoprofiler | Konsolidera kontodata från CRM, automatiserad marknadsföring och externa källor till enhetliga kontoprofiler med hjälp av B2B XDM-schemaklasser |
| B2B-identitetsupplösning | Fas 1: Berikning av kontoprofiler | Lös relationer från människa till konto med hjälp av primära identifierare, mappa kontakter och leder till deras associerade konton |
| Utvärdering av målgrupp för konto | Fas 2: Konto - målgruppsutvärdering | Utvärdera segmentmedlemskapet på kontonivå genom att kombinera kontoattribut, personattribut och personaktivitetsdata |
| Konfiguration för kontomål | Fas 3: Målkonfiguration | Konfigurera anslutningar till B2B-specifika mål ([!DNL Marketo Engage], [!DNL LinkedIn], CRM, molnlagring) med fältmappning på kontonivå |
| Audience Activation | Fas 4: Audience Activation | Publicera kontobaserade målgrupper till konfigurerade mål för målgruppsanpassning, inaktivering eller CRM-synkronisering |
| Integrering av [!DNL Marketo Engage] | Fas 3: Målkonfiguration | Konfigurera dubbelriktat dataflöde med [!DNL Marketo Engage] med inbyggda B2B-käll- och målanslutningar |
| B2B-datastyrning | Fas 5: Styrning och övervakning | Använd dataanvändningspolicyer och samtycke för aktivering av B2B-kontodata för att förhindra obehörig dataexponering |

### [!DNL Real-Time CDP] ([!DNL RT-CDP]) - standardfunktioner

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Målgruppsutvärdering | Fas 2: Konto - målgruppsutvärdering | Underliggande utvärderingsmotor för kontomålgrupper, stöd för batchutvärdering av segmentdefinitioner på kontonivå |
| Målkonfiguration | Fas 3: Målkonfiguration | Kärninfrastruktur för målanslutning som används av B2B-specifik målkonfiguration |
| Audience Activation | Fas 4: Audience Activation | Infrastruktur för huvudaktiveringsdataflöde som används av kontomålets aktivering |
| Verkställande av samtycke och styrning | Fas 5: Styrning och övervakning | Använd samtyckesinställningar och dataanvändningspolicyer vid aktivering |

## Förutsättningar

Slutför följande innan du påbörjar implementeringen.

- [ ] [!DNL RT-CDP] B2B edition-licens har etablerats och aktiverats i organisationen
- [ ] CRM-system ([!DNL Salesforce] eller [!DNL Microsoft Dynamics]) tillgängligt med API-autentiseringsuppgifter för källanslutarkonfigurationen
- [ ] [!DNL Marketo Engage]-instansen har etablerats med API-åtkomst (Munchkin-ID, klient-ID, klienthemlighet) om [!DNL Marketo] används som mål
- [ ] [!DNL LinkedIn] Kampanjhanterarkonto med matchande målgrupper om [!DNL LinkedIn] används som mål
- [ ] B2B XDM-scheman skapade med klasserna konto, person, affärsmöjlighet och kampanj (F2)
- [ ] Source-anslutningar som har konfigurerats och aktivt inhämtar CRM- och marknadsföringsdata (F3)
- [ ] ID-relationer från människa till konto lösta och kontoprofiler enhetliga (F4)
- [ Konventioner och taxonomi för ]-konton har avtalats för målgruppsdefinitioner
- [ ] Datastyrningsprinciper definierade för datakänslighetsklassificeringar på kontonivå

## Implementeringsalternativ

Följande alternativ beskriver olika metoder för att implementera det här användningsmönstret. Granska varje alternativ och välj det som passar dina behov bäst.

### Alternativ A: Direktuppspelande målgruppsaktivering till [!DNL Marketo Engage]

**Passar bäst för:** Organisationer som använder [!DNL Marketo Engage] som sin primära automatiseringsplattform för B2B-marknadsföring, som behöver uppdateringar av målgruppsmedlemskap i nära realtid för att aktivera vårdsprogram, uppdatera lead-poäng eller ändra kampanjmedlemskap när konton kvalificeras eller diskvalificeras. 

**Så här fungerar det:**

Det här alternativet använder den inbyggda [!DNL Marketo Engage]-målkopplingen i [!DNL RT-CDP] för att strömma ändringar av målgruppsmedlemskapet direkt till [!DNL Marketo Engage]. När ett konto kvalificerar sig för eller avslutar ett målgruppssegment, uppdateras associerade leads och kontakter i [!DNL Marketo] med attribut för segmentmedlemskap. [!DNL Marketo] smarta kampanjer kan sedan utlösas baserat på dessa medlemsändringar.

Målet [!DNL Marketo Engage] är ett mål för direktuppspelning, vilket innebär att ändringar av målgruppsmedlemskap skickas stegvis när de inträffar i stället för i schemalagda batchar. Detta ger snabbare time-to-action för kampanjer som behöver reagera på ändringar av kontokvalificeringen. Fältmappningar kopplar profilattribut till [!DNL Marketo] lead-/kontaktfält, vilket möjliggör anrikning av [!DNL Marketo]-poster med kontonivådata från [!DNL RT-CDP].[!DNL RT-CDP]

**Viktiga överväganden:**

- Kräver aktiv [!DNL Marketo Engage]-prenumeration med API-åtkomst
- Aktivering av direktuppspelning skickar inkrementella uppdateringar, inte bilder med full publik
- Poster på personnivå i [!DNL Marketo] uppdateras, inte poster på kontonivå direkt
- [!DNL Marketo] smarta kampanjer måste konfigureras för att kunna agera på uppdateringar av fältet för segmentmedlemskap

**Fördelar:**

- Uppdateringar av målgruppsmedlemskap i nästan realtid i [!DNL Marketo]
- Inbyggd dubbelriktad anslutning förenklar integrering
- Inkrementella uppdateringar minimerar dataöverföringsvolymen
- [!DNL Marketo] kan omedelbart aktivera vårdprogram baserat på målgruppsändringar

**Begränsningar:**

- Begränsat till [!DNL Marketo Engage] som aktiveringsmål
- Behörighetsbegränsningarna för direktutvärdering gäller för de underliggande målgruppsdefinitionerna
- Kräver mappning mellan [!DNL RT-CDP]-kontomålgrupper och [!DNL Marketo] lead-/kontaktposter
- Komplex programlogik för [!DNL Marketo] kan behövas för att översätta uppdateringar på personnivå till åtgärder på kontonivå

**Experience League:**

- [Marketo Engage destination](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/adobe/marketo-engage)
- [Aktivera målgrupper för Marketo Engage](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/adobe/marketo-engage#activate)

### Alternativ B: Batchmålgruppsaktivering till annonseringsplattformar

**Bäst för:** Kontobaserade annonskampanjer på [!DNL LinkedIn], i visningsnätverk eller på andra annonsplattformar där det räcker med dagliga målgruppsuppdateringar och det primära målet är kontonivå och medvetenhet snarare än realtidsrespons.

**Så här fungerar det:**

Med det här alternativet aktiveras kontomålgrupper för att annonsera plattformsmål ([!DNL LinkedIn] matchade målgrupper, [!DNL Google] kundmatchning, [!DNL Facebook] anpassade målgrupper eller [!DNL The Trade Desk]) på en schemalagd batchkonferens. Aktiveringsdataflödet exporterar målgruppsmedlemmar med mappade identitetsfält (vanligtvis hashas-e-postadresser för associerade kontakter) som annonsplattformen använder för att matcha mot sin användarbas.

För [!DNL LinkedIn] specifikt accepteras företagsnamn och domänbaserad matchning i målplatsen [!DNL LinkedIn] Matched Audiences, förutom e-postbaserad matchning, vilket aktiverar korrekt målgruppsanpassning på kontonivå. Andra annonseringsplattformar kräver oftast personnivåidentifierare (e-post, telefon) från de kontakter som är kopplade till kvalificerade konton.

Batchaktivering körs enligt ett konfigurerbart schema (varje dag, var 6: e timme osv.) och exporterar antingen fullständiga målgruppsbilder eller stegvisa ändringar beroende på måltyp. Den här metoden är väl lämpad för kampanjer för kontinuerlig medvetenhet där kraven på målgruppernas aktualitet mäts i timmar i stället för i minuter.

**Viktiga överväganden:**

- Målgruppens aktualitet beror på batchschemat (vanligtvis dagligen)
- Advertising plattformar har egna begränsningar för matchningsfrekvens
- [!DNL LinkedIn] stöder matchning på kontonivå. Andra plattformar kräver identifierare på personnivå
- Exportfilformat och identitetskrav varierar beroende på mål

**Fördelar:**

- Stöd för flera annonsnätverk samtidigt
- Batchbearbetningen hanterar stora målgrupper effektivt
- Motsatt konto minskar bortslösade annonskostnader
- [!DNL LinkedIn] Matchade målgrupper aktiverar intern målgruppsanpassning på kontonivå

**Begränsningar:**

- Målgruppsuppdateringar är inte i realtid; latensen beror på batchschema
- Matchningsfrekvensen varierar beroende på plattform och tillgängliga identitetsfält
- Vissa plattformar stöder inte korrekt matchning på kontonivå, endast på personnivå
- Kräver separat målkonfiguration för varje annonseringsplattform

**Experience League:**

- [LinkedIn Matched Auditions destination](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/social/linkedin)
- [Google kundmatchningsmål](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/advertising/google-customer-match)
- [Målkatalog](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/overview)

### Alternativ C: Filbaserad aktivering till molnlagring

**Passar bäst för:** Organisationer som behöver maximal flexibilitet i hur kontomålgrupper förbrukas längre fram i kedjan, inklusive CRM-import, datalagerberikning, delning av partnerdata eller anpassade integreringar där en filbaserad överlämning är att föredra.

**Så här fungerar det:**

Det här alternativet exporterar kontomaterial som CSV-, JSON- eller Parquet-filer till molnlagringsmål ([!DNL Amazon S3], [!DNL Azure Blob Storage], [!DNL Google Cloud Storage], SFTP) på en schemalagd konferens. Exporten innehåller kontoattribut, fält på personnivå från associerade kontakter och metadata för målgruppsmedlemskap. Nedströmssystem använder dessa filer genom sina egna importprocesser.

Filbaserad aktivering ger störst kontroll över exportformat, fältval och schemaläggning. Det stöder både fullständig export (fullständig målgruppsbild vid varje körning) och inkrementell export (endast ändringar sedan den senaste körningen). Den här metoden används vanligtvis när målsystemet inte har någon intern [!DNL RT-CDP]-målkoppling, eller när organisationen måste förbearbeta eller omvandla data innan de läses in i målsystemet.

**Viktiga överväganden:**

- Kräver molnlagringsinfrastruktur ([!DNL S3], [!DNL Azure Blob], [!DNL GCS] eller SFTP)
- Importprocesser i senare led måste byggas och underhållas
- Filformatet (CSV, JSON, Parquet) måste matcha systemkraven för efterföljande
- Exportplanering måste justeras mot efterföljande bearbetningsfönster

**Fördelar:**

- Maximal flexibilitet i hur målgruppsdata konsumeras
- Stöder alla underordnade system som kan läsa filer
- Full kontroll över exportformat, fält och tidsplanering
- Kan betjäna flera kunder i efterföljande led från en och samma export
- Stöder fullständig och inkrementell export

**Begränsningar:**

- Högsta latens för alla alternativ (endast batch)
- Kräver att arbetsflöden för import längre fram i kedjan skapas och underhålls
- Ingen inbyggd integrering - ytterligare utvecklingsinsatser krävs
- Filhantering (rensning, arkivering) måste hanteras separat

**Experience League:**

- [Amazon S3-mål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/cloud-storage/amazon-s3)
- [Azure Blob Storage-mål](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/cloud-storage/azure-blob)
- [Aktivera målgrupper för batchdestinationer](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/api/connect-activate-batch-destinations)

### Alternativ D: Direktuppspelningsaktivering till CRM-system

**Bäst för:** Justering av försäljning/marknadsföring använder fall där kontokvalificeringsändringar måste återspeglas i CRM ([!DNL Salesforce] eller [!DNL Dynamics]) i nära realtid för säljteamets synlighet, områdestilldelningsuppdateringar eller automatiserade försäljningsarbetsflöden.

**Så här fungerar det:**

Det här alternativet använder direktuppspelade målanslutningar ([!DNL Salesforce] CRM, [!DNL Microsoft Dynamics]) för att skicka ändringar av målgruppsmedlemskap direkt till CRM-konto eller kontaktposter. När ett konto kvalificerar sig för eller avslutar en målgrupp uppdateras CRM-posten med ett anpassat fält som anger segmentmedlemskap. Säljarna kan sedan skapa CRM-rapporter, vyer och aviseringar baserat på dessa fält.

Direktuppspelningskopplingen skickar inkrementella uppdateringar när målgruppsmedlemskapet förändras. Fältmappningar ansluter [!DNL RT-CDP]-konto- och personattribut till CRM-fält, vilket möjliggör berikning av CRM-poster med enhetliga data från [!DNL RT-CDP]. Den här metoden avslutar slingan mellan marknadsföringsanalys (kontokvalificering) och säljutförande (CRM-arbetsflöden).

**Viktiga överväganden:**

- Kräver åtkomst till CRM API med lämpliga skrivbehörigheter
- Anpassade CRM-fält måste skapas för att kunna ta emot data om målgruppsmedlemskap
- Direktuppspelningsvolymen måste ligga inom gränserna för CRM API-hastigheter
- Automatisering av CRM-arbetsflöden måste konfigureras för att kunna hantera fältuppdateringar

**Fördelar:**

- CRM-uppdateringar i nära realtid för säljteamets synlighet
- Möjliggör automatiserade CRM-arbetsflöden som triggas av målgruppsändringar
- Utökar CRM-poster med enhetliga kontodata från [!DNL RT-CDP]
- Stöder fältuppdateringar på både konto- och kontaktnivå

**Begränsningar:**

- Gränsvärden för CRM-API:er kan begränsa uppdateringarna av stora volymer
- Kräver CRM-anpassning (anpassade fält, arbetsflöden)
- Begränsat till [!DNL Salesforce] och [!DNL Microsoft Dynamics] som inbyggda anslutningar
- Begränsningar för direktuppspelad utvärdering gäller för underliggande målgrupper

**Experience League:**

- [Salesforce CRM-mål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/crm/salesforce)
- [Microsoft Dynamics 365-mål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/crm/microsoft-dynamics-365)

### Jämförelse av alternativ

I följande tabell jämförs nyckelegenskaperna för varje implementeringsalternativ.

| Kriterier | Alternativ A: [!DNL Marketo] direktuppspelning | Alternativ B: Advertising Batch | Alternativ C: Molnlagring | Alternativ D: CRM-direktuppspelning |
| --- | --- | --- | --- | --- |
| Bäst för | Aktivering av sjukförsäkringsprogram | Kontobaserad annonsering | Flexibel integrering längre fram i kedjan | Försäljningsjustering |
| Komplex | Lågt | Medelsvåra: | Medium-High | Medelsvåra: |
| Latens | Nära realtid (minuter) | Grupp (timmar) | Grupp (timmar) | Nära realtid (minuter) |
| Flexibilitet | Låg ([!DNL Marketo] endast) | Medium (annonsnätverk) | Hög (alla system i senare led) | Låg (endast CRM) |
| Kräver | [!DNL Marketo Engage] licens | Advertising plattformskonton | Molnlagringsinfrastruktur | Åtkomst till CRM-API |
| Målinriktning på kontonivå | Via personposter | Endast [!DNL LinkedIn] (andra personnivå) | Konfigurerbar | Via konto-/kontaktposter |
| Underhållsarbete | Lågt | Låg-Medium | Högt | Medelsvåra: |

### Välj rätt alternativ

Använd följande riktlinjer för att välja rätt aktiveringsmetod:

1. **Om ditt primära mål är B2B-ledande sjukvård och du använder[!DNL Marketo Engage]** väljer du alternativ A. Den inbyggda direktuppspelningskontakten ger den snabbaste tiden till åtgärd för arbetsflöden för automatiserad marknadsföring.

2. **Om ditt primära mål är kontobaserad medvetenhet och generering av efterfrågan via annonsering** väljer du Alternativ B. [!DNL LinkedIn] Matchade målgrupper ger störst målinriktning på kontonivå. Använd andra annonsplattformar för större räckvidd.

3. **Om du behöver mata in kontomaterial till system utan interna [!DNL RT-CDP] kopplingar**, eller om du behöver största möjliga kontroll över dataformatet och nedladdningsbearbetning, väljer du alternativ C. Detta är också det bästa alternativet för delning av partnerdata eller för berikning av datalager.

4. **Om ditt primära mål är säljaktivering och CRM-synlighet för marknadsföringskvalificerade konton** väljer du alternativ D. Detta avslutar relationsslingan för marknadsföring till försäljning genom att CRM-posterna uppdateras i nära realtid.

De flesta B2B-organisationer implementerar flera alternativ samtidigt - till exempel Alternativ A för vårdprogram, Alternativ B för [!DNL LinkedIn]-annonsering och Alternativ D för CRM-synkronisering. De här alternativen utesluter inte varandra. Samma kontomålgrupp kan aktiveras för flera destinationer samtidigt.

## Implementeringsfaser

I följande faser beskrivs den stegvisa processen för att implementera det här användningsmönstret.

### Fas 1: Berikning av kontoprofiler

Denna fas skapar enhetliga kontoprofiler genom att konsolidera data från CRM, automatiserad marknadsföring och externa källor.

**Programfunktion:** [!DNL RT-CDP] B2B: Jämn kontoprofil, [!DNL RT-CDP] B2B: Identitetsupplösning för B2B

**Så här konfigurerar du:** I den här fasen skapas enhetliga kontoprofiler genom att data från CRM, automatiserad marknadsföring och tredjepartskällor konsolideras. B2B-identitetsupplösning mappar relationer mellan människor och konton så att engagemangsdata (e-postöppningar, webbbesök, innehållsnedladdningar) kan samlas in och användas i målgruppsutvärderingen på kontonivå. Den här fasen bygger på grundfunktionerna F2, F3 och F4 som redan måste finnas.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>**Beslut: Strategi för kontoidentifierare**
>
>Vilken identifierare fungerar som primär kontonyckel för alla system?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| ID för CRM-konto (t.ex. konto-ID för [!DNL Salesforce]) | CRM är systemet för bokföring | Det vanligaste sättet. Garanterar justering mellan [!DNL RT-CDP] och CRM. Kräver att alla källsystem refererar till samma CRM-konto-ID. |
>| ID för anpassat konto | Flera CRM-instanser eller en kontohanterare | Kräver ett mappningslager mellan källsystems-ID:n och det kanoniska konto-ID:t. Mer flexibel men mer komplex. |
>| DUNS-nummer eller domän | Dataanrikning från tredje part är den primära kontokällan | Användbar när firmografiska dataleverantörer är den primära källan. Kan kräva otydlig matchning för domänbaserad upplösning. |

>[!NOTE]
>**Beslut: Relationsmodellen person-till-konto**
>
>Hur är personer (leads, kontakter) kopplade till konton?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| En till en (varje person tillhör ett konto) | Enkel B2B-modell med rena CRM-data | Rak upplösning. De vanligaste för medelstora B2B-företag. |
>| Många-till-många (personer kan tillhöra flera konton) | Komplexa relationer, konsulter eller partnernätverk | [!DNL RT-CDP] B2B edition stöder detta internt. Ökar publikens komplexitet men speglar relationen i verkligheten korrekt. |

**Gränssnittsnavigering:** Plattform > Profiler > Bläddra (för att verifiera profiler för enhetliga konton)

**Information om nyckelkonfiguration:**

- Kontrollera att B2B XDM-scheman (XDM Business Account, XDM Business Person Account) finns på plats från F2
- Bekräfta att CRM- och [!DNL Marketo]-källanslutningar aktivt samlar in konto- och persondata från F3
- Verifiera att relationer från människa till konto är lösta i identitetsdiagrammet från F4
- Granska kontoprofilens fullständighet genom att bläddra bland exempelkontoprofilerna

**Experience League-dokumentation:**

- [Real-Time CDP B2B edition - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#rtcdp-b2b)
- [B2B-scheman i Real-Time CDP](https://experienceleague.adobe.com/sv/docs/experience-platform/rtcdp/schemas/b2b)
- [Marketo Engage Connector](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Salesforce Connector](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/connectors/crm/salesforce)

### Fas 2: Utvärdering av kontopublik

I den här fasen definieras och utvärderas målgrupper på kontonivå med hjälp av en kombination av kontoattribut, personattribut och personaktivitetsdata.

**Programfunktion:** [!DNL RT-CDP] B2B: Kontoutvärdering av målgrupp, [!DNL RT-CDP]: Målgruppsutvärdering

**Vad du ska konfigurera:** I den här fasen definieras och utvärderas målgrupper på kontonivå med hjälp av en kombination av kontoattribut, personattribut och personaktivitetsdata. Med kontomålgrupper i [!DNL RT-CDP] B2B edition kan du segmentera konton baserat både på firmografiska egenskaper (bransch, intäkter, antal anställda) och engagemangsbeteendet hos personer som är kopplade till dessa konton.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>**Beslut: Målgruppsutvärderingsmetod**
>
>Hur snabbt måste ni uppdatera medlemskapet?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Batchutvärdering (daglig) | Kampanjmålgrupper som uppdateras varje dag med filbaserade aktiveringar, målgrupper på annonsplattformar | De flesta målgrupper använder batchutvärdering. Hanterar komplexa multientitetsfrågor som kombinerar konto- och personattribut. Tillräckligt för de flesta B2B-fall där daglig uppdatering är acceptabel. |
>| Utvärdering av strömning | [!DNL Marketo] eller CRM-aktivering där nästan realtidskvalifikation krävs | Målgrupper har begränsad behörighet att strömma. Endast attributvillkor för enkla konton är berättigade för utvärdering av direktuppspelning. Beteendeförhållanden på personnivå kräver vanligtvis en batch. |

>[!NOTE]
>**Beslut: Definitionsmetod för kontomålgrupp**
>
>Hur definierar ni målgruppskriterierna för kontot?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Endast kontoattribut | Enkel, professionell målinriktning (industri, intäkter, region) | Snabbast att implementera. Begränsat till data på kontonivå. Använd för bred målinriktning. |
>| Konto + personattribut | Målkonton där associerade personer matchar specifika kriterier (befattning, avdelning) | Mer exakt målinriktning. Kombinerar data om firmografi och demografiska data. |
>| Konto + personattribut + personaktivitet | Målinrikta konton med engagerade kontakter (e-postöppningar, webbbesök, nedladdningar av innehåll) | Mest kraftfulla men mest komplexa. Kräver beteendehändelsedata från F3. Kräver vanligtvis grupputvärdering. |
>| Målgruppssammansättning | Komplex målgruppslogik som kräver rankning, delning, uteslutning eller berikning | Använd den visuella Audience Composition Canvas för härledda kontomålgrupper. Begränsad till grupputvärdering. |

>[!NOTE]
>**Beslut: Förhindra målgruppsstrategi**
>
>Vilka konton ska inte aktiveras?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Befintlig nedtryckning av kunder | Förvärvningskampanjer med nya konton som mål | Uteslut konton med aktiva prenumerationer eller stängda affärsmöjligheter |
>| Aktiv inaktivering av försäljningscykel | Undvik att störa konton i aktivt försäljningsärende | Uteslut konton med öppna affärsmöjligheter över en viss fas |
>| Undertryckande av senaste engagemang | Förhindra att meddelanden om nyligen kontaktade konton visas över | Uteslut konton som används i ett uppslagsfönster (t.ex. 30 dagar) |
>| Ingen nedtryckning | Kampanjer för varumärkesmedvetenhet som riktar sig till alla kvalificerade konton | Användning med försiktighet; kan leda till slöseri med utgifter för ej berättigade konton |

**Gränssnittsnavigering:** Kund > Publiker > Skapa målgrupp > Skapa regel (välj Konto som målgruppstyp)

**Information om nyckelkonfiguration:**

- Välj&quot;Konto&quot; som målgruppstyp när du skapar en ny målgrupp i segmentverktyget
- Kontoattribut visas under avsnittet Konto i Segment Builder (bransch, intäkt, kontostatus)
- Personattribut och aktiviteter kan läggas till via relationen Personer i kontomålskaparen
- Konfigurera batchutvärderingsschema om det inte redan finns ett för sandlådan
- Skapa både målgrupper (konton som ska inkluderas) och undertryckande målgrupper (konton som ska exkluderas)

**Experience League-dokumentation:**

- [Målgrupper](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/types/account-audiences)
- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Målgruppssammansättning](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/ui/audience-composition)
- [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/home)

### Fas 3: Målkonfiguration

I den här fasen upprättas autentiserade anslutningar till måldestinationer där kontomaterial ska levereras.

**Programfunktion:** [!DNL RT-CDP] B2B: Kontouppsättningskonfiguration, [!DNL RT-CDP] B2B: [!DNL Marketo Engage] Integrering, [!DNL RT-CDP]: Målkonfiguration

**Så här konfigurerar du:** I den här fasen skapas autentiserade anslutningar till de måldestinationer där kontomålgrupperna ska levereras. I konfigurationen ingår att välja mål från katalogen, tillhandahålla autentiseringsuppgifter, konfigurera fältmappningar på kontonivå och personnivå samt att ange exportschema. Varje måltyp har unika krav och funktioner.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>**Beslut: Målmarkering**
>
>Vilka mål kommer att ta emot de aktiverade målgrupperna?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| [!DNL Marketo Engage] | Främjande av leads, poängsättning och kampanjutförande inom B2B | Inbyggd direktuppspelningskontakt. Uppdaterar lead-/kontaktposter. Kräver [!DNL Marketo] API-autentiseringsuppgifter (Munchkin ID, klient-ID, Klienthemlighet). |
>| [!DNL LinkedIn] matchade målgrupper | Kontobaserad annonsering på [!DNL LinkedIn] | Stöder företagsnamn- och domänmatchning för målgruppsanpassning på kontonivå. Gruppaktivering. Kräver [!DNL LinkedIn] åtkomst till Campaign Manager. |
>| [!DNL Salesforce] CRM | Synkronisering av aktivering av försäljning och CRM-kontolista | Streaming Connector uppdaterar konto- eller kontaktposter. Kräver [!DNL Salesforce] API-åtkomst med skrivbehörigheter. |
>| [!DNL Microsoft Dynamics 365] | Säljaktivering för [!DNL Dynamics]-baserade organisationer | Direktuppspelningskontakt. Kräver [!DNL Dynamics 365] API-åtkomst. |
>| Molnlagring ([!DNL S3], [!DNL Azure Blob], [!DNL GCS], SFTP) | Anpassade integreringar, datalager, partnerdelning | Filbaserad batchexport. Maximal flexibilitet, men kräver bearbetning i efterföljande led. |
>| [!DNL Google] kundmatchning | Söka efter och visa annonsering | Matchning på personnivå via hashad e-post. Gruppaktivering. |
>| [!DNL The Trade Desk] | Programmatisk displayannonsering och videoreklam | Personnivåmatchning. Gruppaktivering. |

>[!NOTE]
>**Beslut: Fältmappningsstrategi**
>
>Vilka konto- och personfält ska mappas till målet?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Endast identitetsfält | Advertising-plattformar som bara behöver matchande identifierare | Minimal dataöverföring. Målet matchar på e-postadress eller företagsdomän. |
>| Identitet + attribut för huvudkonto | CRM eller [!DNL Marketo] där kontextens mål förbättras | Inkludera bransch, intäkter, antal anställda och kontonivå. Berika underordnade poster. |
>| Fullständig attributuppsättning | Export av molnlagring eller datalager | Inkludera alla relevanta konto- och personattribut. Största exportnyttolast. |

**Gränssnittsnavigering:** Anslutningar > Destinationer > Katalog > Sök efter mål > Konfigurera

**Information om nyckelkonfiguration:**

- Navigera till målkatalogen och välj måldestinationen
- Ange autentiseringsuppgifter som är specifika för måltypen
- Konfigurera fältkopplingar som ansluter [!DNL RT-CDP] XDM-fält till målfält
- För [!DNL Marketo Engage]: ange Munchkin-ID, klient-ID och klienthemlighet
- För [!DNL LinkedIn]: auktorisera via OAuth och välj annonskontot [!DNL LinkedIn]
- För molnlagring: ange namn, sökväg, filformat och autentiseringsuppgifter för bucket/behållaren
- För CRM: ange instans-URL, API-autentiseringsuppgifter och målobjekttyp (konto eller kontakt)

**Var alternativen skiljer sig:**

**För alternativ A ([!DNL Marketo Engage] direktuppspelning):**

Navigera till Destinationer > Katalog > Adobe > [!DNL Marketo Engage]. Konfigurera autentiseringsuppgifterna för Munchkin ID och API. Mappa [!DNL RT-CDP] identitetsfält (e-post) och profilattribut till [!DNL Marketo] lead-fält. Målet hanterar automatiskt inkrementella direktuppspelningsuppdateringar.

**För alternativ B (Advertising Platform Batch):**

Navigera till Destinations > Catalog > Advertising/Social > select platform. Auktorisera via OAuth. Konfigurera exportschemat (rekommenderas: dagligen). Kartan hashade e-postidentifierare och matchande fält som stöds. För [!DNL LinkedIn] kan du även mappa företagsnamn- och domänfält för kontonivåmatchning.

**För alternativ C (molnlagringsfilsbaserad):**

Navigera till Destinationer > Katalog > Cloud-lagring > välj provider. Konfigurera bucket/container, filsökvägsmall och filformat (CSV, JSON eller Parquet). Ange exportschemat och välj fullständig eller stegvis export. Mappa alla önskade attribut för konto och person.

**För alternativ D (CRM-direktuppspelning):**

Navigera till Destinationer > Katalog > CRM > markera [!DNL Salesforce] eller [!DNL Dynamics]. Ange API-autentiseringsuppgifter och instans-URL. Mappa [!DNL RT-CDP] fält till CRM-konto eller kontaktfält. Kontrollera att det finns anpassade fält i CRM för att ta emot data om målgruppsmedlemskap.

**Experience League-dokumentation:**

- [Översikt över destinationer](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/home)
- [Målkatalog](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/overview)
- [Marketo Engage destination](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/adobe/marketo-engage)
- [LinkedIn Matched Auditions destination](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/social/linkedin)
- [Salesforce CRM-mål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/crm/salesforce)
- [Amazon S3-mål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/cloud-storage/amazon-s3)

### Fas 4: Målgruppsaktivering

I den här fasen publiceras de utvärderade målgrupperna för kontot till de konfigurerade målgrupperna.

**Programfunktion:** [!DNL RT-CDP] B2B: Account Audience Activation, [!DNL RT-CDP]: Audience Activation

**Så här konfigurerar du:** I den här fasen publiceras de utvärderade målgrupperna för kontot till de konfigurerade målgrupperna. Aktiveringen skapar dataflödet som ansluter kontomålgruppen (källan) till det externa målet (målet), tillämpar attributmappningar och initierar exporten enligt det konfigurerade schemat eller direktuppspelningsbeteendet. Du kommer även att konfigurera avvisande målgrupper så att ej konton kan aktiveras.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>**Beslut: Exporttyp**
>
>Ska aktiveringen exportera fullständiga målgruppsbilder eller endast inkrementella förändringar?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Stegvis export | Direktuppspelningsmål ([!DNL Marketo], CRM) eller batchmål där deltas hanteras i underordnade system | Mindre datavolym per export. Snabbare bearbetning. Kräver att system längre fram i kedjan hanterar tillstånd. Standard för direktuppspelningsmål. |
>| Fullständig export | Batchdestinationer där det underordnade systemet ersätter hela målgruppen vid varje körning | Större datavolym, men enklare logik längre fram i kedjan. Användbart när system längre fram i kedjan inte har något tillstånd. Tillgängligt för filbaserade mål. |

>[!NOTE]
>**Beslut: Aktiveringsomfång**
>
>Hur många målgrupper ska aktiveras per mål?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| En målgrupp per dataflöde | Enkel aktivering med tydlig målgruppsmappning | Enklast att övervaka och felsöka. Ett publikmisslyckande påverkar inte andra. |
>| Flera målgrupper per dataflöde | Flera relaterade målgrupper går till samma mål | Effektivare användning av målanslutningar. Alla målgrupper delar samma fältmappning och schema. |

**Gränssnittsnavigering:** Anslutningar > Destinationer > Bläddra > Välj mål > Aktivera målgrupper

**Information om nyckelkonfiguration:**

- Välj målgrupp(er) i målgruppslistan
- Granska och bekräfta fältmappningarna som konfigurerats i fas 3
- För batchmål: konfigurera exportschemat (tid, frekvens)
- För direktuppspelningsmål: aktiveringen börjar omedelbart efter konfigurationen
- Om du vill kan du lägga till undertryckande målgrupper med exkluderingsfunktionen
- Starta en första testaktivering för att validera dataflödet

**Var alternativen skiljer sig:**

**För alternativ A ([!DNL Marketo Engage] direktuppspelning):**

Välj vilka kontomålgrupper som ska aktiveras. Aktiveringen börjar strömma direkt. Verifiera i [!DNL Marketo] att lead-/kontaktposter uppdateras med segmentmedlemsfält. Konfigurera [!DNL Marketo] smarta kampanjer som ska utlösas baserat på de här fältändringarna.

**För alternativ B (Advertising Platform Batch):**

Välj målgrupper och konfigurera dagligt exportschema. När den första exporten är klar kontrollerar du i annonsplattformen att målgruppen visas och har ett ifyllt medlemsantal. Plattformen kan behandla den första målgruppsfilen i 24-48 timmar.

**För alternativ C (molnlagringsfilsbaserad):**

Välj målgrupper och konfigurera exportschemat och filformatet. Efter den första exporten visas verifieringsfilerna på mållagringsplatsen med det förväntade formatet och innehållet. Bekräfta att importprocesserna längre fram i kedjan använder de exporterade filerna.

**För alternativ D (CRM-direktuppspelning):**

Välj vilka kontomålgrupper som ska aktiveras. Aktiveringen börjar strömma direkt. Kontrollera i CRM att konto- eller kontaktposter uppdateras med mappade fält. Konfigurera CRM-rapporter, listvyer eller automatiserade arbetsflöden för att agera på de uppdaterade fälten.

**Experience League-dokumentation:**

- [Aktivera målgrupper för direktuppspelningsmål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Aktivera målgrupper för batchdestinationer](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Aktiveringsskydd](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/guardrails)
- [Översikt över destinationer](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/home)

### Fas 5: Styrning och övervakning

Den här fasen säkerställer att kontomålens aktivering överensstämmer med policyer för datastyrning och medgivanden samt att pågående aktiveringsdataflöden övervakas för hälsa.

**Programfunktion:** [!DNL RT-CDP] B2B: B2B-datastyrning, [!DNL RT-CDP]: Samtycke och styrning

**Vad du konfigurerar:** Den här fasen ser till att kontomålets aktivering uppfyller reglerna för datastyrning och för samtycke, och att pågående aktiveringsdataflöden övervakas för hälsa. B2B-datastyrning tillämpar begränsningar för känsliga kontoattribut (intäkter, antal anställda från tredjepartsleverantörer), medan medgivande säkerställer att meddelanden på personnivå respekterar avanmälningsinställningar. Övervakningen bekräftar att aktiveringsdataflödena har slutförts.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>**Beslut: Styrningsnivå**
>
>Hur strikt ska datastyrning tillämpas för B2B-aktiveringar?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Full kontroll (blockera vid överträdelse) | Produktionsaktiveringar med känsliga data | Förhindrar aktivering som bryter mot styrningsprinciper. Det kan krävas iterativa fältmappningsjusteringar för att åtgärda överträdelser. |
>| Varna och fortsätt | Utvecklings- och testmiljöer | Aktiveringen kan fortsätta, men varningar loggas. Användbar under den första konfigurationen för att identifiera potentiella problem. |

>[!NOTE]
>**Beslut: Övervakningsmetod**
>
>Hur ska aktiveringshälsan övervakas?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Varningsbaserad övervakning | Produktionsmiljöer där fel snabbt måste hanteras | Konfigurera aviseringar om misslyckade målaktiveringar, fel i källflöden och fördröjningar i dataflöden. Kräver inställning av aviseringsprenumeration. |
>| Manuell övervakning | Utvecklings- eller lågvolymsaktiveringar | Granska dataflödet regelbundet i gränssnittet för destinationer. Mindre overhead men risk för upptäckt av fördröjda fel. |
>| Båda | Produktionsmiljöer med komplex multidestinationsaktivering | Varningar för allvarliga fel samt regelbunden granskning av instrumentpanelen för trender. Rekommenderas för de flesta B2B-implementeringar. |

**Gränssnittsnavigering:** Integritet > Principer (för styrning), Anslutningar > Destinationer > Bläddra > Välj mål > Dataflöd (för övervakning)

**Information om nyckelkonfiguration:**

- Tillämpa dataanvändningsetiketter på B2B-datauppsättningar som innehåller begränsade attribut
- Verifiera att styrningsprinciper tillämpas genom att utvärdera aktiveringen mot målmarknadsföringsåtgärden
- Konfigurera aviseringar för målaktiveringsfel och fel i källkopplingen
- Granska körningsmått för dataflöde (exporterade profiler, poster misslyckades) efter varje aktiveringscykel
- Ställ in kontrollpanelsgranskning av licensanvändning för att spåra kontoprofilens volym mot berättiganden

**Experience League-dokumentation:**

- [Översikt över dataförvaltning](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/home)
- [Samtycke och inställningar](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)
- [Övervaka måldataflöden](https://experienceleague.adobe.com/sv/docs/experience-platform/dataflows/ui/monitor-destinations)
- [Översikt över aviseringar](https://experienceleague.adobe.com/sv/docs/experience-platform/observability/alerts/overview)
- [Aktiveringsskydd](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/guardrails)

## Implementeringsöverväganden

Följande avsnitt innehåller ytterligare vägledning för ett lyckat genomförande.

### Skyddsritningar och begränsningar

Granska följande plattformsskyddsutkast och begränsningar som gäller för det här användningsmönstret.

- Maximalt 4 000 segmentdefinitioner per sandlåda, inklusive kontomaterial - [Skyddsritningar för segmentering](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/guardrails)
- Målgrupper utvärderas huvudsakligen genom grupputvärdering; rätten till direktuppspelning begränsas till villkoren för enkla kontoattribut
- Maximalt 100 dataflöden per målanslutning - [Målsäkerhetsutkast](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/guardrails)
- Batchdestinationer exporterar upp till 5 miljoner profiler per filsegment
- Målen för direktuppspelning har genomströmningsgränser per sekund som angetts av målpartnern (t.ex. [!DNL Marketo] API-hastighetsgränser)
- Sammansatta målgrupper (från Audience Composition) är begränsade till grupputvärdering och kan inte använda direktuppspelning
- Max 10 kompositionsblock per Audience Composition Canvas
- [!DNL LinkedIn] matchade målgrupper kräver en minsta målgruppsstorlek (vanligtvis 300 medlemmar) för aktivering
- Målen för CRM-direktuppspelning omfattas av CRM-providerns API-hastighetsbegränsningar (t.ex. [!DNL Salesforce] API-massgränser per dag)
- [!DNL RT-CDP] B2B edition-licensen styr det totala antalet företagskontoprofiler - [RT-CDP-produktbeskrivning](https://helpx.adobe.com/se/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

### Vanliga fallgropar

Tänk på följande vanliga problem när du implementerar det här användningsmönstret.

- **Ofullständig mappning från människa till konto:** Om personposter (leads, kontakter) inte är korrekt länkade till kontoposter via B2B-identitetsupplösning, kommer kontomålgrupper som är beroende av personattribut eller aktiviteter att underräkna kvalificerade konton. Validera relationer från människa till konto i F4 innan du bygger upp målgrupper för konton.

- **Inaktuella CRM-data som orsakar målgruppsdrift:** Om CRM-källanslutningar inte körs regelbundet eller inte fungerar korrekt, blir kontoattributen (bransch, intäkt, status) inaktuella. Detta gör att målgrupper inkluderar konton som inte längre är kvalificerade eller exkluderar konton som bör vara kvalificerade. Övervaka källanslutningens dataflödeshälsa.

- **Advertising-plattformens matchningsförväntningar:** När kontomålgrupper aktiveras för andra annonsnätverk än [!DNL LinkedIn] beror matchningsfrekvensen på att det finns giltiga identifierare på personnivå (hashade e-post) för kontakter som är associerade med kvalificerande konton. Konton utan associerade kontakter som har e-postadresser matchar inte. Övervaka matchningsfrekvenser och överväg att förbättra kontaktdata.

- Felaktig justering av fältmappning för **[!DNL Marketo]:** Vid direktuppspelning till [!DNL Marketo Engage] måste fältmappningen för [!DNL RT-CDP] ha befintliga fält för lead eller kontakt för [!DNL Marketo] som mål. Om det mappade [!DNL Marketo]-fältet inte finns, misslyckas uppdateringen utan fel. Skapa alla målfält i [!DNL Marketo] i förväg innan du konfigurerar målet.

- **Blockeringsaktivering av styrningsprincip:** Dataanvändningsetiketter för kontoattributfält (särskilt profildata från tredje part) kan utlösa styrningsfel när annonseringsmål aktiveras. Utvärdera styrningens efterlevnad innan du aktiverar och justerar fältmappningar för att exkludera begränsade fält vid behov.

- **Kontomålgrupper som kombinerar konto- och persondata med endast grupputvärdering:** Kontomålgrupper som refererar till beteendehändelser på personnivå (t.ex. &quot;konton där minst en kontakt har öppnat ett e-postmeddelande under de senaste 30 dagarna&quot;) kräver grupputvärdering. Om ett användningsfall förväntar sig realtidskvalifikation kan den här begränsningen orsaka oväntad fördröjning.

### God praxis

Följ dessa rekommendationer för optimala resultat.

- Börja med ett litet antal väldefinierade målgrupper (ICP-nivå, branschvertikal, engagemangsnivå) innan du expanderar till komplexa flerattributsdefinitioner
- Skapa dedikerade undertryckningsmålgrupper för befintliga kunder, aktiva möjligheter och nyligen engagerade konton för att undvika slösade utgifter och kanalkonflikter
- Använd Audience Composition för att skapa målgrupper med nivåindelade konton (högt/medelhögt/lågt engagemang) genom att rangordna konton på aggregerade engagemangspoäng
- Aktivera samma kontomålgrupp för flera mål samtidigt för samordnade flerkanalskampanjer (t.ex. [!DNL LinkedIn] för annonsering, [!DNL Marketo] för e-post, CRM för synlighet)
- Implementera en konsekvent namngivningskonvention för kontomålgrupper som innehåller målkriterier och avsedd kanal (t.ex. &quot;B2B_ICP_Enterprise_Tech_LinkedIn&quot; eller &quot;B2B_Suppression_ActiveOpps&quot;)
- Schemalägg batchaktivering under lågbelastningstimmar för att minimera påverkan på system längre fram i kedjan och anpassa sig till reklamplattformens bearbetningsfönster
- Övervaka matchningsfrekvenser per mål efter den initiala aktiveringen och iterera på identitetsfältsmappningar för att förbättra matchningen
- Behåll dubbelriktat dataflöde med [!DNL Marketo Engage]: importera engagemangsdata från [!DNL Marketo] till [!DNL RT-CDP] (källkoppling) och aktivera målgrupper tillbaka till [!DNL Marketo] (målkoppling) för ett slutet loop-system

### Avvecklingsbeslut

Tänk på följande när du fattar implementeringsbeslut.

>[!NOTE]
>**Brytfrekvens: Målgruppens aktualitet kontra utvärderingens komplexitet**
>
>Kontogrupper som kombinerar kontoattribut med beteendedata på personnivå erbjuder den mest exakta målgruppsanpassningen men är begränsade till grupputvärdering (daglig uppdatering). Enklare målgrupper som enbart bygger på kontoattribut kan kvalificera sig för direktuppspelningsutvärdering med uppdateringar i nära realtid.
>
>- **Batch (komplexa kriterier) prioriterar:** Måttprecision, kombinerar febergrafiska signaler och beteendesignaler, omfattande kontobedömning
>- **Direktuppspelning (enkla kriterier) prioriterar:** Snabba upp publiken att uppdatera, svar i realtid på kontoändringar, snabbare time-to-action i [!DNL Marketo] och CRM
>- **Rekommendation:** Använd batchutvärdering för primära målgrupper där daglig uppdatering är acceptabel (de flesta användningsfall för B2B). Reservera utvärdering av direktuppspelning för tidskänsliga utlösare som kontostatusändringar eller kontovarningar med högt värde.

>[!NOTE]
>**Avvikelse: Centraliserad aktivering jämfört med målspecifika målgrupper**
>
>Ni kan aktivera en enda målgrupp för ett enhetligt konto för flera destinationer eller skapa målspecifika målgrupper som är skräddarsydda efter varje kanals funktioner och krav.
>
>- **Centraliserad målgrupp prioriterar:** Enhetlighet i alla kanaler, enklare målgruppshantering, enhetlig rapportering
>- **Målspecifika målgrupper prioriterar:** Optimerad målgruppsanpassning per kanal (t.ex. [!DNL LinkedIn] drar nytta av attribut på företagsnivå medan [!DNL Marketo] behöver information på leads), kanalspecifika undertryckningsregler
>- **Rekommendation:** Börja med centraliserade målgrupper för enhetlighet och skapa sedan destinationsspecifika varianter endast när kanalkraven skiljer sig avsevärt (t.ex. olika inaktiveringsfönster för annonsering och e-post).

>[!NOTE]
>**Brytfrekvens: CRM-synkronisering i realtid jämfört med CRM-uppdateringar i batch**
>
>Direktuppspelning till CRM ger omedelbar försäljningssynlighet men förbrukar CRM API-kvoten. Export av gruppfiler är effektivare men ger fördröjning.
>
>- **Synkronisering av direktuppspelad CRM prioriterar:** Svarstider för försäljning, aviseringar om omedelbart konto, synlighet för pipeline i realtid
>- **Uppdateringar för gruppbaserad CRM prioriterar:** bevarande av API-kvot, gruppuppdatering, justering med inläsningsfönster för CRM-data
>- **Rekommendation:** Använd direktuppspelad CRM-synkronisering för kontokvalificeringsändringar med hög prioritet (t.ex. så flyttas kontot till nivån&quot;Förs.klar&quot;). Använd batchfilexport för bulkuppdateringar som månatliga kontopoänguppdateringar eller områdesomtilldelningslistor.

## Relaterad dokumentation

Följande resurser innehåller ytterligare kontext och detaljerade riktlinjer för de funktioner som används i det här användningsmönstret.

**[!DNL RT-CDP]B2B edition**

- [Real-Time CDP B2B edition - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#rtcdp-b2b)
- [B2B-scheman i Real-Time CDP](https://experienceleague.adobe.com/sv/docs/experience-platform/rtcdp/schemas/b2b)
- [Målgrupper](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/types/account-audiences)
- [RT-CDP B2B edition produktbeskrivning](https://helpx.adobe.com/se/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

**Målgruppsutvärdering och -segmentering**

- [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/home)
- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Målgruppssammansättning](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/ui/audience-composition)
- [Direktuppspelningssegmentering](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Skyddsritningar för segmentering](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/guardrails)

**Destinationer och aktivering**

- [Översikt över destinationer](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/home)
- [Målkatalog](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/overview)
- [Marketo Engage destination](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/adobe/marketo-engage)
- [LinkedIn Matched Auditions destination](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/social/linkedin)
- [Salesforce CRM-mål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/crm/salesforce)
- [Microsoft Dynamics 365-mål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/crm/microsoft-dynamics-365)
- [Amazon S3-mål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/cloud-storage/amazon-s3)
- [Aktivera målgrupper för direktuppspelningsmål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Aktivera målgrupper för batchdestinationer](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Aktiveringsskydd](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/guardrails)

**Datakällor och anslutningar**

- [Översikt över källor](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/home)
- [Marketo Engage Connector](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Salesforce Connector](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/connectors/crm/salesforce)

**Datamodellering och identitet**

- [XDM - systemöversikt](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/home)
- [Översikt över identitetstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/home)
- [Profilöversikt](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/home)
- [Översikt över kopplingsprofiler](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/merge-policies/overview)

**Datastyrning och sekretess**

- [Översikt över dataförvaltning](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/home)
- [Översikt över etiketter för dataanvändning](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/labels/overview)
- [Samtycke och inställningar](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)

**Övervakning och observerbarhet**

- [Översikt över aviseringar](https://experienceleague.adobe.com/sv/docs/experience-platform/observability/alerts/overview)
- [Övervaka måldataflöden](https://experienceleague.adobe.com/sv/docs/experience-platform/dataflows/ui/monitor-destinations)
- [Övervaka källdataflöden](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/api-tutorials/monitor)
- [Kontrollpanel för licensanvändning](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/license-usage-dashboard)

**Rapportering och analys**

- [CJA - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-overview/cja-overview)
- [Anslutningar - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-connections/overview)
- [Översikt över datavyer](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/data-views)

**Självstudiekurser och guider**

- [Komma igång med Real-Time CDP B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro)
- [Skapa ett schema för B2B-källor](https://experienceleague.adobe.com/sv/docs/experience-platform/rtcdp/schemas/b2b)
- [Verktyg för sandlåda](https://experienceleague.adobe.com/sv/docs/experience-platform/sandbox/sandbox-tooling-api/overview)
