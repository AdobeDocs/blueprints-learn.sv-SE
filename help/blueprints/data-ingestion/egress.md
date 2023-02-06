---
title: Layout för dataåtkomst och export
description: Denna plan innehåller en översikt över alla metoder som kan användas för att komma åt och exportera data från Adobe Experience Platform och program.
product: adobe experience platform
solution: Experience Platform, Journey Optimizer, Real-time Customer Data Platform, Tags
exl-id: 2ca51a29-2db2-468f-8688-fc8bc061b47b
source-git-commit: 96f0e4793884b4f77b22fe42a2671d1eda830e15
workflow-type: tm+mt
source-wordcount: '1513'
ht-degree: 0%

---

# Layout för dataåtkomst och export

I skisserna Dataåtkomst och Exportera anger du alla metoder som kan användas för att få åtkomst till och exportera data från Adobe Experience Platform och program.

Blueprint delas upp i två kategorier för dataåtkomst från Experience Platform och program. För det första strategier för att egressera data från Experience Platform och tillämpningar. detta betraktas som en push-typmetod för datagegress. För det andra, metoder för att få tillgång till data från Experience Platform och tillämpningar. detta betraktas som en utdragstyp för dataåtkomst.

Åtkomstmetoder:

* [API för åtkomst till kundprofiler i realtid](#rtcp-profile-access-api)
* [API för dataåtkomst](#data-access-api)
* [Frågetjänst](#query-service)

Metoder för dataexport:

* [Kundsidestaggar](#client-side-tags-extensions)
* [Vidarebefordran av händelser](#event-forwarding)
* [Real-time Customer Data Platform Destinations](#RTCDP-destinations)
* [Journey Optimizer Custom Actions](#jo-custom-actions)

## Översiktsarkitektur för dataåtkomst och -export

<img src="../experience-platform/assets/aep_data_flow.svg" alt="Referensarkitektur för dataförberedelse och matningsutkast" style="width:90%; border:1px solid #4a4a4a; margin-bottom: 15px;" />

## Metoder för dataåtkomst

### API för åtkomst till kundprofiler i realtid {#rtcp-profile-access-api}

Kunderna kan få tillgång till enstaka enhetliga profiler från kundprofilbutiken i realtid, inklusive alla profilidentiteter, målgruppsmedlemskap, attribut och upplevelsehändelser med hjälp av API:t för kundprofilåtkomst i realtid.

Se [API för åtkomst till kundprofiler i realtid](https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html?lang=en) dokumentation för ytterligare information.

#### Användningsexempel

* Sök efter en enskild profil för att lägga till kontext till kundinteraktioner för agenter, som supportinteraktioner via chatt och callcenter, eller en säljinteraktion på försäljningsstället.
* Tillåt tillagd kontext till en personaliseringsbeskrivning som görs av ett externt system, till exempel ett webbpersonaliseringssystem eller ett system för beslut om erbjudande.

#### Överväganden

* Kundprofil i realtid [skyddsräcken](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en) gäller.
* Utformad för sökning efter enstaka profiler åt gången. Används inte för att få tillgång till eller hämta hela profilpopulationen för användning av analys eller datavetenskap.
* Svarstiden för profilsökning följer profilens skyddsprofiler. Låga latenskrav i realtid - exempelvis för krav på sidanpassning bör Edge Profile användas från början till slut [Adobe Target Connection](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en) eller [Anpassad anslutning för anpassning](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=en) för profilåtkomst i realtid för webbläsare och apppersonalisering.

### API för dataåtkomst {#data-access-api}

Med API:t för dataåtkomst kan kunder få direkt åtkomst till de rådatauppsättningsfiler som lagras i Experience Platform datasjön.

* Mer information om hur du använder API:t för dataåtkomst finns i [dokumentation](https://experienceleague.adobe.com/docs/experience-platform/data-access/home.html?lang=en).

#### Användningsexempel

* Dra in råa och bearbetade datafiler från Experience Platform för lagring och utvärdering i företagsmiljöer.

#### Överväganden

* När data används på ett batchasynkront sätt kommer åtkomsten till data att vara till sin natur latent jämfört med metoder för strömmande data som utlitizing Tags, Event Forwarding eller RTCDP Destinations.
* Datafiler som bearbetas till Experience Platform lagras som samlingar av filer i grupper och komprimeras och lagras i parquet-format. När filerna hämtas och laddas ned till en annan miljö måste de därför systematiskt kommas åt av sin batch och fil i stället för en hel datauppsättning, och eventuella dataåtgärder måste ta hänsyn till de filer som komprimeras i parquet-format.

### Frågetjänst {#query-service}

Med hjälp av upplevelseplattformen kan frågetjänstkunder ställa frågor till datauppsättningar i Experience Platform och behålla frågeresultatet. En SQL-klient kan användas för att fråga och behålla frågesvaret i önskat lagringsmål som SQL-klienten kan stödja. Användargränssnittet för frågetjänsten kan användas för att lagra SQL-resultatet i en måldatauppsättning i Experience Platform eller så kan resultaten sparas på den lokala datorn.

* Mer information om hur du ansluter till SQL-klienter för att behålla SQL-resultat från Experience Platform Query Service finns i följande [dokumentation](https://experienceleague.adobe.com/docs/experience-platform/query/clients/overview.html?lang=en).

#### Användningsexempel

* Fråga rådata från datauppsättningarna i Experience Platform och behåll frågeresultaten.
* Hämta profilögonblicksbildsdatauppsättningen för att få insikter om kundprofilen i realtid. [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=en#profile-attribute-datasets).
* Lagra frågeresultat i en separat datauppsättning för åtkomst eller i en profilaktiverad datauppsättning som senare kan komprimeras via RTCDP och andra Experience Cloud-program som använder kundprofilen i realtid.

#### Överväganden

* När data efterfrågas asynkront i en batch kommer åtkomsten till data att vara till sin natur latent jämfört med strategier för att direktuppspela data, till exempel taggar, händelsevidarebefordring eller RTCDP-destinationer.
* Det är bara data som är tillgängliga i dataströmmen i Experience Platform som kan efterfrågas med hjälp av frågetjänsten. Real-time Customer Profile Store, identitetsdiagrammet, Customer Journey Analytics kan inte hämtas direkt med Query Service. Det är bara när datauppsättningar exporteras till datasjön som dessa datauppsättningar kan efterfrågas, som i exemplet med datamängden för profilögonblicksbilder.
* Observera att utkast för antalet frågeresultat och frågans tidsgräns gäller enligt instruktionerna i [Frågetjänster - skyddsutkast](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=en) dokumentation.

## Metoder för dataexport

### Kodtillägg på klientsidan {#client-side-tags-extensions}

Tillägg kan distribueras med hjälp av Adobe Tags-lösningen. När ett tillägg distribueras distribueras dataförfrågningar direkt i en klientwebbläsare eller ett program och en begäran kan anropas för att skicka data och förfrågningar till önskat mål.

Se [Översikt över taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en) dokumentation för ytterligare information.

#### Användningsexempel

* Samla in strömningsinformation direkt från klientmiljöerna med hjälp av taggning.

#### Överväganden

* Ingen direkt åtkomst till information på serversidan, som kundprofilen i Experience Platform och medlemskap för målgrupper i realtid.
* Om du lägger till ytterligare datainsamlingstaggar på sidan kan sidans inläsningstid öka.
* Möjlighet att ställa in regler för att endast begära data när vissa villkor är uppfyllda.
* Data samlas in direkt från klienten och begränsar de typer av omvandlingar och berikning som kan utföras innan data samlas in.

### Vidarebefordran av händelser {#event-forwarding}

Begäranden om datainsamling samlas in direkt till Adobe Edge Network. Från Edge Network-begäranden till externa RESTful-slutpunkter kan konfigureras för att vidarebefordra dessa begäranden till det externa målet.

Se följande [Vidarebefordran av händelser](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=en) dokumentation för ytterligare information.

#### Användningsexempel

* Samla in strömmande rådata direkt från klientmiljöerna till slutpunkterna med hjälp av Adobe serversidans händelsevidarebefordran.

#### Överväganden

* Om du vill använda händelsevidarebefordran måste data skickas till Edge-nätverket med Web SDK eller MobileSDK.
* Vidarebefordra händelser minskar sidans inläsningstid och vikt på grund av att ytterligare taggar läggs till på sidan.
* Ingen anrikning från kantprofilen eller andra datakällor stöds för närvarande.
* Begränsad datafiltrering och enkel mappningsomvandling stöds.

### Real-time Customer Data Platform destinationer {#RTCDP-destinations}

Profilattributsdata och målgruppsmedlemskapsdata kan aktiveras för företags- och annonsmål. Det innebär att data som matas in måste hämtas in i kundprofilen i Experience Platform-realtid.

Se [Real-time Customer Data Platform Destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en) dokumentation för ytterligare information.

#### Användningsexempel

* Aktivera profilattributinformation, inklusive målgruppsmedlemskap i interna datalager, analysverktyg, e-postsystem eller supportsystem.
* Aktivera medlemskap för profilmålgrupper hos en extern reklamleverantör för att anpassa och anpassa innehållet efter profilen.

#### Överväganden

* Profilattribut och målgruppsmedlemskap kan aktiveras. Raw-upplevelsehändelser kan för närvarande inte aktiveras som en del av RTCDP-destinationer.
* Aktiveringar görs i direktuppspelning eller batch beroende på vilken typ av segmentutvärdering det är och vilken typ av ingtionsprotokoll som destinationen accepterar.

### Journey Optimizer egna åtgärder {#jo-custom-actions}

Med Journey Optimizer-kunder kan man anropa en anpassad åtgärd från arbetsytan för att skicka en nyttolast eller ett meddelande till en extern API-slutpunkt som är konfigurerad. En åtgärd kan konfigureras till vilken tjänst som helst från en leverantör som kan anropas via ett REST API med en JSON-formaterad nyttolast. Den här nyttolasten kan innehålla händelseinformation, profilattribut och tidigare händelsedata, omvandlingar och berikningar som har konfigurerats under resan.

Se [Journey Optimizer egna åtgärder](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html?lang=en) dokumentation för ytterligare information.

#### Användningsexempel

* Aktiveringshändelser från Experience Platform och Journey Optimizer som innehåller ytterligare information från kundprofilen i realtid.
* Meddela externa system när en kund har nått en viss punkt på en resa.

#### Överväganden

* Länkar till genomströmningen som stöds av [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=en) och berikning som stöds av [Kundprofil i realtid](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en) gäller.
* Anpassade åtgärder kan utföras i en direktuppspelning en i taget för varje händelse eller profil under en resa. Det går inte att utföra massåtgärder eller massdatagränser i form av filer eller aggregerade förfrågningar över kundresor.
* Direktuppspelad åtkomst till kundprofilattribut i realtid och upplevelsehändelser som kan inkluderas i aktiveringsnyttolasten.
* Händelsedata kan filtreras och enkla mappningsomvandlingar tillämpas innan händelser skickas till externa mål.
