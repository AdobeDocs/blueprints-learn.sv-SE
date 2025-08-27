---
title: Campaign v8, Blueprint, Campaign & Platform
description: Läs mer om planen för Campaign v8.
solution: Campaign,Campaign v8
version: Campaign v8
exl-id: 89b3a761-9cb3-4e01-8da0-043e634fa61f
source-git-commit: 0a3ebcbc6029df46bd988cb8f15ecf838f80c3c9
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 0%

---

# Campaign v8-utkast

Adobe Campaign v8 är nästa generation av kampanjhanteringsplattform som utformats för traditionella marknadsföringskanaler som e-post och direktreklam. Det erbjuder robusta funktioner för ETL och datahantering för att stödja komplex segmentering och målgruppsanpassning, tillsammans med en kraftfull orkestreringsmotor för att skapa multi-touch, batchstyrda marknadsföringsprogram.

Den innehåller också en skalbar realtidsserver för meddelanden som möjliggör transaktionskommunikation - t.ex. lösenordsåterställningar, orderbekräftelser och e-kvitton - genom att man godkänner fullständiga nyttolaster från externa system för omedelbar leverans.

## Användningsfall

>[!BEGINTABS]

>[!TAB Kör gruppkampanj]

- Utforma och leverera storskaliga, schemalagda marknadsföringskampanjer för e-post, SMS och direktreklam.
- Perfekt för reklamblad, nyhetsbrev och säsongserbjudanden med komplex segmentering och målinriktning.

>[!TAB Multi-Touch-orkestrering]

- Skapa flerstegsprogram för flera kanaler som vägleder kunderna genom en fördefinierad marknadsföringsresa.
- Har stöd för återinträde, villkorlig logik och tidsbaserade övergångar.

>[!TAB Datahantering och ETL]

- Infoga, omvandla och hantera kunddata från olika källor för att få exakt målinriktning.
- Gör att du kan skapa egna scheman, beräknade fält och målgruppsdefinitioner.

>[!TAB Transactional Messaging]

- Skicka fördefinierade meddelanden i realtid som triggas av externa system (t.ex. lösenordsåterställningar, orderbekräftelser, e-kvitton).
- Använder en skalbar meddelandeserver som tar emot fullständiga nyttolaster från IT-system för omedelbar leverans.

>[!ENDTABS]

<br>

## Arkitekturdiagram

