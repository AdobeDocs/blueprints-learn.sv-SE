---
title: Batchmeddelanden och Adobe Experience Platform
description: Kör schemalagda meddelandekampanjer och batchkampanjer med Adobe Experience Platform som ett centralt nav för kundprofiler och segmentering.
solution: Experience Platform, Campaign
kt: 7196
translation-type: tm+mt
source-git-commit: e1a9881996a181310bdc32cb083e4c5654139bf0
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---


# Batchmeddelanden och Adobe Experience Platform

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

<img src="assets/aepbatch.svg" alt="Referensarkitektur för Batch Messaging och Adobe Experience Platform" style="border:1px solid #4a4a4a" />

## Guardrails

* Stöder endast driftsättning av enskilda organisationsenheter i Campaign
* Campaign är en källa till sanning för alla aktiva profiler, dvs. profiler måste finnas i Campaign och nya profiler ska inte skapas baserat på Experience Platform-segment.
* Segmentmedlemsrealisering från Experience Platform är latent för både batch (1 per dag) och direktuppspelning (~5 minuter)

**Delning av kunddataplattformssegment i realtid till kampanj:**

* Rekommendation om begränsning av 20 segment
* Aktiveringen är begränsad till var 24:e timme
* Endast attribut för föreningsschema är tillgängliga för aktivering (inget stöd för array-/maps-/experience-händelser).
* Rekommendation om högst 20 attribut per segment
* En fil per segment av alla profiler med&quot;realiserat&quot; segmentmedlemskap ELLER om segmentmedlemskap läggs till som ett attribut i filen, både&quot;realiserade&quot; och&quot;avslutade&quot; profiler
* Export i flera eller hela segment stöds
* Filkryptering stöds inte
* Arbetsflöden för kampanjexport som kan köras högst var fjärde timme
* Se [skyddsutkast för profil och datainmatning för Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)

## Implementeringssteg

### Adobe Experience Platform

#### Schema / Datauppsättningar

1. Konfigurera enskilda profiler, upplevelsehändelser och scheman för flera enheter i Experience Platform utifrån kunddata.
1. Skapa kampanjscheman för widthLog, trackingLog, adresser som inte kan levereras samt profilinställningar (valfritt).
1. Lägg till dataanvändningsetiketter i datauppsättningen för styrning.
1. Skapa profiler som tvingar fram styrning av destinationer.

#### Profil/identitet

1. Skapa alla kundspecifika namnutrymmen.
1. Lägg till identiteter i scheman.
1. Aktivera scheman och datauppsättningar för profilen.
1. Ställ in kopplingsregler för olika vyer av kundprofilen i realtid (valfritt).
1. Skapa segment för kampanjanvändning.

#### Källor/mål

1. Importera data till Experience Platform med hjälp av API:er för direktuppspelning och källanslutningar.
1. Konfigurera [!DNL Azure]-lagringsmålet för blob för användning med Campaign.

#### Distribution av mobilappar

1. Implementera Campaign SDK för Campaign Classic eller Experience Platform SDK för Campaign Standard. Om det finns Experience Platform Launch rekommenderar vi att du använder tillägget Campaign Classic/Standard tillsammans med Experience Platform SDK.

#### Campaign

1. Konfigurera scheman för profil, sökdata och relevanta leveransdata.

>[!IMPORTANT]
>
>Det är viktigt att i det här skedet förstå vad datamodellen finns i Experience Platform för profil- och händelsedata så att ni vet vilka data som krävs i Campaign.

#### Importera arbetsflöden

1. Läs in och importera förenklade profildata till Campaign sFTP.
1. Läs in och importera orkestrerings- och meddelandepersonaliseringsdata till Campaign sFTP.
1. Infoga Experience Platform segment från blob [!DNL Azure] via arbetsflöden.

#### Exportera arbetsflöden

1. Skicka tillbaka kampanjloggar till Experience Platform via arbetsflöden var fjärde timme (broadLog, trackingLog, non-deliverable address).
1. Skicka tillbaka profilinställningarna till Experience Platform via konsultbaserade arbetsflöden var fjärde timme (valfritt).


## Relaterad dokumentation

* [Adobe Experience Platform-dokumentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Campaign Classic dokumentation](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
* [Experience Platform Launch dokumentation](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Experience Platform Mobile SDK-dokumentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
