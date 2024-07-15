---
title: Connexion [!DNL MongoDB] via le tunnel SSH
description: Découvrez comment se connecter à  [!DNL MongoDB] via un tunnel SSH.
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# Connexion de [!DNL MongoDB] via le tunnel SSH

Pour connecter votre base de données [!DNL MongoDB] à [!DNL Commerce Intelligence] via un tunnel SSH, vous devez procéder comme suit :

1. [Récupération de la clé publique  [!DNL Commerce Intelligence] ](#retrieve)
1. [Autoriser l’accès à l’adresse IP  [!DNL Commerce Intelligence] ](#allowlist)
1. [Création d’un utilisateur Linux pour Commerce Intelligence](#linux)
1. [Création d’un utilisateur  [!DNL MongoDB] pour Commerce Intelligence](#mongodb)
1. [Saisissez les informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence].](#finish)

>[!NOTE]
>
>En raison de la nature technique de cette configuration, Adobe vous recommande de faire une boucle dans un développeur pour vous aider si vous ne l’avez pas fait auparavant.

## Récupération de la clé publique [!DNL Commerce Intelligence] {#retrieve}

`public key` est utilisé pour autoriser l’utilisateur [!DNL Commerce Intelligence] `Linux`. La section suivante vous guide tout au long de la création de l’utilisateur et de l’importation des clés.

1. Accédez à **[!UICONTROL Data** > **Connections]** et cliquez sur **[!UICONTROL Add New Data Source]**.
1. Cliquez sur l’icône [!DNL MONGODB] .
1. Une fois la page des informations d’identification [!DNL MongoDB] ouverte, remplacez le bouton d’activation/désactivation `Encrypted` par `Yes`. Le formulaire de configuration SSH s’affiche alors.
1. `public key` se trouve sous ce formulaire.

Laissez cette page ouverte tout au long du tutoriel. Vous en aurez besoin dans la section suivante et à la fin.

Si vous êtes un peu perdu, voici comment parcourir [!DNL Commerce Intelligence] pour récupérer la clé :

![Récupération de la clé publique RJMetrics](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## Autoriser l’accès à l’adresse IP [!DNL Commerce Intelligence] {#allowlist}

Pour que la connexion soit établie, vous devez configurer votre pare-feu pour autoriser l’accès à partir de vos adresses IP. Ils sont `54.88.76.97` et `34.250.211.151`, mais il se trouve également sur la page des informations d’identification [!DNL MongoDB] :

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Création d’un utilisateur `Linux` pour [!DNL Commerce Intelligence] {#linux}

>[!IMPORTANT]
>
>Si le fichier `sshd_config` associé au serveur n’est pas défini sur l’option par défaut, seuls certains utilisateurs disposent d’un accès au serveur, ce qui empêche une connexion réussie à [!DNL Commerce Intelligence]. Dans ce cas, il est nécessaire d’exécuter une commande du type `AllowUsers` pour permettre à l’utilisateur `rjmetric` d’accéder au serveur.

Il peut s’agir d’une machine de production ou secondaire, à condition qu’elle contienne des données en temps réel (ou fréquemment mises à jour). Vous pouvez restreindre cet utilisateur comme vous le souhaitez tant qu&#39;il conserve le droit de se connecter au serveur [!DNL MongoDB].

Pour ajouter le nouvel utilisateur, exécutez les commandes suivantes en tant que root sur votre serveur `Linux` :

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

Vous vous souvenez du `public key` que vous avez récupéré dans la première section ? Pour vous assurer que l’utilisateur a accès à la base de données, vous devez importer la clé dans `authorized_keys`. Copiez la clé entière dans le fichier `authorized_keys` comme suit :

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

Pour terminer la création de l’utilisateur, modifiez les autorisations du répertoire /home/jmetric pour autoriser l’accès via SSH :

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## Création d&#39;un utilisateur [!DNL Commerce Intelligence] [!DNL MongoDB] {#mongodb}

[!DNL MongoDB] serveurs ont deux modes d&#39;exécution : [un avec l&#39;option &quot;auth&quot;](#auth) `(mongod -- auth)` et un sans, [qui est la valeur par défaut](#default). Les étapes de création d’un utilisateur [!DNL MongoDB] varient en fonction du mode utilisé par votre serveur. Veillez à vérifier le mode avant de continuer.

### Si votre serveur utilise l’option `Auth` : {#auth}

Lors de la connexion à plusieurs bases de données, vous pouvez ajouter l’utilisateur en vous connectant à [!DNL MongoDB] en tant qu’utilisateur administrateur et en exécutant les commandes suivantes.

>[!NOTE]
>
>Pour afficher toutes les bases de données disponibles, l’utilisateur [!DNL Commerce Intelligence] a besoin des autorisations pour exécuter `listDatabases.`.

Cette commande permet à l’utilisateur [!DNL Commerce Intelligence] d’accéder à `to all databases` :

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

Utilisez cette commande pour accorder l&#39;accès [!DNL Commerce Intelligence] à l&#39;utilisateur `to a single database` :

```bash
    use < database name >
    db.createUser('rjmetric', '< secure password here >', true)
```

Cela imprime une réponse qui ressemble à ceci :

```bash
    {
    "id": ObjectId("< some object id here >"),
    "user": "rjmetric",
    "readOnly": true,
    "pwd": "< some hash here >"
    }
```

### Si votre serveur utilise l’option par défaut {#default}

Si votre serveur n&#39;utilise pas le mode `auth`, votre serveur [!DNL MongoDB] est accessible même sans nom d&#39;utilisateur et mot de passe. Cependant, vous devez vous assurer que le fichier `mongodb.conf` `(/etc/mongodb.conf)` comporte les lignes suivantes - si ce n&#39;est pas le cas, redémarrez votre serveur après les avoir ajoutés.

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

Pour lier votre serveur [!DNL MongoDB] à une autre adresse, ajustez le nom d’hôte de la base de données à l’étape suivante en conséquence.

## Saisie des informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence] {#finish}

Pour terminer, vous devez saisir les informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence]. Avez-vous laissé la page des informations d’identification [!DNL MongoDB] ouverte ? Dans le cas contraire, accédez à **[!UICONTROL Data > Connections]** et cliquez sur **[!UICONTROL Add New Data Source]**, puis sur l’icône [!DNL MongoDB]. N’oubliez pas de remplacer la bascule `Encrypted` par `Yes`.

Renseignez les informations suivantes dans cette page, en commençant par la section `Database Connection` :

* `Host` : `127.0.0.1`
* `Username` : nom d’utilisateur [!DNL Commerce Intelligence] [!DNL MongoDB] (doit être `rjmetric`)
* `Password` : mot de passe [!DNL Commerce Intelligence] [!DNL MongoDB]
* `Port` : port de MongoDB sur votre serveur (`27017` par défaut)
* `Database Name` (Facultatif) : si vous n’avez autorisé l’accès qu’à une base de données, indiquez son nom dans ce champ.

Sous la section `SSH Connection` :

* `Remote Address` : l’adresse IP ou le nom d’hôte du serveur dans lequel vous allez SSH
* `Username` : nom d’utilisateur [!DNL Commerce Intelligence] Linux (SSH) (doit être jmetric)
* `SSH Port` : port SSH sur votre serveur (22 par défaut)

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save Test]** pour terminer la configuration.

### Associé

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
