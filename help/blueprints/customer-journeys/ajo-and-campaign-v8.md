---
title: Journey Optimizer med Adobe Campaign v8-plan
description: Visar hur Adobe Journey Optimizer kan användas med Adobe Campaign för att skicka meddelanden internt genom att använda meddelandeservern i Campaign
solution: Journey Optimizer, Campaign, Campaign v8, Campaign Classic v7, Campaign Standard
exl-id: 447a1b60-f217-4295-a0df-32292c4742b0
source-git-commit: 5f9384abe7f29ec764428af33c6dd1f0a43f5a89
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 0%

---

# Journey Optimizer med Adobe Campaign v8-plan

Visar hur Adobe Journey Optimizer kan användas tillsammans med Adobe Campaign för att skicka meddelanden internt med hjälp av meddelandeservern i Campaign.

<br>

## Arkitektur

<img src="assets/ajo-campaign-architecture.svg" alt="Referensarkitektur Journey Optimizer - utkast" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

>[!IMPORTANT]
>Det är möjligt att använda både Journey Optimizer och Campaign för att skicka meddelanden oberoende av varandra, men har vissa tekniska överväganden som behöver övervägas. Om du vill fortsätta på den här vägen kan du samarbeta med din Pre-Sales Enterprise Architect för att se till att du vet vad som krävs för att stödja implementeringen.

<br>

## Förutsättningar

### Adobe Experience Platform

* Scheman och datauppsättningar måste konfigureras i systemet innan du kan konfigurera Journey Optimizer-datakällor
* För Experience Event-klassbaserade scheman lägger du till fältgruppen &#39;Orchestration eventID&#39; när du vill att en händelse som inte är en regelbaserad händelse ska aktiveras
* För enskilda profilklassbaserade scheman lägger du till fältgruppen Profiltestinformation för att kunna läsa in testprofiler som ska användas med Journey Optimizer
* Journey Optimizer och Campaign tillhandahålls i samma IMS-organisation

### Campaign v8

* Körningsinstansen av meddelandetjänsten i realtid (dvs. meddelandecentret) måste vara värd för Cloud Service som hanteras av Adobe
* All meddelanderedigering görs i själva Campaign-instansen

<br>

## Guardrails

[Journey Optimizer Guardrails Product Link](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=en)

[Guardrails och Slut-till-slut-vägledning om svarstid](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

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

#### Källor/destinationer

1. [Infoga data i Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) med direktuppspelnings-API:er och källanslutningar.

### Journey Optimizer

1. Konfigurera din Experience Platform-datakälla och bestäm vilka fält som ska cachas som en del av de profileStreaming-data som används för att initiera en kundresa måste konfigureras i Journey Optimizer först för att få ett orchestration-ID. Detta orkestrerings-ID skickas sedan till utvecklaren för användning vid förtäring
1. Konfigurera externa datakällor
1. Konfigurera anpassade åtgärder för Campaign-instansen

### Campaign v8

* Meddelandemallar måste konfigureras med rätt personaliseringskontext
* För Campaign-standard - Exportera arbetsflöden måste konfigureras för att exportera transaktionsmeddelandeloggarna tillbaka till Experience Platform. Rekommendationen är att köras högst var fjärde timme.
* För Campaign v8.4 är det möjligt att utnyttja Adobe Campaign Managed Services Source Connector i Experience Platform för att synkronisera leverans- och spårningshändelser från Campaign till Experience Platform. Mer information finns i dokumentationen för Source Connector. [Länk](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html)

### Mobil push-konfiguration (valfritt)

1. Implementera Experience Platform Mobile SDK för att samla in push-tokens och inloggningsinformation för att koppla tillbaka till kända kundprofiler
1. Utnyttja Adobe-taggar och skapa en mobil egenskap med följande tillägg:
   * Adobe Journey Optimizer | ADOBE CAMPAIGN CLASSIC | ADOBE CAMPAIGN STANDARD
   * Adobe Experience Platform Edge Network
   * Identitet för Edge Network
   * Mobile Core
1. Se till att du har en dedikerad datastam för mobilappsdistributioner jämfört med webbdistributioner
1. Mer information finns i [Adobe Journey Optimizer Mobile Guide](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer)

   >[!IMPORTANT]
   >Mobila tokens kan behöva samlas in i både Journey Optimizer och Campaign om man vill skicka realtidskommunikation via Journey Optimizer och batchpush-meddelanden via Campaign. Campaign v8 kräver att Campaign SDK endast används för att hämta push-tokens.

<br>

## Relaterad dokumentation

* [Journey Optimizer-dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=en)
* [Journey Optimizer produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
* [Kampanjdokumentation v8](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=en)
