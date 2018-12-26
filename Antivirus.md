---
title: Antivirus
permalink: /Antivirus/
---

# Antivirus

Les Antivirus peuvent souvent être utilisés pour élever ses privilèges sur un serveur / machine. Quelques trucs utiles:

- Avec droits admins: checker avec mimikatz si des creds sont en mémoire, notamment quand on lance un update de l'AV
- Sans droits admins: la même chose mais en interceptant un éventuel challenge / response vers un serveur de mise à jour (déjà vu sur Sophos)

### Windows Defender

Désactiver les scans real time en ligne de commande:

``` powershell
Set-MpPreference -DisableRealtimeMonitoring $true
```

## Références

- [GreHack 2018: Abusing Privileged File Manipulation - Clement Lavoillotte](https://www.youtube.com/watch?v=OfPTkx36EWs)

### AMSI
- [How to bypass AMSI and execute ANY malicious Powershell code](https://0x00-0x00.github.io/research/2018/10/28/How-to-bypass-AMSI-and-Execute-ANY-malicious-powershell-code.html)

### Symantec

-   [From Read to Domain Admin – Abusing Symantec Backup Exec with Frida](https://blog.silentsignal.eu/2014/02/27/from-read-to-domain-admin-abusing-symantec-backup-exec-with-frida/)

### McAfee

- [McAfee privileged SiteList.xml leads to Active Directory domain privilege escalation (@tfairane)](https://github.com/tfairane/HackStory/blob/8aadea725c1572a19a3959184fc0dd8f591510e4/McAfeePrivesc.md)
- [McAfee SiteList.xml password decryption](https://funoverip.net/2016/02/mcafee-sitelist-xml-password-decryption/)

### Sophos

- [User accounts required by Sophos Enterprise Console](https://community.sophos.com/kb/en-us/113954)
- [Sophos Anti-Virus updater password decoder](https://github.com/aurainfosec/sophos-pw-decoder)
