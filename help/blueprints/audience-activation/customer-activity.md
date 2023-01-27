---
title: Kundaktivitetshubbskiss
description: "[!UICONTROL Kundprofil i realtid] sökningar för att ge kontext för support och försäljning som utförs av agenter."
solution: Data Collection
kt: 7195
exl-id: 3616cbf1-2e59-4e68-a1ff-1d2e3b344a1c
source-git-commit: b18d491fdefc57762932d1570401b5437bf97c76
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# Kundaktivitetshubbskiss

Kundaktivitetsnubben visar hur externa program kan komma åt Adobe Experience Platform [!UICONTROL Kundprofil i realtid].

Externa program kan komma åt profiler med en API-GET-begäran. Attribut, händelser, segmentmedlemskap och modelldrivna funktioner som lagras i profilen kan sedan användas i dessa externa program som inte kommer från Adobe.

Med den här funktionen kan ni skapa ett avancerat sammanhang när en kund ringer ert callcenter. Supportpersonalen kan få insyn i kundens livstidsvärde, benägenhet att ändra sig eller exponering för marknadsföringskampanjer, till exempel. Säljarna kan också dra nytta av mer kontext och få bättre insikt i sina kunder.

>[!NOTE]
>
>Den aktuella fördröjningen som stöds av API:t för profilsökning är ungefär 500 millisekunder, vilket gör det här tillvägagångssättet olämpligt för integrering av profilen med realtidsmotorer för beslutsfattande, som webben eller mobilpersonalisering på samma sida.

## Användningsexempel

* Ge kunderna ett djupare sammanhang för interaktioner som stöds av agenter, som support och säljupplevelser. Med profilsökningen i Experience Platform kan agenterna få mer kontext om konsumenten, t.ex. nya inköp, kampanjinteraktioner, egenskaper, målgruppsmedlemskap och andra attribut och insikter som lagras i kundprofilen i realtid.

## Arkitektur

<img src="assets/customer_activity_hub.svg" alt="Referensarkitektur för Customer Activity Hub-utkast" style="width:90%; border:1px solid #4a4a4a" />

## Guardrails

* [Guardrails för [!UICONTROL Kundprofil i realtid] data](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)

## Implementeringssteg

1. [Skapa scheman](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) för data som ska importeras.
1. [Skapa datauppsättningar](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) för data som ska importeras.
1. [Konfigurera rätt identiteter och identitetsnamnutrymmen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html) på schemat för att säkerställa att inkapslade data kan sammanfogas till en enhetlig profil.
1. [Aktivera scheman och datauppsättningar för profilen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Ingrediera data](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) till Experience Platform.
1. [Ställ in sammanfogningsprinciper](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html).
1. Använd [Enheter-API för att söka efter ett profilattribut](https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html), antingen från postenheten eller från upplevelsehändelseenheten.

## Relaterad dokumentation

* [Adobe Experience Platform Activation product description](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html)
* [[!UICONTROL Kundprofil i realtid] dokumentation](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en)
* [Profilskydd](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
* [API för profilsökning](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
