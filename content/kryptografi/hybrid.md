+++
title = "Hybride systemer"
date =  2017-12-20T10:48:00+02:00
weight = 3
LastModifierDisplayName = "Audun Larsen"
LastModifierEmail = "audun@larsn.no"
+++

Offentlig-nøkkel algoritmer er ingen perfekt løsning. Mange symmetriske algoritmer
er sterkere fra et sikkerhetsstandpunkt, og offentlig-nøkkel kryptering og
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
