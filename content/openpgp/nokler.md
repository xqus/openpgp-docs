+++
date = "2017-02-22T10:59:58+01:00"
toc = true
next = "/openpgp/noekkelring"
prev = "/openpgp/enigmail"
weight = 3
title = "Dine nøkler"

aliases = [
    "/kom-i-gang/nokler",
    "/kom-i-gang/noekkelpreferanser",
    "/riktig-bruk/noekkelpreferanser",
    "/openpgp/noekkelpreferanser"
]

+++

Dine OpenPGP-nøkler er det du, eller de du kommuniserer med bruker som grunnalag
i de kryptografiske funksjonene. I OpenPGP består dine nøkler av flere
forskjellige nøkler som til sammen danner ditt nøkkelpar.

Et OpenPGP nøkkelpar identifiseres med det som kalles et fingerprint eller
fingeravtrykk. Et fingeravtrykk kan se slik ut:
`EAB9 F918 6C7F E39E EBA3  BAA8 D775 F425 69CD DB80`
Bare ved å verifisere hele fingeravtrykket kan du være sikker på at det er
riktig nøkkel.

Fingeravtrykket for din nøkkel vil være det samme uansett hvilke endringer du
gjør med nøkkelen din.

### Offentlig nøkkel
Din offentlige nøkkel er den delen av nøkkelen du skal dele med andre. Denne
benyttes til å kryptere meldinger som skal sendes til deg, og til å verifisere
meldinger du har signert med OpenPGP.

{{% notice note %}}
Meldinger som er kryptert med din offentlige nøkkel kan bare dekrypteres med din private nøkkel.
{{% /notice %}}

### Privat nøkkel
Din private nøkkel benyttes til å signere meldinger du sender, samt å dekryptere
meldinger som er kryptert med din offentlige nøkkel. Det er mulig å ha flere
undernøkler i ditt nøkkelpar, til forskjellig bruk eller til forskjellige
enheter. De private nøklene kan ha flere funksjoner:

1. **Autorisering:** Benyttes for å signere andre nøkler og brukeridentiteter for å bevise at de tilhører ditt nøkkelpar.
2. **Kryptering:** Benyttes til å motte krypterte meldinger.
3. **Signering:** Benyttes til å signere utgående meldinger for å bevise at de er sendt av eieren av en bestemt OpenPGP nøkkel.
4. **Autentisering:** Benyttes til blandt annet autntisering av SSH.

Når du lager ditt nøkkelpar må du velge hvilken nøkkeltype din primære nøkkel
skal ha. Din primære nøkkel vil alltid benyttes til *autorisering* av eventuelt
andre nøkler og av brukeridentiter.

{{% notice warning %}}
Gjør alt du kan for å holde din private nøkkel privat.
{{% /notice %}}

### Brukeridentiteter
Brukeridentiteter er det som tilegner et navn og en epostadresse til din nøkkel.
Et nøkkelpar kan ha så mange brukeridentiteter man vil, men en av de vil være
primær og vil bli brukt for å gi navn til nøkkelen i OpenPGP verktøyene.
En brukeridentitet består av ``Navn (kommentar) <epost>``. Kommentar og epost er
i utgangspunktet frivillig.

### Generer dine egne nøkler
For å generere dine nøkler starter du GnuPG med `--gen-key` parameteren.
Hvilken nøkkel du skal generere, og hvilke alternativer du skal velger
er avhengig av bruken.


    amnesia@amnesia:~$ gpg2 --gen-key
    gpg (GnuPG) 2.0.30; Copyright (C) 2015 Free Software Foundation, Inc.
    This is free software: you are free to change and redistribute it.
    There is NO WARRANTY, to the extent permitted by law.

    Please select what kind of key you want:
    (1) RSA and RSA (default)
    (2) DSA and Elgamal
    (3) DSA (sign only)
    (4) RSA (sign only)
    Your selection?

Du får da velg om hvilken nøkkel du ønsker. I utgangspunktet er valg 1 greit.



    Your selection? 1
    RSA keys may be between 1024 and 4096 bits long.
    What keysize do you want? (2048)

