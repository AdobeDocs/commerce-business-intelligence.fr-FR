---
title: Connexion de PostgreSQL via le tunnel SSH
description: Découvrez comment connecter votre base de données PostgreSQL à [!DNL MBI] via un tunnel SSH.
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---

# Connexion `PostgreSQL` via `SSH` Tunnel

Pour connecter votre `PostgreSQL` vers la base de données [!DNL MBI] via un `SSH tunnel`, vous (ou votre équipe, si vous n’êtes pas un technicien) devrez effectuer quelques opérations :

1. [Récupération de la variable [!DNL MBI] clé publique](#retrieve)
1. [Autoriser l’accès au [!DNL MBI] Adresse IP](#allowlist)
1. [Création d’un utilisateur Linux pour [!DNL MBI] ](#linux)
1. [Création d’un utilisateur Postgres pour [!DNL MBI] ](#postgres)
1. [Saisissez les informations de connexion et d’utilisateur dans MBI.](#finish)

Ce n&#39;est pas aussi compliqué qu&#39;il pourrait sembler. Commencez.

## Récupération de la variable [!DNL MBI] `public key` {#retrieve}

Le `public key` est utilisé pour autoriser la variable [!DNL MBI] Utilisateur Linux. Dans la section suivante, nous allons créer l&#39;utilisateur et importer la clé.

1. Accédez à **[!UICONTROL Manage Data** > **Connections]** et cliquez sur **[!UICONTROL Add a Data Source]**.
1. Cliquez sur le bouton `PostgreSQL` icône .
1. Après la `PostgreSQL credentials` s’ouvre, définissez `Encrypted` bascule vers `Yes`. Cela affichera la variable `SSH` formulaire de configuration.
1. Le `public key` se trouve sous ce formulaire.

Laissez cette page ouverte tout au long du tutoriel. Vous en aurez besoin dans la section suivante et à la fin.

Si vous êtes un peu perdu, voici comment naviguer [!DNL MBI] pour récupérer la clé :

![Récupération de la clé publique RJMetrics](../../../assets/get-mbi-public-key.gif)

## Autoriser l’accès au [!DNL MBI] Adresse IP {#allowlist}

Pour que la connexion soit établie, vous devez configurer votre pare-feu afin d’autoriser l’accès à partir de notre adresse IP. it `54.88.76.97/32`, mais il est également activé sur la variable `PostgreSQL` informations d’identification. Vous voyez la boîte bleue dans le GIF ci-dessus ? C&#39;est tout !

## Création d’un `Linux` user pour [!DNL MBI] {#linux}

Il peut s’agir d’une machine de production ou secondaire, à condition qu’elle contienne des données en temps réel (ou fréquemment mises à jour). Vous pouvez [restreindre cet utilisateur](../../../administrator/account-management/restrict-db-access.md) comme vous le souhaitez, tant qu&#39;il conserve le droit de se connecter au serveur PostgreSQL.

1. Pour ajouter le nouvel utilisateur, exécutez les commandes suivantes en tant que root sur votre `Linux` server :

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. Mémoriser `public key` nous avons récupéré dans la première section ? Pour garantir l’accès de l’utilisateur à la base de données, nous devons importer la clé dans `authorized\_keys`.

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
>Si la variable `sshd\_config` Le fichier associé au serveur n’est pas défini sur l’option par défaut, seuls certains utilisateurs auront un accès au serveur, ce qui empêchera une connexion réussie à [!DNL MBI]. Dans ce cas, il est nécessaire d’exécuter une commande comme `AllowUsers` pour permettre à l’utilisateur jmetric d’accéder au serveur.

## Création d’une [!DNL MBI] Utilisateur Postgres {#postgres}

Votre organisation peut nécessiter un processus différent, mais la méthode la plus simple pour créer cet utilisateur consiste à exécuter la requête suivante lorsqu’elle est connectée à Postgres en tant qu’utilisateur disposant du droit d’accorder des privilèges. L’utilisateur doit également posséder le schéma qui [!DNL MBI] se voit accorder l’accès à .

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

Remplacer `secure password` avec votre propre mot de passe sécurisé, qui peut être différent du mot de passe SSH. De plus, assurez-vous de remplacer `database name` et `schema name` avec les noms appropriés dans votre base de données.

Si vous souhaitez connecter plusieurs bases de données ou schémas, répétez cette procédure si nécessaire.

## Saisie des informations de connexion et d’utilisateur dans [!DNL MBI] {#finish}

Pour terminer, nous devons saisir les informations de connexion et d’utilisateur dans [!DNL MBI]. Avez-vous laissé la page des informations d’identification PostgreSQL ouverte ? Si ce n’est pas le cas, accédez à **[!UICONTROL Manage Data > Connections]** et cliquez sur **[!UICONTROL Add a Data Source]**, puis l’icône PostgreSQL . N’oubliez pas de définir la variable `Encrypted` bascule vers `Yes`.

Renseignez les informations suivantes dans cette page, en commençant par la section Connexion à la base de données :

* `Username`: Nom d’utilisateur de Postgres RJMetrics (doit être jmetric)
* `Password`: Mot de passe Postgres RJMetrics
* `Port`: Port PostgreSQL sur votre serveur (5432 par défaut)
* `Host`: 127.0.0.1

Sous `SSH Connection`:

* `Remote Address`: Adresse IP ou nom d’hôte du serveur vers lequel SSH sera envoyé
* `Username`: Notre nom de connexion SSH (doit être jmetric)
* `SSH Port`: Port SSH sur votre serveur (22 par défaut)

C&#39;est tout ! Lorsque vous avez terminé, cliquez sur **Enregistrement et test** pour terminer la configuration.

### Associé

* [Réauthentification des intégrations](https://support.magento.com/hc/en-us/articles/360016733151)
