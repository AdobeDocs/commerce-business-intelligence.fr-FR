---
title: Connexion de PostgreSQL via le tunnel SSH
description: Découvrez comment connecter votre base de données PostgreSQL à Commerce Intelligence via un tunnel SSH.
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# Connexion de [!DNL PostgreSQL] via [!DNL SSH Tunnel]

Pour connecter votre base de données [!DNL PostgreSQL] à [!DNL Commerce Intelligence] via un `SSH tunnel`, procédez comme suit :

1. [Récupération de la clé  [!DNL Commerce Intelligence] &#x200B;](#retrieve)
1. [Autoriser l’accès à l’adresse  [!DNL Commerce Intelligence] &#x200B;](#allowlist)
1. [Créez un  [!DNL Linux]  pour  [!DNL Commerce Intelligence]](#linux)
1. [Créez un  [!DNL PostgreSQL]  pour  [!DNL Commerce Intelligence]](#postgres)
1. [Saisissez les informations de connexion et d’utilisateur dans  [!DNL Commerce Intelligence]](#finish)

## Récupération du [!DNL Commerce Intelligence] [!DNL public key] {#retrieve}

Le `public key` est utilisé pour autoriser l’utilisateur [!DNL Commerce Intelligence] [!DNL Linux]. Vous allez maintenant créer l’utilisateur et importer la clé.

1. Accédez à **[!UICONTROL Manage Data** > **Connections]** et cliquez sur **[!UICONTROL Add a Data Source]**.
1. Cliquez sur l’icône [!DNL PostgreSQL] .
1. Une fois la page `PostgreSQL credentials` ouverte, définissez le bouton `Encrypted` sur `Yes`. Le formulaire de configuration de la `SSH` s’affiche.
1. Le `public key` se trouve sous ce formulaire.

Laissez cette page ouverte tout au long du tutoriel. Vous en aurez besoin dans la section suivante et à la fin.

Vous trouverez ci-dessous comment naviguer dans [!DNL Commerce Intelligence] pour récupérer la clé :

![récupération de la clé publique RJMetrics](../../../assets/get-mbi-public-key.gif)

## Autoriser l&#39;accès à l&#39;adresse IP [!DNL Commerce Intelligence] {#allowlist}

Pour que la connexion soit établie, vous devez configurer votre pare-feu afin d’autoriser l’accès à partir de votre adresse IP. Elle est `54.88.76.97/32`, mais elle se trouve également sur la page des informations d’identification `PostgreSQL`. Voir la case bleue dans le GIF ci-dessus.

## Création d’un utilisateur [!DNL Linux] pour [!DNL Commerce Intelligence] {#linux}

Il peut s’agir d’une machine de production ou secondaire, à condition qu’elle contienne des données en temps réel (ou fréquemment mises à jour). Vous pouvez [restreindre cet utilisateur](../../../administrator/account-management/restrict-db-access.md) comme bon vous semble, à condition qu&#39;il conserve le droit de se connecter au serveur [!DNL PostgreSQL].

1. Pour ajouter le nouvel utilisateur, exécutez les commandes suivantes en tant que root sur votre serveur [!DNL Linux] :

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. Vous vous souvenez de la `public key` que vous avez récupérée dans la première section ? Pour vous assurer que l&#39;utilisateur a accès à la base de données, vous devez importer la clé dans `authorized\_keys`.

   Copiez la clé complète dans le fichier `authorized\_keys` comme suit :

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. Pour terminer la création de l’utilisateur, modifiez les autorisations sur le répertoire `/home/rjmetric` pour autoriser l’accès via `SSH` :

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
```

>[!IMPORTANT]
>
>Si le fichier `sshd\_config` associé au serveur n’est pas défini sur l’option par défaut, seuls certains utilisateurs ont accès au serveur, ce qui empêche une connexion réussie à [!DNL Commerce Intelligence]. Dans ce cas, il est nécessaire d’exécuter une commande telle que `AllowUsers` pour autoriser l’utilisateur ou l’utilisatrice rjmetric à accéder au serveur.

## Création d’un utilisateur [!DNL Commerce Intelligence] [!DNL Postgres] {#postgres}

Votre organisation peut nécessiter un processus différent, mais la méthode la plus simple pour créer cet utilisateur consiste à exécuter la requête suivante lorsqu’il est connecté à Postgres en tant qu’utilisateur disposant du droit d’accorder des privilèges. L’utilisateur doit également être propriétaire du schéma auquel [!DNL Commerce Intelligence] a accès.

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

Remplacez `secure password` par votre propre mot de passe sécurisé, qui peut être différent du mot de passe SSH. Veillez également à remplacer `database name` et `schema name` par les noms appropriés dans votre base de données.

Si vous souhaitez connecter plusieurs bases de données ou schémas, répétez ce processus si nécessaire.

## Saisie des informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence] {#finish}

Pour conclure, vous devez saisir les informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence]. Avez-vous laissé la page des informations d’identification [!DNL PostgreSQL] ouverte ? Dans le cas contraire, accédez à **[!UICONTROL Manage Data > Connections]** et cliquez sur **[!UICONTROL Add a Data Source]**, puis sur l’icône [!DNL PostgreSQL] . N’oubliez pas de définir le bouton (bascule) `Encrypted` sur `Yes`.

Saisissez les informations suivantes dans cette page, en commençant par la section `Database Connection` :

* `Username` : nom d’utilisateur RJMetrics Postgres (doit être rjmetric)
* `Password` : mot de passe RJMetrics Postgres
* `Port` : port PostgreSQL sur votre serveur (5432 par défaut)
* `Host` : 127.0.0.1

Sous `SSH Connection` :

* `Remote Address` : adresse IP ou nom d’hôte du serveur sur lequel vous allez effectuer le SSH
* `Username` : votre nom d&#39;utilisateur SSH (doit être rjmetric)
* `SSH Port` : port SSH sur votre serveur (22 par défaut)

Lorsque vous avez terminé, cliquez sur **Enregistrer et tester** pour terminer la configuration.

### Connexe

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=fr)
