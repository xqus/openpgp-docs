+++
date = "2017-02-22T10:59:58+01:00"
toc = true
weight = 1
title = "Grunnleggende kryptografi"

aliases = [
    "/kom-i-gang/konsepter",
    "/grunnleggende/kryptering/"
]

+++

### Symmetrisk kryptering
En symmetrisk krypteringsalgoritme benytter samme nøkkel både til kryptering og
dekryptering. To parter som kommuniserer med symmetrisk kryptering må bli enige
om nøkkelen på forhånd. Så snart de er enige krypterer senderen en melding med
nøkkelen og sender den til mottakeren. Mottakeren dekrypterer meldingen med den
samme nøkkelen. For eksempel brukte den Tyske Enigma maskien symmetrisk algoritme,
og nøklene ble distribuert som kodebøker. Hver dag ville en radiooperatør som
sendte eller mottok meldinger slå opp i kodeboken for å finne dagens nøkkel.
Moderne eksempler på symmetriske krypteringsalgoritmer er 3DES, Blowfish og IDEA.

En god krypteringsalgoritme legger all sikkerheten i nøklene og ingen i selve
algoritmen. Med andre ord skal det ikke være til hjelp for en angriper å vite
hvilken algoritme som benyttes. Bare hvis han vet nøkkelen er behovet for å vite
aloritmen viktig. Algoritmene som benyttes i OpenPGP har denne egenskapen.

Siden all sikkerheten er i nøkkelen er det svært viktig at det er veldig vanskelig
å gjette nøkkelen. Med andre ord må antall mulige nøkler være mange. På engelsk
kalles antall mulig nøkler *key space*.

Britene brukte maskiner til å gjette nøkler under 2. verdenskrig. Den Tyske
Enigma maskinen hadde mange mulige nøkler, men britene bygget spesialiserte maskiner
som gjettet seg frem til dagen nøkkel ved å prøve alle muligheter. Det betyr at
noen dager fant de dagens nøkkel etter få timer mens andre dager fant de aldri
riktig nøkkel.

Dagens datamaskiner kan gjette nøkler utrolig hurtig, og det er derfor nøkkellengde
er viktig i moderne kryptosystemer. Krypteringsalgoritmen DES bruker en 56-bit nøkkel,
som betyr at det er 2<sup>56</sup> mulige nøkler. 2<sup>56</sup> er 72 057 594 037 927 936
nøkler. Dette er veldig mange nøkler, men en vanlig datamaskin kan prøve alle
mulige nøkler i løpet av noen dager. En spesielisert datamaskin kan prøve de i
løpet av timer. På en annen side nye algoritmer slik som 3DES, Blowfish og IDEA
bruker 128-bit nøkler som betyr at det er 2<sup>128</sup> mulige nøkler.
Dette er mange, mange, mange fler nøkler og selv om alle datamaskinene på
planeten sammarbeidet ville de aldri klart å gjette seg frem til riktig nøkkel.

### Offentlig-nøkkel kryptering
Hovedproblemet med symmertrisk kryptering er ikke sikkerheten men utvekslingen
av nøkler. Når sender og mottaker har utvekslet nøkler, så kan denne nøkkelen
benyttes til å kommunisere sikkert. Men hvilken sikker kommunikasjonskanal ble
benyttet for å utveksle nøkkelen. I virkeligeten vil det nok ofte være lettere
for en angriper å snappe opp nøkkelen i steden for å gjette seg frem til riktig
nøkkel.

Offentlig-nøkkel kryptering ble funnet opp for å unngå hele nøkkelutvekslings-problemet.
Offentlig-nøkkel kryptering benytter et par med nøkler for å sende meldinger.
Begge nøklene tilhører personen som mottar meldingen. En nøkkel er den *offentlige nøkkelen*
og kan deles med hvem som helst. Den andre nøkkelen er en *privat nøkkel* og
holdes hemmelig av eieren. En sender krypterer en melding med den offentlige
nøkkelen og når den er kryptert kan den bare dekrypteres med den private nøkkelen.

