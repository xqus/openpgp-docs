+++
date = "2017-02-22T10:59:58+01:00"
toc = true
next = "/kom-i-gang/installer/"
prev = "/kom-i-gang/"
weight = 1
title = "Hva er OpenPGP"

+++

OpenPGP er en standard som definerer formater for kryptering og signering av
digitale meldinger og filer. OpenPGP benyttes i stor grad til kryptering av
epost og kan installeres som et tilegg til flere epostklienter.

OpenPGP benytter en krypteringsmetode som gjør at de partene som skal
kommunisere ikke trenger å avtale krypteringnøkkel på forhånd. I steden benyttes
mottakers offentlige nøkkel til å kryptere data med. Denne kan da bare
dekrypteres dersom man ha den tilhørende private nøkkelen.

Signering fungerer på motsatt måte. Avsender signerer med sin private nøkkel.
Denne signaturen kan så valideres med den offentlige nøkkelen.

### Før du starter
Dersom du vil benytte OpenPGP til kryptering og signering av epost anbefaler jeg
[Email Self Defense Guiden](https://emailselfdefense.fsf.org/en/) til Free
Software Foundation. Denne guider deg gjennom installasjon av GnuPG og Thunderbird
med Enigmail, og hjelper deg sende din første kryptere epost. Det finnes også
en [enklere versjon](/openpgp-docs/kom-i-gang/enigmail) av denne guiden i denne håndboken.

Innholdet videre i denne guiden forklarer OpenPGP konspter bruken av GnuPG fra
kommandolinjen. Bruk av kommandolinjeverktøy er ikke noe alle vil bruke i
hverdagen, men til tross for at du kanske vil benytte et grafisk grensesnitt
i for eksempel Thunderbird vil denne guiden være nyttig da den forklarer
grunnleggende prinsipper med OpenPGP.

### Kom i gang
For å komme i gang med OpenPGP trenger du først og fremst selve OpenPGP
programvaren. Det finnes et par alternativer men vi skal installere den
vanligste *Gnu Privacy Guard*, forkortet GnuPG eller GPG.

GnuPG finnes til de vanligste operativsystem og kan lastes ned fra [GnuPG](http://www.gnupg.org) sine
hjemmesider.

GnuPG er et kommandolinjeverktøy. Det betyr at det i utgangspunktet ikke finnes
noe grafisk grensesnitt og at det kjøres fra kommandolinjen. Det finnes
heldigvis grafiske grensesnitt til en del epostklienter slik at bruken av GnuPG
ikke kompliserer bruken av epost. For å gjøre det enklest mulig anbefaler jeg at
du bruker Thunderbird med Enigmail til epost.

I neste kapittel beskriver jeg hvordan du [installerer GnuPG](/openpgp-docs/kom-i-gang/installer/)
og deretter beskrives installasjon av [Thunderbird og Enigmail](/openpgp-docs/kom-i-gang/enigmail/).
