---
title: Journey Optimizer med Adobe Campaign Blueprint
description: Visar hur Adobe Journey Optimizer kan användas med Adobe Campaign för att skicka meddelanden internt genom att använda meddelandeservern i Campaign
solution: Journey Optimizer, Campaign, Campaign v8, Campaign Classic v7, Campaign Standard
exl-id: 076446a9-dfb9-464c-a04f-6864b8cb7b48
source-git-commit: d19555201107b6aa827e63eb8ecff8642d9f967c
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 0%

---

# Journey Optimizer med Adobe Campaign

Visar hur Adobe Journey Optimizer kan användas tillsammans med Adobe Campaign för att skicka meddelanden internt med hjälp av meddelandeservern i Campaign.

<br>

## Arkitektur

<img src="assets/ajo-campaign-architecture.svg" alt="Referensarkitektur Journey Optimizer - utkast" style="width:100%; border:1px solid #4a4a4a" />

>[!IMPORTANT]
>Det är möjligt att använda både Journey Optimizer och Campaign för att skicka meddelanden oberoende av varandra, men har vissa tekniska överväganden som behöver övervägas. Om du vill fortsätta på den här vägen kan du samarbeta med din Pre-Sales Enterprise Architect för att se till att du vet vad som krävs för att stödja implementeringen.

<br>

## Förutsättningar

### Adobe Experience Platform

* Scheman och datauppsättningar måste konfigureras i systemet innan du kan konfigurera Journey Optimizer-datakällor
* För Experience Event-klassbaserade scheman lägger du till fältgruppen &#39;Orchestration eventID&#39; när du vill att en händelse som inte är en regelbaserad händelse ska aktiveras
* För enskilda profilklassbaserade scheman lägger du till fältgruppen Profiltestinformation för att kunna läsa in testprofiler som ska användas med Journey Optimizer
* Journey Optimizer och Campaign tillhandahålls i samma IMS-organisation

### Campaign v7/v8 eller Campaign Standard

* Körningsinstansen av meddelandetjänsten i realtid (dvs. meddelandecentret) måste vara värd för Cloud Services som hanteras av Adobe
* All meddelanderedigering görs i själva Campaign-instansen

<br>

## Guardrails

[Journey Optimizer Guardrails Product Link](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=en)

### Fler Journey Optimizer-garderobilder

* Funktionen för att hämta innehåll är tillgänglig via API idag för att säkerställa att målsystemet inte är mättat till den punkt där felet uppstod. Detta innebär att meddelanden som överskrider gränsen kommer att tas bort helt och aldrig skickas. Begränsning stöds inte.
   * Maximalt antal anslutningar - maximalt antal http/s-anslutningar som ett mål kan hantera
   * Max antal anrop - maximalt antal anrop som ska göras i parametern periodInms
   * periodInms - tid i millisekunder
* Segmentmedlemsinitierade resor kan fungera i två olika lägen:
   * Gruppsegment (uppdateras var 24:e timme)
   * Strömmande segment (&lt;5min-kvalificering)
* Gruppsegment - måste säkerställa att ni förstår den dagliga volymen av kvalificerade användare och ser till att målsystemet kan hantera den explosionsartade genomströmningen per resa och över alla resor
* Strömmande segment - måste säkerställa att den initiala höjningen av profilkvalifikationer kan hanteras tillsammans med den dagliga strömmande kvalificerande volymen per resa och över alla resor
* offera decisioningen stöds inte
* Affärshändelser stöds inte
* Utgående integreringar med system från tredje part
   * Inget stöd för en enda statisk IP eftersom vår infrastruktur är multi-tenant (måste tillåtelselista alla IP-adresser för datacenter)
   * Endast POST- och PUT-metoder stöds för anpassade åtgärder
   * Autentiseringsstöd: token | lösenord | OAuth2
* Det går inte att paketera och flytta enskilda komponenter i Adobe Experience Platform eller Journey Optimizer mellan olika sandlådor. Måste implementeras på nytt i nya miljöer

<br>

### Campaign (v7/v8)

* Körningsinstansen av meddelandecentret måste vara värd för Cloud Services som hanteras av Adobe
* Måste finnas i version 7 >21.1 eller v8
* Meddelandegenomströmning
   * AC (v7) 50 000 per timme
   * AC (v8) upp till 1 MB per timme baserat på paket
