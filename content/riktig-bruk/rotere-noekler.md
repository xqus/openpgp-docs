+++
weight = 3
title = "Rotere undernøkler"
date = "2017-02-22T12:31:51+01:00"
toc = true
#next = "/riktig-bruk7rotere-noekler"
prev = "/riktig-bruk/sikre-noekler"

+++

{{% notice note %}}
Dette kapittelet forutsetter at du har et offline nøkkelpar som beskrevet i kapittelet om *Sikker oppbevaring av nøkler*.
{{% /notice %}}

Dersom dine undernøkler går tapt eller komprimiteres kan du enkelt tilbakekalle
disse, og generere nye ved å bruke din minnepinne med Tails som har dine hovednøkler på.
Når vi tilbakekaller nøklene sier vi til omverden av disse ikke lenger skal benyttes.
Dersom noen signerer en melding med nøkler som er tilbakekalt vi ikke signaturen
være gyldig.  Deretter gernerer vi nye undernøkler som vi kopierer tilbake på
klientene våre, som beskrevet i kapittelet om *Sikker oppbevaring av nøkler*.

Det er viktig at din nye offentlige nøkkel lastes opp til nøkkelserverene. Det
er slik omverden får vite om dine nye undernøkler, og at de gamle er tilbakekalt.

Tilbakekall dine gamle nøkler
-----------------------------

    amnesia@amnesia:~$ gpg2 --edit-key alice@example.com
    gpg (GnuPG) 2.0.26; Copyright (C) 2013 Free Software Foundation, Inc.
    This is free software: you are free to change and redistribute it.
    There is NO WARRANTY, to the extent permitted by law.

    Secret key is available.

    pub  2048R/0x50AD20916F557D14  created: 2017-02-20  expires: 2018-02-20  usage: SC
                                   trust: ultimate      validity: ultimate
    sub  2048R/0x94B56B273C610BDB  created: 2017-02-20  expires: 2018-02-20  usage: S
    sub  2048R/0xE69C73D0FFA0432F  created: 2017-02-20  expires: 2018-02-20  usage: E
    [ultimate] (1). Alice <alice@example.com>

    gpg> key 1

    pub  2048R/0x50AD20916F557D14  created: 2017-02-20  expires: 2018-02-20  usage: SC
                                   trust: ultimate      validity: ultimate
    sub* 2048R/0x94B56B273C610BDB  created: 2017-02-20  expires: 2018-02-20  usage: S
    sub  2048R/0xE69C73D0FFA0432F  created: 2017-02-20  expires: 2018-02-20  usage: E
    [ultimate] (1). Alice <alice@example.com>

    gpg> key 2

    pub  2048R/0x50AD20916F557D14  created: 2017-02-20  expires: 2018-02-20  usage: SC
                                   trust: ultimate      validity: ultimate
    sub* 2048R/0x94B56B273C610BDB  created: 2017-02-20  expires: 2018-02-20  usage: S
    sub* 2048R/0xE69C73D0FFA0432F  created: 2017-02-20  expires: 2018-02-20  usage: E
    [ultimate] (1). Alice <alice@example.com>

    gpg> revkey
    Do you really want to revoke the selected subkeys? (y/N) y
    Please select the reason for the revocation:
      0 = No reason specified
      1 = Key has been compromised
      2 = Key is superseded
      3 = Key is no longer used
      Q = Cancel
    Your decision? 1
    Enter an optional description; end it with an empty line:
    >
    Reason for revocation: Key has been compromised
    (No description given)
    Is this okay? (y/N) y

    You need a passphrase to unlock the secret key for
    user: "Alice <alice@example.com>"
    2048-bit RSA key, ID 0x50AD20916F557D14, created 2017-02-20


    You need a passphrase to unlock the secret key for
    user: "Alice <alice@example.com>"
    2048-bit RSA key, ID 0x50AD20916F557D14, created 2017-02-20


    pub  2048R/0x50AD20916F557D14  created: 2017-02-20  expires: 2018-02-20  usage: SC
                                   trust: ultimate      validity: ultimate
    The following key was revoked on 2017-02-20 by RSA key 0x50AD20916F557D14 Alice <alice@example.com>
    sub  2048R/0x94B56B273C610BDB  created: 2017-02-20  revoked: 2017-02-20  usage: S
    The following key was revoked on 2017-02-20 by RSA key 0x50AD20916F557D14 Alice <alice@example.com>
    sub  2048R/0xE69C73D0FFA0432F  created: 2017-02-20  revoked: 2017-02-20  usage: E
    [ultimate] (1). Alice <alice@example.com>

    gpg> save

