+++
date = "2017-02-22T10:59:58+01:00"
toc = true
next = "/kom-i-gang/wot"
prev = "/kom-i-gang/signering"
weight = 7
title = "Kryptering"

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

Før du kan sende krypterte meldinger må du importere den offentlige nøkkelen til
mottakeren, slik som beskrevet i Nøkkelring-kapittelet.

{{% notice warning %}}
Før du sender en kryptert melding er det viktig at du verifiserer at du bruker riktig offentlig nøkkel.
{{% /notice %}}

     C:\>gpg --output doc.gpg --encrypt --recipient alice@cyb.org doc.txt

`--recipient` parameteren spesifiseres en gang for hver mottaker og er
etterfulgt av en mottaker. I dette tilfellet `alice@cyb.org`. Dersom du selv
skal kunne dekryptere dokumentet må du også spesifisere deg selv som mottaker i
tillegg.

For å dekryptere et dokument benyttes `--decrypt` parameteren. Du trenger da
den private nøkkelen som tilhører den offentlige nøkkelen som ble brukt for å
kryptere dokumentet.

    C:\>gpg --output doc.txt --decrypt doc.gpg
