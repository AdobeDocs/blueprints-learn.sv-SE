---
title: Custom Data Science for Profile Enrichment Plan
description: Läs om hur datavetenskapsbaserade insikter kan hämtas in i [!DNL Experience Platform] för att förbättra kundprofilen i realtid.
solution: Data Collection
kt: 7203
exl-id: e5ec6886-4fa4-4c9b-a2d8-e843d7758669,f0efaf3c-6c4f-47c3-ab8a-e8e146dd071c
source-git-commit: 7f3bc307f74aa88a7a73f3e50cc48bd16f58b37f
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# Anpassad datavetenskap för en plan för profilberikning

Den anpassade datavetenskapen för profilberikning illustrerar hur data kan användas för att utbilda, driftsätta och poängsätta modeller för att ge maskininlärningsinsikter om [!DNL Experience Platform] och [!DNL Real-Time Customer Data Platform] från datavetenskap och maskininlärningsverktyg.

Modellerade insikter kan hämtas in i [!DNL Experience Platform] för att förbättra kundprofilen i realtid. Exempel på maskininlärningsinsikter är poängsättning för livstid, produkt- och kategoritillhörighet, benägenhet att konvertera eller benägenhet att försvinna.

## Användningsexempel

* Extrahera insikter och upptäck mönster från kunddata, utbildnings- och poängmodeller utifrån dessa data.
* Förbättra [!UICONTROL Kundprofil i realtid] med modellbaserade insikter och attribut för mer detaljerad personalisering och optimerade resor.
* Train- och Score-modeller för att fastställa kundinsikter som kundens livstidsvärde, benägenhet att konvertera eller tappa plats, produkt- och innehållstillhörighet samt engagemangsmätningar.

## Arkitektur

<img src="assets/data_science.svg" alt="Referensarkitektur för Custom Data Science for Profile Enrichment Blueprint" style="width:90%; border:1px solid #4a4a4a" />

## Guardrails

* Detaljerade säkerhetsdetaljer och total latens vid inmatning av datavetenskap ger [!DNL Experience Platform] och kundprofilen i realtid refererar till de utkast för dataöverföringsskydd och latensdiagram som refereras i [distributionsskyddsdokument](../experience-platform/deployment/guardrails.md).

## Implementeringssteg

1. [Skapa scheman](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) för data som ska importeras.
1. [Skapa datauppsättningar](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) för data som ska importeras.
1. [Ingrediera data](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) till [!DNL Experience Platform].

För att modellresultat ska kunna hämtas till kundprofilen i realtid måste du göra följande innan du hämtar in data:

1. [Konfigurera rätt identiteter och identitetsnamnutrymmen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html) på schemat för att säkerställa att inkapslade data kan sammanfogas till en enhetlig profil.
1. [Aktivera scheman och datauppsättningar för profilen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).

## Implementeringsöverväganden

* I de flesta fall bör modellresultat anges som profilattribut och inte upplevas som händelser. Modellresultaten kan vara enkla attributsträngar. Om det finns flera modellresultat som ska importeras rekommenderar vi att du använder ett matris- eller mappningstypsfält.
* Den dagliga ögonblicksbildsdatauppsättningen, som är en daglig export av data för enhetliga profilattribut, kan utnyttjas för att utbilda modeller i profilattributdata. Datadokumentet för ögonblicksbilder av profiler är tillgängligt [här](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html#profile-attribute-datasets).
* För att extrahera data från [!DNL Experience Platform] följande metoder kan användas
   * SDK för dataåtkomst
      * Data finns i råfilsformat
      * Data för händelser för profilupplevelse förblir i oförenat råformat.
   * RTCDP-mål
      * Profilattribut och segmentmedlemskap kan komprimeras.

## Relaterad dokumentation

* [Adobe [!DNL Experience Platform] Beskrivning av Intelligence-produkt](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Adobe [!DNL Experience Platform] Frågetjänst](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=sv)

## Relaterade blogginlägg

* [Innehåll och handel AI: Personalisera interaktionen med kunder via innehållsintelligens](https://medium.com/adobetech/content-and-commerce-ai-personalizing-your-interactions-with-customers-through-content-intelligence-dc182601deab)
* [En introduktion till undersökande dataanalys på Adobe [!DNL Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a)
* [Att skära mellan olika Adobe-upplevelser med maskininlärning till en bättre användarupplevelse](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
* [Segmentering.AI: Automated Audience-Clustering-as-a-Service in Adobe [!DNL Experience Platform]](https://medium.com/adobetech/segmentation-ai-automated-audience-clustering-as-a-service-in-adobe-experience-platform-261f4099462c)