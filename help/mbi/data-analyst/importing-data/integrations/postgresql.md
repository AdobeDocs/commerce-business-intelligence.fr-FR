---
title: Connexion de PostgreSQL via le tunnel SSH
description: Découvrez comment connecter votre base de données PostgreSQL à Commerce Intelligence via un tunnel SSH.
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Connexion [!DNL PostgreSQL] via [!DNL SSH Tunnel]

Pour connecter votre [!DNL PostgreSQL] vers la base de données [!DNL Commerce Intelligence] via un `SSH tunnel`, vous devez effectuer quelques opérations :

1. [Récupération de la variable [!DNL Commerce Intelligence] clé publique](#retrieve)
1. [Autoriser l’accès au [!DNL Commerce Intelligence] Adresse IP](#allowlist)
1. [Créez un [!DNL Linux] user pour [!DNL Commerce Intelligence] ](#linux)
1. [Créez un [!DNL PostgreSQL] user pour [!DNL Commerce Intelligence] ](#postgres)
1. [Saisissez les informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence]](#finish)

## Récupération de la variable [!DNL Commerce Intelligence] [!DNL public key] {#retrieve}

Le `public key` est utilisé pour autoriser la variable [!DNL Commerce Intelligence] [!DNL Linux] utilisateur. Vous allez maintenant créer l’utilisateur et importer la clé.

1. Accédez à **[!UICONTROL Manage Data** > **Connections]** et cliquez sur **[!UICONTROL Add a Data Source]**.
1. Cliquez sur le bouton [!DNL PostgreSQL] icône .
1. Après la `PostgreSQL credentials` s’ouvre, définissez `Encrypted` bascule vers `Yes`. Cette fenêtre affiche le `SSH` formulaire de configuration.
1. Le `public key` se trouve sous ce formulaire.

Laissez cette page ouverte tout au long du tutoriel. Vous en aurez besoin dans la section suivante et à la fin.

Ci-dessous montre comment naviguer [!DNL Commerce Intelligence] pour récupérer la clé :

![Récupération de la clé publique RJMetrics](../../../assets/get-mbi-public-key.gif)

## Autoriser l’accès au [!DNL Commerce Intelligence] Adresse IP {#allowlist}

Pour que la connexion soit établie, vous devez configurer votre pare-feu pour autoriser l’accès à partir de votre adresse IP. Il s’agit de `54.88.76.97/32`, mais il est également activé sur la variable `PostgreSQL` informations d’identification. Voir la zone bleue dans le GIF ci-dessus.

## Création d’un [!DNL Linux] user pour [!DNL Commerce Intelligence] {#linux}

Il peut s’agir d’une machine de production ou secondaire, à condition qu’elle contienne des données en temps réel (ou fréquemment mises à jour). Vous pouvez [restreindre cet utilisateur](../../../administrator/account-management/restrict-db-access.md) de toute façon, tant qu’il conserve le droit de se connecter à la variable [!DNL PostgreSQL] serveur.

1. Pour ajouter le nouvel utilisateur, exécutez les commandes suivantes en tant que root sur votre [!DNL Linux] server :

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. Mémoriser `public key` avez-vous récupéré dans la première section ? Pour vous assurer que l’utilisateur a accès à la base de données, vous devez importer la clé dans `authorized\_keys`.

   Copiez la clé entière dans le `authorized\_keys` comme suit :

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. Pour terminer la création de l’utilisateur, modifiez les autorisations de la variable `/home/rjmetric` pour autoriser l’accès via `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
```

>[!IMPORTANT]
>
>Si la variable `sshd\_config` Le fichier associé au serveur n’est pas défini sur l’option par défaut, seuls certains utilisateurs disposent d’un accès au serveur, ce qui empêche une connexion réussie à [!DNL Commerce Intelligence]. Dans ce cas, il est nécessaire d’exécuter une commande comme `AllowUsers` pour permettre à l’utilisateur jmetric d’accéder au serveur.

## Création d’une [!DNL Commerce Intelligence] [!DNL Postgres] user {#postgres}

Votre organisation peut nécessiter un processus différent, mais la méthode la plus simple pour créer cet utilisateur consiste à exécuter la requête suivante lorsqu’elle est connectée à Postgres en tant qu’utilisateur disposant du droit d’accorder des privilèges. L’utilisateur doit également posséder le schéma qui [!DNL Commerce Intelligence] se voit accorder l’accès à .

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

Remplacer `secure password` avec votre propre mot de passe sécurisé, qui peut être différent du mot de passe SSH. Veillez également à remplacer `database name` et `schema name` avec les noms appropriés dans votre base de données.

Si vous souhaitez connecter plusieurs bases de données ou schémas, répétez cette procédure si nécessaire.

## Saisie des informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence] {#finish}

Pour terminer, vous devez saisir les informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence]. Avez-vous quitté le [!DNL PostgreSQL] la page des informations d’identification s’ouvre ? Si ce n’est pas le cas, accédez à **[!UICONTROL Manage Data > Connections]** et cliquez sur **[!UICONTROL Add a Data Source]**, puis la variable [!DNL PostgreSQL] icône . N’oubliez pas de définir la variable `Encrypted` bascule vers `Yes`.

Renseignez les informations suivantes dans cette page, en commençant par le `Database Connection` section :

* `Username`: Nom d’utilisateur de Postgres RJMetrics (doit être jmetric)
* `Password`: Mot de passe Postgres RJMetrics
* `Port`: Port PostgreSQL sur votre serveur (5432 par défaut)
* `Host`: 127.0.0.1

Sous `SSH Connection`:

* `Remote Address`: L’adresse IP ou le nom d’hôte du serveur vers lequel vous allez SSH
* `Username`: Votre nom de connexion SSH (doit être jmetric)
* `SSH Port`: Port SSH sur votre serveur (22 par défaut)

Lorsque vous avez terminé, cliquez sur **Enregistrement et test** pour terminer la configuration.

### Associé

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
