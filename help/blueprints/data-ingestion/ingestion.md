---
title: Dataförberedelse och matningsutkast
description: I den här översikten visas alla metoder som kan användas för att importera och förbereda data i Adobe Experience Platform.
solution: Experience Platform,Data Collection
kt: 7204
thumbnail: null
exl-id: 21f8a73e-6be7-448e-8cd3-ebee9fc848e1,5c3c94b6-c928-4d93-8b38-f8bd2aad2e68
translation-type: tm+mt
source-git-commit: 77ddc003d4328074ad269de5837a02f5e6d6add5
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---

# Dataförberedelse och matningsutkast

Dataförberedelse och matningsutkast omfattar alla metoder som kan användas för att förbereda och importera data till Adobe Experience Platform.

Datakiveringen inkluderar mappning av källdata till XDM-schema (Experience Data Model). Det omfattar även att utföra dataomvandlingar, inklusive datumformatering, fältdelning/sammanfogning/konverteringar samt att sammanfoga/skriva in poster på nytt. Med hjälp av dataförberedelser kan kunddata sammanställas för att ge en sammanställd/filtrerad analys, inklusive rapportering eller förberedelse av data för sammansättning av kundprofiler/datavetenskap/aktivering.

## Arkitektur

<img src="assets/dataingest.svg" alt="Referensarkitektur för dataförberedelse och matningsutkast" style="border:1px solid #4a4a4a" />

## Metoder för datainmatning

| Inmatningsmetoder | Beskrivning |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Webb/mobil SDK | Svarstid:<ul><li>Realtid - samma sidsamling till Edge Network</li><li>Direktuppspelning till profil ~1 minut</li><li>Direktuppspelat intag till datasjön (mikrobatteri ~15 minuter)</ul>Dokumentation: <ul><li>[Web SDK](https://experienceleague.corp.adobe.com/docs/web-sdk.html)</li><li>[Mobile SDK](https://experienceleague.adobe.com/docs/mobile.html?lang=en)</li></ul> |
| Direktuppspelningskällor | Svarstid:<ul><li>Realtid - samma sidsamling till Edge Network</li><li>Direktuppspelning till profil ~1 minut</li><li>Direktuppspelat intag till datasjön (mikrobatteri ~15 minuter)</li></ul>[Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en#connectors) |
| API för direktuppspelning | Svarstid:<ul><li>Realtid - samma sidsamling till Edge Network</li><li>Direktuppspelning till profil ~1 minut</li><li>Direktuppspelat intag till datasjön (mikrobatteri ~15 minuter)</li><li>7 GB/timme</li></ul>[Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=en#what-can-you-do-with-streaming-ingestion%3F) |
| ETL-verktyg | Använd ETL-verktygen för att modifiera och omvandla företagsdata innan de förs in i Experience Platform.<br><br>Svarstid:<ul><li>Tidsinställningen beror på den externa ETL-verktygets schemaläggning, och då tillämpas standardrutorna för intag baserat på den metod som används för intaget.</li></ul> |
| Batchkällor | Schemalagd hämtning från källor<br>Latens: ~ 200 GB/timme<br><br>[Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en#connectors)<br>[Video Tutorials](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/overview.html) |
| Batch-API | Svarstid:<ul><li>Batchintag till profil beroende på storlek och trafikbelastning ~45 minuter</li><li>Tillförsel av data till sjön i batch beroende på storlek och trafikbelastning</li></ul>[Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=en#batch) |
| Adobe Application Connectors | Automatiskt importera data som hämtas från Adobe Experience Cloud-program<ul><li>Adobe Analytics: [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=en#connectors) och [Videosjälvstudiekurs](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html)</li><li>Audience Manager: [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=en#connectors) och [Videosjälvstudiekurs](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-aam.html)</li></ul> |


## Metoder för dataförberedelse

| Metoder för dataförberedelse | Beskrivning |
|------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Data Science Workspace - Data Prep | Modelldriven omvandling, skriptbaserad omvandling.<br>[Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=en) |
>[!NOTE]
>
>| Externt ETL-verktyg ([!DNL Snaplogic], [!DNL Mulesoft], [!DNL Informatica] och så vidare) | Utför komplexa omformningar i ETL-verktygen och använd Experience Platform-källans API:er eller kopplingar för att importera resulterande data.                                                                                                                                                               |

| Frågetjänst - Datapreposition                                  | Sammanfogar, delar, sammanfogar, omformar, frågar och filtrerar data till en ny datauppsättning. Använda Skapa tabell som markerad (CTAS) <br>[Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=en#sql)                                                                       |
| XDM-mappning och dataförberedelsefunktioner (strömning och batch)     | Mappa källattribut i CSV- eller JSON-format till XDM-attribut vid förtäring av Experience Platform.<br>Beräkna funktioner för data när de importeras. d.v.s. dataformatering, uppdelning, sammanfogning osv.<br>[Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/data-prep/home.html?lang=en) |

## Relaterade blogginlägg

* [Utnyttja externa dataplattformar i Adobe Experience Platform Journey Orchestration](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17?source=your_stories_page-------------------------------------)
* [Intag med hög genomströmning med Iceberg](https://medium.com/adobetech/high-throughput-ingestion-with-iceberg-ccf7877a413f?source=your_stories_page-------------------------------------)
* [Frågetjänsttrick i Adobe Experience Platform (skrivfrågor och lagring av härledda datauppsättningar)](https://medium.com/adobetech/query-service-tricks-in-adobe-experience-platform-writing-queries-and-storing-derived-datasets-eaee0d6d683e?source=your_stories_page-------------------------------------)
* [Förstå kraften i kundprofilen i realtid genom att utnyttja Adobe Experience Platform Experience Data Model](https://medium.com/adobetech/digging-into-adobe-experience-platforms-experience-data-model-to-more-fully-understand-the-power-3e109271e04f?source=your_stories_page-------------------------------------)
* [En introduktion till undersökande dataanalys i Adobe Experience Platform](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a?source=your_stories_page-------------------------------------)
* [Modeling XDM Data for Data Science at Scale on Adobe Experience Platform](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7?source=your_stories_page-------------------------------------)
