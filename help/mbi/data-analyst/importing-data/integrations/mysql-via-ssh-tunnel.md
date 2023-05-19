---
title: Connexion [!DNL MySQL] via le tunnel SSH
description: Découvrez comment vous connecter [!DNL MySQL] via le tunnel SSH.
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# Connexion [!DNL MySQL] via [!DNL SSH Tunnel]

* [Récupération de la variable [!DNL Commerce Intelligence] clé publique](#retrieve)
* [Autoriser l’accès au [!DNL Commerce Intelligence] Adresse IP](#allowlist)
* [Création d’un utilisateur Linux pour [!DNL Commerce Intelligence]](#linux)
* [Créez un [!DNL MySQL] user pour [!DNL Commerce Intelligence]](#mysql)
* [Saisissez les informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence]](#finish)

## ACCÉDER À

* [[!DNL MySQL] via ](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL] via [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

Pour connecter votre [!DNL MySQL] vers la base de données [!DNL Commerce Intelligence] via un `SSH tunnel`, vous devez effectuer quelques opérations :

1. Récupération de la variable [!DNL Commerce Intelligence] `public key`
1. Autoriser l’accès au [!DNL Commerce Intelligence] `IP address`
1. Créez un `Linux` user pour [!DNL Commerce Intelligence]
1. Créez un `MySQL` user pour [!DNL Commerce Intelligence]
1. Saisissez les informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence]


## Récupération de la variable [!DNL Commerce Intelligence] clé publique {#retrieve}

Le `public key` est utilisé pour autoriser la variable [!DNL Commerce Intelligence] `Linux` utilisateur. Dans la section suivante, vous allez créer l’utilisateur et importer la clé.

1. Accédez à **[!UICONTROL Manage Data** > **Connections]** et cliquez sur **[!UICONTROL Add New Data Source]**.
1. Cliquez sur le bouton `MySQL` icône .
1. Après la `MySQL credentials` s’ouvre, définissez `Encrypted` bascule vers `Yes`. Le formulaire de configuration SSH s’affiche alors.
1. Le `public key` se trouve sous ce formulaire.

Laissez cette page ouverte tout au long du tutoriel. Vous en aurez besoin dans la section suivante et à la fin.

Voici comment naviguer [!DNL Commerce Intelligence] pour récupérer la clé :

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## Autoriser l’accès au [!DNL Commerce Intelligence] Adresse IP {#allowlist}

Pour que la connexion soit établie, vous devez configurer votre pare-feu pour autoriser l’accès à partir de vos adresses IP. Ils sont `54.88.76.97` et `34.250.211.151` mais ils sont également sur la `MySQL credentials` page. Voir la zone bleue dans le GIF ci-dessus.

## Création d’un [!DNL Linux] user pour [!DNL Commerce Intelligence] {#linux}

Il peut s’agir d’une machine de production ou secondaire, à condition qu’elle contienne des données en temps réel (ou fréquemment mises à jour). Vous pouvez [restreindre cet utilisateur](../../../administrator/account-management/restrict-db-access.md) de toute façon, tant qu’il conserve le droit de se connecter à la variable `MySQL` serveur.

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
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>Si la variable `sshd\_config` Le fichier associé au serveur n’est pas défini sur l’option par défaut, seuls certains utilisateurs disposent d’un accès au serveur, ce qui empêche une connexion réussie à [!DNL Commerce Intelligence]. Dans ce cas, il est nécessaire d’exécuter une commande comme `AllowUsers` pour autoriser le `rjmetric` accès utilisateur au serveur.

## Création d’un [!DNL MySQL] user pour [!DNL Commerce Intelligence] {#mysql}

Votre organisation peut nécessiter un processus différent, mais la méthode la plus simple pour créer cet utilisateur consiste à exécuter la requête suivante lorsqu’elle est connectée. [!DNL MySQL] en tant qu’utilisateur disposant du droit d’accorder des privilèges :

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

Remplacer `secure password here` avec un mot de passe sécurisé, qui peut différer de la variable `SSH` mot de passe.

Pour empêcher cet utilisateur d’accéder aux données de bases de données, tables ou colonnes spécifiques, vous pouvez exécuter des requêtes GRANT qui autorisent uniquement l’accès aux données que vous autorisez.

## Saisie des informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence] {#finish}

Pour terminer, vous devez saisir les informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence]. Avez-vous quitté le `MySQL credentials` ouverture de la page ? Si ce n’est pas le cas, accédez à **[!UICONTROL Data** > **Connections]** et cliquez sur **[!UICONTROL Add New Data Source]**, puis la variable [!DNL MySQL] icône . N’oubliez pas de définir la variable `Encrypted` bascule vers `Yes`.

Renseignez les informations suivantes dans cette page, en commençant par le `Database Connection` section :

* `Username`: Nom d’utilisateur de la variable [!DNL Commerce Intelligence] [!DNL MySQL] user
* `Password`: Le mot de passe du [!DNL Commerce Intelligence] [!DNL MySQL] user
* `Port`: [!DNL MySQL] port sur votre serveur (3306 par défaut)
* `Host` Par défaut, il s’agit de localhost. En général, il s’agit de la valeur de l’adresse de liaison pour votre [!DNL MySQL] server, qui est par défaut `127.0.0.1 (localhost)`, mais peut également être une adresse réseau locale (par exemple, `192.168.0.1`) ou l’adresse IP publique de votre serveur.

   La valeur se trouve dans votre `my.cnf` (situé à l’emplacement `/etc/my.cnf`) sous la ligne qui indique `\[mysqld\]`. Si la ligne d’adresse de liaison est commentée dans ce fichier, votre serveur est sécurisé suite à des tentatives de connexion externes.

Dans le `SSH Connection` section :

* `Remote Address`: Adresse IP ou nom d’hôte du serveur [!DNL Commerce Intelligence] tunnel
* `Username`: Nom d’utilisateur de la variable [!DNL Commerce Intelligence] SSH ([!DNL Linux]) user
* `SSH Port`: Port SSH sur votre serveur (22 par défaut)

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save & Test]** pour terminer la configuration.

## En rapport :

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
