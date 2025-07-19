---
title: B2B-resor med Marketo Data-plan
description: Design for Rapid Deployment of Journey Optimizer B2B edition Using Marketo Engage Data.
solution: Journey Optimizer B2B Edition
exl-id: d7bd0bd3-0f61-4e59-855f-27afc147c9aa
source-git-commit: a0cbce2b4ed06517234b18020cef7acbda7de736
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 0%

---

# B2B-resor med Marketo Data-plan

Denna omfattande guide beskriver hur man integrerar Marketo Engage med Adobe Journey Optimizer B2B edition. Det omfattar konfiguration av anpassat schema, konsumtion av profiler och konton samt samordning av personaliserade resor för inköpsgrupper. Genom att använda Marketo Engage-data säkerställer den här planen exakt målgruppsanpassning och engagemang i flera kanaler, vilket ökar den kvalificerade efterfrågan och förbättrar kundupplevelserna.

## Användningsfall

* **Skapa och hantera inköpsgrupper**: Använd generativ AI för att samla och hantera inköpsgrupper inom målkonton, vilket ger en heltäckande täckning av viktiga intressenter
* **Automatisera medlemstilldelning**: Tilldela automatiskt medlemmar till inköpsgrupproller baserat på definierade kriterier, som innehållsförbrukning och CRM-data
* **Personaliserade resor**: Designa och visualisera flerstegsresor som är skräddarsydda för varje inköpsgrupp och medlem utifrån deras roll, konto, produktintresse och livscykelstadium
* **Automatisering i realtid**: Automatisera utvecklingen av konton och inköpsgrupper via resor med hjälp av interaktionsutlösare i realtid och kvalificeringsbedömning
* **Cross-Channel Engagement**: Engagera inköpsgrupper över flera kanaler, inklusive e-post, SMS, annonser, chatt, event och webbinarier för att effektivisera generering och kvalificering av efterfrågan
* **AI-drivna insikter**: Använd AI-baserade insikter för att optimera innehållsleverans och engagemangsstrategier för enskilda köpare och hela inköpsgrupper
* **Aktivering av enhetliga data**: Aktivera listorna med enhetliga konton från Adobe Real-Time Customer Data Platform för att tillhandahålla de senaste och fullständiga uppgifterna för att köpa grupper och hantera dem
* **Förbättrade Collaboration**: Koordinera marknadsförings- och säljsatsningar för att skapa exaktare säljmöjligheter och påskynda framtagningen av pipeline

## Tillämpningar

* Journey Optimizer B2B Edition
* Customer Data Platform B2B edition i realtid
* Marketo Engage

## Integreringsmönster

