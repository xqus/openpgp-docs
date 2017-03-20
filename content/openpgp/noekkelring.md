+++
date = "2017-02-22T10:59:58+01:00"
toc = true
next = "/openpgp/signering"
prev = "/openpgp/nokler"
weight = 4
title = "Din nøkkelring"

aliases = [
    "/kom-i-gang/noekkelring",
    "/kom-i-gang/wot"
]


+++

Din nøkkelring er et begrep som brukes om de offentlige og private nøklene du
har en kopi av på din datamaskin.
Din nøkkelring inneholder ikke bare dine egne offentlige og private nøkler,
men også de offentlige nøklene de du kommuniserer med. I tillegg til selve
nøklene finnes det også annen informasjon i den, som for eksmepel hvilke nøkler
du har tillit til. Du bør derfor jevnlig ta sikkerhetskopi av nøkkelringen.
Denne bør du lagre på et trygt sted.

### Hvilke nøkler skal jeg lagre i min nøkkelring?
For det første må du ha din egen private nøekkel, og din offentlige nøkkel
i nøkkelringen din. Disse trenger du for å kunne signere og dekryptere meldinger.
I tillegg til dine egne nøkler må du ha de offentlige nøklene til de du kommuniserer
med. Enten for å verifisere signaturer, eller for å kryptere meldinger.

Før du sender en kryptert melding må du være sikker på at den offentlige
nøkkelen du bruker for å kryptere meldingen faktisk tilhører den personen du
skal sende meldingen til. Hvem som helst kan lage et nøkkelpar og skrive hvilket
navn og hvilken epostadresse de vil. Det er derfor essensielt at du verifiser
fingeravtrykket til den offentlige nøkkelen før du bruker den. Det er flere måter
å gjøre dette på, for eksempel SMS eller over telefon.

For å gjøre det hele litt lettere kan man sertifisere og sette tillit til nøkler.
På denne måten bygger man seg et tillitsnett rundt nøklene. Dersom en nøkkel
er sertifiert av en annen nøkkel du har tillit ti vil OpenPGP automatisk
ha tillit til nøkkelen basert på sertifiseringen.
Tillitsnettet (Web Of Trust) forsøker å skape et nettverk av nøkler du stoler på
slik at man lettere kan knytte et nøkkelpar til en person.

For å holde styr på alle offentlige nøkler og sertifiseringer bruker OpenPGP
noe som kalles nøkkeltjenere. Du kan se på den som en digital telefonkatalog med
offentlige nøkler. Det finnes mange nøkkelservere, og de fleste sammarbeider om å holde seg
oppdatert. Jeg anbefaler at du [bruker](#importere-nøkler) `hkps://hkps.pool.sks-keyservers.net`
som nøkkelserver. Dette er ikke en enkelt nøkkelserver men en samling av oppdaterte
servere.

Det er svært viktig at du regelmessig oppdaterer de offentlige nøklene til de
du kommuniserer med fra nøkkeltjenere. Dette er eneste måte å vite at nøkkelen for eksempel ikke
er tilbakekalt. På samme måte er det viktig at du laster opp endringer i din
offentlige nøkkel dersom du gjør endringer som:

 * Endret utløpsdato
 * Tilbakekalt nøkkel
 * Ny brukeridentitet

{{% notice warning %}}
Tilstedeværelsen av en nøkkel på en nøkkelserver sier ikke noe om gyldigheten eller
tilliten til en nøkkel. Husk å **alltid** verifiser hele fingeravtrykket til en nøkkel
før du bruker den.
{{% /notice %}}  

#### Sertifisering
Når du [sertifiserer en nøkkel](/openpgp/noekkelring/#sertifisere-nøkler)
forteller du omverden at du har verifisert sammenhengen mellom *navn* og *epostadresse*
spesifisert i nøkkelen og den faktiske eieren av nøkkelen.

En sertifisering sier ikke noe om du kan stole på personen som eier nøkkelen eller
ikke. Det eneste en sertifisering sier er at sammenhengen mellom den offentlige
nøkkelen og brukeridentiteten er bekreftet.

Når du sertifiserer en offentlig nøkkel signerer du denne med din private nøkkel.
Du kan velge å lage en *lokal signatur*, denne vil lagres lokalt i din nøkkelring
og kan ikke lastes opp til nøkkelservere. Det vanligste derimot er å sertifisere
nøkler for så å laste opp sertifiseringen til nøkkelserverene.

#### Tillit
Når man snakker om tillit til en nøkkel mener man hvor mye man stoler på at
eieren til nøkkelen verifiserer at eieren til nøklene han/hun sertifiserer
er den han/hun utgir seg for å være.
Dersom du har tillit til Bob sin nøkkel, og Bob har sertifisert Alice sin nøkkel
vil du automatisk også ha tillit til Alice sin nøkkel. Hvilke nøkler du har
tillit til lagres bare lokalt i din nøkkelring. Ingen andre kan se hvem du har
tillit til, og du kan ikke se hvem som har tillit til din nøkkel.

### Importere nøkler
Det letteste når du skal importere offentlige nøkler er å søke på en nøkkelserver.
For å søke etter en offentlig nøkkel på en nøkkelserver bruker du `--search-keys`.

Før du kan ta i bruk nøkkelserver må du spesifisere dette i `gpg.conf`. Denne
filen finner du i `C:\Users\BRUKERNAVN\AppData\Roaming\gnupg` i Windows eller
`~\.gnupg` på Linux. Åpne denne filen i en valgfri teksteditor
(Notepad for eksmepel) og legg inn følgende linje.

    keyserver hkps://pool.sks-keyservers.net

*pool.sks-keyservers.net* er et nettverk av nøkkelservere som synkroniserer seg
selv i mellom. Dette gir høy tilgjengelighet av nøkler, og er derfor anbefalt.


    amnesia@amnesia:~$ gpg2 --search-keys alice@cyb.org
    gpg: searching for "alice@cyb.org" from hkps server keys.drup.no
    (1)     Alice (Rechtsanwältin) <alice@cyb.org>
              1024 bit DSA key FB5797A9, created: 2000-06-06
    Keys 1-1 of 1 for "alice@cyb.org".  Enter number(s), N)ext, or Q)uit >

