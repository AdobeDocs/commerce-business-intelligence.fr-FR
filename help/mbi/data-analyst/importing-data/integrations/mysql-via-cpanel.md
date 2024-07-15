---
title: Connexion de MySQL via cPanel
description: Découvrez comment connecter MySQL via cPanel.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# Connecter [!DNL MySQL] via [!DNL cPanel]

* [Création d’un utilisateur  [!DNL Commerce Intelligence] [!DNL MySQL] dans [!DNL cPanel]](#cpanel)
* [Entrer les informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence]](#finish)

## Accéder à

* [[!DNL MySQL] via le tunnel SSH](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] via une connexion directe](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe] vous recommande d’utiliser SSH ou une autre forme de cryptage pour sécuriser vos données ! S&#39;il ne s&#39;agit pas d&#39;une option, vous pouvez toujours connecter directement [!DNL Commerce Intelligence] à votre base de données en suivant les instructions de cette rubrique.

Cette rubrique vous guide tout au long des étapes nécessaires pour connecter directement votre base de données [!DNL MySQL] à [!DNL Commerce Intelligence] en utilisant [!DNL cPanel]. Ce processus peut également être utilisé pour connecter [!DNL Adobe Commerce] et toute autre base de données eCommerce basée sur MySQL à [!DNL Commerce Intelligence].

1. Créez un utilisateur [!DNL Commerce Intelligence] [!DNL MySQL] dans [!DNL cPanel]
1. Saisissez les informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence].

Commencez.

## Création d&#39;un utilisateur [!DNL Commerce Intelligence] [!DNL MySQL] dans [!DNL cPanel] {#cpanel}

1. Connectez-vous à [!DNL cPanel] via votre fournisseur d&#39;hébergement.
1. Cliquez sur **[!UICONTROL [!DNL MySQL] Databases]**, situé dans la section `Database`.
1. Faites défiler l’écran jusqu’à la section `Add New User` et créez un utilisateur pour [!DNL Commerce Intelligence] :

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. Cliquez sur **[!UICONTROL Create User]**.
1. Maintenant que vous avez créé l’utilisateur, vous devez l’associer à une base de données. Revenez à la section `Add New User` - voir les paramètres pour `Add User to Database?` C’est ce dont vous avez besoin.
1. Dans la liste déroulante `User` de cette section, sélectionnez l’utilisateur que vous avez créé.
1. Dans la liste déroulante `Database` de cette section, sélectionnez la base de données à laquelle vous souhaitez vous connecter [!DNL Commerce Intelligence].
1. Cliquez sur **[!UICONTROL Add]**.
1. Lorsque la liste de contrôle des privilèges s’affiche, cochez la case en regard de `SELECT`. Il s’agit de tout [!DNL Commerce Intelligence] nécessaire pour se connecter à votre base de données.

## Saisie des informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence] {#finish}

Pour terminer, vous devez saisir les informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence]. Avez-vous laissé la page des informations d’identification [!DNL MySQL] ouverte ? Dans le cas contraire, accédez à **[!UICONTROL Manage Data** > **Connections]** et cliquez sur **[!UICONTROL Add New Data Source]**, puis sur l’icône [!DNL MySQL].

Saisissez les informations suivantes dans cette page dans la section `Database Connection` :

* `Username` : nom d’utilisateur de l’utilisateur [!DNL Commerce Intelligence] [!DNL MySQL]
* `Password` : mot de passe de l’utilisateur [!DNL Commerce Intelligence] [!DNL MySQL]
* `Port` : port de MySQL sur votre serveur (`3306` par défaut)
* `Host` : l’adresse publique du serveur `MySQL` [!DNL Commerce Intelligence] se connecte à . Il s’agit généralement de l’URL que vous utilisez pour vous connecter à `[!DNL cPanel]`.

Si vous utilisez un [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md), vous devez saisir les informations de chiffrement. Définissez la bascule `Encrypted` sur `Yes` pour afficher le formulaire.

* `Connection Type` : Définissez ceci sur `SSH Tunnel`
* `Remote Address` : l’adresse IP ou le nom d’hôte du serveur [!DNL Commerce Intelligence] va s’introduire dans
* `Username` : nom d’utilisateur de l’utilisateur [!DNL Commerce Intelligence] `SSH (Linux)`, voir [instructions](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) sur la manière de procéder, si ce n’est déjà fait)
* `SSH Port` : port SSH sur votre serveur (`22` par défaut)

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save & Test]** pour terminer la configuration.

## En rapport :

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
