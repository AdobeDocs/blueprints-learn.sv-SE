---
title: Layout för dataåtkomst och export
description: Denna plan innehåller en översikt över alla metoder som kan användas för att komma åt och exportera data från Adobe Experience Platform och program.
product: adobe experience platform
solution: Experience Platform, Journey Optimizer, Real-Time Customer Data Platform, Data Collection
exl-id: 2ca51a29-2db2-468f-8688-fc8bc061b47b
source-git-commit: 89dcbc4d71a9edff3095a6707cecc823281a9385
workflow-type: tm+mt
source-wordcount: '2052'
ht-degree: 0%

---

# Layout för dataåtkomst och export

I skisserna Dataåtkomst och Exportera anger du alla metoder som kan användas för att få åtkomst till och exportera data från Adobe Experience Platform och program.

Blueprint delas upp i två kategorier för dataåtkomst från Experience Platform och program. För det första strategier för att komprimera data från Experience Platform och program. Detta skulle betraktas som en metod med push-typ av datagegress. För det andra, metoder för att få tillgång till data från Experience Platform och tillämpningar, vilket skulle betraktas som en utsökt metod för dataåtkomst.

Åtkomstmetoder:

* [API för åtkomst till kundprofiler i realtid](#rtcp-profile-access-api)
* [API för dataåtkomst](#data-access-api)
* [Frågetjänst](#query-service)

Dataexportmetoder:

* [Kundsidestaggar](#client-side-tags-extensions)
* [Vidarebefordran av händelser](#event-forwarding)
* [Real-time Customer Data Platform Destinations](#RTCDP-destinations)
* [Journey Optimizer Custom Actions](#jo-custom-actions)

## Översiktsarkitektur för dataåtkomst och -export

<img src="../experience-platform/assets/aep_data_flow.svg" alt="Referensarkitektur för dataförberedelse och matningsutkast" style="width:90%; border:1px solid #4a4a4a; margin-bottom: 15px;" class="modal-image" />

## Metoder för dataåtkomst och -export

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1133px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:39px; vertical-align:top; width:1133px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">Direktuppspelningsmål</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Metod</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Vanliga användningsfall</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Protokoll</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Överväganden</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=en" style="color:#0563c1; text-decoration:underline">Vidarebefordran av händelser</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Vidarebefordran av rådata som samlats in från Adobe SDK för analys och insamling till affärssystem</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ljus viktmärkning för 3<sup>rd</sup> samla in partdata via tillägg</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">REST API</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Lågnivåråhändelser</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ingen aggregering eller tidigare postkontext har lagts till</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en#:~:text=containing%20profile%20exports.-,Direktuppspelning%20segment%20export%20mål,-Segment%20export%20mål" style="color:#0563c1; text-decoration:underline">RTCDP - export av strömmande segment</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Aktivera målgrupper från RTCDP till marknadsföring och reklam, system.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">REST API</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Samlade data som representerar målgruppsmedlemskap</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ingen aktivering av händelsedata för råupplevelser</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en#:~:text=file%2Dbased)%20destinations-,Streaming%20profile%20export%20destinations%20(enterprise%20destinations),-IMPORTANT" style="color:#0563c1; text-decoration:underline">RTCDP - mål för profilexport</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Utnyttja RTCDP:s omfattande beteendeprofiler och målgrupper för att förbättra kundupplevelsen och marknadsföringen.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Aktivera målgrupper och profilattribut från RTCDP till marknadsföring och annonsering, system som arbetar med målgrupper och profilattribut. </span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Aktivera AEP-profiler för e-postleverantörer, ledande vårdssystem och CRM-system.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">REST API</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Samlade data som representerar målgruppsmedlemskap och profilpostattribut</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ingen aktivering av händelsedata för råupplevelser</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=en" style="color:#0563c1; text-decoration:underline">RTCDP - personaliseringsmål</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Få åtkomst till kundprofilen i realtid i webbläsare och på klientsidan för att berika personaliseringen på klientsidan. </span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Kräver distribution av WebSDK</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-sdk/overview.html?lang=en" style="color:#0563c1; text-decoration:underline">RTCDP - Destination SDK</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Konfigurera ett anpassat målkort i RTCDP-destinationerna.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Stöder mål för fil- och direktuppspelningstyp</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">CSV</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Låter partners och varumärken konfigurera anpassade målkort</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html?lang=en" style="color:#0563c1; text-decoration:underline">RTCDP - API för profilsökningshubb</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Få tillgång till profiler för att berika kundupplevelserna med hjälp av agenter som support eller säljagentinteraktioner.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Dra</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">REST API</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Hub-sökning som är idealisk för mer än 500 ms+ - endast användningsfall</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:27px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">RTCDP - profilsökning Edge API* Beta</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:27px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Få tillgång till profiler i toppen för att berika kundupplevelserna för &lt;200 ms-upplevelser i realtid, som personalisering eller beslut om erbjudanden på webben och mobiler.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:27px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Dra</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">REST API</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:27px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">För realtidsupplevelser och server-till-server-integreringar</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html?lang=en" style="color:#0563c1; text-decoration:underline">Journey Optimizer Custom Actions</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Aktivering av 1:1-resehändelser och utlösare för att meddela ett externt system. Övergivna kundvagnar, övergivna ansökningar, registreringar.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">REST API</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Aktivering av enstaka händelse för en viss profil. Inte för aggregering eller gruppåtgärder</span></span></span></li>
</ul>
</td>
</tr>
</tbody>
</table>

<p> </p>

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1132px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:39px; vertical-align:top; width:1132px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">Batchmål</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:245px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Metod</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:462px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Vanliga användningsfall</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Protokoll</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:281px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Överväganden</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:245px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/data-access/api.html?lang=en" style="color:#0563c1; text-decoration:underline">API för dataåtkomst</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:462px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Tillgång till rådata för datavetenskap och XML-arbetsflöden utanför Experience Platform.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Dra</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">REST API</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Parquet-filer</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:281px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Kräver att utvecklingsprocesser får åtkomst till och bearbetar parquet-filer till användbara datauppsättningar</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:245px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=en" style="color:#0563c1; text-decoration:underline">Frågetjänst</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:462px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Behåll frågeresultat från datauppsättningar för sammanställd kunskap och rapportering. </span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Dra</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">PostgreSQL </span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">SQL-klient</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:281px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Sammanställ endast data. Gräns för 10 minuters fråga.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:245px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-datasets.html?lang=en" style="color:#0563c1; text-decoration:underline">Datauppsättningsexport* Beta</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:462px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Exportera händelsedata från Experience Platform för åtkomst i externa verktyg för rapportering, analys och datavetenskap. </span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Export av samlade profilinsikter och målgruppsmedlemskap för externa rapporterings-, analys- och datavetenskapsverktyg. </span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">REST API </span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">CSV</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:281px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">För närvarande i betaversion, med början från delmängd av datauppsättningstyper</span></span></span></li>
</ul>
</td>
</tr>
</tbody>
</table>



## Metoder för dataåtkomst

### API för åtkomst till kundprofiler i realtid {#rtcp-profile-access-api}

Kunderna kan få tillgång till enstaka enhetliga profiler från kundprofilbutiken i realtid, inklusive alla profilidentiteter, målgruppsmedlemskap, attribut och upplevelsehändelser med hjälp av API:t för kundprofilåtkomst i realtid.

Se [API för åtkomst till kundprofiler i realtid](https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html?lang=en) ytterligare information.

#### Användningsexempel

* Sök efter en enskild profil för att lägga till kontext till kundinteraktioner för agenter, som supportinteraktioner via chatt och callcenter, eller en säljinteraktion på försäljningsstället.
* Tillåt tillagd kontext till en personaliseringsbeskrivning som görs av ett externt system, till exempel ett webbpersonaliseringssystem eller ett system för beslut om erbjudande.

#### Överväganden

* Kundprofil i realtid [skyddsräcken](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en) gäller.
* Utformad för sökning efter enstaka profiler åt gången. Används inte för att få tillgång till eller hämta hela profilpopulationen för användning av analys eller datavetenskap.
* Svarstiden för profilsökning följer profilens skyddsprofiler. Låga latenskrav i realtid - exempelvis för krav på sidanpassning bör Edge Profile användas från början till slut [Adobe Target Connection](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en) eller [Anpassad anslutning för anpassning](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=en) för profilåtkomst i realtid för webbläsare och apppersonalisering.

### API för dataåtkomst {#data-access-api}

Med API:t för dataåtkomst kan kunder få direkt åtkomst till de rådatauppsättningsfiler som lagras i Experience Platform datasjön.

* Mer information om hur du använder API:t för dataåtkomst finns i [dokumentation](https://experienceleague.adobe.com/docs/experience-platform/data-access/home.html?lang=en).

#### Användningsexempel

* Dra in råa och bearbetade datafiler från Experience Platform för lagring och utvärdering i företagsmiljöer.

#### Överväganden

* När data används på ett batchasynkront sätt kommer åtkomsten till data att vara till sin natur latent jämfört med metoder för strömmande data som utlitizing Tags, Event Forwarding eller RTCDP Destinations.
* Datafiler som bearbetas till Experience Platform lagras som samlingar av filer i grupper och komprimeras och lagras i parquet-format. När filerna hämtas och laddas ned till en annan miljö måste de därför systematiskt kommas åt av sin batch och fil i stället för en hel datauppsättning, och eventuella dataåtgärder måste ta hänsyn till de filer som komprimeras i parquet-format.

### Frågetjänst {#query-service}

Med hjälp av upplevelseplattformen kan frågetjänstkunder ställa frågor till datauppsättningar i Experience Platform och behålla frågeresultatet. En SQL-klient kan användas för att fråga och behålla frågesvaret i önskat lagringsmål som SQL-klienten kan stödja. Användargränssnittet för frågetjänsten kan användas för att lagra SQL-resultatet i en måldatauppsättning i Experience Platform eller så kan resultaten sparas på den lokala datorn.

* Mer information om hur du ansluter till SQL-klienter för att behålla SQL-resultat från Experience Platform Query Service finns i följande [dokumentation](https://experienceleague.adobe.com/docs/experience-platform/query/clients/overview.html?lang=en).

#### Användningsexempel

* Fråga rådata från datauppsättningarna i Experience Platform och behåll frågeresultaten.
* Hämta profilögonblicksbildsdatauppsättningen för att få insikter om kundprofilen i realtid. [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=en#profile-attribute-datasets).
* Lagra frågeresultat i en separat datauppsättning för åtkomst eller i en profilaktiverad datauppsättning som senare kan komprimeras via RTCDP och andra Experience Cloud-program som använder kundprofilen i realtid.

#### Överväganden

* När data efterfrågas asynkront i en batch kommer åtkomsten till data att vara till sin natur latent jämfört med strategier för att direktuppspela data, till exempel taggar, händelsevidarebefordring eller RTCDP-destinationer.
* Det är bara data som är tillgängliga i dataströmmen i Experience Platform som kan efterfrågas med hjälp av frågetjänsten. Real-time Customer Profile Store, identitetsdiagrammet, Customer Journey Analytics kan inte hämtas direkt med Query Service. Det är bara när datauppsättningar exporteras till datasjön som dessa datauppsättningar kan efterfrågas, som i exemplet med datamängden för profilögonblicksbilder.
* Observera att utkast för antalet frågeresultat och frågans tidsgräns gäller enligt instruktionerna i [Frågetjänster - skyddsräcken](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=en) dokumentation.

## Metoder för dataexport

### Kodtillägg på klientsidan {#client-side-tags-extensions}

Tillägg kan distribueras med hjälp av Adobe Tags-lösningen. När ett tillägg distribueras distribueras dataförfrågningar direkt i en klientwebbläsare eller ett program och en begäran kan anropas för att skicka data och förfrågningar till önskat mål.

Se [Översikt över taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en) ytterligare information.

#### Användningsexempel

* Samla in strömningsinformation direkt från klientmiljöerna med hjälp av taggning.

#### Överväganden

* Ingen direkt åtkomst till information på serversidan, som kundprofilen i Experience Platform och medlemskap för målgrupper i realtid.
* Om du lägger till ytterligare datainsamlingstaggar på sidan kan sidans inläsningstid öka.
* Möjlighet att ställa in regler för att endast begära data när vissa villkor är uppfyllda.
* Data samlas in direkt från klienten och begränsar de typer av omvandlingar och berikning som kan utföras innan data samlas in.

### Vidarebefordran av händelser {#event-forwarding}

Begäranden om datainsamling samlas in direkt till Adobe Edge Network. Från Edge Network-begäranden till externa RESTful-slutpunkter kan konfigureras för att vidarebefordra dessa begäranden till det externa målet.

Se följande [Vidarebefordran av händelser](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=en) ytterligare information.

#### Användningsexempel

* Samla in strömmande rådata direkt från klientmiljöerna till slutpunkterna med hjälp av Adobe serversidans händelsevidarebefordran.

#### Överväganden

* Om du vill använda händelsevidarebefordran måste data skickas till Edge-nätverket med Web SDK eller MobileSDK.
* Vidarebefordra händelser minskar sidans inläsningstid och vikt på grund av att ytterligare taggar läggs till på sidan.
* Ingen anrikning från kantprofilen eller andra datakällor stöds för närvarande.
* Begränsad datafiltrering och enkel mappningsomvandling stöds.

### Real-time Customer Data Platform destinationer {#RTCDP-destinations}

Profilattributsdata och målgruppsmedlemskapsdata kan aktiveras för företags- och annonsmål. Det innebär att data som matas in måste hämtas in i kundprofilen i Experience Platform-realtid.

Se [Real-time Customer Data Platform Destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en) ytterligare information.

#### Användningsexempel

* Aktivera profilattributinformation, inklusive målgruppsmedlemskap i interna datalager, analysverktyg, e-postsystem eller supportsystem.
* Aktivera medlemskap för profilmålgrupper hos en extern reklamleverantör för att anpassa och anpassa innehållet efter profilen.

#### Överväganden

* Profilattribut och målgruppsmedlemskap kan aktiveras. Raw-upplevelsehändelser kan för närvarande inte aktiveras som en del av RTCDP-destinationer.
* Aktiveringar görs i direktuppspelning eller batch beroende på vilken typ av segmentutvärdering det är och vilken typ av ingtionsprotokoll som destinationen accepterar.

### Anpassade åtgärder från Journey Optimizer {#jo-custom-actions}

Med Journey Optimizer-kunder kan man anropa en anpassad åtgärd från arbetsytan för att skicka en nyttolast eller ett meddelande till en extern API-slutpunkt som är konfigurerad. En åtgärd kan konfigureras till vilken tjänst som helst från en leverantör som kan anropas via ett REST API med en JSON-formaterad nyttolast. Den här nyttolasten kan innehålla händelseinformation, profilattribut och tidigare händelsedata, omvandlingar och berikningar som har konfigurerats under resan.

Se [Anpassade åtgärder från Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html?lang=en) ytterligare information.

#### Användningsexempel

* Aktiveringshändelser från Experience Platform och Journey Optimizer som innehåller ytterligare information från kundprofilen i realtid.
* Meddela externa system när en kund har nått en viss punkt på en resa.

#### Överväganden

* Länkar till genomströmningen som stöds av [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=en) och berikning som stöds av [Kundprofil i realtid](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en) gäller.
* Anpassade åtgärder kan utföras i en direktuppspelning en i taget för varje händelse eller profil under en resa. Det går inte att utföra massåtgärder eller massdatagränser i form av filer eller aggregerade förfrågningar över kundresor.
* Direktuppspelad åtkomst till kundprofilattribut i realtid och upplevelsehändelser som kan inkluderas i aktiveringsnyttolasten.
* Händelsedata kan filtreras och enkla mappningsomformningar tillämpas innan händelser skickas till externa mål.
