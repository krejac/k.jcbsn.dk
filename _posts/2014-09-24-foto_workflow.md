---
layout: post
title: Foto backup workflow
---

**[TL;DR](http://en.wikipedia.org/wiki/Wikipedia:Too_long;_didn't_read)** -- Jeg har konstrueret et automatisk workflow, som sikrer husstandens mange billeder og videoer taget med iPhones - samtidigt med, at de ikke behøver fylde på telefonen.

![iPhone i jord]({{ site.url }}/public/assets/20140912_iphone-i-jord@2x.jpg)

Jeg har længe eksperimenteret med - og betalt til - diverse billedbackuptjenester, som kunne frigøre plads på vores iPhones, fandt egentligt en god en som desværre gik rabundus. Så nu har jeg bygget mit eget ret robuste og relativt simple setup, som sikrer vores billeder, selvom iPhones'ne ryger ud af lommen i haven eller vores Macs diske dør. Det giver en vis tryghed at vide, at vores højt skattede billeder er sikre i skyen.

De *ingredienser* der skal bruges i opskriften er:   
- En eller flere smartphones[^0] med kamera og Dropbox-app'en installeret.   
- Et stk. gratisversion af [Dropbox](https://www.dropbox.com).[^1]       
- Et lile skvæt af [Noodlesofts Hazel](http://www.noodlesoft.com/hazel.php).[^2]       
- Én Mac, som får lov at stå tændt rimeligt ofte.   
- Én portion [Backblaze](https://secure.backblaze.com/r/00sexu).[^3]   


### Fremgangsmåde ###
Et billede tages med **telefonen**, uploades med **Dropbox**-app'en, sorteres på **Mac**'en med **Hazel** til en folder, som **Backblaze** tager backup af. Såre simpelt.

Det første trin i workflowet er at aktivere fotoupload i Dropdox-app'en[^4]. Åbn Dropbox app'en gå til Indstillinger og slå både "Kameraoverførsel" og "Upload i baggrunden" til.

![Dropbox' Camera Upload]({{ site.url }}/public/assets/20140908_camera-upload.png)

Dette aktiverer Dropbox' upload funktion og sørger for, at alle dine billeder bliver uploadet til kataloget "Camera Uploads" i roden af din Dropbox mappe.[^5]

Herefter skal du over på din Mac. På Mac'en åbnes Hazel fra "Instillinger" og mappen "Camera Uploads" tilføjes til i dine overvågende mapper. I den mappe skal der køre to regler; én til billeder og én til videoer.

*Billedsorteringsreglen*    

[![Hazel billedsorteringsregel]({{ site.url }}/public/assets/20140908_image-sort.png)]({{ site.url }}/public/assets/20140908_image-sort.png)

>If ```[all]``` of the following conditions are met    
>```[Kind]``` ```[is]``` ```[Image]```    
>```[Kind]``` ```[is not]``` ```[Folder]```    
>```[Extension]``` ```[is not]``` ```[png]``` (valgfri; frasorterer screenshots fra iPhone)    

>Do the following to the matched file or folder:    
>```[Move]``` to folder: ```[STI TIL MAPPE UDEN FOR DROPBOX]```    
>```[Sort into subfolder]``` with pattern: ```[date created]```    

Når man så vælger "date created", trykker man på <i class="fa fa-caret-down"></i> og vælger "Edit Date Pattern...". Alt efter hvordan man vil have sorteret sine billeder vælger man så om de skal opdeles i foldere for hver dag, måned eller år. Jeg har valgt måned, hvorfor mit datoformat ser således ud: ```[1999]```-```[12]```.

*Videosorteringsreglen*   

[![Hazel videosorteringsregel]({{ site.url }}/public/assets/20140908_video-sort.png)]({{ site.url }}/public/assets/20140908_video-sort.png)

>If ```[all]``` of the following conditions are met    
>```[Kind]``` ```[is]``` ```[Movie]```    
>```[Kind]``` ```[is not]``` ```[Folder]```    

>Do the following to the matched file or folder:    
>```[Move]``` to folder: ```[STI TIL MAPPE UDEN FOR DROPBOX]```   
>```[Sort into subfolder]``` with pattern: ```[date created]```    

Her følger "date created" samme form som for billedsorteringsreglen.

Og det var så Hazel-delen. Når du tager et billede med din iPhone, vil Dropbox appen opdage det og smide billedet i Dropbox. Herefter tager Hazel og sorterer billederne ud i din valgte folderstruktur og du kan derfor roligt slette dine billeder fra iPhone. [^6]

*Jeg* slutter så det hele af med at tage backup af folderen med alle mine billeder med Backblaze - og vil på *det kraftigste* anbefale dig at gøre det samme fordi [HARDDISKE DØR](http://log.logiskhave.dk/2014/0908_back-nu-op-mand.html)!

[^0]: Der behøver ikke partout være tale om iPhones; andre telefoner med en Dropbox app, der kan uploade billeder automatisk vil virke.
[^1]: Betalingsversionen kan også bruges, men giver ikke bedre resultater til dette formål.
[^2]: Hazel er min Macs mest brugte, aldrig åbnede, app.
[^3]: Køber du via dette link, for både du og jeg en gratis måned.
[^4]: Det første trin er vel egentligt at oprette en Dropbox-konto og downloade deres app på hhv. Mac og iPhone, men det går altså ud over denne gennemgang.
[^5]: Hvis du ikke ønsker at uploade alle dine billeder til Dropbox - hvis du som mig tager billeder på arbejdet eller lignende - kan du løse dette ved at installere en anden foto app til den slags billeder. Jeg bruger selv Camera+, som er en ganske god foto app (bedre end Apples egen).
[^6]: Men inden du går i gang med at slette derudaf, så tjek lige at Dropbox-app'en ER færdig, ikke?