Generer nye undernøkler
-----------------------

    amnesia@amnesia:~$ gpg2 --edit-key alice@example.com
    gpg (GnuPG) 2.0.26; Copyright (C) 2013 Free Software Foundation, Inc.
    This is free software: you are free to change and redistribute it.
    There is NO WARRANTY, to the extent permitted by law.

    Secret key is available.

    pub  2048R/0x50AD20916F557D14  created: 2017-02-20  expires: 2018-02-20  usage: SC
                                   trust: ultimate      validity: ultimate
    The following key was revoked on 2017-02-20 by RSA key 0x50AD20916F557D14 Alice <alice@example.com>
    sub  2048R/0x94B56B273C610BDB  created: 2017-02-20  revoked: 2017-02-20  usage: S
    The following key was revoked on 2017-02-20 by RSA key 0x50AD20916F557D14 Alice <alice@example.com>
    sub  2048R/0xE69C73D0FFA0432F  created: 2017-02-20  revoked: 2017-02-20  usage: E
    [ultimate] (1). Alice <alice@example.com>

    gpg> addkey
    Key is protected.

    You need a passphrase to unlock the secret key for
    user: "Alice <alice@example.com>"
    2048-bit RSA key, ID 0x50AD20916F557D14, created 2017-02-20

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
    Key expires at Tue 20 Feb 2018 07:45:00 PM UTC
    Is this correct? (y/N) y
    Really create? (y/N) y
    We need to generate a lot of random bytes. It is a good idea to perform
    some other action (type on the keyboard, move the mouse, utilize the
    disks) during the prime generation; this gives the random number
    generator a better chance to gain enough entropy.

    pub  2048R/0x50AD20916F557D14  created: 2017-02-20  expires: 2018-02-20  usage: SC
                                   trust: ultimate      validity: ultimate
    The following key was revoked on 2017-02-20 by RSA key 0x50AD20916F557D14 Alice <alice@example.com>
    sub  2048R/0x94B56B273C610BDB  created: 2017-02-20  revoked: 2017-02-20  usage: S
    The following key was revoked on 2017-02-20 by RSA key 0x50AD20916F557D14 Alice <alice@example.com>
    sub  2048R/0xE69C73D0FFA0432F  created: 2017-02-20  revoked: 2017-02-20  usage: E
    sub  2048R/0x8EE8D15759878C5A  created: 2017-02-20  expires: 2018-02-20  usage: S
    [ultimate] (1). Alice <alice@example.com>

    gpg> addkey
    Key is protected.

    You need a passphrase to unlock the secret key for
    user: "Alice <alice@example.com>"
    2048-bit RSA key, ID 0x50AD20916F557D14, created 2017-02-20

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
    Key expires at Tue 20 Feb 2018 07:45:11 PM UTC
    Is this correct? (y/N) y
    Really create? (y/N) y
    We need to generate a lot of random bytes. It is a good idea to perform
    some other action (type on the keyboard, move the mouse, utilize the
    disks) during the prime generation; this gives the random number
    generator a better chance to gain enough entropy.

    pub  2048R/0x50AD20916F557D14  created: 2017-02-20  expires: 2018-02-20  usage: SC
                                   trust: ultimate      validity: ultimate
    The following key was revoked on 2017-02-20 by RSA key 0x50AD20916F557D14 Alice <alice@example.com>
    sub  2048R/0x94B56B273C610BDB  created: 2017-02-20  revoked: 2017-02-20  usage: S
    The following key was revoked on 2017-02-20 by RSA key 0x50AD20916F557D14 Alice <alice@example.com>
    sub  2048R/0xE69C73D0FFA0432F  created: 2017-02-20  revoked: 2017-02-20  usage: E
    sub  2048R/0x8EE8D15759878C5A  created: 2017-02-20  expires: 2018-02-20  usage: S
    sub  2048R/0x737E8D0A5B17C472  created: 2017-02-20  expires: 2018-02-20  usage: E
    [ultimate] (1). Alice <alice@example.com>

    gpg> save

Oppdater nøkkelserverene
-------------------------

    amnesia@amnesia:~$ gpg2 --send-keys 0x50AD20916F557D14
    gpg: sending key 0x50AD20916F557D14 to hkps server hkps.pool.sks-keyservers.net
