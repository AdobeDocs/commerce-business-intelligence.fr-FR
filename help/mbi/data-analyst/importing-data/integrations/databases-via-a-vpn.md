---
title: Connexion de bases de données via VPN
description: Découvrez comment connecter des bases de données via VPN au lieu du tunnel SSH.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Connexion de bases de données via VPN

Bien qu’Adobe vous recommande de connecter vos bases de données à l’aide d’un tunnel SSH, vous pouvez également utiliser une connexion VPN chiffrée pour maintenir la sécurité. A `VPN` peut être utilisé pour n’importe quelle intégration de base de données. Pour simplifier les choses, le processus est à peu près identique à la configuration d’une `SSH tunnel`:

1. [Créez un [!DNL MBI] utilisateur de base de données](#database)
1. [Créez un [!DNL MBI] Utilisateur VPN](#vpn)
1. [Autoriser l’accès au [!DNL MBI] Adresse IP](#allowlist)
1. [Saisissez les informations de connexion et d’utilisateur VPN dans MBI.](#finish)

Outre les informations d’identification de base de données, vous devez saisir les informations d’identification d’un utilisateur VPN pour terminer. Tout utilisateur VPN fonctionne, mais Adobe vous recommande de créer un [!DNL MBI] user : facilite le suivi des utilisateurs sur votre compte.

## Création d’un utilisateur de base de données pour [!DNL MBI] {#database}

Le processus de création d’un utilisateur de base de données varie en fonction du type de base de données que vous connectez. Pour afficher les instructions pour chaque type de base de données, cliquez sur les liens ci-dessous.

* [Microsoft](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## Création d’un `VPN` user pour [!DNL MBI] {#vpn}

Comme mentionné précédemment, tout `VPN` l’utilisateur fonctionne, mais Adobe vous recommande de créer un utilisateur uniquement pour [!DNL MBI] utilisez .

## Autoriser l’accès au [!DNL MBI] Adresses IP {#allowlist}

Pour que la connexion soit établie, vous devez configurer votre pare-feu pour autoriser l’accès à partir de vos adresses IP. Ils sont `54.88.76.97` et `34.250.211.151`, mais il est également activé sur la variable `credentials` pour toute intégration de base de données :

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Entrer dans la connexion et `VPN` informations sur l’utilisateur [!DNL MBI] {#finish}

Pour terminer, vous devez saisir les informations de connexion et d’utilisateur dans [!DNL MBI]. Avez-vous quitté la base de données `credentials` ouverture de la page ? Si ce n’est pas le cas, accédez à **[!UICONTROL Manage Data** > **Connections]** et cliquez sur **[!UICONTROL Add New Data Source]**, puis l’icône de la base de données que vous connectez. N’oubliez pas de modifier la variable `Encrypted` bascule vers `Yes`.

Renseignez les informations suivantes dans cette page, en commençant par le `Database Connection` section :

* `Username`: Nom d’utilisateur de la variable [!DNL MBI] utilisateur de base de données
* `Password`: Le mot de passe du [!DNL MBI] utilisateur de base de données
* `Port`: Port de la base de données sur votre serveur. Les valeurs par défaut sont les suivantes :
* `MicrosoftSQL`: `1433`
* `MongoDB`: `27017`
* `MySQL`: `3306`
* `PostgreSQL`: `5432`
* `Host`: Par défaut, il s’agit de localhost `127.0.0.1`, mais il peut également s’agir de l’adresse IP publique de votre serveur ou d’une adresse réseau locale.
* `Database Name (optional)`: Si vous n&#39;avez autorisé l&#39;accès qu&#39;à une seule base de données (cette information est indiquée lors de l&#39;étape de création de l&#39;utilisateur de la base de données), indiquez son nom dans cette zone.

Sous , `Encryption Connection` section :

* `Encryption Type`: Définissez cette variable sur `Cisco IPsec VPN`
* `Gateway Address`: Adresse IP du serveur VPN
* `Group Name`: Nom du groupe utilisé pour l’authentification de groupe.
* `Group Secret`: Mot de passe correspondant au groupe.
* `Username`: Le [!DNL MBI] `VPN` username
* `Password`: Le [!DNL MBI] `VPN` mot de passe utilisateur

C&#39;est tout ! Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save & Test]** pour terminer la configuration.
