---
title: Connexion de bases de données via VPN
description: Découvrez comment connecter des bases de données via VPN au lieu du tunnel SSH.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Connexion de bases de données via VPN

Adobe vous recommande de connecter vos bases de données à l’aide d’une `SSH tunnel`, vous pouvez également utiliser un `VPN` connexion pour maintenir la sécurité. A `VPN` peut être utilisé pour n’importe quelle intégration de base de données. Pour simplifier les choses, le processus est à peu près identique à la configuration d’une `SSH tunnel`:

1. [Créez un [!DNL Commerce Intelligence] utilisateur de base de données](#database)
1. [Créez un [!DNL Commerce Intelligence] Utilisateur VPN](#vpn)
1. [Autoriser l’accès au [!DNL Commerce Intelligence] Adresse IP](#allowlist)
1. [Saisissez les informations de connexion et d’utilisateur VPN dans Commerce Intelligence.](#finish)

Outre les informations d’identification de base de données, vous devez saisir les informations d’identification d’un utilisateur VPN pour terminer. Tout utilisateur VPN fonctionne, mais Adobe vous recommande de créer un [!DNL Commerce Intelligence] , car cela facilite le suivi des utilisateurs sur votre compte.

## Créer un utilisateur de base de données pour [!DNL Commerce Intelligence] {#database}

Le processus de création d’un utilisateur de base de données varie en fonction du type de base de données que vous connectez. Pour afficher les instructions pour chaque type de base de données, cliquez sur les liens ci-dessous.

* [MICROSOFT SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## Création d’un `VPN` user pour [!DNL Commerce Intelligence] {#vpn}

Comme mentionné précédemment, tout `VPN` l’utilisateur fonctionne, mais Adobe vous recommande de créer un utilisateur uniquement pour [!DNL Commerce Intelligence] utilisez .

## Autoriser l’accès au [!DNL Commerce Intelligence] Adresses IP {#allowlist}

Pour que la connexion soit établie, vous devez configurer votre pare-feu pour autoriser l’accès à partir de vos adresses IP. Ils sont `54.88.76.97` et `34.250.211.151`, mais il est également activé sur la variable `credentials` pour toute intégration de base de données :

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## la connexion et `VPN` informations sur l’utilisateur [!DNL Commerce Intelligence] {#finish}

Pour terminer, vous devez saisir les informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence]. Avez-vous quitté la base de données `credentials` ouverture de la page ? Dans le cas contraire, accédez à **[!UICONTROL Manage Data** > **Connections]**. Cliquez sur **[!UICONTROL Add New Data Source]**, puis cliquez sur l’icône correspondant à la base de données que vous connectez. N’oubliez pas de modifier la variable `Encrypted` bascule vers `Yes`.

Renseignez les informations suivantes dans cette page, en commençant par le `Database Connection` section :

* `Username`: nom d’utilisateur de la variable [!DNL Commerce Intelligence] utilisateur de base de données
* `Password`: mot de passe de la variable [!DNL Commerce Intelligence] utilisateur de base de données
* `Port`: port de la base de données sur votre serveur. Les valeurs par défaut sont :
   * `MicrosoftSQL`: `1433`
   * `MongoDB`: `27017`
   * `MySQL`: `3306`
   * `PostgreSQL`: `5432`
* `Host`: par défaut, il s’agit de localhost `127.0.0.1`, mais il peut également s’agir de l’adresse IP publique de votre serveur ou d’une adresse réseau locale.
* `Database Name (optional)`: si vous n’avez autorisé l’accès qu’à une seule base de données (cette information est indiquée lors de l’étape de création de l’utilisateur de base de données), saisissez le nom de cette base de données dans ce champ.

Sous , `Encryption Connection` section :

* `Encryption Type`: définissez cette variable sur `Cisco IPsec VPN`
* `Gateway Address`: adresse IP du serveur VPN
* `Group Name`: nom du groupe utilisé pour l’authentification de groupe.
* `Group Secret`: mot de passe correspondant au groupe.
* `Username`: la variable [!DNL Commerce Intelligence] `VPN` username
* `Password`: la variable [!DNL Commerce Intelligence] `VPN` mot de passe utilisateur

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save & Test]** pour terminer la configuration.
