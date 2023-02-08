---
title: Campaign v8-plan, Campaign & Platform
description: Adobe Campaign v8 är nästa generations kampanjverktyg som tagits fram för traditionella marknadsföringskanaler som e-post och direktreklam. Den erbjuder robusta ETL- och datahanteringsfunktioner för att hjälpa till att utforma och strukturera den perfekta kampanjen. Dess orkestreringsmotor ger möjlighet till multitouch-marknadsföring med fokus på batchbaserade resor.  Den levereras också tillsammans med en skalbar meddelandeserver i realtid som gör det möjligt för marknadsföringsteamen att skicka fördefinierade meddelanden baserat på en totalbelastning från alla IT-system för exempelvis lösenordsåterställning, orderbekräftelse, e-kvitto och mycket annat.
solution: Campaign,Campaign v8
exl-id: 89b3a761-9cb3-4e01-8da0-043e634fa61f
source-git-commit: dabb5ae0bf2fc186f67d4aa93a2e9e8c5bb04498
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 2%

---

# Campaign v8, utkast

Adobe Campaign v8 är nästa generations kampanjverktyg som tagits fram för traditionella marknadsföringskanaler som e-post och direktreklam. Den erbjuder robusta ETL- och datahanteringsfunktioner för att hjälpa till att utforma och strukturera den perfekta kampanjen. Dess orkestreringsmotor ger möjlighet till multitouch-marknadsföring med fokus på batchbaserade resor.  Den levereras också tillsammans med en skalbar meddelandeserver i realtid som gör det möjligt för marknadsföringsteamen att skicka fördefinierade meddelanden baserat på en totalbelastning från alla IT-system för exempelvis lösenordsåterställning, orderbekräftelse, e-kvitto och mycket annat.

<br>

## Användningsexempel

* Mycket komplexa batchbaserade meddelandeprogram
* Påbörja och återmarknadsföra kampanjer
* Reklam för direktreklam, broschyrer och tidskrifter
* Enkelt transaktionsmeddelande (t.ex. lösenordsåterställning, e-postkvittenser, orderbekräftelser etc.)
* Integrering av Campaign-data till Adobe Experience Platform för analys och profilskapande
* Dela Real-time Customer Data Platform målgrupper med Campaign.

<br>

## Arkitektur

<img src="assets/campaign-v8-architecture.svg" alt="Referensarkitektur för Campaign v8-utkast" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Integreringsmönster

| Scenario | Beskrivning | Funktioner |
| :-- | :--- | :--- |
| [Kunddataplattform i realtid med Adobe Campaign](rtcdp-and-campaign-v8.md) | Visar hur Adobe Experience Platform och dess kundprofil i realtid och centraliserade segmenteringsverktyg kan användas med Adobe Campaign för att leverera personanpassade konversationer | <ul><li>Delning av profiler och målgrupper från Real-Time CDP till Adobe Campaign med hjälp av molnlagringsfilsutbyte och arbetsflöden för inhämtning från Adobe Campaign </li><li>Dela enkelt data om leverans och interaktion från kundkonversationer tillbaka till Real-Time CDP från Adobe Campaign för att förbättra både kundprofilen i realtid och tillhandahålla flerkanalsrapportering om meddelandekampanjer</li></ul> |
| [Journey Optimizer med Adobe Campaign](ajo-and-campaign.md) | Visar hur du kan använda Adobe Journey Optimizer för att orkestrera 1:1-upplevelser med hjälp av kundprofilen i realtid och utnyttja Adobe Campaign transaktionsmeddelandesystem för att skicka meddelandet | Utnyttja Journey Optimizer kundprofil i realtid och kraften i att orkestrera i det ögonblick upplevelserna inträffar, samtidigt som ni använder Adobe Campaign inbyggda funktioner för realtidsmeddelanden för att kommunicera på sista milen<br><br>Att tänka på:<br><ul><li>Kan skicka upp till 1 miljon meddelanden per timme via meddelandeservern i realtid<li>Ingen begränsning görs från Journey Optimizer, så man kan försäkra sig om teknisk kontroll genom en företagsarkitekt före försäljningen</li><li>Beslutshantering stöds inte i nyttolaster till Campaign v8</li></ul> |

<br>

## Förutsättningar


### Programserver och meddelandeserver i realtid

* Adobe Campaign Client Console krävs för att interagera och använda Campaign v8-programmet. Det är en Windows-baserad klient som använder standardInternet-protokoll (SOAP, HTTP osv.). Kontrollera att du har de behörigheter som krävs aktiverade i organisationen för att distribuera, installera och köra programvara

