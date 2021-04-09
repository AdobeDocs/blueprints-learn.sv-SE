---
title: Dataanalys och informationsutkast
description: Denna plan visar hur Adobe Experience Platform kan genomföra experimentella frågor och analyser av data som finns i sjön.
solution: Experience Platform
kt: 7207
thumbnail: null
exl-id: 3b22dfdd-3fbe-40b3-b798-1ee983723039,a972ea56-d1c8-45da-9044-ed31222a2441
translation-type: tm+mt
source-git-commit: 9a5137c5e71946c258cb94188ee53d742396d361
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Dataanalys och informationsutkast

Dataanalys och intelligens omfattar möjligheten inom Adobe Experience Platform att utföra experimentella frågor och analyser av data som finns i sjön.

Experience Platform [!UICONTROL Query Service] tillåter att SQL-frågor utförs på data. [!UICONTROL Data Science ] Workspace möjliggör datautforskande, datavetenskap och maskininlärningsarbetsbelastningar som kan utföras på data.

Dessutom tillåter Experience Platform anslutningar med SQL-klienter, gränssnitt och Business Intelligence-verktyg (BI) från tredje part att ansluta direkt till, komma åt och fråga data i Experience Platform med [!DNL PostgreSQL]-protokollet.

Vissa skyddsutkast gäller för frågetidsgränsen och för den datamängd som ingår i frågeresultatet, vilket beskrivs i scenarioinformationen.

## Användningsexempel

* Interaktiv fråga och sammanställning av data
* Rad- och kolumnåtkomst till inmatade data för utforskning och validering
* Instrumentpaneler och visualisering av data via verktyg för Business Intelligence

## Program

* Adobe Experience Platform

## Arkitektur

<img src="assets/dataexplore.svg" alt="Referensarkitektur för Enterprise Data Exploration and Reporting Blueprint" style="border:1px solid #4a4a4a" />

## Guardrails

* 10-minuters tidsgräns för interaktiva frågor
* Gränsen på 100 poster returnerades i användargränssnittet
* Gränsen på 50 000 poster returnerades via SQL-kopplingen

## Implementeringssteg

1. Konfigurera datauppsättningar och scheman för datainhämtning i datasjön.
1. Ingest data.
1. Bekräfta att data är tillgängliga för [!UICONTROL Query Service] och [!UICONTROL Data Science Workspace] för obearbetad åtkomst och fråga.
1. Koppla Business Intelligence- och SQL-klienter till [!UICONTROL Query Service] för visualisering, datafrågor och sökning.

## Relaterad dokumentation

* [Adobe Experience Platform Intelligence - produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [[!UICONTROL Query ] Service-dokumentation](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=en)
