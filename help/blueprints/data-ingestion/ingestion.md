---
title: Dataförberedelse och intag
description: I den här planen visas alla metoder som kan användas för att importera och förbereda data i Adobe  [!DNL Experience Platform].
solution: Data Collection
kt: 7204
thumbnail: null
exl-id: 21f8a73e-6be7-448e-8cd3-ebee9fc848e1
source-git-commit: 72eb4e2ff276279a2fc88ead0b17d77cc8e99b97
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 0%

---

# Utarbetande av data och intag

Dataförberedelse och matningsutkast omfattar alla metoder som data kan förberedas och hämtas med till Adobe [!DNL Experience Platform].

Datakompilering innefattar mappning av källdata till XDM-schema (Experience Data Model). Det omfattar även att utföra dataomvandlingar, inklusive datumformatering, fältdelning/sammanfogning/konverteringar samt att sammanfoga/skriva in poster på nytt. Med hjälp av dataförberedelser kan kunddata sammanställas för att ge en sammanställd/filtrerad analys, inklusive rapportering eller förberedelse av data för sammansättning av kundprofiler/datavetenskap/aktivering.

## Arkitektur

<img src="../experience-platform/assets/aep_data_flow.svg" alt="Referensarkitektur för dataförberedelse och matningsutkast" style="width:90%; border:1px solid #4a4a4a; margin-bottom: 15px;" class="modal-image" />

## Skyddsförslag för dataöverföring

Bilden nedan visar de genomsnittliga prestandagarantierna och latensen för dataöverföring till Adobe [!DNL Experience Platform].

<img src="../experience-platform/deployment/assets/aep_data_flow_guardrails.svg" alt="[!DNL Experience Platform] Dataflöde" style="border:1px solid #4a4a4a; margin-bottom: 15px;" width="90%" class="modal-image" />

## Metoder för dataöverföring

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1123px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:31px; vertical-align:top; width:1123px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">Direktuppspelningskällor</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Metod</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:401px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Vanliga användningsfall</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Protokoll</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:282px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Överväganden</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=en" style="color:#0563c1; text-decoration:underline">Adobe Web/Mobile SDK</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Datainsamling från webbplatser och mobilappar.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Önskad metod för klientsidsamling.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, HTTP, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Implementera flera Adobe-program med hjälp av en enda SDK.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/streaming/http.html?lang=en" style="color:#0563c1; text-decoration:underline">HTTP API Connector</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Samling från strömningskällor, transaktioner, relevanta kundhändelser och signaler</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, REST API, JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Data strömmas direkt till navet så att ingen Edge-segmentering eller händelsevidarebefordran sker i realtid.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/data-collection/interactive-data-collection.html?lang=en" style="color:#0563c1; text-decoration:underline">[!DNL Edge Network] API</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Samling från strömningskällor, transaktioner, relevanta kundhändelser och signaler från den globalt distribuerade [!DNL Edge Network]</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, REST API, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Data direktuppspelas via [!DNL Edge Network]. Stöd för segmentering i realtid på Edge. </span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=en" style="color:#0563c1; text-decoration:underline">Adobe-program</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Tidigare implementering av Adobe Analytics, Marketo, Campaign, Target, AAM</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, Source Connectors och API</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Rekommenderad metod är migrering till webb-/mobilSDK över traditionella SDK:er för program.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=en" style="color:#0563c1; text-decoration:underline">Strömmande Source Connectors</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Inmatning av en Enterprise-händelseström, som vanligtvis används för att dela företagsdata med flera nedströmsapplikationer. </span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, REST API, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Måste direktuppspelas i XDM-format.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">SDK för strömningskällor</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Precis som HTTP API Connector tillåter självbetjäningskonfigurationskort för en extern dataström.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, HTTP API, JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">[!DNL Edge Network]</span></span></span></li>
</ul>
</td>
</tr>
</tbody>
</table>

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1105px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:37px; vertical-align:top; width:1105px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">Batchkällor</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Metod</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:397px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Vanliga användningsfall</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Protokoll</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:277px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Överväganden</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/getting-started.html?lang=en" style="color:#0563c1; text-decoration:underline">API för gruppinmatning</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Inmatning från en företagsstyrd serviceteknik. Rensning och omvandling av data före intag.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, JSON eller Parquet</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Måste hantera grupper och filer för inmatning</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/cloud-storage/blob-s3.html?lang=en" style="color:#0563c1; text-decoration:underline">Batch Source Connectors</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Vanlig metod för att importera filer från molnlagringsplatser.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Kopplingar till vanliga CRM- och marknadsföringsprogram.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Perfekt för konsumtion av stora mängder historiska data.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Pull, CSV, JSON, Parquet</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Inte alltid, omedelbart intag. </span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Återkommande frekvenskontroller för att importera delta-filer minst var 15:e minut.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/cloud-storage/data-landing-zone.html?lang=en" style="color:#0563c1; text-decoration:underline">Datallandningszon</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Fillagringsplats som Adobe har etablerat för att överföra filer till för inhämtning.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, CSV, JSON, Parquet</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">- Filerna tillhandahålls en 7-dagars TTL</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/sdk/overview.html?lang=en" style="color:#0563c1; text-decoration:underline">SDK för batchkällor</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Tillåter självbetjäningskonfigurationskort för en extern datakälla.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Perfekt för partneranslutningar eller för en skräddarsydd arbetsflödesupplevelse för att skapa en företagskontakt.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Pull-, REST API-, CSV- eller JSON-filer</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Minsta frekvens på 15 min</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Exempel: MailChimp, One Trust, Zendesk</span></span></span></li>
</ul>

