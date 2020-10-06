# Dockerisation de Grr

Ce dépôt contient une dockerisation de Grr: [https://grr.devome.com]
Au premier lancement, la base de données initiale est rentrée. GRR est donc préinstallé.

Vous aurez besoin de versions récentes de docker et docker-compose (en particulier, acceptant la version 3.2 des spécifications de fichier yml).

Les images de base utilisées sont `php:7.3-fpm-alpine`, `mariadb/server` et `nginx:stable-alpine`.

## Personnalisation et Installation

### Submodule, récupération des sources de Grr
Commencez par récupérer le submodule:
```
git submodule init
git submodule update
```

Les sources devraient être réglées sur la version 3.4.1e (dernière version lors de l'écriture de ce fichier). Si ce n'était pas le cas:
```
cd app/src
git checkout v3.4.1e
```

### Personnalisation

La personnalisation pour Grr est effectuée dans le dossier `app`.

Le fichier `connect.inc.php` ne doit pas être modifié.

Vous pouvez personnaliser les fichiers `config.inc.php` et `config_ldap.inc.php` selon vos besoins, puis activer leur copie dans le fichier `Dockerfile` en activant les 2 lignes suivantes:
```
#COPY config.inc.php /var/www/html/include/config.inc.php
#COPY config_ldap.inc.php /var/www/html/include/config_ldap.inc.php
```

### Réglages de l'environnement

à la racine du projet, dans le fichier `.env`, vous pouvez régler le port externe ainsi que le mot de passe de base de données.

### Installation

Une fois la personnalisation et les réglages de l'environnement effectués, il ne vous reste plus qu'à lancer la création des images et le lancement des container avec docker-compose:
```
docker-compose up --build --detach
```
