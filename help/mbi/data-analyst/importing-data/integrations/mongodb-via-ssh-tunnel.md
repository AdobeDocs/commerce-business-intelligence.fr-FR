---
title: Connexion [!DNL MongoDB] via le tunnel SSH
description: Découvrez comment vous connecter [!DNL MongoDB] via le tunnel SSH.
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# Connexion [!DNL MongoDB] via le tunnel SSH

Pour connecter votre [!DNL MongoDB] vers la base de données [!DNL Commerce Intelligence] via un tunnel SSH, il faut faire quelques opérations :

1. [Récupération de la variable [!DNL Commerce Intelligence] clé publique](#retrieve)
1. [Autoriser l’accès au [!DNL Commerce Intelligence] Adresse IP](#allowlist)
1. [Création d’un utilisateur Linux pour Commerce Intelligence](#linux)
1. [Créez un [!DNL MongoDB] utilisateur pour Commerce Intelligence](#mongodb)
1. [Saisissez les informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence]](#finish)

>[!NOTE]
>
>En raison de la nature technique de cette configuration, Adobe vous recommande de faire une boucle dans un développeur pour vous aider si vous ne l’avez pas fait auparavant.

## Récupération de la variable [!DNL Commerce Intelligence] clé publique {#retrieve}

Le `public key` est utilisé pour autoriser la variable [!DNL Commerce Intelligence] `Linux` utilisateur. La section suivante vous guide tout au long de la création de l’utilisateur et de l’importation des clés.

1. Accédez à **[!UICONTROL Data** > **Connections]** et cliquez sur **[!UICONTROL Add New Data Source]**.
1. Cliquez sur le bouton [!DNL MONGODB] icône .
1. Après la [!DNL MongoDB] la page des informations d’identification s’ouvre, modifiez `Encrypted` bascule vers `Yes`. Le formulaire de configuration SSH s’affiche alors.
1. Le `public key` se trouve sous ce formulaire.

Laissez cette page ouverte tout au long du tutoriel. Vous en aurez besoin dans la section suivante et à la fin.

Si vous êtes un peu perdu, voici comment naviguer [!DNL Commerce Intelligence] pour récupérer la clé :

![Récupération de la clé publique RJMetrics](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## Autoriser l’accès au [!DNL Commerce Intelligence] Adresse IP {#allowlist}

Pour que la connexion soit établie, vous devez configurer votre pare-feu pour autoriser l’accès à partir de vos adresses IP. Ils sont `54.88.76.97` et `34.250.211.151`, mais il est également activé sur la variable [!DNL MongoDB] page des informations d’identification :

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Création d’un `Linux` user pour [!DNL Commerce Intelligence] {#linux}

>[!IMPORTANT]
>
>Si la variable `sshd_config` Le fichier associé au serveur n’est pas défini sur l’option par défaut, seuls certains utilisateurs disposent d’un accès au serveur, ce qui empêche une connexion réussie à [!DNL Commerce Intelligence]. Dans ce cas, il est nécessaire d’exécuter une commande comme `AllowUsers` pour autoriser le `rjmetric` accès utilisateur au serveur.

Il peut s’agir d’une machine de production ou secondaire, à condition qu’elle contienne des données en temps réel (ou fréquemment mises à jour). Vous pouvez restreindre cet utilisateur comme vous le souhaitez tant qu&#39;il conserve le droit de se connecter au [!DNL MongoDB] serveur.

Pour ajouter le nouvel utilisateur, exécutez les commandes suivantes en tant que root sur votre `Linux` server :

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

Mémoriser `public key` avez-vous récupéré dans la première section ? Pour vous assurer que l’utilisateur a accès à la base de données, vous devez importer la clé dans `authorized_keys`. Copiez la clé entière dans le `authorized_keys` comme suit :

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

Pour terminer la création de l’utilisateur, modifiez les autorisations du répertoire /home/jmetric pour autoriser l’accès via SSH :

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## Création d’une [!DNL Commerce Intelligence] [!DNL MongoDB] user {#mongodb}

[!DNL MongoDB] Les serveurs comportent deux modes d’exécution : [une avec l’option &quot;auth&quot;](#auth) `(mongod -- auth)` et un sans, [qui est la valeur par défaut](#default). Les étapes de création d’un [!DNL MongoDB] l’utilisateur varie en fonction du mode utilisé par votre serveur. Veillez à vérifier le mode avant de continuer.

### Si votre serveur utilise la variable `Auth` Option : {#auth}

Lors de la connexion à plusieurs bases de données, vous pouvez ajouter l’utilisateur en vous connectant à [!DNL MongoDB] en tant qu’utilisateur administrateur et en exécutant les commandes suivantes.

>[!NOTE]
>
>Pour afficher toutes les bases de données disponibles, la variable [!DNL Commerce Intelligence] l’utilisateur a besoin des autorisations pour s’exécuter. `listDatabases.`

Cette commande permet d’octroyer le [!DNL Commerce Intelligence] accès utilisateur `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

Utilisez cette commande pour accorder la variable [!DNL Commerce Intelligence] accès utilisateur `to a single database`:

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

Si votre serveur n’utilise pas `auth` , votre [!DNL MongoDB] est accessible même sans nom d’utilisateur ni mot de passe. Cependant, vous devez vous assurer que la variable `mongodb.conf` fichier `(/etc/mongodb.conf)` contient les lignes suivantes. dans le cas contraire, redémarrez votre serveur une fois que vous les avez ajoutées.

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

Pour lier votre [!DNL MongoDB] sur une autre adresse du serveur, ajustez le nom d’hôte de la base de données en conséquence à l’étape suivante.

## Saisie des informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence] {#finish}

Pour terminer, vous devez saisir les informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence]. Avez-vous quitté le [!DNL MongoDB] la page des informations d’identification s’ouvre ? Si ce n’est pas le cas, accédez à **[!UICONTROL Data > Connections]** et cliquez sur **[!UICONTROL Add New Data Source]**, puis la variable [!DNL MongoDB] icône . N’oubliez pas de modifier la variable `Encrypted` bascule vers `Yes`.

Renseignez les informations suivantes dans cette page, en commençant par le `Database Connection` section :

* `Host`: `127.0.0.1`
* `Username`: Le [!DNL Commerce Intelligence] [!DNL MongoDB] nom d’utilisateur (doit être `rjmetric`)
* `Password`: Le [!DNL Commerce Intelligence] [!DNL MongoDB] password
* `Port`: Port de MongoDB sur votre serveur (`27017` par défaut)
* `Database Name` (Facultatif) : Si vous n’avez autorisé l’accès qu’à une seule base de données, indiquez son nom ici.

Sous , `SSH Connection` section :

* `Remote Address`: L’adresse IP ou le nom d’hôte du serveur vers lequel vous allez SSH
* `Username`: Le [!DNL Commerce Intelligence] Nom d’utilisateur Linux (SSH) (doit être jmetric)
* `SSH Port`: Le port SSH sur votre serveur (22 par défaut)

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save Test]** pour terminer la configuration.

### Associé

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
