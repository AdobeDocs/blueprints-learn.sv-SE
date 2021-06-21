---
title: Utlöst meddelande och Adobe Experience Platform Blueprint
description: Kör triggade meddelanden och upplevelser med Adobe Experience Platform som ett centralt nav för strömmande data, kundprofiler och segmentering.
solution: Experience Platform, Campaign, Journey Orchestration
kt: 7197
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: 584007cc71e00729732c67a97546e2c21aed3f87
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Utlöst meddelande och Adobe Experience Platform Blueprint

Kör triggade meddelanden och upplevelser med Adobe Experience Platform som ett centralt nav för strömmande data, kundprofiler och segmentering.

## Användningsexempel

* Utlösta meddelanden
* Registreringsbekräftelser
* Kundvagn och blankettinlämning
* Platsutlösta meddelanden

## Arkitektur

<img src="assets/triggered.svg" alt="Referensarkitektur för Triggered Messaging och Adobe Experience Platform plan" style="border:1px solid #4a4a4a" />

## Integrationsmönster

* Adobe Experience Platform -> Journey Orchestration

## Förutsättningar

* Adobe Experience Platform
* Journey Orchestration

## Guardrails

### Journey Orchestration

* Se länken för [mer information om begränsningar](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=en#starting-with-journeys)
* Funktionen för att kapsla är tillgänglig via API-inställningar för att säkerställa att målsystemet inte är mättat till den punkt där felet uppstod. Takning innebär att meddelanden som överskrider gränsen tas bort helt och aldrig skickas. Begränsning stöds fortfarande inte.
   * max antal anslutningar: Maximalt antal http/s-anslutningar som ett mål kan hantera
   * max antal samtal: Maximalt antal anrop som ska göras i parametern periodInms
   * periodInms: Tid i millisekunder
* Segmentmedlemsinitierade resor kan fungera i två lägen:
   * gruppsegment (uppdateras var 24:e timme)
   * Strömmande segment (&lt;5-minuters kvalificering)
* Gruppsegment: Se till att ni förstår den dagliga volymen kvalificerade användare och ser till att målsystemet kan hantera den explosionsartade genomströmningen per resa och över alla resor
* Strömningssegment: Se till att den inledande uppgången av profilkvalifikationer kan hanteras tillsammans med den dagliga direktuppspelningskvalificeringsvolymen per resa och över alla resor
* Slutdestinationen måste ha stöd för REST API och JSON-nyttolast
* Stöder för närvarande inte Offer decisioning
* Se [skyddsutkast för profil och datainmatning för Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)

### Adobe Campaign Standard

* Kan endast hantera 14 tps (50 000 per timme) i genomströmning
* Segmentmedlemsinitierade resor stöds inte
* Reaktionshändelser för öppna/klickade transaktionsmeddelanden stöds i Journey Orchestration.
* Loggar för transaktionsmeddelanden synkroniseras för närvarande inte direkt till Experience Platform, vilket kräver en manuell konfiguration. Du bör exportera loggar var fjärde timme.


## Implementeringssteg

### Adobe Experience Platform

#### Schema/datauppsättningar

1. [Konfigurera enskilda profiler, upplevelsehändelser och ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html) flerenhetskarta i Experience Platform baserat på data som kunden har tillhandahållit.
1. Skapa Adobe Campaign-scheman för widthLog, trackingLog, adresser som inte kan levereras samt profilinställningar (valfritt).
1. [Skapa ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) datauppsättningar i Experience Platform för data som ska importeras.
1. [Lägg till ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html) etiketter för dataanvändning i Experience Platform i datauppsättningen för styrning.
1. [Skapa ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html) policyer som tvingar fram styrning av destinationer.

#### Profil/identitet

1. [Skapa alla kundspecifika namnutrymmen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Lägg till identiteter i scheman](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Aktivera scheman och datauppsättningar för profilen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Ställ in sammanslagningsprinciper ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html) för olika vyer av kundprofilen [!UICONTROL  i ] realtid (valfritt).
1. Skapa segment för Adobe Campaign.

#### Källor/mål

1. [Importera data till Experience ](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) Platform med hjälp av API:er för direktuppspelning och källkopplingar.1. Konfigurera  [!DNL Azure] blobblagringsmålet för användning med Adobe Campaign.

#### Distribution av mobilappar

1. Implementera Adobe Campaign SDK för Adobe Campaign Classic eller Experience Platform SDK för Adobe Campaign Standard. Om det finns Experience Platform Launch rekommenderar vi att du använder tillägget Adobe Campaign Classic eller Adobe Campaign Standard tillsammans med Experience Platform SDK.


### Journey Orchestration

1. Direktuppspelningsdata som används för att initiera en kundresa måste konfigureras inom Journey Orchestration först för att få ett orkestrerings-ID. Detta Orchestration-ID skickas sedan till utvecklaren för användning vid intag.
1. Konfigurera externa datakällor.
1. Konfigurera anpassade åtgärder.

### Adobe Campaign Standard

1. Konfigurera meddelandemallar med lämpliga personaliseringsinställningar.
1. Konfigurera exportarbetsflöden exportera transaktionsmeddelandeloggar. Rekommendationen är att köras högst var fjärde timme.


## Relaterad dokumentation

* [Adobe Experience Platform-dokumentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Journey Orchestration dokumentation](https://experienceleague.adobe.com/docs/journey-orchestration.html?lang=en)
* [Adobe Campaign Classic-dokumentation](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [Adobe Campaign Standard-dokumentation](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
* [Experience Platform Launch dokumentation](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Experience Platform Mobile SDK-dokumentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
