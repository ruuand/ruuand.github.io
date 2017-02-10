---
title: Kerberoasting
permalink: /Kerberoasting/
---

L'attaque Kerberoasting consiste à récupérer des TGS associés à un utilisateur du domaine et à essayer des les cracker.

Méthodologie
------------

Les étapes de cette attaque sont:

1.  Lister les **Service Principal Names (SPNs)**. Un SPN est de la forme suivante TERMSRV/DC1 (où TERMSRV est le type de service et DC1 est le serveur où le service est actif).
2.  Faire des requêtes pour récupérer les tickets Kerberos.
3.  Exporter les tickets pour les manipuler
4.  Convertir les tickets en un format manipulable par JtR ou Hashcat.
5.  Casser les hashs avec hashcat/JtR

Pratique
--------

La suite Powersploit permet de récupérer la liste des utilisateurs qui on un SPN associé:

``` powershell
Get-NetUser -Domain blabla.local -DomainController XX.XX.XX.XX -Verbose -SPN
```

Il est possible de récupérer les parties à cracker avec [Impacket](/Impacket "wikilink") et l'outil **GetUsersSPN.py**
``` python
GetUserSPNs.py -dc-ip 192.168.1.1 -request domain.local/validaccount
```

Correction
----------

Il est difficile de bloquer Kerberoasting qui utilise le fonctionnement normal de Kerberos. On peut cependant essayer de détecter une attaque en cours:
- [Detecting Kerberoasting Activity](https://adsecurity.org/?p=3458)
- [Detecting Kerberoasting Activity Part 2 – Creating a Kerberoast Service Account Honeypot](https://adsecurity.org/?p=3513)


Ressources
----------

-   Kerberoasting - Room326:
    -   [Partie 1](https://room362.com/post/2016/kerberoast-pt1/)
    -   [Partie 2](https://room362.com/post/2016/kerberoast-pt2/)
    -   [Partie 3](https://room362.com/post/2016/kerberoast-pt3/)
-   [t120 Attacking Microsoft Kerberos Kicking the Guard Dog of Hades Tim Medin](https://www.youtube.com/watch?v=PUyhlN-E5MU)
-   [Cracking Kerberos TGS Tickets Using Kerberoast – Exploiting Kerberos to Compromise the Active Directory Domain](https://adsecurity.org/?p=2293)
-   [Kerberoasting Without Mimikatz - Harmj0y](http://www.harmj0y.net/blog/powershell/kerberoasting-without-mimikatz/)

[Category:Méthodologies](/Category:Méthodologies "wikilink") [Category:Active Directory](/Category:Active_Directory "wikilink")
