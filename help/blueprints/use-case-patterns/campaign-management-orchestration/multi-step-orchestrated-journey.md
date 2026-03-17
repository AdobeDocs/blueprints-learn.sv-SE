---
title: Flerstegsdirigerad resa
description: Lär dig hur du guidar en profil genom en förgreningsprocess med flera kontaktytor, väntetider, villkor och flera meddelandeåtgärder över tid.
solution: Journey Optimizer, Real-Time Customer Data Platform
source-git-commit: b2e496eb521fc3dd3290fccdd9a8203384934b88
workflow-type: tm+mt
source-wordcount: '8173'
ht-degree: 0%

---


# Samlad resa i flera steg

Den här guiden innehåller en omfattande implementeringsplan för att skapa flerstegsdirigerade resor med [!DNL Adobe Journey Optimizer] (AJO) och [!DNL Real-Time Customer Data Platform] (RT-CDP). Det är utformat för lösningsarkitekter, marknadsföringsteknologer och implementeringstekniker som behöver orkestrera förgrenade kundresor med flera kontaktytor som levererar flera budskap över tid.

Den innehåller alla genomförbara implementeringsalternativ, beslutsöverväganden vid varje konfigurationspunkt och länkar till [!DNL Adobe Experience League]-dokumentation. Använd den här guiden för att planera, konfigurera och validera implementeringen av din resa i flera steg.

## Använd ärendeöversikt

Flerstegsdirigerade resor åtgärdar affärsscenarier där ett enda meddelande inte räcker till för att uppnå önskat kundresultat. I stället för att skicka en gång guidar resan varje profil genom en sekvens av kontaktytor - e-post, SMS-meddelanden, push-meddelanden eller meddelanden i appen - som fördelas över dagar eller veckor, med förgreningslogik som anpassar sökvägen baserat på profilattribut, beteendesignaler eller händelsedata.

Dessa resor är det mest komplexa kampanjmönstret i AJO. De kombinerar målgruppsbaserad eller händelsebaserad post med en arbetsyta med actionnoder (meddelanden), villkorsnoder (förgreningslogik), väntenoder (tidsfördröjningar) och avslutningskriterier (konverteringshändelser eller tidsgränser). Varje profil går igenom resan självständigt i sin egen takt och tar emot relevant innehåll i varje steg.

Det här mönstret underbygger de enklare mönstren - batchaktivering av utgående meddelanden för kampanjer med en sändning och händelseutlösta meddelanden för svar med en händelse. Använd det här mönstret när användningsfallet kräver att du vårdar en profil genom flera interaktioner över tiden.

## Viktiga verksamhetsmål

Följande affärsmål stöds av det här användningsmönstret.

### få nöjdare kunder

Håll befintliga kunder engagerade och förnyade genom värdestyrda upplevelser och kontinuerlig relationshantering.

**KPI:er:** Kvarhållning, kundens livstidsvärde, engagemang

[Läs mer om hur ni kan förbättra kundlojaliteten](/help/blueprints/business-objectives/customer-experience/improve-customer-retention.md)

### Förbättra kundintroduktionen

Snabba upp time-to-value för nya kunder med smidiga, personaliserade välkomstupplevelser och aktiveringsresor.

**KPI:er:** engagemang, lagring, konverteringsgrader

[Läs mer om hur man förbättrar kundintroduktionen](/help/blueprints/business-objectives/customer-experience/improve-customer-onboarding.md)

### Återengagera vilande kunder

Få tillbaka inaktiva eller dolda kunder med riktade reaktiveringskampanjer baserade på beteendesignaler.

**KPI:er:** engagemang, lagring, konverteringsgrader

### Återvinn övergivna varukorgar och resor

Engagera användare som slutade på grund av köp, ansökningar eller registreringar med skräddarsydda uppföljningar i rätt tid.

**KPI:er:** Konverteringsgrader, inkrementell intäkt, engagemang

[Läs mer om hur man återställer övergivna varukorgar och resor](/help/blueprints/business-objectives/customer-experience/recover-abandoned-carts-journeys.md)

## Exempel på taktiska användningsfall

Följande scenarier illustrerar vanliga applikationer för det flerstegsorienterade resemönstret.

- **Serien för kundintroduktion** - Välkomstmeddelande, följt av funktionsutbildning, och sedan en uppmaning om aktivering under de första 14 dagarna efter registreringen
- **Ångra-engagemangskampanj** - Ett påminnelsemejl, sedan ett incitamentserbjudande och sedan ett slutligt meddelande för förfallna kunder under tre veckor
- **Förmånens milstolpe-resa** - Meddelande om uppgradering av nivån följt av ett exklusivt erbjudande, och sedan en påminnelse om förnyelse när medlemskapsförnyelsen närmar sig
- **Win-back-sekvens** -&quot;Vi saknar dig&quot;, ett rabatterbjudande via e-post och sedan en slutgiltig SMS-påminnelse för annullerade köpare
- **Produktintroduktionsresa** - Välkomna till testversionen, användningstips och sedan ett uppgraderingsmeddelande allt eftersom testperioden fortskrider
- **Sekvens för förnyelse av prenumeration** - 30-dagars meddelande, 7-dagars påminnelse och sedan ett meddelande om att prenumerationen kan förnyas
- **Vård efter köp** - Tack för ditt e-postmeddelande, användarhandbok, korsförsäljningsrekommendation och sedan en granskningsförfrågan över 30 dagar efter köp

## Nyckeltal för prestanda

Använd följande nyckeltal för att mäta effektiviteten i er flerstegssamordnade implementering av resor.

| KPI | Beskrivning | Mätningsmetod |
| --- | --- | --- |
| Färdavslut | Procentandel profiler som slutför hela resan utan tidig utgång | Reserapport: Avslutad (slutförd) / Angiven |
| Stegkonverteringsgrad | Procentandel profiler som går från ett steg till nästa | Mätvärden per nod i reserapporten |
| Kanalengagemang | Öppetfrekvenser, klickfrekvens och svarsfrekvens vid varje kontaktyta | Mätvärden för leverans och engagemang per meddelande |
| Konverteringshastighet för avslutsvillkor | Procentandel av profiler som utlöser händelsen exit (till exempel köp, registrering) före timeout för resan | Antal träff/totalt antal angivna för avslutningskriterier |
| Tid till konvertering | Genomsnittlig varaktighet från reseinträde till utträdeshändelse | Reseanalys: tidsstämpel för post till tidstämpel för konverteringshändelse |
| Avlämningsfrekvens för resa | Procentandel profiler som slutar engagera i varje steg (bortfallsanalys) | CJA utfallsvisualisering över hela kundresan |
| Kvarhållande/återengagemang | Procentandel målprofiler som återgår till aktiv status | Beteendeanalys efter resan i CJA |

## Använd skiftlägesmönster

**Samlad resa i flera steg**

Vägled en profil genom en förgreningsprocess med flera kontaktytor, väntetider, villkor och flera meddelandeåtgärder över tid.

**Funktionskedja:** Målgruppsutvärdering > Resekörning (flera noder) > Villkorsförgreningar > Meddelandeleverans (xN) > Avsluta villkor > Rapportering

## Tillämpningar

Följande program används för att implementera det här användningsmönstret.

