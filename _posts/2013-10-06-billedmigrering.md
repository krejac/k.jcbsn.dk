---
layout: post
title: (DA) Migrering af billeder
---

![find + sed]({{ site.url }}/public/assets/20131006_migrering.png)

For at lette arbejdsgangen for publicering af posts her på loggen, har jeg i dag flyttet alle billeder fra at ligge i en mediefolder under "www/" til sit helt eget subdomæne. Det tog ca. 10 minutter fra start til slut; for da alle posts er skrevet i ren tekst (og formateret med [Markdown](http://daringfireball.net/projects/markdown/)) kunne jeg nemlig bare fyre nedenstående af via terminalen.

    find . -name "*.md" -exec sed -i '' "s/\/media\//http\:\/\/static\.logiskhave\.dk\//g" '{}' \;

Det substituerer alle referencer til "{{ site.url }}/public/assets/" med referencer til "{{ site.url }}/public/assets/" i *alle* mine posts. Herefter var det bare at uploade billederne til static.logiskhave.dk. Simpelt og nemt fordi det hele ligger som flade filer.

Det betyder så, at jeg nu slipper for at flytte alle de tunge mediefiler hver gang jeg laver en ny post. Dejligt!
