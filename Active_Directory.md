---
title: Active Directory
permalink: /Active_Directory/
---

# Active Directory

Active Directory est un des éléments centraux d'un environnement Windows. Le site <https://adsecurity.org/> est une référence à consulter. Cette page est un index 

- Authentification
  - [Kerberos](/Kerberos/)
  - [MsCacheV2](/MsCacheV2/)
	- [NTLM & NetNTLM](/NTLM/)

- Attaques
  - [Kerberoasting](/Kerberoasting/)
  - [Pass the hash](/Pass_The_Hash/)
	- [Dump des hashs du domaine](/Dump_des_hashs_du_domaine/)
	- [SMB Relay](/SMB_Relay/)
  
- Divers
	- [Group Policy Object](/Group_Policy_Object/)
	- [Just Enough Administration](/Just_Enough_Administration/)
	- [WMI](/WMI/)
	- [LLMNR](/LLMNR/)
	- [Trust Relationships](/Trust_Relationships/)
	- [Local Admin Password Solution](/LAPS/)
	- [Read Only Domain Controllers](/RODC/)
  - AdminSDHolder: objet AD qui contient les permissions à appliquer aux groupes administratifs. Si on supprime des permissions sur le groupe Domain Admins, une routine viendra les rétablir en se basant sur les permissions de l'objet AdminSDHolder. Ceci peut être utile pour faire une backdoor (voir [ADSecurity](https://adsecurity.org/?p=1906))
  - [Restricted RDP](https://blogs.technet.microsoft.com/kfalde/2013/08/14/restricted-admin-mode-for-rdp-in-windows-8-1-2012-r2/)


## Ressources

### Outils

- [PingCastle](https://www.pingcastle.com/): petit tool pour des audits AD. A tester.

### Articles
-   [Attack Methods for Gaining Domain Admin Rights in Active Directory](https://adsecurity.org/?p=2362)
-   [Red vs Blue Modern Active Directory Attacks Defense - Sean Metcalf](https://www.youtube.com/watch?v=Lz6haohGAMc&feature=youtu.be)
-   [Active Directory Kill Chain Attack & Defense](https://github.com/infosecn1nja/AD-Attack-Defense): liste d'articles sur des problématiques liées à Active Directory.