- **[!DNL Adobe Journey Optimizer] (AJO)** - Journey-orkestreringsmotor, meddelanderedigering, kanalkonfiguration, innehållsexperimenterande, frekvens- och konflikthantering samt rapportering
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** - Målgruppsutvärdering och definition för målgrupper för kundinträde, profildata för personalisering och villkorsförgreningar
- **[!DNL Adobe Experience Platform] (AEP)** - Profilarkiv, identitetstjänst, inmatning av händelsedata och grundläggande datainfrastruktur

## Foundationsfunktioner

Följande grundläggande funktioner måste finnas för det här användningsmönstret. För varje funktion anger statusen om den vanligtvis är obligatorisk, antas vara förkonfigurerad eller inte tillämplig.

| Funktionen Foundation | Status | Vad måste finnas på plats | Experience League referens |
| --- | --- | --- | --- |
| Administration och styrning | Antagen på plats | AJO sandlåda med behörighet att skapa och publicera resor. Kanalytor för alla kanaler som används under resan måste konfigureras. Användarna måste ha rätt roller (Marketer, Resechef) med rätt behörighet för resan och kampanjen. | [Översikt över sandlådor](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/home), [Översikt över åtkomstkontroll](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| Datamodellering och förberedelse | Obligatoriskt | XDM-profilschema med attribut som används för villkorsförgrening och personalisering i flera meddelanden (t.ex. lojalitetsnivå, produktintresse, engagemangsmätning). Upplev händelsescheman för konverteringshändelser som styr avslutningskriterier och villkorsutvärdering (t.ex. köphändelser, formuläröverföringar). | [Systemöversikt för XDM](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/home), [Grundläggande om schemakomposition](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| Datakällor och samling | Antagen på plats | Händelseströmning måste vara aktiv om avslutningskriterierna eller avslutningsvillkoren är beroende av händelser i realtid (t.ex. köphändelse för att avsluta resan). Batchåtkomster för profilattribut som används vid förgreningar. SDK eller serversides-API för beteendehändelseinsamling. | [Översikt över direktuppspelning &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/streaming/overview), [Översikt över källor](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home) |
| Konfiguration av identitet och profil | Antagen på plats | Profiler måste kunna matchas i alla kanaler som används under resan (e-post, SMS, push). Enhetsidentiteten måste vara konfigurerad om resan omfattar både webb- och mobilkontaktytor. Sammanslagningsprincipen måste konfigureras för sandlådan. | [Översikt över identitetstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/home), [Översikt över sammanslagningsprinciper](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| Målgruppsdefinition och segmentering | Obligatoriskt | Tävlingsdeltagare måste definieras för målgruppsresor. Segment kan också användas i villkorsnoder för förgreningar. Utvärderingsmetoden (batch- eller direktuppspelning) måste överensstämma med kraven för reseanmälan. | [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/home), [Användargränssnittsguide för segmentbyggaren](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/ui/segment-builder) |

## Stödfunktioner

Följande funktioner förstärker det här användningsmönstret, men behövs inte för att köra kärnan.

| Stödfunktioner | Status | Varför det spelar någon roll | Experience League referens |
| --- | --- | --- | --- |
| Skapande av beräknat/härlett attribut | Rekommenderad | Beräknade attribut som engagemangsmusik, dagar sedan senaste aktivitet eller livstidsvärde förbättrar logiken för villkorsförgreningar, vilket möjliggör smartare beslut om kundresan. | [Översikt över beräknade attribut](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/computed-attributes/overview) |
| Livscykelhantering för data | Rekommenderad | Datalagring av resthändelser bör konfigureras med datauppsättningens förfalloprinciper för att hantera lagring och följa regler för datalagring. Samtycke säkerställer att endast profiler med valfri notation tar emot meddelanden vid varje kanalkontaktyta. | [Översikt över livscykelhantering av avancerade data](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home), [Giltighetsperioder för datauppsättningar](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration) |
| Dataanvändningsetiketter och -tillämpning | Rekommenderad | Styrningsetiketter säkerställer att personaliseringen fungerar som den ska över flera kontaktytor, särskilt när resor använder PII eller känsliga data för personalisering över flera kanaler. | [Översikt över datastyrning](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/home), [Översikt över etiketter för dataanvändning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/labels/overview) |
| Övervakning och observerbarhet | Ingår | Övervakning av körning på resande varningar om misslyckade bearbetningar, flaskhalsar för profilregistrering och leveransproblem. Oumbärlig för produktionsresor där förseningar eller fel påverkar kundupplevelsen. | [Aviseringsöversikt](https://experienceleague.adobe.com/sv/docs/experience-platform/observability/alerts/overview), [Översikt över Insikter i observabilitet](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| Rapportering och analys | Ingår | CJA funnel och bortfallsanalys under hela resan ger djupare insikter än enbart AJO-rapporter. Möjliggör stegvis konverteringsanalys, kohortjämförelse och reseoptimering. | [CJA - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-overview/cja-overview), [Analysis Workspace - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/home) |

## Programfunktioner

I den här planen används följande funktioner från programfunktionskatalogen. Funktioner mappas till implementeringsfaser i stället för till numrerade steg.

### [!DNL Journey Optimizer] (AJO)

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Kanalkonfiguration | Fas 1: Kanalinställning | Konfigurera kanalytor (e-post, SMS, push) för varje kontaktyta i ett meddelande under resan |
| Redigering av meddelanden | Fas 2: Skapa meddelandeinnehåll | Skapa meddelandeinnehåll med personalisering, dynamiskt innehåll och mallar för varje kundåtgärdsnod |
| Journey Orchestration | Fas 3: Resedesign och aktivering | Utforma arbetsytan för flerstegsresor med noder för start, åtgärd, villkor, väntan och avslutning; testa och publicera |
| Frekvens och affärsregler | Fas 4: Styrning och optimering | Konfigurera frekvensgränser för att förhindra att fler meddelanden visas över resans kontaktytor och andra samtidiga kampanjer |
| Konflikt- och prioritetshantering | Fas 4: Styrning och optimering | Tilldela prioriteringspoäng och konfigurera konfliktidentifiering för resor som konkurrerar med annan aktiv kommunikation |
| Experimentera med innehåll | Fas 4: Styrning och optimering | Kör A/B-tester på meddelandeinnehåll i åtgärdsnoder för resan för att optimera prestandan |
| Rapportering och prestandaanalys | Fas 5: Rapportering och övervakning | Övervaka reseutförande, leveransstatistik per steg och engagemangsprestanda |

### [!DNL Real-Time CDP] (RT-CDP)

| Funktion | Implementeringsfas | Beskrivning |
| --- | --- | --- |
| Målgruppsutvärdering | Fas 1: Kanalinställning (nödvändig) | Definiera och utvärdera målgruppen för målgruppsresor; definiera villkorsmålgrupper för förgreningar |
| Verkställande av samtycke och styrning | Fas 4: Styrning och optimering | Använd samtyckesinställningar och dataanvändningspolicyer för åtgärder för att skicka meddelanden på resan |

## Förutsättningar

Slutför följande krav innan du påbörjar implementeringen.

- [ ] AJO-sandlådan har etablerats med behörighet att skapa och publicera resor
- [ ] Minst en kanalyta (e-post, SMS eller push) har konfigurerats och är aktiv
- [ ]-profilschemat innehåller attribut som behövs för förgrening av villkor och anpassning
- [ ] Experience Event-schemat har konfigurerats för konverteringshändelser som används i avslutningskriterier
- [ ] Händelseströmning är aktiv för realtidshändelser som används i avslutsvillkor eller händelseutlösta poster
- [ ] Identitetsnamnutrymmen och sammanfogningsprinciper har konfigurerats för upplösning av flerkanalsprofiler
- [ ] Innehållsresurser (bilder, kopia, CTA) förbereds för varje kontaktyta för meddelandet
- [ ] målgrupp definieras och utvärderas (för målgruppsläsare)
- [ ] Utlösande händelseschema har konfigurerats (för händelseutlösta resor)
- [ ] testprofiler är tillgängliga för validering av testläge för resan
- [ ] Supprestionslistan granskas och är uppdaterad för alla kanaler som används

## Implementeringsalternativ

Granska följande alternativ för att fastställa den bästa metoden för en flerstegsdirigerad resa.

### Alternativ A: Målgruppsläsad, iscensatt resa

**Bäst för:** Tidsbaserade vårdsekvenser där en känd målgrupp kommer in på resan och utvecklas via schemalagda kontaktytor - introduktionsserier, förnyelsesekvenser, återengagemangsdroppar, milstolpar för lojalitet.

**Så här fungerar det:**

En målgrupp läses vid reseanmälan, antingen som en engångsläsning eller enligt ett återkommande schema. Alla kvalificerande profiler går in på resan samtidigt och går sedan igenom arbetsytan i sin egen takt, styrt av väntetider och villkorsutvärderingar. Varje profils väg genom resan är självständig - vissa kan ta den &quot;engagerade&quot; grenen medan andra tar den &quot;ej engagerade&quot; grenen baserat på deras beteende eller attribut.

Publiken utvärderas när aktiviteten Läs publik körs. För återkommande resor omprövas publiken för varje återkommande resa, och nya kvalificerande profiler går in på resan medan profiler som redan ingår i resan fortsätter. Den här metoden ger förutsägbar tidsram för inträde och passar bra för schemalagda livscykelprogram.

**Viktiga överväganden:**

- Målgruppen måste definieras och utvärderas innan resan aktiveras
- Återkommande läsning ger nya kvalificerare möjlighet att gå in i varje cykel
- Profilerna i resan läses inte om, bara nya kvalificerare skriver in vid efterföljande läsningar
- Väntestegen har en minsta varaktighet på 1 timme för målgruppsläsningar

**Fördelar:**

- Förutsägbar tidsåtgång för inmatning i linje med affärsscheman
- Stöder stora målgruppsvolymer (upp till 20 000 profiler per sekund standardbegränsning)
- Enkelt att testa och övervaka med kända målgrupper
- Kan schemaläggas för återkommande inmatning (varje dag, varje vecka, varje månad)

**Begränsningar:**

- Posten är batchbaserad, inte i realtid - profiler anges vid den schemalagda lästiden, inte när de kvalificerar sig
- Passar inte för beteendeinitierade sekvenser som kräver omedelbar respons
- Målgruppsändringar mellan läsningar återspeglas inte för profiler som redan är på resan

**Experience League:**

- [Läs målgruppsaktivitet](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Skapa en resa](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)

### Alternativ B: Händelseutlöst iscensatt resa

**Passar bäst för:** Beteendeinitierade sekvenser där en realtidshändelse startar resan - eskalering av kundvagnsavbrott, näring efter köp, milstolpe-utlöst lojalitetsresa, testaktiveringssekvenser.

**Så här fungerar det:**

En enhetshändelse (t.ex. ett inköp, övergivna varukorgar, inskickade formulär eller appinstallation) utlöser reseregistrering för enskilda profiler i realtid. När händelsen tas emot tar profilen sig in på resan och fortsätter sedan genom sekvensen av kontaktytor med villkor, väntetider och förgreningar. Med den här metoden kombineras omedelbar händelseutlöst meddelanden med flerstegssamordning av en hel resa.

Den utlösande händelsen måste konfigureras som en resehändelse med dess schema och villkor definierade. Resan lyssnar kontinuerligt efter händelsen och anger profiler en i taget när händelserna anländer. Efterföljande kundnoder kan utvärdera profilens svar för att avgöra vilken gren som ska följas.

**Viktiga överväganden:**

- Kräver att händelseströmning i realtid är aktiv
- Händelseschema och villkor måste vara exakt konfigurerade för att undvika falska utlösare
- Regler för återinträde är viktiga - avgöra om en profil kan ange om händelsen utlöses igen
- Stöder upp till 5 000 händelser per sekund per sandlåda

**Fördelar:**

- Inträde i realtid baserat på kundbeteende - ytterst kontextuellt
- Varje profil anges oberoende när händelsen inträffar, inte enligt ett schema
- Naturligt lämpligt för beteendebaserade svarssekvenser (övergivna varukorgar, efterköp)
- Kan kombineras med profildata för personaliserad förgrening efter registrering

**Begränsningar:**

- Kräver att infrastruktur för direktuppspelningshändelser finns på plats
- Högre komplexitet i konfiguration och testning av händelseschema
- Varje händelse anger en profil - passar inte för massvis målgruppsaktivering
- Felsökning kräver spårning av enskilda profilresor

**Experience League:**

- [Allmänna händelser](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Elevkvalificeringshändelser](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)

### Alternativ C: Flerkanalsdirigerad resa

**Bäst för:** Flerkanalssekvenser som använder olika kanaler vid varje kontaktyta - e-post, sedan SMS, push-eskalering eller e-post plus komplementära meddelanden i appen. Kan använda antingen målgruppsläsare eller händelseutlösande post.

**Så här fungerar det:**

Det här alternativet utökar alternativ A eller Alternativ B genom att införliva flera meddelandekanaler inom samma resa. Varje åtgärdsnod på resan kan ha en egen kanal (e-post, SMS, push, in-app eller webb) som kräver en separat kanal för varje kanal. Resedesignern väljer lämplig kanal i varje steg och aktiverar eskaleringsmönster (till exempel e-post först, sedan SMS om det inte finns något engagemang) eller komplementära mönster (till exempel e-post med förstärkning i appen).

Flerkanalsresor kräver kanalytor för varje kanal som används och måste ta hänsyn till kanalspecifik personalisering, teckenbegränsningar och krav på deltagande. Villkorsnoder kan kontrollera interaktion med tidigare meddelanden (till exempel&quot;öppnad e-post?&quot;) som ett förgreningsvillkor) för att bestämma nästa kanal.

**Viktiga överväganden:**

- Kräver aktiva kanalytor för varje kanal som används i resan
- Varje kanal har olika personaliseringsfunktioner och innehållsbegränsningar
- Samtycket måste verifieras per kanal - en profil kan väljas för e-post men inte för SMS
- Kanalspecifika frekvenstak bör konfigureras för att förhindra att meddelanden skickas över olika kanaler

**Fördelar:**

- Maximera räckvidden genom att engagera profiler i de kanaler de föredrar
- Aktiverar eskaleringsstrategier för profiler som inte svarar
- Stöder komplementära meddelanden över flera kanaler för förstärkning
- Mest sofistikerade kundupplevelser är möjliga

**Begränsningar:**

- Högsta komplexitet i implementeringen - kräver konfiguration för varje kanal
- Innehållet måste skapas för varje kanal vid varje kontaktyta
- Hantering av samtycke och frekvens blir mer komplicerat över alla kanaler
- Testning kräver validering över alla kanalytor

**Experience League:**

- [Konfigurera SMS-kanal](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Konfigurera kanal för push-meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Jämförelse av alternativ

I följande tabell jämförs de tre implementeringsalternativen över de viktigaste kriterierna.

| Kriterier | Alternativ A: Målgruppsläsare | Alternativ B: Händelseutlösta | Alternativ C: Flerkanaligt |
| --- | --- | --- | --- |
| Bäst för | Schemalagda livscyklprogram, vårdsserier | Beteendesvarssekvenser, övergivna varukorgar | Eskalering över flera kanaler, kompletterande meddelanden |
| Tidsinställning | Schemalagd (batch) | Realtid (händelsestyrd) | Antingen schemalagd eller realtid |
| Komplex | Medelsvåra: | Medium-High | Högt |
| Ingångsvolym | Upp till 20 000 profiler/sek | Upp till 5 000 händelser/sek | Samma som underliggande postmetod |
| Kanalomfång | En eller flera kanaler | En eller flera kanaler | Flera kanaler krävs |
| Kräver | Definierad målgrupp, utvärderingsschema | Infrastruktur för direktuppspelningshändelser | Kanalytor för varje kanal |
| Realtidssvar | Nej - batchregistrering | Ja - direkt vid händelse | Beroende på anmälningsmetod |

### Välj rätt alternativ

Använd följande beslutsflöde för att välja rätt implementeringsmetod:

1. **Har resan initierats av ett kundbeteende eller en händelse?** Om ja, välj **Alternativ B** (händelseutlöst). Om resan initieras av en schemalagd målgruppsläsare väljer du **Alternativ A** (Audience-Read).

2. **Använder resan flera meddelandekanaler (till exempel e-post OCH SMS)?** Om ja, använd **alternativ C** (flerkanal) ovanpå valet av anmälningsmetod (A eller B). Om resan omfattar en enda kanal räcker det med alternativ A eller B.

3. **Behöver du eskalera till en annan kanal baserat på engagemang?** Om ja, välj **Alternativ C** med villkorsnoder som kontrollerar interaktionen med tidigare meddelanden och växla till alternativa kanaler.

4. **Är målgruppen känd i förväg och bearbetad enligt ett schema?** Om ja, välj **Alternativ A**. Välj **Alternativ B** om profiler ska gå in på resan så fort de utför en åtgärd.

## Implementeringsfaser

Följande faser går igenom hela implementeringen av en flerstegsstyrd resa.

### Fas 1: Konfigurera kanaler och förbereda målgrupper

**Programfunktioner:** AJO: Kanalkonfiguration, RT-CDP: Målgruppsutvärdering

Innan resan kan designas måste alla kanalytor vara aktiva och ingångspubliken (för alternativ A) måste definieras och utvärderas. Denna fas säkerställer att infrastrukturen är redo för meddelandeleverans.

#### Bestäm kanaltyp för varje kontaktyta

Vilka meddelandekanaler kommer resan att använda vid varje kontaktyta?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Endast e-post | Resan kommunicerar exklusivt via e-post (onboarding, plantture) | Enklare konfiguration; kräver e-postunderdomän och IP-pool; reservation för inkorgsplacering |
| Endast SMS | Tidskänsliga aviseringar, påminnelser om avtalade tider | Kräver autentiseringsuppgifter för SMS-provider (Sinch, Twilio, Infobip), högre kostnad per meddelande, striktare avanmälningsregler |
| Skjut bara | Interaktionssekvenser i appen för mobilanvändare | Kräver APN/FCM-autentiseringsuppgifter. Användarna måste ha appen installerad |
| Flerkanals | Eskalering eller komplementära meddelanden över alla kanaler | Kräver kanalyta per kanal; mest komplex men med störst räckvidd |

#### Beslut om metod för målgruppsbedömning (alternativ A)

Hur snabbt måste profilerna kvalificera sig för tävlingsdeltagarna?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Batchutvärdering | Målgruppen läses enligt ett schema (varje dag, varje vecka); ingen realtidsregistrering behövs | Enkel konfiguration; målgruppen utvärderas före läsning av resan; stöder komplexa segmentregler |
| Utvärdering av strömning | Profilerna ska kvalificeras i nära realtid när attributen ändras | Segmentregeluttrycket måste vara direktuppspelningsbart, nästan i realtid-kvalificering |

#### Bestäm metod för delegering av underdomän (e-postkanal)

Hur ska den e-postsändande underdomänen delegeras till Adobe?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Fullständig delegering | Adobe hanterar DNS-poster; enklaste konfiguration | Snabbast att konfigurera; Adobe hanterar SPF, DKIM, DMARC |
| CNAME-delegering | Organisationen behåller DNS-kontrollen | Kräver DNS-administratörsinblandning. CNAME-poster måste konfigureras |

#### Gränssnittsnavigering

- Kanalytor: Administration > Kanaler > Kanalytor > Skapa yta
- Underdomäner: Administration > Kanaler > Underdomäner
- SMS-konfiguration: Administration > Kanaler > SMS-konfiguration
- Push-konfiguration: Administration > Kanaler > Inställningar för push-meddelanden
- Målgrupper: Kund > Publiker > Skapa målgrupp > Skapa regel

#### Information om nyckelkonfiguration

- Verifiera IP-poolens värmerstatus för e-post - nya IP-pooler kräver en gradvis värmerplan under 2-4 veckor
- Konfigurera autentiseringsuppgifter för SMS och verifiera registrering av avsändarnummer
- Överför APN-certifikat och FCM-servernycklar för push-meddelanden
- Definiera målgruppen med hjälp av segmentverktyget med segmentregler som omfattar målpopulationen
- Inkludera undertryckningsregler i målgruppsdefinitionen (exkludera nyligen konverterad, globalt avbruten prenumeration)

#### Var alternativen skiljer sig

**För alternativ A (målgruppsläsare):**
Definiera och utvärdera målgruppen. Bekräfta att målgruppen har en population som inte är noll. Bestäm om resan ska använda ett engångs-lässchema eller ett återkommande lässchema.

**För alternativ B (händelseutlöst):**
Kontrollera att det utlösande händelseschemat är konfigurerat och att händelser direktuppspelas till plattformen. Ingen fördefinierad målgrupp krävs - profilerna anger var för sig vid ett kvitto.

**För alternativ C (flera kanaler):**
Konfigurera kanalytor för varje kanal som används under resan (e-post, SMS, push, i appen). Verifiera godkännandestatus per kanal för målpopulationen.

#### Experience League-dokumentation

- [Konfigurera kanalytor](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Kom igång med e-postkonfiguration](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Konfigurera SMS-kanal](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Konfigurera kanal för push-meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [Planer för IP-värmare](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/ui/segment-builder)


### Fas 2: Skapa meddelandeinnehåll

**Programfunktion:** AJO: Meddelanderedigering

Skriv meddelandeinnehållet för varje kontaktyta i resan. Varje meddelande kan ha olika innehåll, personaliseringsdjup och kanal. I den här fasen skapas allt innehåll som kan slutas och som reseåtgärdsnoderna refererar till.

#### Bestäm dig för innehållsstrategi

Ska alla meddelanden börja från en mall, utformas från grunden eller importera HTML?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Befintlig innehållsmall | Varumärkesstyrda meddelanden med väletablerade layouter | Snabbast; säkerställer varumärkeskommunikation; mallen måste finnas och matcha kanaltypen |
| Designa från grunden | Unik, anpassad layout för varje kontaktyta | Mest flexibel, längre byggtid; använd dra och släpp-funktionen i e-post för Designer |
| Importera HTML | Förbyggda HTML från externa designverktyg | Kräver rena HTML; kan behöva justeras för att svara |

#### Bestäm dig för djupet i personaliseringen

Hur mycket personalisering ska varje meddelande innehålla?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Grundläggande infogning av token | Förnamn, ort, enkla profilattribut | Låg komplexitet: använder Handlebars syntax med XDM-sökvägar |
| Villkorliga innehållsblock | Annat innehåll visas baserat på segment eller attribut | Komplexitet i Medium; kräver regler för dynamiskt innehåll |
| Resesammanhangsbaserad personalisering | Innehållet varierar beroende på resans gång, tidigare interaktioner | Högre komplexitet: utnyttjar variabler för reskontext och händelsedata |

#### Bestäm fragmentstrategi

Ska delade innehållsblock (sidhuvuden, sidfötter, juridisk text) skapas som återanvändbara fragment?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Återanvändbara fragment | Flera meddelanden delar gemensamma element; enhetliga varumärken krävs | Ändringarna sprids till alla meddelanden med fragmentet; maximalt 30 fragment per meddelande |
| Textbundet innehåll | Engångsmeddelanden med unika layouter | Snabbare för enstaka material; inga fördelar med att skicka flera meddelanden samtidigt |

#### Gränssnittsnavigering

- Content Management > Content Templates > Browse
- Skicka e-post till Designer (inom kampanj eller resa)
- Innehållshantering > Fragment > Skapa fragment

#### Information om nyckelkonfiguration

- Skapa innehåll för varje enskild meddelandeåtgärd under resan - en resa i fyra steg kan kräva fyra separata meddelandedesigner
- Använd anpassningsuttryck som refererar till sökvägar för XDM-profiler (till exempel `{{profile.person.name.firstName}}`)
- Konfigurera dynamiska innehållsblock för segmentspecifika varianter
- Förhandsgranska varje meddelande med testprofiler för att verifiera återgivning av personalisering
- Skicka korrektur till interna intressenter för granskning av innehåll
- För SMS måste du respektera teckenbegränsningar (160 tecken för GSM-standardkodning)
- Konfigurera titel, brödtext, bild och åtgärden djuplänk/URL för push

#### Experience League-dokumentation

- [Designa e-postinnehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Skapa ett e-postmeddelande](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/channels/email/create-email)
- [Lägg till personalisering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization syntax](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Dynamiskt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Arbeta med innehållsmallar](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Arbeta med innehållsfragment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Skapa ett SMS-meddelande](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/create-sms)
- [Utforma ett push-meddelande](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/design-push)
- [Förhandsgranska och testa ditt innehåll](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/content-management/preview-test/preview-test)


### Fas 3: Utforma och aktivera resan

**Programfunktion:** AJO: Journey Orchestration

Utforma arbetsytan för flera steg, inklusive startnod, åtgärdsnoder (meddelanden), villkorsnoder (förgreningar), väntenoder (tidsfördröjningar) och avslutningskriterier. Testa sedan med testprofiler och publicera.

#### Bestäm anmälningstyp

Hur ska profiler ta sig in på resan?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Läs målgrupp | Schemalagda vårdsekvenser; känd publik bearbetad i batch | Målgruppen utvärderas vid läsning; stöder engångs- eller återkommande läsningar; upp till 20 000 profiler/sek |
| Enhetshändelse | Beteendeutlösare i realtid (inköp, övergivna varukorgar) | Realtidspost; kräver händelseströmning; upp till 5 000 händelser/sek |
| Målgruppskvalifikation | Anmäl dig när en profil kommer in i eller lämnar en publik i nästan realtid | Utvärdering av direktuppspelning, utlöses av byte av segmentmedlemskap |
| Affärshändelse | Organisationsomfattande event triggar resan för en viss målgrupp | Användbar för produktlanseringar, väderhändelser, systemvarningar |

#### Bestäm vilken policy för återinträde som gäller

Kan en profil återansluta till resan efter att ha slutfört eller avslutat den?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Tillåt återinträde (med nedkylning) | Profilerna kan behöva upprepa resan (återkommande köp, säsongsbunden återkoppling) | Minsta nedkylning på 5 minuter; förhindrar dubblettposter i nedkylningsfönstret |
| Ingen återinträde | Engångsresor (onboarding, single lifecycle event) | Profilen slutför eller avslutar resan och kan inte anges igen |

#### Bestäm väntetider mellan kontaktytor

Hur länge ska resan vänta mellan varje meddelande?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Fast varaktighet (t.ex. 3 dagar) | Enhetlig pacing oavsett profilbeteende | Enkel, förutsägbar timing; minst 1 timme för målgruppsresor |
| Specifikt datum/tid | Meddelandet måste komma fram vid en exakt tidpunkt (till exempel förnyelsedatum) | Använder profilattribut eller uttryck för att bestämma exakt datum/tid |
| Anpassat uttryck | Dynamisk väntan baserad på profildata eller resekontext | Mest flexibel; kräver uttrycksredigering |

#### Bestäm vilka förgreningsvillkor som ska gälla

Vilka villkor avgör vilken sökväg en profil tar?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Kontroll av profilattribut | Gren baserat på lojalitetsnivå, produktintresse, geografi | Använder profildata som är tillgängliga vid utvärderingen |
| Kontroll av segmentmedlemskap | Förgreningen baseras på om profilen tillhör en viss målgrupp | Kräver att målgruppen definieras och utvärderas |
| Kontroll av händelsedata | Förgreningen baseras på om profilen utförde en åtgärd (öppnad e-post, klickad länk) | Utvärderar händelsedata som omfattar hela kundresan; användbart för engagemangsbaserad förgrening |
| Procentdelning | Distribuera profiler slumpmässigt över banor (för A/B-tester eller kontrollerade rollouts) | Använder inte profildata; enbart slumpmässig allokering |

#### Bestäm vilka utträdeskriterier som ska gälla

Vilken händelse eller vilket villkor gör att en profil avslutar resan tidigt?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Konverteringshändelse | Profilen slutför den önskade åtgärden (köp, registrering, inlämning av formulär) | Kräver direktuppspelning av händelser; de vanligaste avslutningskriterierna |
| Avsluta målgruppsmedlemskap | Profilen lämnar en deltagare eller delar en exkluderande publik | Utvärderar i nära realtid för strömmande målgrupper |
| Timeout | Maximal resans längd (upp till 91 dagar) | Standardsäkerhetsnät; konfigurerbart i resans egenskaper |
| Inga avslutningskriterier | Profilen slutför hela resan naturligt | Enklast; alla profiler går igenom hela resan såvida de inte tas bort manuellt |

#### Bestäm tidsgräns för resa

Hur lång tid har en profil kvar på resan?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| 91 dagar (max) | Långa resor (kvartalsvis förnyelse, utökad introduktion) | Högsta tillåtna antal; profiler som fortfarande finns på resan vid timeout avslutas automatiskt |
| Kortare längd | Resan ska slutföras inom ett angivet fönster (7 dagar, 14 dagar, 30 dagar) | Ange baserat på användningsfallets naturliga livscykel |

#### Gränssnittsnavigering

- Skapa resa: Resor > Skapa resa
- Reseegenskaper: Researbetsyta > Egenskapspanelen
- Deltagarnod: Researbetsyta > Dra &quot;Läs målgrupp&quot; eller händelseaktivitet
- Åtgärdsnoder: Researbetsyta > Drag channel action (email, SMS, push)
- Villkorsnoder: Researbetsyta > Dra villkorsaktivitet
- Vänta-noder: Researbetsyta > Dra aktiviteten Vänta
- Avslutsvillkor: Reseegenskaper > Avslutningsvillkor > Konfigurera
- Testläge: Resursyta > Växla testläge
- Publicera: Researbetsyta > Publicera

#### Information om nyckelkonfiguration

- Namnge resan med en tydlig, beskrivande konvention (till exempel&quot;Onboarding_Series_Email_v1&quot;)
- Ange tidszon för resan för konsekvent bearbetning av väntesteg
- Konfigurera varje åtgärdsnod med rätt kanalyta och länka till det redigerade meddelandeinnehållet
- Varje gren måste avslutas med en End-aktivitet
- Konfigurera regler för återregistrering som passar användningsfallet
- Använd testläge med testprofiler för att simulera hela resan före publicering
- Verifiera att testprofiler går igenom förväntade sökvägar och tar emot korrekta meddelanden

#### Var alternativen skiljer sig

**För alternativ A (målgruppsläsare):**

- Dra aktiviteten Läs målgrupp som startnod
- Välj målgrupp som definieras i fas 1
- Du kan även konfigurera ett återkommande lässchema (varje dag, varje vecka)
- Konfigurera läshastighetsbegränsningen om systeminläsningen är ett bekymmer

**För alternativ B (händelseutlöst):**

- Dra den utlösande händelsen som startnod
- Konfigurera händelseschemat och inmatningsvillkor
- Ange regler för återinträde noggrant för att undvika dubblettposter från upprepade händelser

**För alternativ C (flera kanaler):**

- Använd inmatningsmetoden från alternativ A eller B
- Vid varje åtgärdsnod väljer du lämplig kanalyta för den kontaktytan
- Lägg till villkorsnoder mellan kanaler för att kontrollera engagemang (till exempel&quot;Öppnade profilen e-postmeddelandet?&quot;) och dirigera till alternativa kanaler

#### Experience League-dokumentation

- [Skapa en resa](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Resans egenskaper](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Läs målgruppsaktivitet](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Allmänna händelser](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Elevkvalificeringshändelser](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [Lägg till ett meddelande i en resa](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Villkorsaktivitet](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Vänta på aktivitet](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Avslutningskriterier](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [Avsluta aktivitet](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/end-activity)
- [Anställningshantering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Testa din resa](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [Publicera resan](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)


### Fas 4: Konfigurera styrning och optimering

**Programfunktioner:** AJO: Frekvens- och affärsregler, AJO: Konflikt- och prioritetshantering, AJO: Innehållsexperimentering, RT-CDP: Tvingande av samtycke och styrning

Använd frekvensgränser för att förhindra överbudspublicering, tilldela prioritetspoäng för konfliktlösning med annan aktiv kommunikation, konfigurera A/B-tester inom kundmeddelanden och verifiera medgivande.

#### Bestäm konfigurationen för frekvensbegränsning

Ska resmeddelandena respektera globala frekvensgränser?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Använd frekvensregler | Resan samverkar med andra kampanjer och resor; profilerna får inte vara alltför meddelandefyllda | Meddelanden kan ignoreras om profilen redan har tryckts ned från andra kommunikationssätt |
| Undanta från begränsning | Reseddelanden är viktiga och måste alltid levereras (transaktioner, bestämmelser) | Undvik sparsam användning. Kan bidra till utmattning av meddelanden om de används för mycket |

#### Bestäm prioritetstilldelningar

Hur ska den här resan rangordnas i förhållande till andra aktiva kampanjer och resor?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Hög prioritet (70-100) | Reseddelanden är viktiga under livscykeln (registrering, förnyelse) | Högre prioritet vinner när konflikter uppstår med annan kommunikation |
| Medium prioritet (30-69) | Reseddelanden är viktiga men inte brådskande (sjukvård, utbildning) | Kan undertryckas av kommunikation med högre prioritet |
| Låg prioritet (0-29) | Reseddelanden är kompletterande eller kampanjmässiga | Kommer att undertryckas när du konkurrerar med meddelanden med högre prioritet |

#### Bestäm dig för innehållsexperiment

Ska ett resemeddelande innehålla ett A/B-test eller multivariat-test?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Ja - A/B-test | Optimera ärenderader, CTA:er eller innehållslayouter vid en viss kontaktyta | Kräver tillräcklig volym per variant för statistisk signifikans; 2-10 behandlingar stöds |
| Inga experiment | Innehållet är färdigt eller volymen är för låg för meningsfull testning | Enklare installation; ingen variantspårning behövs |

#### Gränssnittsnavigering

- Frekvensregler: Administration > Affärsregler > Skapa regel
- Prioritetspoäng: Resegenskaper > Prioritetspoäng
- Konfliktidentifiering: Administration > Affärsregler > Konflikt och prioritet
- Innehållsexperiment: Researbetsyta > Välj meddelandeåtgärd > Växla mellan olika innehållsexperiment
- Samtyckesprinciper: Integritet > Profiler > Samtyckesprinciper

#### Information om nyckelkonfiguration

- Ange kanalspecifika frekvensgränser (t.ex. max 3 e-postmeddelanden/vecka, max 1 SMS/dag, max 2 push/dag)
- Tilldela en prioritetspoäng till resan (0-100) som återspeglar dess affärsbetydelse i förhållande till annan aktiv kommunikation
- Granska panelen för konfliktidentifiering för att identifiera överlappande kampanjer eller resor
- Om du kör ett innehållsexperiment definierar du behandlingsvarianter, anger trafikallokering, väljer framgångsmått (öppningar, klickningar eller konverteringar) och anger ett konfidensintervall (vanligtvis 95 %)
- Verifiera att verkställighet av samtycke är aktivt för varje kanal som används i resan

#### Experience League-dokumentation

- [Frekvensregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Översikt över affärsregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [Prioritetspoäng](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Identifiera potentiella konflikter](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [Resegotypning och skiljeförfarande](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/conflict-prioritization/journey-capping)
- [Kom igång med innehållsexperiment](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Skapa ett innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Samtycke i Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)


### Fas 5: Konfigurera rapportering och övervakning

**Programfunktioner:** AJO: Rapporterings- och prestandaanalys, Övervakning och observerbarhet, Rapportering och analys

Övervaka körning av resan under och efter aktivering, granska steg för steg-statistik för leverans och engagemang, konfigurera varningar för misslyckad bearbetning av resan och (valfritt) skapa CJA-analyser av arbetsytan för djup funnel och utfallsvisualisering.

#### Beslut om rapporteringsmetod

Vilka rapporteringsverktyg behövs för den här resan?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Endast inbyggda AJO-rapporter | Grundläggande leverans- och engagemangsövervakning räcker | Live-rapport (under körning) och rapporten All Time (efter körning). Uppdateras var 60:e sekund för live |
| AJO + CJA - analys | Djupgående analyser från funnel, stegvisa konverteringsgrader, visualisering av bortfall eller jämförelser mellan olika kundresor krävs | Kräver CJA-anslutning och datavy som är länkad till AJO datamängder; mest omfattande |
| Endast CJA | Organisationen använder CJA som den primära analysplattformen | Kräver CJA-konfiguration. AJO systemspecifika rapporter finns fortfarande som säkerhetskopia |

#### Bestäm aviseringskonfiguration

Vilka misslyckade resor bör utlösa varningsmeddelanden?

| Alternativ | Välj när | Överväganden |
| --- | --- | --- |
| Varningar om resehantering | Rekommenderas alltid för produktionsresor | Varningar om misslyckade profilinmatningar, åtgärdsnodfel och avbrutna resor |
| Aviseringar om leveransfel | Kritisk för resor med högvärdeskommunikation | Varningar om avhoppsfrekvenser som överstiger tröskelvärden, leveransfel |

#### Gränssnittsnavigering

- Resedirektrapport: Resor > Välj resa > Live-rapport
- Rapport för hela resan: Resor > Välj resa > Rapport för all tid
- Varningar: Varningar > Varningsregler > Prenumerera
- CJA arbetsyta: Projekt > Skapa nytt projekt

#### Information om nyckelkonfiguration

- Få åtkomst till liverapporten under körningen för att övervaka profilinmatningar, utträden och leveransstatistik i realtid per steg
- Efter det att resan är klar (eller efter det att tillräckliga data har samlats in), gå igenom rapporten All Time för en omfattande analys
- Konfigurera plattformsaviseringar för fel vid resehantering och leveransproblem
- För CJA-analyser kontrollerar du att CJA-anslutningen innehåller data om AJO Experience-händelser (Message Feedback, Email Tracking, Journey Step Events)
- Bygg en CJA Workspace med
   - Visualisering av funnel som visar antalet profiler vid varje kundresa
   - Utfallsvisualisering för att identifiera bortfallspunkter
   - Stega konverteringsberäkningar
   - Analys av tid till konvertering
   - Uppdelning av engagemanget på kanalnivå (för flerkanalsresor)

#### Experience League-dokumentation

- [Rapport om livesändning på resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Global reserapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Arbeta med Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Översikt över aviseringar](https://experienceleague.adobe.com/sv/docs/experience-platform/observability/alerts/overview)
- [Analysis Workspace - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/home)
- [Integreringsguide för AJO + CJA](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

## Implementeringsöverväganden

Granska följande utkast, fallgropar, metodtips och kompromisser före och under implementeringen.

### Gardrutor och begränsningar

- Max **500 live-resor** per sandlåda - [Journey Optimizer-garderobilder](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/get-started/guardrails)
- Maximal **resans varaktighet är 91 dagar** (global tidsgräns) - profiler som fortfarande finns kvar vid tidsgränsen avslutas automatiskt
- Maximalt **50 aktiviteter** per arbetsyta
- Läs målgruppsresor som bearbetar upp till **20 000 profiler per sekund** (standardbegränsning)
- Unitära händelseresändningar har stöd för upp till **5 000 händelser per sekund** per sandlåda
- Väntestegen har en varaktighet på **minst 1 timme** för målgruppsläsningar
- Resa **minst 5 minuter för återinträde**
- Maximalt **10 kanalytor per kanaltyp** per sandlåda
- Maximal e-poststorlek på **100 kB** rekommenderas för optimal leverans
- Maximalt **30 innehållsfragment** per meddelande
- Maximalt antal **10 testbehandlingar av innehållsexperiment** (varianter) per experiment
- Maximalt **10 takkonfigurationer** per sandlåda
- Maximalt **4 000 segmentdefinitioner** per sandlåda

### Vanliga fallgropar

- **Publicering utan testning:** Använd alltid testläge med testprofiler för att validera hela resan innan publicering. Kontrollera att profilerna går igenom de förväntade grenarna, vänta tills stegen är korrekta och att meddelandena återges korrekt.
- **Saknade slutaktiviteter för grenar:** Varje resegren måste avslutas med en End-aktivitet. Resan kommer inte att kunna publiceras om någon gren lämnas utan en avslutningsnod.
- **För breda anmälningsvillkor:** En löst definierad målgrupp eller ett händelseläge kan översvämma resan med oönskade profiler. Förfina anmälningskriterierna med specifika attributkontroller och undertryckningsregler.
- **Ignorerar regler för återinträde:** För händelseutlösta resor kan profiler utlösa den utlösande händelsen flera gånger. Utan korrekt konfiguration för återinträde (neka återinträde eller nedladdning) kan profiler ackumuleras under resan och orsaka dubblettmeddelanden.
- **Förväxling av tidszon för väntesteg:** Väntetider bearbetas i UTC. Ställ in tidszonen för resan explicit i resans egenskaper för att säkerställa att väntestegen flyttas fram vid den förväntade lokala tiden.
- **Redigera en direktresa:** Direktresor kan inte redigeras direkt. Om du vill göra ändringar duplicerar du resan, ändrar kopian, stoppar originalet och publicerar den nya versionen. Planera reseversionshantering innan du publicerar.
- **Inga avslutningskriterier har definierats:** Utan avslutningskriterier kommer profiler som konverterar mitt resande att fortsätta få följande meddelanden - potentiellt irrelevanta eller motsägelsefulla. Konfigurera alltid avslutningskriterier för konverteringshändelser.
- **Felmatchning av kanalgodkännande:** En profil kan väljas för e-post men inte för SMS. Flerkanalsresor måste följa samtycke per kanal. Verifiera att godkännandefält fylls i och används vid varje kanalyta.

### God praxis

- **Börja enkelt, iterera:** Börja med en linjär 2-3-stegsresa innan du lägger till komplexa förgreningar. Validera kärnflödet innan du lagrar i villkor och kanaler.
- **Använd beskrivande namnkonventioner:** Namnge resenoder, villkor och väntesteg tydligt (till exempel &quot;Wait_3_Days_After_Welcome&quot; i stället för &quot;Wait 1&quot;). Detta gör felsökning i testläge och tolkning av rapporter mycket enklare.
- **Konfigurera avslutsvillkor tidigt:** Definiera konverteringshändelsen som ett avslutsvillkor innan du utformar resesökvägarna. Detta garanterar att de profiler som konverterar tas bort från resan oavsett vilket steg de är på.
- **Ange meningsfulla väntetider:** Basera väntetider på kundbeteendedata - tid mellan typiska interaktioner, förväntade svarstider och kanalanpassad stängsel (t.ex. 2-3 dagar mellan e-postmeddelanden, 1 vecka mellan SMS).
- **Använd villkorsnoder för att kontrollera engagemang:** Efter en meddelandeåtgärd lägger du till ett villkor för att kontrollera om profilen har aktiverats (öppnad, klickad). Dirigera engagerade profiler till en bana och ej engagerade profiler till en eskaleringsväg eller alternativ kanalväg.
- **Utnyttja beräknade attribut för förgrening:** Använd beräknade attribut som engagemangsmätningar, inköpsfrekvens eller dagar sedan senaste aktivitet för att fatta förgrenade beslut datadrivet i stället för godtyckligt.
- **Övervaka och optimera iterativt:** Granska reserapporter varje vecka under den inledande körningen. Identifiera bortfallspunkter, justera väntetider, förfina villkor och optimera meddelandeinnehållet baserat på prestandadata i varje steg.
- **Version av dina resor:** När du gör ändringar duplicerar du resan för att skapa en ny version. Underhåll en logg över versionsändringar för granskning och optimeringsspårning.

### Avvecklingsbeslut

Följande kompromisser bör utvärderas i relation till dina specifika affärskrav.

#### Audience-read entry vs. event-triggered entry

Audience-read entry ger förutsägbar, batchbaserad bearbetning som är enklare att hantera och testa. Händelseutlöst inträde ger svarstider i realtid som är mer kontextuellt relevant men kräver strömmande infrastruktur och mer noggrann hantering av återinträde.

- **Målgruppsläsare:** Förutsägbarhet, bearbetning av stora volymer, schemalagda livscykelprogram, enklare testning
- **Händelseutlösta tjänster:** Relevans i realtid, beteendesammanhang, individuell profilpaketering, omedelbar respons på kundåtgärder
- **Rekommendation:** Använd målgruppsläsare för planerade livscykelprogram (introduktion, förnyelse) där timing är affärsdriven. Använd händelseutlösta för beteendebaserade svarssekvenser (kundvagnsöverlåtelse, efterköp) där timing är kundstyrd.

#### En kanal kontra flerkanalsresa

Enkanalsresor är enklare att implementera, testa och hantera. Flerkanalsresor ger bredare räckvidd och fler möjligheter till eskalering, men ökar komplexiteten när det gäller att skapa innehåll, hantera samtycke och frekvensstyrning.

- **Enkanalsfördelar:** Snabbare implementering, enklare hantering av samtycke, lägre innehållsproduktion, enklare felsökning
- **Flerkanalsmarknadsföring:** Högre engagemangspotential, kanaleskalering för profiler som inte svarar, mer omfattande kundupplevelse
- **Rekommendation:** Börja med en enkelkanalsresa och validera flödet och affärseffekten innan du expanderar till flerkanalsmarknadsföring. Lägg till kanaler inkrementellt där engagemangsdata visar att den primära kanalen inte når målgruppen effektivt.

#### Förenklad resa jämfört med hanterbarhet

En omfattande resa med många villkor och sökvägar kan hantera fler scenarier men blir svårare att testa, felsöka och optimera. En enklare resa med färre grenar är enklare att hantera men kan ge en mindre personaliserad upplevelse.

- **Komplexa resor gynnar:** Detaljanpassning, segmentspecifika sökvägar, omfattande scenariotäckning
- **Enklare resor:** Snabbare driftsättning, enklare testning, tydligare rapportering, lägre underhållsbörda
- **Rekommendation:** Begränsa resor till 3-5 större grenar och 15-25 aktiviteter. Om logiken kräver större komplexitet bör man överväga att dela upp sig i flera resor med samordning mellan olika resor i stället för en enda monolitisk resa.

#### Frekvensbegränsning jämfört med slutförd resa

Strikta anfanger för frekvens skyddar mot övermeddelanden men kan utelämna kundmeddelanden, vilket gör att profiler hoppar över steg och minskar antalet slutförda kundresor. Tack vare milda ändar kan man vara säker på att kundens budskap levereras men att de är trötta på riskkanalen.

- **Strikta anspråk till förmån:** Kundupplevelseskydd, minskad avanmälan, varumärkesförtroende
- **Stöd för milstolpar:** Färdigställningsgrad för resa, leverans av fullständiga meddelandesekvenser, effektivitet för marknadsföringsprogram
- **Rekommendation:** Tilldela högre prioritetspoäng till viktiga resemeddelanden (registrering, förnyelse) så att de har företräde framför kampanjerna när tidsgränsen nås. Reservera&quot;undantaget från capping&quot; endast för verkligt viktig kommunikation.

## Relaterad dokumentation

Följande resurser ger mer information om de funktioner som används i den här implementeringen.

### Resor

- [Kom igång med resor](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [Skapa en resa](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Resans egenskaper](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [Publicera resan](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)
- [Testa din resa](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)

### Reseverksamhet

- [Läs målgruppsaktivitet](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [Allmänna händelser](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [Elevkvalificeringshändelser](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [Villkorsaktivitet](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [Vänta på aktivitet](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [Lägg till ett meddelande i en resa](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [Avsluta aktivitet](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/end-activity)
- [Konfigurera en anpassad åtgärd](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions)

### Hantering av in- och utträde

- [Anställningshantering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [Avslutningskriterier](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)

### Kanalkonfiguration

- [Kom igång med e-postkonfiguration](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [Konfigurera kanalytor](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [Delegera underdomäner](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [Skapa IP-pooler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [Planer för IP-värmare](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [Konfigurera SMS-kanal](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [Konfigurera kanal för push-meddelanden](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### Framtagning och personalisering av meddelanden

- [Skapa ett e-postmeddelande](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/channels/email/create-email)
- [Designa e-postinnehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [Använda e-postinnehållskomponenter för Designer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/content-components)
- [Lägg till personalisering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization syntax](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [Hjälpfunktioner](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [Dynamiskt innehåll](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [Arbeta med innehållsmallar](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [Arbeta med innehållsfragment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [Förhandsgranska och testa ditt innehåll](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### Innehållsexperiment

- [Kom igång med innehållsexperiment](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [Skapa ett innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Rapport om innehållsexperiment](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Statistikberäkningar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

### Täthet, konflikt och prioritet

- [Frekvensregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [Översikt över affärsregler](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [Kom igång med konflikthantering och prioritetshantering](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [Prioritetspoäng](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [Resegotypning och skiljeförfarande](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/conflict-prioritization/journey-capping)
- [Identifiera potentiella konflikter](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/conflict-prioritization/conflicts)

### Målgrupper och segmentering

- [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/home)
- [Användargränssnittsguide för segmentbyggare](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/ui/segment-builder)
- [Profile Query Language referens](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/pql/overview)
- [Direktuppspelningssegmentering](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/api/streaming-segmentation)
- [Edge segmentering](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/api/edge-segmentation)

### Rapportering och analys

- [Rapport om livesändning på resa](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [Global reserapport](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Arbeta med Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Integreringsguide för AJO + CJA](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Analysis Workspace - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-workspace/home)
- [CJA - översikt](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-overview/cja-overview)

### Medgivande och styrning

- [Samtycke i Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [Översikt över dataförvaltning](https://experienceleague.adobe.com/sv/docs/experience-platform/data-governance/home)
- [Hantera undertryckningslista](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### Data Foundation

- [XDM - systemöversikt](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/home)
- [Översikt över identitetstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/home)
- [Profilöversikt](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/home)
- [Översikt över beräknade attribut](https://experienceleague.adobe.com/sv/docs/experience-platform/profile/computed-attributes/overview)
