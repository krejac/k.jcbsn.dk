---
layout: post
title: (DA) Rundt i manegen med en telescammer
---

**[TL;DR](http://en.wikipedia.org/wiki/Wikipedia:Too_long;_didn't_read)** - Tele-scammere ringer jævnligt rundt til uforvarende for at franarre dem penge eller lignende. Jeg prøvede i dag, da +45 4266 9829[^1] igen ringede, at tage med på turen for at se hvordan de ville snyde mig.

![tele-scammeren]({{ site.url }}/public/assets/20171003_scam.jpg)

I dag havde jeg _endelig_ tid til at tale med den venlige indiske "Microsoft support"-dame, der med jævne mellemrum ringer og fortæller mig den er gal med min Windows-maskine[^2] - og den var tilsyneladende _helt_ gal for de kunne nemt påvise mange fejl.

<img class="screen" src="{{ site.url }}/public/assets/20171003_run-command-box.png" alt="cmd">

Først vil "supporteren" have mig til at åbne en kommandoprompt ([win]+r efterfulgt af "cmd" og et tryk på ok) og b-o-g-s-t-a-v-v-e-r-e-r mig igennem "assoc" så hun kunne læse min maskines "unikke identifikator" op.

<img class="screen" src="{{ site.url }}/public/assets/20171003_assoc-output.png" alt="assoc">

    .ZFSendToTarget=CLSID\{888DCA60-FC0A-11CF-8F0F-00C04FD7D062}

Jæs, jæs. Den passede[^3]. Så jeg blev sendt videre til 2. level support - meget professionelt.

Second level-supporteren, som var en mand, som bad mig åbne "event viewer" ([win]+r efterfulgt af "eventvwr" og et tryk på ok) og navigere frem til en laang list med "fejl"[^4]. Her havde jeg lidt travl med at billedsøge igennem nettet samtidigt med for at kunne virke som om det rent faktisk stod på min skærm, når han bad mig forklare hvad jeg så. Men min langsomme reaktion har sikkert bare bestyrket hans forventning om at her var en, som han kunne snyde.

<img class="screen" src="{{ site.url }}/public/assets/20171003_event-log.jpg" alt="event log">

Når jeg så ved selvsyn kunne konstatere (ved ovenstående screenshot, som jeg [fandt på nettet](https://www.google.com/search?sa=G&hl=en&q=windows+10+event+viewer&tbm=isch&tbs=simg:CAQSlQEJrJpkkE2vflwaiQELEKjU2AQaAggKDAsQsIynCBpiCmAIAxIoxh2GE8UdhxOYE8Md9weXE5wT5gfUP9M_1xT_1DP409uj7EP_1w2wj--Phowdjj_1Jviy90mzAUnZLTLwjLvEanRikQzheeOfMd8nqeUm7WRlFc1j7Lq-wZkUzZF1IAQMCxCOrv4IGgoKCAgBEgSb5eTlDA&ved=0ahUKEwiGhJDk8dTWAhUMmrQKHcJnD2MQwg4IIygA&biw=1356&bih=793) mens vi talte), at der er en masse fejl på min maskine, bad second level-supporteren mig om at navigere til www[.]support[.]me og logge ind. Men den side linker til et [fjernskrivebordsværktøj](https://en.wikipedia.org/wiki/LogMeIn), som man bliver bedt om at downloade og installere, hvorefter man giver dem fuld adgang til maskinen - _så her skal man altså stå af_.

Det var så også her jeg bekendte kulør og sagde at jeg desværre måtte indrømme, at jeg arbejdede med it til dagligt og blot havde trukket dem en tur rundt i manegen for at finde ud af hvordan det foregik og havde spildt deres tid.

Og jeg skal da SÅ ellers lige love for at jeg fik en sviner på et ellers meget sødt engelsk med indisk accent. "You fucking-fuck; you arshole; I'm gonna ..." \*klik\* Så lagde jeg på.

[^1]: Telefonnummer medtaget, så folk kan finde denne advarsel, hvis de søger på nummeret.
[^2]: Hvilket er spøjst fordi jeg bruger macOS.
[^3]: Fordi det naturligvis [_ikke_ er en "unik identifikator" for en given maskine](https://msdn.microsoft.com/en-us/library/windows/desktop/ms691424(v=vs.85).aspx).
[^4]: Som en alindelig bruger ikke bør bekymre sig om - de logs er primært til udviklere og / eller systemadministratorer.
