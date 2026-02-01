---
title: Edge Profile Access för webb och mobil Personalization i realtid
description: '[!UICONTROL Åtkomst till kundprofilen i realtid] ger kontext för webb- och mobilpersonalisering i realtid.'
solution: Real-Time Customer Data Platform, Data Collection
kt: 719
exl-id: null
source-git-commit: 5530337ed9a9c67285db4abd0afba3809466e42c
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 0%

---

# Edge Profile Access för webb och mobil Personalization i realtid

Profilåtkomst i realtid för Edge för webb och mobila Personalization-modeller visar hur webb- och mobilprogram kan komma åt Adobe Experience Platform [!UICONTROL kundprofil i realtid] vid sidan om för personalisering med hög genomströmning och låg latens.

Applikationerna kan få åtkomst till profilattribut och målgrupper i realtid med millisekundersfördröjning. Attribut, målgruppsmedlemskap och modellstyrda funktioner som lagras i profilen som attribut kan nås i realtid för samma sida och nästa sida-personalisering över webb- och mobilkanaler.

Med den här funktionen kan ni leverera personaliserade upplevelser på era webbplatser och i mobilappar baserat på kundprofilen i realtid, inklusive målgrupper som härrör från beteenden i realtid, attribut som är inkapslade i kundprofilen i realtid samt beräknade insikter.

>[!NOTE]
>
>Edge profilåtkomst är särskilt utformad för användning med hög genomströmning och låg latens, till exempel webb-/mobilpersonalisering och offertsbeslut i realtid. För scenarier med lägre genomströmning, t.ex. agentstödd support eller säljinteraktioner, är navprofilens söknings-API lämpligare. I [Real-time Profile Access finns en översikt över support- och säljscenarier](customer-activity.md) för hubbbaserad profilåtkomst.

## Tillämpningar

* Kunddataplattform i realtid
* Adobe Experience Platform Data Collection (Web SDK/Mobile SDK)
* Edge Network Server-API

## Användningsfall

* Personalisering i realtid i webb- och mobilkanaler för kända kundupplevelser
* Personalisering på samma sida och nästa sida baserad på profilattribut och målgrupper i realtid
* Innehåll och erbjud personalisering baserat på kundprofiler, inklusive beteendedata, attribut och beräknade insikter i realtid
* Integrering med personaliseringsmotorer, content management-system och externa applikationer för realtidsbeslutsfattande
* Testning och innehållsoptimering med profilkontext i realtid

## Förutsättningar

Den här planen kräver en av följande datainsamlingsmetoder om du vill att profilen ska uppdateras i realtid med strömmande data. Det går att få åtkomst till Edge-profilen i realtid utan att behöva samla in data direkt till Edge-profilen. Data kan samlas in till navet och projiceras till Edge-profilen också. Observera att det kommer att finnas ytterligare fördröjning för data som samlas in på hubben och sedan projiceras för Edge.

* Använd [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html?lang=sv-SE) om du vill samla in data från din webbplats.
* Använd [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/) om du vill samla in data från ditt mobilprogram.
* Använd [Edge Network Server-API:t](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=sv-SE) om du inte använder Web SDK eller Mobile SDK, eller implementerar en mer direkt server-till-server-anslutning.

>[!IMPORTANT]
>
>Innan du implementerar kantanpassning bör du läsa guiden om hur du [aktiverar målgruppsdata för kantanpassningsmål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations). Den här guiden tar dig igenom de nödvändiga konfigurationsstegen för användning av samma sida och nästa sida för personalisering, i flera Experience Platform-komponenter.

## Arkitekturdiagram

<img src="assets/real-time-edge-lookup.svg" alt="Referensarkitektur för Edge Profile Access för Personalization för webb och mobiler" style="width:90%; border:1px solid #4a4a4a"  class="modal-image" />

## Skyddsräcken