<p> </p>
</td>
</tr>
</tbody>
</table>



| Inmatningsmetoder | Beskrivning |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Webb/mobil SDK | Svarstid:<ul><li>Realtid - samma sidsamling till [!DNL Edge Network]</li><li>Direktuppspelningsuppläsning till profil &lt; 15 minuter vid den 95:e percentilen</li><li>Direktuppspelat intag till datasjön (mikrobatteri ~15 minuter)</ul>Dokumentation: <ul><li>[Web SDK](https://experienceleague.adobe.com/docs/web-sdk.html)</li><li>[Implementera Adobe Experience Cloud med Web SDK, genomgång](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html)</li><li>[Mobile SDK](https://experienceleague.adobe.com/docs/mobile.html?lang=en)</li><li>[Implementera Adobe Experience Cloud i mobilappar, självstudiekurs](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html)</li></ul> |
| Direktuppspelningskällor | [Direktuppspelningskällor](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en#connectors)<br>Latens:<ul><li>Realtid - samma sidsamling till [!DNL Edge Network]</li><li>Direktuppspelning till profil ~1 minut</li><li>Direktuppspelat intag till datasjön (mikrobatteri ~15 minuter)</li></ul> |
| API för direktuppspelning | [[!DNL Edge Network] Server-API:t (helst)](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/data-collection/interactive-data-collection.html) - stöder Edge-tjänster, inklusive Edge Segmentation och <br>[bastjänst-API:t för datainsamling](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/streaming/http.html) - stöder inte Edge Services, dirigeringar direkt till navet.<br>Latens:<ul><li>Realtid - samma sidsamling till [!DNL Edge Network]</li><li>Direktuppspelning till profil ~1 minut</li><li>Direktuppspelat intag till datasjön (mikrobatteri ~15 minuter)</li><li>7 GB/timme</li></ul>[Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=en#what-can-you-do-with-streaming-ingestion%3F) |
| ETL-verktyg | Använd ETL-verktygen för att ändra och omvandla företagsdata innan intag till [!DNL Experience Platform].<br><br>Latens:<ul><li>Tidsinställningen beror på den externa ETL-verktygets schemaläggning, och då tillämpas standardrutorna för intag baserat på den metod som används för intaget.</li></ul> |
| Batchkällor | Schemalagd hämtning från källor<br>Latens: ~ 200 GB/timme<br><br>[Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en#connectors)<br>[Tutorials för video](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/overview.html) |
| Batch-API | Svarstid:<ul><li>Batchintag till profil beroende på storlek och trafikbelastning ~45 minuter</li><li>Tillförsel av data till sjön i batch beroende på storlek och trafikbelastning</li></ul>[Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=en#batch) |
| Adobe Application Connectors | Automatiskt importera data som hämtas från Adobe Experience Cloud-program<ul><li>Adobe Analytics: [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=en#connectors) och [Videosjälvstudiekurs](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html)</li><li>Audience Manager: [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=en#connectors) och [Videosjälvstudiekurs](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-aam.html)</li></ul> |


## Metoder för dataförberedelse

| Metoder för dataförberedelse | Beskrivning |
|------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Externt ETL-verktyg ([!DNL Snaplogic], [!DNL Mulesoft], [!DNL Informatica] osv.) | Utför komplexa omformningar i ETL-verktygen och använd [!DNL Experience Platform] [!UICONTROL API:er för Flow Service] eller källanslutningar för att importera resulterande data. |
| [!UICONTROL Frågetjänst] - Dataprep | Sammanfogar, delar, sammanfogar, omformar, frågar och filtrerar data till en ny datauppsättning. Använda Skapa tabell som markerad (CTAS) <br>[Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=en#sql) |
| Funktionerna XDM-mappning och dataförberedelse (direktuppspelning och batch) | Mappa källattribut i CSV- eller JSON-format till XDM-attribut vid [!DNL Experience Platform]-intag.<br>Beräkna funktioner på data när de importeras, d.v.s. dataformatering, delning, sammanfogning och så vidare.<br>[Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/data-prep/home.html?lang=en) |

## Relaterade blogginlägg

* [Utnyttjar externa dataplattformar i Adobe [!DNL Experience Platform] [!DNL Journey Orchestration]](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17?source=your_stories_page)
* [Inmatning med hög genomströmning med Iceberg](https://medium.com/adobetech/high-throughput-ingestion-with-iceberg-ccf7877a413f?source=your_stories_page)
* [Frågetjänsten tricks i Adobe [!DNL Experience Platform] (Skriver frågor och sparar härledda datauppsättningar)](https://medium.com/adobetech/query-service-tricks-in-adobe-experience-platform-writing-queries-and-storing-derived-datasets-eaee0d6d683e?source=your_stories_page)
* [Diggar in i Adobe [!DNL Experience Platform]s Experience Data Model för att bättre förstå kraften i kundprofilen i realtid](https://medium.com/adobetech/digging-into-adobe-experience-platforms-experience-data-model-to-more-fully-understand-the-power-3e109271e04f?source=your_stories_page)
* [En introduktion till utforskande dataanalys på Adobe [!DNL Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a?source=your_stories_page)
* [Modellerar XDM-data för datavetenskap på skalnivå på Adobe [!DNL Experience Platform]](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7?source=your_stories_page)
