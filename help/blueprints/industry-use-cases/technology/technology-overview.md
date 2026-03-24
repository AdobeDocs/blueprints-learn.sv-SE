---
title: Användningsexempel inom teknik
description: Upptäck hur teknikföretag använder Adobe Experience Platform för att samla in data, vidarebefordra händelser i realtid samt för energianalys och aktivering i olika digitala produkter.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
exl-id: a1b2c3d4-e5f6-7890-abcd-ef1234567890
source-git-commit: 77908fd8a9f4309cbe66063cd33f065424697e55
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# Användningsexempel inom teknik

Teknikföretag använder Adobe Experience Platform för att centralisera datainsamlingen från webben, mobiler och produktytor och distribuera realtidshändelser till analyser, datalager och aktiveringsdestinationer som driver deras produkter och marknadsföringsprogram. Genom att konsolidera händelseinsamlingen i toppen minskar teknikteam komplexiteten på klientsidan, förbättrar datakvaliteten och ser till att alla system i efterföljande led får konsekventa beteendedata från en enda auktoritativ källa.

## Händelsevidarebefordran i realtid

Vidarebefordra beteendehändelser i realtid som samlats in via Edge Network till tredjepartsanalyser, datalager och partnerplattformar för berikning och aktivering. Genom att centralisera händelseinhämtningen vid sidan om och vidarebefordran till flera destinationer minskar taggkostnaderna på klientsidan, förbättrar datakvaliteten och ser till att alla underordnade system får enhetliga händelsedata från en enda auktoritativ källa.

### Affärspåverkan

Teknikorganisationer som implementerar händelsevidarebefordran i realtid minskar belastningen på taggar på klientsidan och därmed sammanhängande prestandaförluster samtidigt som händelsedata blir mer enhetliga för analyser, datalager och aktiveringsmål. Vidarebefordran på serversidan minskar också sidvikten och förbättrar inläsningsprestanda, vilket direkt gynnar användarens upplevelsestatistik.

### Implementera

Använd mönstret [Händelsevidarebefordran](/help/blueprints/use-case-patterns/audience-building-activation/event-forwarding.md) för att dirigera händelser som samlats in av Adobe Experience Platform Web SDK via Edge Network till konfigurerade mål på serversidan. Det här är det rätta mönstret när målet är att distribuera server-till-server-händelser från en enda samlingspunkt, i stället för att hantera separata taggar för varje mål på klientsidan, vilket ger högre sidbredd och skapar inkonsekventa data i olika system.

### Tekniska överväganden

- Edge Network-händelsevidarebefordran kräver migrering av händelseinsamling till Adobe Experience Platform Web SDK eller Mobile SDK. Befintliga taggbaserade implementeringar måste bedömas för kompatibilitet innan vidarebefordringsmål konfigureras.
- Vidarebefordringsregler måste konfigureras så att endast de fält som krävs för varje mål skickas - undvik att vidarebefordra fullständiga XDM-nyttolaster till mål som bara behöver en liten delmängd av fält, eftersom detta ökar dataöverföringskostnaderna och skapar efterlevnadsexponering.
- Målanslutningarna måste hantera fel på ett säkert sätt. I pipelines för vidarebefordran av händelser bör återförsökslogik och varningar implementeras för mål som inte blir tillgängliga för att förhindra dataförlust vid avbrott.
- Datastyrningsprinciper måste granskas för varje vidarebefordringsmål för att säkerställa att de inställningar för användargodkännande som hämtas vid sidan av respekteras i vidarebefordringskonfigurationen.
