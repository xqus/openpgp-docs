+++
date = "2017-02-22T10:59:58+01:00"
toc = true
next = "/kom-i-gang/kryptering"
prev = "/kom-i-gang/noekkelring"
weight = 6
title = "Signering"

+++

Et av kriteriene for sikker kommunikasjon er at man kan verifisere avsenderen
og samtidig verifisere at innholdet ikke har blitt endret på veien.
Digitale signaturer gir deg denne sikkerheten. En digital signatur kan brukes
på meldinger som skal sendes til mange mottakere, der kryptering ikke nødvendigvis
er et behov, eller ønskelig.

OpenPGP lar deg signere meldinger med din private nøkkel. Mottakeren kan verifisere
at du er avsenderen, og at meldingen ikke har blitt modifisert på veien ved å bruke
din offentlige nøkkel.

OpenPGP lar deg signere et dokument på tre forskjellige måter:

 * [Integrert signatur](#integrert-signatur)
 * [Klartekstsignatur](#klartekstsignatur)
 * [Frakoblet signatur](#frakoblet-signatur)

{{% notice tip %}}
Alle de tre signaturtypene har ulike fordeler og ulemper, men gir samme sikkerhet.
Bruk den signaturtypen som passer deg best i hvert tilfelle.
{{% /notice %}}  

### Integrert signatur
Dette er standardvalget for signering av dokumenter i GnuPG. Denne måten å signere
et dokument lager et nytt dokument som inneholder både din digitale signatur og det
originale dokumentet. Dokumentet er komprimert og i binært formart.

    amnesia@amnesia:~$ gpg2 --sign test.txt > test.sig

Dette produserer et signert dokument `test.txt.gpg`. Dokumentet inneholder både din
digitale signatur og det originale dokumentet `test.txt`.
Dokumentet er komprimert og i binært format.

For å kontrollere signaturen på et signert dokument, samt for å gjennopprette det
originale dokumentet bruker du `--decrypt` kommandoen (selv om dokumentet ikke er
kryptert).

    amnesia@amnesia:~$ gpg2 --output test.txt --decrypt test.txt.gpg
    gpg: Signature made Sat 25 Feb 2017 09:23:14 AM UTC
    gpg:                using RSA key 0x3E2A6E298A8C9B2C
    gpg: Good signature from "Alice <alice@example.com>" [ultimate]
    Primary key fingerprint: 52E9 0DB3 F32A E6B0 C7BD  C939 3E2A 6E29 8A8C 9B2C

Denne måten å signere dokumenter på er praktisk dersom du vet at mottakeren
benytter OpenPGP, men det er fork eksempel ikke mulig å åpne det originale
dokumentet uten å først verifisere signaturen.

### Klartekstsignatur
Et vanlig bruksområde for digitale signaturer er epost eller andre digitale
meldinger. I slike tilfeller er det ikke ønskelig å pakke inn meldingen i en
binær fil. Til slike tilfeller kan man benytte en klartekstsignatur.
En klartekstsignatur gjøres med `--clearsign` parameteren. Når man produserer en
klartekstsignatur, lages en ASCII signatur som omgir det originale dokumentet i
et nytt dokument `test.txt.asc`.

    amnesia@amnesia:~$ gpg2 --clearsign test.txt

    You need a passphrase to unlock the secret key for
    user: "Alice <alice@example.com>"
    2048-bit RSA key, ID 0x3E2A6E298A8C9B2C, created 2017-02-25

    amnesia@amnesia:~$ cat test.txt.asc
    -----BEGIN PGP SIGNED MESSAGE-----
    Hash: SHA512

    Hello World
    -----BEGIN PGP SIGNATURE-----

    iQEcBAEBCgAGBQJYsU+HAAoJED4qbimKjJsssYUH/1mxNBPGv9uTb8hqTXj3G207
    RmKwEhSeuaNUjH+E/rxNVSVBhWBMSuEFfXth1YkCvdi/oo9rDB4pZaqUSocQyg8t
    nRsg2EWEg6qM3iaknVqdSCoKvQ2M0FwrnpqdTcUShrrYXgIQVXA3E8/yh3Y2ZJH2
    Vibt5QHYXZor5s2RbMsnT9+KXpHqAFbHgMxmi554tpGfdqSwTJhJdk2yoTjV03Ps
    4wdu3OkCVhK+54IpVVzWrZZCZ9fWshcU/AWzBs4KWtsJeE4v5nUCCpKGFB6NGi6O
    1ZpDTPqUI1jWSi7AVluh/n1S79So41ArhuRJOa4dnw7yV1J7TsnNZnjYUpISN+4=
    =4vOI
    -----END PGP SIGNATURE-----

En slik signert melding kan enkelt sendes som epost, eller som en annen form for
melding. Selv om ikke alle mottakerene bruker OpenPGP kan de uansett lese innholdet
i meldingen.

En klartekstsignatur verifiseres på samme måte som en vanlig signatur, med `--decrypt`.

    amnesia@amnesia:~$ gpg2 --decrypt test.txt.asc
    Hello World
    gpg: Signature made Sat 25 Feb 2017 09:33:59 AM UTC
    gpg:                using RSA key 0x3E2A6E298A8C9B2C
    gpg: Good signature from "Alice <alice@example.com>" [ultimate]
    Primary key fingerprint: 52E9 0DB3 F32A E6B0 C7BD  C939 3E2A 6E29 8A8C 9B2C

### Frakoblet signatur
Begge de to måtene beskrevet over har begrenset nytteverdi, og begge metodene
gjør endringer i det originale dokumentet. Derfor finnes det en tredje metode
som lagrer signaturen i en separat fil, uten å gjøre endringer i det originale
dokumentet. Dette gjøres med `--detach-sign` parameteren.
Det kan være praktisk dersom du ønsker å distribuere for eksempel software som
er signert.

    amnesia@amnesia:~$ gpg2 --detach-sign test.txt

    You need a passphrase to unlock the secret key for
    user: "Alice <alice@example.com>"
    2048-bit RSA key, ID 0x3E2A6E298A8C9B2C, created 2017-02-25

Dette lager en signaturfil som har samme filnavn som det originale dokumentet
etterfulgt av `.sig`.

For å verfifisere signaturen trenger man både det originale dokumentet og
signaturfilen.

    amnesia@amnesia:~$ gpg2 --verify test.txt.sig test.txt
    gpg: Signature made Sat 25 Feb 2017 09:41:47 AM UTC
    gpg:                using RSA key 0x3E2A6E298A8C9B2C
    gpg: Good signature from "Alice <alice@example.com>" [ultimate]
    Primary key fingerprint: 52E9 0DB3 F32A E6B0 C7BD  C939 3E2A 6E29 8A8C 9B2C

Dersom man gjør endringer i det originale dokumentet vil signaturen bli ugyldig.

    amnesia@amnesia:~$ echo "Hello" >> test.txt
    amnesia@amnesia:~$ gpg2 --verify test.txt.sig test.txt
    gpg: Signature made Sat 25 Feb 2017 09:41:47 AM UTC
    gpg:                using RSA key 0x3E2A6E298A8C9B2C
    gpg: BAD signature from "Alice <alice@example.com>" [ultimate]
