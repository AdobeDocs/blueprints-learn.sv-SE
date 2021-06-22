---
title: Kundaktivitetshubbsknapp - översikt
description: '[!UICONTROL Kundprofiler i realtid ] för att ge kontext för support och försäljning som utförs av agenter.'
solution: Experience Platform,Data Collection
kt: 7195
exl-id: 3616cbf1-2e59-4e68-a1ff-1d2e3b344a1c
source-git-commit: 8b055d87a9c55b640bd35e54325977526ce21d94
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# Kundaktivitetshubbsknapp - översikt

Kundaktivitetshubben visar hur externa program kan komma åt Adobe Experience Platform [!UICONTROL kundprofil i realtid].

Externa program kan komma åt profiler med en API-GET-begäran. Attribut, händelser, segmentmedlemskap och modelldrivna funktioner som lagras i profilen kan sedan användas i dessa externa program som inte kommer från Adobe.

Med den här funktionen kan ni skapa ett avancerat sammanhang när en kund ringer ert callcenter. Supportpersonalen kan få insyn i kundens livstidsvärde, benägenhet att ändra sig eller exponering för marknadsföringskampanjer, till exempel. Säljarna kan också dra nytta av mer kontext och få bättre insikt i sina kunder.

>[!NOTE]
>
>Den aktuella fördröjningen som stöds av API:t för profilsökning är ungefär 500 millisekunder, vilket gör det här tillvägagångssättet olämpligt för integrering av profilen med realtidsmotorer för beslutsfattande, som webben eller mobilpersonalisering på samma sida.

## Användningsexempel

* Ge kunderna ett djupare sammanhang för interaktioner som stöds av agenter, som support och säljupplevelser. Med profilsökningen i Experience Platform kan agenterna få mer kontext om konsumenten, t.ex. nya inköp, kampanjinteraktioner, egenskaper, målgruppsmedlemskap och andra attribut och insikter som lagras i kundprofilen i realtid.

## Arkitektur

<img src="assets/customer_activity_hub.svg" alt="Referensarkitektur för Customer Activity Hub-utkast" style="border:1px solid #4a4a4a" />

## Guardrails

* [Guardrails for  [!UICONTROL Real-time Customer ] Profiledata](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)

## Implementeringssteg

1. [Skapa ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html) scheman för data som ska importeras.
1. [Skapa ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) datauppsättningar för data som ska importeras.
1. [Konfigurera rätt identiteter och ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html) identitetsnamnutrymmen i schemat för att säkerställa att inkapslade data kan sammanfogas till en enhetlig profil.
1. [Aktivera scheman och datauppsättningar för profilen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Ingest ](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) data into Experience Platform.
1. [Ställ in sammanfogningsprinciper](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html).
1. Använd [Entities-API:t för att söka efter ett profilattribut](https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html), antingen från postentiteten eller upplevelsehändelseentiteten.

## Relaterad dokumentation

* [Adobe Experience Platform Activation product description](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html)
* [[!UICONTROL Kundprofildokumentation ] i realtid](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en)
* [Profilskydd](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
* [API för profilsökning](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
