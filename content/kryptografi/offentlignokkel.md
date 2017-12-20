+++
title = "Offentlig-nøkkel kryptering"
date =  2017-12-20T10:46:00+02:00
weight = 2
LastModifierDisplayName = "Audun Larsen"
LastModifierEmail = "audun@larsn.no"
+++

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
