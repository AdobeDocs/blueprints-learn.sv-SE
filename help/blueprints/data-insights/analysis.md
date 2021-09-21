---
title: Dataanalys och informationsutkast
description: Denna plan visar hur Adobe Experience Platform kan genomföra experimentella frågor och analyser av data som finns i sjön.
solution: Experience Platform
kt: 7207
thumbnail: null
exl-id: a972ea56-d1c8-45da-9044-ed31222a2441
source-git-commit: 5e93d3a5a09a3a20418ec7e563b93d22aef3ddc7
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Dataanalys och informationsutkast

Dataanalys och intelligens omfattar möjligheten inom Adobe Experience Platform att utföra experimentella frågor och analyser av data som finns i sjön.

Experience Platform [!UICONTROL Query Service] tillåter att SQL-frågor utförs på data. [!UICONTROL Data Science ] Workspace möjliggör datautforskande, datavetenskap och maskininlärningsarbetsbelastningar som kan utföras på data.

Dessutom tillåter Experience Platform anslutningar med SQL-klienter, gränssnitt och Business Intelligence-verktyg (BI) från tredje part att ansluta direkt till, komma åt och fråga data i Experience Platform med [!DNL PostgreSQL]-protokollet.

Vissa skyddsutkast gäller för frågans tidsgräns och för den datamängd som ingår i frågeresultatet, vilket beskrivs i ritningsinformationen.

## Användningsexempel

* Interaktiv fråga och sammanställning av data
* Rad- och kolumnåtkomst till inmatade data för utforskning och validering
* Instrumentpaneler och visualisering av data via verktyg för Business Intelligence

## Program

* Adobe Experience Platform

## Arkitektur

<img src="assets/data_exploration.svg" alt="Referensarkitektur för Enterprise Data Exploration and Reporting Blueprint" style="border:1px solid #4a4a4a" />

## Guardrails

Läs produktdokumentationen för frågetjänsten för mer information om bästa praxis och skyddsanvisningar.
[Vägledning för frågetjänst](https://experienceleague.adobe.com/docs/experience-platform/query/best-practices/writing-queries.html?lang=en#best-practices)

## Implementeringssteg

1. [Skapa ](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) scheman för data som ska importeras.
1. [Skapa ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) datauppsättningar för data som ska importeras.
1. [Ingest ](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) data into Experience Platform.
1. Bekräfta att data är tillgängliga för [[!UICONTROL Query Service]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html?lang=en) och [[!UICONTROL Data Science Workspace]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/load-data-in-jupyterlab-notebooks.html?lang=en) för obearbetad åtkomst och fråga.
1. [Koppla samman Business Intelligence- och SQL-klienter med  [!UICONTROL Query ]](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.qsvc.dash) Service för visualisering, datafrågor och utforskning.

## Relaterad dokumentation

* [Adobe Experience Platform Intelligence - produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [[!UICONTROL Query ] Service-dokumentation](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=en)
