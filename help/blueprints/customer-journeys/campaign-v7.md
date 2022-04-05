---
title: Campaign v7 Blueprint
description: Adobe Campaign v7 är ett kampanjverktyg som är byggt för traditionella marknadsföringskanaler som e-post och direktreklam. Den erbjuder robusta ETL- och datahanteringsfunktioner för att hjälpa till att utforma och strukturera den perfekta kampanjen. Dess orkestreringsmotor ger möjlighet till multitouch-marknadsföring med fokus på batchbaserade resor.  Den levereras också tillsammans med en realtidsserver för meddelanden som gör det möjligt för marknadsföringsteamen att skicka fördefinierade meddelanden baserat på en total nyttolast från alla IT-system för exempelvis lösenordsåterställning, orderbekräftelse, e-kvitto och mycket annat.
solution: Campaign,Campaign Classic v7
exl-id: 71c808f5-59e6-4f49-a6ba-581ed508bc04
source-git-commit: 24d5ec498d09f6dac443561bd530d58a33dae7af
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 0%

---

# Campaign v7 Blueprint

Adobe Campaign v7 är ett kampanjverktyg som är byggt för traditionella marknadsföringskanaler som e-post och direktreklam. Den erbjuder robusta ETL- och datahanteringsfunktioner för att hjälpa till att utforma och strukturera den perfekta kampanjen. Dess orkestreringsmotor ger möjlighet till multitouch-marknadsföring med fokus på batchbaserade resor.  Den levereras också tillsammans med en realtidsserver för meddelanden som gör det möjligt för marknadsföringsteamen att skicka fördefinierade meddelanden baserat på en total nyttolast från alla IT-system för exempelvis lösenordsåterställning, orderbekräftelse, e-kvitto och mycket annat.

<br>

## Användningsexempel

* Batchbaserade meddelandeprogram
* Påbörja och återmarknadsföra kampanjer
* Reklam för direktreklam, broschyrer och tidskrifter
* Enkelt transaktionsmeddelande med låg volym (t.ex. lösenordsåterställning, e-postkvittenser, orderbekräftelser osv.)

<br>

## Arkitektur

<img src="assets/campaign-v7-architecture.svg" alt="Referensarkitektur för Campaign v7 Blueprint" style="width:100%; border:1px solid #4a4a4a" />

<br>

## Integrationsmönster

| Scenario | Beskrivning | Funktioner |
| :-- | :--- | :--- |
| [Journey Optimizer med Adobe Campaign](ajo-and-campaign.md) | Visar hur du kan använda Adobe Journey Optimizer för att orkestrera 1:1-upplevelser med hjälp av kundprofilen i realtid och utnyttja Adobe Campaign transaktionsmeddelandesystem för att skicka meddelandet | Utnyttja Journey Optimizer kundprofil i realtid och kraften i att orkestrera i det ögonblick upplevelserna inträffar, samtidigt som ni använder Adobe Campaign inbyggda funktioner för realtidsmeddelanden för att kommunicera på sista milen<br><br>Att tänka på:<br><ul><li>Kan skicka upp till 50 000 meddelanden per timme via meddelandeservern i realtid<li>Ingen begränsning görs från Journey Optimizer, så man kan försäkra sig om teknisk kontroll genom en företagsarkitekt före försäljningen</li><li>offer decisioning stöds inte i nyttolaster till Campaign v7-meddelandeservern i realtid</li></ul> |
| [Real-Time CDP med Adobe Campaign](rtcdp-and-campaign.md) | Visar hur Adobe Experience Platform Real-Time CDP och dess centraliserade segmenteringsverktyg kan användas tillsammans med Adobe Campaign för att leverera personaliserade konversationer | <ul><li>Delning av målgrupper från Real-Time CDP till Adobe Campaign via utbyte av molnlagringsfiler och arbetsflöden för Adobe Campaign-import </li><li>Dela enkelt data om leverans och interaktion från kundkonversationer tillbaka till CDP från Adobe Campaign i realtid för att förbättra både kundprofilen i realtid och tillhandahålla kanalövergripande rapporter om meddelandekampanjer</li></ul> |

