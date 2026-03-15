---
title: '[!DNL Journey Optimizer] - Kampanjsamordning'
description: Marknadsförarna kan koordinera schemalagd, målgruppsbaserad marknadsföring i flera steg över utgående meddelandekanaler.
solution: Journey Optimizer
exl-id: a8ff16f8-146d-4e1f-9bd0-9eda6af0c69b
source-git-commit: a632042b3a7434dd88f52804e15e30fa06057e3b
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# [!DNL Journey Optimizer] - Kampanjsamordning - utkast

AJO Campaign-samordning gör det möjligt för marknadsförare att utforma och genomföra schemalagda, målgruppsbaserade flerstegskommunikationer i utgående kanaler som e-post, SMS, push och direktreklam. Till skillnad från AJO Journeys, som reagerar på individuella kundbeteenden med realtidsdata från kundprofilen i realtid, är kampanjer samordnade marknadsföringsaktiviteter som riktar sig till målgrupper med planerade intervall. Tillsammans erbjuder kampanjer och resor kompletterande strategier - kampanjer driver varumärkesengagemangsstrategier, medan resor levererar personaliserade, responsiva upplevelser.

<br>

## Arkitektur

<img src="images/ajo-campaigns-architecture.svg" alt="Referensarkitektur Adobe Journey Optimizer Campaign Orchestration-utkast" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

### Meddelandeexekveringsarkitektur

<img src="images/ajo-campaigns-message-sending-architecture.png" alt="Referensarkitektur Adobe Journey Optimizer Campaign Orchestration-utkast" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

### Relationsarkiv - svarstid för datainmatning

<img src="images/ajo-campaigns-data-ingestion-architecture.png" alt="Referensarkitektur Adobe Journey Optimizer Campaign Orchestration-utkast" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Arkitektur för resor

- **Dataarkitektur**: AJO Campaign Orchestration använder en relationsdatabas under för målgruppsbyggnad och -samordning
- **Målgruppsportalsintegrering**: Inbyggt i målgruppsportalen i kundprofilen i realtid för att både läsa från befintliga målgrupper och spara nya målgrupper när ni skapar kampanjer
- **On-demand Audience Creation**: bygg, utvärdera och genomför en målgrupp omedelbart för brådskande marknadsföringssituationer
- **Integrering av kundprofil i realtid:** källa till sanning för medgivande och kommunikationshistorik; stöder design av tunn profil för personalisering
- **Skicka meddelande för flera entiteter:** möjlighet att skicka flera meddelanden per profil i en enda leverans (t.ex. skicka ett meddelande per reservation till kundens e-postadress)
- **Segmentering för flera enheter**: börja skapa en målgrupp från en enhet i relationsbutiken (dvs. produkt, lager, plan osv.)

<br>

## Skyddsräcken

[Produktlänk för samordnade kampanjer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/campaigns/orchestrated-campaigns/guardrails)

[Guardrails och Slut-till-slut-vägledning om svarstid](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails)

<br>

## Relaterad dokumentation

- [[!DNL Journey Optimizer] samordnade kampanjer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/orchestrated-campaigns/orchestrated-campaigns-landing-page.html)
- [Dokumentation för [!DNL Experience Platform]](https://experienceleague.adobe.com/docs/experience-platform.html?lang=sv-SE)
- [Dokumentation för [!DNL Experience Platform] taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv-SE)
- [Dokumentation för [!DNL Experience Platform Mobile SDK]](https://experienceleague.adobe.com/docs/mobile.html?lang=sv-SE)
- [Dokumentation för [!DNL Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=sv-SE)
- [[!DNL Journey Optimizer] produktbeskrivning](https://helpx.adobe.com/se/legal/product-descriptions/adobe-journey-optimizer.html)
