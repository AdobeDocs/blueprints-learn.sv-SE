---
title: Journey Optimizer - plan för tredjepartsmeddelanden
description: Visar hur Adobe Journey Optimizer kan användas med tredjeparts meddelandesystem för att samordna och skicka personaliserad kommunikation.
solution: Journey Optimizer
exl-id: 3a14fc06-6d9c-4cd8-bc5c-f38e253d53ce
source-git-commit: 60a7785ea0ec4ee83fd9a1e843f0b84fc4cb1150
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 2%

---

# Design för tredjepartsmeddelanden

Visar hur Adobe Journey Optimizer kan användas med tredjeparts meddelandesystem för att samordna och skicka personaliserad kommunikation.

<br>

## Arkitektur

<img src="assets/3rd-party-messaging-architecture.svg" alt="Referensarkitektur Journey Optimizer - utkast" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Förutsättningar

Adobe Experience Platform

* Scheman och datauppsättningar måste konfigureras i systemet innan du kan konfigurera Journey Optimizer-datakällor
* För Experience Event-klassbaserade scheman lägger du till fältgruppen &#39;Orchestration eventID&#39; när du vill att en händelse som inte är en regelbaserad händelse ska aktiveras
* För enskilda profilklassbaserade scheman lägger du till fältgruppen Profiltestinformation för att kunna läsa in testprofiler som ska användas med Journey Optimizer

Meddelandeprogram från tredje part

* Måste ha stöd för REST API-anrop för att skicka transaktionsnyttolaster

<br>

## Skyddsräcken

[Journey Optimizer Guardrails - produktlänk](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=sv-SE)

[Garantier och Vägledning för svarstid från slut till slut](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=sv-SE)


## Implementeringssteg

### Adobe Experience Platform

#### Schema/datauppsättningar

1. [Konfigurera enskilda profiler, upplevelsehändelser och scheman för flera entiteter](https://experienceleague.adobe.com/?lang=sv&recommended=ExperiencePlatform-D-1-2021.1.xdm) i Experience Platform utifrån data som kunden har angett.
1. [Skapa datauppsättningar](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=sv-SE) i Experience Platform för data som ska importeras.
1. [Lägg till dataanvändningsetiketter](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=sv-SE) i Experience Platform i datauppsättningen för styrning.
1. [Skapa profiler](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=sv-SE) som framtvingar styrning på mål.

#### Profil/identitet

1. [Skapa alla kundspecifika namnutrymmen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=sv-SE).
1. [Lägg till identiteter i scheman](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=sv-SE).
1. [Aktivera scheman och datauppsättningar för profilen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=sv-SE).
1. [Ställ in sammanslagningsprinciper](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=sv-SE) för olika vyer av [!UICONTROL Kundprofil i realtid] (valfritt).
1. Skapa segment för reseanvändning.

#### Källor/destinationer

1. [Infoga data i Experience Platform](https://experienceleague.adobe.com/?lang=sv&recommended=ExperiencePlatform-D-1-2020.1.dataingestion) med hjälp av direktuppspelnings-API:er och källanslutningar.

### Journey Optimizer

1. Konfigurera din Experience Platform-datakälla och bestäm vilka fält som ska cachas som en del av de profileStreaming-data som används för att initiera en kundresa måste konfigureras i Journey Optimizer först för att få ett orchestration-ID. Detta orkestrerings-ID skickas sedan till utvecklaren för användning vid förtäring
1. Konfigurera externa datakällor
1. Konfigurera anpassade åtgärder för program från tredje part

### Mobil push-konfiguration (valfritt eftersom tredje part kan samla in token)

1. Implementera Experience Platform Mobile SDK för att samla in push-tokens och inloggningsinformation för att koppla tillbaka till kända kundprofiler
1. Utnyttja Adobe-taggar och skapa en mobil egenskap med följande tillägg:
   * Adobe Journey Optimizer
   * Adobe Experience Platform Edge Network
   * Identitet för [!DNL Edge Network]
   * Mobile Core
1. Se till att du har en dedikerad datastam för mobilappsdistributioner jämfört med webbdistributioner
1. Mer information finns i [Adobe Journey Optimizer Mobile Guide](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer/)

<br>

## Relaterad dokumentation

* [Experience Platform-dokumentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=sv-SE)
* [Experience Platform Tags documentation](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv-SE)
* [Experience Platform Mobile SDK-dokumentation](https://experienceleague.adobe.com/docs/mobile.html?lang=sv-SE)
* [Journey Optimizer-dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=sv-SE)
* [Journey Optimizer produktbeskrivning](https://helpx.adobe.com/se/legal/product-descriptions/adobe-journey-optimizer.html)
