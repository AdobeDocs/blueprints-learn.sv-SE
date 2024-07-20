---
title: Dataanalys och informationsutkast
description: Använd Adobe [!DNL Experience Platform] (AEM) för att utföra experimentell fråga och analys av data som finns i sjön.
solution: Experience Platform
kt: 7207
thumbnail: null
exl-id: a972ea56-d1c8-45da-9044-ed31222a2441
source-git-commit: 7f3bc307f74aa88a7a73f3e50cc48bd16f58b37f
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 2%

---

# Dataanalys och intelligensutkast

Dataanalys och intelligens omfattar möjligheten inom [!DNL Experience Platform] att utföra experimentell fråga och analys av data som finns i sjön.

[!UICONTROL Frågetjänsten ] för [!DNL Experience Platform] tillåter att SQL-frågor utförs på data.

[!DNL Experience Platform] tillåter anslutningar med SQL-klienter, gränssnitt och Business Intelligence-verktyg (BI) från tredje part att ansluta direkt till, komma åt och fråga data i [!DNL Experience Platform] med protokollet [!DNL PostgreSQL].

## Användningsfall

* Interaktiv fråga och sammanställning av data
* Rad- och kolumnåtkomst till inmatade data för utforskande och validering
* Instrumentpaneler och visualisering av data via verktyg för Business Intelligence

Fler vanliga användningsexempel för frågetjänsten beskrivs här [Använd ärenden för frågetjänsten](https://experienceleague.adobe.com/docs/experience-platform/query/use-cases/abandoned-browse.html)

## Tillämpningar

* Adobe [!DNL Experience Platform]

## Arkitektur

<img src="assets/data_exploration.svg" alt="Referensarkitektur för Enterprise Data Exploration and Reporting Blueprint" style="width:90%; border:1px solid #4a4a4a" />

## Skyddsräcken

Läs produktdokumentationen för frågetjänsten för mer information om bästa praxis och skyddsanvisningar.
[Frågetjänstvägledning](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html)

## Implementeringssteg

1. [Skapa scheman](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) för data som ska importeras.
1. [Skapa datauppsättningar](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) för data som ska importeras.
1. [Infoga data](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) i [!DNL Experience Platform].
1. Bekräfta att data är tillgängliga för [[!UICONTROL frågetjänsten]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html?lang=en).
1. [Anslut Business Intelligence-verktyg och SQL-klienter till [!UICONTROL frågetjänsten]](https://experienceleague.adobe.com/docs/experience-platform/query/clients/overview.html) för visualisering, datafråga och sökning.

## Relaterad dokumentation

* [Adobe [!DNL Experience Platform] Beskrivning av informationsprodukt](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [[!UICONTROL Frågetjänsten] dokumentation](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=en)
