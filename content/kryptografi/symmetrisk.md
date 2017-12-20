+++
date = "2017-02-22T10:59:58+01:00"
toc = true
weight = 1
title = "Symmetrisk kryptering"

aliases = [
    "/kom-i-gang/konsepter",
    "/grunnleggende/kryptering/",
    "/kryptografi/grunnleggende/"
]

+++

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
