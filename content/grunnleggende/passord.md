+++
weight = 2
title = "Gode passord"
date = "2017-03-13T12:24:25+01:00"
toc = true
next = "/openpgp"
prev = "/grunnleggende/introduksjon"

+++

Et av de grunnleggende krav i all sikker kommunikasjon er valg av passord.
Det finnes utallige tanker om hvordan man lager, husker, oppbevarer og bytter
passord. De fleste konseptene er basert på antagelser og tradisjon, fremfor
forskning og sunn fornuft.

 > Rule 1 about passwords is "there are no rules!"

### Hvorfor er gode passord viktig?

Gode passord er viktig av flere årsaker. Passordet er ofte det eneste som står
mellom en angriper og full tilgang til din Facebook-konto, datamaskin eller epost.
Det finnes avanserte dataprogramer som kan gjette seg frem til ditt passord basert
på offentlig informasjon om deg, som for eksempel navn på samboer/ektefelle, barn
kjæledyr osv. Det betyr at navnet på katten etterfulgt av fødselsåret til barna
er typisk passord som enkelt kan gjettes.

### Så hva er et bra passord?

Et godt passord er et passord som ikke enkelt kan gjettes basert på informasjon
om deg som person. Det er også en fordel at du klarer å huske passordet ditt.

![XKCD: Password Strength](https://imgs.xkcd.com/comics/password_strength.png)

Man kan diskutere om budskapet i stripen over er riktig eller ikke, men den er i
alle tilfeller inne på noe. Gammeldagsepassord tips er, gammeldagse.
Jeg skrev i starten at det ikke finnes noen regler om passord, men det finnes
noen tips.

 1. Et passord skal være lett å huske, men vanskelig å gjette. Bruk gjerne setininger.
 2. Bruk *aldri* det samme passordet på tvers av internettjenester.
 3. Husk de passordene du trenger hver dag. Resten kan du skrive ned hjemme. Det finnes god software for lagring av passord.
 4. Bruk to-faktors autentisering der det er mulig (hvertfall på epost kontoen din).

### Diceware

{{% notice info %}}
I mange tilfeller brukes ordet *passfrase* brukes besvisst i steden for ordet passord. Meningen er å oppmuntre til
bruk av setninger eller flere ord som passord.
{{% /notice %}}

[Diceware](http://world.std.com/~reinhold/diceware.html) er en meteode for å generere passord ved bruk av terninger. Tanken er
at man benytter en liste med numererte ord og et sett med vanlige terninger til
å lage en passfrase bestående av flere tilfeldige ord fra ordlisten.
Alle sifferne som blir brukt i nummereringen av ordene i ordlisten er mellom 1 og
6, slik at du kan bruke utfallet av terningene til å velge ord.

Det finnes utallige ordlister, noen krever 5 terninger, andre krever 4. Antall ord
i ordlisten sammen med antall ord i paafrasen vil avgjøre styrken til passordet.

Jeg har satt sammen en [Norsk ordliste](https://gist.github.com/xqus/6f779b73b617aeb180800fe38965ac0e) der
vanskelige ord, og ord som ligner på hverandre er tatt ut.
