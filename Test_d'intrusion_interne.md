---
title: Test d'intrusion interne
permalink: /Test_d'intrusion_interne/
---

# Test d'intrusion interne

Cette article présente une liste (non-exhaustive) de méthodologies et outils qui peuvent être utilisées dans des pentests internes. Ces méthodologies sont divisées en plusieurs catégories:

-   Reconnaissance: ensemble des éléments qui permettent d'avoir une première vue sur le réseau quand on arrive dessus. Ceci inclut des méthodes qui peuvent être appliquées sans compte et d'autres qui nécessitent un compte du domaine (généralement n'importe quel compte du domaine suffira).
-   Compromission "locale": ensemble de méthodologies qui visent à prendre le contrôle d'une application / d'un serveur / d'une BDD / etc. Il s'agit de méthodologies centrées autour d'attaques sur un élément unique sans forcément prendre en compte son intégration dans un environnement Active Directory
-   Déplacement latéral & élévation de privilèges: ensemble des méthodes qui permettent d'étendre son influence sur un domaine une fois qu'on compromis un élément.

Poste utilisateur
-----------------

**Note:** partie à revoir.

Cette section décrit les tests qui peuvent être effectués sur un poste utilisateur. Les points suivants concernent le chiffrement.

-   Poste sans chiffrement: récupérer le disque et lire / modifier son contenu. S'il n'y a pas non plus de protection de la séquence de boot on peut facilement lancer un support amovible pour faire ces modifications.
-   Poste avec chiffrement sans TPM: il est possible de bruteforcer le mot de passe Bitlocker (TODO)
-   Poste avec chiffrement & TPM: le TPM est utilisé pour déchiffrer le disque. Il n'est pas possible de faire des attaques "offlines".

Les points suivants concernent la protection de la séquence de boot:

-   Il est possible de modifier le bootloader pour y insérer un malware qui sauvegardera le mot de passe de déchiffrement par exemple.
-   Le mécanisme de "SecureBoot" permet de se protéger contre ces attaques car le Bootloader devra être signé.

Les grandes phases d'un test d'intrusion interne sont:

-   La phase de [reconnaissance](/Reconnaissance_(Interne) "wikilink") permettant de gagner une compréhension du réseau
-   La phase de **compromission initiale** qui consiste à gagner un accès à un serveur / machine
-   La phase de [déplacement latéral](/déplacement_latéral "wikilink") et d'élévation de priviléges avec l'objectif global de devenir DA ou équivalent
-   La phase de **looting** où on récupére des preuves / éléments intéressants dans le but de montrer l'impact

Arrivée initiale
----------------

Protocoles présents:

-   LLMNR / Netbios-NS: Responder
-   Connection SMB sur la machine auditeur: SMBRelay

A l'attribution d'une adresse IP:

-   Adresse du serveur DNS / DHCP
-   Adresse du LAN local

Attaques de type man in the middle:

-   Cibler un utilisateur pour faire un arpspoof (ceci permet de découvrir des plages avec lesquelles les utilisateurs intéragissent)
-   Responder (en faisant attention à l'existence d'un wpad)

Scans de découverte réseau:

-   Scans sur les LAN identifiés

``` bash
nmap -sS -sV -A -F 192.168.199.0/24 -oA scan_nmap_192.168.199.0_24
```

-   Scans en "aveugle" (nmap ou masscan)

``` bash
nmap sP 192.168.160.0/24
```

Compromission initiale
----------------------

L'objectif de cette partie est de trouver et d'exploiter une vulnérabilité qui va nous permettre d'étendre notre contrôle sur le réseau. De très nombreuses possibilités existent.

### Attaques de type MiTM

Les attaque de type "Man in the middle" consistent en l'ensemble des attaques dans lesquelles l'attaquant va forcer les machines des utilisateurs à se connecter à sa machine. Le but peut être de juste observer le traffic (e.g. Passive credentials gathering), de le modifier (e.g. SMBRelay), ou de se faire passer pour un service légitime.

-   Sniffing de mot de passe
-   Sniffing de challenge NTLM
-   LLMNR/NetBios-NS Spoofing avec Responder
-   SMBRelay

-   Applications Web
-   [Microsoft SQL Server](/Microsoft_SQL_Server "wikilink")
    - Il est possible d'utiliser les SPN pour identifier des serveurs SQL !
    - Mots de passe par défaut / faibles / comptes du domaine
    - Avec un compte SQL:
        - Si admin: execution de code avec xp_cmdshell
        - Si non admin: SMB Relay / Hash avec xp_dirtree / xp_filexist ou élévation de priviléges

Avec un compte du domaine:

-   Mots de passe dans SYSVOL ([Group Policy Preferences](/Group_Policy_Preferences "wikilink"))
-   Trouver des partages réseaux via des scans ([nmap](/nmap "wikilink"), [metasploit](/metasploit "wikilink"), [CrackMapExec](/CrackMapExec "wikilink"), [ShareCheck](http://www.sec-1.com/blog/2014/sharecheck)) ou via l'interrogation de l'[Active Directory](/Active_Directory "wikilink")
-   Attaques liées à [Kerberos](/Kerberos "wikilink") (ex: [Kerberoasting](/Kerberoasting "wikilink"))
-   Attaques sur le DC
    -   MS14-068 (Elévation de privilèges d'utilisateur à Domain Admin)

### Mot de passe triviaux

Il peut être intéressant de prendre le contrôle d'un élément en identifiant des mots de passes par défaut.

### Local Privilege Escalation

Dans certains cas on aura un accès limité au serveur compromis. Ceci est notamment le cas lorsqu'on a compromis un service qui tournait avec un utilisateur aux droits limités.

- [Elévation de priviléges (Windows)](/Elévation_de_priviléges_(Windows) "wikilink")
- [Elevation de priviléges (Linux)](/Elevation_de_priviléges_(Linux) "wikilink")

## Déplacement latéral

Voir l'article [Déplacement latéral](/Déplacement_latéral "wikilink").

## Domain Admin

Avec les priviléges d'administrateurs du domaine il est généralement intéressant de montrer l'impact possible de tels priviléges:

-   Récupérer des fichiers sensibles dans les partages réseaux
-   Dumper les hashs du domaine

## Divers

Cette section regroup divers éléments sur des sujets trop précis pour faire l'object d'un article à part:

- [Abusing DNSAdmins privilege for escalation in Active Directory](http://www.labofapenetrationtester.com/2017/05/abusing-dnsadmins-privilege-for-escalation-in-active-directory.html): cet article décrit une méthode permettant de devenir administrrrateur du domaine avec un compte administrateur du DNS.
- [Week of Evading Microsoft ATA](http://www.labofapenetrationtester.com/2017/08/week-of-evading-microsoft-ata-day2.html): différentes méthodes pour contourner Microsoft ATA

## Ressources

-   [Présentation d'ADSecurity](https://adsecurity.org/?page_id=1352)
-   [Attack Methods for Gaining Domain Admin Rights in Active Directory](https://adsecurity.org/?p=2362)

### Vidéos

-   [Derbycon 2016 - Attacking EvilCorp Anatomy of a Corporate Hack](https://www.youtube.com/watch?v=nJSMJyRNvlM)
-   [Derbycon 2014 - Passing the Torch Old School Red Teaming New School Tactics David McGuire and Will Schroeder](https://www.youtube.com/watch?v=rpwrKhgMd7E): présente les anciennes et nouvelles méthodes pour faire des pentest internes.


