---
title: JAVA
permalink: /JAVA/
---

# Java

## Configuration

Configurer les différentes variables d'environnement pour Java (basé sur https://stackoverflow.com/questions/1672281/environment-variables-for-java-installation):
``` text
JAVA_HOME : C:\Program Files\Java\jdk1.8.0_112
JDK_HOME  : %JAVA_HOME%
JRE_HOME  : %JAVA_HOME%\jre
CLASSPATH : .;%JAVA_HOME%\lib;%JAVA_HOME%\jre\lib
PATH      : your-unique-entries;%JAVA_HOME%\bin
```

## Interception HTTPS

Voir [Burp Suite Proxy with java application](https://stackoverflow.com/questions/50157307/burp-suite-proxy-with-java-application/50177906?noredirect=1)

## JavaSnoop

JavaSnoop est un outil permettant de se hooker à une application Java. JavaSnoop utilise Java 1.6 (http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase6-419409.html)

## Références
- "Hookons" avec JavaSnoop (Misc 77)