| Integrering | Beskrivning |
| :-- | :--- |
| [Marketo Engage-anslutning](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) | Adobe Experience Platform underlättar inmatningen av data från Marketo och ger möjlighet att strukturera, märka och förbättra data med hjälp av dess tjänster. |
| [Journey Optimizer B2B edition - Marketo Engage-åtgärd](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/account-journeys/journey-nodes/action-nodes#marketo-engage-actions) | Synkronisera Account-Based Marketing i Journey Optimizer B2B edition med huvudinsatser i Marketo Engage med personbaserade åtgärder för att hantera listmedlemskap, personpartitioner och begära kampanjer. |
| [Journey Optimizer B2B edition - Marketo Engage-resurser](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/content-management/assets/marketo-engage-dam/marketo-engage-design-studio) | Marketo Engage Design Studio är standardresurskällan för Journey Optimizer B2B edition och möjliggör enkel hantering av mediefiler på kontoresor. |

## Arkitektur

![Lösningsarkitektur för AJO B2B med endast Marketo-data](./assets/ajo-b2b-marketo-only.png){zoomable="yes"}

## Implementeringssteg

* Installera B2B-scheman och namnutrymmen med något av alternativen nedan
   * Använder [Postman-samling](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility)
   * Använda [mallar](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/ui-tutorials/templates) i plattformsgränssnittet
* Skapa en dataordlista som definierar mappningen mellan Marketo-fält och Experience Platform XDM-schema
   * Använd [Marketo-objektmetadata](https://experienceleague.adobe.com/sv/docs/marketo/using/product-docs/administration/field-management/export-all-object-metadata) som startpunkt
   * [Anpassa XDM-schemat](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/ui/fields/overview) så att dina anpassade fält inkluderas
   * Granska [XDM-standardfälten](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/accounts/field-mapping) som stöds av Journey Optimizer B2B edition. Om du behöver ytterligare fält öppnar du en supportanmälan så att de konfigureras
      * **workEmail.address** krävs för persondatauppsättningen
      * **accountName** krävs i kontouppsättningen
   * Lägg till en ny XDM-fältkolumn i det exporterade Marketo-metadatakalkylbladet för att registrera den avsedda mappningen
* Konfigurera [Marketo Engage-källanslutningen](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
   * Använd dataordlistan som definieras ovan för att definiera [importmappningen](https://experienceleague.adobe.com/sv/docs/experience-platform/data-prep/ui/mapping#import-mapping) för källkopplingen
   * Rekommendationen är inte att aktivera profilen innan hänsyn tas till [implementeringshändelserna](#implementation-considerations)
   * Rekommendationer om att importera personer, företag, affärsmöjligheter och aktiviteter till ett minimum eftersom de här objekten är de mest användbara när du skapar din kontopublik
* Implementera länkningsregler för [identitetsdiagram](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/features/identity-graph-linking-rules/overview) för personer:
   * Definiera hur personposter ska länkas med hjälp av ID-namnutrymmen.
   * Konfigurera identitetsnamnutrymmen och regler för identitetssammanslagning i AEP.
   * Validera länkning med exempelpersondata och förhandsvisningsverktyg.
* Aktivera datauppsättningar för person, företag, affärsmöjligheter och aktiviteter för [profilen](https://experienceleague.adobe.com/sv/docs/experience-platform/catalog/datasets/user-guide#enable-profile)
* Definiera din första [målgrupp för ditt konto](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/accounts/account-audience-overview)
* [Köpgrupper](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/accounts/buying-groups/buying-groups-overview) eller en [kontoresa](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/account-journeys/journey-overview) kan definieras med hjälp av en Account Audience
   * När ett konto kvalificerar sig för kontouppspelningen körs jobbet för inköpsgrupper dagligen för att skapa inköpsgrupper och tilldela roller till associerade personer så fort som målgruppen uppdateras.
   * Dessutom går det att köpa gruppunderhåll varje fredag kl. 24.00 CT. Denna veckoprocess hanterar uppdateringar, t.ex. borttagning av medlemmar som inte längre är kvalificerade eller tillägg av nykvalificerade medlemmar som inte togs med i den initiala målgruppsuppdateringen.

## Rekommenderad konfiguration

För att effektivisera implementeringen och säkerställa kompatibilitet med Adobe Journey Optimizer B2B edition rekommenderas följande konfiguration:

* **Använd standardfälten för identitet:**
   * _email_ och _b2b_person_ bör behållas som identitetsfält i personschemat för att stödja identitetssammanfogning och målgruppsaktivering.
* **Använd standardmappningarna för Marketo Source Connector:**
   * Utnyttja de färdiga fältmappningarna från Adobe för att förenkla inmatningen av data och minska kostnaderna för konfigurering.
* **Använd standardmappningar för AJO B2B:**
   * Använd [standardfältmappningarna](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/accounts/field-mapping) för Journey Optimizer B2B edition för att säkerställa kompatibilitet med inköpsgrupplogik och resesamordning.
* **Blockera fältuppdateringar för alla fält utom e-post:**
   * I Marketo Engage konfigurerar du fälthantering till [blockera uppdateringar](https://experienceleague.adobe.com/sv/docs/marketo/using/product-docs/administration/field-management/block-updates-to-a-field) från Adobe Experience Platform för alla fält utom _e-post_. Detta bidrar till att upprätthålla dataintegriteten samtidigt som identitetsupplösningen aktiveras.
* **Implementera regler för identitetslänkning med e-post som ett unikt ID-namnområde**
   * Konfigurera [identitetsgrafens länkningsregler](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/features/identity-graph-linking-rules/overview) i Adobe Experience Platform så att _email_ uttryckligen används som ett unikt ID-namnområde. Dessa regler säkerställer att profiler sammanfogas korrekt över datakällor där _email_ finns, vilket möjliggör robust identitetsupplösning. I enlighet med Adobe bästa praxis kan du definiera länkningsregler som prioriterar e-post som en stabil och globalt unik identifierare för att behålla ett konsekvent och sekretesskompatibelt identitetsdiagram.
Denna konfiguration ger en balans mellan enkel driftsättning och datastyrning, vilket ger en tillförlitlig grund för att samordna B2B-resor.

## Implementeringsöverväganden

När du implementerar Adobe Journey Optimizer B2B edition är det viktigt att förstå de funktioner för identitetssammanfogning som finns i kunddataplattformen i realtid. Den här plattformen sammanfogar identiteter på både person- och kontonivå och ger en enhetlig bild av kunddata.

### Viktiga punkter

* **Identitetskorrigering**: Plattformen sätter samman identiteter med hjälp av standardidentifierare som Marketo ID, CRM ID och e-post. Detta hjälper till att skapa en heltäckande profil genom att sammanfoga data från olika källor.
* **Potentiella risker**: Om du använder e-post som identifierare för sammanfogning kan det leda till oavsiktlig identitetskomprimering. Det innebär att olika personer som delar samma e-postadress kan sammanfogas felaktigt till en enda profil. Den här identitetskomprimeringen kan negativt påverka precisionen hos CRM-data och äventyra dess integritet.
* **Sammanslagningsstrategi**: I B2B CDP används en tidsbaserad sammanslagningsstrategi, där det senaste lastUpdatedDate-värdet för ett visst profilattribut används. Den här strategin ser till att de senaste data visas i profilen.
* **Att tänka på för e-post**: Det är viktigt att noggrant utvärdera hur e-post används som identifierare för att sammanfoga profilfragment. Även om det kan vara fördelaktigt måste risken för identitetskollaps noggrant beaktas mot fördelarna. En nackdel är att det externa målgruppsmedlemskap som skapats av AJO B2B inte kan integreras i den befintliga profilen utan e-post som identifierare.
* **Marketo personintegrering**: AJO B2B använder Marketo-personen med det lägsta lead-ID:t när flera Marketo-poster sammanfogas till en enda profil.

Genom att tänka på detta kan ni fatta välgrundade beslut om hur ni konfigurerar identitetskaruschering i Adobe Journey Optimizer B2B edition, vilket ger korrekta och tillförlitliga kundprofiler.

### Utvärdera utfall av identitetskänsla

Frågetjänsten kan användas för att se effekten av identitetssammanfogning i en datauppsättning som inte är profilaktiverad. Följande fråga kan användas för utvärderingen

#### Antal inlästa poster

Den här frågan returnerar det totala antalet poster som har importerats till personprofildatauppsättningen

```sql
select
    count(distinct b2b.personKey.sourceKey)
from
    marketo_person_ajo_b2b
```

#### Duplicera e-post

Den här frågan returnerar antalet personposter som ska sammanfogas som en del av plattformens identitetssammanfogning

>[!NOTE]
>
>Datatabellen marketo_person_ajo_b2b används som ett komplett exempel på hur du arbetar med Marketo persondatauppsättning.
>&#x200B;>Du kan hitta sandlådans datauppsättning på arbetsytan [Dataset](https://experienceleague.adobe.com/sv/docs/experience-platform/catalog/datasets/user-guide).

```sql
select
    SUM(personCount)
from
    (
        select
            emailAddress,
            count(*) as personCount
        from
            (
                select
                    MAX(workemail.address) as emailAddress
                from
                    marketo_person_ajo_b2b
                where
                    workemail.address IS NOT NULL
                group by
                    b2b.personKey.sourceKey
            )
        group by
            emailAddress
        having
            count(*) > 1
    )
```

#### E-postadresser med dubblettposter

Den här frågan returnerar e-postmeddelanden med de mest duplicerade posterna i datauppsättningen.  Den här listan kan användas för att kontrollera vissa av posterna för att bättre förstå hur länkar mellan identiteter kan påverka Marketo och CRM.  Mer information om hur identitetslänkning fungerar finns i [Översikt över identitetstjänsten](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/home).

```sql
select
    *
from
    (
        select
            emailAddress,
            MAX(personId) as personId,
            count(*) as personCount
        from
            (
                select
                    b2b.personKey.sourceKey,
                    MAX(workemail.address) as emailAddress,
                    MAX(b2b.personKey.sourceId) as personId
                from
                    marketo_person_ajo_b2b
                where
                    workemail.address IS NOT NULL
                group by
                    b2b.personKey.sourceKey
            )
        group by
            emailAddress
        having
            count(*) > 1
    )
order by
    personCount desc
```

### Alternativ

#### Tar bort e-post som identitet

Om du efter din analys fastställer att e-post inte är ett giltigt fält som ska användas som identitetsfält kan personschemat ändras till [ta bort e-post som identitetsfält](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/ui/fields/identity)

#### Blockera uppdateringar från Adobe Experience Platform

Om det är bäst att behålla e-post som identitetsfält för dina användningsfall finns det ett alternativ för att [blockera fältuppdateringar](https://experienceleague.adobe.com/sv/docs/marketo/using/product-docs/administration/field-management/block-updates-to-a-field) från AJO B2B och tillåter att AJO B2B huvudsakligen körs på Marketo-data.

## Skyddsräcken

För att få en heltäckande bild av de skyddsräcken som gäller för B2B-resor med Marketo Engage, se följande officiella dokumentation:

* [Adobe Journey Optimizer B2B edition - produktbeskrivning](https://helpx.adobe.com/se/legal/product-descriptions/adobe-journey-optimizer-b2b.html)
Innehåller specifika skyddsutkast och användningsparametrar för Journey Optimizer B2B edition.
* [Adobe Experience Platform distributionsguider](https://experienceleague.adobe.com/sv/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails?lang=en)
Täcker allmänna arkitektur- och driftsättningsgarantier i Adobe Experience Platform-lösningar.
* [Adobe Marketo Engage - produktbeskrivning](https://helpx.adobe.com/se/legal/product-descriptions/adobe-marketo-engage---product-description.html#performance-guardrails)
Information om prestanda och användningsskydd för Marketo Engage, inklusive aktivering och synkronisering av CRM.
* [Real-Time CDP Guardrails](https://experienceleague.adobe.com/sv/docs/experience-platform/rtcdp/guardrails/overview?lang=en)
Tillhandahåller vägledning om dataintag, segmentering och aktiveringsgränser inom Real-Time Customer Data Platform.

## Relaterad dokumentation

* [B2B edition för kunddataplattform i realtid](https://experienceleague.adobe.com/sv/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview)
* [Komma igång med kunddataplattformen B2B edition i realtid](https://experienceleague.adobe.com/sv/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial)
* [Guardrails for Real-time Customer Data Platform B2B edition](https://experienceleague.adobe.com/sv/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails)
* [Adobe Experience Platform](https://experienceleague.adobe.com/sv/docs/experience-platform)
* [Adobe Experience Platform identitetstjänst](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/home)
* [Marketo Engage](https://experienceleague.adobe.com/sv/docs/marketo/using/home)
* [Adobe Experience Platform - Marketo Source Connector](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
* [Adobe Journey Optimizer B2B edition Documentation](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/guide-overview)
