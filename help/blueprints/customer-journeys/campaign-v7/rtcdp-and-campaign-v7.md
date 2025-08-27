---
title: Real-Time CDP med integreringsmönstret  [!DNL Campaign] v7 och Campaign Standard
description: Visar hur Adobe Experience Platform och dess kundprofil i realtid och centraliserade segmenteringsverktyg kan användas med Adobe [!DNL Campaign] för att leverera personaliserade konversationer.
solution: Real-Time Customer Data Platform, [!DNL Campaign]
exl-id: a15e8304-2763-42fc-9978-11f2482ea8b8
source-git-commit: 10d49e3b712fc9d4ecdf41defe6e62dde2a86b72
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 1%

---

# [!DNL Real-Time Customer Data Platform] med [!DNL Campaign]-integreringsmönster

Visar hur Adobe [!DNL Experience Platform] och dess kundprofil i realtid och centraliserade segmenteringsverktyg kan användas med Adobe [!DNL Campaign] för att leverera personaliserade konversationer.

## Tillämpningar

* Adobe [!DNL Experience Platform Real-Time Customer Data Platform]
* Adobe [!DNL Campaign] v7 eller [!DNL Campaign Standard]

## Arkitektur

<img src="assets/rtcdp-campaign-architecture.svg" alt="Referensarkitektur för integreringsmönstret Batch Messaging och Adobe Experience Platform" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## Förutsättningar

* Experience Platform och [!DNL Campaign] rekommenderas att etableras i samma IMS-organisation och att använda Adobe Admin Console för användaråtkomst. Detta garanterar också att kunderna kan utnyttja lösningens väljare inifrån marknadsföringsgränssnittet

## Skyddsräcken

I följande avsnitt beskrivs skyddsutkast för den här integreringen.

### Adobe [!DNL Campaign]

* Stöder endast Adobe [!DNL Campaign]-distributioner av en organisationsenhet
* Adobe [!DNL Campaign] är en källa till sanning för alla aktiva profiler som betyder profiler måste finnas i Adobe [!DNL Campaign] och nya profiler ska inte skapas baserat på Experience Platform-segment.
* [!DNL Campaign] exportarbetsflöden som kan köras högst var fjärde timme
* XDM-schema och datauppsättningar för Adobe [!DNL Campaign], wideLog, trackingLogs och adresser som inte kan levereras finns inte i lådan och måste utformas och byggas

### Real-Time Customer Data Platform segmentdelning

* Se RTCDP [!DNL Campaign] målanslutning - [RTCDP Campaign-anslutning](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/adobe-campaign-managed-services.html)

* Se [Standardskyddsutkast för [!DNL Real-Time Customer Profile Data] och segmentering](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)

## Implementeringssteg

I följande avsnitt beskrivs implementeringsstegen för respektive program.

### Adobe Experience Platform

#### Schema/datauppsättningar

1. [Konfigurera enskilda profiler, upplevelsehändelser och scheman för flera entiteter](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) i Experience Platform utifrån data som kunden tillhandahållit.
1. Skapa Adobe [!DNL Campaign]-scheman för widthLog, trackingLog, adresser som inte kan levereras och profilinställningar (valfritt).
1. [Skapa datauppsättningar](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) i Experience Platform för data som ska importeras.
1. [Lägg till dataanvändningsetiketter](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html) i Experience Platform i datauppsättningen för styrning.
1. [Skapa profiler](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html) som framtvingar styrning på mål.

#### Profil/identitet

1. [Skapa alla kundspecifika namnutrymmen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Lägg till identiteter i scheman](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Aktivera scheman och datauppsättningar för profilen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Ställ in sammanslagningsprinciper](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html) för olika vyer av [!UICONTROL Kundprofil i realtid] (valfritt).
1. Skapa segment för användning av Adobe [!DNL Campaign].

#### Källor/destinationer

1. [Experience Platform och [!DNL Campaign] Standardkällor och -designer](https://experienceleague.adobe.com/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/aep-sources-destinations/get-started-sources-destinations.html)
1. [Experience Platform och [!DNL Campaign] v7 Källor och destinationer](https://experienceleague.adobe.com/docs/campaign-classic/using/integrating-with-adobe-experience-cloud/aep-sources-destinations/get-started-sources-destinations.html)
1. [Importera data till Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) med direktuppspelnings-API:er och källanslutningar.
1. Konfigurera [!DNL Azure]-blobblagringsmålet för användning med Adobe [!DNL Campaign].

#### Adobe [!DNL Campaign]

1. Konfigurera scheman för profil, sökdata och relevanta data för leveranspersonalisering.

>[!IMPORTANT]
>
>Det är viktigt att du i nuläget förstår vad datamodellen finns i Experience Platform för profil- och händelsedata så att du vet vilka data som krävs i Adobe [!DNL Campaign].

#### Importera arbetsflöden

1. Läs in och importera förenklade profildata till Adobe [!DNL Campaign] sFTP.
1. Läs in och importera Orchestration- och Messaging-personaliseringsdata till Adobe [!DNL Campaign] sFTP.
1. Infoga Experience Platform-segment från blobben [!DNL Azure] via arbetsflöden.

#### Exportera arbetsflöden

1. Skicka tillbaka [!DNL Campaign]-loggar till Experience Platform via arbetsflöden var fjärde timme (broadLog, trackingLog, non-deliverable address).
1. Skicka tillbaka profilinställningarna till Experience Platform via konsultbaserade arbetsflöden var fjärde timme (valfritt).

### Mobil push-konfiguration

* Två metoder som stöds för integrering med mobila enheter för push-meddelanden:
   * Experience Platform Mobile SDK
   * [!DNL Campaign] Mobile SDK
* Experience Platform Mobile SDK:
   * Utnyttja Adobe Tags och tillägget [!DNL Campaign Classic] för att konfigurera integreringen med Experience Platform Mobile SDK
   * Kunskap om Adobe Tags och datainsamling
   * behöver mobilutvecklingsupplevelse med push-meddelanden i både Android och iOS för att driftsätta SDK, integrera med FCM (Android) och APNS (iOS) för att få push-token, konfigurera din app så att den tar emot push-meddelanden och hantera push-interaktioner
* [!DNL Campaign] Mobile SDK
   * Se [dokumentationen för Campaign Classic SDK](https://developer.adobe.com/client-sdks/solution/adobe-campaign-classic/)

>[!IMPORTANT]
>
>Om du distribuerar [!DNL Campaign] SDK och arbetar med andra Experience Cloud-program måste de använda Experience Platform Mobile SDK för datainsamling. Detta skapar dubblettanrop på klientsidan på enheten.

## Relaterad dokumentation

* [Adobe [!DNL Experience Platform] documentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [[!DNL Campaign Classic] dokumentation](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [[!DNL Campaign Standard] dokumentation](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
* [[!DNL Experience Platform] Starta dokumentation](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [[!DNL Experience Platform] Mobile SDK-dokumentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
