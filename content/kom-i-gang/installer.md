+++
prev = "/kom-i-gang/hva-er-openpgp"
weight = 2
title = "Installere GnuPG"
date = "2017-02-26T11:07:38+01:00"
toc = true
next = "/kom-i-gang/enigmail"

+++

[GnuPG](http://gnupg.org) er en komplett, **gratis** og **åpen kildekode** *implementasjon* av
OpenPGP standaren. GnuPG lar deg kryptere og signere dine data og meldinger.
Du kan i tillegg administrere dine private og andres offentlige nøkler.

GnuPG er et kommandolinje verktøy for enkel integrering mot andre applikasjoner.
Det finnes grafiske grensesnitt for GnuPG, som for eksempel Enigmail som beskrives
seinere i håndboken men de fleste eksempler som er beskrevet i håndboken viser
bruk av GnuPG fra kommandolinjen.

{{% notice info %}}
Konseptene og teorien bak er like både fra kommandolinjen og gjennom de forskjellige grafiske grensesnittene,
så det anbefales at du leser gjennom eksemplene selv om du bruker et grafisk grensesnitt.
{{% /notice %}}

#### Forskjellige versjoner
GnuPG kommer i tre versjoner.

 * **Stable.**
 Versjon 2.0. Den stabile versjonen av GnuGP. Støtter SSH autentisering
 og S/MIME.
 * **Modern.**
Versjon 2.1. Den mest moderne versjonen av GnuPG. Skal snart erstatte *stable*. Støtter ECC.
 * **Classic.**
 Versjon 1.4. Gammel arkitektur. Anbefales ikke med mindre operativsystemet ikke støtter *stable*.

I de aller fleste tilfeller anbefaler jeg *Stable*.

### Installere på Windows
De forskjellige installasjonsfilene for Windows er tilgjengelig **nederst** på
[nedlastingssiden](https://www.gnupg.org/download/index.html) til GnuPG.
Last ned **Simple installer for GnuPG modern** eller **Gpg4win** avhengig av
hvilken versjon du ønker.

#### Integritetskontroll
Før du installerer GnuPG må du kontrollere at ingen har modifisert programvaren
du skal installere. Siden du ikke har GnuPG fra før er det beste vi kan gjøre
å kontrollere sjekksummen til filen. Dette må vi gjøre fra kommandolinjen.
For å gjøre det enklere kan du kopiere filen du akkurat lastet ned til
`C:\Users\DITTBRUKERNAVN`

For å åpne kommandolinjen trykk `WIN+R` skriv inn `cmd` og trykk ENTER.
Skriv inn følgende kommando, men bytt `filnavn.exe` med filnavnet til filen
du akkurat lastet ned.

    certUtil -hashfile filnavn.exe sha1

Dersom du lastet ned *Gpg4win* sammenligner du resultet med sjekksummen for filen
du lastet ned med [denne](https://www.gpg4win.org/download.html)
listen, lastet du ned *GnuPG modern* bruker du
[denne](https://www.gnupg.org/download/integrity_check.html) listen.

#### Start installasjonsveiviseren
For å installere OpenPGP dobbeltklikker du på filen du lastet ned. Dette starter
installasjonsveiviseren.

Når den er ferdig skal du kunne kjøre `gpg` kommandoen fra kommandolinjen.

{{% notice tip %}}
Eksemplene i denne håndboken er tatt fra et Linux operativsystem.
Alle eksemplene virker på Windows også, men må du erstatte `gpg2` i eksemplene
med `gpg` dersom du bruker Windows.
{{% /notice %}}

For å kontrollere at alt har gått som det skal, kan du skrive følgende i kommandolinjen:
`gpg --version` og trykke ENTER. For å åpne kommandolinjen trykker du `WIN+R`, skriv inn `cmd` og trykk ENTER.
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

Legg merke til Home: `C:/Users/BRUKERNAVN/AppData/Roaming/gnupg`. Det er i
denne mappen konfigurasjonsfiler og nøkler lagres. Den kan være forskjellig
på din datamaskin. Vi kommer tilbake til denne mappen seinere i håndboken så det
kan være greit å legge merke til denne.

### Installere på Linux
For å installere GnuPG *stable* søk etter GnuPG pakken i ditt pakkesystem.
På Ubuntu for eksempel installeres det slik:

    apt-get install gnupg2

GnuPG *classic* kommer som regel forhåndsinstallert, men kan eksistere sammen
med GnuPG *stable*. GnuPG *stable* er tilgangelig som `gpg2` fra terminalen.
Jeg anbefaler ikke å bruke GnuPG *classic* selv om det er forhåndsinstallert på
ditt system.

For å verifisere at GnuPG er installert som det skal kan du kjøre `gpg2 --version`.

    amnesia@amnesia:~$ gpg2 --version
    gpg (GnuPG) 2.0.26
    libgcrypt 1.6.3
    Copyright (C) 2013 Free Software Foundation, Inc.
    License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
    This is free software: you are free to change and redistribute it.
    There is NO WARRANTY, to the extent permitted by law.

    Home: ~/.gnupg
    Supported algorithms:
    Pubkey: RSA, RSA, RSA, ELG, DSA
    Cipher: IDEA, 3DES, CAST5, BLOWFISH, AES, AES192, AES256, TWOFISH,
            CAMELLIA128, CAMELLIA192, CAMELLIA256
    Hash: MD5, SHA1, RIPEMD160, SHA256, SHA384, SHA512, SHA224
    Compression: Uncompressed, ZIP, ZLIB, BZIP2
