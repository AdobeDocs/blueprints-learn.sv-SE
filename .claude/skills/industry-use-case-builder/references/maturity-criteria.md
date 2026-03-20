---
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---
# Kriterier för bedömning av fallets förfallotid

## Löptider

### Foundational

**Märke:** `[!BADGE Foundational]{type=Neutral}`

Ett användningsfall är **Foundational** när det:

- Mappar till ett enstegs- eller händelseutlösande mönster (händelseutlöst meddelanden, batchaktivering av utgående meddelanden)
- Har enkla datakrav (händelsetyp, standardprofilattribut)
- Kräver minimala eller inga AI/ML-funktioner
- Använder standardkanalleverans (e-post, SMS, push) utan komplex samordning
- Har väletablerade implementeringsmönster med tydlig bästa praxis
- Kräver färre systemintegreringar (vanligtvis 1-2 datakällor)

**Typiska mönster:** Meddelanden som utlösts av händelser, aktivering av utgående meddelanden i grupp

**Exempel:** Återställning av övergiven kundvagn, påminnelser om avtalad tid, tjänstmeddelanden, påminnelser om prisfall, påminnelser om fakturabetalning

### Nya

**Märke:** `[!BADGE Emerging]{type=Informative}`

Ett användningsfall är **Emerging** när det:

- Mappar till ett personaliseringsmönster i flera steg (Multi-Step Orchestrated Journey, Known-Visitor Personalization, Behavioral recommendation, Anonymous Visitor Personalization)
- Kräver insamling och analys av beteendedata
- Använder rekommendationsmodeller eller profilupplösning för kända besökare
- Involverar multitouch-moderssekvenser med förgreningslogik
- Har måttlig komplexitet i integreringen (2-4 datakällor)
- Kan kräva målgruppsaktivering eller segmentbaserad målinriktning

**Typiska mönster:** Orchestrated Journey i flera steg, Known-Visitor Web/App Personalization, Behavioral recommendation, Anonymous Visitor Web Personalization, B2B Audience Activation

**Exempel:** Välkomstserier, uppföljningskampanjer för medicinering, personliga kontouppsättningar, poängsättning för leads, innehållsrekommendationer

### Avancerat

**Märke:** `[!BADGE Advanced]{type=Caution}`

Ett användningsfall är **Avancerat** när det:

- Mappar till ett decimalmönster eller flerkanalsmönster (Cross-Channel Journey with Decision, Offer Decisioning)
- Kräver AI-baserad prediktion eller benägenhetsbedömning
- Använder centraliserad beslutslogik i flera kanaler samtidigt
- Omfattar komplex samordning med realtidsbeslut vid flera respunkter
- Har hög integrationskomplexitet (över 4 datakällor, dataflöden i realtid)
- Kräver avancerade affärsregler, prioritetshantering och frekvensstyrning

**Typiska mönster:** Flerkanalsresa med beslut, Offer Decisioning

**Exempel:** Kravförebyggande med AI-poäng, produktrekommendationer i vardagsstadiet, optimering av korsförsäljning, personalisering av lojalitetsprogram, exklusiva erbjudanden från VIP

## Utvärderingsarbetsflöde

1. Identifiera vilket fallmönster som användningsfallet mappas till
2. Se listan&quot;Typiska mönster&quot; ovan för att få en snabb matchning
3. Om mönstret inte tydligt visar mognad, ska du utvärdera datakomplexitet, AI/ML-krav och integreringsomfång
4. Presentera utvärderingen för användaren med en motivering: &quot;Baserat på mönstermappningen ({pattern}) och {key factors} klassificerar jag den som {level} eftersom {reasoning}.&quot;
5. Låt användaren bekräfta eller åsidosätta innan han/hon fortsätter
