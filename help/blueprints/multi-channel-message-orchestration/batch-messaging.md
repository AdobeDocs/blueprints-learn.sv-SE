---
title: Batch Messaging och Adobe Experience Platform Blueprint
description: Kör schemalagda meddelandekampanjer och batchkampanjer med Adobe Experience Platform som ett centralt nav för kundprofiler och segmentering.
solution: Experience Platform, Campaign
kt: 7196
exl-id: 4e55218c-c158-4f78-9f0b-c03528d992fa
translation-type: tm+mt
source-git-commit: 01f70fe432d7be38b71889ae19c0d5fe4cf0f78a
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# Batch Messaging och Adobe Experience Platform Blueprint

Kör schemalagda meddelandekampanjer och batchkampanjer med Adobe Experience Platform som ett centralt nav för kundprofiler och segmentering.

## Användningsexempel

* Schemalagda e-postkampanjer
* Påbörja och återmarknadsföra kampanjer

## Program

* Adobe Experience Platform
* Adobe Campaign Classic eller Standard

## Integrationsmönster

* Adobe Experience Platform → Adobe Campaign Classic
* Adobe Experience Platform → Adobe Campaign Standard

## Arkitektur

<img src="assets/aepbatch.svg" alt="Referensarkitektur för Batch Messaging och Adobe Experience Platform Blueprint" style="border:1px solid #4a4a4a" />

## Guardrails

* Stöder endast driftsättning av en enda Adobe Campaign-enhet
* Adobe Campaign är en källa till sanning för alla aktiva profiler, dvs. profiler måste finnas i Adobe Campaign och nya profiler ska inte skapas baserat på Experience Platform.
* Segmentmedlemsrealisering från Experience Platform är latent för både batch (1 per dag) och direktuppspelning (~5 minuter)

**[!UICONTROL Delning av kunddata ] på Adobe Campaign i realtid:**

* Rekommendation om begränsning av 20 segment
* Aktiveringen är begränsad till var 24:e timme
* Endast attribut för föreningsschema är tillgängliga för aktivering (inget stöd för array-/maps-/experience-händelser).
* Rekommendation om högst 20 attribut per segment
* En fil per segment av alla profiler med&quot;realiserat&quot; segmentmedlemskap ELLER om segmentmedlemskap läggs till som ett attribut i filen, både&quot;realiserade&quot; och&quot;avslutade&quot; profiler
* Export i flera eller hela segment stöds
* Filkryptering stöds inte
* Adobe Campaign exportarbetsflöden som kan köras högst var fjärde timme
* Se [skyddsutkast för profil och datainmatning för Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)

## Implementeringssteg

### Adobe Experience Platform

#### Schema / Datauppsättningar

1. [Konfigurera enskilda profiler, upplevelsehändelser och ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html) flerenhetskarta i Experience Platform baserat på data som kunden har tillhandahållit.
1. Skapa Adobe Campaign-scheman för widthLog, trackingLog, adresser som inte kan levereras samt profilinställningar (valfritt).
1. [Skapa ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) datauppsättningar i Experience Platform för data som ska importeras.
1. [Lägg till ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html) etiketter för dataanvändning i Experience Platform i datauppsättningen för styrning.
1. [Skapa ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html) policyer som tvingar fram styrning av destinationer.

#### Profil/identitet

1. [Skapa alla kundspecifika namnutrymmen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Lägg till identiteter i scheman](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Aktivera scheman och datauppsättningar för profilen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Ställ in sammanslagningsprinciper ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html) för olika vyer av kundprofilen [!UICONTROL  i ] realtid (valfritt).
1. Skapa segment för Adobe Campaign.

#### Källor/mål

1. [Importera data till Experience ](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) Platform med hjälp av API:er för direktuppspelning och källanslutningar.
1. Konfigurera [!DNL Azure]-lagringsmålet för blob för användning med Adobe Campaign.

#### Distribution av mobilappar

1. Implementera Adobe Campaign SDK för Adobe Campaign Classic eller Experience Platform SDK för Adobe Campaign Standard. Om det finns Experience Platform Launch rekommenderar vi att du använder tillägget Adobe Campaign Classic eller Adobe Campaign Standard tillsammans med Experience Platform SDK.

#### Adobe Campaign

1. Konfigurera scheman för profil, sökdata och relevanta leveransdata.

>[!IMPORTANT]
>
>Det är viktigt att du i nuläget förstår vad datamodellen finns i Experience Platform för profil- och händelsedata så att du vet vilka data som krävs i Adobe Campaign.

#### Importera arbetsflöden

1. Läs in och importera förenklade profildata till Adobe Campaign sFTP.
1. Läs in och importera orkestrerings- och meddelandepersonaliseringsdata till Adobe Campaign sFTP.
1. Infoga Experience Platform segment från blob [!DNL Azure] via arbetsflöden.

#### Exportera arbetsflöden

1. Skicka tillbaka Adobe Campaign-loggar till Experience Platform via arbetsflöden var fjärde timme (broadLog, trackingLog, non-deliverable address).
1. Skicka tillbaka profilinställningarna till Experience Platform via konsultbaserade arbetsflöden var fjärde timme (valfritt).


## Relaterad dokumentation

* [Adobe Experience Platform-dokumentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Campaign Classic dokumentation](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
* [Experience Platform Launch dokumentation](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Experience Platform Mobile SDK-dokumentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
