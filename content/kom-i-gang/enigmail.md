+++
date = "2017-02-24T08:57:52+01:00"
toc = true
next = "/kom-i-gang/konsepter"
prev = "/kom-i-gang/hva-er-openpgp"
weight = 2
title = "Kryptert epost med Enigmail"

+++

Installer Thunderbird
---------------------
[Thunderbird](https://www.mozilla.org/nb-NO/thunderbird/) er en **gratis**
åpen-kildekode **epost klient** utviklet av Mozilla, de samme som har utviklet
**Firebird**. En epost klient som Thunderbird fungerer fint som en erstating for
det nettleserbaserte grenesnittet til din eposttilbyder (Gmail eller lignende).
Det første du må gjøre er å sette opp Thunderbird til å lese din e-post. Første
gang du starter [Thunderbird](https://www.mozilla.org/nb-NO/thunderbird/) vil
den veilede deg gjennom oppsettet av din epost.

![Steg 1a](../../images/step1a-install-wizard.png?width=30%)

Installer GnuPG
---------------
Dersom du ikke har installert GnuPG enda følg veilednignen
[her](/openpgp-docs/kom-i-gang/hva-er-openpgp/#kom-i-gang).

Installer Enigmail
------------------
Enigmail er en utvidelse til Thunderbird som gir deg et grensesnitt til *GnuPG*
for automatisk å kryptere og signere epost. Denne utvidelsen kan installeres
gjennom Utvidelses grensesnittet til Thunderbird.

I Thunderbird velg **Verktøy** og så **Utvidelser**.
![Steg 1b](../../images/step1b-01-tools-addons.png?width=20%)
Søk etter **Enigmail** i søkreruten øverst til høyre.
![Steg 1b](../../images/step1b-02-search.png?width=20%)
Finn **Enigmail** i listen og velg installer.
![Steg 1b](../../images/step1b-03-install.png?width=20%)
Følg anvisingene på skjermen og restart Thunderbird når du er ferdig.

Lag dine nøkler
---------------
Før du kan sende og motta kryptert epost, og sende epost signert med din digitale
signatur må du opprette et nøkkelpar.
![Steg 1b](../../images/step2a-01-make-keypair.png?width=20%)

Første gang du starter Thunderbird etter at Enigmail er installert skal
**Oppsettsveilederen** starte. Dersom den ikke gjør det kan du starte den ved å
velge **Enigmail** og så **Oppsettsveileder**.
Følg anvinsingen på skjermen så vil programet generere nøklene for deg.
Før du lager dine nøkler anbefaler jeg at du leser
[Komme i gang med nøkler](/openpgp-docs/kom-i-gang/nokler/) (du trenger **ikke**
generere dine nøkler slik som beskrevet her) og
[Nøkkelpreferanser](/openpgp-docs/riktig-bruk/noekkelpreferanser/).

{{% notice tip %}}
Nøkler du oppretter og importerer i Enigmail vil være tilgjengelig i GnuPG og omvendt.
{{% /notice %}}

Publiser din offentlige nøkkel
------------------------------
For at andre lettere skal kunne finne din offentlige nøkkel kan du laste den
opp til en [nøkkeltjener](/openpgp-docs/kom-i-gang/wot/#nøkkelservere).

For å gjøre dette velg **Thunderbird** og så **Nøkkelhåndtering**.
Høyreklikk på din nøkkel og velg **Last opp offentlige nøkler til nøkkeltjener**.

*Images are copyright © 2014-2016 Free Software Foundation, Inc.*