Velg så nøkkelen du vil importere. Husk å å verfiser hele fingeravtrykket sammen
med eieren til nøkkelen før du tar den i bruk.


    Keys 1-1 of 1 for "alice@cyb.org".  Enter number(s), N)ext, or Q)uit > 1
    gpg: requesting key FB5797A9 from hkps server keys.drup.no
    gpg: key FB5797A9: public key "Alice (Rechtsanwältin) <alice@cyb.org>" imported
    gpg: Total number processed: 1
    gpg:               imported: 1

Du kan nå se at den nye offentlige nøkkelen er kommet inn i din nøkkelring
sammen med ditt eget nøkkelpar når du bruker  `-k --fingerprint` kommandoen.


    amnesia@amnesia:~$ gpg2 -k --fingerprint
    pub   2048R/86D91256 2016-12-29 [expires: 2017-12-29]
          Key fingerprint = A0EF C173 8E8E 8772 25AC  AAFD 3E7C 7812 86D9 1256
    uid       [ultimate] Simba Larki <simba@example.org>
    sub   2048R/27FA711C 2016-12-29 [expires: 2017-12-29]

    pub   1024D/FB5797A9 2000-06-06
          Key fingerprint = 738C 2FE2 AF16 B223 B2CC  4CED 5B2A 0A6D FB57 97A9
    uid       [ unknown] Alice (Rechtsanwältin) <alice@cyb.org>
    sub   1024g/C8B3998F 2000-06-06


Dersom du har mottat en offentlig nøkkel i for eksmepel et vedlegg til en epost
kan du importere den med `--import` paramteren.


    amnesia@amnesia:~$ gpg2 --import -i key.asc

Når nøklene er i din nøkkelring kan du benytte de til å kryptere meldinger og
verifisere signaturer.

### Eksportere nøkler
For at andre skal kunne kryptere meldinger til deg eller verifisere dine digitale
signaturer er de avhengig å importert din offentlige nøkkel føsr.

For å eksportere din offentlige nøkkel til en fil som du for eksempel kan legge
ved epost bruker du `--export` paramteren.


    amnesia@amnesia:~$ gpg2 -a --export alice@cyb.org -o key.asc
    -----BEGIN PGP PUBLIC KEY BLOCK-----
    Version: GnuPG v2

    mQENBFgM8S4BCACsRH
    [...]
    w49DLEkc
    =h9GD
    -----END PGP PUBLIC KEY BLOCK-----

### Laste opp nøkler til nøkkeltjenere
Du kan også laste opp nøkkelen din til en nøkkelserver slik at andre kan søke
den opp og laste den ned der. Dersom du har sertifisert en annen offentlig nøkkel
kan du også laste opp denne sertifiseringen. Da bruker du nøkkelid til den
offentlige nøkkelen du sertifiserte.

    amnesia@amnesia:~$ gpg2 --send-keys 0x69CDDB86
    gpg: sending key 69CDDB86 to hkps server keys.drup.no

{{% notice note %}}
Når du kommuniserer med nøkkelservere må du benytte nøkkelid. For eksempel 0x69CDDB86.
{{% /notice %}}

