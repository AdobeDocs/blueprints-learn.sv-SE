---
title: Journey Optimizer med Adobe Campaign v7-ritning
description: Visar hur Adobe Journey Optimizer kan användas med Adobe Campaign för att skicka meddelanden internt genom att använda meddelandeservern i Campaign
solution: Journey Optimizer, Campaign, Campaign Classic v7, Campaign Standard
exl-id: 6d9bc65c-cca0-453f-8106-d2895d005ada
source-git-commit: 60a7785ea0ec4ee83fd9a1e843f0b84fc4cb1150
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 1%

---

# Journey Optimizer med Adobe Campaign v7-ritning

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

### Campaign v7

* Körningsinstansen av meddelandetjänsten i realtid (dvs. meddelandecentret) måste vara värd för Cloud Service som hanteras av Adobe
* All meddelanderedigering görs i själva Campaign-instansen

<br>

## Skyddsräcken

[Journey Optimizer Guardrails - produktlänk](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=en)

[Garantier och Vägledning för svarstid från slut till slut](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

## Implementeringssteg

### Adobe Experience Platform

#### Schema/datauppsättningar

1. [Konfigurera enskilda profiler, upplevelsehändelser och scheman för flera entiteter](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) i Experience Platform utifrån data som kunden har angett.
1. Skapa Experience Event-klassbaserade scheman för tabeller med adresser i Adobe Campaign brushlog, trackingLog och icke-levererbara adresser (valfritt).
1. [Skapa datauppsättningar](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) i Experience Platform för data som ska importeras.
1. [Lägg till dataanvändningsetiketter](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html) i Experience Platform i datauppsättningen för styrning.
1. [Skapa profiler](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html) som framtvingar styrning på mål.

#### Profil/identitet

1. [Skapa alla kundspecifika namnutrymmen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Lägg till identiteter i scheman](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Aktivera scheman och datauppsättningar för profilen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Ställ in sammanslagningsprinciper](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html) för olika vyer av [!UICONTROL Kundprofil i realtid] (valfritt).
1. Skapa segment för reseanvändning.

#### Källor/destinationer

1. [Infoga data i Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) med hjälp av direktuppspelnings-API:er och källanslutningar.

### Journey Optimizer

1. Konfigurera din Experience Platform-datakälla och bestäm vilka fält som ska cachas som en del av de profileStreaming-data som används för att initiera en kundresa måste konfigureras i Journey Optimizer först för att få ett orchestration-ID. Detta orkestrerings-ID skickas sedan till utvecklaren för användning vid förtäring
1. Konfigurera externa datakällor
1. Konfigurera anpassade åtgärder för Campaign-instansen

### Campaign v7

* Meddelandemallar måste konfigureras med rätt personaliseringskontext
* För Campaign v7 - Exportera arbetsflöden måste konfigureras för att exportera transaktionsmeddelandeloggarna tillbaka till Experience Platform. Rekommendationen är att köras högst var fjärde timme.

### Mobil push-konfiguration (valfritt)

1. Implementera Experience Platform Mobile SDK för att samla in push-tokens och inloggningsinformation för att koppla tillbaka till kända kundprofiler
1. Utnyttja Adobe-taggar och skapa en mobil egenskap med följande tillägg:
   * Adobe Journey Optimizer | Adobe Campaign Classic | Adobe Campaign Standard
   * Adobe Experience Platform [!DNL Edge Network]
   * Identitet för [!DNL Edge Network]
   * Mobile Core
1. Se till att du har en dedikerad datastam för mobilappsdistributioner jämfört med webbdistributioner
1. Mer information finns i [Adobe Journey Optimizer Mobile Guide](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer)

   >[!IMPORTANT]
   >Mobila tokens kan behöva samlas in i både Journey Optimizer och Campaign om man vill skicka realtidskommunikation via Journey Optimizer och batchpush-meddelanden via Campaign. Campaign v8 kräver att Campaign SDK endast används för att hämta push-tokens.

<br>

## Relaterad dokumentation

* [Journey Optimizer-dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=en)
* [Journey Optimizer produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
* [Kampanjdokumentation v7](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
