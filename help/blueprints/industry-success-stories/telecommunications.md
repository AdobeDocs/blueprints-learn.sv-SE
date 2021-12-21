---
title: Telekommunikationsbranschen - Journey Optimizer för Triggered Messaging
description: Ge kunderna skräddarsydda erbjudanden i realtid samtidigt som ni effektivt kan introducera nya kunder för långsiktig lojalitet.
solution: Experience Platform, Journey Optimizer
kt: 9486
source-git-commit: c393d73d2fa7acd4e5c2d99c098503b023b6115d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Telekom Industry - problem

Innan denna utkast implementerades använde telekommunikationsföretagets e-postkampanjer som byggde på om användaren hade konverterat och bara kontrollerat detta efter en 7-dagars vänteperiod. När dessa kriterier var uppfyllda initierades ytterligare beröringspunkter.

Denna begränsning måste lösas för att man ska kunna inleda en tidsbesparande uppföljning av användare som vill lägga till en rad som är tidigare än den nuvarande 7-dagars vänteperioden.

## Adobe

* Adobe Analytics-data för att identifiera användare som inte kunnat konvertera för att lägga till en ny rad inkluderas som datakälla för Adobe Journey Optimizer.
* Adobe Journey Optimizer använder en regel som styr när kunden får ett anpassat meddelande om att kunden överger sin prenumeration som är avsett att uppmuntra kunden att konvertera genom att lägga till en ny rad på sitt konto.


## Affärsvärde levererat

| Mål | Taktik | Värdet upplåst |
|---|---|---|
| **Få högre kampanjkonverteringsgrader **<br></br>**Öka intäkterna från årsredovisningar**</ul> | <ul><li>Skapa ett nytt segment i nära realtid för användare som har visat intresse av att lägga till en rad men ännu inte konverterat.</li><li>Få uppföljning för okonverterade kunder med en andra kontaktyta för intresserade icke-konverterare. </li><li>Använd en teststrategi för att mäta resans resultat och optimera för konvertering via e-post.</li></ul> | <ul><li><strong>Relevanta upplevelser med hög kvalitet:</strong> Med en fungerande kundresa får kunderna mer relevanta meddelanden, vilket minskar bortfallet av e-postlistor.</li><li><strong>Journey Orchestration vid skalförändring:</strong>En personaliserad och tidsödande resa kan skapas för att öka antalet konverteringar och totala intäkter.</li></ul> |

## Primär blå: Målgrupp och aktivering med Experience Cloud-program

### Beskrivning

<ul><li>Kör triggade meddelanden och strömmande meddelanden med Adobe Experience Platform som ett centralt nav för strömmande data, kundprofiler och segmentering, med Journey Orchestration för direktuppspelad resesamordning och meddelandeleverans</li></ul>

### Experience Cloud-program

<ul><li>Adobe Journey Optimizer</li></ul>

### Blåtrycksarkitektur

<a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer.html?lang=en"><img alt="miniatyrbild för ett telekomföretag erbjuder skräddarsydda erbjudanden i realtid samtidigt som man effektivt kan introducera nya kunder för långsiktig lojalitet." src="https://experienceleague.adobe.com/docs/blueprints-learn/assets/journey-optimizer.png?lang=en"/></a>