* [Guardsutkast för [!UICONTROL Kundprofildata i realtid] &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=sv-SE)
* [Edge Network Guardrails](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* Edge-profiler har en TTL-fil (time-to-live) på 14 dagar. Om en användare inte har varit aktiv på kanten på 14 dagar kan kantprofilen upphöra att gälla och måste hämtas från navet, vilket kan påverka personaliseringen på första sidan.
* Edge personalisering stöder utvärdering av målgruppsmedlemskap i realtid för målgrupper som uppfyller villkoren för kantsegmentering. Målgrupper för grupp- och direktuppspelning från navet finns också tillgängliga i toppen med lämplig konfiguration.

## Implementeringsmönster

Edge-personalisering kan implementeras med målet [Anpassad Personalization-anslutning](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/personalization/custom-personalization) i kunddataplattformen i realtid. Den här destinationen stöder flera datainsamlingsmetoder beroende på ditt användningsfall.

### Mönster 1: Målgruppsbaserad personalisering med Web SDK/Mobile SDK

* Använd Adobe Experience Platform Web SDK eller Mobile SDK tillsammans med Edge Network för målgruppsbaserad personalisering.
* Den här metoden ger låg latens och bästa prestanda för kantanpassning baserat på målgruppsmedlemskap.
* Kantsegmentering i realtid kräver implementering av Web/Mobile SDK.
* SDK och SDK för mobiler **på webben stöder endast personalisering baserat på målgruppsmedlemskap**.
* [Se Experience Platform Web and Mobile SDK Blueprint](../experience-platform/deployment/websdk.md) för SDK-baserad implementering.
* För implementering av Mobile SDK måste tillägget [Adobe Journey Optimizer - Decisioning](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/) vara installerat i Mobile SDK.

### Mönster 2: Attributbaserad anpassning med Edge Network Server-API (krävs för profilattribut)

>[!IMPORTANT]
>
>**Attributbaserade personaliseringskrav:** Om du vill anpassa baserat på profilattribut (inte bara målgruppsmedlemskap) måste du **&#x200B;**&#x200B;använda [Edge Network Server-API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=sv-SE) med autentiserad integration på serversidan, oavsett om du också använder Web SDK eller Mobile SDK för datainsamling.

* Möjliggör integrering med externa personaliseringsmotorer och CDN-baserad personalisering.
* Edge Network Server-API:t är **obligatoriskt** för att säkert hämta profilattribut för personalisering.
* Du kan hämta profilattribut via Edge Network Server-API:t genom att lägga till en integration på serversidan som använder samma dataström som du redan använder för din webb- eller Mobile SDK-implementering.
* Alla API-anrop till Edge Network Server för profilattribut måste göras i en autentiserad kontext för att skydda känsliga data.
* Det här mönstret möjliggör både målgruppsbaserad personalisering och attributbaserad personalisering.
* Lämplig för personalisering på serversidan, API-baserade integreringar och scenarier som kräver åtkomst till profilattribut.

## Implementeringssteg

1. [Skapa scheman](https://experienceleague.adobe.com/?lang=sv&recommended=ExperiencePlatform-D-1-2021.1.xdm) för data som ska importeras.
1. [Skapa datauppsättningar](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=sv-SE) för data som ska importeras.
1. [Konfigurera rätt identiteter och identitetsnamnutrymmen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=sv-SE) i schemat för att säkerställa att inkapslade data kan sammanfogas till en enhetlig profil.
1. [Aktivera scheman och datauppsättningar för profilen &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=sv-SE).
1. [Infoga data](https://experienceleague.adobe.com/?lang=sv&recommended=ExperiencePlatform-D-1-2020.1.dataingestion) i Experience Platform.
1. [Konfigurera sammanfogningsprinciper](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=sv-SE) för att säkerställa korrekt identitetssammanfogning och profilsammanfogning.
1. [Konfigurera en datastream](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=sv-SE) i Experience Platform Data Collection med målkonfigurationen aktiverad. Datastream avgör i vilken datainsamling som målgrupperna inkluderas i svaret på sidan.
1. Implementera [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html?lang=sv-SE) eller [Mobile SDK](https://developer.adobe.com/client-sdks/home/) på webb- och mobilegenskaper för datainsamling.
1. Konfigurera kantsegmentering för målgrupper som behöver realtidsutvärdering. [Edge segmenteringsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=sv-SE).
1. Ange [Anpassad Personalization-anslutning](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/personalization/custom-personalization) som mål i målkatalogen:
1. [Aktivera målgrupper till kantanpassningsmålet](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations). Välj vilka målgrupper du vill aktivera till målet.
1. (Valfritt för attributbaserad personalisering) Om du behöver anpassa dig baserat på profilattribut utöver målgruppsmedlemskapet implementerar du [Edge Network Server-API:t](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=sv-SE) med autentiserad integration på serversidan med samma datastam. Detta är **obligatoriskt** för åtkomst av profilattribut.
1. Implementera anpassningslogik i webb-/mobilapplikationen för att förbruka exporterade målgruppsdata och profilattribut:
   * Om du använder taggar i Adobe Experience Platform använder du funktionen [skicka-händelse, fullständig](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=sv-SE), för att få åtkomst till variabeln `event.destinations` med exporterade data.
   * Om du inte använder taggar kan du använda [kommandosvar](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/commands/command-responses.html?lang=sv-SE) för att tolka JSON-svaret från Adobe Experience Platform och hämta målar-ID:n och profilattribut.

## Implementeringsöverväganden

### Identitetsaspekter

* Alla primära identiteter kan användas för kantanpassning när du använder Web SDK eller Mobile SDK med Edge Network.
* För personalisering av första inloggningen med kända kunddata måste personaliseringsbegäran använda en primär identitet som matchar den kända kundidentiteten i kunddataplattformen i realtid. Om det primära ID:t är ECID eller en anonym identitet som ännu inte sytts ihop med den kända kundprofilen, tar det tid för identitetssammanställningen att realiseras, vilket kan påverka tillgängligheten av historiska profildata för personalisering.
* Edge-profiler måste initieras innan de kan användas för personalisering. Första gången besökare eller återkommande besökare vars edge-profil har upphört att gälla (14-dagars TTL) kan få en inledande personalisering baserat på begränsade profildata tills edge-profilen är helt ifylld.

### Attributbaserad personalisering

>[!IMPORTANT]
>
>Profilattribut kan innehålla känsliga data. För att skydda dessa data **måste** använda [Edge Network Server-API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=sv-SE) när du konfigurerar det anpassade Personalization-målet för attributbaserad personalisering. Alla Edge Network Server-API-anrop måste göras i en autentiserad kontext.

* För attributbaserad personalisering med hjälp av profilattribut måste du lägga till en integration på serversidan med Edge Network Server-API:t som använder samma dataström som du använder för din webb- eller Mobile SDK-implementering.
* Du måste konfigurera vilka profilattribut som ska inkluderas i kantprojektionen via den anpassade målkonfigurationen för Personalization Connection.
* **Endast SDK och SDK för mobiler stöder endast personalisering baserat på målgruppsmedlemskap**. Edge Network Server-API:t är **obligatoriskt** för att säkert hämta profilattribut för personalisering.
* Om du inte implementerar Edge Network Server-API:t för attributåtkomst kommer personaliseringen endast att baseras på målgruppsmedlemskap.
* API-svaret för anpassade Personalization med attribut innehåller ett `attributes`-avsnitt förutom målgruppssegmenten.

### Målgruppshänsyn

* Målgrupper som utvärderas genom strömning eller gruppsegmentering på navet projiceras till utkanten och kan användas för personalisering.
* Målgrupper som uppfyller villkoren för kantsegmentering utvärderas i realtid för helsidespersonalisering.
* Konfigurera lämpliga målgrupper för kantutvärdering baserat på deras användning i realtidspersonalisering.

## Relaterad dokumentation

### Målkonfigurationer

* [Anpassad Personalization-anslutning](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/personalization/custom-personalization) - primär implementeringsguide
* [Översikt över Personalization-mål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/personalization/overview)
* [Aktivera målgrupper för att kanalisera personaliseringsmål](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations)
* [Leta upp profilattribut på kanten i realtid](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/ui/activate/activate-edge-profile-lookup)

### SDK-dokumentation

* [Experience Platform Web SDK-dokumentation](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html?lang=sv-SE)
* [Experience Platform Mobile SDK-dokumentation](https://developer.adobe.com/client-sdks/home/)
* [Edge Network Server-API-dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=sv-SE)
* [Experience Platform Tags-dokumentation](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv)
* [Kommandosvar i Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/commands/command-responses.html?lang=sv-SE)

### Profil- och segmenteringsdokumentation

* [[!UICONTROL Kundprofil i realtid] dokumentation](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=sv-SE)
* [Profilsäkerhetsutkast](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=sv-SE)

### Självstudiekurser

* [Nästa steg i personaliseringen med Real-Time CDP och Adobe Target](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=sv-SE)
* [Dataströmskonfiguration](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=sv-SE)
