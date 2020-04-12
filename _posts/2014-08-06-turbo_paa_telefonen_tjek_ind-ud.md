---
layout: post
title: (DA) Turbo på telefonen - tjek ind / ud
---

**TL**;**DR** - Jeg har lavet en arbejdsgang, der minder mig om at tjekke ind / ud vha. en automatiseret proces, når jeg ankommer eller forlader arbejdet.

![If This Then That]({{ site.url }}/public/assets/20140806_ifttt@2x.jpg)

Hver dag, når jeg ankommer på arbejde logger jeg min ankomsttid i et [Google Spreadsheet][]. Her laver jeg en række med en tjek ind tid og så gør jeg det samme, når jeg går. På den måde kan jeg holde øje med om jeg arbejder for meget eller for lidt. Relativt simpelt, men også ret besværligt, hvis jeg skal ind og "håndskrive" det hver gang. Så derfor har jeg lavet en automatiseret løsning med lidt fiks sammenblanding af appen [Launch Center Pro][] (LCP) og tjenesten [If This Then That][IFTTT] (IFTTT).

Med [LCP-app'en][] har jeg defineret to handlinger; en til tjek ind og en til tjek ud. Begge handlinger bliver 'trigget' via et geofence, når jeg hhv. ankommer og forlader mit arbejde. Når det sker, spørger LCP om jeg vil køre handlingen og gør jeg det starter jeg en prædefineret handling via [IFTTT-app'en][].

Launch Center Pro handlingerne er relativt simple; de starter blot hver deres IFTTT-handling med det *præcise* IFTTT-navn angivet i mellem `\{\{` og `\}\}`.

Stempel ind: `launch://ifttt/trigger?name\{\{Stempel ind\}\}`

Stempel ud: `launch://ifttt/trigger?name\{\{Stempel ud\}\}`

Det mere interessante arbejde ligger i deres respektive IFTTT handlinger[^1], som laver det tunge arbejde med at skrive til regnearket.

Det der sker, når de bliver startet er, at de åbner regnearket navngivet som angivet i "Spreadsheet name" i mappen defineret i "Drive folder path" og skriver indholdet i "Formattet row" i næste ledige række. Indholdet i formattet row har jeg så sat til at være `Stemplet ud`, skifter til næste kolonne i regnearket med `|||` og skriver der det aktuelle tidspunkt med `{{TriggeredAt}}`, som er en special IFTTT-angivelse af det specifikke tidspunkt gældende for ens iOS-enhed. Se handlingerne herunder.

<a href="https://ifttt.com/view_embed_recipe/194027-tjek-ind" target = "_blank" class="embed_recipe embed_recipe-l_8" id= "embed_recipe-194027"><img src= 'https://ifttt.com/recipe_embed_img/194027' alt="IFTTT Recipe: Tjek ind connects launch-center to google-drive" width="370px" style="max-width:100%"/></a><script async type="text/javascript" src= "//ifttt.com/assets/embed_recipe.js"></script>

<a href="https://ifttt.com/view_embed_recipe/194028-tjek-ud" target = "_blank" class="embed_recipe embed_recipe-l_7" id= "embed_recipe-194028"><img src= 'https://ifttt.com/recipe_embed_img/194028' alt="IFTTT Recipe: Tjek ud connects launch-center to google-drive" width="370px" style="max-width:100%"/></a><script async type="text/javascript" src= "//ifttt.com/assets/embed_recipe.js"></script>

Når begge dele af af de to arbejdsgange er på plads *og* har jeg sat LCP op til at minde mig om at tjekke ind, når jeg ankommer til arbejde og når jeg går fra arbejdet ser det så således ud, når jeg ankommer på arbejdet (billedet til venstre herunder) og med et swipe på  påmindelsen, startes tjek ind handlingen (billedet til højre)[^2].

![Screenshot af arbejdsgang]({{ site.url }}/public/assets/20140806_iphone_screenshot@2x.png)

Et voila! Du har nu tjekket ind på arbejde.

[Launch Center Pro]: http://contrast.co/launch-center-pro/
[LCP-app'en]: https://itunes.apple.com/da/app/launch-center-pro/id532016360?mt=8
[Google Spreadsheet]: http://www.google.com/sheets/about/
[IFTTT]: http://ifttt.com
[IFTTT-app'en]: https://itunes.apple.com/dk/app/ifttt/id660944635?mt=8

[^1]: Selvom de faktisk også er ret simple.
[^2]: Det hele kunne også godt gøres fuldautomatisk - det skal jeg til at gøre for min kone - men jeg kommer relativt ofte forbi min arbejdsplads i fritiden og der vil jeg helst ikke risikere af stemple ind (eller ud).