Denne protokollen løser problemet med utveksling av nøkler som eksisterer med
symmetrisk kryptering. Det er ikke behov for sender og mottaker å bli enige
om en nøkkel på forhånd. Det eneste som kreves er at senderen av meldingen får
den offentlige nøkkelen til mottakeren på et tidspunkt før de skal kommunisere.
I tillegg kan den ene offentlige nøkkelen benyttes av alle som ønsker å kommunisere
med eieren.

Offentlig-nøkkel kryptering baserer seg på enveis falldør-funksjoner. En enveisfunksjon
er en funksjon som er lett å regne ut men vanskelig å reversere. For eksempel
er det lett å gange to primtall for å få et kompositt tall, men det er vanskelig
å faktorisere et kompositt-tall til sine primtallkomponenter. En enveis falldør
funksjon er lik, men den har en falldør. Det betyr at dersom en del av infomasjonen
er kjent så blir det lett å reversere funksjonen. For eksempe dersom du har et
tall som er faktoren av to primtall, så vil det å vite det ene primtallet gjøre
det lett å regne seg frem til det andre. Gitt att offentlig-nøkkel kryptering
baserer seg på primfaktorisering, den offentlige nøkkelen består av et kompositt-tall
som er faktoren av to primtall og krypteringsalgoritmen bruker dette tallet for
å kryptere meldingen. Algoritmen for å dekryptere meldingen krever at du vet begge
primtallene så det å dekryptere er enkelt hvis du har den private nøkkelen som
inneholder ett av primtallene men veldig vanskelig dersom du ikke har den.

Som med gode symmetriske algoritmer så ligger all sikkerheten til offentlig-nøkkel
algoritmer i nøkkelen. Derfor er nøkkelelngde en måleenhet for systemets sikkerhet.
Men du kan ikke sammenligne størrelsen på nøkkelene til en symmetrisk algoritme
og en offentlig-nøkkel algoritme for å sammenligne sikkerheten til de to algoritmene.
I et *brute-force* angrep på en symmetrisk algoritme med en nøkkellengde på 80 bit, må
angriperen forsøke opp til 2<sup>80</sup> nøkler for å finne den riktige nøkkelen.
I et *brute-force* angrep på en offentlig-nøkkel algoritme med en nøkkelstørrelse på
512 bit må angriperen faktorisere et kompositt-tall kodet i 512 bit (opp til 155 desimaltall).
Arbeidsmengen til en angriper er fundamentalt anderledes avhengig av hvilken type
algoritme han angriper. Mens 256 bit er tilstrekkelig for symmetrisk algoritmer,
gitt dagens faktoriserings-teknologi offenlitge nøkler med 2048 bits er anbefalt
for de fleste tilfeller.

### Hybride-systemer
Offentlig-nøkkel algoritmer er ingen perfekt løsning. Menage symmetriske algoritmer
er sterkere fra et sikkerhetsstandpunkt., og offentlig-nøkkel kryptering og
dekryptering er mer krevende enn de tilsvarende operasjonene i en symmetrisk
algoritme. Offentlig-nøkkel algoritmer er derimot et effektivt verktøy for å
distribuere symmetriske krypteringsnøkler, og det er slik de benyttes i hybride
systemer.

Et hybrid-system benytter både en symmetrisk algoritme og en offentlig-nøkkel
algoritme. Det virker slik at det benytter en offentlig-nøkkel algoritme for å
utveksle en nøkkel som brukes for den symmetriske algoritmen. Den faktiske
maldingen er kryptert med en symmetrisk algoritme før den sendes til mottakeren.
Siden utveksling av den symmetriske nøkkelen er sikker, er denne nøkkelen
forskjellige for hver melding som sendes. Derfor kalles den ofte *sesjonsnøkkel*.

OpenPGP benytter hybride-systemer. Sesjonsnøkkelen, kryptert med den offentlige-
nøkkelen og meldingen som sendes, kryptert med sesjonsnøkkelen er automatisk
kobinert i en pakke. Mottakeren benytter sin private nøkkel for å dekryptere
sesjonsnøkkelen som deretter benyttes for å dekryptere selve meldingen.

Et hybrid-system er ikke sikere enn den svakeste algoritmen som benyttes. I OpenPGP
er muligens offentlig-nøkkel algoritmen den svakeste av de to. Heldigvis, hvis en
angriper klarer å dekryptere en sesjonsnøkkel vil den bare klare å dekryptere
en melding. Angriperen må så starte på nytt og dekryptere en sesjonsnøkkel til
for å klare å lese en annen melding.