Läs mer om [Campaign v8-distributionsmodeller](https://experienceleague.adobe.com/docs/campaign/campaign-v8/config/architecture/architecture.html#ac-deployment){target="_blank"}.

### Driftsättning av kampanjföretag (FFDA)

<img src="images/campaign-v8-ffda.svg" alt="Referensarkitektur för driftsättningsutkast för Campaign v8 (FFDA)" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

### Driftsättning av Campaign v8 FDA

<img src="images/campaign-v8-fda.svg" alt="Referensarkitektur för Campaign v8 (FDA)-utkast" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## Integreringsmönster

| Scenario | Beskrivning | Tekniska överväganden |
| :-- | :--- | :--- |
| [[!DNL Real-time Customer Data Platform] med Adobe [!DNL Campaign]](rtcdp-and-campaign-v8.md) | Visar hur Adobe Experience Platform och dess kundprofil i realtid och centraliserade segmenteringsverktyg kan användas med Adobe [!DNL Campaign] för att leverera personaliserade konversationer | <ul><li>Delning av profiler och målgrupper från [!DNL Real-Time CDP] till Adobe [!DNL Campaign] via utbyte av molnlagringsfiler och Adobe [!DNL Campaign]-arbetsflöden för inhämtning </li><li>Dela enkelt leverans- och interaktionsdata från kundkonversationer tillbaka till [!DNL Real-Time CDP] från Adobe [!DNL Campaign] för att förbättra både kundprofilen i realtid och tillhandahålla kanalövergripande rapporter om meddelandekampanjer</li></ul> |
| [[!DNL Journey Optimizer] med Adobe [!DNL Campaign]](ajo-and-campaign-v8.md) | Visar hur du kan använda Adobe Journey Optimizer för att orkestrera 1:1-upplevelser med hjälp av kundprofilen i realtid och utnyttja det inbyggda transaktionsmeddelandesystemet i Adobe [!DNL Campaign] för att skicka meddelandet | <ul><li>Kan skicka upp till 1 miljon meddelanden per timme via meddelandeservern i realtid<li>Ingen begränsning har utförts från [!DNL Journey Optimizer] så kontrollera teknisk kontroll av en företagsarkitekt före försäljning</li><li>Beslutshantering stöds inte i nyttolaster till Campaign v8</li></ul> |

<br>

## Förutsättningar

Följande krav gäller för den här planen.

### Programserver och meddelandeserver i realtid

- Adobe [!DNL Campaign] Client Console krävs för att interagera och använda programvaran [!DNL Campaign] v8. Det är en Windows-baserad klient som använder vanliga Internet-protokoll (SOAP, HTTP, etc.). Kontrollera att du har de behörigheter som krävs aktiverade i organisationen för att distribuera, installera och köra programvara

- Lista över tillåtna IP-adresser:
   - Identifiera de IP-intervall som alla användare utnyttjar vid åtkomst till klientkonsolen.
   - Identifiera vilka affärssystem som får användas för att kommunicera med Real-Time Messaging-servern och se till att de har en statiskt tilldelad IP eller ett intervall som ni kan tillåta.
   - Detta kan konfigureras och styras via Campaign-kontrollpanelen.
- Nyckelhantering via FTP:
   - Ha offentliga SSH-nycklar tillgängliga för användning med Campaign via sFTP. Detta kan konfigureras och styras via Campaign-kontrollpanelen.

### E-post

- Ha en underdomän klar att användas för att skicka meddelanden.
- Underdomänen kan antingen delegeras helt till Adobe (rekommenderas) eller CNAME kan användas för att peka på Adobe-specifika DNS-servrar (anpassade).
- Google TXT-post krävs för varje underdomän för att säkerställa god levererbarhet.

### Mobilpush

- Ha en mobilutvecklare tillgänglig för att driftsätta, konfigurera och bygga mobilappen.
- Adobe tillhandahåller bara en SDK som samlar in den information som behövs från FCM (Android) och APNS (iOS) för att skicka meddelandenyttolaster till sina servrar. Kunden ansvarar för hur mobilappen behöver kodas, distribueras, hanteras och felsökas.

### Webbprogram (valfritt)

- Kan delegera ytterligare en underdomän för Campaign-värdbaserade avbeställnings- och landningssidor.
- SSL-certifikat rekommenderas.

<br>

## Skyddsräcken

### Programserverns storlek

- Lagring kan skalas upp till 200 MB-profiler med möjlighet att skala upp till 1B-profiler.
- Konfigurera och kontrollera användaråtkomst via Adobe [!DNL Admin Console].
- Datainläsning till [!DNL Campaign] förväntas göras via gruppfiler:
   - Stöd för inläsning av API-data är främst avsett för hantering av profiler eller enkla objekt i databasen (d.v.s. skapa och uppdatera). Den är inte avsedd att användas för att läsa in stora datavolymer eller batchliknande åtgärder.
   - Det går inte att använda API:er för att läsa data för anpassade programsyften
   - Data som läses in via API mellanlagras i programdatabasen och replikeras sedan varje timme till molndatabasen
- Begränsningar för API-anrop gäller. Läs mer i [Adobe Campaign produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-campaign-managed-cloud-services.html){target="_blank"}.

### Storlek på batchmeddelandeserver

- Kan skalas för att hantera upp till 20 miljoner meddelanden per timme

### Storlek på meddelandeserver i realtid

- Kan skicka upp till 1 miljon meddelanden per timme
- Som standard etableras två meddelandeservrar i realtid. Möjlighet att skala upp till åtta meddelandeservrar i realtid.

### SMS-konfiguration

- Campaign ger möjlighet att integrera med en SMS-leverantör. Leverantören anskaffas av kunden och integreras med kampanjer för att skicka SMS-baserade meddelanden.
- Stöd ges via SMPP-protokollet.
- Det finns tre (3) olika typer av SMS som Adobe kan stödja:
   - SMS MT (Mobile Terminated): Ett SMS som skickas av Adobe [!DNL Campaign] till mobiltelefoner via SMPP-providern.
   - SMS MO (Mobile Originated): Ett SMS som skickas av en mobil till Adobe [!DNL Campaign] via SMPP-providern.
   - SMS SR (statusrapport), DR eller DLR (leveranskvitto): ett returkvitto som skickas av mobilen till Adobe [!DNL Campaign] via SMPP-providern som anger att SMS:et har tagits emot. Adobe [!DNL Campaign] kan också få SR som anger att meddelandet inte kunde levereras, ofta med en beskrivning av felet.

<br>

## Implementeringssteg

Se guiden Komma igång för [Implementera Adobe Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/implement/implement.html)

## Relaterad dokumentation

- [Kampanjdokumentation v8](https://experienceleague.adobe.com/docs/campaign-v8.html)
- [Produktbeskrivning för Campaign v8](https://helpx.adobe.com/legal/product-descriptions/adobe-campaign-managed-cloud-services.html)
- [Experience Platform Tags-dokumentation](https://experienceleague.adobe.com/docs/launch.html)
- [Experience Platform Mobile SDK-dokumentation](https://experienceleague.adobe.com/docs/mobile.html)