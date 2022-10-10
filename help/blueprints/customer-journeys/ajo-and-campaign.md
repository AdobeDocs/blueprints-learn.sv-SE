---
title: Journey Optimizer med Adobe Campaign Blueprint
description: Visar hur Adobe Journey Optimizer kan användas med Adobe Campaign för att skicka meddelanden internt genom att använda meddelandeservern i Campaign
solution: Journey Optimizer, Campaign, Campaign v8, Campaign Classic v7, Campaign Standard
exl-id: 076446a9-dfb9-464c-a04f-6864b8cb7b48
source-git-commit: 6901596cbb661ffa8cf57c6ae958db1978bf1520
workflow-type: tm+mt
source-wordcount: '504'
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
* Beslutshantering stöds inte
* Affärshändelser stöds inte
* Utgående integreringar med system från tredje part
   * Inget stöd för en enda statisk IP eftersom vår infrastruktur är multi-tenant (måste tillåtelselista alla IP-adresser för datacenter)
   * Endast POST- och PUT-metoder stöds för anpassade åtgärder
   * Autentiseringsstöd: token | lösenord | OAuth2
* Det går inte att paketera och flytta enskilda komponenter i Adobe Experience Platform eller Journey Optimizer mellan olika sandlådor. Måste implementeras på nytt i nya miljöer

<br>

### Kampanjintegrering

Om du vill ha mer information om hur du integrerar med en viss version av Adobe Campaign och Adobe Journey Optimizer läser du i motsvarande guide för respektive Adobe Campaign-version.

* [Adobe Journey Optimizer &amp; Campaign v7](ajo-and-campaign-v7.md)
* [Adobe Journey Optimizer &amp; Campaign v8](ajo-and-campaign-v8.md)