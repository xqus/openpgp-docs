+++
title = "Digitale signaturer"
date =  2017-12-20T10:50:00+02:00
weight = 4
LastModifierDisplayName = "Audun Larsen"
LastModifierEmail = "audun@larsn.no"
+++

En sjekksum er en kort kode som brukes til å sjekke integriteten av data, eller
den matematiske funksjonen av dataene, algoritmen, som genererer koden,
ofte kalt hash-funksjon.

Et dokuments digitale signatur er resultatet av en hash-funksjon av dokumentet.
For å være nyttig må en hash-funksjon ha to viktige egenskaper. For det første
bør det være vanskelig å finne to dokumenter som resulterer i samme sjekksum. I
tillegg bør det være vanskelig å gjennopprette det originale dokumentet ut fra en
sjekksum.

Ved å bruke en slik hash-funksjon et dokument kan signeres ved å produsere en
sjekksum, og denne er signaturen. En annen person kan sjekke signaturen ved å
kjøre dokumentet gjennom samme hash-funksjon og sammenligne sin sjekksum med den
som kom som signatur. Dersom de er like, er det nesten helt sikkert at dokumentene
er identiske.

Problemet er å benytte en hahs-funksjon uten å tillate at en angiper interferer
med signatur-kontrollen. Hvis dokumentet og signaturen er sendt ukryptert, så kan
en angriper modifisere dokumentet og generere en ny signatur uten at mottaker
merker det. Dersom bare dokumentet er kryptert så kan en angriper endre på signaturen
og gjøre slik at kontrollen av signaturen feiler.

En algoritme som virker er å benytte en offentlig-nøkkel algoritme for å kryptere
signaturen. Faktisk så krypteres sjekksummen med den private nøkkelen til personen
som signerer, og hvem som helst kan kontrollere signaturen ved å benytte den offentlige
signaturen. Det signerte dokumentet kan sendes ved å benytte hvilken som helst
annen krypteringsalgoritme, eller det kan sendes ukryptert. Hvis dokumentet
modifiseres vil signaturkontrollen feile. *The Digital Signature Standard (DSA)*
er en offentlig-nøkkel algoritme som virker som akkurat beskrevet. DSA er en del
av OpenPGP standaren, men RSA kan også benyttes til digitale signaturer.
