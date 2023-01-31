---
title: Connexion à vos données
description: Découvrez comment parcourir les tables disponibles pour la synchronisation dans Data Warehouse Manager.
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---

# Connexion à vos données

Dans [!DNL MBI], les sources de données sont appelées `integrations`. Après une `integration` est correctement connecté, vous pourrez parcourir les tables disponibles pour la synchronisation dans Data Warehouse Manager.

Les intégrations sont ajoutées et gérées à l’aide de la variable `Connections` , accessible en cliquant sur **[!UICONTROL Manage Data** > **Connections]**. Vous trouverez ici une liste de toutes les intégrations connectées à votre compte, le type d’intégration, l’état ([!DNL Google Analytics] et [!DNL Data Import API] les connexions auront des champs d’état vides) et la dernière fois qu’un test de connexion (`Last Connection` (colonne Démarré) a été effectuée.

![Data\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## Types d’intégrations

Il existe quatre façons de transférer vos données dans [!DNL MBI]: connexion à une base de données, connexion à une intégration SaaS, chargement d’un `.csv` ou utilisez notre API.

## Intégrations de base de données

![Database\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL MBI] prend en charge les bases de données SQL et NoSQL, telles que [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [Microsoft SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md), et [PostgreSQL](../integrations/postgresql.md).

Vous pouvez connecter directement votre base de données à [!DNL MBI] en utilisant les informations d’identification de base de données, nous vous recommandons d’utiliser une méthode de chiffrement éprouvée comme un tunnel SSH. Cela garantit la sécurité et la sécurité de vos données lors de leur entrée dans votre entrepôt de données.

Selon la méthode de connexion et le type de base de données, une expertise technique peut être nécessaire pour terminer la configuration.

## `SaaS` Intégrations

![](../../../assets/SaaS_icons.jpg)

`SaaS` intégrations sont des services comme [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md), et [[!DNL Zendesk]](../integrations/zendesk.md). Il est important de noter que, puisque les données tierces résident sur le serveur du fournisseur, vous ne pouvez pas y accéder directement comme vous le pouvez avec les données de votre base de données.

Dans la plupart des cas, la configuration d’une intégration dans [!DNL MBI] est aussi facile que de simplement saisir les informations d’identification de votre compte. Certains services peuvent avoir besoin d’une clé API pour terminer l’autorisation. Extrayez le [section intégrations](../integrations/integrations.md) pour obtenir des instructions sur la génération des informations d’identification dont vous avez besoin.

## Téléchargement du fichier

Vous ne savez pas comment obtenir des données d’une source supplémentaire dans votre entrepôt de données ? [En utilisant la variable `File Upload` fonctionnalité](../connecting-data/using-file-uploader.md) est un bon moyen d’extraire des données dont vous n’avez pas besoin pour prendre des décisions quotidiennes. En suivant nos règles de mise en forme, vous pouvez rapidement télécharger des `.csv` dans votre entrepôt de données et rejoignez-les avec d’autres sources de données.

## [!DNL MBI] `Import API`

Si vous préférez automatiser la récupération des données à partir d’une de vos propres sources, vous pouvez utiliser la variable [!DNL MBI] `Import API`. Fondamentalement : s’il ne se trouve pas dans une base de données ou une `SaaS` l’intégration, `Import API` est votre meilleure option.

L’utilisation de l’API nécessite un peu d’expertise technique : une personne qui sait écrire et gérer un petit script Ruby ou PHP sera plus que qualifiée.

Pour en savoir plus sur la prise en main de la méthode `Import API`, extrayez le [Site de développement](https://developer.adobe.com/commerce/services/reporting/) et [Comment générer une clé API](https://developer.adobe.com/commerce/services/reporting/import-api/).

## Ajout d’une intégration

Pour ajouter une intégration, cliquez sur **[!UICONTROL Manage Data** > **Connections]** puis cliquez sur **[!UICONTROL Add a New Data Source]**. Cliquez sur l’icône de l’intégration que vous souhaitez ajouter et suivez les instructions de nos articles d’aide pour configurer les éléments :

* [FAQ sur l’intégration](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [Disponible ](../integrations/integrations.md)
* [Consolidation des tableaux](../../../best-practices/consolidating-your-tables.md)
* [Limitation de l’accès à votre base de données](../../../administrator/account-management/restrict-db-access.md)

**Vous ne voyez pas une intégration que vous souhaitez ?** Certaines intégrations doivent être activées pour qu’elles soient visibles dans votre compte. Si vous recherchez quelque chose, par exemple : [!DNL Facebook] - mais il n&#39;est pas répertorié, [envoi d’un ticket d’assistance](../../../guide-overview.md).

**Si un état d’erreur s’affiche pour une intégration**, ne paniquez pas - consultez la [Section de dépannage](https://support.magento.com/hc/en-us/sections/360003078151) pour obtenir de l’aide.
