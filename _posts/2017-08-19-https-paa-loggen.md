---
layout: post
title: HTTPS på loggen
---

**[TL;DR](http://en.wikipedia.org/wiki/Wikipedia:Too_long;_didn't_read)** - Der er kommet hængelås på siden her, men trafikken er kun krypteret mellem browseren og [CDN](https://en.wikipedia.org/wiki/Content_delivery_network)'en. Er det så nok? (Spoiler: Ja, det er det.)

![https://]({{ site.url }}/public/assets/20170819_https.jpg)
<!--more-->

Indtil nu har al trafik mellem de besøgende og siden her været læsbar af tredje part. Det betyder at alle, der kan finde ud af at lytte på trafikken, principielt har haft mulighed for at opsnappe hvad man læser her på siden. Nu har jeg dog langt om længe fået lagt et ekstra lag af sikkerhed på, så det pludselig er langt mere besværligt (men ikke umuligt). Til det formål bruger jeg [Cloudflares Flexible](https://www.cloudflare.com/ssl/) option. Det betyder at kommunikation mellem browseren og Cloudflares datacentre er krypteret, men at forbindelsen fra Cloudflares datacenter til [GitHub](https://github.com/) _ikke_ er.

<img class="screen" src="{{ site.url }}/public/assets/20170819_cloudflare-flexible-ssl.jpg" alt="Cloudfare Flexible">

Helt konkret, vil det betyde at man skal finde ud af hvilket af Cloudflares datacentre browseren kontakter og lytte med på linien bag ved dét. Før kunne man sidde på lokalnetværket og lytte til - eller værre endnu ændre på data, inden de nåede browseren. Så nu er man altså _langt_ bedre beskyttet mod målrettet overvågning / manipulation. Men man er altså _ikke_ beskyttet mod en modstander, med mulighed for at lytte på trafikken mellem Cloudflare og GitHubs servere. Men selv der, er et ikke trivielt at afgøre _hvem_ der læser siden, da det eneste man ser er at Cloudflare og GitHub taler sammen om siden her.

Derudover cacher Cloudflares infrastruktur siden og leverer den, hvis den kan, direkte fra sine egne servere og kontakter i dette tilfælde slet ikke GitHub. Og når det sker er _al_ trafikken altså krypteret. I tilfældet med siden her er der tale om en ret aggresiv caching, hvorfor lang de fleste forespørgsler aldrig kommer længere end Cloudflare.

Men er det så godt nok? Tja, det afhænger helt og holdent af hvad det ønskede niveau er. I dette tilfælde, ja. Siden her har ingen inputfelter, som besøgende kunne indtaste privat info i og gemmer ingen data om læserene. Så ræsonnementet for mig er, at det er godt nok i det ingen personføsomme oplysninger transmitteres.

Alternativet ville for mig være at flytte siden til en anden host, som tillader ssl-terminering på et selvvalgt domæne. Men det ville dels ødelægge min arbejdsgang, som afhænger af GitHub og formodentligt betyde at jeg så - igen - skulle til at vedligeholde en server; og så afhænger sikkerheden pludselig af mig personligt og ikke et stort firma med en masse at tabe. ;)
