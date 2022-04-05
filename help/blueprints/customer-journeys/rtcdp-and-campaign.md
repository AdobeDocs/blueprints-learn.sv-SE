---
title: Real-Time CDP med Adobe Campaign integreringsmönster
description: Visar hur Adobe Experience Platform och dess kundprofil i realtid och centraliserade segmenteringsverktyg kan användas med Adobe Campaign för att leverera personaliserade konversationer.
solution: Real-time Customer Data Platform, Campaign
exl-id: a15e8304-2763-42fc-9978-11f2482ea8b8
source-git-commit: 24d5ec498d09f6dac443561bd530d58a33dae7af
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# Real-Time CDP med Adobe Campaign integreringsmönster

Visar hur Adobe Experience Platform och dess kundprofil i realtid och centraliserade segmenteringsverktyg kan användas med Adobe Campaign för att leverera personaliserade konversationer.

<br>

## Program

* Adobe Experience Platform Real-Time CDP
* Adobe Campaign v7 eller Campaign Standard

<br>

## Arkitektur

<img src="assets/rtcdp-campaign-architecture.svg" alt="Referensarkitektur för Batch Messaging och Adobe Experience Platform Integration Pattern" style="width:100%; border:1px solid #4a4a4a" />

<br>

## Förutsättningar

* Experience Platform och Campaign rekommenderas att etableras i samma IMS-organisation och att Adobe Admin Console används för användaråtkomst. Detta garanterar också att kunderna kan utnyttja lösningens väljare inifrån marknadsföringsgränssnittet

<br>

## Guardrails

### Adobe Campaign

* Stöder endast driftsättning av enskilda enheter i Adobe Campaign
* Adobe Campaign är en källa till sanning för alla aktiva profiler, dvs. profiler måste finnas i Adobe Campaign och nya profiler ska inte skapas baserat på Experience Platform.
* Arbetsflöden för kampanjexport som kan köras högst var fjärde timme
* XDM-scheman och datauppsättningar för Adobe Campaign brushlog, trackingLogs och adresser som inte kan levereras finns inte i lådan och måste utformas och byggas

### Experience Platform CDP-segmentdelning

* Rekommendation om 20-segmentsgräns
* Aktiveringen är begränsad till var 24:e timme
* Endast attribut för föreningsschema är tillgängliga för aktivering (inget stöd för array-/maps-/experience-händelser)
* Rekommendation om högst 20 attribut per segment
* En fil per segment av alla profiler med&quot;realiserat&quot; segmentmedlemskap ELLER om segmentmedlemskap läggs till som ett attribut i filen, både&quot;realiserade&quot; och&quot;avslutade&quot; profiler
* Stöd för export till hela segment
* Filkryptering stöds inte

<br>

## Implementeringssteg

### Adobe Experience Platform

#### Schema / Datauppsättningar

1. [Konfigurera enskilda profiler, upplevelsehändelser och scheman för flera enheter](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) i Experience Platform, baserat på kunddata.
1. Skapa Adobe Campaign-scheman för widthLog, trackingLog, adresser som inte kan levereras samt profilinställningar (valfritt).
1. [Skapa datauppsättningar](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) i Experience Platform för data som ska importeras.
1. [Lägg till etiketter för dataanvändning](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html) i Experience Platform till datauppsättningen för styrning.
1. [Skapa profiler](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html) som tillämpar styrning av destinationer.

#### Profil/identitet

1. [Skapa alla kundspecifika namnutrymmen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Lägga till identiteter i scheman](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Aktivera scheman och datauppsättningar för profilen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Ställ in sammanfogningsprinciper](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html) för olika vyer av [!UICONTROL Kundprofil i realtid] (valfritt).
1. Skapa segment för Adobe Campaign.

#### Källor/mål

1. [Infoga data i Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) med direktuppspelnings-API:er och källanslutningar.
1. Konfigurera [!DNL Azure] lagringsmål för blob som kan användas med Adobe Campaign.

#### Adobe Campaign

1. Konfigurera scheman för profil, sökdata och relevanta leveransdata.

>[!IMPORTANT]
>
>Det är viktigt att du i nuläget förstår vad datamodellen finns i Experience Platform för profil- och händelsedata så att du vet vilka data som krävs i Adobe Campaign.

#### Importera arbetsflöden

1. Läs in och importera förenklade profildata till Adobe Campaign sFTP.
1. Läs in och importera orkestrerings- och meddelandepersonaliseringsdata till Adobe Campaign sFTP.
1. Infoga segment i Experience Platform från [!DNL Azure] blob via arbetsflöden.

#### Exportera arbetsflöden

1. Skicka tillbaka Adobe Campaign-loggar till Experience Platform via arbetsflöden var fjärde timme (broadLog, trackingLog, non-deliverable address).
1. Skicka tillbaka profilinställningarna till Experience Platform via konsultbaserade arbetsflöden var fjärde timme (valfritt).


### Konfiguration av Mobile Push

* Två metoder som stöds för integrering med mobila enheter för push-meddelanden:
   * Experience Platform Mobile SDK
   * Campaign Mobile SDK
* Experience Platform Mobile SDK-väg:
   * Utnyttja Adobe Tags och tillägget Campaign Classic för att integrera med Experience Platform Mobile SDK
   * behöver kunskaper om Adobe-taggar och datainsamling
   * Behöver mobilutvecklingsupplevelse med push-meddelanden i både Android och iOS för att distribuera SDK, integrera med FCM (Android) och APNS (iOS) för att få push-token, konfigurera din app så att den tar emot push-meddelanden och hantera push-interaktioner
* Campaign Mobile SDK
   * Följ [Kampanjens SDK-dokumentation](Campaign Mobile SDK Följ distributionsdokumentationen som beskrivs här)

   >[!IMPORTANT]
   >Om ni distribuerar Campaign SDK och arbetar med andra Experience Cloud-program måste de använda Experience Platform Mobile SDK för datainsamling. Detta skapar dubblettanrop på klientsidan på enheten.

## Relaterad dokumentation

* [Adobe Experience Platform-dokumentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Campaign Classic dokumentation](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
* [Experience Platform Launch dokumentation](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Experience Platform Mobile SDK-dokumentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
