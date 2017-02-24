+++
date = "2017-02-22T10:59:58+01:00"
toc = true
next = "/kom-i-gang/fallgruver"
prev = "/kom-i-gang/kryptering"
weight = 7
title = "Tillitsnett"

+++

Før du sender en kryptert melding må du være sikker på at den offentlige
nøkkelen du bruker for å kryptere meldingen faktisk tilhører den personen du
skal sende meldingen til. Det at en nøkkel finnes på en nøkkelserver betyr ikke
at den faktisk tilhører personen du vil kommunisere med. Hvem som helst kan lage
et nøkkelpar og skrive hvilket navn og hvilken epostadresse de vil.
Tillitsnettet (Web Of Trust) forsøker å skape et nettverk av nøkler du stoler på
slik at man lettere kan knytte et nøkkelpar til en person.

### Sertifisering
Når du [sertifiserer en nøkkel](/openpgp-docs/kom-i-gang/noekkelring/#sertifisere-nøkler)
forteller du omverden at du har verifisert sammenhengen mellom *navn* og *epostadresse*
spesifisert i nøkkelen og den faktiske eieren av nøkkelen.

### Tillit
Når man snakker om tillit til en nøkkel mener man hvor mye man stoler på at
eieren til nøkkelen verifiserer at eieren til nøklene han/hun sertifiserer
er den han/hun utgir seg for å være.
Dersom du har tillit til Bob sin nøkkel, og Bob har sertifisert Alice sin nøkkel
vil du automatisk også ha tillit til Alice sin nøkkel.

### Nøkkelservere
Nøkkelservere benyttes for å laste ned eller oppdatere offentlige nøkler.
Det er svært viktig at du regelmessig oppdaterer de offentlige nøklene til de
du kommuniserer med. Dette er eneste måte å vite at nøkkelen for eksempel ikke
er tilbakekalt.
