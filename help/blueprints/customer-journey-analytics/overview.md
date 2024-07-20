---
title: Customer Journey Analytics-ritningar
description: Sammanställ och analysera data och kundbeteenden från hela kundresan
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 3bb2dada-f4cd-43f7-a0d0-f276510ad224
source-git-commit: b69e73349741b829f05d04cfac70aa0161ef7684
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 7%

---

# Customer Journey Analytics-ritningar

Customer Journey Analytics visar hur varumärken kan sammanställa kunddata och kundbeteenden från olika interaktionskanaler och källor för att skapa en resebaserad bild av alla kundinteraktioner. Rapportering och analys kan utföras i programtjänsten Customer Journey Analytics för att utvärdera och få insikt i kundinteraktions- och beteendemönster.

En fullständig lista över användningsfall för Customer Journey Analytics finns i Customer Journey Analytics-dokumentationen som finns här.

## Användningsexempel i Customer Journey Analytics

[Exempel på vanliga användningsområden](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/cja-usecases.html?lang=en) är:

* Create and Publish Auditions to Real-time Customer Data Platform
* Konvertera banor uppifrån och ned
* Kanalengagemang och -konvertering
* Viktigaste visade innehåll
* De viktigaste kategorierna och produkterna
* Vilka kampanjer resulterade i konvertering och ökat engagemang
* Verktygsanvändningsanalys för att optimera självbetjäning

## Arkitektur för Customer Journey Analytics

![Arkitekturdiagram](assets/CJA.svg){zoomable="yes"}

Exempel på primära användningsområden är följande:

| Blueprint | Beskrivning | Experience Cloud-program |
|---|---|---|
| **[Reseanalys över flera kanaler](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/cross-channel.html)** | <ul><li>Få en samlad bild av kundernas beteende i olika kanaler genom att samla data från olika webb-, mobil- och offlineegenskaper.</li></ul> | <ul><li>Adobe Experience Platform</li><li>Customer Journey Analytics</li><li>Adobe Analytics (valfritt)</li></ul> |
| **[Publish-målgrupper till Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html)** | <ul><li>skapa och publicera målgrupper som identifieras i Customer Journey Analytics (CJA) till kundprofilen i realtid i Adobe Experience Platform för kundanpassning och personalisering. Idealiskt för att skapa målgrupper med hjälp av historiska data eller mer raffinerade målgrupper från granulatfiltrering och beräknade fält i Customer Journey Analytics.</li></ul> | <ul><li>Real-time Customer Data Platform</li><li>Customer Journey Analytics</li> |
| **[Anropa avböjningsreseanalys](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/call-center.html)** | <ul><li>Bestäm vilka beteenden som är mest indikativa och skapa agentstödda samtal genom att samla ihop data från Call Center med webb-, mobil- och andra interaktionsdata.</li><li>Dessa insikter kan sedan användas för att optimera kundupplevelsen och minska vägen till handläggarassisterade interaktioner genom optimerat självbetjäningsinnehåll och verktyg.  </li></ul> | <ul><li>Adobe Experience Platform</li><li>Customer Journey Analytics</li> |

## Guardrail-diagram för ritningar från Customer Journey Analytics

* Detaljerade skyddsförslag och sista-till-sista-latenser finns i dokumentet [Distributionsskyddsförslag](../experience-platform/deployment/guardrails.md)

![Skyddsdiagram](../experience-platform/deployment/assets/CJA_guardrails.svg){zoomable="yes"}

## Relaterade blogginlägg

* [[!DNL Blueprint for Multi-Channel Orchestration in Adobe Experience Platform]](https://medium.com/adobetech/blueprint-for-multi-channel-orchestration-in-adobe-experience-platform-c68317e94184){target="_blank"}
* [[!DNL Leveraging External Data Platforms in Adobe Experience Platform Journey Orchestration]](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17){target="_blank"}
* [[!DNL Event-Based Triggering on Adobe Experience Platform Orchestration Service using Apache Airflow]](https://medium.com/adobetech/event-based-triggering-on-adobe-experience-platform-orchestration-service-using-apache-airflow-8607b28251f1){target="_blank"}
* [[!DNL Adobe Campaign Classic Integration with Journey Orchestration]](https://medium.com/adobetech/adobe-campaign-classic-integration-with-journey-orchestration-ae577653281){target="_blank"}
* [[!DNL Demonstrating the Power of Adobe's New Journey Orchestration Service to Build Personalized Omnichannel Experiences in Real-Time]](https://medium.com/adobetech/demonstrating-the-power-of-adobes-new-journey-orchestration-service-to-build-personalized-aa60d88cd34){target="_blank"}
* [[!DNL Journey Orchestration in an Omnichannel World]](https://medium.com/adobetech/journey-orchestration-in-an-omnichannel-world-3a2d32d556d9){target="_blank"}
