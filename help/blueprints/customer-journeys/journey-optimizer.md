---
title: Journey Optimizer - Triggered Messaging och Adobe Experience Platform Blueprint
description: Kör triggade meddelanden och upplevelser med Adobe Experience Platform som ett centralt nav för strömmande data, kundprofiler och segmentering.
solution: Experience Platform, Campaign, Journey Orchestration
kt: 7197
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: d19f42a181b51135c3cf672eeb957709279fe49a
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Journey Optimizer

Adobe Journey Optimizer är ett särskilt utformat system för marknadsföringsteam som i realtid kan reagera på kundbeteenden och möta dem där de befinner sig. Funktioner för datahantering har flyttats till Adobe Experience Platform, vilket gör att marknadsföringsteamen kan fokusera på det de gör bäst: som skapar kundresor och personaliserade konversationer i världsklass.  Denna plan beskriver programmets tekniska funktioner och ger en djupdykning i de olika arkitektoniska komponenterna som Adobe Journey Optimizer består av.

## Användningsexempel

* Utlösta meddelanden
* Registreringsbekräftelser
* Kundvagn och blankettinlämning
* Platsutlösta meddelanden

## Arkitektur

<img src="assets/journey-optimizer.png" alt="Referensarkitektur för Triggered Messaging och Adobe Experience Platform plan" style="border:1px solid #4a4a4a" />

## Integrationsmönster

* Adobe Experience Platform -> Journey Optimizer

## Förutsättningar

1. Kunden måste etableras för Experience Cloud med en giltig IMS-organisation
1. Mobilpush

* Kunden måste ha en mobilutvecklare tillgänglig för att kunna bygga appen
* Adobe Experience Platform Mobile SDK
* Datainsamling
   * Egenskapen Mobile-taggar
      * Tillägg:
         * Adobe Journey Optimizer Extension
         * Adobe Experience Platform Edge Network
         * Identitet
         * Mobile Core
         * Profil
   * Appkonfigurationer
   * Datastreams
      * Aktiverat för Experience Platform
      * Händelsedatauppsättning - används för att samla in allmänt mobilbeteende
      * Profildatauppsättning - AJO-push-profildatauppsättning (kan inte vara en annan)

## Guardrails

* Mer information om skyddsutkast för Journey Optimizer [LINK](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=en) finns på länken
* Gruppsegment - måste säkerställa att ni förstår den dagliga volymen av kvalificerade användare och ser till att målsystemet kan hantera den explosionsartade genomströmningen per resa och över alla resor
* Strömmande segment - måste säkerställa att den initiala höjningen av profilkvalifikationer kan hanteras tillsammans med den dagliga strömmande kvalificerande volymen per resa och över alla resor
* Profiluppdateringsaktivitet - Real-Time Customer Profile kan uppdateras direkt från en resa.  Uppdateringen till profilarkivet fördröjs med upp till 1 min
* Affärshändelser - en lässegmentbaserad resa kan utlösas för att starta baserat på ett externt anrop till JO-systemet
* Inbyggt stöd för Offer decisioning endast i meddelanden. Framtida stöd via inbyggda åtgärder
* Kanaler som stöds:
   * E-post
   * Push (FCM / APNS)
   * Resterande API-slutpunkter
* Bearbetar 5 000 händelser per sekund med vågrät skalförändring (plånboken är begränsad)
* A/B-tester utförs genom att två leveranser används och resultaten fastställs med hjälp av QS eller CJA
* Litmus Integration - måste ha ett konto med Litmus för att kunna utnyttja integreringen

## Implementeringssteg

### Adobe Experience Platform

#### Schema/datauppsättningar

1. [Konfigurera enskilda profiler, upplevelsehändelser och ](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) flerenhetskarta i Experience Platform baserat på data som kunden har tillhandahållit.
1. Skapa Adobe Campaign-scheman för widthLog, trackingLog, adresser som inte kan levereras samt profilinställningar (valfritt).
1. [Skapa ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) datauppsättningar i Experience Platform för data som ska importeras.
1. [Lägg till ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html) etiketter för dataanvändning i Experience Platform i datauppsättningen för styrning.
1. [Skapa ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html) policyer som tvingar fram styrning av destinationer.

#### Profil/identitet

1. [Skapa alla kundspecifika namnutrymmen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Lägg till identiteter i scheman](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Aktivera scheman och datauppsättningar för profilen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Ställ in sammanslagningsprinciper ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html) för olika vyer av kundprofilen [!UICONTROL  i ] realtid (valfritt).
1. Skapa segment för kampanjanvändning.

#### Källor/mål

1. [Importera data till Experience ](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) Platform med hjälp av API:er för direktuppspelning och källkopplingar.1. Konfigurera  [!DNL Azure] blobblagringsmålet för användning med Adobe Campaign.

#### Distribution av mobilappar

1. Implementera Adobe Campaign SDK för Adobe Campaign Classic eller Experience Platform SDK för Adobe Campaign Standard. Om det finns Experience Platform Launch rekommenderar vi att du använder tillägget Adobe Campaign Classic eller Adobe Campaign Standard tillsammans med Experience Platform SDK.


### Journey Orchestration

1. Direktuppspelningsdata som används för att initiera en kundresa måste konfigureras inom Journey Optimizer först för att få ett orkestrerings-ID. Detta Orchestration-ID skickas sedan till utvecklaren för användning vid intag.
1. Konfigurera externa datakällor.
1. Konfigurera anpassade åtgärder.

## Relaterad dokumentation

* [Adobe Experience Platform-dokumentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Journey Optimizer-dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=en)
* [Experience Platform Launch dokumentation](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Experience Platform Mobile SDK-dokumentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
