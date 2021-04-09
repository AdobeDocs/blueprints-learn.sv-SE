---
title: Utlöst meddelande och Adobe Experience Platform Blueprint
description: Kör triggade meddelanden och upplevelser med Adobe Experience Platform som ett centralt nav för strömmande data, kundprofiler och segmentering.
solution: Experience Platform, Campaign, Journey Orchestration
kt: 7197
exl-id: 97831309-f235-4418-bd52-28af815e1878
translation-type: tm+mt
source-git-commit: 009a55715b832c3167e9a3413ccf89e0493227df
workflow-type: tm+mt
source-wordcount: '607'
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

### Campaign Standard

* Kan endast hantera 14 tps (50 000 per timme) i genomströmning
* Segmentmedlemsinitierade resor stöds inte
* Reaktionshändelser för öppna/klickade transaktionsmeddelanden stöds i Journey Orchestration.
* Loggar för transaktionsmeddelanden synkroniseras för närvarande inte direkt till Experience Platform, vilket kräver en manuell konfiguration. Du bör exportera loggar var fjärde timme.


## Implementeringssteg

### Adobe Experience Platform

#### Schema/datauppsättningar

1. Konfigurera enskilda profiler, upplevelsehändelser och scheman för flera enheter i Experience Platform baserat på kunddata.
1. Skapa kampanjscheman för följande: broadLog, trackingLog, icke-levererbara adresser och profilinställningar (valfritt).
1. Lägg till dataanvändningsetiketter i datauppsättningen för styrning.
1. Skapa profiler för att genomdriva styrning av destinationer.

#### Profil/identitet

1. Skapa alla kundspecifika namnutrymmen.
1. Lägg till identiteter i scheman.
1. Aktivera scheman och datauppsättningar för profilen.
1. Ställ in kopplingsregler för olika vyer av [!UICONTROL Kundprofil för realtid] (valfritt).
1. Skapa segment för kampanjanvändning.

#### Källor/mål

1. Importera data till Experience Platform med hjälp av API:er för direktuppspelning och källanslutningar.
1. Konfigurera [!DNL Azure]-lagringsmålet för blob för användning med Campaign.

#### Distribution av mobilappar

1. Implementera Campaign SDK för Campaign Classic eller Experience Platform SDK för Campaign Standard. Om det finns Experience Platform Launch rekommenderar vi att du använder tillägget Campaign Classic/Standard tillsammans med Experience Platform SDK.


### Journey Orchestration

1. Direktuppspelningsdata som används för att initiera en kundresa måste konfigureras inom Journey Orchestration först för att få ett orkestrerings-ID. Detta Orchestration-ID skickas sedan till utvecklaren för användning vid intag.
1. Konfigurera externa datakällor.
1. Konfigurera anpassade åtgärder.

### Campaign Standard

1. Konfigurera meddelandemallar med lämpliga personaliseringsinställningar.
1. Konfigurera exportarbetsflöden exportera transaktionsmeddelandeloggar. Rekommendationen är att köras högst var fjärde timme.


## Relaterad dokumentation

* [Adobe Experience Platform-dokumentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Journey Orchestration dokumentation](https://experienceleague.adobe.com/docs/journey-orchestration.html?lang=en)
* [Campaign Classic dokumentation](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
* [Experience Platform Launch dokumentation](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Experience Platform Mobile SDK-dokumentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