<br>

## Förutsättningar

### Application Server och Real-Time Messaging Server

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

* Lagring kan skalas till upp till 100 miljoner profiler
* Konfigurera och styr åtkomsten till användare via Adobe Admin Console (rekommenderas) eller lokalt i själva programmet
* Datainläsning till Campaign förväntas ske via gruppfiler
   * Stöd för inläsning av API-data är främst avsett för hantering av profiler eller enkla objekt i databasen (d.v.s. skapa och uppdatera). Den är inte avsedd att användas för att läsa in stora datavolymer eller batchliknande åtgärder.
   * Det går inte att använda API:er för att läsa data för anpassade programsyften
* API-anrop är begränsade till 15 per sekund eller 150 kB per dag i skala

### Storlek på batchmeddelandeserver

* Kan skalas för att hantera upp till 2,5 miljoner meddelanden per timme

### Storlek på meddelandeserver i realtid

* Kan skicka upp till 50 000 meddelanden per timme
* Som standard etableras två meddelandeservrar i realtid. Möjlighet att skala upp till åtta meddelandeservrar i realtid.

### SMS-konfiguration

* Campaign ger möjlighet att integrera med en SMS-leverantör. Leverantören anskaffas av kunden och integreras med kampanjen för att skicka SMS-baserade meddelanden
* Stöd ges via SMPP-protokollet
* Det finns tre (3) olika typer av SMS som Adobe kan stödja:
   * SMS MT (Mobile Terminated): ett SMS som Adobe Campaign skickar till mobiltelefoner via SMPP-leverantören.
   * SMS MO (Mobile Originated): ett SMS som skickas av en mobil till Adobe Campaign via SMPP-leverantören.
   * SMS SR (statusrapport), DR eller DLR (leveranskvitto): Ett returkvitto som skickas av mobilen till Adobe Campaign via SMPP-leverantören som anger att SMS:et har tagits emot. Adobe Campaign kan också få ett SR-meddelande som anger att meddelandet inte kunde levereras, ofta med en beskrivning av felet.

### Konfiguration av Mobile Push

* Två metoder som stöds för integrering med mobila enheter för push-meddelanden:
   * Experience Platform Mobile SDK (rekommenderas)
   * Campaign Mobile SDK
* Experience Platform Mobile SDK-väg:
   * Utnyttja Adobe Tags och tillägget Campaign Classic för att integrera med Experience Platform Mobile SDK
   * behöver kunskaper om Adobe-taggar och datainsamling
   * Behöver mobilutvecklingsupplevelse med push-meddelanden i både Android och iOS för att distribuera SDK, integrera med FCM (Android) och APNS (iOS) för att få push-token, konfigurera din app så att den tar emot push-meddelanden och hantera push-interaktioner
* Campaign Mobile SDK
   * Kontakta Adobe kundtjänst för att få åtkomst
   * Följ [Kampanjens SDK-dokumentation](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/sending-push-notifications/integrating-campaign-sdk-into-the-mobile-application.html?lang=en) för att lära dig hur du installerar och konfigurerar SDK

   >[!IMPORTANT]
   >Om ni distribuerar Campaign SDK och arbetar med andra Experience Cloud-program måste de använda Experience Platform Mobile SDK för datainsamling. Detta är ett annat SDK och måste installeras tillsammans med Campaign SDK

<br>

## Implementeringssteg

Se [Starthandbok](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html?lang=en) för implementering av Adobe Campaign v7


## Relaterad dokumentation

* [Dokumentation för Campaign v7](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [Produktbeskrivning för Campaign v7](https://helpx.adobe.com/legal/product-descriptions/adobe-campaign-managed-cloud-services.html)
* [Dokumentation för Experience Platform-taggar](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Experience Platform Mobile SDK-dokumentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
