+++
next = "/grunnleggende/passord"
prev = "/grunnleggende"
weight = 1
title = "Introduksjon"
date = "2017-03-19T13:54:13+01:00"
toc = true

+++

### Informasjonssikkerhet
Informasjonssikkerhet er et fellesbegrep for veldig mange ting. De aller fleste
har et forhold til hva det betyr, selv om det å komme med en enkel definisjon er
vanskelig. Kort sagt så er det tre hovedprisipper vi ønsker å oppnå med
informasjonssikkerhet.

 * Konfidensialitet
 * Integritet
 * Tilgjengelighet

#### Konfidensialitet
Konfidensialitet går ut på å skjule vår data fra andre enn den tiltenkte mottakgeren,
enten det er oss selv, eller andre. Dette gjøres som regel med kryptering. Det
finnes utallige typer kryptering, og hver type har også utallige algoritmer, eller
formler for å skjule informasjonen fra uvedkommede.

#### Integritet
Integriteten til data er også viktig. Det å kunne stole på at en melding ikke
har blitt endret med på veien, eller at ingen har tuklet med arkivet ditt over
kontoutskrifter gir deg trygghet slik at du kan stole på informasjonen.

#### Tilgjengelighet
Tilgjengelighet går ut på at din data er tilgjengelig for deg når du trenger den.
Vi skal ikke snakke så mye om dette punktet i denne håndboken da det i hovedsak
berører de som drifter it-systemer. Det du skal huske på er **sikkerhetskopiering**, alltid.

### Kommunikasjonssikkerhet
Det meste i denne håndboken omhandler kommunikasjonssikkerhet. Kommunikasjonssikkerhet
kan man se på som et samlebegrep for **konfidensialitet** og **integritet**.
Hvis vi skal kommunisere sikkert med noen er vi helt avhengig av begge disse to.
Det finnes mangen måter å oppnå konfidensialitet og integritet på, og metodene
varierer med hvilken form for kommunikasjon vi driver med. Jeg liker å dele inn
informasjon inn i to grupper, siden måten vi praktiserer kommunikasjonssikkerhet
er veldig forskjellig basert på hvilken type data vi snakker om.

 * Hvilende data
 * Data i transit

#### Data i transit
Data i transit er kortlevd informasjon. Som for eksempel når du sender
fødselsnummeret ditt til nettbanken din for å starte innloggingsprosessen.
Data i transit er altså **data som beveger seg fra en enhet til en annen**. Mye av
data i transit går over til hvilende data når den når sin destinasjon.
De aller fleste kjenner igjen den grønne hengelåsen og informasjon om selskapet
bak nettsiden i adressefeltet i nettleseren når vi besøker "sikre" nettsider.

![HTTPS](/images/https.png)

Denne hengelåsen forteller oss ingen ting om hvor sikkert et nettsted er. Det
denne hengelåsen forteller oss er at informasjonen som sendes fra din nettleser
til nettsiden er kryptert, og hvem som driver nettsiden. Dette gir oss
*konfindeisalitet* og *integritet* på informasjonen i transit mellom nettleser og
nettsiden. Den forteller ingen ting om hva som skjer med informasjonen på
systemene til de som mottar den. Dersom denne informasjonen lagres på dette
systemet liker jeg å se på den som *hvilende data*.

Data i transit bør sikres så godt man kan da denne informasjonen sendes over internett og passerer mange
enhter. Disse enhetene eies av mange forskjellige firma og organisasjoner, og alle
er utenfor din kontroll. Det betyr at man kan ikke vite hvordan disse behandler
informasjonen dersom den ikke er kryptert. Ukryptert informasjon kan snappes opp og
endres på veien. Man kan se på det som å sende et postkort i posten. Alle som
jobber i posten i de forskjellige landene kortet passerer kan både lese det og
endre innholdet uten at avsender eller mottaker merker det.

#### Hvilende data
Det finnes mange typer hvilende data. All data som lagres er egentlig hvilende
data. Grunnen til at jeg liker å skille disse to datatypene er at de systemene
som beskytter data i transit ikke beskytter hvilende data. Det betyr at selv om
nettbutikker har en kryptert forbindelse til din nettleser (grønn hengelås) betyr
ikke det at kredittkortinformasjonen din lagres på en slik måte at den er
beskyttet. Krypteringssystemet som beskyttet kredittkortnummeret ditt på veien
til nettbutikken vil ikke lenger være til hjelp etter at det er kommet frem.

Hvilende data som er kryptert kan sendes fra en enhet til en annen uten at
man trenger å benytte de systemene som skal beskytte data i transit.

Denne guiden handler i stor grad om OpenPGP / GnuPG som et system for kryptering
av hvilende data. OpenPGP brukes i stor grad til kryptering av epost, samt digital
signering av programvare.
