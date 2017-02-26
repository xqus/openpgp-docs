+++
prev = "/kom-i-gang/hva-er-openpgp"
weight = 2
title = "Installere GnuPG"
date = "2017-02-26T11:07:38+01:00"
toc = true
next = "/kom-i-gang/enigmail"

+++

### Installere på Windows
Last ned **Simple installer for GnuPG modern** og følg installeringsveiviseren.
Når den er ferdig skal du kunne kjøre `gpg` kommandoen fra kommandolinjen.
For å åpne kommandolinjen trykk `WIN+R` skriv inn `cmd` og trykk ENTER.

{{% notice tip %}}
Eksemplene i denne håndboken er tatt fra et Linux operativsystem.
Alle eksemplene virker på Windows også, men må du erstatte `gpg2` i eksemplene
med `gpg` dersom du bruker Windows.
{{% /notice %}}

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
