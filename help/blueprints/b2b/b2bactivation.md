---
title: B2B-målgrupps- och profilaktiveringsplan
description: Leverera kontobaserade målgrupper och profilbaserade kundupplevelser med Real-time Customer Data Platform ​.
solution: Real-Time Customer Data Platform
kt: 9311
exl-id: 5215d077-b0a9-4417-ae9b-f4961d4a73fa
source-git-commit: 3dfdb1a237995e7f17e280e24f8865e992d9eb5f
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---

# B2B-målgrupps- och profilaktiveringsplan

Använd konto-, affärsmöjlighets- och lead-information som är knuten till en enskild kund för att skapa användbara b2b-profiler för förbättrad personalisering och målinriktning över alla kanaler.

## Användningsfall

* Skapa målgrupper av människor för målinriktning och personalisering över alla kanaler mot B2B-data, inklusive konton, möjligheter och leads.
* Aktivera målgrupper för alla Experience Platform-destinationer för målinriktning och personalisering.
* Skapa målgrupper med konton (t.ex. företagslistorna) och rikta in er på dessa företag via t.ex. LinkedIn som accepterar listor med företag som indata eller som exporterar till molnlagringsdestinationer för målinriktning och försäljning.

## Tillämpningar

* Real-time Customer Data Platform B2B Edition

## Integreringsmönster

* Datakällor från B2B (Marketo, Salesforce osv.) -> Real-time Customer Data Platform B2B Edition -> Destinationer
* Olika B2B-datakällor kan användas för att mappa data för konton, leads, affärsmöjligheter och människor till B2B-utgåvan av Real-time Customer Data Platform.

## Arkitektur

![Referensarkitektur för B2B-aktiveringsutkast](assets/b2b-activation.png)

## Skyddsräcken

* Observera att säkerhetsutkast och implementeringsåtgärder som rör Marketo Engage endast är relevanta när Marketo Engage används som källa och/eller mål.

* Mer information och skyddsförslag för datamodell, storlek och segmentering finns i dokumentet [Distributionsskyddsutkast](../experience-platform/deployment/guardrails.md)


### Stöd för flera instanser och IMS-organisation:

Följande visar vilka mönster som stöds för mappning av instanser av Experience Platform och Marketo Engage.

#### Marketo som datakälla för Experience Platform:

* Flera Marketo Engage-instanser till en Experience Platform-instans stöds.
* En Marketo Engage-instans till många Experience Platform-instanser stöds inte.
* En Marketo Engage-instans till en Experience Platform-instans och flera sandlådor stöds.

#### Marketo som destination till Experience Platform:

* Experience Platform till många Marketo Engage-instanser stöds
* Många Experience Platform-instanser till en Marketo Engage-instans stöds

#### Profil- och segmenteringsskydd för Experience Platform:

* Visa utkast för profil och segmenteringsskydd för Experience Platform - [Profil- och segmenteringsstödlinjer](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* B2B-segment som inkluderar konton, leads, affärsmöjligheter använder relationer med flera enheter vilket gör att segmentutvärderingen blir en batch. Direktuppspelningssegmentering stöds för segment som är begränsade till personer och händelser.
* Inkludera ett batch b2b-segment som indata till en direktuppspelning eller ett edge-segment för att stödja direktuppspelande b2b-segmentanvändningsfall. Batchsegmentmedlemskapet baseras på det senaste resultatet av den dagliga gruppsegmenteringsutvärderingen.

#### Experience Platform - Marketo Engage Source Connector:

* Historisk backfill kan ta upp till 7 dagar att slutföra, beroende på datavolym.
* Pågående datauppdateringar och ändringar från Marketo skickas till Experience Platform via API för direktuppspelning som kan vara latent upp till ca 10 minuter till profilen och kan ta upp till 60 minuter till datasjön beroende på volym.

#### Experience Platform - Marketo målanslutning:

* Det kan ta upp till 15 minuter att strömma segmentdelning från Real-time Customer Data Platform till Marketo Engage. Det kan ta upp till 24 timmar att fylla i profiler som redan fanns i segmentet före aktiveringen för första gången.
* Gruppsegmentering delas en gång per dag baserat på segmenteringsschemat för Experience Platform. B2B-segment som använder relationer med flera enheter, till exempel segment som använder data i konto- och affärsmöjlighetsobjekten, körs alltid i gruppläge.

#### Marketo Engage Guardrails:

* Kontakter och leads måste hämtas och definieras direkt i Marketo Engage för att Real-time Customer Data Platform ska matcha en kontakt och ett lead i Marketo Engage.
* RTCDP Marketo-destinationen kan även skapa nya leads i Marketo för kunder som befinner sig i ett segment men som inte finns i Marketo.

#### Målgarantins

* Mer information om destinationerna finns i måldokumentationen. [Målstödlinjer](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=en)


## Implementeringssteg

Mer information om hur du implementerar och konfigurerar B2B Edition av Real-time Customer Data Platform finns i B2B Edition av Real-time Customer Data Platform Documentation. [B2B-utgåvan av Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/b2b-overview.html?lang=en)

Det finns två möjliga implementeringsparter. Både möjligheten att importera B2B-data och profiler från Marketo Engage eller möjligheten att importera B2B-data från andra CRM-datakällor.

## Implementeringsöverväganden

Vägledning om viktiga överväganden och konfigurationer av ritningen.

* CRM-integrering med och utan Marketo:
Om implementeringen använder Marketo Engage som källa och Marketo Engage är ansluten till CRM flödar CRM-data automatiskt genom samma anslutning, vilket eliminerar behovet av att ansluta CRM direkt till plattformen, såvida det inte finns ytterligare CRM-dataobjekt som inte skickas via Marketo. Använd källkopplingen för Experience Platform om ytterligare tabeller behöver hämtas. Om implementeringen inte kommer att använda Marketo Engage som källa ansluter du CRM-källan direkt till plattformen med hjälp av CRM-källkopplingen för Experience Platform.
* Marketo Engage målkoppling för Platform, som överför målgrupper till Marketo Engage för aktivering, delar målgruppsmedlemmar baserat på matchande e-postadresser och ECID. Den har möjlighet att skapa en ny lead om kontakten inte redan finns. När du skapar ett nytt lead kan upp till 50 profilattribut (icke-matris- eller mappattribut) i Real-time Customer Data Platform mappas till personfält i Marketo.

## Relaterad dokumentation

* [B2B-utgåvan av Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/b2b-overview.html?lang=en)
* [Komma igång med Real-time Customer Data Platform B2B Edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial)
* [Guardrails för Real-time Customer Data Platform B2B Edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails)
* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Marketo Engage](https://experienceleague.adobe.com/docs/marketo/using/home.html)
* [Adobe Experience Platform - Marketo Source Connector](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo.html?lang=en)
* [Adobe Experience Platform - Marketo målanslutning](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html)
