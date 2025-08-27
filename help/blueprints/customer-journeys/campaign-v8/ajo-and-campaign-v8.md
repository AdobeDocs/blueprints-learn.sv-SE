---
title: Journey Optimizer med Adobe Campaign v8-plan
description: Visar hur Adobe Journey Optimizer kan användas med Adobe Campaign för att skicka meddelanden internt genom att använda meddelandeservern i Campaign
solution: Journey Optimizer, Campaign, Campaign v8, Campaign v8 Client Console
version: Campaign v8, Campaign v8 Client Console
exl-id: 447a1b60-f217-4295-a0df-32292c4742b0
source-git-commit: 6ec61ae7e1cfe3bad7beff127dc2e80873424d53
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 2%

---

# Journey Optimizer med Adobe Campaign v8 Blueprint

Visar hur Adobe [!DNL Journey Optimizer] kan användas med Adobe [!DNL Campaign] internt för att skicka meddelanden genom att använda realtidsmeddelandeservern i [!DNL Campaign].

## Arkitektur

<img src="images/ajo-campaign-v8-architecture.svg" alt="Referensarkitektur Journey Optimizer - utkast" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

>[!IMPORTANT]
>Det är möjligt att använda både Journey Optimizer och Campaign för att skicka meddelanden oberoende av varandra, men har vissa tekniska överväganden som behöver övervägas. Om du vill fortsätta på den här vägen ska du tillsammans med din Pre-Sales Enterprise Architect se till att du vet vad som krävs för implementeringen

<br>

## Förutsättningar

Granska följande krav för varje program.

### Adobe Experience Platform

* Scheman och datauppsättningar måste konfigureras i systemet innan du kan konfigurera Journey Optimizer-datakällor
* För Experience Event-klassbaserade scheman lägger du till fältgruppen &#39;Orchestration eventID&#39; när du vill att en händelse som inte är en regelbaserad händelse ska aktiveras
* För enskilda profilklassbaserade scheman lägger du till fältgruppen &quot;Profiltestinformation&quot; för att kunna läsa in testprofiler som ska användas med Journey Optimizer
* Journey Optimizer och Campaign tillhandahålls i samma IMS-organisation

### Campaign v8

* Adobe Managed Cloud Services måste vara värd för körningsinstansen av meddelandetjänsten i realtid (dvs. meddelandecenter)
* All meddelanderedigering görs i själva Campaign-instansen

## Skyddsräcken

* [Journey Optimizer Guardrails - produktbegränsningar](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)

* [Garantier och vägledning från början till slut ](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/guardrails.html)

## Implementeringssteg

Följ implementeringarna för varje program som beskrivs nedan.

### Adobe Experience Platform

#### Schema/datauppsättningar

1. [Konfigurera enskilda profiler, upplevelsehändelser och scheman för flera entiteter](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) i Experience Platform utifrån data som kunden tillhandahållit.
1. (Valfritt) Skapa Experience Event-klassbaserade scheman för adresstabellerna Adobe Campaign broadLog, trackingLog och non-deliverable.
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

1. [Importera data till [!DNL Experience Platform]](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) med direktuppspelnings-API:er och källanslutningar.

### Journey Optimizer

1. Konfigurera din [!DNL Experience Platform]-datakälla och avgöra vilka fält som ska cachas
1. Direktuppspelningsdata som används för att initiera en kundresa måste konfigureras inom Journey Optimizer först för att få ett orkestrerings-ID. Detta Orchestration-ID skickas sedan till utvecklaren för användning vid intag.
1. Konfigurera externa datakällor.
1. Konfigurera anpassade åtgärder för Campaign-instansen.

### Campaign v8

* Meddelandemallar måste konfigureras med rätt personaliseringskontext.
* För standard [!DNL Campaign]: Exportera arbetsflöden måste konfigureras för att exportera transaktionsmeddelandeloggarna tillbaka till Experience Platform. Rekommendationen är att köras högst var fjärde timme.
* För [!DNL Campaign] v8.4 är det möjligt att använda Adobe [!DNL Campaign] Managed Services Source Connector i Experience Platform för att synkronisera leverans- och spårningshändelser från Campaign till Experience Platform. Mer information finns i dokumentationen för [Source Connector](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html).

### Mobil push-konfiguration (valfritt)

1. Implementera [!DNL Experience Platform] Mobile SDK för att samla in push-tokens och inloggningsinformation för att koppla tillbaka till kända kundprofiler.
1. Utnyttja Adobe Tags och skapa en mobil egenskap med följande tillägg:
   * Adobe [!DNL Journey Optimizer] | Adobe [!DNL Campaign Classic] | Adobe [!DNL Campaign Standard]
   * Adobe [!DNL Experience Platform] [!DNL Edge Network]
   * Identitet för [!DNL Edge Network]
   * Mobile Core
1. Se till att du har en dedikerad datastam för mobilappsdistributioner jämfört med webbdistributioner.
1. Mer information finns i [Adobe Journey Optimizer Mobile Guide](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer/push-notification/).

   >[!IMPORTANT]
   >Mobila tokens kan behöva samlas in i både Journey Optimizer och Campaign om man vill skicka realtidskommunikation via Journey Optimizer och batchpush-meddelanden via Campaign. Campaign v8 kräver att Campaign SDK enbart används för att hämta push-tokens.

## Relaterad dokumentation

* [Journey Optimizer-dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=en)
* [Journey Optimizer produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
* [Kampanjdokumentation v8](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=en)
