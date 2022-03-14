---
title: Journey Optimizer - meddelandeplan från tredje part
description: Visar hur Adobe Journey Optimizer kan användas med tredjeparts meddelandesystem för att samordna och skicka personaliserad kommunikation.
solution: Experience Platform, Journey Optimizer
source-git-commit: 1c46cbdfc395de4fc9139966cf869ba1feeceaaa
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# Meddelanden från tredje part

Visar hur Adobe Journey Optimizer kan användas med tredjeparts meddelandesystem för att samordna och skicka personaliserad kommunikation.

<br>

## Arkitektur

<img src="assets/3rd-party-messaging-architecture.svg" alt="Referensarkitektur Journey Optimizer - utkast" style="width:100%; border:1px solid #4a4a4a" />

<br>

## Förutsättningar

Adobe Experience Platform

* Scheman och datauppsättningar måste konfigureras i systemet innan du kan konfigurera Journey Optimizer-datakällor
* För Experience Event-klassbaserade scheman lägger du till fältgruppen &#39;Orchestration eventID&#39; när du vill att en händelse som inte är en regelbaserad händelse ska aktiveras
* För enskilda profilklassbaserade scheman lägger du till fältgruppen Profiltestinformation för att kunna läsa in testprofiler som ska användas med Journey Optimizer

Meddelandeprogram från tredje part

* Måste ha stöd för REST API-anrop för att skicka transaktionsnyttolaster

<br>

## Guardrails

[Journey Optimizer Guardrails Product Link](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=en)

Fler Journey Optimizer-garderobilder:

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
* Utgående integreringar med system från tredje part
   * Inget stöd för en enda statisk IP eftersom vår infrastruktur är multi-tenant (måste tillåtelselista alla IP-adresser för datacenter)
   * Endast POST- och PUT-metoder stöds för anpassade åtgärder
   * Autentiseringsstöd: token | lösenord | OAuth2
* Det går inte att paketera och flytta enskilda komponenter i Adobe Experience Platform eller Journey Optimizer mellan olika sandlådor. Måste implementeras på nytt i nya miljöer

<br>

Meddelandesystem från tredje part

* Måste förstå vilken belastning systemet kan hantera för transaktions-API-anrop
   * Antal anrop som tillåts per sekund
   * Antal anslutningar
* Måste förstå vilken autentisering som krävs för att kunna göra API-anrop
   * Autentiseringstyp: token | lösenord | OAuth2 stöds via Journey Optimizer
   * Giltighetstid för autentiseringscache: Hur länge är token giltig? 
* Om batchinmatning bara stöds behöver strömning ske till en molnlagringsmotor som Amazon Kinesis eller Azure Event Grid 1st
   * Data kan samlas in från dessa molnlagringsmotorer och överföras till tredje part
   * All mellanvara som krävs är kundens eller tredjepartsens ansvar att tillhandahålla

<br>

## Implementeringssteg

### Adobe Experience Platform

#### Schema/datauppsättningar

1. [Konfigurera enskilda profiler, upplevelsehändelser och scheman för flera enheter](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) i Experience Platform, baserat på kunddata.
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
1. Konfigurera anpassade åtgärder för program från tredje part

### Konfiguration av Mobile Push (valfritt eftersom tredje part kan samla in token)

1. Implementera Experience Platform Mobile SDK för att samla in push-tokens och inloggningsinformation för att koppla tillbaka till kända kundprofiler
1. Utnyttja Adobe-taggar och skapa en mobil egenskap med följande tillägg:
   * Adobe Journey Optimizer
   * Adobe Experience Platform Edge Network
   * Identitet för Edge Network
   * Mobile Core
1. Se till att du har en dedikerad datastam för mobilappsdistributioner jämfört med webbdistributioner
1. Mer information finns i [Adobe Journey Optimizer Mobile Guide](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer)

<br>

## Relaterad dokumentation

* [Experience Platform dokumentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Dokumentation för Experience Platform-taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en)
* [Experience Platform Mobile SDK-dokumentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
* [Journey Optimizer-dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=en)
* [Journey Optimizer produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)