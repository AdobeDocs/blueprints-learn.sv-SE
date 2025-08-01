---
title: B2B-målgrupps- och profilaktiveringsplan
description: Leverera kontobaserade målgrupper och profilbaserade kundupplevelser med kunddataplattformen i realtid ​.
solution: Real-Time Customer Data Platform
kt: 9311
exl-id: 5215d077-b0a9-4417-ae9b-f4961d4a73fa
source-git-commit: 0509c5a8ce92c25040262130a5f583cdd7f08e59
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 0%

---

# B2B-målgrupps- och profilaktiveringsplan

Använd konto-, affärsmöjlighets- och lead-information som är knuten till en enskild kund för att skapa användbara b2b-profiler för förbättrad personalisering och målinriktning över alla kanaler.

## Användningsfall

* Skapa målgrupper av människor för målinriktning och personalisering över alla kanaler mot B2B-data, inklusive konton, möjligheter och leads.
* Aktivera målgrupper för alla Experience Platform-destinationer för målinriktning och personalisering.
* Skapa målgrupper med konton (till exempel listor över företag) och inrikta dig på dessa företag via mål som LinkedIn som accepterar listor över företag som indata eller export till molnlagringsdestinationer för målinriktning och försäljning.

## Tillämpningar

* Customer Data Platform B2B edition i realtid

## Integreringsmönster

* B2B-datakällor (Marketo, Salesforce osv.) -> Kunddataplattform i realtid B2B edition -> Destinationer
* Olika B2B-datakällor kan användas för att mappa konton, leads, affärsmöjligheter och persondata till B2B edition för kunddataplattformen i realtid.

## Arkitektur

![Referensarkitektur för B2B-aktiveringsutkast](assets/b2b-activation.png)

## Skyddsräcken

* Observera att Marketo Engage-relaterade säkerhetsutkast och implementeringssteg bara är relevanta när Marketo Engage används som källa och/eller mål.

* Mer information och skyddsförslag för datamodell, storlek och segmentering finns i dokumentet [Distributionsskyddsutkast](../experience-platform/guardrails.md)


### Stöd för flera instanser och IMS-organisation:

Följande visar vilka mönster som stöds för mappning av Experience Platform- och Marketo Engage-instanser.

#### Marketo som datakälla för Experience Platform:

* Flera Marketo Engage-instanser till en Experience Platform-instans stöds.
* En Marketo Engage-instans för många Experience Platform-instanser stöds inte.
* En Marketo Engage-instans till en Experience Platform-instans och flera sandlådor stöds.

#### Marketo som destination till Experience Platform:

* Experience Platform i många Marketo Engage-instanser stöds
* Många Experience Platform-instanser till en Marketo Engage-instans stöds

#### Experience Platform Profil- och segmenteringsskydd:

* Visa utkast för profil och segmenteringsskydd för Experience Platform - [Profil- och segmenteringsstödlinjer](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=sv-SE)
* B2B-segment som inkluderar konton, leads, affärsmöjligheter använder relationer med flera enheter vilket gör att segmentutvärderingen blir en batch. Direktuppspelningssegmentering stöds för segment som är begränsade till personer och händelser.
* Inkludera ett batch b2b-segment som indata till en direktuppspelning eller ett edge-segment för att stödja direktuppspelande b2b-segmentanvändningsfall. Batchsegmentmedlemskapet baseras på det senaste resultatet av den dagliga gruppsegmenteringsutvärderingen.

#### Experience Platform - Marketo Engage Source Connector:

* Historisk backfill kan ta upp till 7 dagar att slutföra, beroende på datavolym.
* Pågående datauppdateringar och ändringar från Marketo skickas till Experience Platform via API för direktuppspelning som kan vara latent upp till ca 10 minuter till profilen och kan ta upp till 60 minuter till datasjön beroende på volym.

#### Experience Platform - Marketo målanslutning:

* Det kan ta upp till 15 minuter efter segmentutvärderingen att strömma segmentdelning från kunddataplattformen i realtid till Marketo Engage. Det kan ta upp till 24 timmar att fylla i profiler som redan fanns i segmentet före aktiveringen för första gången.
* Gruppsegmentering delas en gång per dag baserat på Experience Platform segmenteringsschema. B2B-segment som använder relationer med flera enheter, till exempel segment som använder data i konto- och affärsmöjlighetsobjekten, körs alltid i gruppläge.

#### Marketo Engage Guardrails:

* Kontakter och leads måste hämtas och definieras direkt i Marketo Engage för att kunddataplattformen i realtid ska matcha en Marketo Engage-kontakt och lead.
* RTCDP Marketo-destinationen kan också skapa nya leads i Marketo för kunder som är i ett segment men som inte finns i Marketo.

#### Målgarantins

* Mer information om destinationerna finns i måldokumentationen. [Målstödlinjer](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=sv-SE)


## Implementeringssteg

Mer information om hur du implementerar och konfigurerar B2B edition för kunddataplattformen i realtid finns i B2B edition i dokumentationen för kunddataplattformen i realtid. [B2B edition för kunddataplattform i realtid](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/b2b-overview.html?lang=sv-SE)

Det finns två möjliga implementeringsparter. Både möjligheten att importera B2B-data och profiler från Marketo Engage eller möjligheten att importera B2B-data från andra CRM-datakällor.

## Implementeringsöverväganden

Vägledning om viktiga överväganden och konfigurationer av ritningen.

* CRM-integrering med och utan Marketo:
Om implementeringen använder Marketo Engage som källa och Marketo Engage är ansluten till CRM flödar CRM-data automatiskt genom samma anslutning, vilket eliminerar behovet av att ansluta CRM direkt till plattformen, såvida det inte finns ytterligare CRM-dataobjekt som inte skickas via Marketo. Använd Experience Platform-källkopplingen om ytterligare tabeller behöver importeras. Om implementeringen inte kommer att använda Marketo Engage som källa ansluter du CRM-källan direkt till plattformen med hjälp av Experience Platform-kontakten i CRM-källan.
* Marketo Engage målanslutning för Platform, som överför målgrupper till Marketo Engage för aktivering, delar målgruppsmedlemmar baserat på matchande e-postadresser och ECID:n. Den har möjlighet att skapa en ny lead om kontakten inte redan finns. När du skapar ett nytt lead kan upp till 50 profilattribut (icke-matris- eller mappattribut) i kunddataplattformen i realtid mappas till personfält i Marketo.

## Relaterad dokumentation

* [B2B edition för kunddataplattform i realtid](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/b2b-overview.html?lang=sv-SE)
* [Komma igång med kunddataplattformen B2B edition i realtid](https://experienceleague.adobe.com/sv/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial)
* [Guardrails for Real-time Customer Data Platform B2B edition](https://experienceleague.adobe.com/sv/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails)
* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=sv-SE)
* [Marketo Engage](https://experienceleague.adobe.com/docs/marketo/using/home.html?lang=sv-SE)
* [Adobe Experience Platform - Marketo Source Connector](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo.html?lang=sv-SE)
* [Adobe Experience Platform - Marketo målanslutning](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=sv-SE)
