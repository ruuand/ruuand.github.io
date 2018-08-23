---
title: Java Deserialization
permalink: /Java_Deserialization/
---

# Java Deserialization

Certaines applications utilisent le mécanisme de serialization de Java pour envoyer ou stocker des données. On peut identifier rapidement la serialization en regardant les échanges:
- 0xAC ED 00 05 (pas systématique)
- Noms de classes Java
- 'application/x-java-serialized-object' en header
- rO0 en base64

## Outils

L'outil [ysoserial](https://github.com/frohoff/ysoserial) permet de générer facilement des payloads permettant d'exploiter une serialization Java:
- Les versions les plus récentes de Java intégrent des protections contre ces payloads.
- Le payload URLDNS (qui va faire une requête DNS) ne fait rien de bien méchant et a plus de chance de passer si un simple PoC suffit.
- Plusieurs plugins Burp intégrent l'outil.

## Références
### Outils
- [ysoserial](https://github.com/frohoff/ysoserial)
- [Serialization Dumper](https://github.com/NickstaDB/SerializationDumper)
- [BurpJDSer](https://github.com/khai-tran/BurpJDSer)

### Articles
- [Attacking Java Deserialization](https://nickbloor.co.uk/2017/08/13/attacking-java-deserialization/)
- https://diablohorn.com/2017/09/09/understanding-practicing-java-deserialization-exploits/
- https://deadcode.me/blog/2016/09/02/Blind-Java-Deserialization-Commons-Gadgets.html
- [What Do WebLogic, WebSphere, JBoss, Jenkins, OpenNMS, and Your Application Have in Common? This Vulnerability.](https://foxglovesecurity.com/2015/11/06/what-do-weblogic-websphere-jboss-jenkins-opennms-and-your-application-have-in-common-this-vulnerability/)
