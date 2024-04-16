---
title: "[!DNL Journey Optimizer] - Triggered Messaging och Adobe Experience Platform Blueprint"
description: Kör utlösta meddelanden och upplevelser med Adobe Experience Platform som ett centralt nav för strömmande data, kundprofiler och segmentering.
solution: Journey Optimizer
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: a1f3aef5b508575019bd651b9706efc7d6db5306
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 3%

---

# [!DNL Journey Optimizer] utkast

Adobe [!DNL Journey Optimizer] är ett särskilt utformat system för marknadsföringsteam som i realtid kan reagera på kundbeteenden och möta dem där de befinner sig. Datahanteringsfunktionerna har flyttats till Adobe [!DNL Experience Platform] så att marknadsföringsteamen kan fokusera på vad de gör bäst: vilket är att skapa kundresor och personaliserade konversationer i världsklass.

Denna plan visar programmets tekniska funktioner och ger en djupdykning i de olika arkitektoniska komponenterna som utgör [!DNL Journey Optimizer].

## Användningsexempel

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
| [Meddelanden från tredje part](3rd-party-messaging.md) | Visar hur Adobe [!DNL Journey Optimizer] kan användas med meddelandesystem från tredje part för att samordna och skicka personaliserad kommunikation | Leverera personlig kommunikation direkt till kunderna när de interagerar med ert varumärke eller företag<br><br>Att tänka på:<br><ul><li>Tredjepartssystem måste ha stöd för innehavartoken för autentisering</li><li>Inget stöd för statiska IP-adresser på grund av multi-tenant-arkitektur</li><li>Var medveten om arkitektoniska begränsningar för system från tredje part när det gäller API-anrop per sekund.  Det kan vara ett behov för kunden att köpa ytterligare volym från tredjepartsleverantören för att stödja volym från [!DNL Journey Optimizer]</li><li>Stöder inte beslutshantering i meddelanden eller nyttolaster</li></ul> |

<br>

## Integreringsmönster

| Integrering | Beskrivning | Funktioner |
| :-- | :--- | :--- |
| [[!DNL Journey Optimizer] med Adobe Campaign](ajo-and-campaign.md) | Visar hur du kan använda Adobe [!DNL Journey Optimizer] för att samordna 1:1-upplevelser med kundprofilen i realtid och utnyttja Adobe Campaign transaktionsmeddelandesystem för att skicka meddelandet | Utnyttja kundprofilen i realtid och kraften i [!DNL Journey Optimizer] att orkestrera upplevelserna i ögonblicket och samtidigt använda de inbyggda realtidsfunktionerna i Adobe Campaign för att kommunicera på sista mils sätt<br><br>Att tänka på:<br><ul><li>Kampanjprogrammet måste finnas i antingen v7 build >21.1 eller v8</li><li>Meddelandegenomströmning</li><ul><li>Campaign v7 - upp till 50 000 per timme</li><li>Campaign v8 - upp till 1 MB per timme</li><li>Campaign Standard - upp till 50 000 per timme</li></ul><li>Ingen begränsning utförs, så användningsfall kräver teknisk kontroll av en företagsarkitekt</li><li>Inget stöd för att använda beslutsstöd i ett meddelande som skickas av Campaign</li></ul> |

<br>

## Förutsättningar

Adobe [!DNL Experience Platform]:

* Scheman och datauppsättningar måste konfigureras i systemet innan du kan konfigurera [!DNL Journey Optimizer] datakällor
* För Experience Event-klassbaserade scheman lägger du till fältgruppen &#39;Orchestration eventID&#39; när du vill att en händelse som inte är en regelbaserad händelse ska aktiveras
* För enskilda profilklassbaserade scheman lägger du till fältgruppen &#39;Profiltestinformation&#39; för att kunna läsa in testprofiler som ska användas med [!DNL Journey Optimizer]

E-post:

* Måste ha en underdomän klar att användas för att skicka meddelanden
* Underdomänen kan antingen delegeras helt till Adobe (rekommenderas) eller CNAME kan användas för att peka mot Adobe-specifika DNS-servrar (anpassad)
* Google TXT-post krävs för varje underdomän för att säkerställa god levererbarhet

Mobilpush:

* Kunden måste ha en mobilutvecklare tillgänglig för att kunna bygga appen
* Adobe Experience Platform Mobile SDK

## Guardrails

[[!DNL Journey Optimizer] Länk till gåtorutor](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html)

[Guardrails och Slut-till-slut-vägledning om svarstid](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

## Relaterad dokumentation

* [[!DNL Experience Platform] dokumentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [[!DNL Experience Platform] Dokumentation för taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en)
* [[!DNL Experience Platform Mobile SDK] dokumentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
* [[!DNL Journey Optimizer] dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=en)
* [[!DNL Journey Optimizer] produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
