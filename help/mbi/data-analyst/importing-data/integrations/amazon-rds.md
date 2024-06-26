---
title: Connexion à Amazon RDS
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

[!DNL Amazon Relational Database Services (RDS)] est un service de base de données géré qui s’exécute sur des moteurs de base de données que vous connaissez probablement déjà :

* [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)
* [[!DNL PostgreSQL]](../integrations/postgresql.md)

Les étapes de connexion à votre [!DNL RDS] varie selon le type de base de données utilisé et selon que vous utilisez une connexion chiffrée (comme une [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)), mais voici les principes de base.

## Autoriser [!DNL Commerce Intelligence] pour accéder à votre base de données

Sur la page des informations d’identification (**[!UICONTROL Manage Data** > **Integrations]**) pour chaque base de données, une boîte contenant les adresses IP que vous devez autoriser à connecter R[!DNL RDS] to [!DNL Commerce Intelligence]: `54.88.76.97` et `34.250.211.151`. Voici un aperçu de la `MySQL credentials` , où vous avez mis en surbrillance la zone Adresse IP :

![](../../../assets/RDS_IP.png)

Pour [!DNL Commerce Intelligence] pour vous connecter correctement à votre [!DNL RDS] vous devez ajouter ces adresses IP au groupe de sécurité de la base de données approprié via la console de gestion AWS. Ces adresses IP peuvent être ajoutées à un groupe existant ou vous pouvez en créer un. L&#39;important est que le groupe soit autorisé à accéder à l&#39;instance à laquelle vous souhaitez vous connecter. [!DNL Commerce Intelligence].

Lors de l’ajout de la variable [!DNL Commerce Intelligence] Adresses IP, veillez à ajouter une `/32` à la fin de l’adresse à indiquer à [!DNL Amazon] qu’il s’agit d’une adresse IP exacte. Ne vous inquiétez pas : l’interface d’AWS indique clairement que cela est nécessaire.

## Créez un `Linux` user pour [!DNL Commerce Intelligence] {#linux}

>[!NOTE]
>
>Cette étape n’est nécessaire que si vous utilisez une connexion chiffrée. Pour plus d’informations sur la procédure à suivre, reportez-vous à la rubrique de configuration de la base de données que vous utilisez (par exemple : MySQL). La variable `Linux` l’utilisateur nous permet de créer une `SSH tunnel`, qui est la méthode la plus sûre pour envoyer des données sur Internet.

## Créer un utilisateur de base de données pour [!DNL Commerce Intelligence]

Il s’agit de la partie du processus dans laquelle les étapes varient en fonction de la base de données que vous utilisez. L’idée est la même, cependant, vous créez un utilisateur pour [!DNL Commerce Intelligence] qui permet d’accéder à votre base de données. Instructions pour créer une base de données [!DNL Commerce Intelligence] Vous trouverez l’utilisateur dans la rubrique de configuration de la base de données que vous utilisez.

## Saisissez les informations de connexion dans [!DNL Commerce Intelligence]

Après avoir accordé [!DNL Commerce Intelligence] l&#39;accès à votre instance et la création d&#39;un utilisateur pour nous, la dernière chose à faire est d&#39;entrer les informations de connexion dans [!DNL Commerce Intelligence].

Pages d’informations d’identification pour `MySQL`, `Microsoft SQL`, et `PostgreSQL` sont accessibles via le `Integrations` page (**[!UICONTROL Manage Data** > **Integrations]**) en cliquant sur **[!UICONTROL Add Integration]**. Lorsque la liste des intégrations s’affiche, cliquez sur l’icône correspondant à la base de données que vous utilisez pour accéder à la page des informations d’identification. Si vous n’avez actuellement pas accès à l’intégration dont vous avez besoin, contactez votre équipe de compte d’Adobe.

Pour terminer la création de la connexion, vous avez besoin des informations suivantes :

* Adresse publique de votre instance RDS : se trouve dans la section [!DNL AWS] console de gestion.
* Le port utilisé par votre instance de base de données : certaines bases de données possèdent un port par défaut, qui renseigne automatiquement la variable `Port` champ . Ces informations sont également disponibles dans la documentation de configuration de la base de données.
* Nom d’utilisateur et mot de passe de l’utilisateur pour lequel vous avez créé [!DNL Commerce Intelligence].

Si vous utilisez une connexion chiffrée, modifiez la variable `Encrypted` basculez la page des informations d’identification de la base de données sur `Yes`. Un formulaire supplémentaire s’affiche alors pour configurer le chiffrement :

![](../../../assets/sql-integration-encrypted-yes.png)