* AC (v7) stöder endast händelseinitierade resor
   * Inget segment eller segmentmedlemskap initierades på Journeys
   * Läsning av målgrupps- och affärshändelsebaserade resor stöds inte på grund av volym som kan skickas till körningsinstanserna
* Varken AC (v7) eller AC (v8) stöder Offer decisioning i meddelanden
* Ingen begränsning av utgående API-anrop till Campaign
* Loggar för transaktionsmeddelanden synkroniseras inte direkt till AEP. Kräver konsultation. Rekommendation att exportera loggar högst var fjärde timme

<br>

### Campaign Standard

* Stöder genomströmning på 14 tps (50 000 per timme)
* Stöder endast händelseinitierade resor
   * Inget segment eller segmentmedlemskap initierades på Journeys
   * Läsning av målgrupps- och affärshändelsebaserade resor stöds inte på grund av volym som kan skickas till körningsinstanserna
* Öppna och klicka-aktiviteter från transaktionsmeddelanden som skickas till Campaign Standarden visas som&quot;händelser&quot; i realtid på Journey Optimizer arbetsyta
* Loggar för transaktionsmeddelanden synkroniseras inte direkt till Experience Platform. Kräver konsultation. Rekommendation att exportera loggar högst var fjärde timme

<br>

## Implementeringssteg

### Adobe Experience Platform

#### Schema/datauppsättningar

1. [Konfigurera enskilda profiler, upplevelsehändelser och scheman för flera enheter](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) i Experience Platform, baserat på kunddata.
1. Skapa Experience Event-klassbaserade scheman för tabeller med adresser i Adobe Campaign brushlog, trackingLog och icke-levererbara adresser (valfritt).
1. [Skapa datauppsättningar](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) i Experience Platform för data som ska importeras.
1. [Lägg till etiketter för dataanvändning](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html) i Experience Platform till datauppsättningen för styrning.
1. [Skapa profiler](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html) som tillämpar styrning av destinationer.

#### Profil/identitet

1. [Skapa alla kundspecifika namnutrymmen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Lägga till identiteter i scheman](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Aktivera scheman och datauppsättningar för profilen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Ställ in sammanfogningsprinciper](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html) för olika vyer av [!UICONTROL Kundprofil i realtid] (valfritt).
1. Skapa segment för reseanvändning.

#### Källor/mål

1. [Infoga data i Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) med direktuppspelnings-API:er och källanslutningar.

### Journey Optimizer

1. Konfigurera din Experience Platform-datakälla och bestäm vilka fält som ska cachas som en del av de profileStreaming-data som används för att initiera en kundresa måste konfigureras i Journey Optimizer först för att få ett orchestration-ID. Detta orkestrerings-ID skickas sedan till utvecklaren för användning vid förtäring
1. Konfigurera externa datakällor
1. Konfigurera anpassade åtgärder för Campaign-instansen

### Campaign v7/v8 eller Campaign Standard

* Meddelandemallar måste konfigureras med rätt personaliseringskontext
* Exportera arbetsflöden måste konfigureras för att exportera transaktionsmeddelandeloggarna tillbaka till Experience Platform. Rekommendationen är att köras högst var fjärde timme

### Konfiguration av Mobile Push (tillval)

1. Implementera Experience Platform Mobile SDK för att samla in push-tokens och inloggningsinformation för att koppla tillbaka till kända kundprofiler
1. Utnyttja Adobe-taggar och skapa en mobil egenskap med följande tillägg:
   * Adobe Journey Optimizer | Adobe Campaign Classic | Adobe Campaign Standard
   * Adobe Experience Platform Edge Network
   * Identitet för Edge Network
   * Mobile Core
1. Se till att du har en dedikerad datastam för mobilappsdistributioner jämfört med webbdistributioner
1. Mer information finns i [Adobe Journey Optimizer Mobile Guide](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer)

   >[!IMPORTANT]
   >Mobile-tokens kan behöva samlas in både i Journey Optimizer och Campaign om man vill skicka realtidskommunikation via Journey Optimizer och batchpush-meddelanden via Campaign. Campaign v8 kräver att Campaign SDK endast används för att hämta push-tokens.

<br>

## Relaterad dokumentation

* [Experience Platform dokumentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Dokumentation för Experience Platform-taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en)
* [Experience Platform Mobile SDK-dokumentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
* [Journey Optimizer-dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=en)
* [Journey Optimizer produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
* [Kampanjdokumentation v8](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=en)
* [Dokumentation för Campaign v7](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
