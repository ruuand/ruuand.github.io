---
title: Active Directory
permalink: /Active_Directory/
---

# Active Directory

Active Directory est un des éléments centraux d'un environnement Windows. Le site <https://adsecurity.org/> est une référence à consulter.

Points à étudier
----------------

-   AdminSDHolder: <https://adsecurity.org/?p=1906>
-   adminCount
-   RestrictedAdmin: <https://blogs.technet.microsoft.com/kfalde/2013/08/14/restricted-admin-mode-for-rdp-in-windows-8-1-2012-r2/>
-   Sites AD: <https://technet.microsoft.com/en-us/library/cc754697(v=ws.11).aspx>
-   Managed Services Accounts

Authentification AD
-------------------

Il existe plusieurs mécanismes d'authentification dans Active Directory:

-   [Authentification Lan Manager](/Lan_Manager/)
-   [Authentification Kerberos](/Kerberos/")

### Authentification par carte à puce

Voir Annexe VII du guide ANSSI: <https://www.ssi.gouv.fr/uploads/IMG/pdf/NP_ActiveDirectory_NoteTech.pdf>

### Stockage de mot de passes

-   NTDIS.DIT: hashs des mots de passe des utilisateurs du domaine.
-   Base SAM: hashs des mots de passe des utilisateurs locaux.
-   Processus LSASS: hashs de mot de passe, tickets Kerberos, mots de passe en clair.

### Hashs dans le cache

Par défaut les hashs des mots de passe des utilisateurs du domaine sont conservés en cache. Ceci permet de se connecter même lorsque l'ordinateur n'est plus lié au domaine. Cependant ceci ne sert à rien dans le cas de serveur. Le nombre de credentials gardé en cache est contrôlé par une clé de registre:

``` text
   HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\Current Version\Winlogon\

   ValueName: CachedLogonsCount
   Data Type: REG_SZ
   Values: 0 - 50
```

Source: <https://support.microsoft.com/en-us/kb/172931>

Groupes AD
----------

La page suivante donne des informations sur les principaux groupes Active Directory: <https://blogs.technet.microsoft.com/lrobins/2011/06/23/admin-free-active-directory-and-windows-part-1-understanding-privileged-groups-in-ad/>

Les 4 groupes les plus sensibles sont:

-   Enterprise Admins: existe à la racine d'une forêt. Ils sont administrateurs de l'ensemble des domaines de la forêt et peuvent effectuer des modifications sur l'ensemble de celle-ci.
-   Domain Admins: peuvent administrer un domaine et l'ensemble des serveurs / postes de travails liés à celui-ci.
-   Administrators: peuvent administrer un domaine mais n'ont pas de privilèges particuliers sur les postes de travails & serveurs.
-   Schema Admins: existe seulement à la racine d'une forêt. Le groupe est destiné à n'être utilisé que quand des modifications du schéma de la forêt sont effectués.

Il est à noter que les privilèges qu'ont les membres de ces groupes font qu'ils peuvent généralement s'attribuer les priviléges pour aller dans n'importe quel autre groupe.

Ressources
----------

-   [Attack Methods for Gaining Domain Admin Rights in Active Directory](https://adsecurity.org/?p=2362)
-   [Red vs Blue Modern Active Directory Attacks Defense - Sean Metcalf](https://www.youtube.com/watch?v=Lz6haohGAMc&feature=youtu.be)
