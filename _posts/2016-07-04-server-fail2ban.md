---
layout: post
title: Server hardening - Bloker uønsket trafik med fail2ban
---

[TL;DR](http://en.wikipedia.org/wiki/Wikipedia:Too_long;_didn't_read) - Jeg har et par servere snurrende rundt om i verdenen og ser derfor tydeligt, hvor ofte de bliver udsat for angreb. Her er mine noter til opsætning af fail2ban på en Ubuntu/Debian-box[^1].

![Serving]({{ site.url }}/public/assets/20160126_server.jpg "Live to serve...")

Fail2ban er en service, som holde øje med din servers logfiler og ændrer firewallregler baseret på, hvad fail2ban tror er uvedkomne forsøg på at tilgå maskinen. Som sådan er det uhyre effektivt til at blokere for forsøg på at få adgang til serveren via 'brute force'.

Før vi begynder at installere noget som helst på en Linux-maskine (via distroens repositories ihvertfald), bør man opdatere kildefilerne, så man sikrer at man får de nyeste pakker ned. Dette gøres med:

    sudo apt-get update

Hvorefter man gan installere fail2ban med:

    sudo apt-get install fail2ban

Den primære konfigurationsfil for fail2ban er `/etc/fail2ban/jail.conf`, men hvis vi retter i den rissikerer vi at en fremtidig opdatering af fail2ban ødelægger vores konfiguration. Derfor kopieres filen til en lokal fil, som vi bruger i stedet. Dette gøres med:

    sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local

Og herefter kan den lokale fil redigeres, så den holder øje med nginx[^nginx]:

    sudo nano /etc/fail2ban/jail.local

Under direktivet `[nginx-http-auth]` sættes - ikke overraskende - `enabled = true`, for at aktivere den indbyggede nginx beskyttelse. Desværre har fail2ban ikke supermeget beskyttelse på nginx fronten og jeg foretrækker også at aktivere beskyttelse for ondsindet afvikling af scripts og onde robotter ved at indsætte nedenstående direktiver umiddelbart under `[nginx-http-auth]` direktivet:

    [nginx-noscript]

    enabled  = true
    port     = http,https
    filter   = nginx-noscript
    logpath  = /var/log/nginx/access.log
    maxretry = 6

    [nginx-badbots]

    enabled  = true
    port     = http,https
    filter   = nginx-badbots
    logpath  = /var/log/nginx/access.log
    maxretry = 2

I de direktiver vi lige har sat op, er der referencer til nogle filtre. Disse skal vi naturligvis også have sat op. Gem derfor `/etc/fail2ban/jail.local` og skift til kataloget med filtrene:

    cd /etc/fail2ban/filter.d

I første omgang skal vi lige ændre et enkelt parameter i filtret til den medfølgende `[nginx-http-auth]` direktiv. Rediger derfor filen `nginx-http-auth.conf` med:

    sudo nano nginx-http-auth.conf

Indsæt regex'en `^ \[error\] \d+#\d+: \*\d+ no user/password was provided for basic authentication, client: <HOST>, server: \S+, request: "\S+ \S+ HTTP/\d+\.\d+", host: "\S+"\s*$` under den anden, gem og luk.

Herefter stjæler vi apache-direktivets badbot-filter, da det er ganske glimrende som det står, således:

    sudo cp apache-badbots.conf nginx-badbots.conf

Og endelig laver vi et filter til vores `[nginx-noscript]` direktiv:

    sudo nano nginx-noscript.conf

Og klippe-klisterer nedenstående ind i den tomme fil:

    [Definition]

    failregex = ^<HOST> -.*GET.*(\.php|\.asp|\.exe|\.pl|\.cgi|\.scgi)

    ignoreregex =

Og gemmer. Det er i øvrigt helt lovligt at sætte yderligere filendelser ind, men pas på du ikke blokerer for noget du skal bruge...

Til sidst skal det hele naturligvis (gen-)startes for at den nye konfiguration læses og aktiveres:

    sudo service fail2ban restart

Og endelig - efter det hele er gjort - kan man tjekke status på fail2ban med:

    sudo fail2ban-client status

Gør man som mig, finder man så lige ud af at man havde glemt et eller andet undervejs og kan begynde fejlsøgningen. :)

*BONUS*: Vil man følge lidt med i hvad der bliver bannet, kan man bruge nedenstående kommandoer til at se, hvad der aktuelt er sat i skammekrogen.[^skammekrog]


    sudo fail2ban-client status nginx-http-auth
    sudo fail2ban-client status nginx-noscript
    sudo fail2ban-client status nginx-badbots
    sudo fail2ban-client status ssh


---

*Posts om server hardening:*

- [Automatiske opdateringer](/2016/server-opdater.html)
- [Sikring af SSH](/2016/server-ssh.html)
- [Skærm af med en firewall](/2016/server-firewall.html)
- *Kommer*: [Login med private keys]()
- [Bloker uønsket trafik med fail2ban](/2016/server-fail2ban.html)
- *Kommer*: ???

[^1]: Herefter bare Ubuntu; men det meste vil også gælde på Debian.
[^nginx]: Jeg bruger nginx, men hvis det er en anden service, der skal beskyttes, må du lige google den. SSH beskyttelse er sat op per default.
[^skammekrog]: Eller man kan sætte emailrapportering op. Men det må vente til en anden post.
