---
title: Vidarebefordran av händelser
description: Lär dig hur du vidarebefordrar händelsedata i realtid som samlats in via Edge Network till destinationer utanför Adobe för analys, lagring eller annonsering.
solution: Experience Platform
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '6342'
ht-degree: 0%

---


# Vidarebefordran av händelser

Den här guiden beskriver implementeringen av händelsevidarebefordran på serversidan med hjälp av [!DNL Adobe Experience Platform] Edge Network. Det är utformat för lösningsarkitekter, marknadsföringsteknologer och implementeringstekniker som behöver distribuera händelsedata i realtid som samlats in via Edge Network till icke-Adobe-destinationer - som analysplattformar från tredje part, molnlagringsslutpunkter, annonsnätverk eller anpassade webhooks.

Den presenterar alla användbara metoder för att konfigurera händelsevidarebefordran, förklarar skillnaderna mellan dem och länkar till [!DNL Adobe Experience League]-dokumentation för detaljerad procedurvägledning.

## Använd ärendeöversikt

Organisationer som samlar in beteendedata via [!DNL Adobe Experience Platform] Web SDK, Mobile SDK eller Server API måste ofta dela samma händelseström med andra system än Adobe - analysplattformar som [!DNL Google Analytics] eller [!DNL Snowflake], annonsnätverk för konverteringsspårning, datalager för långsiktig lagring eller anpassade interna tjänster. Traditionellt sett är det här krav på spridning av taggar på klientsidan, vilket ökar sidans vikt, ger fördröjning och skapar sekretess- och styrningsrisker.

Vidarebefordran av händelser löser detta genom att använda en server i Edge Network. När en besökarinteraktion utlöser en händelse via webb-SDK eller Server-API:t dirigeras händelsen via ett datastream till Edge Network. Regler för vidarebefordran av händelser - konfigurerade i en dedikerad egenskap för vidarebefordran av händelser - utvärderar inkommande händelsedata och vidarebefordrar dem selektivt till en eller flera konfigurerade destinationer. Serversidan minskar taggblocket på klientsidan, förbättrar sidprestanda, centraliserar datastyrningen och ger organisationen kontroll över exakt vilka data som lämnar Adobe ekosystem.

Målgruppen för det här mönstret innehåller organisationer som redan har distribuerat (eller planerar att distribuera) API:t [!DNL Adobe Experience Platform] Web SDK eller Server för datainsamling och som vill utöka den investeringen genom att distribuera händelsedata till slutpunkter som inte är från Adobe utan att lägga till JavaScript-taggar på klientsidan.

## Viktiga verksamhetsmål

Följande affärsmål stöds av det här användningsmönstret.

### Förbättra datakvaliteten och styrningen

Säkerställ rena, fullständiga och kompatibla data för korrekt målinriktning, minskat avfall och tillförlitlig analys. Vidarebefordran av händelser centraliserar datadistributionen på serversidan och ger organisationen en enda kontrollpunkt för vilka data som delas med externa system, vilket minskar risken för dataläckage och säkerställer att styrningsprinciper tillämpas innan data lämnar [!DNL Adobe] Edge Network.

**KPI:er:** Effektivitet, kostnadsbesparingar

Mer information finns i [Förbättra datakvaliteten och styrningen](../../business-objectives/cost-efficiency/improve-data-quality-governance.md).

### Konsolidera och modernisera marknadsföringsteknologi

Minska verktygets fragmentering och tekniska skulder genom att gå över till enhetliga, skalbara plattformar. Med händelsevidarebefordran kan organisationer ersätta flera leverantörstaggar på klientsidan med en enda datadistributionsmekanism på serversidan, vilket minskar belastningen på sidan och förenklar teknikstacken.

**KPI:er:** kostnadsbesparingar, effektivitet, hastighet till marknad

Mer information finns i [Konsolidera och modernisera marknadsföringsteknologi](../../business-objectives/cost-efficiency/consolidate-modernize-marketing-technology.md).

## Exempel på taktiska användningsfall

Här följer några vanliga taktiska scenarier där det här använder fallmönstret.

- **Analysberikning från tredje part** - Vidarebefordra sidvy, klickningar och konverteringshändelser till [!DNL Google Analytics], [!DNL Snowflake] eller andra analysplattformar i realtid utan att lägga till taggar på klientsidan
- **Advertising-konverteringsspårning** - Skicka köp- och leadgenereringshändelser till [!DNL Meta] Konverterings-API, [!DNL Google Ads], [!DNL TikTok] eller [!DNL Snap] för mätning och optimering av konvertering på serversidan
- **Direktuppspelning av datalager** - Dirigera råhändelsedata till ett molndatalager ([!DNL Google BigQuery], [!DNL Amazon S3], [!DNL Azure Event Hubs]) för långtidslagring och offlineanalys
- **Anpassad webbkrokintegrering** - Vidarebefordra filtrerade eller transformerade händelsedata till interna mikrotjänster, CRM-system eller partnerplattformar via HTTP-slutpunkter
- **Taggreducering och bättre sidprestanda** - Ersätt flera JavaScript-taggar från klientsidan med en enda Web SDK-implementering plus regler för vidarebefordran av händelser på serversidan, minska sidvikten och förbättra Core Web Vitals
- **Sekretesskompatibel datadelning** - Använd datafiltrering och bortredigeringsregler på fältnivå på serversidan innan du delar händelsedata med tredje part, så att PII-filerna rensas eller hashas innan de når externa system
- **Händelsedistribution i flera moln** - Vidarebefordra samtidigt samma händelseström till flera mål (till exempel analyser, annonsering och datalager) från en enda regeluppsättning på serversidan
- **Vidarebefordra signaler om bedrägeri i realtid** - Vidarebefordra transaktioner med högt värde till system för upptäckt av bedrägeri för riskbedömning och larm i realtid

## Nyckeltal för prestanda

Följande nyckeltal hjälper till att mäta hur bra det här användningsmönstret är.

- **Tidsreduktion för sidinläsning** - Uppmätt förbättring av sidinläsningshastighet och Core Web Vitals efter migrering av klienttaggar till händelsevidarebefordran på serversidan
- **Slutförandefrekvens för dataleverans** - Procent av händelser som har vidarebefordrats till målslutpunkter utan fel eller timeout
- **Minskning av antal taggar** - Antal leverantörstaggar på klientsidan som tagits bort efter implementering av motsvarigheter på serversidan
- **Dataaktualitet/fördröjning** - Tid mellan händelseförekomst på klienten och händelseankomst till målslutpunkten (mål: subsekund till sekund)
- **Kompatibilitetsnivå för styrning** - Procentandel utgående dataresurser som passerar genom filtreringsregler på serversidan, vilket säkerställer att inga PII-data eller begränsade data når obehöriga mål
- **Driftseffektivitet** - Minska antalet utvecklartimmar som har ägnats åt att hantera taggdistributioner på klientsidan och felsöka taggkonflikter

