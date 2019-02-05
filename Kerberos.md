---
title: Kerberos
permalink: /Kerberos/
---

# Kerberos

Kerberos est un protocole d'authentification utilisé dans les domaines Windows.

## Présentation

Kerberos est un protocole d'authentification dans les domaines Windows. Il repose principalement sur un système de "tickets" et du chiffrement symétrique utilisant notamment les hashs des utilisateurs (**Note:** connaître le hash d'un utilisateur permet de générer des tickets Kerberos pour celui-ci).

Le mécanisme Kerberos repose sur 4 tiers:

-   Le **client** (ex: un utilisateur du domaine)
-   Le **serveur de ressources** (ex: un partage réseau, un serveur SQL, etc.)
-   Le **Key Distribution Center** (KDC)
    -   L'**Authentication Server** (AS)
    -   Le **Ticket Granting Service** (TGS)

Le principe est le suivant :

-   Tous les utilisateurs vont utiliser leur hash NT pour effectuer des opérations permettant de s'authentifier auprès du KDC
-   Le client demande un **Ticket Granting Ticket** (TGT) au KDC. Ce TGT sera valable pour une durée de 10 heures (renouvelable pour une durée maximale de 7 jours):
    -   (Client) - **PREAUTH** est calculé par le client basé sur le chiffrement d'un timestamp avec le hash NT. Si un écart trop grand de temps est identifié entre le KDC et la machine utilisateur est identifié, un erreur sera renvoyée (KRB_AP_ERR_SKEW)
    -   (Client -> KDC) - **AS-REQ** contenant le **PREAUTH** afin de faire une demande pour un TGT.
    -   (KDC -> Client) - **AS-REP** contenant le **Privileged Attribute Certificate** (PAC) qui détaille les groupes de sécurité dont l'utilisateur est membre. Cette partie est chiffrée avec la clé du compte krbtgt et seul le KDC pourra donc le déchiffrer. **L'AS-REP contient également une partie chiffrée avec la clé du client et qui va permettre de communiquer pour récupérer les TGS**. Cette partie chiffrée avec la clé de l'utilisateur explique la nécessite de la pré authentification. Sans ce mécanisme, un attaquant pourrait récupérer des *AS-REP* pour n'importe quel utilisateur et faire du brute force offline.
-   Le client demande ensuite un **Ticket Granting Service** (TGS) au KDC. Ce TGS permettra d'accéder à un service spécifique:
    -   (Client -> KDC) - Le client fournit son TGT au KDC et indique le service auquel il veut accéder grâce à son **Service Principal Name** (SPN)
    -   (KDC) - Le client valide le TGT grâce à sa signature et construit le TGS qui contient une partie chiffrée par krbtgt et une partie chiffrée avec la clé du service (cette partie contient notamment les informations d'appartenance à des groupes)
-   L'utilisateur accéde finalement au service ciblé en lui présentant son TGS. Celui-ci est validé grâce à la clé du service (connue du service et du KDC) et ensuite la validation basée sur les groupes est effectuée.

## Délégation Kerberos
Voir les articles suivants:
- [Kerberos Unconstrained Delegation (or How Compromise of a Single Server Can Compromise the Domain)](https://adsecurity.org/?p=1667)
- [Kerberos Delegation, SPNs and More...](https://www.coresecurity.com/blog/kerberos-delegation-spns-and-more)
- [Trust? Years to earn, seconds to break](https://labs.mwrinfosecurity.com/blog/trust-years-to-earn-seconds-to-break/)
- [Delegate to the Top: Abusing Kerberos for arbitrary impersonations and RCE](https://www.blackhat.com/docs/asia-17/materials/asia-17-Hart-Delegate-To-The-Top-Abusing-Kerberos-For-Arbitrary-Impersonations-And-RCE-wp.pdf)


## Chiffrement
Les tickets Kerberos contiennent une partie chiffrée qui peut être chiffrée avec RC4, AES128, AE256. Dans le cas d'AES il est difficile d'envisager une attaque [Kerberoasting](/Kerberoasting/).

La décision du protocole de chiffrement utilisée semble reposer entièrement sur le Contrôleur de domaine. RC4 est systématiquement utilisé dans les cas suivants (basé sur le talk [Return From The Underworld The Future Of Red Team Kerberos](https://www.youtube.com/watch?v=E_BNhuGmJwM)) :
- Le DC est sous W2003 ou antérieur (AES n'était pas supporté)
- La machine est sous W2003/XP ou antérieur (ceci concerne les comptes machines)
- La machine n'est pas jointe au domaine (il y a une entrée pour une machine dans l'AD. Ceci peut à priori correspondre à des comptes pour des machines Linux)
- Comportement par défaut pour un compte utilisateur ayant un SPN.

En revanche AES sera utilisé dans le cas suivant:
- La machine est sous W2008 ou supérieur et le DC est supérieur à W2008 (ceci concerne les comptes machines)
- Le compte utilisateur a l'option "The account supports Kerberos AES 128/256". Cependant ceci empêchera Kerberos de fonctionner correctement si le compte machine est utilisé sous un W2003, XP (qui ne supportent pas AES). Plus d'informations sur le [site de Microsoft](https://blogs.msdn.microsoft.com/openspecification/2011/05/30/windows-configurations-for-kerberos-supported-encryption-type/).
    
## Attaques possibles

### Attaques génériques

-   [Kerberoasting](/Kerberoasting "wikilink"): méthodologie pour récupérer des hashs utilisés par Kerberos pour les services et essayer de casser ceux-ci. Cette attaque se base sur l'utilisation du hash d'un service pour chiffrer les TGS.
-   [Attaque sur AS-REP](http://www.harmj0y.net/blog/activedirectory/roasting-as-reps/): Cette attaque cible les comptes pour lesquels la pré authentification (la partie **PREAUTH**) est désactivé.
-   [Silver Ticket](/Silver_Ticket "wikilink"): forger un TGS
-   [Golden Ticket](/Golden_Ticket "wikilink"): forger un TGT
-   [Pass The Hash](/https://malicious.link/post/2018/pass-the-hash-with-kerberos/): il est possible de faire une attaque de type pass the hash via Kerberos
-   Il est possible de faire des attaques de type Man in the Middle sur le protocole Kerberos. On peut ensuite faire du cracking offline avec hashcat.

### Attaques spécifiques

-   [MS14-068](/MS14-068 "wikilink"): uniquement sur un DC vulnérable. Ceci permet de passer de Domain User à Domain Admin.
-   [Diamond PAC](/Diamond_PAC "wikilink"): attaque combinant MS14-068 et un Golden Ticket
-   [Skeleton Key](/Skeleton_Key "wikilink"): malware patchant LSASS sur un DC. Ce malware permet de créer une **skeleton key** qui permet de se logger à n'importe quel compte du domaine.

## Ressources

-   [Active Directory](/Active_Directory "wikilink")
-   [Explain Like I'm 5: Kerberos](http://www.roguelynn.com/words/explain-like-im-5-kerberos/)
-   [What Is Kerberos Authentication? - Microsoft Technet](https://technet.microsoft.com/en-us/library/cc780469(v=ws.10).aspx)
-   [Kerberos, Active Directory’s Secret Decoder Ring](http://adsecurity.org/?p=227)
-   [Return From The Underworld The Future Of Red Team Kerberos](https://www.youtube.com/watch?v=E_BNhuGmJwM)
-   [Kerberos en Active Directory](https://beta.hackndo.com/kerberos/)
