---
title: Imprimantes
permalink: /Imprimantes/
---

# Imprimantes

## Fonctionnalités classiques

- Scan vers fichier: accès FTP ou SMB sur des serveurs
- Scan vers e-mail: accès SMTP
- Notification par e-mail: accès SMTP
- Intégration LDAP
- Logs systèmes
- Backups

## Attaques

Gagner un accès:
- Identifiants par défauts
- Bypass du cloisonnement

Après avoir eu un accès:
- Accès aux informations (LDAP, identifiants, etc.)
- "Passback" attaque
- Fonctionnalités de backup, etc.

## Checklist

Voir [Printer Security Testing Cheat Sheet](http://hacking-printers.net/wiki/index.php/Printer_Security_Testing_Cheat_Sheet)

- Identification des imprimantes: scanner les port 9091, 515, 631 et souvent 21, 23, 80, 443.
- Service SNMP: ```snmpwalk -v1 -c public $ip```

## Références
- [From Printer To Pwnd: Leveraging Multifunction Printers During Penetration Testing](https://www.youtube.com/watch?v=bAgMUXtxNa8)
- [Run PJL Commands From A Shell Script](https://jacobsalmela.com/2017/01/10/run-pjl-commands-from-a-shell-script/)
- [Hacking Network Printers](https://www.irongeek.com/i.php?page=security/networkprinterhacking)
- [Hacking Printer Wiki](http://hacking-printers.net/wiki/index.php/Main_Page)
- [An Introduction to Printer Exploitation #1](https://0x00sec.org/t/an-introduction-to-printer-exploitation-1/3565)
