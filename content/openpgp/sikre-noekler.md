+++
weight = 9
title = "Sikker oppbevaring av nøkler"
date = "2017-02-22T12:31:51+01:00"
toc = true
next = "/openpgp/rotere-noekler"
prev = "/openpgp/noekkelpreferanser"

aliases = [
    "/kom-i-gang/sikre-noekler",
    "/riktig-bruk/sikre-noekler"
]

+++

Sikker oppbevaring av din private nøkkel er viktig av flere årsaker. For det
første vil personer med tilgang til din nøkkel kunne lese meldinger du har
mottatt, samtidig som man kan signere meldinger på vegne av deg.

Dersom du mister din egen nøkkel vil du måtte generere nye, distribuere de
til de du kommuniserer med samt du må bygge et nytt tillitsnettverk. Alt dette
er arbeid som med enkle steg kan ungås.

I dette kapittelet skal vi generere nøkler på en sikker installasjon av Tails,
som lagres kryptert på en USB-minnepinne.

Tails
-----
For å ungå at en angriper får tilgang til dine nøkler ved hjelp av malware eller
lignende installert på din maskin anbefales [Tails](https://tails.boum.org/).
Tails er et operativsystem som installeres på en USB-minnepinne, som ikke
lagrer endringer som blir gjort.
Vi beskriver ikke selve installasjoen av Tails da den er meget godt beskrevet i
[installasjonsguiden for Tails](https://tails.boum.org/install/os/index.en.html).

{{% notice note %}}
Når du installerer Tails må du sette opp varig (*persistent*) lagring. Dette må også [aktiveres for GnuPG](https://tails.boum.org/doc/first_steps/persistence/configure/).
{{% /notice %}}

{{% notice warning %}}
Etter at du har installert Tails, og satt opp varig lagring for GnuPG må du teste
at dette fungerer. Det gjør du ved å generere en testnøkkel, og så restarter du
maskinen. Dersom denne fremdeles er der etter en restart vet du at det virker.
{{% /notice %}}

Oppsett
-------
Det vi ønsker å oppnå er å lagre hovednøkkelen på en kryptert USB-minnepinne,
mens vi kopierer ut en undernøkkel for kryptering og signering til de enhetene
vi ønsker. Dersom denne enheten eller nøkkelen komprimiteres kan vi tilbakekalle
undernøkkelen og generere en ny. Så lenge vår krypterete USB-minnepinne ikke
komprimiteres kan vi beholde vår hovednøkkel og dermed også fingeravtrykket og
tillitsnettet vårt.

Generere nøkler
---------------
{{% notice note %}}
Tails kommer med både GnuPG 2.0 og 1.4. For å bruke 2.0 kjører vi *gpg2*.
{{% /notice %}}

    amnesia@amnesia:~$ gpg2 --gen-key
    gpg (GnuPG) 2.0.26; Copyright (C) 2013 Free Software Foundation, Inc.
    This is free software: you are free to change and redistribute it.
    There is NO WARRANTY, to the extent permitted by law.

    Please select what kind of key you want:
       (1) RSA and RSA (default)
       (2) DSA and Elgamal
       (3) DSA (sign only)
       (4) RSA (sign only)
    Your selection? 4
    RSA keys may be between 1024 and 4096 bits long.
    What keysize do you want? (2048)
    Requested keysize is 2048 bits
    Please specify how long the key should be valid.
             0 = key does not expire
          <n>  = key expires in n days
          <n>w = key expires in n weeks
          <n>m = key expires in n months
          <n>y = key expires in n years
    Key is valid for? (0) 1y
    Key expires at Tue 20 Feb 2018 06:19:33 PM UTC
    Is this correct? (y/N) y

    GnuPG needs to construct a user ID to identify your key.

    Real name: Alice
    Email address: alice@example.com
    Comment:
    You selected this USER-ID:
        "Alice <alice@example.com>"

    Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o
    You need a Passphrase to protect your secret key.

    We need to generate a lot of random bytes. It is a good idea to perform
    some other action (type on the keyboard, move the mouse, utilize the
    disks) during the prime generation; this gives the random number
    generator a better chance to gain enough entropy.
    gpg: key 0x9384FE7B9D82D22F marked as ultimately trusted
    public and secret key created and signed.

    gpg: checking the trustdb
    gpg: 3 marginal(s) needed, 1 complete(s) needed, PGP trust model
    gpg: depth: 0  valid:   1  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 1u
    gpg: next trustdb check due at 2018-02-20
    pub   2048R/0x9384FE7B9D82D22F 2017-02-20 [expires: 2018-02-20]
          Key fingerprint = CB24 6911 23AD 4842 6247  EA24 9384 FE7B 9D82 D22F
    uid                 [ultimate] Alice <alice@example.com>

    Note that this key cannot be used for encryption.  You may want to use
    the command "--edit-key" to generate a subkey for this purpose.

Vi genererer nøkler på vanlig måte, men legg merke til at vi bare laget
signeringsnøkkel. Vi må nå lage en undernøkkel for å motta krypterte meldinger,
samt en undernøkkel for å signere meldinger.

Gnerere undernøkler
-------------------

    amnesia@amnesia:~$ gpg2 --edit-key alice@example.com
    gpg (GnuPG) 2.0.26; Copyright (C) 2013 Free Software Foundation, Inc.
    This is free software: you are free to change and redistribute it.
    There is NO WARRANTY, to the extent permitted by law.

    Secret key is available.

    pub  2048R/0x9384FE7B9D82D22F  created: 2017-02-20  expires: 2018-02-20  usage: SC
                                   trust: ultimate      validity: ultimate
    [ultimate] (1). Alice <alice@example.com>

    gpg> addkey
    Key is protected.

    You need a passphrase to unlock the secret key for
    user: "Alice <alice@example.com>"
    2048-bit RSA key, ID 0x9384FE7B9D82D22F, created 2017-02-20

    Please select what kind of key you want:
       (3) DSA (sign only)
       (4) RSA (sign only)
       (5) Elgamal (encrypt only)
       (6) RSA (encrypt only)
    Your selection? 4
    RSA keys may be between 1024 and 4096 bits long.
    What keysize do you want? (2048)
    Requested keysize is 2048 bits
    Please specify how long the key should be valid.
             0 = key does not expire
          <n>  = key expires in n days
          <n>w = key expires in n weeks
          <n>m = key expires in n months
          <n>y = key expires in n years
    Key is valid for? (0) 1y
    Key expires at Tue 20 Feb 2018 06:33:24 PM UTC
    Is this correct? (y/N) y
    Really create? (y/N) y
    We need to generate a lot of random bytes. It is a good idea to perform
    some other action (type on the keyboard, move the mouse, utilize the
    disks) during the prime generation; this gives the random number
    generator a better chance to gain enough entropy.

    pub  2048R/0x9384FE7B9D82D22F  created: 2017-02-20  expires: 2018-02-20  usage: SC
                                   trust: ultimate      validity: ultimate
    sub  2048R/0x3FA64433C98A17BA  created: 2017-02-20  expires: 2018-02-20  usage: S
    [ultimate] (1). Alice <alice@example.com>

    gpg> addkey
    Key is protected.

    You need a passphrase to unlock the secret key for
    user: "Alice <alice@example.com>"
    2048-bit RSA key, ID 0x9384FE7B9D82D22F, created 2017-02-20

    Please select what kind of key you want:
       (3) DSA (sign only)
       (4) RSA (sign only)
       (5) Elgamal (encrypt only)
       (6) RSA (encrypt only)
    Your selection? 6
    RSA keys may be between 1024 and 4096 bits long.
    What keysize do you want? (2048)
    Requested keysize is 2048 bits
    Please specify how long the key should be valid.
             0 = key does not expire
          <n>  = key expires in n days
          <n>w = key expires in n weeks
          <n>m = key expires in n months
          <n>y = key expires in n years
    Key is valid for? (0) 1y
    Key expires at Tue 20 Feb 2018 06:33:44 PM UTC
    Is this correct? (y/N) y
    Really create? (y/N) y
    We need to generate a lot of random bytes. It is a good idea to perform
    some other action (type on the keyboard, move the mouse, utilize the
    disks) during the prime generation; this gives the random number
    generator a better chance to gain enough entropy.

    pub  2048R/0x9384FE7B9D82D22F  created: 2017-02-20  expires: 2018-02-20  usage: SC
                                   trust: ultimate      validity: ultimate
    sub  2048R/0x3FA64433C98A17BA  created: 2017-02-20  expires: 2018-02-20  usage: S
    sub  2048R/0x8797A8A2930D2881  created: 2017-02-20  expires: 2018-02-20  usage: E
    [ultimate] (1). Alice <alice@example.com>

    gpg> save
    amnesia@amnesia:~$

Du kan nå se at det finnes to undernøkler (*sub*), en for kryptering (*E*), og en
for signering (*S*).

Eksportere undernøkler
----------------------
Vi kan nå eksportere undernøklene til de enhenten vi bruker i hverdagen.


    amnesia@amnesia:~$ gpg2 --export-secret-subkeys > subkeys.gpg

Dette lagrer våre *private* undernøkler i filen *subkeys.gpg*. Disse har
samme passord som vi satt når vi genererte hovednøkkelen. Denne filen kan vi
nå kopiere til de klientne vi vil benytte OpenPGP på.

Importere nøkler på klienten
----------------------------

Når du har kopiert *subkeys.gpg* inn på klienten din importerer vi undernøklene
våre.


    amnesia@amnesia:~$ gpg2 --import subkeys.gpg
    gpg: key 0x9384FE7B9D82D22F: secret key imported
    gpg: key 0x9384FE7B9D82D22F: public key "Alice <alice@example.com>" imported
    gpg: Total number processed: 1
    gpg:               imported: 1  (RSA: 1)
    gpg:       secret keys read: 1
    gpg:   secret keys imported: 1

    amnesia@amnesia:~$ gpg2 -K
    /home/amnesia/.gnupg/secring.gpg
    --------------------------------
    sec#  2048R/0x9384FE7B9D82D22F 2017-02-20 [expires: 2018-02-20]
          Key fingerprint = CB24 6911 23AD 4842 6247  EA24 9384 FE7B 9D82 D22F
    uid                            Alice <alice@example.com>
    ssb   2048R/0x3FA64433C98A17BA 2017-02-20
    ssb   2048R/0x8797A8A2930D2881 2017-02-20

Vi ser nå at nøklene er importert, men også at vår hovednøkkel (*sec*) er etterfulgt
av en firkant (*#*). Dette betyr at denne nøkkelen ikke er tilgjengelig på denne
enheten.

Ta backup
---------

Det er nå på tide å [sikkerhetskopiere](/openpgp/noekkelring/#sikkerhetkopiering) nøklene.
Sikkerhetskopien lagrer du på en egen USB-minnepinne. Du har nå en kopi av nøklene
på din Tails minnepinne, samt en ekstra kopi på en egen USB-minnepinne.

{{% notice warning %}}
Sikkerhetskopien er bare beskyttet av passordet du satt når du genererte nøklene. Husk derfor å bare benytte denne minnepinnen når du kjører Tails.
{{% /notice %}}
