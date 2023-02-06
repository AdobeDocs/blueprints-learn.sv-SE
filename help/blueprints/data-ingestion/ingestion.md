---
title: Dataförberedelse och intag
description: I det här utkastet visas alla metoder som kan användas för att mata in och förbereda data i Adobe Experience Platform.
solution: Data Collection
kt: 7204
thumbnail: null
exl-id: 21f8a73e-6be7-448e-8cd3-ebee9fc848e1
source-git-commit: 5110ee2a7a079945475055cbcfdabf7cdcaa0ab5
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 4%

---

# Dataförberedelse och intag

Dataförberedelse och matningsutkast omfattar alla metoder som kan användas för att förbereda och importera data till Adobe Experience Platform.

Datakompilering innefattar mappning av källdata till XDM-schema (Experience Data Model). Det omfattar även att utföra dataomvandlingar, inklusive datumformatering, fältdelning/sammanfogning/konverteringar samt att sammanfoga/skriva in poster på nytt. Med hjälp av dataförberedelser kan kunddata sammanställas för att ge en sammanställd/filtrerad analys, inklusive rapportering eller förberedelse av data för sammansättning av kundprofiler/datavetenskap/aktivering.

## Arkitektur

<img src="../experience-platform/assets/aep_data_flow.svg" alt="Referensarkitektur för dataförberedelse och matningsutkast" style="width:90%; border:1px solid #4a4a4a; margin-bottom: 15px;" class="modal-image" />

## Skyddsförslag för dataöverföring

Bilden nedan visar de genomsnittliga prestandagarantierna och latensen för dataöverföring till Adobe Experience Platform.

<img src="../experience-platform/assets/aep_data_flow_guardrails.svg" alt="Experience Platform dataflöde" style="border:1px solid #4a4a4a; margin-bottom: 15px;" width="90%" class="modal-image" />

## Metoder för dataöverföring

| Inmatningsmetoder | Beskrivning |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Webb/mobil SDK | Svarstid:<ul><li>Realtid - samma sidsamling till Edge Network</li><li>Direktuppspelning till profil ~1 minut</li><li>Direktuppspelat intag till datasjön (mikrobatteri ~15 minuter)</ul>Dokumentation: <ul><li>[Web SDK](https://experienceleague.adobe.com/docs/web-sdk.html)</li><li>[Självstudiekurs om att implementera Adobe Experience Cloud med webb-SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html)</li><li>[Mobile SDK](https://experienceleague.adobe.com/docs/mobile.html?lang=en)</li><li>[Implementera Adobe Experience Cloud i mobilappar, genomgång](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html)</li></ul> |
| Direktuppspelningskällor | [Direktuppspelningskällor](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en#connectors)<br>Svarstid:<ul><li>Realtid - samma sidsamling till Edge Network</li><li>Direktuppspelning till profil ~1 minut</li><li>Direktuppspelat intag till datasjön (mikrobatteri ~15 minuter)</li></ul> |
| API för direktuppspelning | [Edge Network Server API (rekommenderas)](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/data-collection/interactive-data-collection.html) - har stöd för Edge Services inklusive Edge Segmentation och <br>[Huvudtjänst-API för datainsamling](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/streaming/http.html) - saknar stöd för Edge Services, dirigeringar direkt till navet.<br>Svarstid:<ul><li>Realtid - samma sidsamling till Edge Network</li><li>Direktuppspelning till profil ~1 minut</li><li>Direktuppspelat intag till datasjön (mikrobatteri ~15 minuter)</li><li>7 GB/timme</li></ul>[Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=en#what-can-you-do-with-streaming-ingestion%3F) |
| ETL-verktyg | Använd ETL-verktygen för att modifiera och omvandla företagsdata innan de förs in i Experience Platform.<br><br>Svarstid:<ul><li>Tidsinställningen beror på den externa ETL-verktygets schemaläggning, och då tillämpas standardrutorna för intag baserat på den metod som används för intaget.</li></ul> |
| Batchkällor | Schemalagd hämtning från källor<br>Svarstid: ~ 200 GB/timme<br><br>[Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en#connectors)<br>[Video Tutorials](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/overview.html) |
| Batch-API | Svarstid:<ul><li>Batchintag till profil beroende på storlek och trafikbelastning ~45 minuter</li><li>Tillförsel av data till sjön i batch beroende på storlek och trafikbelastning</li></ul>[Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=en#batch) |
| Adobe Application Connectors | Automatiskt importera data som hämtas från Adobe Experience Cloud-program<ul><li>Adobe Analytics: [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=en#connectors) och [Videosjälvstudiekurs](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html)</li><li>Audience Manager: [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=en#connectors) och [Videosjälvstudiekurs](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-aam.html)</li></ul> |


## Metoder för dataförberedelse

| Metoder för dataförberedelse | Beskrivning |
|------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Externt ETL-verktyg ([!DNL Snaplogic], [!DNL Mulesoft], [!DNL Informatica], osv.) | Utför komplexa omvandlingar med ETL-verktyg och använd Experience Platform som standard [!UICONTROL Flödestjänst] API:er eller källanslutningar för import av resulterande data. |
| [!UICONTROL Frågetjänst] - Dataprep | Sammanfogar, delar, sammanfogar, omformar, frågar och filtrerar data till en ny datauppsättning. Använda Skapa tabell som markerad (CTAS) <br>[Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=en#sql) |
| Funktionerna XDM-mappning och dataförberedelse (strömning och batch) | Mappa källattribut i CSV- eller JSON-format till XDM-attribut vid förtäring av Experience Platform.<br>Beräkna funktioner för data när de importeras. d.v.s. dataformatering, uppdelning, sammanfogning osv.<br>[Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/data-prep/home.html?lang=en) |

## Relaterade blogginlägg

* [[!DNL Leveraging External Data Platforms in Adobe Experience Platform Journey Orchestration]](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17?source=your_stories_page-------------------------------------)
* [[!DNL High Throughput Ingestion with Iceberg]](https://medium.com/adobetech/high-throughput-ingestion-with-iceberg-ccf7877a413f?source=your_stories_page-------------------------------------)
* [[!DNL Query Service Tricks in Adobe Experience Platform (Writing Queries and Storing Derived Datasets)]](https://medium.com/adobetech/query-service-tricks-in-adobe-experience-platform-writing-queries-and-storing-derived-datasets-eaee0d6d683e?source=your_stories_page-------------------------------------)
* [[!DNL Digging into Adobe Experience Platform's Experience Data Model to More Fully Understand the Power of Real-time Customer Profile]](https://medium.com/adobetech/digging-into-adobe-experience-platforms-experience-data-model-to-more-fully-understand-the-power-3e109271e04f?source=your_stories_page-------------------------------------)
* [[!DNL An Introductory Look at Exploratory Data Analysis on Adobe Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a?source=your_stories_page-------------------------------------)
* [[!DNL Modeling XDM Data for Data Science at Scale on Adobe Experience Platform]](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7?source=your_stories_page-------------------------------------)
