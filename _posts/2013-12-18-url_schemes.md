---
layout: post
title: (DA) URL Schemes
---

**tl**;**dr** - Jeg roder for tiden med [x-callback-urls](http://x-callback-url.com) og [URL skemaer](https://developer.apple.com/library/ios/featuredarticles/iPhoneURLScheme_Reference/Introduction/Introduction.html) på mine iOS enheder og har her skrevet en kort gennemgang af hvad dét er for noget og hvad det kan bruges til.

![Actions]({{ site.url }}/public/assets/20131218_x-callback-url.png)

### Hvad er URL Schemes?
URL Schemes, eller URL skemaer på dansk, er en metode til at lave inter-app kald på iOS enheder. Det vil groft sige, at man kan kalde en app, der har et URL skema, fra en anden app. Det er i sig selv smart nok, da man på denne måde kan spare et par tastetryk, når man skifter fra en app til en anden. Men der hvor det bliver rigtig smart er, når man sender data og instruktioner, i form af en tekststreng, med. URL'en skal være på en form, som den modtagende app forstår - altså følge app'ens URL skema - og kan så udføre en prædefineret handling på noget prædefineret data[^1].

Et eksempel på et x-callback-url kald, som den type URL'er, der anvendes her hedder kunne være dette, som virker i app'en Clean Links.

     clean-links://x-callback-url/clean?url=[clipboard]

Denne x-callback-url kalder Clean Links app'en og beder den rense[^2] det link, man har liggende i clipboard'et og kopierer det rensede link til clipboard, så eks. linket fra Youtubes mobilside her:

    http://m.youtube.com/watch?v=dQw4w9WgXcQ

Ville blive til:

     http://www.youtube.com/watch?v=dQw4w9WgXcQ

Hvilket jeg indrømmer er et lidt sjovt eksempel, da det rigtige link faktisk er længere end mobilsidens, men ikke desto mindre peger på den rigtige side - uden redirects ol.

### Hvad bruger jeg så URL Schemes til?

Ovenstående eksempel er selvfølgelig ikke helt grebet ud af den blå luft, for det er faktisk en del af en handling, som jeg har defineret på min telefon og som jeg bruger ret ofte[^3]. Jeg læser nemlig en del artikler på min mobil og bliver der ofte præsenteret for en mobiludgave eller en URL med en masse - for mig - overflødig information i. Jeg vil derfor gerne have renset mine URL'er, så de er mere retvisende inden jeg gemmer dem. Det gør jeg med følgende x-callback-url:

     clean-links://x-callback-url/clean?url=[clipboard]&x-success=\{\{pinswift://add?url=<URL>\}\}

Den krabat kalder jeg så fra en app, der kan eksekvere den slags hjemmelavede URL'er; nemlig [Launch Center Pro](http://contrast.co/launch-center-pro/).

Så det eneste jeg skal gøre nu er, at åbne Launch Center og vælge den definerede handling, så får jeg renset linket (via Clean Links) og bogmærket det rette link til min bogmærketjeneste, [Pinboard](https://pinboard.in/) (via [Pinswift](http://pinswiftapp.com/index.html)).  Nemt og hurtigt.

[^1]: Data sendes i form af ren tekst, så det er ikke muligt at sende filer mellem apps. Man bryder med andre ord ikke Apples sandboxing.

[^2]: Rense i den forstand at Clean Links finder det tilsvarende link på den rigtige, ikke-mobil

[^3]: Jeg har andre handlinger også, men de er lidt mere komplicerede...