* Tillåt listning av IP-adress
   * Identifiera de IP-intervall som alla användare kommer att utnyttja vid åtkomst till klientkonsolen
   * Identifiera vilka affärssystem som kommer att få användas för att prata med Real-Time Messaging-servern och se till att de har en statiskt tilldelad IP eller ett intervall som du kan tillåtelselista
   * Detta kan konfigureras och styras via Campaign Control Panel
* Nyckelhantering via FTP
   * Ha offentliga SSH-nycklar tillgängliga för användning med Campaign via sFTP. Detta kan konfigureras och styras via Campaign-kontrollpanelen.

### E-post

* Ha en underdomän klar att användas för att skicka meddelanden
* Underdomänen kan antingen delegeras helt till Adobe (rekommenderas) eller CNAME kan användas för att peka mot Adobe-specifika DNS-servrar (anpassad)
* Google TXT-post krävs för varje underdomän för att säkerställa god levererbarhet

### Mobilpush

* Ha en mobilutvecklare tillgänglig för att driftsätta, konfigurera och bygga mobilappen
* Adobe tillhandahåller bara ett SDK för att samla in den information som behövs från FCM (Android) och APNS (iOS) för att skicka meddelandenyttolaster till sina servrar. Kunden ansvarar för hur mobilappen behöver kodas, driftsättas, hanteras och felsökas

### Webbprogram (valfritt)

* Kan delegera ytterligare en underdomän för Campaign-värdbaserade avbeställnings- och landningssidor
* SSL-certifikat rekommenderas

<br>

## Guardrails

### Programserverns storlek

* Lagring kan skalas upp till 200 M-profiler med möjlighet att skala upp till 1B-profiler
* Konfigurera och styr åtkomsten till användare via Adobe Admin Console
* Datainläsning till Campaign förväntas ske via gruppfiler
   * Stöd för inläsning av API-data är främst avsett för hantering av profiler eller enkla objekt i databasen (d.v.s. skapa och uppdatera). Den är inte avsedd att användas för att läsa in stora datavolymer eller batchliknande åtgärder.
   * Det går inte att använda API:er för att läsa data för anpassade programsyften
   * Data som läses in via API mellanlagras i programdatabasen och replikeras sedan varje timme till molndatabasen
* API-anrop är begränsade till 15 per sekund eller 150 kB per dag i skala

### Storlek på batchmeddelandeserver

* Kan skalas för att hantera upp till 20 miljoner meddelanden per timme

### Storlek på meddelandeserver i realtid

* Kan skicka upp till 1 miljon meddelanden per timme
* Som standard etableras två meddelandeservrar i realtid. Möjlighet att skala upp till åtta meddelandeservrar i realtid.

### SMS-konfiguration

* Campaign ger möjlighet att integrera med en SMS-leverantör. Leverantören anskaffas av kunden och integreras med kampanjen för att skicka SMS-baserade meddelanden
* Stöd ges via SMPP-protokollet
* Det finns tre (3) olika typer av SMS som Adobe kan stödja:
   * SMS MT (Mobile Terminated): ett SMS som Adobe Campaign skickar till mobiltelefoner via SMPP-leverantören.
   * SMS MO (Mobile Originated): ett SMS som skickas av en mobil till Adobe Campaign via SMPP-leverantören.
   * SMS SR (statusrapport), DR eller DLR (leveranskvitto): Ett returkvitto som skickas av mobilen till Adobe Campaign via SMPP-leverantören som anger att SMS:et har tagits emot. Adobe Campaign kan också få ett SR-meddelande som anger att meddelandet inte kunde levereras, ofta med en beskrivning av felet.

### Mobil push-konfiguration

* Endast Campaign SDK stöds för Campaign v8. Kontakta Adobe kundtjänst för att få åtkomst
* Följ [Kampanjens SDK-dokumentation](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/sending-push-notifications/integrating-campaign-sdk-into-the-mobile-application.html?lang=en) för att lära dig hur du installerar och konfigurerar SDK

   >[!IMPORTANT]
   >För andra Experience Cloud-program måste Experience Platform Mobile SDK användas för datainsamling. Detta är ett annat SDK och måste installeras tillsammans med Campaign SDK

<br>

## Implementeringssteg

Se guiden Komma igång för [Implementera Adobe Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/implement/implement.html?lang=en)


## Relaterad dokumentation

* [Kampanjdokumentation v8](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=en)
* [Produktbeskrivning för Campaign v8](https://helpx.adobe.com/legal/product-descriptions/adobe-campaign-managed-cloud-services.html)
* [Dokumentation för Experience Platform-taggar](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Experience Platform Mobile SDK-dokumentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
