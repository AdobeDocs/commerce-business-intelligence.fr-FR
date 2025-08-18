---
title: Connecter Amazon RDS
description: Découvrez les étapes de connexion de votre instance RDS.
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# Connexion [!DNL Amazon RDS]

[!DNL Amazon Relational Database Services (RDS)] est un service de base de données géré qui s&#39;exécute sur des moteurs de base de données que vous connaissez probablement déjà :

* [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)
* [[!DNL PostgreSQL]](../integrations/postgresql.md)

Les étapes de connexion de votre instance [!DNL RDS] varient selon le type de base de données utilisé et selon que vous utilisez ou non une connexion chiffrée (telle qu’une [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)), mais voici les principes de base.

## Autoriser les [!DNL Commerce Intelligence] à accéder à votre base de données

Sur la page des informations d’identification (**[!UICONTROL Manage Data** > **Integrations]**) de chaque base de données, une zone contenant les adresses IP que vous devez autoriser pour connecter R[!DNL RDS] à [!DNL Commerce Intelligence] : `54.88.76.97` et `34.250.211.151` s’affiche. Voici un aperçu de la page `MySQL credentials`, où vous avez mis en surbrillance la zone d’adresse IP :

![](../../../assets/RDS_IP.png)

Pour [!DNL Commerce Intelligence] connecter correctement à votre instance [!DNL RDS], vous devez ajouter ces adresses IP au groupe de sécurité de base de données approprié via la console de gestion AWS. Ces adresses IP peuvent être ajoutées à un groupe existant ou vous pouvez en créer un. L’important est que le groupe soit autorisé à accéder à l’instance à laquelle vous souhaitez vous connecter [!DNL Commerce Intelligence].

Lors de l’ajout des adresses IP [!DNL Commerce Intelligence], veillez à ajouter un `/32` à la fin de l’adresse pour indiquer à [!DNL Amazon] qu’il s’agit d’une adresse IP exacte. Ne vous inquiétez pas, l’interface d’AWS vous indique clairement que cela est nécessaire.

## Créer un utilisateur `Linux` pour [!DNL Commerce Intelligence] {#linux}

>[!NOTE]
>
>Cette étape n’est nécessaire que si vous utilisez une connexion chiffrée. Pour plus d’informations sur la procédure à suivre, reportez-vous à la rubrique de configuration de la base de données que vous utilisez (MySQL, par exemple). L’utilisateur `Linux` nous permet de créer un `SSH tunnel`, qui est la méthode la plus sûre pour envoyer des données sur Internet.

## Créer un utilisateur de base de données pour [!DNL Commerce Intelligence]

Il s’agit de la partie du processus où, selon la base de données que vous utilisez, les étapes varient. L’idée est la même, cependant, vous créez un utilisateur pour [!DNL Commerce Intelligence] qui est utilisé pour accéder à votre base de données. Les instructions relatives à la création d&#39;une base de données [!DNL Commerce Intelligence] d&#39;un utilisateur se trouvent dans la rubrique de configuration de la base de données que vous utilisez.

## Saisir les informations de connexion dans [!DNL Commerce Intelligence]

Après avoir accordé à [!DNL Commerce Intelligence] l’accès à votre instance et créé un utilisateur pour nous, la dernière chose à faire est de saisir les informations de connexion dans [!DNL Commerce Intelligence].

Les pages d’informations d’identification pour `MySQL`, `Microsoft SQL` et `PostgreSQL` sont accessibles via la page `Integrations` (**[!UICONTROL Manage Data** > **Integrations]**) en cliquant sur **[!UICONTROL Add Integration]**. Lorsque la liste des intégrations s&#39;affiche, cliquez sur l&#39;icône de la base de données que vous utilisez pour accéder à la page des informations d&#39;identification. Si vous n’avez pas actuellement accès à l’intégration dont vous avez besoin, contactez l’équipe chargée de votre compte Adobe.

Pour terminer la création de la connexion, vous avez besoin des informations suivantes :

* L’adresse publique de votre instance RDS : elle se trouve dans la console de gestion [!DNL AWS].
* Port utilisé par votre instance de base de données : certaines bases de données disposent d’un port par défaut qui renseigne automatiquement le champ `Port`. Vous trouverez également ces informations dans la documentation relative à la configuration de la base de données.
* Nom d’utilisateur et mot de passe de l’utilisateur que vous avez créé pour [!DNL Commerce Intelligence].

Si vous utilisez une connexion chiffrée, remplacez le bouton `Encrypted` de la page des informations d’identification de la base de données par `Yes`. Un formulaire supplémentaire s’affiche pour configurer le chiffrement :

![](../../../assets/sql-integration-encrypted-yes.png)


