---
title: Local File Inclusion (LFI)
permalink: /LFI/
---

# Local File Inclusion (LFI)

## Path Truncations

Plusieurs problèmes dans les versions PHP < 5.3 facilitent les LFI. Voir
- [Les PATH truncations: The old one](https://www.dailysecurity.fr/les-path-truncations/)

## PHP Wrappers

LFI spécifiques à php:
- [Wrapper phar://](https://0x1337seichi.wordpress.com/2015/03/15/codgate-2015-ctf-quals-owlur-writeup-web-200/)
- Le wrapper zip:// est similaire

## Ressources

- [LFI](https://github.com/lucyoa/ctf-wiki/tree/master/web/file-inclusion)
