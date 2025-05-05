---
title: Customer Journey Analytics med Real-time Customer Data Platform-utkast
description: Sammanställ och analysera data och kundbeteenden från hela kundresan i Customer Journey Analytics, publicera målgrupper från CJA till RTCDP
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 9e1ba723-63f2-4622-ba67-f2a315c3ba0c
source-git-commit: 9fe44d93dcc05711c77ce1325b6549bb6c27a860
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Customer Journey Analytics med Real-time Customer Data Platform-utkast

Skapa och publicera målgrupper som identifieras i Customer Journey Analytics (CJA) till kundprofilen i realtid i Adobe Experience Platform för kundanpassning och personalisering. Idealiskt för att skapa målgrupper med hjälp av historiska data eller mer raffinerade målgrupper från granulatfiltrering och beräknade fält i Customer Journey Analytics.

## Publiceringshandbok för Customer Journey Analytics

I följande dokumentation finns vägledning om implementering och konfigurering av publikationer från Customer Journey Analytics till Real-time Customer Data Platform. [Dokumentation](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=sv-SE)

## Arkitektur för Customer Journey Analytics-ritningar

![Arkitekturdiagram](assets/CJA.svg){zoomable="yes"}

## Guardrail-diagram för ritningar från Customer Journey Analytics

* Detaljerade skyddsförslag och sista-till-sista-latenser finns i dokumentet [Distributionsskyddsförslag](../experience-platform/deployment/guardrails.md)

![Skyddsdiagram](../experience-platform/deployment/assets/CJA_guardrails.svg){zoomable="yes"}

## Frågor och svar

* Om det inte finns någon motsvarande profil i RTCDP som CJA har skickat, kommer en ny profil att skapas eller spelas målgrupper bara in från CJA för profiler som redan finns? Ja, en ny profil skapas. Om RTCDP-implementeringen bara är till för kända kunder, bör därför målgruppsreglerna för CJA skrivas för att filtrera enbart efter profiler med kända identiteter. Detta säkerställer att RTCDP-profilantalet inte ökar från anonyma profiler om det inte behövs.

* Vilka identiteter skickar CJA? CJA skickar över de identiteter som konfigurerats som &quot;person-ID&quot; under CJA-konfigurationen.

* Vad anges som primär identitet? Vilken identitet användaren än valde när han/hon konfigurerade CJA som primär &quot;person&quot;-ID.

* Bearbetar identitetstjänsten även CJA-meddelandena? Kan CJA lägga till identiteter i ett profilidentitetsdiagram genom målgruppsdelning? Nej, identitetstjänsten bearbetar inte CJA-meddelandena.