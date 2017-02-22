+++
date = "2017-02-22T10:59:58+01:00"
toc = true
next = "/kom-i-gang/konsepter/"
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

Før du starter
--------------
Dersom du vil benytte OpenPGP til kryptering og signering av epost anbefaler jeg
[Email Self Defense Guiden](https://emailselfdefense.fsf.org/en/) til Free
Software Foundation. Denne guider deg gjennom installasjon av GnuPG og Thunderbird
med Enigmail, og hjelper deg sende din første kryptere epost.

Innholdet videre i denne guiden forklarer OpenPGP konspter bruken av GnuPG fra
kommandolinjen. Bruk av kommandolinjeverktøy er ikke noe alle vil bruke i
hverdagen, men til tross for at du kanske vil benytte et grafisk grensesnitt
i for eksempel Thunderbird vil denne guiden være nyttig da den forklarer
grunnleggende prinsipper med OpenPGP.

Kom i gang
----------
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

Installere på Windows
---------------------
Last ned **Simple installer for GnuPG modern** og følg installeringsveiviseren.
Når den er ferdig skal du kunne kjøre `gpg` kommandoen fra kommandolinjen.
For å åpne kommandolinjen trykk `WIN+R` skriv inn `cmd` og trykk ENTER.

For å kontrollere at alt har gått som det skal kan du skrive: `gpg --version`
og trykke ENTER.
Det skal gi deg noe slikt som:


    C:\>gpg --version
    gpg (GnuPG) 2.1.17
    libgcrypt 1.7.5
    Copyright (C) 2016 Free Software Foundation, Inc.
    License GPLv3+: GNU GPL version 3 or later <https://gnu.org/licenses/gpl.html>
    This is free software: you are free to change and redistribute it.
    There is NO WARRANTY, to the extent permitted by law.

    Home: C:/Users/BRUKERNAVN/AppData/Roaming/gnupg
    Supported algorithms:
    Pubkey: RSA, ELG, DSA, ECDH, ECDSA, EDDSA
    Cipher: IDEA, 3DES, CAST5, BLOWFISH, AES, AES192, AES256, TWOFISH,
          CAMELLIA128, CAMELLIA192, CAMELLIA256
    Hash: SHA1, RIPEMD160, SHA256, SHA384, SHA512, SHA224
    Compression: Uncompressed, ZIP, ZLIB, BZIP2

Legg merke til ``Home: C:/Users/BRUKERNAVN/AppData/Roaming/gnupg``. Det er i
denne mappen konfigurasjonsfiler og nøkler lagres. Den kan være forskjellig
på din datamaskin.

Installere på Linux
-------------------
For å installere GnuPG søk etter GnuPG pakken i ditt pakkesystem. På Ubuntu for
eksempel installere det slik:


    apt-get install gnupg2
