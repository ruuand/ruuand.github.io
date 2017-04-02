---
title: Windows 10
permalink: /Windows_10/
---

# Windows 10

Virtual Secure Mode
-------------------
Virtual Secure Mode (VSM) est une technologie basée sur la virtualisation. Un hyperviseur se situe au dessus de l'OS Windows qui est virtualisé. Une autre "VM" peut alors contenir les processus sensibles, c'est le VSM. Ceci permet notamment de séparer des processus sensibles comme LSASS. Ainsi si l'OS est compromis, l'attaquant n'a pas accès aux secrets, ceux-ci se situant dans une VM différente. Il faut alors parvenir à compromette l'hyperviseur se situant au dessus.

Device Guard
------------
Device Guard contient trois principaux composants:
* Configurable Code Integrity (CCI): CCI impose que le code executé par la machine soit signé et trusté.
* VSM Protected Code Integrity:
* UEFI Secure Boot

Credential Guard
----------------
Basé sur VSM, Credential Guard permet de s'assurer que LSA soit sécurisé dans VSM.

Références
----------
- [Windows 10 Microsoft Passport (aka Microsoft Next Generation Credential) In Detail](https://adsecurity.org/?p=1535)
