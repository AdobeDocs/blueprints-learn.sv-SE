---
title: Journey Optimizer - Triggered Messaging och Adobe Experience Platform Blueprint
description: Utför utlösta meddelanden och upplevelser med Adobe Experience Platform som ett centralt nav för strömmande data, kundprofiler och segmentering.
solution: Journey Optimizer
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: d7901280f1bc23e6d37bcb285f20343c5ed8b46e
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 1%

---

# Journey Optimizer-ritningar

Adobe Journey Optimizer är ett särskilt utformat system för marknadsföringsteam som i realtid kan reagera på kundbeteenden och möta dem där de befinner sig. Funktioner för datahantering har flyttats till Adobe Experience Platform, vilket gör att marknadsföringsteamen kan fokusera på vad de gör bäst: att skapa kundresor och personaliserade konversationer i världsklass.  Denna plan beskriver programmets tekniska funktioner och ger en djupdykning i de olika arkitektoniska komponenterna som Adobe Journey Optimizer består av.

<br>

## Användningsexempel

* Utlösta meddelanden
* Välkomstbekräftelse och registreringsbekräftelse
* Kundvagn och blankettinlämning
* Platsutlösta meddelanden
* Erfarenheter på stadion
* Resor och turism före ankomst och vistelse

<br>

## Arkitektur

<img src="assets/ajo-architecture.svg" alt="Referensarkitektur Journey Optimizer - utkast" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Scenarier

| Scenario | Beskrivning | Funktioner |
| :-- | :--- | :--- |
| [Meddelanden från tredje part](3rd-party-messaging.md) | Visar hur Adobe Journey Optimizer kan användas med tredjeparts meddelandesystem för att samordna och skicka personaliserad kommunikation | Leverera personlig kommunikation direkt till kunderna när de interagerar med ert varumärke eller företag<br><br>Att tänka på:<br><ul><li>Tredjepartssystem måste ha stöd för innehavartoken för autentisering</li><li>Inget stöd för statiska IP-adresser på grund av multi-tenant-arkitektur</li><li>Var medveten om arkitektoniska begränsningar för system från tredje part när det gäller API-anrop per sekund.  Kunderna kan behöva köpa ytterligare volymer från tredjepartsleverantören för supportvolym från Journey Optimizer</li><li>Stöder inte beslutshantering i meddelanden eller nyttolaster</li></ul> |

<br>

## Integreringsmönster

| Integrering | Beskrivning | Funktioner |
| :-- | :--- | :--- |
| [Journey Optimizer med Adobe Campaign](ajo-and-campaign.md) | Visar hur du kan använda Adobe Journey Optimizer för att orkestrera 1:1-upplevelser med hjälp av kundprofilen i realtid och utnyttja Adobe Campaign transaktionsmeddelandesystem för att skicka meddelandet | Utnyttja Journey Optimizer kundprofil i realtid och kraften i att orkestrera i det ögonblick upplevelserna inträffar, samtidigt som ni använder Adobe Campaign inbyggda funktioner för realtidsmeddelanden för att kommunicera på sista milen<br><br>Att tänka på:<br><ul><li>Kampanjprogrammet måste finnas i antingen v7 build >21.1 eller v8</li><li>Meddelandegenomströmning</li><ul><li>Campaign v7 - upp till 50 000 per timme</li><li>Campaign v8 - upp till 1 MB per timme</li><li>Campaign Standard - upp till 50 000 per timme</li></ul><li>Ingen begränsning utförs, så användningsfall kräver teknisk kontroll av en företagsarkitekt</li><li>Inget stöd för att använda beslutsstöd i ett meddelande som skickas av Campaign</li></ul> |

<br>

## Förutsättningar

Adobe Experience Platform

