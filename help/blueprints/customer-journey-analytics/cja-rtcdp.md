---
title: Customer Journey Analytics med Real-time Customer Data Platform-utkast
description: Sammanställ och analysera data och kundbeteenden från hela kundresan i Customer Journey Analytics, publicera målgrupper från CJA till RTCDP
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 9e1ba723-63f2-4622-ba67-f2a315c3ba0c
source-git-commit: 8355a36a235d847a6faf2398f3fadbed28ccac37
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---

# Customer Journey Analytics med Real-time Customer Data Platform-utkast

Skapa och publicera målgrupper som identifieras i Customer Journey Analytics (CJA) till kundprofilen i realtid i Adobe Experience Platform för kundanpassning och personalisering. Idealiskt för att skapa målgrupper med hjälp av historiska data eller mer raffinerade målgrupper från granulatfiltrering och beräknade fält i Customer Journey Analytics.

## Publiceringshandbok för Customer Journey Analytics

I följande dokumentation finns vägledning om implementering och konfigurering av publikationer från Customer Journey Analytics till Real-time Customer Data Platform. [Dokumentation](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html)

## Arkitektur för Customer Journey Analytics-ritningar

![Arkitektur](assets/CJA_RTCDP.svg)

## Guardrail-diagram för ritningar från Customer Journey Analytics

* Detaljerade skyddsförslag och sista-till-sista-latenser finns i [distributionsskyddsdokument](../experience-platform/deployment/guardrails.md)

![Guardradit-diagram](../experience-platform/assets/CJA_guardrails.svg)

## Frågor och svar

* Om det inte finns någon motsvarande profil i RTCDP som CJA har skickat, kommer en ny profil att skapas eller spelas målgrupper bara in från CJA för profiler som redan finns? Ja, en ny profil skapas. Om RTCDP-implementeringen bara är till för kända kunder, bör därför målgruppsreglerna för CJA skrivas för att filtrera enbart efter profiler med kända identiteter. Detta säkerställer att RTCDP-profilantalet inte ökar från anonyma profiler om det inte behövs.

* Skickar CJA målgruppsdata som rörliga händelser eller som en platt fil som också går till sjön? CJA-målgrupper direktuppspelas via pipeline till RTCDP Profile Service, men data lagras även i datasjön som en datauppsättning.

* Vilka identiteter skickar CJA? CJA skickar över de identiteter som konfigurerats som &quot;person-ID&quot; under CJA-konfigurationen.

* Vad anges som primär identitet? Vilken identitet användaren än valde när han/hon konfigurerade CJA som primär &quot;person&quot;-ID.

* Bearbetar identitetstjänsten även CJA-meddelandena? Kan CJA lägga till identiteter i ett profilidentitetsdiagram genom målgruppsdelning? Nej, identitetstjänsten bearbetar inte CJA-meddelandena.

## Relaterade blogginlägg

* [[!DNL Blueprint for Multi-Channel Orchestration in Adobe Experience Platform]](https://medium.com/adobetech/blueprint-for-multi-channel-orchestration-in-adobe-experience-platform-c68317e94184)
* [[!DNL Leveraging External Data Platforms in Adobe Experience Platform Journey Orchestration]](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17)
* [[!DNL Event-Based Triggering on Adobe Experience Platform Orchestration Service using Apache Airflow]](https://medium.com/adobetech/event-based-triggering-on-adobe-experience-platform-orchestration-service-using-apache-airflow-8607b28251f1)
* [[!DNL Adobe Campaign Classic Integration with Journey Orchestration]](https://medium.com/adobetech/adobe-campaign-classic-integration-with-journey-orchestration-ae577653281)
* [[!DNL Demonstrating the Power of Adobe's New Journey Orchestration Service to Build Personalized Omnichannel Experiences in Real-Time]](https://medium.com/adobetech/demonstrating-the-power-of-adobes-new-journey-orchestration-service-to-build-personalized-aa60d88cd34)
* [[!DNL Journey Orchestration in an Omnichannel World]](https://medium.com/adobetech/journey-orchestration-in-an-omnichannel-world-3a2d32d556d9)
