+++
date = "2017-02-22T10:59:58+01:00"
toc = true
next = "/kom-i-gang/kryptering"
prev = "/kom-i-gang/noekkelring"
weight = 6
title = "Signering"

+++

Man kan signere meldinger med OpenPGP for å verifisere at eieren av et bestemt
nøkkelpar har skrevet meldingen, og at ingen har modifisert den på veien.

For å verifisere signaturen bruker man den offentlige nøkkelen tilhørende
nøkkelparet.

OpenPGP pakker normalt sett signatur og filen man signerer inn i en og samme fil.

    C:\>gpg -output doc.sig --sign doc.txt

Dette produserer et signert dokument `doc.sig`. Dokumentet inneholder både din
digitale signatur og det originale dokumentet. Dokumentet er komprimert og i
binært format.

Hvis du mottar et signert dokument kan du kontrollere signaturen samtidig som
du gjennoppretter det originale dokumentet.

    C:\>gpg --output doc.txt --decrypt doc.sig

  gpg: Signature made Sun Jan 1 12:02:38 2017 CDT using RSA key ID AB4T76AC
  gpg: Good signature from "Alice (Judge) <alice@cyb.org>"

Klartekstsignatur
-----------------

Et vanlig bruksområde for digitale signaturer er epost eller andre digitale
meldinger. I tilfeller der det ikker er ønskelig å komprimere meldingen og pakke
den inn i en binær fil kan man bruke klartekstsignaturer.

En klartekstsignatur gjøres med `--clearsign` parameteren som produserer en
ASCII signatur som omgir det originale dokumentet.

    C:\>gpg --clearsign doc.txt

    You need a passphrase to unlock the secret key for
    user: "Alice (Judge) <alice@cyb.org>"
    2048-bit RSA key, ID AB4T76AC, created 2016-06-04

    -----BEGIN PGP SIGNED MESSAGE-----
    Hash: SHA2

    [...]
    -----BEGIN PGP SIGNATURE-----
    iEYEARECAAYFAjdYCQoACgkQJ9S6ULt1dqz6IwCfQ7wP6i/i8HhbcOSKF4ELyQB1
    oCoAoOuqpRqEzr4kOkQqHRLE/b8/Rw2k
    =y6kj
    -----END PGP SIGNATURE-----

Frakoblet signatur
------------------

Begge de to måtene beskrevet over har begrenset nytteverdi, og begge metodene
gjør endringer i det originale dokumentet. Derfor finnes det en tredje metode
som lagrer signaturen i en separat fil, uten å gjøre endringer i det originale
dokumentet. Dette gjøres med `--detach-sig` parameteren.

    C:\>gpg --output doc.sig --detach-sig doc.txt

    You need a passphrase to unlock the secret key for
    user: "Alice (Judge) <alice@cyb.org>"
    2048-bit RSA key, ID AB4T76AC, created 2016-06-04

    Enter passphrase:

For å verfifisere signaturen trenger man både det originale dokumentet og
signaturen.

    C:\>gpg --verify doc.sig doc.txt
    gpg: Signature made Fri Jun  4 12:38:46 2016 CDT using RSA key ID AB4T76AC
    gpg: Good signature from "Alice (Judge) <alice@cyb.org>"
