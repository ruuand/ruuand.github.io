# Wiki / Cheat-Sheet de pentesting
Les informations contenues dans ce site sont plus ou moins mises à jours et plus ou moins fiable. A utiliser avec précaution. Le regroupement en différentes catégories est très aproximatif.

## Liens généraux

Cette section contient des sites / articles généraux contenant de nombreuses ressources:

## Pentest Interne

Cette section contient des éléments relatifs aux tests d'intrusion internes, principalement sur les parties Windows.

- [Read Teaming Experiments](https://ired.team/): un site contenant de nombreux articles / notes sur des techniques relatives aux missions Red Team / TI interne.


- [Cheat Sheet](/CheatSheet_AD/)

- [Test d'intrusion interne](/Test_d'intrusion_interne/)
- [Post Exploitation](/Post_Exploitation/)
- [User Hunting](/User_Hunting/)
- [DHCP](/DHCP/)
- [Firewall](/Firewall/)
- [Windows](/Windows/)

- [Active Directory](/Active_Directory/)
	- [Group Policy Object](/Group_Policy_Object/)
	- [Kerberos](/Kerberos/)
	- [Azure Active Directory](/Azure_AD/)
    - [Kerberos Delegation](/Kerberos_Delegation/)
	- [Kerberoasting](/Kerberoasting/)
	- [MS-RPRN](/MS_RPRN/)
	- [Pass The Hash](/Pass_The_Hash/)
	- [Dump des hashs du domaine](/Dump_des_hashs_du_domaine/)
	- [Just Enough Administration](/Just_Enough_Administration/)
	- [WMI](/WMI/)
	- [LLMNR](/LLMNR/)
	- [SMB Relay](/SMB_Relay/)
    - [NTLM Relay](/NTLM_Relay/)
	- [Trust Relationships](/Trust_Relationships/)
	- [MSCacheV2](/MsCacheV2/)
	- [Local Admin Password Solution](/LAPS/)
	- [Read Only Domain Controllers](/RODC/)
	- [NTLM & NetNTLM](/NTLM/)
	- [Linux et Active Directory](/Linux_AD/)
	- [Microsoft Exchange](/Exchange/)

- [Poste de travail](/Poste_de_travail/)
	- [SecureBoot](/SecureBoot/)
	- [Windows 10](/Windows_10/)
	- [Mode Kiosque](/Kiosk_Mode/)
	- [Bitlocker](/Bitlocker/)
    - [Applocker](/Applocker/)

- Outils
	- [Powershell](/Powershell/)
	- [CrackMapExec](/CrackMapExec/)
	- [Powershell Empire](/Powershell_Empire/)
	- [PowerSploit](/PowerSploit/)
	- [Mimikatz](/Mimikatz/)
	- [BloodHound](/BloodHound/)
	- [MailSniper](/MailSniper/)
	- [Responder](/Responder/)
	- [nmap](/nmap/)

- Antivirus
    - [Antivirus](/Antivirus)
	- [Contournement d'antivirus](/Contournement_d'antivirus/)

- Vulnérabilités
	- [MS14-068](/MS14-068/)


- Divers
	- [Network Access Control](/Network_Access_Control/)
	- [Smartcard](/Smartcard/)
	- [Transfert de fichiers](/Transfert_de_fichiers/)
	- [Wifi](/Wifi/)
	- [Elévation de priviléges (Windows)](/Elévation_de_priviléges_(Windows)/)
	- [Imprimantes](/Imprimantes/)
	- [Logging](/Logging/)
	- [Citrix](/Citrix/)

Services
--------
Cette section contient différents services (e.g. DNS, FTP, etc).

- [DHCP](/DHCP/)
- [DNS (tcp/53)](/DNS/)
- [MySQL (tcp/3306)](/MySQL/)
- [NTP (tcp/123)](/NTP/)
- [FTP (tcp/21)](/FTP/)
- [Kerberos (tcp/88)](/Kerberos/)
- [LLMNR](/LLMNR/)
- [SMB (tcp/445)](/SMB/)
- [SNMP (upd/161)](/SNMP/)
- [Microsoft SQL Server (tcp/1433)](/Microsoft_SQL_Server/)
- [MongoDB (tcp/27017)](/MongoDB/)
- [Remote Desktop Protcol (tcp/3389)](/RDP/)
- [RSH (Remote SHell) (tcp/54)](/RSH/)
- [NFS (Network File System)](/NFS/)
- Applications web: voir section **Web**

Web & Applicatifs
---
Cette section contient différents éléments relatifs aux tests d'intrusions webs & clients lourds.

- [Test d'intrusion Web](/web/)

- Outils & Techniques
	- [CyberChef](https://gchq.github.io/CyberChef): une page HTML permettant d'effectuer des opérations sur des chaînes (base64, puis URLencode, etc.)
	- [Dirb](/Dirb/)
	- [Local File Include](/Local_File_Include/)
	- [Mots de passes par défaut](/Mots_de_passes_par_défaut/)
	- [Messages d'erreurs](/Messages_d'erreurs/)
	- [Google Search](/Google_Search/)
	- [Certificate Transparency](/Certificate_Transparency/)
	- [Content Security Policy (CSP)](/CSP/)
	- [Cross Origin Ressource Sharing (CORS)](/CORS/)
	- [XSLT](/XSLT/)
	- Headers HTTP:   
		- [Header Host](/Host_Header/)
		- [Content Security Policy (CSP)](/CSP/)
	- [Websockets](/Websockets/)
	- [ZIP](/ZIP/)
	- [Gestion de version](/Gestion_Version) (Git, SVN)

- Vulnérabilités
	- [CRLF (Injection)](/CRLF/)
	- [Cross Site Request Forgery (CSRF)](/CSRF/)
	- [CSV Injection](/CSV_Injection/)
	- Deserialization:
		- [Java Deserialization](/Java_Deserialization/)
	- [DNS Rebinding](/DNS_Rebinding/)
		- [Injection HQL](/HQL/)
		- [LDAP Injection](/LDAP_Injection/)
	- [File Upload](/Upload/)
	- [SQL Injection](/SQL_Injection/)
	- [Server Side Request Forgery](/SSRF/)
	- [Server Side Template Injection (SSTI)](/SSTI/)
	- [Subdomain Takeover](/Subdomain_Takeover/)
	- [Web Cache (Attaques)](/Web_Cache/)
	- [XSS](/XSS/)
	- [XML eXternal Entity (XXE)](/XXE/)

- Technologies
	- [Adobe ColdFusion](/Adobe_ColdFusion/)
	- [Adobe Flash](/Flash/)
	- [Apache](/Apache/)
	- [Apache Tomcat](/Apache_Tomcat/)
	- [Web2py](/Web2py/)
	- [WebDAV](/WebDAV/)
	- [WordPress](/WordPress/)
	- [Microsoft Silverlight](/Silverlight/)
	- [Amazon Web Services (AWS)](/AWS/)
	- [Java](/JAVA/)
	- [Jenkins](/Jenkins/)
	- [Cloudflare](/Cloudflare/)
	- [WAF](/WAF/)
	- [HP ILO](/HP_ILO/)
	- [Google Web Toolkit (GWT)](/GWT/)
    - [JSON Web Tokens (JWT)](/JWT/)


## Exploitation & RE
- [Buffer Overflows](/Buffer_Overflows/)
- [Corelan Exploit Course](/Corelan_Exploit_Course/)
- [Egg Hunter](/Egg_Hunter/)
- [Assembleur](/Assembleur/)
- [Reverse Engineering](/RE/)

Linux
-----
- [Elevation de priviléges (Linux)](/Elevation_de_priviléges_(Linux)/)
- [Bash](/Bash/)
- [Netcat](/Netcat/)

IoT
---
- [Bluetooth Low Energy](/BLE/)

Mobile
-----
- [Android](/Android/)
- [iOS](/iOS/)

Divers
------
- [Divers](/Divers/)
- [Installation serveur](/Installation_serveur/)
- [Pentest Lab](/Pentest_Lab/)
- [Proxy SSH](/Proxy_SSH/)
- [Sudo](/Sudo/)
- [Virtualisation](/Virtualisation/)
- [Phishing](/Phishing/)
- [Reverse Shells](/Reverse_Shells/)
- [Internet Explorer](/Internet_Explorer/)
- [Vulnérabilités](/Vulnerabilités/)
- [Décompilation](/Décompilation/)
- [RedTeam](/RedTeam/)
- [AIX](/AIX/)
- [ATM](/ATM/)
- [Bug Bounty](/Bug_Bounty/)
- [Actualités](/Actualité/)
- [Python](/python/)
- [Multi Factor Authentication](/MFA/)
- [Scan réseau](/Scan_reseau/)
