---
title: Connexion à vos données
description: Découvrez comment parcourir les tables disponibles pour la synchronisation dans Data Warehouse Manager.
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# Connexion à vos données

Dans [!DNL Adobe Commerce Intelligence], les sources de données sont appelées `integrations`. Une fois la connexion à `integration` établie, vous pourrez parcourir les tables disponibles pour la synchronisation dans le Gestionnaire de Data Warehouse.

Les intégrations sont ajoutées et gérées à l’aide de la page `Connections`, accessible en cliquant sur **[!UICONTROL Manage Data** > **Connections]**. Ici, vous voyez :

* liste de toutes les intégrations connectées à votre compte

* le type d’intégration

* status ([!DNL Google Analytics] et [!DNL Data Import API] les connexions ont des champs d’état vides)

* la dernière fois qu’un test de connexion (`Last Connection Started` colonne) a été effectué

![Data\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## Types d’intégrations

Il existe quatre méthodes pour intégrer vos données dans [!DNL Commerce Intelligence] : connexion à une base de données, connexion à une intégration SaaS, chargement d’un fichier `.csv` ou utilisation de l’API Adobe.

## Intégrations de base de données

![Base de données\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL Commerce Intelligence] prend en charge les bases de données basées sur SQL et NoSQL telles que [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [Microsoft SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md) et [PostgreSQL](../integrations/postgresql.md).

Bien que vous puissiez directement connecter votre base de données à [!DNL Commerce Intelligence] à l’aide des informations d’identification de la base de données, Adobe vous recommande d’utiliser une méthode de cryptage éprouvée comme un tunnel SSH. Cela garantit la sécurité et la sécurité de vos données lors de leur entrée dans votre Data Warehouse.

Selon la méthode de connexion et le type de base de données, une expertise technique peut être nécessaire pour terminer la configuration.

## `SaaS` Intégrations

![](../../../assets/SaaS_icons.jpg)spree-commerce-logo.png

Les intégrations `SaaS` sont des services tels que [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md) et [[!DNL Zendesk]](../integrations/zendesk.md). Les données tierces résidant sur le serveur du fournisseur, vous ne pouvez pas y accéder directement comme vous le pouvez avec les données de votre base de données.

En règle générale, la configuration d’une intégration dans [!DNL Commerce Intelligence] est aussi simple que de saisir les informations d’identification de votre compte. Certains services peuvent nécessiter une clé API pour terminer l’autorisation. Consultez la [section sur les intégrations](../integrations/integrations.md) pour obtenir des instructions sur la génération des informations d’identification dont vous avez besoin.

## Téléchargement du fichier

Vous ne savez pas comment obtenir des données d’une source supplémentaire dans votre Data Warehouse ? [L’utilisation de la fonction `File Upload`](../connecting-data/using-file-uploader.md) est un bon moyen d’extraire des données dont vous n’avez pas besoin pour prendre des décisions quotidiennes. En suivant les règles de formatage, vous pouvez rapidement charger `.csv` fichiers dans votre Data Warehouse et les joindre à d’autres sources de données.

## [!DNL Commerce Intelligence] `Import API`

Si vous préférez automatiser la récupération des données à partir d&#39;une de vos propres sources, vous pouvez utiliser le [!DNL Commerce Intelligence] `Import API`. En gros, s&#39;il ne se trouve pas dans une base de données ou une intégration `SaaS`, la fonction `Import API` est votre meilleure option.

L’utilisation de l’API nécessite un peu d’expertise technique : une personne qui sait écrire et gérer un petit script Ruby ou PHP est plus que qualifiée.

Pour en savoir plus sur la prise en main de `Import API`, consultez le [site développeur](https://developer.adobe.com/commerce/services/reporting/) et [comment générer une clé API](https://developer.adobe.com/commerce/services/reporting/import-api/).

## Ajout d’une intégration

Pour ajouter une intégration, cliquez sur **[!UICONTROL Manage Data** > **Connections]**, puis sur **[!UICONTROL Add a New Data Source]**. Cliquez sur l’icône de l’intégration que vous souhaitez ajouter et suivez les instructions des rubriques d’aide pour configurer les éléments :

* [FAQ sur l’intégration](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [Disponible ](../integrations/integrations.md)
* [Consolidation des tableaux](../../../best-practices/consolidating-your-tables.md)
* [Limitation de l’accès à votre base de données](../../../administrator/account-management/restrict-db-access.md)

**Vous ne voyez pas une intégration que vous souhaitez ?** Certaines intégrations doivent être activées pour qu’elles soient visibles dans votre compte. Si vous recherchez quelque chose comme [!DNL Facebook] mais qu&#39;il n&#39;est pas répertorié, [soumettez un ticket d&#39;assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

**Si vous voyez un état d’erreur pour une intégration**, consultez la [section de dépannage](https://support.magento.com/hc/en-us/sections/360003078151) pour obtenir de l’aide.
