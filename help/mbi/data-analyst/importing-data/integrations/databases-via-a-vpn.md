---
title: Connexion de bases de données via VPN
description: Découvrez comment connecter des bases de données via VPN au lieu du tunnel SSH.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Connexion de bases de données via VPN

Bien qu’Adobe vous recommande de connecter vos bases de données à l’aide d’un `SSH tunnel`, vous pouvez également utiliser une connexion `VPN` chiffrée pour maintenir la sécurité des éléments. Un `VPN` peut être utilisé pour n’importe quelle intégration de base de données et, pour simplifier les choses, le processus est à peu près identique à la configuration d’un `SSH tunnel` :

1. [Création d’un utilisateur de base de données  [!DNL Commerce Intelligence] ](#database)
1. [Créer un utilisateur  [!DNL Commerce Intelligence] VPN](#vpn)
1. [Autoriser l’accès à l’adresse IP  [!DNL Commerce Intelligence] ](#allowlist)
1. [Saisissez les informations de connexion et d’utilisateur VPN dans Commerce Intelligence.](#finish)

Outre les informations d’identification de base de données, vous devez saisir les informations d’identification d’un utilisateur VPN pour terminer. Tout utilisateur VPN fonctionne, mais Adobe vous recommande de créer un utilisateur [!DNL Commerce Intelligence], car cela facilite le suivi des utilisateurs sur votre compte.

## Création d’un utilisateur de base de données pour [!DNL Commerce Intelligence] {#database}

Le processus de création d’un utilisateur de base de données varie en fonction du type de base de données que vous connectez. Pour afficher les instructions pour chaque type de base de données, cliquez sur les liens ci-dessous.

* [MICROSOFT SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## Création d’un utilisateur `VPN` pour [!DNL Commerce Intelligence] {#vpn}

Comme mentionné précédemment, tout utilisateur `VPN` valide fonctionne, mais Adobe vous recommande de créer un utilisateur uniquement pour une utilisation [!DNL Commerce Intelligence].

## Autoriser l’accès aux adresses IP [!DNL Commerce Intelligence] {#allowlist}

Pour que la connexion soit établie, vous devez configurer votre pare-feu pour autoriser l’accès à partir de vos adresses IP. Ils sont `54.88.76.97` et `34.250.211.151`, mais ils se trouvent également sur la page `credentials` pour toute intégration de base de données :

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Saisie de la connexion et des informations sur l&#39;utilisateur `VPN` dans [!DNL Commerce Intelligence] {#finish}

Pour terminer, vous devez saisir les informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence]. Avez-vous laissé la page de base de données `credentials` ouverte ? Dans le cas contraire, accédez à **[!UICONTROL Manage Data** > **Connections]**. Cliquez sur **[!UICONTROL Add New Data Source]**, puis sur l’icône correspondant à la base de données que vous vous connectez. N’oubliez pas de remplacer la bascule `Encrypted` par `Yes`.

Renseignez les informations suivantes dans cette page, en commençant par la section `Database Connection` :

* `Username` : nom d’utilisateur de la base de données [!DNL Commerce Intelligence]
* `Password` : mot de passe de l’utilisateur de base de données [!DNL Commerce Intelligence]
* `Port` : port de la base de données sur votre serveur. Les valeurs par défaut sont :
   * `MicrosoftSQL` : `1433`
   * `MongoDB` : `27017`
   * `MySQL` : `3306`
   * `PostgreSQL` : `5432`
* `Host` : par défaut, il s’agit de localhost `127.0.0.1`, mais il peut également s’agir de l’adresse IP publique de votre serveur ou d’une adresse réseau locale.
* `Database Name (optional)` : si vous n’avez autorisé l’accès qu’à une base de données (cette information est spécifiée lors de l’étape de création de l’utilisateur de base de données), saisissez le nom de cette base de données ici.

Sous la section `Encryption Connection` :

* `Encryption Type` : Définissez ceci sur `Cisco IPsec VPN`
* `Gateway Address` : adresse IP du serveur VPN
* `Group Name` : nom du groupe utilisé pour l’authentification de groupe
* `Group Secret` : mot de passe correspondant au groupe.
* `Username` : nom d’utilisateur [!DNL Commerce Intelligence] `VPN`
* `Password` : mot de passe de l’utilisateur [!DNL Commerce Intelligence] `VPN`

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save & Test]** pour terminer la configuration.
