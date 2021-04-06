---
title: Custom Data Science for Profile Enrichment Blueprint
description: Denna plan visar hur Adobe Experience Platform Data Science Workspace kan använda data i Experience Platform för att utbilda, driftsätta och göra poäng i modeller för maskininlärning.
solution: Experience Platform,Data Collection
kt: 7203
exl-id: e5ec6886-4fa4-4c9b-a2d8-e843d7758669,f0efaf3c-6c4f-47c3-ab8a-e8e146dd071c
translation-type: tm+mt
source-git-commit: 7a097d7579d0e217ee5c6b469856bf786b17e6cb
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# Custom Data Science for Profile Enrichment Blueprint

Denna skiss visar hur data i Adobe Experience Platform används av Data Science Workspace för att utbilda, driftsätta och poängsätta modeller för maskininlärningsinsikter. Dessa modeller kan direkt matas ut till en datauppsättning som är aktiverad för kundprofil i realtid. Exempel på maskininlärningsinsikter är livstidsvärde, produkt- och kategoritillhörighet, benägenhet att konvertera eller benägenhet att försvinna.

## Användningsexempel

* Extrahera insikter och upptäck mönster från kunddata i Experience Platform. Modeller för utbildning och poäng utifrån dessa data.
* Berika kundprofilen i realtid med modellstyrda insikter och attribut för mer detaljerad personalisering och optimerad reseoptimering.
* Train- och Score-modeller för att fastställa kundinsikter som kundens livstidsvärde, benägenhet att konvertera eller tappa plats, produkt- och innehållstillhörighet samt engagemangsmätningar.

## Scenarier

| Scenario | Scenariobeskrivning | Experience Cloud-program |
|---|---|---|
| Experimentell datavetenskap | <ul><li>Identifiera signaler, fullständighet, korrekthet i data</li><li>Upptäck nya insikter med datavetenskap</li></ul> | <ul><li>Experience Platform Intelligence</li></ul> |
| Profilberikning med AI/ML<br> - batch | <ul><li>Upptäck, skapa, utbilda, driftsätta, poängsätta och driftsätta modeller.</li><li>Använd modellförutsägelse för profil eller datasjön för batchbaserad aktivering.</li></ul> | <ul><li>Experience Platform Intelligence</li></ul> |

## Arkitektur

<img src="assets/datascience.svg" alt="Referensarkitektur för Custom Data Science for Profile Enrichment Blueprint" style="border:1px solid #4a4a4a" />

## Implementeringssteg

1. Skapa scheman och datauppsättningar.
1. Importera data till Experience Platform.
1. Skapa en DSW-anteckningsbok.
1. Välj ett språk. Python och PySpark stöds.
1. Författarmodell i anteckningsbok.
1. Tåla modellen.
1. Testa modellen för att generera prognoser med måldata.
1. Aktivera modellresultatdatauppsättningen för profilen om modellresultat överförs till kundprofilen i realtid.

## Relaterad dokumentation

* [Adobe Experience Platform Intelligence - produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Dokumentation för Data Science Workspace](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=en)
* [Självstudiekurser för datavetenskap](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/understanding-data-science-workspace.html)

## Relaterade blogginlägg

* [Förenkla datavetenskapens livscykel med Adobe Platform Experience](https://medium.com/adobetech/simplifying-the-data-science-lifecycle-with-adobe-platform-experience-8ea4f056d82f)
* [Innehåll och handel AI: Personalisera interaktionen med kunderna via innehållsintelligens](https://medium.com/adobetech/content-and-commerce-ai-personalizing-your-interactions-with-customers-through-content-intelligence-dc182601deab)
* [Få en djupare förståelse för Churn Using Data Science Workspace](https://medium.com/adobetech/gaining-a-deeper-understanding-of-churn-using-data-science-workspace-18a2190e0cf3)
* [Understanding Data Science in Adobe Experience Platform](https://medium.com/adobetech/understanding-data-science-in-adobe-experience-platform-5bce5a17b42)
* [En introduktion till undersökande dataanalys i Adobe Experience Platform](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a)
* [Skära över Adobe Experience Products med maskininlärning till en bättre användarupplevelse](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
* [Modeling XDM Data for Data Science at Scale on Adobe Experience Platform](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7)
* [Segmentering.AI: Automated Audience-Clustering-as-a-Service i Adobe Experience Platform](https://medium.com/adobetech/segmentation-ai-automated-audience-clustering-as-a-service-in-adobe-experience-platform-261f4099462c)
* [Nya Jupyter-anteckningsböcker för storskalig användning](https://medium.com/adobetech/reimagining-jupyter-notebooks-for-enterprise-scale-8bc6340d504a)
* [Accelerate Intelligent Insights with Adobe Experience Platform Data Science Workspace](https://medium.com/adobetech/accelerate-intelligent-insights-with-adobe-experience-platform-data-science-workspace-89538bacbbea)
* [A Preview of Time Series Forecasting with Adobe Experience Platform](https://medium.com/adobetech/preview-of-time-series-forecasting-with-adobe-experience-platform-38a2fc778e89)
* [Skära över Adobe Experience Products med maskininlärning till en bättre användarupplevelse](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
