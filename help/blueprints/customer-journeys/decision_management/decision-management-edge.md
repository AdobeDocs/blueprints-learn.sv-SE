---
title: Beslutshantering om Edge-planen
description: Leverera personaliserade erbjudanden till konsumenter i alla kanaler, även i realtid via webben och mobilupplevelser.
solution: Experience Platform, Journey Optimizer
exl-id: 31e5f624-5578-49e1-ab92-5cabd596a632
source-git-commit: 60a7785ea0ec4ee83fd9a1e843f0b84fc4cb1150
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 1%

---

# Journey Optimizer - [!DNL Decision Management] på Edge-ritningen

[!DNL Decision Management] är en tjänst som tillhandahålls som en del av [!DNL Journey Optimizer]. Denna plan beskriver användningsfall och teknisk kapacitet i programmet och ger en djupdykning i de olika arkitektoniska komponenterna och överväganden som utgör beslutsstöd.

>[!MORELIKETHIS]
>
>Mer information om [!DNL Decision Management] finns i översikten [för utkast](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-overview.html?lang=en) eller i [produktdokumentationen](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html).

[!DNL Decision Management] kan distribueras på ett av två sätt. Det första är via [!DNL Experience Platform]-hubben, som är en enda datacenterarkitektur. I navet-metoden utförs, personaliseras och levereras med andra fördröjning. Hub-arkitekturen är därför bäst lämpad för kundupplevelser som inte kräver en sekundär fördröjning. Exempel på sådana är erbjudandebeslut som ges för kioskdatorer eller agentassisterade upplevelser som callcenters eller personliga interaktioner.

Den andra metoden är via Experience Platform [!DNL Edge Network], som är en globalt distribuerad, geografiskt belägen infrastruktur som kan leverera snabba, subsekundära och millisekundsupplevelser. Den slutanvändarupplevelse som Edge-infrastrukturen närmast konsumenterna kör för att minimera latensen. [!DNL Decision Management] på Edge är utformat för att leverera konsumentupplevelser i realtid. Det kan vara upplevelser som webb- eller mobilförfrågningar om inkommande personalisering.

Denna plan kommer att omfatta de specifika delarna av beslutsförvaltningen på Edge.

Mer information om beslutshantering för navet finns i [beslutshanteringen för navet](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-hub.html?lang=en).

## Användningsexempel för beslutshantering i utkanten

* Direktuppspelning använder fall där svarstiden för profilkontext är lägre än 15 minuters fördröjning och körning av beslutshantering är mindre än 15 sekunder.
* Onlinepersonalisering via webb eller mobilupplevelser.
* Flerkanalsmarknadsföring - ger enhetlighet över webben, mobilen, e-post och andra interaktionskanaler via Adobe Journey Optimizer.

<br>

## Arkitektur

<img src="../assets/offers_edge.svg" alt="Referensarkitekturbeslutshantering i den främsta planen" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Integreringsmönster

| Integrering | Beskrivning |
| :-- | :--- |
| [Beslutshantering med Adobe Target](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html) | Beslutshantering kan integreras med Adobe Target så att erbjudandena kan testas och levereras som Target-upplevelser. |

## Förutsättningar

Adobe Experience Platform

* Scheman och datauppsättningar måste konfigureras i systemet innan du kan konfigurera Journey Optimizer-datakällor
* För Experience Event-klassbaserade scheman lägger du till fältgruppen &#39;Orchestration eventID&#39; när du vill att en händelse som inte är en regelbaserad händelse ska aktiveras
* För enskilda profilklassbaserade scheman lägger du till fältgruppen Profiltestinformation för att kunna läsa in testprofiler som ska användas med Journey Optimizer

<br>

## Skyddsräcken

* För Journey Optimizer skyddsräcken, se följande [Journey Optimizer-skyddsräcken](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/limitations.html).

* För chefsutkast för beslutshantering, se följande [produktbeskrivning för beslutshantering](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html).

[Garantier och Vägledning för svarstid från slut till slut](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)


## Implementeringsmönster

* Använd webb- eller Mobile SDK för distribution på webbplatser och mobilappar för att implementera beslutshantering där SDK distribuerades.
   * [Web/Mobile SDK-utkast](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/websdk.html?lang=en)
   * [Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/offer-decisioning/offer-decisioning-overview.html)
   * [MobileSDK](https://aep-sdks.gitbook.io/docs/)

eller

* För en API-server-till-server-baserad implementering använder du Edge Network Service API för direkt server-till-server-implementering av Beslutshantering.
   * [Edge Network Server-API](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/deliver-offers.html)

<br>

## Implementeringssteg

### Adobe Experience Platform

#### Schema/datauppsättningar

1. [Konfigurera enskilda profiler, upplevelsehändelser och scheman för flera entiteter](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) i Experience Platform utifrån data som kunden har angett.
1. [Skapa datauppsättningar](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) i Experience Platform för data som ska importeras.
1. [Lägg till dataanvändningsetiketter](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html) i Experience Platform i datauppsättningen för styrning.
1. [Skapa profiler](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html) som framtvingar styrning på mål.

#### Profil/identitet

1. [Skapa alla kundspecifika namnutrymmen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Lägg till identiteter i scheman](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Aktivera scheman och datauppsättningar för profilen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Ställ in sammanslagningsprinciper](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html) för olika vyer av [!UICONTROL Kundprofil i realtid] (valfritt).
1. Skapa segment för reseanvändning.

#### Källor/destinationer

1. [Infoga data i Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) med hjälp av direktuppspelnings-API:er och källanslutningar.

## Relaterad dokumentation

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html)
* [Adobe Journey Optimizer Beslutshantering](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)
* [Adobe Journey Optimizer produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
* [Produktbeskrivning för beslutshantering för Adobe](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html)
