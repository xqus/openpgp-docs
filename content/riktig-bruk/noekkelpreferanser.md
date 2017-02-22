+++
weight = 1
title = "Nøkkelpreferanser"
date = "2017-02-22T12:31:51+01:00"
toc = true
next = "/riktig-bruk/sikre-noekler"
prev = "/riktig-bruk"

+++

Når du genererer dine OpenPGP nøkler har du mange forskjellige valg når det
gjelder type nøkkel, funksjonen til nøklene og nøkkellengde. Hva som passer best
for deg er vanskelig å si da hver enkelt har forskjellige behov. Jeg har alikavel
forsøkt å oppsummere hva som er god praksis.

Nøkkeltype
----------

Når du genererer nøkler kan du velge mellom RSA, DSA og Elgamal. Du kan også
velge å bare generere signerings nøkler. Det vil si at det ikke er mulig å
kryptere data til den offentlige nøkkelen. Dette kan være fornuftig dersom du
ønsker å lagre din mesternøkkel på en datamaskin som du ikke bruker til daglig.
I så fall må du lage en egen undernøkkel til bruk for kryptering.

I utgangspunktet anbefales RSA forran DSA av flere årsaker
(se [GnuPG.org sin FAQ](https://www.gnupg.org/faq/gnupg-faq.html#recommended_ciphers)).


Undernøkler
-----------

Det er mulig å opprette undernøkler til ditt masternøkkelpar. Du kan for eksempel
opprette en signeringsnøkkel for hver enhet du sender e-post fra. Det er dersverre
problematisk å ha flere undernøkler for kryptering da bare en av de vil bli brukt
når data krypteres. Det vil si at meldingen bare kan dekrypteres på en enhet.


Nøkkellengde
------------

GnuPG støtter RSA nøkler opp til 4096 bits men anbefalingen er RSA 2048.
Grunnen til det er at RSA-4096 gir minimalt bedre sikkerhet enn RSA-2048 mens
ytelsen reduseres drastisk med RSA-4096.

Hvis du ikke føler at RSA-2048 er godt nok anbefales eliptisk-kurve-algoritmer.

Se foreøvrig [GnuPG.org sin FAQ](https://www.gnupg.org/faq/gnupg-faq.html#please_use_ecc).
