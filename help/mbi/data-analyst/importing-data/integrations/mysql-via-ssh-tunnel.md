---
title: Connexion de MySQL via un tunnel SSH
description: Découvrez comment connecter MySQL via le tunnel SSH.
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# Connexion `MySQL` via `SSH Tunnel`

* [Récupération de la variable [!DNL MBI] clé publique](#retrieve)
* [Autoriser l’accès au [!DNL MBI] Adresse IP](#allowlist)
* [Création d’un utilisateur Linux pour [!DNL MBI]](#linux)
* [Création d’un utilisateur MySQL pour [!DNL MBI]](#mysql)
* [Saisissez les informations de connexion et d’utilisateur dans [!DNL MBI]](#finish)

## ACCÉDER À

* `MySQL via SSH tunnel`
* [`MySQL`](../integrations/mysql-via-a-direct-connection.md)
* [`MySQL`](../integrations/mysql-via-cpanel.md)

Pour connecter votre `MySQL` vers la base de données [!DNL MBI] via un `SSH tunnel`, vous (ou votre équipe, si vous n’êtes pas un technicien) devrez effectuer quelques opérations :

1. Récupération de la variable [!DNL MBI] `public key`
1. Autoriser l’accès au [!DNL MBI] `IP address`
1. Créez un `Linux` user pour [!DNL MBI]
1. Créez un `MySQL` user pour [!DNL MBI]
1. Saisissez les informations de connexion et d’utilisateur dans [!DNL MBI]

Ce n&#39;est pas aussi compliqué qu&#39;il pourrait sembler. Commençons !

## Récupération de la variable [!DNL MBI] clé publique {#retrieve}

Le `public key` est utilisé pour autoriser la variable [!DNL MBI] `Linux` utilisateur. Dans la section suivante, nous allons créer l&#39;utilisateur et importer la clé.

1. Accédez à **[!UICONTROL Manage Data** > **Connections]** et cliquez sur **[!UICONTROL Add New Data Source]**.
1. Cliquez sur le bouton `MySQL` icône .
1. Après la `MySQL credentials` s’ouvre, définissez `Encrypted` bascule vers `Yes`. Le formulaire de configuration SSH s’affiche alors.
1. Le `public key` se trouve sous ce formulaire.

Laissez cette page ouverte tout au long du tutoriel. Vous en aurez besoin dans la section suivante et à la fin.

Si vous êtes un peu perdu, voici comment naviguer [!DNL MBI] pour récupérer la clé :

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## Autoriser l’accès au [!DNL MBI] Adresse IP {#allowlist}

Pour que la connexion soit établie, vous devez configurer votre pare-feu afin d’autoriser l’accès à partir de nos adresses IP. Ils sont `54.88.76.97` et `34.250.211.151` mais ils sont également sur la `MySQL credentials` page. Vous voyez la boîte bleue dans le GIF ci-dessus ? C&#39;est tout !

## Création d’un `Linux` user pour [!DNL MBI] {#linux}

Il peut s’agir d’une machine de production ou secondaire, à condition qu’elle contienne des données en temps réel (ou fréquemment mises à jour). Vous pouvez [restreindre cet utilisateur](../../../administrator/account-management/restrict-db-access.md) de toute façon, tant qu’il conserve le droit de se connecter à la variable `MySQL` serveur.

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
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>Si la variable `sshd\_config` Le fichier associé au serveur n’est pas défini sur l’option par défaut, seuls certains utilisateurs auront un accès au serveur, ce qui empêchera une connexion réussie à [!DNL MBI]. Dans ce cas, il est nécessaire d’exécuter une commande comme `AllowUsers` pour autoriser le `rjmetric` accès utilisateur au serveur.

## Création d’un `MySQL` user pour [!DNL MBI] {#mysql}

Votre organisation peut nécessiter un processus différent, mais la méthode la plus simple pour créer cet utilisateur consiste à exécuter la requête suivante lorsqu’elle est connectée. `MySQL` en tant qu’utilisateur disposant du droit d’accorder des privilèges :

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

Remplacer `secure password here` avec un mot de passe sécurisé, qui peut être différent du `SSH` mot de passe.

Pour empêcher cet utilisateur d’accéder aux données de bases de données, tables ou colonnes spécifiques, vous pouvez exécuter des requêtes GRANT qui autorisent uniquement l’accès aux données que vous autorisez.

## Saisie des informations de connexion et d’utilisateur dans [!DNL MBI] {#finish}

Pour terminer, nous devons saisir les informations de connexion et d’utilisateur dans [!DNL MBI]. Avez-vous quitté le `MySQL credentials` ouverture de la page ? Si ce n’est pas le cas, accédez à **[!UICONTROL Data** > **Connections]** et cliquez sur **[!UICONTROL Add New Data Source]**, puis l’icône MySQL. n’oubliez pas de définir la variable `Encrypted` bascule vers `Yes`.

Renseignez les informations suivantes dans cette page, en commençant par la section Connexion à la base de données :

* `Username`: Nom d’utilisateur de la variable [!DNL MBI] Utilisateur MySQL
* `Password`: Le mot de passe du [!DNL MBI] Utilisateur MySQL
* `Port`: Port de MySQL sur votre serveur (3306 par défaut)
* `Host` Par défaut, il s’agit de localhost. En général, il s’agit de la valeur de l’adresse de liaison de votre serveur MySQL, qui est, par défaut, `127.0.0.1 (localhost)`, mais peut également être une adresse réseau locale (par exemple, `192.168.0.1`) ou l’adresse IP publique de votre serveur.

   La valeur se trouve dans votre `my.cnf` (situé généralement à l’emplacement `/etc/my.cnf`) sous la ligne qui indique `\[mysqld\]`. Si la ligne d’adresse de liaison est commentée dans ce fichier, votre serveur est sécurisé suite à des tentatives de connexion externes.

Dans le `SSH Connection` section :

* `Remote Address`: Adresse IP ou nom d’hôte du serveur [!DNL MBI] tunnel
* `Username`: Nom d’utilisateur de la variable [!DNL MBI] Utilisateur SSH (Linux)
* `SSH Port`: Port SSH sur votre serveur (22 par défaut)

C&#39;est tout ! Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save & Test]** pour terminer la configuration.

## En rapport :

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
