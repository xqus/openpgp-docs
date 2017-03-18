+++
date = "2017-02-22T10:59:58+01:00"
toc = true
next = "/openpgp/wot"
prev = "/openpgp/signering"
weight = 7
title = "Kryptering"


aliases = [
    "/kom-i-gang/kryptering"
]
+++

Kryptering av en melding eller fil gjør at ingen andre enn avsender og
mottaker kan lese innholdet. Når du skal sende og motta krypterte meldinger har
din offentlige og private nøkkel helt klare funksjoner. Du kan se på din offentlige
nøkkel som en åpen safe. Når du krypterer et dokument legger du det inn i safen
og vrir om kodelåsen flere ganger. Den private nøkkelen er kombinasjonen du
trenger for å åpne safen.

Hvis du vil kryptere en melding til Alice bruker du Alice sin offentlige nøkkel.
Hun kan da dekryptere den med sin private nøkkel. Hvis Alice vil sende deg en
kryptert melding krypterer hun den med din offentlige nøkkel. Du kan da
dekryptere den med din private nøkkel.

## Kryptering
{{% notice warning %}}
Før du kan sende krypterte meldinger må du importere den offentlige nøkkelen til
mottakeren, slik som beskrevet i Nøkkelring-kapittelet.
{{% /notice %}}

     amnesia@amnesia:~$ gpg2 --output doc.gpg --encrypt -r alice@example.com test.txt

`-r` parameteren spesifiseres en gang for hver mottaker og er
etterfulgt av en mottaker. I dette tilfellet `aliceexample.com`. Dersom du selv
skal kunne dekryptere dokumentet må du også spesifisere deg selv som mottaker i
tillegg.

Du kan også lagre de krypterte dokumentet som ASCII tekst som er litt mer lesbart
ved å bruke `--armor` parameteren.

    amnesia@amnesia:~$ gpg2 --armor --output doc.asc --encrypt -r alice@example.com test.txt
    amnesia@amnesia:~$ cat doc.asc
    -----BEGIN PGP MESSAGE-----

    hQEMA2t88U6yRa3AAQgAslk5MYEmM8Mqjtj9dACFzuOIwfM+vwGZ06zXheOo9oId
    SsV3Uowpxi74YApXbPvEoMpSpQMUgegF0GafBbBzFL/W/f0IK3nBM4mxsK07M98e
    Ub77azNkx2oLilKnYstN4IhZr9Xu2fFSle0hRFo/u0XU0+GS97bKri64ABJFWZwF
    Y+kiFaB9QG0ETPSWulCL2us6miZ8x8yDZQ/tUNCsaIYukYAxiqZYbSn2vQ+yB1sJ
    ki6MqWPw6lLLl90XJumL3YMS3s2Yi+yUOU9xhpqLGt2kaN86AEQJcSSUC7fxDJu3
    kJyEjAe8aNcWk0o16VNhCdqIzwnBCVnFExfcezUzDdJSAc1ql7DCa8XN2BmM/DzE
    S2TYrahjX9J+JN+vu+h5/Y733Yekxd2wt7HWAbYcFGiL+UGFiXxmHKW1fsTMh/d2
    0Idfdb8BsZ/ROkv2JFfHMBboFw==
    =E/Yx
    -----END PGP MESSAGE-----


### Dekryptering
For å dekryptere et dokument benyttes `--decrypt` parameteren. Du trenger da
den private nøkkelen som tilhører den offentlige nøkkelen som ble brukt for å
kryptere dokumentet.

    amnesia@amnesia:~$ gpg2 --output doc.txt --decrypt doc.gpg

    You need a passphrase to unlock the secret key for
    user: "Alice <alice@example.com>"
    2048-bit RSA key, ID 0x6B7CF14EB245ADC0, created 2017-02-25
         (subkey on main key ID 0x3E2A6E298A8C9B2C)

    gpg: encrypted with 2048-bit RSA key, ID 0x6B7CF14EB245ADC0, created 2017-02-25
      "Alice <alice@example.com>"
    amnesia@amnesia:~$ cat doc.txt
    Hello World
    Hello
    amnesia@amnesia:~$
