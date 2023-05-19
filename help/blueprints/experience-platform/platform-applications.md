---
title: Diagram över Adobe Experience Platform- och programarkitektur
description: Arkitekturen visar hur Adobe Experience Platform relaterar till andra Adobe Experience Cloud-program och -programtjänster.
solution: Experience Platform, Campaign, Analytics, Target, Customer Journey Analytics, Journey Orchestration, Real-time Customer Data Platform
kt: 7199
thumbnail: null
exl-id: 9b12cd7a-5e5f-443a-91a1-44273cdabc2d
source-git-commit: 478a9bf0449e7953d527b5a54580f8eec7a7c30f
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 0%

---

# Diagram över Adobe Experience Platform- och programarkitektur

## Arkitektur för Adobe Experience Platform och program

Arkitekturen visar hur Adobe Experience Platform relaterar till Adobe Experience Cloud program och programtjänster.

<img src="assets/aep+apps.svg" alt="Experience Platform och program" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />

## Adobe Experience Platform &amp; Applications Overview

<img src="assets/aep+apps_overview.svg" alt="Experience Platform och program" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />

## Adobe Experience Platform &amp; Applications - detaljerad arkitektur

<img src="assets/aep+apps_detailed.svg" alt="Experience Platform och program" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />

>[!VIDEO](https://video.tv.adobe.com/v/32456/?quality=12&learn=on)

## Adobe Experience Platform och Experience Cloud

<table class="relative-table wrapped" style="width: 100%;">
<colgroup>
<col style="width: 16.0202%;" />
<col style="width: 29.3423%;" />
<col style="width: 33.5582%;" />
<col style="width: 21.0793%;" />
</colgroup>
<tbody>
<tr>
<th>Program</th>
<th>Experience Platform till program</th>
<th>Program till Experience Platform</th>
<th>Relaterade utkast</th>
</tr>
<tr>
<td colspan="1">Ad Cloud</td>
<td colspan="1">
<ul>
<li>Målgrupper som definieras i Real-time Customer Data Platform kan delas med Ad Cloud för målgruppsanpassning via Audience Manager.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Ingen aktuell integrering</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/anonymous.html?lang=en">Anonym Audience Activation</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html">Känd kundaktivering</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html">Aktivering med Experience Platform och program</a></li>
</ul>
</td>
</tr>
<tr>
<td>Analyser</td>
<td>
<ul>
<li>Data som samlas in via webb/mobil SDK kan vidarebefordras till Adobe Analytics.</li>
</ul>
</td>
<td>
<ul>
<li>Data som samlas in av Analytics kan skickas till datavjön och profilarkivet i Experience Platform. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=en">Analytics Data Connector</a></li>
</ul>
</td>
<td>
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-data-flow.html?lang=en">Experience Platform dataflöden</a></li>
</ul>
</td>
</tr>
<tr>
<td>Audience Manager</td>
<td>
<ul>
<li>Publikationer som definieras i Real-time Customer Data Platform kan delas med Audience Manager för aktivering till cookie-destinationer från tredje part.</li>
</ul>
</td>
<td>
<ul>
<li>Data som samlas in och utvärderas tillsammans med målgruppsmedlemskap från Audience Manager kan delas till Experience Platform Data Lake och Profile Store. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=en">Audience Manager Source Connector</a></li>
</ul>
</td>
<td>
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/anonymous.html?lang=en">Anonym Audience Activation</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html">Känd kundaktivering</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Aktivering med Experience Platform och program</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Campaign Classic</td>
<td colspan="1">
<ul>
<li>Målgrupper som definieras i Real-time Customer Data Platform kan delas med Campaign Classic som målgrupp för att initiera kampanjer.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Interaktions- och kampanjdata som samlas in av Campaign kan förtäras av Experience Platform som en datakälla för ytterligare användning i målgruppsuppbyggnaden via Real-time Customer Data Platform och analys via Customer Journey Analytics och Experience Platform Query Service.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/overview.html?lang=en">Kundresor</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Campaign Standard</td>
<td colspan="1">
<ul>
<li>Målgrupper som definieras i Real-time Customer Data Platform kan delas med Campaign Standarden som målgrupp för att initiera kampanjer.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Interaktions- och kampanjdata som samlas in av Campaign kan förtäras av Experience Platform som en datakälla för ytterligare användning i målgruppsuppbyggnaden via Real-time Customer Data Platform och analys via Customer Journey Analytics och Experience Platform Query Service.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/overview.html">Kundresor</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Customer Journey Analytics</td>
<td colspan="1">
<ul>
<li>Data som samlas in och hämtas in i Experience Platform Data Lake görs tillgängliga för behandling till Customer Journey Analytics. </li>
<li>Profil- och målgruppsdata från Real-time Customer Data Platform kan hämtas till CJA. <a href="https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/ingest-aep-segments.html?lang=en">Integrering mellan RTCDP och CJA</a>.
</li>
</ul>
</ul>
</td>
<td colspan="1">
<ul>
<li>Bygg målgrupper i kundreseanalyser och dela målgruppsresultaten med Real-time Customer Data Platform. <a href="https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=en">CJA Audience Publishing</a></li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journey-analytics/overview.html?lang=en">Customer Journey Analytics</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Experience Manager</td>
<td colspan="1">
<ul>
<li>Experience Platform-profilen kan nås direkt från serversidan för att ge kraft åt personaliserade upplevelser som levereras via Experience Manager. Observera att personaliseringsaktiviteter oftast levereras via Experience Manager via Target-integreringen. </li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Ingen aktuell integrering, inga beteenden eller interaktioner som utförs på Experience Manager webbplatser samlas in direkt via Experience Platform Web och Mobile SDK.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=en">Känd kundaktivering</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Journey Optimizer</td>
<td colspan="1">
<ul>
<li>Dataevent och profiler som hämtas in till Experience Platform görs tillgängliga för Journey Optimizer så att man kan starta och driva resor i Journey Optimizer.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Interaktions- och kampanjdata som producerats av Journey Optimizer samlas in i Experience Platform för ytterligare användning i målgruppsuppbyggnaden via Real-time Customer Data Platform och för analys via Customer Journey Analytics och Experience Platform Query Service.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer.html?lang=en">Journey Optimizer</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Adobe Commerce</td>
<td colspan="1">
<ul>
<li>Profiler och målgrupper som skapats i Real-time Customer Data Platform kan göras tillgängliga för personalisering i Adobe Commerce. </li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Data som är inbyggda i Adobe Commerce kan skickas till Experience Platform via en Adobe Commerce-källanslutning. </li>
</ul>
</td>
<td colspan="1">Ingen aktuell integrering</td>
</tr>
<tr>
<td colspan="1">Marketo</td>
<td colspan="1">
<ul>
<li>Målgrupper som definieras i Real-time Customer Data Platform kan delas med Marketo som målgrupp för att starta Marketo-kampanjer och uppdatera Marketo-objekt.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Marketo konton, kontakter och data om affärsmöjligheter, tillsammans med interaktions- och kampanjdata från Marketo, hämtas till Experience Platform för vidare användning i målgruppsuppbyggnaden via B2B-CDP och analys via Customer Journey Analytics och Experience Platform Query Service. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo.html?lang=en">Marketo Engage Connector</a></li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/b2b-activation/b2bactivation.html?lang=en">B2B-aktiveringsutkast</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Real-Time CDP</td>
<td colspan="1">
<ul>
<li>Data som hämtas in och samlas in i Experience Platform är datakällan för att sammanställa kundprofiler i realtid som driver Real-time Customer Data Platform.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Målgrupps- och profilmätvärden skickas till datavjön i Experience Platform för att ge bättre inblick i rapportinstrumentpaneler.</li>
<li>Data för målgrupp och profil i datasjön kan användas för ytterligare insikter via Query Service och Customer Journey Analytics.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=en">Känd kundaktivering</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Aktivering med Experience Platform och program</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Mål</td>
<td colspan="1">
<ul>
<li>Målgrupper och profilattribut som definieras i Real-time Customer Data Platform kan delas med Target och användas i personaliserings- och målinriktningsupplevelser som levereras av Target.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Data som samlas in för Target-upplevelser och interaktioner kan samlas in till Experience Platform via Experience Platform Web/Mobile SDK. Dessa data kan användas i målgruppsuppbyggnaden via Real-time Customer Data Platform och för analys via Customer Journey Analytics och Experience Platform Query Service.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=en">Känd kundaktivering</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Aktivering med Experience Platform och program</a></li>
</ul>
</td>
</tr>
</tbody>
</table>