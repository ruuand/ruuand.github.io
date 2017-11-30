---
title: CRLF Injection
permalink: /CRLF/
---

# CRLF Injection

## Points de contrôles

Les points suivants sont à vérifier:

- Valeurs réutilisées dans les headers (paramètre GET, POST, élément du Referer, etc.)
- Peut-on faire des retours à la ligne ? Essayer différents encodages.
- Peut-on ajouter un cookie arbitraire (Cookie: lang=$p avec $p = "xx; session=truc)

## Payloads

Voir [PayloadAllTheThings](https://github.com/ruuand/PayloadsAllTheThings/tree/master/CRLF%20injection)
