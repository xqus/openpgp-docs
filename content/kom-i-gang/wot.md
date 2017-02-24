+++
date = "2017-02-22T10:59:58+01:00"
toc = true
next = "/kom-i-gang/fallgruver"
prev = "/kom-i-gang/kryptering"
weight = 7
title = "Tillitsnett"

+++

Hvordan kan man vite at en nøkkel virkelig tilhører den personen som den
tilsynelatende tilhører? Hvem som helst kan lage et nøkkelpar og skrive hvilket
navn og hvilken epostadresse de vil. Tillitsnettet (Web Of Trust) forsøker å
skape et nettverk av nøkler du stoler på slik at man lettere kan knytte et
nøkkelpar til en person.

Sertifisering
-------------

Sertifisering (eller signering) gjør man når man har verifisert sammenhengen
mellom nøkkel og person. Når man sertifiserer en nøkkel signerer du den med din
private nøkkel, slik at andre ser at du går god for denne nøkkelen.

Tillit
------

Når man snakker om tillit til en nøkkel mener man hvor mye man stoler på at
eieren til nøkkelen verifiserer at eieren til en nøkkel er den han/hun utgir seg
for å være. Dersom du har tillit til Bob sin nøkkel, og Bob har sertifisert
Alice sin nøkkel vil du automatisk også ha tillit til Alice sin nøkkel.


Nøkkelservere
-------------

Nøkkelservere benyttes for å laste ned eller oppdatere offentlige nøkler.
Det er svært viktig at du regelmessig oppdaterer de offentlige nøklene til de
du kommuniserer med. Dette er eneste måte å vite at nøkkelen for eksempel ikke
er tilbakekalt.
