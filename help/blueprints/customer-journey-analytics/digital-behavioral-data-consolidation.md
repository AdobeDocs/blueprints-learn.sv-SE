---
title: Scenario för digital beteendedatakonsolidering
description: Analysera och extrahera insikter från kundinteraktioner under hela kundresan.
solution: Experience Platform, Customer Journey Analytics, Data Collection
kt: 7208
translation-type: tm+mt
source-git-commit: e1a9881996a181310bdc32cb083e4c5654139bf0
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---


# Scenario för digital beteendedatakonsolidering

Få en samlad bild av kundernas beteende i olika kanaler genom att samla data från olika webb-, mobil- och offlineegenskaper.

## Användningsexempel

* Analysera kundinteraktioner på både dator och mobil för att förstå kundbeteenden och få insikter för att optimera digitala kundupplevelser.
* Analysera kundinteraktioner över alla kanaler, inklusive digitala och offlinekanaler som supportinteraktioner och butiksköp för att bättre förstå och optimera kundresan. 

## Program

* Adobe Experience Platform
* Customer Journey Analytics
* Adobe Analytics (valfritt)

## Integrationsmönster

* Adobe Experience Platform → Customer Journey Analytics
* Adobe Analytics → Adobe Experience Platform → Customer Journey Analytics

## Arkitektur

<img src="assets/CJA.svg" alt="Referensarkitektur för Customer Journey Analytics Blueprint" style="border:1px solid #4a4a4a" />

## Guardrails

Dataintag i Customer Journey Analytics:

* Intag av data till sjö: API ~ 7 GB/timme, källanslutning ~ 200 GB/timme, direktuppspelning till sjö ~ 15 minuter, Adobe Analytics källanslutning till sjö ~ 45 minuter.
* Efter att data har publicerats till datasjön kan det ta upp till 90 minuter att bearbeta dem i Customer Journey Analytics.

## Implementeringssteg

1. Konfigurera datauppsättningar och scheman.
1. Importera data till Platform.
Data måste hämtas till plattformen innan de kan bearbetas till Customer Journey Analytics.
1. Analysera händelsedatamängder för flera kanaler som ska analyseras tillsammans för att se till att de har ett gemensamt namnområdes-ID eller att de eftersöks med hjälp av den fältbaserade sammanfogningsfunktionen i Customer Journey Analytics. 

   >[!NOTE]
   >
   >Customer Journey Analytics använder för närvarande inte profiltjänsten eller identitetstjänsten Experience Platform för sammanfogning.

1. Utför en anpassad dataförberedelse eller användning av fältbaserad identitetssammanfogning på data för att säkerställa en gemensam nyckel över tidsseriens datauppsättningar som ska importeras till Customer Journey Analytics.
1. Ge sökdata ett primärt ID som kan kopplas till ett fält i händelsedata. Räknas som rader i licensiering.
1. Ange samma primära ID för profildata som det primära ID:t för händelsedata.
1. Konfigurera en dataanslutning för import av data från Experience Platform till Customer Journey Analytics. Efter att data har landat i datasjön bearbetas de till Customer Journey Analytics inom 90 minuter.
1. Konfigurera en datavy för anslutningen för att välja de specifika dimensioner och mått som ska inkluderas i vyn. Attribution- och allokeringsinställningar konfigureras också i datavyn. Dessa inställningar beräknas vid rapporttillfället.
1. Skapa ett projekt för att konfigurera kontrollpaneler och rapporter i Analysis Workspace.

## Överväganden gällande implementering

### Överväganden om identitetskorrigering

* De tidsseriedata som ska förenas måste ha samma ID-namnutrymme på alla poster.
* Unionsprocessen för att sammanfoga olika datauppsättningar kräver en gemensam primärnyckel för personen/enheten i alla datauppsättningar.
* Sekundära nyckelbaserade föreningar stöds för närvarande inte.
* Den fältbaserade identitetssammanfogningsprocessen gör det möjligt att skriva in identiteter på nytt i rader baserat på efterföljande tillfälliga ID-poster, till exempel ett autentiserings-ID. Detta gör det möjligt att lösa olika poster till ett enda ID för analys på personnivå i stället för på enhets- eller cookienivå.
* Sömningen sker en gång i veckan, med repriser efter stygn.

## Vanliga frågor

* Vilka konsekvenser får datamodellerna i Customer Journey Analytics?

   Objekt och attribut i samma XDM-fält sammanfogas till en dimension i Customer Journey Analytics. Till  sammanfoga flera attribut från olika datauppsättningar i samma Customer Journey Analytics-dimension, datauppsättningarna ska referera till samma XDM-fält eller -schema.

## Relaterad dokumentation

* [Customer Journey Analytics produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/customer-journey-analytics.html)
* [Customer Journey Analytics dokumentation](https://experienceleague.adobe.com/docs/customer-journey-analytics.html)
* [Självstudiekurser för Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/overview.html)



