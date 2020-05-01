---
layout: post
title: 'Server hardening' - Opsætning af firewall
---

[TL;DR](http://en.wikipedia.org/wiki/Wikipedia:Too_long;_didn't_read) - Jeg har et par servere snurrende rundt om i verdenen og ser derfor tydeligt, hvor ofte de bliver udsat for angreb. Her er mine noter til opsætning af en firewall Ubuntu/Debian-box[^1].

![Serving]({{ site.url }}/public/assets/20160126_server.jpg "Live to serve...")

En firewall er en effektiv måde at blokere ikke-ønsket trafik mod din server. På Ubuntu kan man selv rette i de relativt komplicerede [iptables](http://manpages.ubuntu.com/manpages/trusty/man8/iptables.8.html) eller installere UFW (Uncomplicated FireWall), ved at apt-get'e pakken ufw. ufw er en slags 'front end' til iptables og noget lettere at have med at gøre. Vi snupper den sidste her.

    sudo apt-get install ufw

Først garanteres trafik via ssh og http.

    sudo ufw allow ssh
    sudo ufw allow http

Derefter blokeres telnet specifikt og resten per default...

    sudo ufw deny 23
    sudo ufw default deny

Slå firewallen til.

    sudo ufw enable

Og endelig: Check status på firewallen.

    sudo ufw status verbose

*Bonus*: Som nævnt er ufw et administrationsmodul til iptables og man kan læse reglerne i ip-tables.

    sudo iptables -L

Det kan dog være lidt svært at gennemskue hvad der er sket, hvis ikke også man har kørt ovenstående før man lavede ændringerne og så sammenligner. ;)

---

*Posts om server hardening:*

- [Automatiske opdateringer](/2016/server-opdater.html)
- [Sikring af SSH](/2016/server-ssh.html)
- [Skærm af med en firewall](/2016/server-firewall.html)
- *Kommer*: [Login med private keys]()
- [Bloker uønsket trafik med fail2ban](/2016/server-fail2ban.html)
- *Kommer*: ???

[^1]: Herefter bare Ubuntu; men det meste vil også gælde på Debian.