### Sette tillit til nøkler
Når man snakker om tillit til en nøkkel mener man hvor mye man stoler på at
eieren til nøkkelen verifiserer at eieren til en nøkkel er den han/hun utgir
seg for å være. Dersom du har tillit til Bob sin nøkkel, og Bob har sertifisert
Alice sin nøkkel vil du automatisk også ha tillit til Alice sin nøkkel.

Du setter tillit til en nøkkel med `--edit-key` parameteren.


    amnesia@amnesia:~$ gpg2 --edit-key alice@cyb.org
    gpg (GnuPG) 2.0.30; Copyright (C) 2015 Free Software Foundation, Inc.
    This is free software: you are free to change and redistribute it.
    There is NO WARRANTY, to the extent permitted by law.


    pub  1024D/FB5797A9  created: 2000-06-06  expires: never       usage: SCA
                         trust: unknown       validity: unknown
    sub  1024g/C8B3998F  created: 2000-06-06  expires: never       usage: E
    [ unknown] (1). Alice (Rechtsanwältin) <alice@cyb.org>

    gpg>

Du blir nå vist hvilken nøkkel du skal endre. For å sette tillit bruker vi
`trust` kommandoen.

    gpg> trust
    pub  1024D/FB5797A9  created: 2000-06-06  expires: never       usage: SCA
                       trust: unknown       validity: unknown
    sub  1024g/C8B3998F  created: 2000-06-06  expires: never       usage: E
    [ unknown] (1). Alice (Rechtsanwältin) <alice@cyb.org>

    Please decide how far you trust this user to correctly verify other users' keys
    (by looking at passports, checking fingerprints from different sources, etc.)

    1 = I don't know or won't say
    2 = I do NOT trust
    3 = I trust marginally
    4 = I trust fully
    5 = I trust ultimately
    m = back to the main menu

    Your decision?

Spesifiser hvor god tillit du har til eieren av denne nøkkelen.


    gpg> save

For å lagre endringene bruker vi `save` kommandoen.

### Sertifisere nøkler
Sertifisering (eller signering) gjør man når man har verifisert sammenhengen
mellom nøkkel og person. Når man sertifiserer en nøkkel signerer du den med din
private nøkkel, slik at andre ser at du går god for denne nøkkelen.

For å signere nøkler gjør du samme som over, men i steden for `trust` bruker
du `sign` kommandoen.

{{% notice warning %}}
 Bare signer nøkler der du har verifisert sammenhengen mellom nøkkelen og personen. Verifiser **alltid** hele fingeravtrykket til en nøkkel før du signerer den.
{{% /notice %}}

Når du har signert en nøkkel kan du laste opp din signatur til nøkkelserverene
slik at andre kan se at du har verifisert nøkkelen og identiten til eieren.

    amnesia@amnesia:~$ gpg2 -send-keys 0xFB5797A9
    gpg: sending key FB5797A9 to hkps server keys.drup.no


### Oppdatere offentlige nøkler
Nøkler kan tilbakekalles eller signeres av andre brukere uten at du nødvendigvis
får vite det. Slike endringer er viktig at du får med deg. Derfor bør du synkronisere
din nøkkelring mot nøkkelservere reglemessig. Dette gjøres med `--refresh-keys`

    amnesia@amnesia:~$ gpg2 --refresh-keys

### Sikkerhetkopiering
Etterhvert som nøkkelringen vokser blir det viktigere å viktigere å ha en
sikkerhetskopi av denne.

Det er tre ting som må sikkerhetkopieres: Offentlige nøkler, tillitsdatabasen og
private nøkler.

#### Offentlige nøkler

For å sikkerhetskopiere de offentlige nøklene kopierer du bare filene
`pubring.gpg` og `pubring.kbx` fra  `C:\Users\BRUKERNAVN\AppData\Roaming\gnupg`
mappen på Windows eller i `~/.gnupg` mappen på Linux/Unix.

Får gjennopprette disse kan du bare kopiere disse tilbake på samme sted.

#### Tillitsdatabase

Tillitsdatabasen kopieres med følgende kommando

    amnesia@amnesia:~$ gpg2 --export-ownertrust > ownertrust-gpg.txt

og importeres med denne kommandoen

    C:\>gpg --import-ownertrust ownertrust-gpg.txt

#### Private nøkler

Dine private nøkler eksporteres med `--export-secret-keys`.

    amnesia@amnesia:~$ gpg2 -a --export-secret-keys -o private-keys.asc

For å importere dine private nøkler bruker du `--import`


    amnesia@amnesia:~$ gpg2 --import private-keys.asc

{{% notice warning %}}
Gjør alt du kan for å holde din private nøkkel privat.
{{% /notice %}}

Alle 4 filene bør lagres sikkert og ikke på datamaskinen, gjerne på en minnepinne.
