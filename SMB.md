---
title: SMB
permalink: /SMB/
---

# SMB

Enumération
-----------

Il est possible de se connecter à un service SMB avec l'outil [smbclient](/smbclient "wikilink"):

``` bash
smbclient -L 192.168.31.201 -U administrator --no-pass
```

La commande suivante permet d'accéder au partage *Share*

``` bash
smbclient //192.168.31.201/Share -U administrator --no-pass
```

L'outil [enum4linux](/enum4linux "wikilink") permet de rassembler des informations à partir de services SMB:

``` bash
enum4linux 192.168.31.222
```

La commande suivante checker les vulnérabilités SMB pouvant mener à une RCE:

``` bash
nmap -p 445 192.168.31.201 --script smb-vuln-ms06-025,smb-vuln-ms08-067 -oA nmap_192.168.31.201_smb_vuln
nmap -p U:137,T:139 192.168.31.201 --script smb-vuln-ms06-025,smb-vuln-ms08-067 -oA nmap_192.168.31.201_smb_vuln
```

Exploitation
------------

Les attaques suivantes sont possibles:

-   Attaque [SMB Relay](/SMB_Relay "wikilink")

Resources
---------

### Liens externes

-   [Nice tutorial](https://www.ethicalhacker.net/features/root/tutorial-fun-with-smb-on-the-command-line)
-   [SANS Article](https://pen-testing.sans.org/blog/2013/07/24/plundering-windows-account-info-via-authenticated-smb-sessions)
-   [Article from iodigicatlsec](http://www.iodigitalsec.com/windows-null-session-enumeration/)
-   [Article from Carnal0wnage](http://carnal0wnage.attackresearch.com/2010/06/more-with-rpcclient.html)


