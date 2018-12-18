# Wiki / Cheat-Sheet de pentesting
Les informations contenues dans ce site sont plus ou moins mises à jours et plus ou moins fiable. A utiliser avec précaution. Le regroupement en différentes catégories est très aproximatif.



Pentest Interne & Active Directory
----------------------------------
Cette section contient des éléments relatifs aux tests d'intrusion internes, principalement sur les parties Windows.

- [Test d'intrusion interne](/Test_d'intrusion_interne/)
- [Post Exploitation](/Post_Exploitation/)
- [User Hunting](/User_Hunting/)
- [DHCP](/DHCP/)
- [Firewall](/Firewall/)
- [Windows](/Windows/)

- [Active Directory](/Active_Directory/)
	- [Group Policy Object](/Group_Policy_Object/)
	- [Kerberos](/Kerberos/)
	- [Kerberoasting](/Kerberoasting/)
	- [MS-RPRN](/MS_RPRN/)
	- [Pass The Hash](/Pass_The_Hash/)
	- [Dump des hashs du domaine](/Dump_des_hashs_du_domaine/)
	- [Just Enough Administration](/Just_Enough_Administration/)
	- [WMI](/WMI/)
	- [LLMNR](/LLMNR/)
	- [SMB Relay](/SMB_Relay/)
	- [Trust Relationships](/Trust_Relationships/)
	- [MSCacheV2](/MsCacheV2/)
	- [Local Admin Password Solution](/LAPS/)
	- [Read Only Domain Controllers](/RODC/)
	- [NTLM & NetNTLM](/NTLM/)

- [Poste de travail](/Poste_de_travail/)
	- [SecureBoot](/SecureBoot/)
	- [Windows 10](/Windows_10/)

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
	- [Web Cache](/Web_Cache/)
	- [Certificate Transparency](/Certificate_Transparency/)
	- [Server Side Request Forgery](/SSRF/)
	- [XSS](/XSS/)
	- [Injection HQL](/HQL/)
	- [CSV Injection](/CSV_Injection/)
	- [Injection SQL](/SQL_Injection/)
	- [Injection LDAP](/LDAP_Injection/)
	- [File Upload](/Upload/)
	- [Cross Site Request Forgery (CSRF)](/CSRF/)
	- [Server Side Template Injection (SSTI)](/SSTI/)
	- [CRLF](/CRLF/)
	- [Content Security Policy (CSP)](/CSP/)
	- [Subdomain Takeover](/Subdomain_Takeover/)
	- [DNS Rebinding](/DNS_Rebinding/)
	- [Cross Origin Ressource Sharing (CORS)](/CORS/)
	- [XSLT](/XSLT/)
	- [ZIP](/ZIP/)
	- [Gestion de version](/Gestion_Version) (Git, SVN)
	- Deserialization:
		- [Java Deserialization](/Java_Deserialization/)
	- Headers HTTP:   
		- [Header Host](/Host_Header/)
		- [Content Security Policy (CSP)](/CSP/)
	
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
	- [Cloudflare](/Cloudflare/)
	- [WAF](/WAF/)
	- [HP ILO](/HP_ILO/)

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
