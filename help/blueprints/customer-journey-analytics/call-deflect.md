---
title: Anropa scenariot för avböjningsanalys
description: Analysera kundbeteendet innan de kontaktar kundtjänsten.
solution: Experience Platform, Customer Journey Analytics
kt: 7209
translation-type: tm+mt
source-git-commit: e1a9881996a181310bdc32cb083e4c5654139bf0
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---


# Anropa scenariot Resursanalys

Analysera en kunds beteende på både dator och mobil innan de kontaktar kundtjänst. Identifiera möjligheter att förbättra kundresan genom att förstå vilka åtgärder kunderna försöker slutföra, vilket innehåll de ser och vilka termer de söker innan de kontaktar kundsupporten. Ta reda på vilket innehåll och vilka självbetjäningsverktyg som kan förbättras för att hjälpa kunderna att lösa problem utan att behöva ringa in.

## Användningsexempel

* Analysera kundbeteende innan kunderna kontaktar supporten
* Upptäck möjligheter att förbättra självbetjäning

## Program

* Adobe Experience Platform
* Customer Journey Analytics

## Integrationsmönster

* Adobe Experience Platform → Customer Journey Analytics

## Arkitektur

<img src="assets/CJA.svg" alt="Referensarkitektur för Customer Journey Analytics Blueprint" style="border:1px solid #4a4a4a" />

## Guardrails

Dataintag i Customer Journey Analytics:

* Intag av data till sjö: API ~ 7 GB/timme, källanslutning ~ 200 GB/timme, direktuppspelning till sjö ~ 15 minuter, Analytics-källkoppling till sjö ~ 45 minuter.
* Efter att data har publicerats till datasjön kan det ta upp till 90 minuter att bearbeta dem i Customer Journey Analytics.

## Implementeringssteg

1. Konfigurera datauppsättningar och scheman.
1. Importera data till Platform.
Data måste hämtas till plattformen innan de kan hämtas till Customer Journey Analytics.
1. Analysera händelsedatamängder för olika kanaler.
Datauppsättningar som analyseras i en union måste ha ett gemensamt namnområdes-ID eller skrivas in på nytt med fältbaserade sammanfogningsfunktioner för Customer Journey Analytics. 

   >[!NOTE]
   >
   >Customer Journey Analytics använder för närvarande inte profiltjänsten eller identitetstjänsten Experience Platform för sammanfogning.

1. Utför en anpassad dataförberedelse eller användning av fältbaserad identitetssammanfogning på data för att säkerställa en gemensam nyckel över tidsseriens datauppsättningar som ska hämtas till Customer Journey Analytics.
1. Ange ett primärt ID för sökdata, som kan kopplas till ett fält i händelsedata. Räknas som rader i licensiering.
1. Ange samma primära ID för profildata som det primära ID:t för händelsedata.
1. Konfigurera en dataanslutning för import av data från Experience Platform till Customer Journey Analytics. Efter att data har landat i datasjön bearbetas de till Customer Journey Analytics inom 90 minuter.
1. Konfigurera en datavy för anslutningen för att välja de specifika dimensioner och mått som ska inkluderas i vyn. Attribution- och allokeringsinställningar konfigureras också i datavyn. Dessa inställningar beräknas vid rapporttillfället.
1. Skapa ett projekt för att konfigurera kontrollpaneler och rapporter i Analysis Workspace.

## Överväganden gällande implementering

### Överväganden om identitetskorrigering

* De tidsseriedata som ska förenas måste ha samma id-namnutrymme på alla poster. Om du vill ansluta callcenter-data till anonyma enhetsdata måste det digitala ID:t vara knutet till det anropande ID:t. Denna koppling kan ske genom flera möjliga mekanismer:
   * Uppringningsnumret är ett unikt uppringningsnummer för besökaren för den tiden, tillsammans med en uppslagstabell för att spåra relationen.
   * Kräv att användaren autentiserar sig innan support begärs och koppla autentiseringen till en identifierare som bestäms av samtalsagenten (till exempel telefonnummer eller e-post).
   * Använd en startpartner för att skriva in enhetsidentifierare online med kända identifierare kopplade till supportförfrågan.
* Unionsprocessen för att sammanfoga olika datauppsättningar kräver en gemensam primärnyckel för personen/enheten i alla datauppsättningar.
* Sekundära nyckelbaserade föreningar stöds för närvarande inte.
* Den fältbaserade identitetssammanfogningsprocessen gör det möjligt att skriva in identiteter på nytt i rader baserat på efterföljande tillfälliga ID-poster, till exempel ett autentiserings-ID. Med den här processen kan olika poster matchas till ett enda ID för analys på personnivå i stället för på enhets- eller cookienivå.
* Sömningen sker en gång i veckan, med repriser efter stygn.

## Vanliga frågor

* Vilka konsekvenser får datamodellerna i Customer Journey Analytics?

   Objekt och attribut i samma XDM-fält sammanfogas till en dimension i Customer Journey Analytics. Om du vill sammanfoga flera attribut från olika datauppsättningar till samma CJA-dimension, ska datauppsättningarna referera till samma XDM-fält eller -schema.

## Relaterad dokumentation

* [Customer Journey Analytics produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/customer-journey-analytics.html)
* [Customer Journey Analytics dokumentation](https://experienceleague.adobe.com/docs/customer-journey-analytics.html)
* [Självstudiekurser för Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/overview.html)