* Scheman och datauppsättningar måste konfigureras i systemet innan du kan konfigurera Journey Optimizer-datakällor
* För Experience Event-klassbaserade scheman lägger du till fältgruppen &#39;Orchestration eventID&#39; när du vill att en händelse som inte är en regelbaserad händelse ska aktiveras
* För enskilda profilklassbaserade scheman lägger du till fältgruppen Profiltestinformation för att kunna läsa in testprofiler som ska användas med Journey Optimizer

E-post

* Måste ha en underdomän klar att användas för att skicka meddelanden
* Underdomänen kan antingen delegeras helt till Adobe (rekommenderas) eller CNAME kan användas för att peka mot Adobe-specifika DNS-servrar (anpassad)
* Google TXT-post krävs för varje underdomän för att säkerställa god levererbarhet

Mobil pensel

* Kunden måste ha en mobilutvecklare tillgänglig för att kunna bygga appen
* Adobe Experience Platform Mobile SDK

<br>

## Guardrails

[Journey Optimizer Guardrails Product Link](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=en)

Observera dessa som inte finns med på länken ovan:

* Gruppsegment - måste säkerställa att ni förstår den dagliga volymen av kvalificerade användare och ser till att målsystemet kan hantera den explosionsartade genomströmningen per resa och över alla resor
* Strömmande segment - måste säkerställa att den initiala höjningen av profilkvalifikationer kan hanteras tillsammans med den dagliga strömmande kvalificerande volymen per resa och över alla resor
* Inbyggt stöd för Beslutshantering endast i meddelanden (inga anpassade åtgärder)
* Meddelandetyper som stöds:
   * E-post
   * Push (FCM / APNS)
   * Anpassade åtgärder (via Rest API)
* Utgående integreringar med system från tredje part
   * Inget stöd för en enda statisk IP eftersom vår infrastruktur är multi-tenant (måste tillåtelselista alla IP-adresser för datacenter)
   * Endast POST- och PUT-metoder stöds för anpassade åtgärder
   * Autentisering via användar-/pass- eller auktoriseringstoken
* Det går inte att paketera och flytta enskilda komponenter i Adobe Experience Platform eller Journey Optimizer mellan olika sandlådor. Måste implementeras på nytt i nya miljöer

### Skyddsförslag för dataöverföring

<img src="../experience-platform/deployment/assets/aep_data_flow_guardrails.svg" alt="Experience Platform dataflöde" style="border:1px solid #4a4a4a" width="85%" class="modal-image" />

<br>

### Aktiveringsskydd

<img src="../experience-platform/deployment/assets/AJO_guardrails.svg" alt="Referensarkitektur Journey Optimizer - utkast" style="width:85%; border:1px solid #4a4a4a" class="modal-image" />

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

#### Källor/destinationer

1. [Infoga data i Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) med direktuppspelnings-API:er och källanslutningar.

### Journey Optimizer

1. Konfigurera datakällan för Experience Platform och bestäm vilka fält som ska cachas som en del av de profileStreaming-data som används för att initiera en kundresa måste konfigureras i Journey Optimizer först för att få ett orchestration-ID. Detta orkestrerings-ID skickas sedan till utvecklaren för användning vid förtäring
1. Konfigurera externa datakällor.
1. Konfigurera anpassade åtgärder.

### Mobil push-konfiguration

1. Implementera Experience Platform Mobile SDK för att samla in push-tokens och inloggningsinformation för att koppla tillbaka till kända kundprofiler
1. Utnyttja Adobe-taggar och skapa en mobil egenskap med följande tillägg:
1. Adobe Journey Optimizer
1. Adobe Experience Platform Edge Network
1. Identitet för Edge Network
1. Mobile Core
1. Se till att du har en dedikerad datastam för mobilappsdistributioner jämfört med webbdistributioner
1. Mer information finns i [Adobe Journey Optimizer Mobile Guide](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer)


## Relaterad dokumentation

* [Experience Platform dokumentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Dokumentation för Experience Platform-taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en)
* [Experience Platform Mobile SDK-dokumentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
* [Journey Optimizer-dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=en)
* [Journey Optimizer produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
