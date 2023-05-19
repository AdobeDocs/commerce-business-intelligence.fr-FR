---
title: Connexion de MySQL via cPanel
description: Découvrez comment connecter MySQL via cPanel.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# Connexion [!DNL MySQL] via [!DNL cPanel]

* [Créez un [!DNL Commerce Intelligence] [!DNL MySQL] utilisateur dans [!DNL cPanel]](#cpanel)
* [Saisissez les informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence]](#finish)

## Accéder à

* [[!DNL MySQL] via le tunnel SSH](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] via une connexion directe](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe] vous recommande d’utiliser SSH ou une autre forme de chiffrement pour sécuriser vos données ! S’il ne s’agit pas d’une option, vous pouvez toujours vous connecter directement. [!DNL Commerce Intelligence] à votre base de données en suivant les instructions de cette rubrique.

Cette rubrique vous guide tout au long des étapes nécessaires pour connecter directement votre [!DNL MySQL] vers la base de données [!DNL Commerce Intelligence] using [!DNL cPanel]. Ce processus peut également être utilisé pour se connecter. [!DNL Adobe Commerce] et toute autre base de données eCommerce basée sur MySQL vers [!DNL Commerce Intelligence].

1. Créez un [!DNL Commerce Intelligence] [!DNL MySQL] utilisateur dans [!DNL cPanel]
1. Saisissez les informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence]

Commencez.

## Création d’une [!DNL Commerce Intelligence] [!DNL MySQL] utilisateur dans [!DNL cPanel] {#cpanel}

1. Connectez-vous à [!DNL cPanel] via votre fournisseur d’hébergement.
1. Cliquez sur **[!UICONTROL [!DNL MySQL] Databases]**, situé dans le `Database` .
1. Faites défiler l’écran vers le bas jusqu’à `Add New User` et créer un utilisateur pour [!DNL Commerce Intelligence]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. Cliquez sur **[!UICONTROL Create User]**.
1. Maintenant que vous avez créé l’utilisateur, vous devez l’associer à une base de données. Revenez au `Add New User` section - voir les paramètres pour `Add User to Database?` C&#39;est ce dont vous avez besoin.
1. Dans le `User` dans la liste déroulante de cette section, sélectionnez l’utilisateur que vous avez créé.
1. Dans le `Database` dans la liste déroulante de cette section, sélectionnez la base de données à laquelle vous souhaitez vous connecter. [!DNL Commerce Intelligence].
1. Cliquez sur **[!UICONTROL Add]**.
1. Lorsque la liste de contrôle des privilèges s’affiche, cochez la case en regard de `SELECT` - tout ceci [!DNL Commerce Intelligence] doit se connecter à votre base de données.

## Saisie des informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence] {#finish}

Pour terminer, vous devez saisir les informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence]. Avez-vous quitté le [!DNL MySQL] la page des informations d’identification s’ouvre ? Si ce n’est pas le cas, accédez à **[!UICONTROL Manage Data** > **Connections]** et cliquez sur **[!UICONTROL Add New Data Source]**, puis la variable [!DNL MySQL] icône .

Renseignez les informations suivantes dans cette page du `Database Connection` section :

* `Username`: Nom d’utilisateur de la variable [!DNL Commerce Intelligence] [!DNL MySQL] user
* `Password`: Le mot de passe du [!DNL Commerce Intelligence] [!DNL MySQL] user
* `Port`: Port de MySQL sur votre serveur (`3306` par défaut)
* `Host`: Adresse publique du `MySQL` server [!DNL Commerce Intelligence] se connecte à . Il s’agit généralement de l’URL que vous utilisez pour vous connecter à `[!DNL cPanel]`.

Si vous utilisez une [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md), vous devez saisir les informations de chiffrement. Définissez la variable `Encrypted` bascule vers `Yes` pour afficher le formulaire.

* `Connection Type`: Définissez cette variable sur `SSH Tunnel`
* `Remote Address`: Adresse IP ou nom d’hôte du serveur [!DNL Commerce Intelligence] tunnel
* `Username`: Nom d’utilisateur de la variable [!DNL Commerce Intelligence] `SSH (Linux)` utilisateur, voir [instructions](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) sur la manière de procéder, si ce n’est déjà fait)
* `SSH Port`: port SSH sur votre serveur (`22` par défaut)

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save & Test]** pour terminer la configuration.

## En rapport :

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
