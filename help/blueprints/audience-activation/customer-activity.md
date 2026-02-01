---
title: Profilåtkomst i realtid för support- och säljscenarier
description: '[!UICONTROL Kundprofil &#x200B;] i realtid söker efter kontext för agentassisterad support och försäljning.'
solution: Data Collection
kt: 7195
exl-id: 3616cbf1-2e59-4e68-a1ff-1d2e3b344a1c
source-git-commit: 88a15765c0a998d49c19d9853ad0c44d6e3bfaa1
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 1%

---

# Profilåtkomst i realtid för support- och säljscenarier

Profilåtkomst i realtid för support- och säljscenarier visar hur externa program kan komma åt Adobe Experience Platform [!UICONTROL kundprofil i realtid].

Externa program har åtkomst till profiler med en API GET-begäran. Attribut, händelser, segmentmedlemskap och modelldrivna funktioner som lagras i profilen kan sedan användas i dessa externa program som inte kommer från Adobe.

Med den här funktionen kan ni skapa ett avancerat sammanhang när en kund ringer ert callcenter. Supportpersonalen kan få insyn i kundens livstidsvärde, benägenhet att ändra sig eller exponering för marknadsföringskampanjer, till exempel. Säljarna kan också dra nytta av mer kontext och få bättre insikt i sina kunder.

>[!NOTE]
>
>Profilsökning på navet är inte avsedd för hög genomströmning och låg latens, till exempel webb-/mobilpersonalisering. Profilsökning på hubben är avsedd för scenarier med lägre latens, t.ex. agentstödd support eller säljinteraktioner. För låg latens, höga genomströmningsscenarier som webb-/mobilpersonalisering eller offertbeslut i realtid bör Edge-profilen utnyttjas. Edge-profilen möjliggör åtkomst i realtid via [Anpassad Personalization Connection](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/personalization/custom-personalization) i kunddataplattformen i realtid.

## Användningsfall

* Ge kunderna ett djupare sammanhang för interaktioner som stöds av agenter, som support och säljupplevelser. Med profilsökningen i Experience Platform kan agenterna få mer kontext om konsumenten, t.ex. nya inköp, kampanjinteraktioner, egenskaper, målgruppsmedlemskap och andra attribut och insikter som lagras i kundprofilen i realtid.

## Arkitektur

<img src="assets/customer_activity_hub.svg" alt="Referensarkitektur för Customer Activity Hub-utkast" style="width:90%; border:1px solid #4a4a4a"  class="modal-image" />

## Skyddsräcken

* [Guardsutkast för [!UICONTROL Kundprofildata i realtid] &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=sv-SE)

## Implementeringssteg

1. [Skapa scheman](https://experienceleague.adobe.com/?lang=sv&recommended=ExperiencePlatform-D-1-2021.1.xdm) för data som ska importeras.
1. [Skapa datauppsättningar](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=sv-SE) för data som ska importeras.
1. [Konfigurera rätt identiteter och identitetsnamnutrymmen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=sv-SE) i schemat för att säkerställa att inkapslade data kan sammanfogas till en enhetlig profil.
1. [Aktivera scheman och datauppsättningar för profilen &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=sv-SE).
1. [Infoga data](https://experienceleague.adobe.com/?lang=sv&recommended=ExperiencePlatform-D-1-2020.1.dataingestion) i Experience Platform.
1. [Konfigurera sammanfogningsprinciper](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=sv-SE).
1. Använd [Entities-API:t för att leta upp ett profilattribut](https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html?lang=sv-SE).

## Relaterad dokumentation

* [Produktbeskrivning för Adobe Experience Platform-aktivering](https://helpx.adobe.com/se/legal/product-descriptions/adobe-experience-platform0.html)
* [[!UICONTROL Kundprofil i realtid] dokumentation](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=sv-SE)
* [Profilsäkerhetsutkast](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=sv-SE)
* [API för profilsökning](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
