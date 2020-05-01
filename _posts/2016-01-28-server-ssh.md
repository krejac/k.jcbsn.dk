---
layout: post
title: 'Server hardening' - Sikring af SSH
---

[TL;DR](http://en.wikipedia.org/wiki/Wikipedia:Too_long;_didn't_read) - Jeg har et par servere snurrende rundt om i verdenen og ser derfor, hvor ofte de bliver udsat for angreb. Her er mine noter til at lukke ssh af for uvedkomne på en Ubuntu/Debian-box[^1].

![Serving]({{ site.url }}/public/assets/20160126_server.jpg "Live to serve...")

SSH er et vigtigt redskab til drift og administration af servere og kan sjældent helt undværes. Derfor har mange servere åben for SSH-adgang, og det er et af de første steder du bliver forsøgt hacket. Derfor er det også vigtigt at sikre adgangen hertil hurtigt.

Første skridt for at sikre din ssh-indgang er at forbyde at login med root. Brugere skal i stedet ssh'e ind med deres personlige bruger og su'e til root, hvis det er påkrævet - eller endnu bedre: bruge 'sudo'. Først laves en ny bruger ('mario' herunder er brugernavnet på den nye bruger).

    adduser mario

Giv mario sudo-rettigheder.

    gpasswd -a mario sudo

Åbn ssh-servicens konfigurationsfil.

    nano /etc/ssh/sshd_config

Find det parameter der hedder 'PermitRootLogin' og ændr det fra 'yes' til 'no' og gem filen med 'CTRL-X'. Endelig genstaters ssh-servicen, så den læser de nye indstillinger.

    service ssh restart

Inden man lukker forbindelsen til serveren, bør man lige teste brugeren med en ny ssh-session, for ikke at blive låst ude.

Man *kan* faktisk gå skridtet videre og begrænse adgangen til serveren til udelukkende at stamme fra kendte ip-adresser. I samme fil som ovenfor (/etc/ssh/sshd_config) sættes parametret 'ListenAddress' til den ip-adresse som man godt må logge ind fra - men pas på: ændrer din adresse sig, ryger ssh-adgangen til serveren...

---

*Posts om server hardening:*

- [Automatiske opdateringer](/2016/server-opdater.html)
- [Sikring af SSH](/2016/server-ssh.html)
- [Skærm af med en firewall](/2016/server-firewall.html)
- *Kommer*: [Login med private keys]()
- [Bloker uønsket trafik med fail2ban](/2016/server-fail2ban.html)
- *Kommer*: ???

[^1]: Herefter bare Ubuntu; men det meste vil også gælde på Debian.