## Använd skiftlägesmönster

I det här avsnittet beskrivs mönstret och funktionskedjan som används för att implementera händelsevidarebefordran.

**Händelsevidarebefordran** - Vidarebefordra händelsedata i realtid som samlats in via Edge Network till andra mål än Adobe för analys, lagring eller annonsering.

**Funktionskedja:** Datastream Configuration > Event Rule Definition > Destination Mapping > Forwarding Execution > Monitoring

## Tillämpningar

Följande program används i det här fallmönstret.

- **[!DNL Adobe Experience Platform](Edge Network)** - Tar emot och skickar händelsedata i realtid från Web SDK, Mobile SDK eller Server-API via konfigurerade datastreams
- **[!DNL Adobe Experience Platform](Händelsevidarebefordran)** - Tillhandahåller regelmotorn på serversidan för utvärdering, filtrering, omformning och vidarebefordran av händelsedata till externa mål
- **[!DNL Adobe Experience Platform](Taggar/Datainsamling)** - Hanterar livscykeln, tilläggen, reglerna och publiceringsarbetsflödet för egenskapen för vidarebefordran av händelse

## Foundationsfunktioner

Följande grundläggande funktioner måste finnas för det här användningsmönstret. För varje funktion anger statusen om den vanligtvis är obligatorisk, antas vara förkonfigurerad eller inte tillämplig.

