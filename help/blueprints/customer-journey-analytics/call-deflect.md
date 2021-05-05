---
title: Analysutkast för anropsavböjning
description: Analysera kundbeteendet innan de kontaktar kundtjänsten.
solution: Experience Platform, Customer Journey Analytics
kt: 7209
exl-id: 13593c1c-4c58-4b8a-aa6c-7530fd679a14
translation-type: tm+mt
source-git-commit: 9fe9d67c5f97b633e45155bd54e2006f1b797332
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# Analysutkast för anropsavböjning

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

## Implementeringssteg

1. [Skapa ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html) scheman för data som ska importeras.
1. [Skapa ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) datauppsättningar för data som ska importeras.
1. [Ingest ](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) data into Experience Platform.
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
