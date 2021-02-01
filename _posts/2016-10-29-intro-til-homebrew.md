---
layout: post
title: Intro til Homebrew
---

**[TL;DR](http://en.wikipedia.org/wiki/Wikipedia:Too_long;_didn't_read)** -- en appetitvækker til Homebrew for folk, der ikke _nødvendigvis_ er hjemmevante i [Terminal](https://web.archive.org/web/20130510222144/http://www.apple.com/osx/apps/all.html#terminal), men som omvendt heller ikke er bange for at fyre et par kommandoer af i ny og næ. Programmerne der bliver brugt er [Homebrew](http://brew.sh), [Caskroom](https://caskroom.github.io) og [mas-cli](https://github.com/mas-cli/mas).

![mas-cli logo]({{ site.url }}/public/assets/20161029_mas-cli.png)
<!--more-->

'brew'
======
[Homebrew](http://brew.sh) er kernen i vores setup og er et værktøj til at at installere andre værktøjer med. Nogen vil genkende lignende systemer fra Linux (eks. [apt](https://wiki.debian.org/Apt), [yum](http://yum.baseurl.org) eller [pacman](https://wiki.archlinux.org/index.php/pacman)). For at komme i gang med brew, skal man et smut forbi deres [hjemmeside](http://brew.sh) hvor de fortæller os hvad vi skal gøre for at installere. For nuværende er den nemmeste metode til at installere, at køre følgende kommando I terminalen:

    '/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"'

Det der sker, når man afvikler den kommando er at den downloader installationsprogrammet og kører det i terminalen med det samme. Når brew er installeret er man klar til at installere yderligere termialprogrammer.

### Installering, søgning og opdatering af programmer

Installer med `brew install app-navn`. Eks. `brew install youtube-dl`[^1].

Søg i alle de programmer du kan installere med `brew search del-af-app-navn`. Eks. `brew search youtu`, som bl.a. vil finde youtube-dl.

Opdater med `brew upgrade app-navn`. Eks. `brew upgrade youtube-dl`. Opdater alle programmer installeret med brew med `brew upgrade`.

### Husholdning

Med Homebrew følger dog en lille smule "husholdning", for ligesom værktøjerne fra Linux, skal selve pakkehåndteringssystemet vedligeholdes. Og med Homebrew gøres dette nemmest med `brew update; brew cleanup`, som først opdaterer brew og dernæst renser ud i cache ol.

--------

'cask'
======
[Caskroom](https://caskroom.github.io) er en udvidelse til Homebrew, hvorfra man kan hente og installer over 3000 af de apps, du normalt skal ud på en internettet for at finde.For at komme i gang med caskroom, skal man køre følgende cask-kommando:

    'brew tap caskroom/cask'

Dette åbner ret beset bare op for et ekstra repositorie man kan hente apps fra (caskroom). Når der er åbnet for cask's tap[^2] er man klar til at installere løs.

### Installering, søgning og opdatering af programmer

Installer med `brew cask install app-navn`. Eks. `brew cask install wireshark`.

Søg blandt casks med `brew cask search del-af-app-navn`. Eks. `brew cask search wireshark`.

Apps installeret med Caskroom bruger typisk den opdateringsfunktion, der er indbygget i den enkelt app. Har app'en ikke en opdateringsfunktion selv, kan man afinstallere og efterfølgende installere en ny version fra Caskroom. Eks. `brew cask uninstall --force wireshark && brew cask install wireshark`.

--------

'mas'
====
[Mas-cli](https://github.com/mas-cli/mas)[^3] er tredje og sidste ben i vores mål om terminal-app-installerings-nirvana. Mas-cli fjerner nemlig behovet for at åbne Mac App Store for at installere og opdatere dine apps derfra. Desværre skal du have hentet programmet tidligere[^4], men det behøver du trods alt kun gøre een gang.

### Installering, søgning og opdatering af programmer

Installering og opdatering med mas er lidt mere omstændigt, derfor er rækkefølgen også lidt omvendt her. Tricket er nemlig at man bruger et unikt tal til at installere med - og det tal stammer fra en søgning. Derfor søger man typisk først efter en app, kopierer tallet ud for app'en man vil installere og der efter installerer. Så derfor:

Søg i _hele_ Mac App Store med `mas search del-af-app-navn`. Eks. `mas search Number`. Noter herfra tallet.

Installer med `mas install tal-fra-før`. Eks. `mas install 409203825` (for at installere Numbers).

Opdater en enkelt app med `mas upgrade 409203825` og opdater alle med `mas upgrade`. (Pro tip: Se alle apps, med updates klar, med `mas outdated`.)

--------

Bonus
=====
Selvom vi med ovenstående kan installere programmer til kommandolinien, fra internettet og fra Mac App Store, slipper vi endnu ikke helt for grafiske installere. Opdatering af macOS kan nemlig ikke ske via ovenstående. Men det er der heldigvis råd for, for der kommer Apple os rent faktisk til undsætning. Så med nedenstående kommando, kan du også køre en opdatering af macOS fra terminalen med `sudo softwareupdate -i -a`.

Så med den lille krølle, kan man lave en fuld softwareopdatering med blot én linie i terminalen:

    sudo softwareupdate -i -a; brew update; brew upgrade; brew cleanup; mas upgrade

God fornøjelse! :)

[^1]: youtube-dl er et program til at downloade videoer fra YouTube, hvis man bare har url'en. Ret praktisk.
[^2]: 'Brew' betyder bryg og en 'tap' er en hane eller en kilde om man vil.
[^3]: Kort for "Mac App Store - Command Line Interface".
[^4]: Ikke nødvendigvis på samme computer - programmet skal bare figurere i listen over tidligere køb i Mac App Store.
