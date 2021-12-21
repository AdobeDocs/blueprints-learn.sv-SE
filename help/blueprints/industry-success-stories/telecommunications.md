---
title: Telekommunikationsbranschen - Journey Optimizer för Triggered Messaging
description: Ge kunderna skräddarsydda erbjudanden i realtid samtidigt som ni effektivt kan introducera nya kunder för långsiktig lojalitet.
solution: Experience Platform, Journey Optimizer
kt: 9486
source-git-commit: 7a81ea5d71355323a784e12207542fb7dd6b286b
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# Telekom Industry - problem

Innan denna utkast implementerades använde telekommunikationsföretagets e-postkampanjer som byggde på om användaren hade konverterat och bara kontrollerat detta efter en 7-dagars vänteperiod. När dessa kriterier var uppfyllda inleddes eventuella ytterligare kontaktytor.

Denna begränsning måste lösas för att man ska kunna inleda en tidsbesparande uppföljning av användare som vill lägga till en rad som är tidigare än den nuvarande 7-dagars vänteperioden.

## Adobe

* Adobe Analytics-data för att identifiera användare som inte kunnat konvertera för att lägga till en ny rad inkluderas som datakälla för Adobe Journey Optimizer.
* Adobe Journey Optimizer använder en regel som styr när kunderna får ett anpassat meddelande om att de vill överge en kund genom att lägga till en ny rad på sitt konto.


## Affärsvärde levererat

| Mål | Taktik | Värde ej låst |
|---|---|---|
| **Få högre kampanjkonverteringsgrader **<br></br>**Öka intäkterna från årsredovisningar**</ul> | <ul><li>Skapa ett nytt segment i nära realtid för användare som har visat intresse av att lägga till en rad men ännu inte konverterat.</li><li>Uppföljning för okonverterade kunder med en andra kontaktyta för intresserade icke-konverterare. </li><li>Använd en teststrategi för att mäta resans resultat och optimera för konvertering via e-post.</li></ul> | <ul><li><strong>Relevanta upplevelser med hög kvalitet:</strong> Med en fungerande kundresa får kunderna mer relevanta meddelanden, vilket minskar bortfallet av e-postlistor.</li><li><strong>Journey Orchestration vid skalförändring:</strong>En personaliserad och tidsödande resa kan skapas för att öka antalet konverteringar och totala intäkter.</li></ul> |

## Key Blueprint: Målgrupp och aktivering med Experience Cloud-program

<strong>Beskrivning</strong>
<ul><li>Kör triggade meddelanden och strömmande meddelanden med Adobe Experience Platform som ett centralt nav för strömmande data, kundprofiler och segmentering, med Journey Orchestration för direktuppspelad resesamordning och meddelandeleverans</li></ul>

<strong>Experience Cloud-program</strong>
<ul><li>Adobe Journey Optimizer</li></ul> 
<br>

### Blåtrycksarkitektur

<a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer.html?lang=en"><img alt="miniatyrbild för ett telekomföretag erbjuder skräddarsydda erbjudanden i realtid samtidigt som man effektivt kan introducera nya kunder för långsiktig lojalitet." src="https://experienceleague.adobe.com/docs/blueprints-learn/assets/journey-optimizer.png?lang=en"/></a>