Deretter må du velge nøkkellengde. Standardvalget på **2848** er i de fleste
tilfeller fornuftig, selv om større egentlig er bedre.

{{% notice tip %}}
GnuPG støtter RSA nøkler opp til 4096 bits men anbefalingen er RSA 2048.
Grunnen til det er at RSA-4096 gir minimalt bedre sikkerhet enn RSA-2048 mens
ytelsen reduseres drastisk med RSA-4096.
Hvis du ikke føler at RSA-2048 er godt nok anbefales eliptisk-kurve-algoritmer.
Se foreøvrig [GnuPG.org sin FAQ](https://www.gnupg.org/faq/gnupg-faq.html#please_use_ecc).
{{% /notice %}}

    What keysize do you want? (2048) 2048
    Requested keysize is 2048 bits
    Please specify how long the key should be valid.
           0 = key does not expire
        <n>  = key expires in n days
        <n>w = key expires in n weeks
        <n>m = key expires in n months
        <n>y = key expires in n years
    Key is valid for? (0)

Neste steg er gyldighetsperioden til nøkkelen. Denne kan du endre når som helst,
også etter at den er gått ut. Derfor anbefaler jeg at du setter denne til et år,
slik at dersom du mister tilgangen til nøkkelen og må lage en ny så går den gamle
ut på et eller annet tidspunkt.


    Key is valid for? (0) 1y
    Key expires at 12/29/17 19:06:04 W. Europe Standard Time
    Is this correct? (y/N) y

    GnuPG needs to construct a user ID to identify your key.

    Real name:

Nå skal du lage nøkkelparets første brukeridentitet. Det er dette som vises
når andre laster inn ditt nøkkelpar. Skriv inn ditt navn og epostadresse.


    Real name: Simba Larki
    Email address: simba@exaple.com
    Comment:
    You selected this USER-ID:
        "Simba Larki <simba@exaple.com>"

    Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o
    You need a Passphrase to protect your secret key.

Siste steget er å valge et passord, eller passfrase. Velg et skikkelig passord,
eller en setning. Det er dette som hindrer at andre får tilgang til din private
nøkkel dersom de får tilgang til datmaskinen eller filene dine.


    We need to generate a lot of random bytes. It is a good idea to perform
    some other action (type on the keyboard, move the mouse, utilize the
    disks) during the prime generation; this gives the random number
    generator a better chance to gain enough entropy.
    gpg: key 86D91256 marked as ultimately trusted
    public and secret key created and signed.

    pub   2048R/86D91256 2016-12-29 [expires: 2017-12-29]
          Key fingerprint = A0EF C173 8E8E 8772 25AC  AAFD 3E7C 7812 86D9 1256
    uid       [ultimate] Simba Larki <simba@example.org>
    sub   2048R/27FA711C 2016-12-29 [expires: 2017-12-29]

Du kan nå se at nøkkelen med fingeravtrykket
`A0EF C173 8E8E 8772 25AC  AAFD 3E7C 7812 86D9 1256` og nøkkelid `0x86D91256`
er opprettet.

{{% notice note %}}
Nøkkelid består av de 8 (kort nøkkelid) eller 16 (lang nøkkelid) siste tegnene i fingeravtrykket med `0x` rett forran.
{{% /notice %}}

Du kan se dine nøkkelpar med kommandoen `amnesia@amnesia:~$ gpg2 -K --fingerprint`

### Tilbakekallingssertifikat
Et tilbakekallingssertifikat benyttes dersom du ikke lenger har kontroll over din
private nøkkel. Dette kan brukes uten at du har tilgang til den private nøkkelen.
Dersom du tilbakekaller nøkkelen din vil den ikke lenger kunne brukes til å
signere eller kryptere meldinger.


    amnesia@amnesia:~$ gpg2 --output revoke.asc --gen-revoke simba@example.org

Dette vil lagre ditt tilbakekallingssertifikat som `revoke.asc`. Ta godt vare
på dette. Dersom andre får tilgang til det kan de tilbakekalle dit nøkkelpar.
