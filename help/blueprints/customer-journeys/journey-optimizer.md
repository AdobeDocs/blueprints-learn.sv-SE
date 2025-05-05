---
title: '[!DNL Journey Optimizer] - utlöst meddelanden och Adobe Experience Platform Blueprint'
description: Kör utlösta meddelanden och upplevelser med Adobe Experience Platform som ett centralt nav för strömmande data, kundprofiler och segmentering.
solution: Journey Optimizer
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: f8b9cc115739b53bba71d06b228dcce57df9dd7b
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 4%

---

# [!DNL Journey Optimizer] utkast

Adobe [!DNL Journey Optimizer] är ett särskilt utformat system för marknadsföringsteam som i realtid kan reagera på kundbeteenden och möta dem där de befinner sig. Datahanteringsfunktionerna har flyttats till Adobe [!DNL Experience Platform], vilket gör att marknadsföringsteamen kan fokusera på vad de gör bäst: att skapa kundresor och personaliserade konversationer i världsklass.

Den här planen beskriver programmets tekniska funktioner och ger en djup genomgång av de olika arkitektoniska komponenterna som består av [!DNL Journey Optimizer].

## Användningsfall

* Utlösta meddelanden
* Välkomstbekräftelse och registreringsbekräftelse
* Kundvagn och blankettinlämning
* Platsutlösta meddelanden
* Erfarenheter på stadion
* Resor och turism före ankomst och vistelse

## Arkitektur

<img src="assets/ajo-architecture.svg" alt="Referensarkitektur Journey Optimizer - utkast" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## Scenarier

| Scenario | Beskrivning | Funktioner |
| :-- | :--- | :--- |
| [Meddelanden från tredje part](3rd-party-messaging.md) | Visar hur Adobe [!DNL Journey Optimizer] kan användas med meddelandesystem från tredje part för att orkestrera och skicka personaliserad kommunikation | Leverera 1:1 i ögonblicket personaliserad kommunikation till kunder när de interagerar med ert varumärke eller ert företag<br><br>Överväganden:<br><ul><li>Tredjepartssystem måste ha stöd för innehavartoken för autentisering</li><li>Inget stöd för statiska IP-adresser på grund av multi-tenant-arkitektur</li><li>Var medveten om arkitektoniska begränsningar för system från tredje part när det gäller API-anrop per sekund.  Det kan vara ett behov för kunden att köpa ytterligare volym från tredjepartsleverantören för supportvolym från [!DNL Journey Optimizer]</li><li>Stöder inte beslutshantering i meddelanden eller nyttolaster</li></ul> |

<br>

## Integreringsmönster

| Integrering | Beskrivning | Funktioner |
| :-- | :--- | :--- |
| [[!DNL Journey Optimizer] med Adobe Campaign](ajo-and-campaign.md) | Visar hur du kan använda Adobe [!DNL Journey Optimizer] för att orkestrera 1:1-upplevelser med hjälp av kundprofilen i realtid och utnyttja Adobe Campaign transaktionsmeddelandesystem för att skicka meddelandet | Utnyttja kundprofilen i realtid och kraften hos [!DNL Journey Optimizer] för att orkestrera i det ögonblick upplevelserna inträffar, samtidigt som ni använder de inbyggda meddelandefunktionerna i Adobe Campaign i realtid för att göra den senaste ledighetskommunikationen<br><br>Överväganden:<br><ul><li>Kampanjprogrammet måste finnas i antingen v7 build >21.1 eller v8</li><li>Meddelandegenomströmning</li><ul><li>Campaign v7 - upp till 50 000 per timme</li><li>Campaign v8 - upp till 1 MB per timme</li><li>Campaign Standard - upp till 50 000 per timme</li></ul><li>Ingen begränsning utförs, så användningsfall kräver teknisk kontroll av en företagsarkitekt</li><li>Inget stöd för att använda beslutsstöd i ett meddelande som skickas av Campaign</li></ul> |

<br>

## Förutsättningar

Adobe [!DNL Experience Platform]:

* Scheman och datauppsättningar måste konfigureras i systemet innan du kan konfigurera [!DNL Journey Optimizer]-datakällor
* För Experience Event-klassbaserade scheman lägger du till fältgruppen &#39;Orchestration eventID&#39; när du vill att en händelse som inte är en regelbaserad händelse ska aktiveras
* För enskilda profilklassbaserade scheman lägger du till fältgruppen Profiltestinformation för att kunna läsa in testprofiler som ska användas med [!DNL Journey Optimizer]

E-post:

* Måste ha en underdomän klar att användas för att skicka meddelanden
* Underdomänen kan antingen delegeras helt till Adobe (rekommenderas) eller CNAME kan användas för att peka mot Adobe-specifika DNS-servrar (anpassad)
* Google TXT-post krävs för varje underdomän för att säkerställa god levererbarhet

Mobilpush:

* Kunden måste ha en mobilutvecklare tillgänglig för att kunna bygga appen
* Adobe Experience Platform Mobile SDK

## Skyddsräcken

[[!DNL Journey Optimizer] Produktlänk för säkerhetsutkast](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/get-started/guardrails)

[Garantier och Vägledning för svarstid från slut till slut](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=sv-SE)

## Relaterad dokumentation

* [[!DNL Experience Platform] dokumentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=sv-SE)
* [[!DNL Experience Platform] Dokumentation för taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv-SE)
* [[!DNL Experience Platform Mobile SDK] dokumentation](https://experienceleague.adobe.com/docs/mobile.html?lang=sv-SE)
* [[!DNL Journey Optimizer] dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=sv-SE)
* [[!DNL Journey Optimizer] produktbeskrivning](https://helpx.adobe.com/se/legal/product-descriptions/adobe-journey-optimizer.html)
