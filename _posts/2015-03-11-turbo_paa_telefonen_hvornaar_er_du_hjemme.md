---
layout: post
title: Turbo på telefonen - "hvornår er du hjemme?"
---

[TL;DR](http://en.wikipedia.org/wiki/Wikipedia:Too_long;_didn't_read) - Jeg har lavet en arbejdsgang, så jeg hurtigt kan svare min kone på hvornår jeg er hjemme ved hjælp af [Launch Center Pro](http://contrast.co/launch-center-pro/) og især [Pythonista](http://omz-software.com/pythonista/index.html).

![iPhone]({{ site.url }}/public/assets/20150311_iphone5s.jpg "iPhone")

Hver dag på vej hjem i toget spørger min bedre halvdel mig om hvornår jeg mon er hjemme. Og hver dag skal jeg kigge på oversigten, tælle stationerne, regne en ca. tid ud og skrive en SMS. Men ikke mere. For nu har jeg lavet et lille pythonscript, som ved hjælp af Pythonistas `location` metode finder mine aktuelle GPS-koordinater og sammenholder dem med S-togsstationernes ditto, finder den nærmeste station og ud fra det danner en sms med nærmeste station og forventet rejsetid (antallet af stationer * 2 minutter + 10 minutters cykeltid). Meget simpel idé, men det gav mig da lidt hovedbrud undervejs.[^1]

Resultatet er en proces, hvor jeg 1) vælger en handling fra appen [Launch Center Pro](http://contrast.co/launch-center-pro/), som 2) trigger et pythonscript i [Pythonista](http://omz-software.com/pythonista/index.html) og 3) returnerer til Launch Center Pro, med en færdig SMS.

![Arbejdsgang]({{ site.url }}/public/assets/20150311_workflow.jpg "Handling, script, SMS")

Triggeren i Launch Center Pro ser således ud:

    pythonista://home_in.py?action=run

Python koden (som nok er meget lidt elegant) kan ses her:

    :::python
    #!/usr/bin/env python
    # -*- coding: utf-8 -*-

    import location, time, webbrowser
    import math

    # Getting my coordinates and storing them in the variable 'me'
    location.start_updates()
    time.sleep(2)
    loc = location.get_location()
    location.stop_updates()
    me = [loc['latitude'], loc['longitude']]

    # Stations [longitude, latitude, url encoded stationname]
    skovlunde = [55.723190, 12.400950, 'Skovlunde%20st.']
    herlev = [55.718919, 12.443674, 'Herlev%20st.']
    husum = [55.7117845, 12.4530939, 'Husum%20st.']
    islev = [55.6978563, 12.4683289, 'Islev%20st.']
    jyllingevej = [55.6879452, 12.4735431, 'Jyllingevej%20st.']
    vanlose = [55.6879452, 12.4735431, 'Vanl%C3%B8se%20st.']
    flintholm = [55.685284, 12.4871472, 'Flintholm%20st.']
    peter_bangs_vej = [55.6775657, 12.4975328, 'Peter%20Bangs%20Vej%20st.']
    langgade = [55.6588926, 12.5074033, 'Langgade%20st.']
    valby = [55.660563, 12.5163726, 'Valby%20st.']
    enghave = [55.660563, 12.5163726, 'Enghave%20st.']
    dybbolsbro = [55.6602483, 12.5567988, 'Dybb%C3%B8lsbro%20st.']
    kobenhavn_h = [55.6683331, 12.5670127, 'Hovedbaneg%C3%A5rden%20st.']
    vesterport = [55.6757871, 12.5709609, 'Vesterport%20st.']
    norreport = [55.6810076, 12.5748877, 'N%C3%B8rreport%20st.']

    # Defining the part of the C line I use on my way home from work
    c_line = [skovlunde, herlev, husum, islev, jyllingevej, vanlose, flintholm, peter_bangs_vej, langgade, valby, enghave, dybbolsbro, kobenhavn_h, vesterport, norreport]

    list_of_distances = []

    # GPS coordinate pair math
    def distance_from(my_coordinates, station):
    distance = math.hypot(station[0]-my_coordinates[0], station[1]-my_coordinates[1])
    return distance

    # Generating a list of distances from which the shortest is found
    for station in c_line:
    list_of_distances.append(distance_from(me, station))

    # Variables used in the url derived from list_of_distances
    station = c_line[list_of_distances.index(min(list_of_distances))][2]
    minutes = str(c_line.index(c_line[list_of_distances.index(min(list_of_distances))]) *2+10)

    # Concatenating url elements and calling the url using Launch Center Pros url-scheme
    sms_url = 'launch://messaging?to=%2B4529725044&body=' + 'Er%20ved%20' + station +  '%20er%20hjemme%20om%20ca.%20' + minutes + '%20minutter...'
    webbrowser.open(sms_url)

I første omgang ville jeg egentligt have brugt et eller andet kort-api. Det havde nok været mere elegant. Men dels så gad jeg ikke rette til, hvis de laver noget om, dels vil det tage længere tid at slå op i et api end selv at beregne og dels er det her bare nemmere. :)

[^1]: Dog nok ikke der hvor man forestiller sig, for logikken var relativt nem. Det største problem opstod nemlig som en formateringsfejl på et '&', da jeg kopierede koden fra min computer til min telefon. Men her var [@launchcenterpro](https://twitter.com/LaunchCenterPro) hurtige med svar på twitter.
