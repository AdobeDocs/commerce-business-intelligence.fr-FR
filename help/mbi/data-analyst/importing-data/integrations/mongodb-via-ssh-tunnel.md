---
title: Connexion [!DNL MongoDB] via le tunnel SSH
description: Découvrez comment vous connecter [!DNL MongoDB] via le tunnel SSH.
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# Connexion [!DNL MongoDB] via le tunnel SSH


Pour connecter votre [!DNL MongoDB] vers la base de données [!DNL MBI] via un tunnel SSH, vous (ou votre équipe, si vous n&#39;êtes pas un technicien) devrez effectuer quelques opérations :

1. [Récupération de la variable [!DNL MBI] clé publique](#retrieve)
1. [Autoriser l’accès au [!DNL MBI] Adresse IP](#allowlist)
1. [Création d’un utilisateur Linux pour MBI](#linux)
1. [Créez un [!DNL MongoDB] utilisateur pour MBI](#mongodb)
1. [Saisissez les informations de connexion et d’utilisateur dans [!DNL MBI]](#finish)

>[!NOTE]
>
>En raison de la nature technique de cette configuration, nous vous suggérons de faire une boucle dans un développeur pour vous aider si vous ne l’avez pas fait auparavant.

## Récupération de la variable [!DNL MBI] clé publique {#retrieve}

Le `public key` est utilisé pour autoriser la variable [!DNL MBI] `Linux` utilisateur. Dans la section suivante, nous créons l’utilisateur et importez la clé.

1. Accédez à **[!UICONTROL Data** > **Connections]** et cliquez sur **[!UICONTROL Add New Data Source]**.
1. Cliquez sur le bouton [!DNL MONGODB] icône .
1. Après la [!DNL MongoDB] la page des informations d’identification s’ouvre, modifiez `Encrypted` bascule vers `Yes`. Le formulaire de configuration SSH s’affiche alors.
1. Le `public key` se trouve sous ce formulaire.

Laissez cette page ouverte tout au long du tutoriel. Vous en aurez besoin dans la section suivante et à la fin.

Si vous êtes un peu perdu, voici comment naviguer [!DNL MBI] pour récupérer la clé :

![Récupération de la clé publique RJMetrics](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## Autoriser l’accès au [!DNL MBI] Adresse IP {#allowlist}

Pour que la connexion soit établie, vous devez configurer votre pare-feu afin d’autoriser l’accès à partir de nos adresses IP. Ils sont `54.88.76.97` et `34.250.211.151`, mais il est également activé sur la variable [!DNL MongoDB] page des informations d’identification :

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Création d’un `Linux` user pour [!DNL MBI] {#linux}

>[!IMPORTANT]
>
>Si la variable `sshd_config` Le fichier associé au serveur n’est pas défini sur l’option par défaut, seuls certains utilisateurs auront un accès au serveur, ce qui empêchera une connexion réussie à [!DNL MBI]. Dans ce cas, il est nécessaire d’exécuter une commande comme `AllowUsers` pour autoriser le `rjmetric` accès utilisateur au serveur.

Il peut s’agir d’une machine de production ou secondaire, à condition qu’elle contienne des données en temps réel (ou fréquemment mises à jour). Vous pouvez restreindre cet utilisateur comme vous le souhaitez tant qu&#39;il conserve le droit de se connecter au [!DNL MongoDB] serveur.

Pour ajouter le nouvel utilisateur, exécutez les commandes suivantes en tant que root sur votre `Linux` server :

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

Mémoriser `public key` nous avons récupéré dans la première section ? Pour garantir l’accès de l’utilisateur à la base de données, nous devons importer la clé dans `authorized_keys`. Copiez la clé entière dans le `authorized_keys` comme suit :

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

Pour terminer la création de l’utilisateur, modifiez les autorisations du répertoire /home/jmetric pour autoriser l’accès via SSH :

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## Création d’une [!DNL MBI] [!DNL MongoDB] user {#mongodb}

[!DNL MongoDB] Les serveurs comportent deux modes d’exécution : [une avec l’option &quot;auth&quot;](#auth) `(mongod -- auth)` et un sans, [qui est la valeur par défaut](#default). Les étapes de création d’un [!DNL MongoDB] L’utilisateur varie légèrement en fonction du mode utilisé par votre serveur. Veillez donc à vérifier le mode avant de continuer.

### Si votre serveur utilise la variable `Auth` Option : {#auth}

Lors de la connexion à plusieurs bases de données, vous pouvez ajouter l’utilisateur en vous connectant à [!DNL MongoDB] en tant qu’utilisateur administrateur et en exécutant les commandes suivantes.

>[!NOTE]
>
>Pour afficher toutes les bases de données disponibles, la variable [!DNL MBI] l’utilisateur a besoin des autorisations pour s’exécuter. `listDatabases.`

Cette commande permet d’octroyer le [!DNL MBI] accès utilisateur `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

Utilisez cette commande pour accorder la variable [!DNL MBI] accès utilisateur `to a single database`:

```bash
    use < database name >
    db.createUser('rjmetric', '< secure password here >', true)
```

Cela imprimera une réponse qui ressemble à ceci :

```bash
    {
    "id": ObjectId("< some object id here >"),
    "user": "rjmetric",
    "readOnly": true,
    "pwd": "< some hash here >"
    }
```

### Si votre serveur utilise l’option par défaut {#default}

Si votre serveur n’utilise pas `auth` , votre [!DNL MongoDB] Le serveur sera toujours accessible, même sans nom d’utilisateur et mot de passe. Cependant, vous devez vous assurer que la variable `mongodb.conf` fichier `(/etc/mongodb.conf)` contient les lignes suivantes. dans le cas contraire, redémarrez votre serveur une fois que vous les avez ajoutées.

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

Pour lier votre [!DNL MongoDB] sur une autre adresse du serveur, ajustez le nom d’hôte de la base de données en conséquence à l’étape suivante.

## Saisie des informations de connexion et d’utilisateur dans [!DNL MBI] {#finish}

Pour terminer, nous devons saisir les informations de connexion et d’utilisateur dans [!DNL MBI]. Avez-vous quitté le [!DNL MongoDB] la page des informations d’identification s’ouvre ? Si ce n’est pas le cas, accédez à **[!UICONTROL Data > Connections]** et cliquez sur **[!UICONTROL Add New Data Source]**, puis la variable [!DNL MongoDB] icône . n’oubliez pas de modifier la variable `Encrypted` bascule vers `Yes`.

Renseignez les informations suivantes dans cette page, en commençant par le `Database Connection` section :

* `Host`: `127.0.0.1`
* `Username`: Le [!DNL MBI] [!DNL MongoDB] nom d’utilisateur (doit être `rjmetric`)
* `Password`: Le [!DNL MBI] [!DNL MongoDB] password
* `Port`: Port de MongoDB sur votre serveur (`27017` par défaut)
* `Database Name` (Facultatif) : Si vous n’avez autorisé l’accès qu’à une seule base de données, indiquez son nom ici.

Sous , `SSH Connection` section :

* `Remote Address`: Adresse IP ou nom d’hôte du serveur vers lequel SSH sera envoyé
* `Username`: Le [!DNL MBI] Nom d’utilisateur Linux (SSH) (doit être jmetric)
* `SSH Port`: Le port SSH sur votre serveur (22 par défaut)

C&#39;est tout ! Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save Test]** pour terminer la configuration.

### Associé

* [Réauthentification des intégrations](https://support.magento.com/hc/en-us/articles/360016733151)
