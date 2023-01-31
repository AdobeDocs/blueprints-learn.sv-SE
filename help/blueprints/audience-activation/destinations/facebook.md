---
title: Aktivering till Facebook anpassade målgrupper
description: Aktivera för Facebook anpassade målgrupper.
solution: Real-Time Customer Data Platform, Data Collection
kt: 7086
exl-id: b75a7a01-04ba-4617-960d-f73f7a9cc6c7
source-git-commit: 8355a36a235d847a6faf2398f3fadbed28ccac37
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 0%

---

# Aktivering till Facebook anpassade målgrupper

Importera kunddata från olika källor för att skapa en enda profilvy av kunden, segmentera profilerna för att bygga målgrupper för marknadsföring och personalisering, dela dessa målgrupper med sociala annonsnätverk som Facebook för att rikta och personalisera kampanjer mot dessa målgrupper.

## Användningsexempel

* Målgruppsanpassning för kända målgrupper på sociala medier och reklamdestinationer.
* Anpassning online med online- och offlineattribut.

## Program

* Real-time Customer Data Platform

## Arkitektur

<img src="../assets/facebook.svg" alt="Referensarkitektur för Facebook Custom Audience Activation" style="width:90%; border:1px solid #4a4a4a" />

## Implementeringssteg

1. Konfigurera identitetsnamnutrymmen som ska användas i profildatakällor.
   * Använd namnutrymmen som e-post och SHA256-hash för e-post, om sådana finns.
   * Facebook har en lista över identiteter som stöds. För att kunna aktivera anpassade målgrupper i Facebook måste en av de identiteter som stöds finnas i de profiler som ska aktiveras.
   * Följande identiteter stöds för närvarande av Facebook: GAID, IDFA, phone_sha256, email_lc_sha256, extern_id.
   * Mer information finns i [Facebook Destinationshandbok](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/social/facebook.html).
   * Skapa egna namnutrymmen där det inte finns några namnutrymmen i rutan för de tillämpliga identiteterna.
1. Konfigurera scheman och datauppsättningar för datakällor för profiler.
   * Skapa profilpostscheman för alla profilpostens källdata.
      * Ange primär identitet och sekundära identiteter för varje schema.
      * Aktivera schemat för profilinmatning.
   * Skapa profilpostdatauppsättningar för alla profilpostens källdata och tilldela det associerade schemat.
      * Aktivera datauppsättningen för profilinmatning.
   * Skapa profilupplevelsehändelsescheman för alla profiltidsseriebaserade källdata.
      * Ange primär identitet och sekundära identiteter för schemat.
   * Aktivera schemat för profilinmatning.
   * Skapa data om händelser för profilupplevelser för alla händelsekälldata för profilupplevelser, och tilldela det associerade schemat.
      * Aktivera datauppsättningen för profilinmatning.
1. Infoga källdata med en källanslutning i den associerade datauppsättningen som konfigurerats ovan.
   * Konfigurera källanslutarkontot med autentiseringsuppgifter.
   * Konfigurera ett dataflöde för att importera data från källfilen eller mappplatsen enligt ett angivet schema till den angivna datauppsättningen.
   * Mappa fält från källdata till målschemat.
   * Omvandla alla fält till rätt format för intag till Experience Platform.
      * Datumomformningar
      * Omvandla till gemener där det är lämpligt - t.ex. e-postadress
      * Mönsteromformningar (till exempel telefonnummer)
      * Lägg till unika post-ID:n för upplevelsehändelseposter om de inte finns i källdata.
      * Omforma arrayer och mappa typfält för att säkerställa korrekt mappning och modellering av arrayer och kartor för segmentering i Experience Platform.
1. Konfigurera profilkopplingsprincipen för att säkerställa att identitetsdiagrammet konfigureras korrekt och vilka datauppsättningar som ska ingå i sammanslagningen av profiler.
1. När dataflödena har körts kontrollerar du att inmatningen av profildata lyckades utan fel.
   * Inspect identitetsdiagrammet för flera profiler för att säkerställa korrekt behandling av identitetsrelationer.
   * Inspect anger attribut och händelser för flera profiler för att säkerställa korrekt intag av attribut och händelser till profilerna.
1. Skapa segment för att skapa profilmålgrupper
   * Bygg segment i segmentbyggaren med regler mot attribut och händelser.
   * Spara segmentet för utvärdering. Segmenten utvärderas enligt angivet schema en gång om dagen.
      * Om segmentreglerna är berättigade till direktuppspelningssegmentering utvärderas segmentet som nya direktuppspelningsdata hämtas för profilerna. Direktuppspelningssegment utvärderas också en gång per dag under den schemalagda gruppsegmenteringen.
1. Se till att segmentresultaten blir som förväntat.
   * Granska segmentresultatantalet för de angivna segmenten.
   * Undersök den profil som ska inkluderas i segmentet för att verifiera att segmentmedlemskapet ingår i segmentmedlemskapsdelen i profilen.
1. Konfigurera leveransen av målgruppen till målet i målkonfigurationen.
   * Se [Facebook Destinationshandbok](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/social/facebook.html) om du vill ha mer information om hur du konfigurerar Facebook Destination.
   * När du konfigurerar ett mål väljer du vilken målgrupp du vill aktivera för målet.
   * Fastställ det schemalagda startdatum som du vill att måldataflödet ska börja leverera målgruppen till målet.
   * Varje mål har obligatoriska och valfria attribut som ska skickas.
      * För Facebook måste en av de identiteter som krävs inkluderas och användas för att matcha profilerna i målgrupperna i Experience Platform med en profil som Facebook har som mål.
   * Varje mål har också en angiven leveranstyp, vare sig det gäller direktuppspelning eller batch, filbaserad eller JSON-nyttolast.
      * För Facebook levereras målgruppsmedlemskap i direktuppspelande form till en Facebook-slutpunkt i JSON-format.
      * Målgruppsmedlemskap kommer att levereras i direktuppspelande läge efter utvärderingen av direktuppspelning eller gruppsegmentering i Experience Platform.
1. Kontrollera att målgruppen har levererats till destinationen som förväntat.
   * Kontrollera övervakningsgränssnittet för att bekräfta att målgruppen levererades med det förväntade antalet profiler. Publiken bör ha en storlek som motsvarar det förväntade antalet profiler som är aktiverade. Observera att specifika mål som Facebook kräver vissa fält, t.ex. en hash-identitet för e-post, och om de inte finns i profilen som är medlem av målgruppen aktiveras de inte för målgruppen.
   * Kontrollera om det finns profiler som hoppats över för att se om det saknas profiler eller attribut som var obligatoriska saknas.
   * Kontrollera om det finns andra fel som behöver åtgärdas.
1. Kontrollera att målgruppen aktiverades till slutmålet med det förväntade antalet målgruppsmedlemskap.
   * Logga in på Facebook Custom Audience Portal för att bekräfta att målgruppen från Real-time Customer Data Platform levererades och att matchningsfrekvensen för profiler i Facebook rimligen matchar antalet profiler i målgruppen från Real-time Customer Data Platform.

## Guardrails

[Profil- och segmenteringsskydd](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)

## Relaterad dokumentation

Aktivering till Facebook anpassade målgrupper - [Målkonfiguration](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/social/facebook.html)