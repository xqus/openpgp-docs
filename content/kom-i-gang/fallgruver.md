+++
date = "2017-02-24T16:09:30+01:00"
toc = true
next = "/riktig-bruk/"
prev = "/kom-i-gang/wot"
weight = 8
title = "Fallgruver"

+++

OpenPGP er ikke en magisk flosshatt som løser alle problemer i verden uten å
skape noen nye utfordringer. Det finnes flere fallgruver ved bruk av OpenPGP.
Dette er ikke en komplett liste, men en oversikt over noen av de fallgruvene som
oftest skaper problemer for de som benytter OpenPGP.

### Dårlig passord
I kapittelet om [konsepter](/kom-i-gang/konsepter/) skrev jeg at
all sikkerheten i krypteringsalgortimene ligger i din private nøkkel. Det
eneste som beskytter din private nøkkel fra å bli missbrukt dersom den kommer
på avveie er passfrasen som beskytter den. Passfrasen er faktisk en kryteringsnøkkel
for din private nøkkel. Derfor er det veldig viktig at denne passfrasen er god.

{{% notice info %}}
Ordet *passfrase* brukes besvisst i steden for ordet passord. Meningen er å oppmuntre til
bruk av setninger eller flere ord som passord.
{{% /notice %}}  

![Password Strength](https://imgs.xkcd.com/comics/password_strength.png?width=50%&classes=border)

Det finnes mange meninger om hvordan man skal lage seg et bra passord, og hvor
mange passord man skal ha. Hvis det er et passord som bør være forskjellig fra
alle andre så er det passordet som beskytter din private nøkkel. Tegnestripen over
er ikke bare morsom, men også et veldig bra tips.

Det finnes flere måter å generere en passfrase. [Diceware](http://world.std.com/~reinhold/diceware.html)
er kanskje en av de mest nerdete, men da får du et meget bra passord. Bitcoin
lommebøker bruker en variant av Diceware. Jeg anbefaler [følgende ordliste](https://raw.githubusercontent.com/bitcoin/bips/master/bip-0039/english.txt)
hvis du vil lage deg en diceware passfrase. Denne ordlisten inneholder ikke ord
som staves nesten likt. Dersom du vil generere en passfrase automatisk fra denne
ordlisten finnes det et [online verktøy](https://iancoleman.github.io/bip39/).

### Metadata
En av de største svakhetene med OpenPGP når det brukes til kryptering av epost
er at det bare selve innholdet i meldingen som krypteres. Det betyr at metadata
i eposten er synlig for epostopertøren og andre snokere. Innholdet i denne
metadataen varierer litt avhengig av epostklient og hvordan den blir sendt, men
i de fleste tilfeller vil denne inneholde:

 * Emne
 * Avsender
 * Mottaker
 * Epostserver som ble benyttet
 * Tidspunkt når meldingen ble sendt

Merk at metadata vil være identisk enten du bruker OpenPGP eller ikke til å
kryptere epost. Lekasjen av metadata blir ikke større om du benytter OpenPGP men
det betyr at selv om du sender en kryptert epost så vil deler av den være
ukryptert.

{{% notice tip %}}
Noen epostklienter (bl.a. *Thunderbird*) støtter kryptering av emnefeltet. Selv
om dette ikke er en standarisert metode kan det være verdt å undersøke.
{{% /notice %}}  

### Tapte nøkler
Dersom du mister tilgangen til din egen private nøkkel vil du ikke lenger være
i stand til å dekryptere meldinger som var kryptert med den nøkkelen som mottaker.
Dette er normalt sett ikke et stort problem med kryptert epost, men kan være et
større problem dersom du hadde en kryptert backup av feriebildene. Det er derfor
veldig viktig med
[sikkerhetskopi](/kom-i-gang/noekkelring/#sikkerhetkopiering) av
din private nøkkel.

Oppbevar sikkerhetskopien på en minnepinne som du oppbevarer et trygt sted.
Sammen med denne minnepinnen bør du også ha en lapp med passfrasen som
beskytter nøkkelen din.

### Ikke oppdaterte nøkler
Dersom de du kommuniserer med ikke oppdaterer din offentlige nøkkel fra
nøkkeltjenere regelmessig, og du ikke oppdaterer de offentlige nøklene til de du
kommuniserer med kan man rissikere at du krypterer meldinger med nøkler som
er utgått eller tilbakekalt. I beste falle får du beskjed om å kryptere meldingen
på nytt med mottakeren sin nye nøkkel. I værste fall kan meldingen havne i
hendene til en angriper som har fått tilgang til den private nøkkelen.
