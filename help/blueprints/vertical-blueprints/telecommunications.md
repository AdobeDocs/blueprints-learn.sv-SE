---
title: Telekommunikationsindustrin - Journey Optimizer för utlösta meddelanden
description: Ge kunderna skräddarsydda erbjudanden i realtid samtidigt som ni effektivt kan introducera nya kunder för långsiktig lojalitet.
solution: Journey Optimizer
kt: 9486
exl-id: fa4a6569-3972-4b97-91f1-7ca8ffd3c5b3
source-git-commit: cf7721ea01579182fdb200aad448be6fc94b34cf
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Affärsproblem inom telekombranschen

Innan den här planen implementerades använde telekomföretagets e-postkampanjer som byggde på om användaren hade konverterat och bara kontrollerat detta efter en sju dagars vänteperiod. När dessa kriterier var uppfyllda initierades ytterligare beröringspunkter.

Denna begränsning måste lösas för att man ska kunna inleda en tidsbesparande uppföljning av användare som vill lägga till en rad som är tidigare än den nuvarande 7-dagars vänteperioden.

## Adobe

* Adobe Analytics-data för att identifiera användare som inte kunnat konvertera för att lägga till en ny rad inkluderas som datakälla för Adobe Journey Optimizer.
* Adobe Journey Optimizer använder en regel som styr när kunden får ett anpassat meddelande om att kunden överger sin prenumeration som är avsett att uppmuntra kunden att konvertera genom att lägga till en ny rad på sitt konto.

## Affärsvärde levererat

| Mål | Taktik | Värdet är upplåst |
|---|---|---|
| **Öka konverteringsgraden för kampanjer **<br></br>**Öka årsomsättningen**</ul> | <ul><li>Skapa ett nytt segment i nära realtid för användare som har visat intresse av att lägga till en rad men ännu inte konverterat.</li><li>Få en uppföljning för okonverterade kunder med en andra kontaktyta för intresserade icke-konverterare. </li><li>Använd en teststrategi för att mäta resans resultat och optimera för konvertering via e-post.</li></ul> | <ul><li><strong>Hög kvalitet, relevanta upplevelser:</strong> Med resesamordning på plats får kunderna mer relevanta meddelanden, vilket minskar bortfallet av e-postlistor.</li><li><strong>Journey Orchestration på skalan:</strong>En personaliserad och tidsödande resa kan skapas för att öka antalet konverteringar och totala intäkter.</li></ul> |

## Primär ritning: Målgrupp och aktivering med Experience Cloud

### Beskrivning

<ul><li>Kör triggade meddelanden och strömmande meddelanden med Adobe Experience Platform som ett centralt nav för strömmande data, kundprofiler och segmentering, med Journey Orchestration för direktuppspelad resesamordning och meddelandeleverans</li></ul>

### Experience Cloud-program

<ul><li>Adobe Journey Optimizer</li></ul>

### Blåtrycksarkitektur

<a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer.html?lang=en"><img alt="för ett telekomföretag som erbjuder skräddarsydda erbjudanden i realtid med effektiv kundintroduktion för långsiktig lojalitet." src="https://experienceleague.adobe.com/docs/blueprints-learn/assets/ajo-architecture.svg"/></a>
