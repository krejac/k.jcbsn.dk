---
layout: post
title: (DA) Turbo på Terminalen - ssh To My Mac
---

[TL;DR](http://en.wikipedia.org/wiki/Wikipedia:Too_long;_didn't_read) - Jeg har lavet et lille [script](), der tillader at man ssh'er tilbage til sin Mac uden at rode med routere, portforwarding ol. Alt det kræver er at Back To My Mac er aktiveret på begge maskiner.

<img src="{{ site.url }}/public/assets/20170322-icloud-icon-ssh.png" alt="iCloud+SSH" style="width: 200px;">

Nogle gange har jeg brug for at kunne forbinde til min hjemme-mac og har hidtil gjort det via 'screen sharing' via 'Back To My Mac'. Det virker egentligt også fint, men som oftest har jeg slet ikke brug for den grafiske brugergrænseflade som skærmdeling giver mig. Jeg har bare brug for en terminal-adgang. Derfor ville jeg faktisl helst ssh'e mig ind til min maskine. Men jeg gider ikke rigtig rode med 'port forwarding' og åbne (mere) op til mit hjemmenetværk i min router. Så jeg kom til at tænke på, om man mon ikke kunne udnytte Back To My Mac-forbindelsen til dette formål. Og jo, efter 10 sekunder på [duckduckgo](https://duckduckgo.com/?q=Remote+SSH+using+Back+To+My+Mac) fandt jeg [svaret](http://onethingwell.org/post/27835796928/remote-ssh-bact-to-my-mac). :)

Herefter skrev jeg mit eget lille script, som håndterer det tunge arbejde med at identificere iCloud-id'et og forbinde korrekt.

Kør det sådan her:

    ./sshtomymac.sh [navn-på-mac]

eller bare:

    ./sshtomymac.sh

---

Scriptet:

    :::bash
    #!/bin/bash

    ACCOUNT=$(echo "show Setup:/Network/BackToMyMac" | scutil | sed -n 's/.* : *\(.*\).$/\1/p')

    if [ ! -n "$1" ]; then
        echo "ssh to which Mac? "
        read MAC

        # Uncomment the following two lines if you need to login to the remote host with a different user than the current local user.
        #echo "As who? "
        #read USER

        if [[ USER ]]; then
            ssh $USER"@"$MAC"."$ACCOUNT
            else
            ssh $MAC"."$ACCOUNT
        fi
    else
        ssh $1"."$ACCOUNT
    fi
