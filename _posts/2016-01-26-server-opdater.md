---
layout: post
title: Server hardening - Automatiske opdateringer
---


[TL;DR](http://en.wikipedia.org/wiki/Wikipedia:Too_long;_didn't_read) - Jeg har et par servere snurrende rundt om i verdenen og ser derfor, hvor ofte de bliver udsat for angreb. Her er mine noter til at holde en Ubuntu/Debian-box[^1] opdateret - også når man ikke har tid.

![Serving]({{ site.url }}/public/assets/20160126_server.jpg "Live to serve...")

Første skridt i denne "server hardening for begyndere" er at opdatere serveren med de seneste pacthes. På Ubuntu, gøres dette nemmest med apt-get. Opdater først repositories og dernæst pakker.

    sudo apt-get update
    sudo apt-get upgrade -y

Herefter hentes programmet '[unattended-upgrades](https://help.ubuntu.com/lts/serverguide/automatic-updates.html)', som bruges til at konfigurere serveren til at selv at hente og applicere sikkerhedsopdateringer løbende og programmet startes.

    sudo apt-get install unattended-upgrades
    sudo dpkg-reconfigure -plow unattended-upgrades

Svar 'y', når du bliver spurgt om du automatisk vil downloade og installere opdateringer. Så er din server konfigureret til automatiske opdateringer.

Bemærk dog at serveren som standard ikke installerer pakker, der kræver genstart og du slipper derfor ikke helt for at skulle logge ind en gang i mellem. Dette kan selvfølgelig også [automatiseres](http://askubuntu.com/questions/614589/automatically-update-commands-for-ubuntu-server-system), men jeg vil generelt ikke anbefale at automatisere opgaver, der kræver genstart, da det især er der, man risikerer noget skal håndholdes. :)

---

*Posts om server hardening:*

- [Automatiske opdateringer](/2016/server-opdater.html)
- [Sikring af SSH](/2016/server-ssh.html)
- [Skærm af med en firewall](/2016/server-firewall.html)
- *Kommer*: [Login med private keys]()
- [Bloker uønsket trafik med fail2ban](/2016/server-fail2ban.html)
- *Kommer*: ???

[^1]: Herefter bare Ubuntu; men det meste vil også gælde på Debian.
