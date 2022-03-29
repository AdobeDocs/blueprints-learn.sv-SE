---
title: Custom Data Science for Profile Enrichment Blueprint
description: Denna plan visar hur Adobe Experience Platform Data Science Workspace kan använda data i Experience Platform för att utbilda, driftsätta och göra poäng i modeller för maskininlärning.
solution: Data Collection
kt: 7203
exl-id: e5ec6886-4fa4-4c9b-a2d8-e843d7758669,f0efaf3c-6c4f-47c3-ab8a-e8e146dd071c
source-git-commit: 1d286f4dabe71f359c14a88c91f306ea443646a6
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Custom Data Science for Profile Enrichment Blueprint

Custom Data Science for Profile Enrichment Blueprint visar hur data i Adobe Experience Platform kan användas i [!UICONTROL Datavetenskapens arbetsyta] för att utbilda, driftsätta och göra poäng i modeller för maskininlärning. Dessa modeller kan direkt mata ut till en datauppsättning som är aktiverad för [!UICONTROL Kundprofil i realtid] ytterligare berika kundprofilerna. Dessa insikter kan sedan hanteras för personalisering. Exempel på maskininlärningsinsikter är poängsättning för livstid, produkt- och kategoritillhörighet, benägenhet att konvertera eller benägenhet att försvinna.

## Användningsexempel

* Extrahera insikter och upptäck mönster från kunddata i Experience Platform. Modeller för utbildning och poäng utifrån dessa data.
* Förbättra [!UICONTROL Kundprofil i realtid] med modellbaserade insikter och attribut för mer detaljerad personalisering och optimerade resor.
* Train- och Score-modeller för att fastställa kundinsikter som kundens livstidsvärde, benägenhet att konvertera eller tappa plats, produkt- och innehållstillhörighet samt engagemangsmätningar.

## Arkitektur

<img src="assets/data_science.svg" alt="Referensarkitektur för Custom Data Science for Profile Enrichment Blueprint" style="width:80%; border:1px solid #4a4a4a" />

## Implementeringssteg

1. [Skapa scheman](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) för data som ska importeras.
1. [Skapa datauppsättningar](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) för data som ska importeras.
1. [Ingrediera data](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) till Experience Platform.
1. [Skapa en DSW-anteckningsbok](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/load-data-in-jupyterlab-notebooks.html?lang=en).
1. Välj ett språk. Python och PySpark stöds.
1. [Författarmodell](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/recipe-builder-template.html?lang=en) i anteckningsboken.
1. [Tåg modellen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/schedule-training-scoring.html?lang=en).
1. [Visa modellen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/schedule-training-scoring.html?lang=en) för att generera prognoser med måldata.
1. [Aktivera datamängden för modellresultat för profilen om modellresultaten skickas till [!UICONTROL Kundprofil i realtid]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/dsw-profile-segmentation.html?lang=en).

## Relaterad dokumentation

* [Adobe Experience Platform Intelligence - produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [[!UICONTROL Datavetenskapens arbetsyta] dokumentation](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=en)
* [[!UICONTROL Datavetenskapens arbetsyta] självstudiekurser](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/understanding-data-science-workspace.html)

## Relaterade blogginlägg

* [[!DNL Simplifying the Data Science Lifecycle with Adobe Platform Experience]](https://medium.com/adobetech/simplifying-the-data-science-lifecycle-with-adobe-platform-experience-8ea4f056d82f)
* [[!DNL Content and Commerce AI: Personalizing Your Interactions with Customers Through Content Intelligence]](https://medium.com/adobetech/content-and-commerce-ai-personalizing-your-interactions-with-customers-through-content-intelligence-dc182601deab)
* [[!DNL Gaining a Deeper Understanding of Churn Using Data Science Workspace]](https://medium.com/adobetech/gaining-a-deeper-understanding-of-churn-using-data-science-workspace-18a2190e0cf3)
* [[!DNL Understanding Data Science In Adobe Experience Platform]](https://medium.com/adobetech/understanding-data-science-in-adobe-experience-platform-5bce5a17b42)
* [[!DNL An Introductory Look at Exploratory Data Analysis on Adobe Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a)
* [[!DNL Cutting Across Adobe Experience Products with Machine Learning to Elevated User Experience]](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
* [[!DNL Modeling XDM Data for Data Science at Scale on Adobe Experience Platform]](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7)
* [[!DNL Segmentation.AI: Automated Audience-Clustering-as-a-Service in Adobe Experience Platform]](https://medium.com/adobetech/segmentation-ai-automated-audience-clustering-as-a-service-in-adobe-experience-platform-261f4099462c)
* [[!DNL Reimagining Jupyter Notebooks for Enterprise Scale]](https://medium.com/adobetech/reimagining-jupyter-notebooks-for-enterprise-scale-8bc6340d504a)
* [[!DNL Accelerate Intelligent Insights with Adobe Experience Platform Data Science Workspace]](https://medium.com/adobetech/accelerate-intelligent-insights-with-adobe-experience-platform-data-science-workspace-89538bacbbea)
* [[!DNL A Preview of Time Series Forecasting with Adobe Experience Platform]](https://medium.com/adobetech/preview-of-time-series-forecasting-with-adobe-experience-platform-38a2fc778e89)
* [[!DNL Cutting Across Adobe Experience Products with Machine Learning to Elevated User Experience]](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