## Digitale signaturer
En sjekksum er en kort kode som brukes til å sjekke integriteten av data, eller
den matematiske funksjonen av dataene, algoritmen, som genererer koden,
ofte kalt hash-funksjon.

Et dokuments digitale signatur er resultatet av en hash-funksjon av dokumentet.
For å være nytteig må en hash-funksjon ha to viktige egenskaper. For det første
bør det være vanskelig å finne to dokumenter som resulterer i samme sjekksum. I
tillegg bør det være vanskelig å gjennopprette det originale dokumentet ut fra en
sjekksum.

Ved å bruke en slik hash-funksjon et dokument kan signeres ved å produsere en
sjeksum, og denne er signaturen. En annen person kan sjekke signaturen ved å
kjøre dokumentet gjennom samme hash-funksjon og sammenligne sin sjekksum men den
som kom som signatur. Dersom de er like, er det nestne helt sikkert at dokumentene
er identiske.

Problemet er å benytte en hahs-funksjon uten å tillate at en angiper interferer
med signatur-kontrollen. Hvis dokumentet og signaturen er sendt ukryptert, så kan
en angriper modifere dokumentet og generere en ny signatur uten at mottaker
merker det. Dersom bare dokumentet er kryptert en angriper kan endre på signaturen
og gjøre slik at kontrollen av signaturen feiler.

En algiritme som virker er å benytte en offentlig-nøkkel algoritme får å kryptere
signaturen. Faktisk så krypteres sjekksummen med den private nøkkelen til personen
som signerer, og hvem som helst kan kontrollere signaturen ved å benytte den offentlige
signaturen. Det signerte dokumentet kan senes ved å benytte hvilken som helst
annen krypteringsalgoritme, eller det kan sendes ukryptert. Hvis dokumentet
modifiseres vil signaturkontrollen feile. *The Digital Signature Standard (DSA)*
er en offentlig-nøkkel algoritme som virker som akkurat beskrevet. DSA er en del
av OpenPGP standaren, men RSA kan også benyttes til digitale signaturer.

## Eliptiske kurver
Eliptiske kurver skal løse samme utfordring som tradisjonelle
offentlig-nøkkel algoritmer. Nemmelig å lage en ennveis falldør-funksjon.
Problemet med tradisjonelle offentlig-nøkkel algoritmer er at forholdet mellom
nøkkelstørrelse og sikkerhet ikke er lineært. Det betyr at en dobling i
nøkkelstørrelse ikke gir en dobling av sikkerheten, men tiden det tar for å
kryptere / dekryptere i beste fall dobles. Det betyr at på et eller annet
tidspunkt må vi gå over til en annen type falldør-funksjon.

Eliptiske kurver er spesielle kurver som kan gjennkjennes på sin symmetriske
utforming. Under er et eksempel på noen kurver. Kurvene som benyttes i
kryptering er mye mer komplekse, men disse eksemplene gjør det lett å se for seg
hvordan det virker.

![Eliptiske kurver](/images/ecc-lines.png)
Eksempel på eliptiske kurver fra [Wikipedia](https://en.wikipedia.org/wiki/Elliptic_curve>).

Eliptiske kurver har den egenskapen at dersom du trekker en ikke horisontal
linje fra et punkt *A* på kurven til et annet *B* gjennom punkt *C*. Så vil *C*
invertert være *A + B*. Denne egenskapen er det vi benytter i eliptisk krurve
kryptografi.

Meget forenklet kan det forklares slik: Vår private nøkkel er et tilfeldig valgt
tall *n* som vi ganger opp med et forhåndsbestemt punkt på kurven, *G* for å få
et annet punkt på kurven. Dette er vår offentlige nøkkel *K*.  *K = n * G*.
Dette er et eneklt regnestykke, men dersom du vet *K* og *G* og vil komme frem til
*n*, så er dette meget komplisert.

Ved å benytte eliptiske kurver i kryptografi kan man redusere nøkkellengden
betraktelig i forhold til tradisjonell kryptering. Det sies at en 256 bit ECC nøkkel
skal gi samme sikkerhet som en 3072 bit RSA nøkkel.
