---
title: Connecter vos données
description: Découvrez comment parcourir les tables disponibles pour synchronisation dans le Gestionnaire Data Warehouse.
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# Connecter vos données

En [!DNL Adobe Commerce Intelligence], les sources de données sont appelées `integrations`. Une fois la connexion d’un `integration` établie, vous pourrez parcourir les tables disponibles pour synchronisation dans le gestionnaire Data Warehouse.

Les intégrations sont ajoutées et gérées à l’aide de la page `Connections`, accessible en cliquant sur **[!UICONTROL Manage Data** > **Connections]**. Ici, vous voyez :

* une liste de toutes les intégrations connectées à votre compte .

* le type d’intégration

* statut (les connexions [!DNL Google Analytics] et [!DNL Data Import API] ont des champs de statut vides)

* la dernière fois qu’un test de connexion (colonne `Last Connection Started`) a été effectué

![Data\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## Types d’intégrations

Il existe quatre façons d’intégrer vos données dans [!DNL Commerce Intelligence] : connecter une base de données, connecter une intégration SaaS, charger un fichier `.csv` ou utiliser l’API Adobe.

## Intégrations de base de données

![Database\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL Commerce Intelligence] prend en charge les bases de données SQL et NoSQL telles que [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [Microsoft SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md) et [PostgreSQL](../integrations/postgresql.md).

Bien que vous puissiez connecter directement votre base de données à [!DNL Commerce Intelligence] à l’aide des informations d’identification de base de données, Adobe vous recommande d’utiliser une méthode de chiffrement éprouvée telle qu’un tunnel SSH. Cela permet de s’assurer que vos données restent sûres et sécurisées lorsqu’elles arrivent dans votre Data Warehouse.

Selon la méthode de connexion et le type de base de données, une expertise technique peut être nécessaire pour terminer la configuration.

## Intégrations `SaaS`

![](../../../assets/SaaS_icons.jpg)spree-commerce-logo.png

Les intégrations `SaaS` sont des services tels que [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md) et [[!DNL Zendesk]](../integrations/zendesk.md). Comme les données tierces résident sur le serveur du fournisseur, vous ne pouvez pas y accéder directement comme vous le pouvez avec les données de votre base de données.

En règle générale, la configuration d’une intégration dans [!DNL Commerce Intelligence] est aussi simple que la saisie des informations d’identification de votre compte. Certains services peuvent nécessiter une clé API pour terminer l’autorisation. Consultez la [section intégrations](../integrations/integrations.md) pour obtenir des instructions sur la génération des informations d’identification dont vous avez besoin.

## Chargement de fichier

Vous ne savez pas comment obtenir des données d’une source supplémentaire dans votre Data Warehouse ? [L’utilisation de la fonctionnalité `File Upload`](../connecting-data/using-file-uploader.md) est un bon moyen d’extraire des données dont vous n’avez pas besoin pour la prise de décision quotidienne. En suivant les règles de formatage, vous pouvez rapidement charger des fichiers `.csv` dans votre Data Warehouse et les joindre à d’autres sources de données.

## [!DNL Commerce Intelligence] `Import API`

Si vous préférez automatiser la récupération des données de l’une de vos propres sources, vous pouvez utiliser le [!DNL Commerce Intelligence] `Import API` . En gros, s&#39;il n&#39;est pas dans une base de données ou une intégration `SaaS`, la fonction `Import API` est votre meilleur pari.

L&#39;utilisation de l&#39;API nécessite un peu d&#39;expertise technique - quelqu&#39;un qui est à l&#39;aise avec l&#39;écriture et la maintenance d&#39;un petit script Ruby ou PHP est plus que qualifié.

Pour en savoir plus sur la prise en main du `Import API`, consultez le [site destiné aux développeurs](https://developer.adobe.com/commerce/services/reporting/) et [comment générer une clé API](https://developer.adobe.com/commerce/services/reporting/import-api/).

## Ajouter une intégration

Pour ajouter une intégration, cliquez sur **[!UICONTROL Manage Data** > **Connections]**, puis sur **[!UICONTROL Add a New Data Source]**. Cliquez sur l’icône de l’intégration à ajouter et suivez les instructions des rubriques d’aide pour configurer les éléments suivants :

* [FAQ sur l’intégration](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [Available ](../integrations/integrations.md)
* [Consolidation des tables](../../../best-practices/consolidating-your-tables.md)
* [Limitation de l&#39;accès à votre base de données](../../../administrator/account-management/restrict-db-access.md)

**Vous ne voyez pas d’intégration souhaitée ?** Certaines intégrations doivent être activées pour être visibles dans votre compte. Si vous recherchez quelque chose comme [!DNL Facebook] mais qui n’est pas répertorié, [envoyez un ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

**Si le statut d’erreur d’une intégration s’affiche** consultez la [section de dépannage](https://support.magento.com/hc/en-us/sections/360003078151) pour obtenir de l’aide.
