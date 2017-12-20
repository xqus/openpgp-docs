+++
title = "Eliptiske kurver"
date =  2017-12-20T10:51:00+02:00
weight = 5
LastModifierDisplayName = "Audun Larsen"
LastModifierEmail = "audun@larsn.no"
+++

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
