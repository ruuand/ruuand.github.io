---
title: Amazon Web Services
permalink: /AWS/
---

# Amazon Web Services
AWS propose des services clouds. Certaines vulnérabilités spécifiques à AWS peuvent être intéressantes à connaître.

## Buckets AWS
AWS utilise des "buckets" (un peu comme un repo github) pour gérer les sites. Quand ils sont mals configurés il est possible de lister le contenu des buckets, ou même modifier le contenu !

Quand des permissions sont définies pour "tout le monde":
```
[~] aws s3 ls  s3://flaws.cloud/ --no-sign-request --region us-west-2                                                    
2017-03-02 23:00:18       2540 hint1.html
2017-03-02 23:05:17       1707 hint2.html
2017-03-02 23:05:11       1101 hint3.html
2017-03-02 23:01:15       2878 index.html
2017-02-26 20:59:28         46 robots.txt
2017-02-26 20:59:30       1051 secret-dd02c7c.html
```

La région peut varier. On peut la retrouver via host:
```
[~] host flaws.cloud 
flaws.cloud has address 54.231.176.231
[~] host 54.231.176.231 
231.176.231.54.in-addr.arpa domain name pointer s3-website-us-west-2.amazonaws.com.
```

Dans certains cas il est nécessaire d'avoir au moins un compte (https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html):
```
[~] aws s3 --profile ruuand ls s3://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud     
2017-02-26 21:02:15      80751 everyone.png
2017-03-02 22:47:17       1433 hint1.html
2017-02-26 21:04:39       1035 hint2.html
2017-02-26 21:02:14       2786 index.html
2017-02-26 21:02:14         26 robots.txt
2017-02-26 21:02:15       1051 secret-e4443fc.html
```

Quelques points importants:
- Les noms des buckets sont uniques sur tout AWS.
- Pour accéder à un bucket via un nom de domaine il faut que le DNS corresponde au nom du bucket.
- Un utilisateur ayant le droit de lister les buckets d'un compte pourra lister TOUT les buckets. Il n'y a pas de restrictions du type (liste seulement bucket1, bucket2 mais pas bucket3), en revanche on peut restreindre l'accès aux buckets.

## Snapshots
Il est possible de faire des snapshots. L'accès à ceux-ci est restreint par défaut mais certains utilisateurs les rendent public
```
aws --profile attack ec2 describe-snapshots --region us-west-2
```
Si on peut récupérer un snapshot alors il est possible de le monter dans une instance que l'on contrôle pour fouiller un peu.

## Commandes utiles
```
aws configure --profile ruuand # Configure le profil ruuand
aws s3 --profile ruuand sync s3://level3-9afd3927f195e10225021a578e6f78df.flaws.cloud/ . # Télécharge le contenu d'un bucket
aws --profile ruuand s3 ls # Liste les buckets avec le profil ruuand
```

# Références
- [FLAWS](http://flaws.cloud)