| Foundational Function | Status | Vad måste finnas på plats | Experience League Reference |
| --- | --- | --- | --- |
| Administration och styrning | Obligatoriskt | En sandlåda måste vara aktiv med lämpliga användarroller och behörigheter konfigurerade. Användare som hanterar händelsevidarebefordran behöver behörighet för datainsamling i [!DNL Adobe Admin Console], inklusive behörighet att hantera egenskaper, tillägg och regler för händelsevidarebefordran. | [Översikt över åtkomstkontroll](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Datamodellering och förberedelse | Obligatoriskt | XDM-scheman måste definieras för händelsedata som flödar genom Edge Network. Datastream måste referera till ett giltigt XDM ExperienceEvent-schema så att regler för vidarebefordran av händelser kan komma åt strukturerade fält för filtrering, omvandling och mappning. | [Översikt över XDM-systemet](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home) |
| Datakällor och samling | Obligatoriskt | En datainsamlingsmekanism måste vara aktiv - Web SDK, Mobile SDK eller Edge Network Server API - för att skicka händelser via en konfigurerad datastream. Datastream är det grundläggande routningslagret som kopplar klientsidans samling till händelsevidarebefordran på serversidan. | [Konfigurera datastreams](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure) |
| Konfiguration av identitet och profil | Ej tillämpligt | Vidarebefordran av händelser utförs på råhändelsedata i Edge Network-lagret, innan identitetsupplösning eller profilåtergivning sker. Identitetsnamnutrymmen och sammanfogningsprinciper krävs inte såvida inte de vidarebefordrade händelserna också behöver bidra till kundprofilen i realtid (som är en separat konfiguration för datastream-tjänsten, inte ett problem med händelsevidarebefordran). | |
| Målgruppsdefinition och segmentering | Ej tillämpligt | Vidarebefordran av händelser behandlar enskilda händelser i realtid och utvärderar inte medlemskap för målgruppen. Målgruppsbaserad filtrering ingår inte i funktionskedjan för vidarebefordran av händelser. Om målgruppsbaserad aktivering krävs, se referensplanen för Audience Activation till destinationer. | |

## Stödfunktioner

Följande funktioner förstärker det här användningsmönstret, men behövs inte för att köra kärnan.

| Stödfunktioner | Status | Varför det spelar någon roll | Experience League Reference |
| --- | --- | --- | --- |
| Skapande av beräknat/härlett attribut | Ej tillämpligt | Vidarebefordran av händelser utförs på råhändelsedata, inte på profilnivå beräknade attribut. Beräknade attribut är inte tillgängliga i kontexten för händelsevidarebefordran. | |
| Livscykelhantering för data | Rekommenderad | Om händelsedata också hämtas in till AEP datauppsättningar (via samma datastream) bör datalagringsprinciper (förfallodatum) konfigureras för dessa datauppsättningar för att hantera lagringskostnader och uppfylla gällande bestämmelser. Själva händelsevidarebefordran lagrar inte data, men den parallella inmatningssökvägen för AEP gör det. | [Översikt över livscykelhantering av avancerade data](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| Dataanvändningsetiketter och -tillämpning | Rekommenderad | Regler för vidarebefordran av händelser ger filtrering på fältnivå (vilket gör att du kan exkludera känsliga data från vidarebefordrade nyttolaster), men om du tillämpar etiketter för dataanvändning på underliggande scheman och datauppsättningar säkerställs att styrningsprinciper tillämpas om samma data används för målgruppsaktivering eller personalisering. | [Datastyrningsöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home) |
| Övervakning och observerbarhet | Ingår | Övervakning är nödvändigt för vidarebefordran av händelser. Kontrollpanelen för övervakning av vidarebefordran av händelser ger dig insyn i antal lyckade händelser, felfrekvenser och svarskoder för destinationen. Varningar ska konfigureras för målfel. | [Övervakning av vidarebefordran av händelser](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/monitoring) |
| Rapportering och analys | Rekommenderad | Om vidarebefordrade händelser matar in en analysplattform från tredje part bör du överväga att ansluta samma AEP-händelsedatamängder till CJA för en enhetlig flerkanalsvy. Detta möjliggör jämförelse mellan analyser på Adobe-sidan och på tredjepartssidan. | [CJA - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## Programfunktioner

I den här planen används följande funktioner från programfunktionskatalogen. Funktioner mappas till implementeringsfaser i stället för till numrerade steg.

### [!DNL Adobe Experience Platform] (AEP)

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Datastream-konfiguration | Fas 1: Datastream-konfiguration | Konfigurera en dataström för att ta emot Edge Network-händelser och aktivera tjänsten för vidarebefordran av händelser |
| Egenskapsinställningar för händelsevidarebefordran | Fas 2: Egenskap och tillägg för vidarebefordran av händelser | Skapa en egenskap för vidarebefordring av händelser och installera målspecifika tillägg |
| Händelseregeldefinition | Fas 3: Händelseregeldefinition | Definiera regler som utvärderar inkommande händelsedata och avgör vad som ska vidarebefordras och var |
| Målmappning | Fas 3: Händelseregeldefinition | Mappa händelsedataelement till målspecifika nyttolastformat inuti vidarebefordringsregler |
| Vidarebefordra körning | Fas 4: Publicering och aktivering | Publicera konfigurationen för vidarebefordran av händelser till Edge Network för direktkörning |
| Övervakning | Fas 5: Övervakning och validering | Övervaka antalet lyckade vidarebefordran, felkoder och destinationshälsa |

## Förutsättningar

Kontrollera att följande finns på plats innan implementeringen påbörjas.

- [ ] [!DNL Adobe Experience Platform] licens med tillstånd för Edge Network och händelsevidarebefordran
- [ ] Behörigheter för datainsamling har konfigurerats i [!DNL Adobe Admin Console] (hantera egenskaper, tillägg, regler och publicering för händelsevidarebefordran)
- [ ] Minst en aktiv datainsamlingsmekanism (Web SDK, Mobile SDK eller Server API) skickar händelser via ett datastream
- [ ] XDM ExperienceEvent-schema definierat för händelsedata som samlas in
- [ ] Datastream har skapats och länkats till samlingsmekanismen
- [ ] Det finns tillgängliga autentiseringsuppgifter och dokumentation för målslutpunkten (till exempel [!DNL Meta] Åtkomsttoken för konverteringsgränssnittet, [!DNL Google Analytics] mått-ID, webkros-URL, autentiseringsuppgifter för molnlagring)
- [ ] Förstå händelsemodellen och vilka fält/händelser som varje mål kräver

## Implementeringsalternativ

I det här avsnittet beskrivs de tillgängliga metoderna för att implementera vidarebefordran av händelser och du får vägledning om hur du väljer rätt alternativ.

### Alternativ A: Vidarebefordran av tilläggsbaserade händelser

**Bäst för:** Team som använder målplattformar som stöds ([!DNL Meta], [!DNL Google], [!DNL AWS], [!DNL Azure], [!DNL Snowflake] osv.) som har fördefinierade tillägg för händelsevidarebefordran tillgängliga i datainsamlingskatalogen.

**Så här fungerar det:**

Extension-baserad vidarebefordran av händelser utnyttjar färdiga integreringar som underhålls av Adobe eller tredjepartspartners. Varje tillägg är särskilt utformat för ett specifikt mål och hanterar autentisering, nyttolastformatering och slutpunktskommunikation. Implementeraren installerar tillägget i egenskapen för händelsevidarebefordran, konfigurerar autentiseringsuppgifter och skapar regler som mappar XDM-dataelement till tilläggets åtgärdsfält.

Den här metoden minimerar den anpassade utvecklingen eftersom tillägget abstraherar målets API-krav. API-tillägget [!DNL Meta] Conversions översätter till exempel XDM-handelshändelser till det format som förväntas av [!DNL Meta], vilket hanterar hashning av PII-fält, dedupliceringsparametrar och åtkomsttokenhantering. Tilläggen [!DNL Google Cloud Platform] eller [!DNL AWS] hanterar autentiserings- och nyttolastformatering för respektive molntjänst.

En kompromiss är att tillgängligheten för tillägg avgör vilka destinationer som stöds. Om det inte finns något tillägg för ett målmål måste alternativ B (anpassad webkrok) användas i stället.

**Viktiga överväganden:**

- Tilläggstillgängligheten varierar — kontrollera [tilläggskatalogen för datainsamling](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/overview) innan du planerar
- Tillägg underhålls av Adobe eller partners. Uppdateringar kan medföra förändringar som kräver regeljusteringar
- Vissa tillägg har endast stöd för särskilda händelsetyper eller kräver specifika XDM-fältkopplingar
- Tilläggen hanterar autentisering och autentiseringshantering i sitt konfigurationsgränssnitt

**Fördelar:**

- Snabbast implementering för destinationer som stöds
- Fördefinierad nyttolastformatering minskar mappningsfel
- Autentisering och autentiseringshantering som hanteras av tillägget
- Underhålls och uppdateras av Adobe eller certifierade partners
- Minskad egen kod och lägre underhållsbörda

**Begränsningar:**

- Begränsat till destinationer med tillgängliga tillägg
- Mindre flexibilitet vid anpassning av nyttolasten jämfört med anpassade webhooks
- Tilläggsuppdateringar kan kräva regelomkonfigurering
- Vissa tillägg kanske inte stöder alla mål-API-funktioner

**Experience League:**

- [Katalog för tillägg för vidarebefordran av händelser](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/overview)
- [API-tillägg för Meta Conversion](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/meta/overview)
- [Google Cloud Platform-tillägg](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/google-cloud-platform/overview)
- [AWS-tillägg](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/aws/overview)
- [Snowflake-tillägg](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/snowflake/overview)

### Alternativ B: Vidarebefordran av anpassade webkrokar (Fetch API)

**Passar bäst för:** Team som behöver vidarebefordra händelser till mål utan ett fördefinierat tillägg, eller som kräver fullständig kontroll över HTTP-begärans nyttolast, huvuden och autentiseringsmekanism.

**Så här fungerar det:**

Anpassad webkrosbaserad händelsevidarebefordring använder tillägget [!DNL Adobe Cloud Connector] (ingår som standard) för att göra godtyckliga HTTP-begäranden till alla slutpunkter. Implementeraren definierar dataelement för att extrahera och omvandla värden från den inkommande XDM-händelsen och konfigurerar sedan en regelåtgärd med åtgärdstypen &quot;Make Fetch Call&quot; i molnkopplingen. Den här åtgärden ger fullständig kontroll över HTTP-metoden, URL-adressen, rubrikerna och begärandetexten.

Begärandetexten konstrueras vanligtvis med dataelement och anpassad kod för att formatera nyttolasten enligt målets API-specifikation. Den här metoden stöder alla HTTP-tillgängliga slutpunkter - REST API:er, webbhooks, molnfunktioner eller interna tjänster - vilket gör den till det mest flexibla alternativet.

Avvikelsen är större implementeringsinsatser och fortlöpande underhåll. Implementeraren måste förstå mål-API:t, hantera autentiseringen manuellt (till exempel ange auktoriseringshuvuden, hantera tokenuppdatering) och behålla nyttolastformatet om mål-API:t utvecklas.

**Viktiga överväganden:**

- Kräver förståelse för mål-API-specifikationen (HTTP-metod, URL-struktur, nyttolastformat, autentisering)
- Autentiseringsuppgifter måste hanteras manuellt i dataelement eller hemligheter
- Anpassad kod kan behövas för omformning av nyttolasten (hash, encoding, structure)
- Inga automatiska uppdateringar när mål-API ändras - manuellt underhåll krävs
- Funktionen Secrets i datainsamlingen kan lagra API-nycklar och tokens på ett säkert sätt

**Fördelar:**

- Stöder alla HTTP-tillgängliga slutpunkter - inget tilläggsberoende
- Full kontroll över nyttolast, huvuden och autentisering av begäranden
- Kan vidarebefordra till interna tjänster, anpassade API:er eller nischplattformar
- Aktiverar komplexa nyttolastsomformningar med anpassad kod
- Kan implementera återförsökslogik och felhantering i anpassad kod

**Begränsningar:**

- Högre inledande implementeringsinsats
- Pågående underhållsansvar för nyttolastformat och autentisering
- Ingen fördefinierad felhantering eller rotation av autentiseringsuppgifter - måste implementeras manuellt
- Kräver utvecklarexpertis i HTTP-protokoll och mål-API-specifikationer

**Experience League:**

- [Adobe Cloud Connector-tillägg](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/cloud-connector/overview)
- [Sekretesser vid vidarebefordran av händelser](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/secrets)

### Alternativ C: Hybrid (extensions + custom webhooks)

**Passar bäst för:** Organisationer som vidarebefordrar händelser till flera destinationer där vissa har fördefinierade tillägg och andra kräver anpassad integrering.

**Så här fungerar det:**

Den hybridbaserade metoden kombinerar tilläggsbaserad vidarebefordran för destinationer som stöds med anpassade webkrok-åtgärder för destinationer som saknar tillägg. En enda egenskap för vidarebefordring av händelser innehåller flera regler - vissa som använder tilläggsåtgärder (till exempel [!DNL Meta] API-tillägg för konvertering för annonsspårning) och andra som använder hämtningsåtgärder för Cloud Connector (till exempel vidarebefordran till en intern datasjöslutpunkt).

Det här sättet maximerar täckningen samtidigt som onödig anpassad utveckling minimeras. Varje regel fungerar oberoende av varandra, så tilläggsbaserade regler drar nytta av fördefinierad nyttolastformatering medan anpassade regler behåller full flexibilitet.

**Viktiga överväganden:**

- Egenskapens komplexitet ökar med antalet regler och mål
- Testning och felsökning kan kräva olika metoder för tilläggsbaserade och anpassade regler
- Publiceringsändringar påverkar alla regler i egenskapen - använd bibliotek och miljöer för att hantera ändringar på ett säkert sätt
- Överväg att organisera regler med tydliga namnkonventioner för att skilja på tilläggsbaserade och anpassade åtgärder

**Fördelar:**

- Bästa täckning för olika måltyper
- Utnyttjar färdiga tillägg där det finns tillgängligt, vilket minskar arbetsinsatsen
- Bevarar flexibilitet för anpassade destinationer
- Egenskapen för vidarebefordran av en händelse hanterar all vidarebefordringslogik

**Begränsningar:**

- Komplexare egenskaper med flera regeltyper
- Blandad underhållsmodell - vissa regler uppdateras automatiskt via tillägg, andra kräver manuell uppdatering
- Felsökning kräver att du är bekant med både tilläggskonfigurationer och anpassade mönster för hämtning av anrop

**Experience League:**

- [Översikt över vidarebefordran av händelser](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview)
- [Komma igång med händelsevidarebefordran](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started)

### Jämförelse av alternativ

I följande tabell jämförs de tre implementeringsalternativen.

| Kriterier | Alternativ A: Tilläggsbaserad | Alternativ B: Anpassad webkrok | Alternativ C: Hybrid |
| --- | --- | --- | --- |
| Bäst för | Mål som stöds ([!DNL Meta], [!DNL Google], [!DNL AWS] osv.) | Anpassade slutpunkter, nischplattformar, interna tjänster | Flera mål med blandat stöd |
| Komplex | Lågt | Medium-High | Medelsvåra: |
| Implementeringstid | Dagar | Dagar-veckor | Varierar efter målblandning |
| Flexibilitet | Begränsat till tilläggsfunktioner | Full kontroll | Full kontroll vid behov |
| Underhåll | Låg (tilläggshantering) | Hög (manuell uppladdning) | Blandad |
| Kräver | Tillägget är tillgängligt för målet | Dokumentation för mål-API | Båda, beroende på mål |
| Anpassad kod krävs | Minimal | Måttlig - signifikant | Varierar |

### Välj rätt alternativ

Börja med att inventera målplatserna och kontrollera om det finns fördefinierade tillägg för händelsevidarebefordran för varje mål.

1. **Om alla mål har tillägg** väljer du alternativ A. Detta ger er den snabbaste implementeringen med den lägsta underhållsbördan. Tillägg hanterar autentisering, nyttolastformatering och API-versionshantering.

2. **Om inga mål har tillägg, eller om du behöver fullständig nyttolastkontroll**, väljer du alternativ B. Använd tillägget Cloud Connector för att göra anpassade HTTP-begäranden till alla slutpunkter. Det här är också det rätta valet när du behöver använda komplexa omformningar, anpassade hashningar eller skicka till interna tjänster.

3. **Om du har en blandning av mål som stöds och inte stöds** väljer du alternativ C. Använd tillägg för plattformar som [!DNL Meta], [!DNL Google] och [!DNL AWS] samt anpassade webbhooks för allt annat. Detta är det vanligaste produktionsscenariot för organisationer med olika analys- och reklamstackar.

## Implementeringsfaser

I följande faser beskrivs den kompletta implementeringsprocessen för vidarebefordran av händelser.

### Fas 1: Datastream-konfiguration

**Programfunktion:** AEP: Datastream Configuration

**Så här konfigurerar du:** Ett datastream som tar emot händelser från API-implementeringen för Web SDK, Mobile SDK eller Server och dirigerar dem till Edge Network där reglerna för vidarebefordran av händelser kan bearbeta dem. Om händelsevidarebefordran läggs till i en befintlig datainsamlingsdistribution aktiverar du händelsevidarebefordran på den befintliga datastreamen.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>
>**Beslut: Ny datastream jämfört med befintlig datastream**
>
>Bör du skapa en ny datastream för vidarebefordran av händelser eller aktivera vidarebefordran av händelser för en befintlig datastream?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Använd befintlig datastream | Du har redan Web SDK- eller Server-API som skickar händelser via ett datastream | Det vanligaste scenariot: Vidarebefordran av händelser aktiveras helt enkelt som en extra tjänst på datastream. Inga ändringar på klientsidan behövs. |
>| Skapa nytt datastream | Detta är en ny fältimplementering utan befintlig datainsamling, eller så behöver du ett separat dataflöde för specifika händelsetyper | Kräver att klientsidans SDK-konfiguration pekar på det nya datastream-ID:t. Tillåter isolerad konfiguration. |

>[!NOTE]
>
>**Beslut: Vilka AEP-tjänster som ska aktiveras tillsammans med händelsevidarebefordran**
>
>Datastream kan dirigera händelser till flera AEP-tjänster samtidigt. Vidarebefordran av händelser är en tjänst. Andra (AEP datainmatning, [!DNL Target], [!DNL Analytics]) kan köras parallellt.
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Endast händelsevidarebefordran | Du behöver bara vidarebefordra händelser till andra mål än Adobe och behöver inte data i AEP datamängder | Minimerar databehandlingskostnaderna. Händelserna flödar genom Edge Network till att förmedla regler, men är inte inmatade i AEP datasjön. |
>| Vidarebefordran av händelser + AEP-förtäring | Du behöver samma händelser både i AEP (för profiler, målgrupper, resor) och som vidarebefordras till externa system | De vanligaste för organisationer som använder [!DNL RT-CDP] eller [!DNL AJO] tillsammans med tredjepartsanalyser. Datastream skickar händelser till både AEP datauppsättningar och regler för vidarebefordran av händelser. |
>| Vidarebefordran av flera Adobe-tjänster | Du behöver händelser som dirigeras till AEP, [!DNL Target], [!DNL Analytics] och externa mål samtidigt | Aktivera alla nödvändiga tjänster på datastream. Varje tjänst tar emot händelsen oberoende av varandra. |

**Gränssnittsnavigering:** [!DNL Experience Platform] > Datasamling > Datastreams > Välj eller skapa datastream

**Information om nyckelkonfiguration:**

- Dataströmmen måste ha händelsevidarebefordran aktiverad under dess avancerade inställningar eller tjänstkonfiguration
- Länka händelsevidarebefordringsegenskapen (skapad i fas 2) till datastream
- Bekräfta att det XDM-schema som tilldelats datastream matchar den händelsestruktur som din samlingsmekanism skickar

**Experience League-dokumentation:**

- [Konfigurera datastreams](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Översikt över datastreams](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview)
- [Översikt över vidarebefordran av händelser](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview)

### Fas 2: Egenskaper och tillägg för vidarebefordran av händelser

**Programfunktion:** AEP: Egenskapsinställningar för händelsevidarebefordran

**Så här konfigurerar du:** En egenskap för vidarebefordran av händelser i användargränssnittet för datainsamling, tillsammans med de tillägg som behövs för målmålen. Egenskapen för vidarebefordran av händelser är behållaren för alla regler, dataelement och tillägg som definierar vidarebefordringslogiken på serversidan.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>
>**Beslut: En egenskap kontra flera egenskaper**
>
>Ska du använda en händelsevidarebefordringsegenskap för alla mål eller separata egenskaper?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| En egenskap | De flesta implementeringar; alla regler för vidarebefordran har samma händelseström | Enklare att hantera, ett enda publiceringsarbetsflöde, utvärderas alla regler mot varje händelse. Använd regelvillkor för att filtrera vilka händelser som ska dit. |
>| Flera egenskaper | Du behöver olika team för att hantera olika målintegreringar oberoende av varandra, eller så har du strikta krav på miljöisolering | Varje egenskap har ett eget publiceringsarbetsflöde och kan länkas till olika datastreams. Ökar den administrativa overheadkostnaden men förbättrar gränserna för åtkomstkontroll. |

>[!NOTE]
>
>**Beslut: Vilka tillägg som ska installeras**
>
>Välj tillägg baserat på måldestinationer och valt implementeringsalternativ (A, B eller C ovan).
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Målspecifika tillägg ([!DNL Meta], [!DNL Google], [!DNL AWS] osv.) | Målet har ett fördefinierat tillägg och du vill ha minimal anpassad konfiguration (alternativ A eller C) | Varje tillägg kräver målspecifika autentiseringsuppgifter (API-token, mått-ID, konto-ID). Granska tilläggsdokumentationen för de händelsetyper och obligatoriska fält som stöds. |
>| Endast tillägg för molnanslutning | Alla mål använder anpassade HTTP-begäranden (alternativ B) | Cloud Connector-tillägget installeras som standard. Använd funktionen Secrets för att säkert lagra API-nycklar och autentiseringstoken. |
>| Både målspecifik och Cloud Connector | Du har en blandning av mål som stöds och anpassade mål (alternativ C) | Installera specifika tillägg för mål som stöds och använd Cloud Connector för resten. |

**Gränssnittsnavigering:** [!DNL Experience Platform] > Datainsamling > Händelsevidarebefordran > Skapa egenskap (eller välj befintlig)

**Information om nyckelkonfiguration:**

- Namnge egenskapen med en tydlig konvention (t.ex.&quot;Händelsevidarebefordran - produktion&quot; eller&quot;EF - Analytics &amp; Advertising&quot;)
- Installera tillägget [!DNL Adobe Cloud Connector] (ingår som standard för anpassade webkrok-åtgärder)
- Installera målspecifika tillägg och konfigurera deras autentiseringsuppgifter
- Använd funktionen Secrets (Datainsamling > Händelsevidarebefordran > Secrets) för att på ett säkert sätt lagra API-nycklar, tokens och autentiseringsuppgifter
- Konfigurera miljöer (utveckling, mellanlagring, produktion) för säkra publiceringsarbetsflöden

**Experience League-dokumentation:**

- [Komma igång med händelsevidarebefordran](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started)
- [Katalog för tillägg för vidarebefordran av händelser](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/overview)
- [Sekretesser vid vidarebefordran av händelser](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/secrets)
- [Adobe Cloud Connector-tillägg](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/cloud-connector/overview)

### Fas 3: Händelseregeldefinition

**Programfunktion:** AEP: Händelseregeldefinition, AEP: Målmappning

**Vad du konfigurerar:** Regler som utvärderar inkommande händelsedata, tillämpar villkor för att filtrera vilka händelser som ska vidarebefordras och definierar åtgärder som skickar data till målslutpunkterna. Varje regel består av villkor (när de ska utlösas) och åtgärder (vad som ska göras). Dataelementen extraherar och transformerar värden från XDM-händelsens nyttolast för användning i regelförhållanden och åtgärdskonfigurationer.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>
>**Beslut: Strategi för händelsefiltrering**
>
>Hur avgör du vilka händelser som vidarebefordras till varje mål?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Vidarebefordra alla händelser | Målet behöver en fullständig händelseström (till exempel ett datalager för lagring av Raw-händelser) | Enklast konfiguration - inga villkor krävs. Hög datavolym vid målet. Överväg destinationskostnad och hastighetsbegränsningar. |
>| Filtrera efter händelsetyp | Olika destinationer behöver olika händelsetyper (t.ex. annonsköp, sidvisningar till analyser) | Användningsvillkor baserade på `arc.event.xdm.eventType` eller liknande XDM-fält. Minskar onödiga data på målet. |
>| Filtrera efter händelseattribut | Endast specifika händelser som uppfyller vissa villkor ska vidarebefordras (t.ex. köp över ett tröskelvärde, händelser från specifika sidsökvägar) | Använd dataelementvärden i regelvillkor. Mer komplex men minskar bruset på målet. |

>[!NOTE]
>
>**Beslut: Dataomvandlingsmetod**
>
>Hur ska XDM-händelsedata transformeras för målnyttolasten?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Direkt XDM-fältmappning via dataelement | Målfälten mappas korrekt till XDM-fält (vanligt vid tilläggsbaserad vidarebefordran) | Skapa dataelement som refererar till XDM-sökvägar (till exempel `arc.event.xdm.commerce.order.priceTotal`). Tillägg har ofta ett mappningsgränssnitt. |
>| Anpassad kodomformning | Målet kräver ett nyttolastformat som skiljer sig avsevärt från XDM, eller fälten behöver hash, sammanfogning eller omstrukturering | Använd anpassade kodelement eller anpassad kod på åtgärdsnivå för att omforma nyttolasten. Mer flexibel men svårare att underhålla. |
>| Kombination av dataelement och anpassad kod | Vissa fält mappas direkt medan andra behöver omformas | Använd dataelement för enkla mappningar och anpassade kodblock för komplexa omformningar. Balansera underhållet med flexibilitet. |

>[!NOTE]
>
>**Beslut: PII-hantering i vidarebefordrade data**
>
>Hur ska personligt identifierbar information hanteras före vidarebefordran?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Uteslut PII-fält helt | Målet behöver inte PII och styrningsprinciper begränsar delning | Konfigurera regler för att utelämna PII-fält från den vidarebefordrade nyttolasten. Det enklaste sättet att se på integritetsefterlevnad. |
>| Hash PII-fält före vidarebefordran | Målet kräver hash-kodade identifierare (till exempel: [!DNL Meta] kräver SHA-256-hash-kodad e-post för Conversions API) | Använd anpassade kodelement för att tillämpa SHA-256-hash. Vissa tillägg hanterar automatiskt hashning. |
>| Vidarebefordra PII med kontraktsbaserad grund | Målet har ett databehandlingsavtal och den rättsliga grunden för delning av PII finns | Se till att dataanvändningsetiketter och styrningsprinciper (S3) tillåter delning. Dokumentera den rättsliga grunden. |

**Gränssnittsnavigering:** [!DNL Experience Platform] > Datainsamling > Händelsevidarebefordran > Välj egenskap > Dataelement / Regler

**Information om nyckelkonfiguration:**

- **Dataelement** refererar till den inkommande XDM-händelsen med sökvägsprefixet `arc.event.xdm.` (t.ex. `arc.event.xdm.web.webPageDetails.URL` för sidans URL)
- **Regelvillkor** utvärderar dataelementvärden för att avgöra om regeln ska utlösas
- **Regelåtgärder** använder tilläggsspecifika åtgärder (för alternativ A) eller Cloud Connector-åtgärderna&quot;Make Fetch Call&quot; (för alternativ B) för att skicka data till mål
- Varje regel kan ha flera åtgärder så att en enda händelse kan vidarebefordras till flera mål
- Använd regelordning för att styra utvärderingssekvensen när flera regler kan aktiveras för samma händelse
- Testa reglerna grundligt i utvecklingsmiljön innan publicering till produktion

**Var alternativen skiljer sig:**

**För alternativ A (tilläggsbaserat):**

Konfigurera regelåtgärder med måltilläggets fördefinierade åtgärdstyper. API-tillägget [!DNL Meta] Conversion ger till exempel en&quot;Skicka händelse&quot;-åtgärd där du mappar XDM-fält till [!DNL Meta] händelseparametrar (event_name, event_time, user_data, custom_data). Tillägget hanterar nyttolastsformatering, hash-kodning och API-kommunikation.

**För alternativ B (anpassad webkrok):**

Konfigurera regelåtgärder med åtgärden&quot;Make Fetch Call&quot; i tillägget Cloud Connector. Ange mål-URL, HTTP-metod (vanligtvis POST), begäranrubriker (inklusive auktorisering) och konstruera begärandetexten med dataelement och/eller anpassad kod. Du ansvarar för att matcha mål-API:ts förväntade nyttolastformat exakt.

**För alternativ C (hybrid):**

Skapa separata regler för varje mål. Tilläggsbaserade regler använder tilläggets åtgärdstyper. Anpassade regler använder anrop från hämtning av Cloud Connector. Alla regler finns samtidigt i samma egenskap och utvärderas oberoende av varje inkommande händelse.

**Experience League-dokumentation:**

- [Regler för vidarebefordran av händelser](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview)
- [Dataelement vid händelsevidarebefordran](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/data-elements)
- [Regler i datainsamling](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules)
- [Adobe Cloud Connector-tillägg](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/cloud-connector/overview)

### Fas 4: Publicering och aktivering

**Programfunktion:** AEP: Vidarebefordrar körning

**Så här konfigurerar du:** Publiceringsarbetsflödet som befordrar reglerna för vidarebefordran av händelser från Development till Staging till Production. Vid vidarebefordran av händelser används samma biblioteksbaserade publiceringsmodell som taggar, med miljöer och med artefakter som styr vilken konfiguration som är aktiv på Edge Network.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>
>**Beslut: Utlösare för publiceringsarbetsflöde**
>
>Hur rigorös ska publiceringsprocessen vara?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Direkt till produktion (Utveckling > Produktion) | Små team, lågriskdestinationer eller koncepttestimplementeringar | Snabbare driftsättning men större risk för produktionsproblem. Passar för inledande testning med icke-kritiska destinationer. |
>| Fullständig miljöutveckling (Utveckling > Förproduktion > Produktion) | Produktionsimplementationer med kritiska destinationer (annonseringsplattformar, datalager) | Rekommenderas för alla användningsområden. Med mellanlagring kan du validera med verklig trafik före driftsättning. |

**Gränssnittsnavigering:** [!DNL Experience Platform] > Datainsamling > Händelsevidarebefordran > Välj egenskap > Publiceringsflöde

**Information om nyckelkonfiguration:**

- Skapa ett bibliotek som innehåller alla regler, dataelement och tilläggskonfigurationer som ska publiceras
- Bygg och testa i utvecklingsmiljön först med verktyget Övervakning av händelsespårning för att verifiera att händelser vidarebefordras korrekt
- Befordra till mellanlagring för validering före produktion med livtrafik
- Publicera till produktion endast efter bekräftelse av lyckad händelseleverans i Förproduktion
- Använd biblioteksversionshantering för att spåra ändringar och aktivera återställning vid behov

**Experience League-dokumentation:**

- [Översikt över publicering](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/overview)
- [Bibliotek](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/libraries)
- [Miljöer](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/environments)
- [Bygger](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/builds)

### Fas 5: Övervakning och validering

**Programfunktion:** AEP: Övervakning

**Det här konfigurerar du:** Övervaka instrumentpaneler och verifieringsprocesser för att bekräfta att händelser har vidarebefordrats, diagnostisera fel och upprätthålla den operativa statusen för händelsevidarebefordringsdistributionen.

**Beslutspunkter i den här fasen:**

>[!NOTE]
>
>**Beslut: Övervaka djup**
>
>Hur djupt bör vidarebefordran av händelser övervakas?
>
>| Alternativ | Välj när | Överväganden |
>| --- | --- | --- |
>| Endast kontrollpanelen för övervakning av händelsevidarebefordran | Grundläggande övervakning för icke-kritiska destinationer eller inledande driftsättningar | Ger en översikt över lyckade/misslyckade åtgärder och målsvarskoder. Tillräckligt för de flesta implementeringar. |
>| Övervakning av vidarebefordran av händelser + validering på målsidan | Viktiga destinationer där datainfo direkt påverkar affärsresultatet (annonsspårning, datalagerintegritet) | Korsreferensstatistik för vidarebefordran på Adobe-sidan med bekräftelse av mottagningskvitto på mottagarsidan. Fångar kantfall där målet accepterar begäran men inte bearbetar data. |
>| Full observerbarhet (händelsevidarebefordringsövervakning + målvalidering + AEP Alerts) | Storskaliga installationer med SLA krav på dataleverans | Kombinera övervakning av vidarebefordran av händelser med AEP plattformsaviseringar för en heltäckande bild. Konfigurera varningsmeddelanden för feltrösklar vid vidarebefordran. |

**Gränssnittsnavigering:** [!DNL Experience Platform] > Datainsamling > Vidarebefordra händelser > Välj egenskap > Övervakning

**Information om nyckelkonfiguration:**

- Verktyget Övervakning av händelsespårning visar händelsenolym, antal lyckade åtgärder och felinformation per regel och per mål
- Övervaka HTTP-svarskoder från mål - 2xx indikerar lyckade, 4xx indikerar klientfel (trolig nyttolast eller autentiseringsproblem), 5xx indikerar fel på målsidan
- Använd webbläsartillägget [!DNL Adobe Experience Platform Debugger] för att inspektera händelser som flödar från klienten via Edge Network till regler för händelsevidarebefordran
- Validera från början till slut genom att kontrollera att vidarebefordrade händelser visas i målsystemet (kontrollera till exempel [!DNL Google Analytics] realtidsrapporter, [!DNL Meta] händelsehanterare eller datalagertabeller)
- Ställ in AEP Alerts för käll- och dataflödesfel för att fånga upp problem som skulle förhindra händelser från att nå regler för händelsevidarebefordran

**Experience League-dokumentation:**

- [Övervakning av vidarebefordran av händelser](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/monitoring)
- [Adobe Experience Platform Debugger](https://experienceleague.adobe.com/en/docs/experience-platform/debugger/home)
- [Översikt över aviseringar](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)

## Implementeringsöverväganden

Detta avsnitt behandlar skyddsförslag, vanliga fallgropar, bästa praxis och beslut om kompromisser som ska beaktas under hela implementeringen.

### Gardrutor och begränsningar

- Händelsevidarebefordring bearbetar händelser i realtid på Edge Network - det finns inget batchläge och det finns ingen återförsökskö för misslyckade leveranser som standard
- Edge Network hastighetsbegränsningar gäller för den totala händelsevolymen som bearbetas per datastream - [Edge Network skyddsräcken](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/guardrails)
- Regler för vidarebefordran av händelser kör serversidan och kan inte komma åt resurser på klientsidan (DOM, cookies, localStorage)
- Anpassad kod i regler för vidarebefordran av händelser körs i en sandlådemiljö - alla webbläsar-API:er är inte tillgängliga
- Hämtningsanropet för Cloud Connector har timeout-gränser - mål som svarar långsamt kan orsaka timeout
- Vidarebefordran av händelser sker enligt Edge Network geografiska dirigering - händelserna behandlas på den närmaste Edge-platsen
- Största nyttolaststorlek för vidarebefordrade begäranden styrs av Edge Network-begränsningar

### Vanliga fallgropar

- **Om du vidarebefordrar alla XDM-fält utan filtrering:** Om du skickar hela XDM-händelsenyttolasten till ett mål som bara behöver ett fåtal fält går bandbredd förlorad, destinationskostnaderna ökar och PII-filen kan delas oavsiktligt. Mappa alltid bara de obligatoriska fälten i vidarebefordringsreglerna.

- **Det går inte att skydda autentiseringsuppgifter med hemligheter:** En säkerhetsrisk uppstår om API-nycklar eller token kodas i dataelement eller regelåtgärder. Använd alltid funktionen Datainsamlingshemlighet för att lagra inloggningsuppgifter säkert och referera till dem i regler.

- **Ångrar målhastighetsbegränsningar:** Tredjepartsmål har ofta API-hastighetsbegränsningar. Om din händelsvolym överskrider en måls kapacitet kan händelser tas bort eller så kan API-åtkomsten strykas. Granska måldokumentationen för hastighetsbegränsningar och implementera filtrering för att minska händelsemängden vid behov.

- **Publicering direkt till produktion utan mellanlagring:** Om du hoppar över mellanlagringsmiljön upptäcks endast fel i produktionen, vilket kan orsaka dataförlust på kritiska destinationer. Validera alltid i mellanlagring med direkttrafik först.

- **Övervakar inte HTTP-svarskoder:** En regel som utlöses utan fel garanterar inte att målplatsen har bearbetat data. Övervaka målsvarskoder (som finns i verktyget Övervakning av händelsespårning) och utforska eventuella svar som inte är 2xx.

- **Felkonfigurerade XDM-sökvägsreferenser:** Dataelement använder prefixet `arc.event.xdm.` för att referera till inkommande händelsefält. En felaktig sökväg (till exempel om en nivå av kapsling saknas) ger i tysthet null-värden i stället för att utlösa fel. Validera dataelementvärden med Felsökning.

### God praxis

- **Börja med ett enda mål och expandera gradvis** - Verifiera händelsesändning från slutpunkt till slutpunkt med ett mål innan du lägger till ytterligare regler och mål. Detta förenklar felsökningen och skapar förtroende för infrastrukturen.

- **Använd konsekventa namnkonventioner** - Namnge dataelement, regler och bibliotek med en tydlig konvention som identifierar mål, händelsetyp och miljö (t.ex. &quot;Regel: Meta - Inköpshändelser&quot;, &quot;DE: Ordersumma&quot;).

- **Implementera filtrering på fältnivå för sekretess** - Även om målplatsen gör anspråk på att hantera PII korrekt bör du använda filtrering på serversidan för att ta bort eller hash-koda känsliga fält innan de lämnar Edge Network. Det här är den främsta styrningsfördelen med händelsevidarebefordran över taggar på klientsidan.

- **Version av dina konfigurationer** - Använd arbetsflödet för bibliotekspublicering för att behålla versionshanterade ögonblicksbilder av konfigurationen för händelsevidarebefordran. Dokumentera vad varje biblioteksversion innehåller för revision och återställning.

- **Testa med plattformsfelsökaren** - Tillägget [!DNL Adobe Experience Platform Debugger] ger synlighet i händelselivscykeln från SDK på klientsidan genom Edge Network-bearbetning. Använd det under utveckling och felsökning.

- **Justera regler för vidarebefordran av händelser mot XDM-schemats design** - Om vidarebefordran av händelser är ett känt krav ska du utforma XDM-schemat och händelsetaxonomin så att de innehåller fälten som destinationen behöver. Det är mer störande att anpassa schemaändringar efter distributionen.

### Avvecklingsbeslut

>[!NOTE]
>
>**Brytfrekvens: Enkelt tillägg jämfört med flexibilitet för webkrok**
>
>Färdiga tillägg minimerar implementeringsinsatser och underhåll, men de begränsar dig till tilläggets funktioner och nyttolastformat som stöds. Anpassade webhooks ger full kontroll men kräver mer utveckling och kontinuerligt underhåll.
>
>- **Tilläggsbaserade (alternativ A) prioriterar:** Snabba upp time-to-market, minskat utvecklarberoende, automatisk autentiseringshantering, lägre underhållsnivå
>- **Webkrokbaserad (alternativ B) prioriterar:** Full nyttolastkontroll, stöd för alla HTTP-slutpunkter, anpassad transformeringslogik, oberoende av versionscykler för tillägg
>- **Rekommendation:** Använd tillägg när det är tillgängligt och tillräckligt. Gå bara tillbaka till anpassade webhooks när målet saknar ett tillägg eller när tillägget inte stöder de specifika API-funktioner du behöver. Det hybrida tillvägagångssättet (alternativ C) är det pragmatiska valet för de flesta organisationer.

>[!NOTE]
>
>**Avvikelse: Vidarebefordra alla händelser kontra selektiv filtrering**
>
>Om du vidarebefordrar alla händelser till en destination säkerställs fullständigheten, men datavolymen, destinationskostnaderna och sekretessexponeringen ökar. Selektiv filtrering minskar bruset men riskerar att missa händelser som kan vara värdefulla.
>
>- **Vidarebefordra alla händelser till förmån för:** Datakompatibilitet, enkelhet, framtida korrektur (data finns där om det behövs senare)
>- **Selektiv filtrering prioriterar:** Kostnadseffektivitet, minskad sekretessrisk, renare måldata, efterlevnad av dataminimeringsprinciper
>- **Rekommendation:** Välj selektiv filtrering baserat på händelsetyp och affärsrelevans som standard. Vidarebefordra endast de händelser och fält som varje mål verkligen behöver. Detta är förenligt med dataminimeringsprinciperna (GDPR-artikel 5) och minskar driftskostnaderna.

>[!NOTE]
>
>**Avvikelse: En egenskap kontra flera egenskaper**
>
>En enda egenskap för vidarebefordran av händelser är enklare att hantera, men innebär att alla regler har ett gemensamt publiceringsarbetsflöde. Flera egenskaper ger isolering men ökar hanteringskostnaderna.
>
>- **Enstaka egenskap prioriterar:** Enkelhet, enhetlig publicering, delade dataelement, enklare felsökning
>- **Flera egenskaper prioriterar:** Åtkomstkontroll på teamnivå, oberoende publiceringskoncadenser, isolering av målfel
>- **Rekommendation:** Börja med en enda egenskap för de flesta implementeringar. Dela bara upp i flera olika egenskaper om olika team har olika målintegreringar och behöver oberoende releasecykler, eller om lagstadgade krav kräver strikt isolering mellan dataflöden.

## Relaterad dokumentation

Följande resurser innehåller mer information om de ämnen som behandlas i den här handboken.

**Vidarebefordran av händelser**

- [Översikt över vidarebefordran av händelser](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview)
- [Komma igång med händelsevidarebefordran](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started)
- [Övervakning av vidarebefordran av händelser](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/monitoring)
- [Sekretesser vid vidarebefordran av händelser](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/secrets)

**Tillägg för vidarebefordran av händelser**

- [Katalog för tillägg på serversidan](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/overview)
- [Adobe Cloud Connector-tillägg](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/cloud-connector/overview)
- [API-tillägg för Meta Conversion](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/meta/overview)
- [Google Cloud Platform-tillägg](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/google-cloud-platform/overview)
- [AWS-tillägg](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/aws/overview)
- [Snowflake-tillägg](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/snowflake/overview)
- [Google Ads Enhanced Conversion Extension](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/google-ads-enhanced-conversions/overview)
- [Mailchimp-tillägg](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/mailchimp/overview)

**Datainsamling och Edge Network**

- [Konfigurera datastreams](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Översikt över datastreams](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview)
- [SDK - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Edge Network Server API - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)
- [Översikt över taggar](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)
