---
title: Audience Activation till sociala medier och Advertising destinationer
description: Lär dig hur du importerar kunddata från flera källor för att skapa en enda profilvy av kunden.
solution: Real-Time Customer Data Platform, Data Collection
kt: 7086
exl-id: b75a7a01-04ba-4617-960d-f73f7a9cc6c7
source-git-commit: 88a15765c0a998d49c19d9853ad0c44d6e3bfaa1
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 0%

---

# Audience Activation till sociala medier och Advertising destinationer

Inhämta kunddata från flera källor för att skapa en enda profilvy av kunden. Ni kan segmentera dessa profiler för att bygga målgrupper för marknadsföring och personalisering, dela dessa målgrupper med annonsnätverk som Facebook och Google för att rikta och personalisera kampanjer mot dessa målgrupper.

## Användningsfall

* Målgruppsanpassning för kända målgrupper på sociala medier och reklamdestinationer.
* Anpassning online med online- och offlineattribut.

## Tillämpningar

* Kunddataplattform i realtid

## Arkitektur

<img src="./assets/social_activation.svg" alt="Referensarkitektur för Facebook Custom Audience Activation" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## Implementeringssteg

1. Konfigurera identitetsnamnutrymmen som ska användas i profildatakällor.
   * Använd namnutrymmen som e-post och SHA256-hash för e-post, om sådana finns.
   * Facebook har en lista över identiteter som stöds. För att kunna aktivera anpassade målgrupper på Facebook måste en av de identiteter som stöds finnas i de profiler som ska aktiveras.
   * Följande identiteter stöds för närvarande av Facebook: GAID, IDFA, phone_sha256, email_lc_sha256, extern_id.
   * Mer information finns i [Facebook-målguiden](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/social/facebook.html?lang=sv-SE).
   * Google Customer Match innehåller en lista över identiteter som stöds. För att kunna aktivera till Google kundmatchning måste en av de identiteter som stöds finnas i profilerna som ska aktiveras.
   * Följande identiteter stöds för närvarande av Google Customer Match: GAID, IDFA, phone_sha256_e.164, email_lc_sha256, user_id.
   * Mer information finns i [Google kundmatchningsmålguide](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-customer-match.html?lang=sv-SE).
   * Skapa egna namnutrymmen där det inte finns några namnutrymmen i rutan för de tillämpliga identiteterna.
1. Konfigurera scheman och datauppsättningar för datakällor för profiler.
   * Skapa profilpostscheman för alla profilpostens källdata.
      * Ange primär identitet och sekundära identiteter för varje schema.
      * Aktivera schemat för profilinmatning.
   * Skapa profilpostdatauppsättningar för alla profilpostens källdata och tilldela det associerade schemat.
      * Aktivera datauppsättningen för profilinmatning.
   * Skapa profilupplevelsehändelsescheman för alla profiltidsseriebaserade källdata.
      * Ange den primära identiteten och de sekundära identiteterna för schemat.
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
   * Granska identitetsdiagrammet för flera profiler för att säkerställa korrekt behandling av identitetsrelationer.
   * Granska attribut och händelser för flera profiler för att säkerställa korrekt intag av attribut och händelser till profilerna.
1. Skapa segment för att skapa profilmålgrupper
   * Bygg segment i segmentbyggaren med regler mot attribut och händelser.
   * Spara segmentet för utvärdering. Segmenten utvärderas enligt angivet schema en gång om dagen.
      * Om segmentreglerna är berättigade till direktuppspelningssegmentering utvärderas segmentet som nya direktuppspelningsdata hämtas för profilerna. Direktuppspelningssegment utvärderas också en gång per dag under den schemalagda gruppsegmenteringen.
1. Se till att segmentresultaten blir som förväntat.
   * Granska segmentresultatantalet för de angivna segmenten.
   * Undersök den profil som ska inkluderas i segmentet för att verifiera att segmentmedlemskapet ingår i segmentmedlemskapsdelen i profilen.
1. Konfigurera leveransen av målgruppen till målet i målkonfigurationen.
   * Mer information om hur du konfigurerar Facebook-målet finns i [Facebook-målguiden](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/social/facebook.html?lang=sv-SE).
   * Mer information om hur du konfigurerar Google-destinationen finns i [Google kundmatchningsguide](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-customer-match.html?lang=sv-SE).
   * När du konfigurerar ett mål väljer du vilken målgrupp du vill aktivera för målet.
   * Fastställ det schemalagda startdatum som du vill att måldataflödet ska börja leverera målgruppen till målet.
   * Varje mål har obligatoriska och valfria attribut som ska skickas.
      * För Facebook måste en av de nödvändiga identiteterna inkluderas och används för att matcha profilerna i målgrupperna inom Experience Platform med en profil som kan användas på Facebook.
      * För Google Customer Match måste en av de identiteter som krävs inkluderas och används för att matcha profilerna i målgrupperna inom Experience Platform med en profil som Google Customer Match har som mål.
   * Varje mål har också en angiven leveranstyp, vare sig det gäller direktuppspelning eller batch, filbaserad eller JSON-nyttolast.
      * För Facebook levereras målgruppsmedlemskap i direktuppspelande form till en Facebook-slutpunkt i JSON-format.
      * För Google Customer Match levereras målgruppsmedlemskap i direktuppspelande form till en Google Customer Match-slutpunkt i JSON-format.
      * Målgruppsmedlemskap levereras i direktuppspelande läge efter utvärderingen av direktuppspelning eller gruppsegmentering i Experience Platform.
1. Kontrollera att målgruppen har levererats till destinationen som förväntat.
   * Kontrollera övervakningsgränssnittet för att bekräfta att målgruppen levererades med det förväntade antalet profiler. Målgruppens storlek bör återspegla det förväntade antalet profiler som är aktiverade, och observera att specifika mål som Facebook och Google kräver vissa fält, till exempel en e-posthash-identitet, och om de inte finns i profilen som är medlem av målgruppen aktiveras de inte till målplatsen.
   * Kontrollera om det finns profiler som hoppats över för att se om det saknas profiler eller attribut som var obligatoriska saknas.
   * Kontrollera om det finns andra fel som behöver åtgärdas.
1. Kontrollera att målgruppen aktiverades till slutmålet med det förväntade antalet målgruppsmedlemskap.
   * Logga in på Facebooks anpassade målgruppsportal för att verifiera målgruppen från kunddataplattformen i realtid och att matchningsfrekvensen för profiler i målgruppen på Facebook på ett rimligt sätt matchar antalet profiler i målgruppen från kunddataplattformen i realtid.
   * När aktiveringsflödet är klart växlar du till ditt Google Ads-konto. De aktiverade segmenten visas i ditt Google-konto som kundlistor. Observera att beroende på segmentstorleken fyller vissa målgrupper inte i bilden om det inte finns fler än 100 aktiva användare att betjäna.

## Skyddsräcken

[Profil- och segmenteringsstödlinjer](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=sv-SE)

## Relaterad dokumentation

Aktivering till anpassade målgrupper på Facebook - [målkonfiguration](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/social/facebook.html?lang=sv-SE)

Aktivering av Google kundmatchning - [målkonfiguration](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-customer-match.html?lang=sv-SE)