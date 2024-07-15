---
title: Gestionnaire de Data Warehouse
description: Découvrez comment gérer les paramètres de synchronisation des tableaux et des colonnes, explorer le schéma d’un tableau et créer des colonnes calculées à utiliser dans les rapports.
exl-id: b9577919-0db0-47f1-a426-1abe48443ac0
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 0%

---

# Gestionnaire de Data Warehouse

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../administrator/user-management/user-management.md)

Le Gestionnaire de Data Warehouse, accessible en cliquant sur **[!UICONTROL Manage Data > Data Warehouse]**, est le portail de votre Data Warehouse [!DNL Adobe Commerce Intelligence]. Le Gestionnaire des Data Warehouse vous permet de gérer les paramètres de synchronisation des tableaux et des colonnes, d’explorer en détail le schéma d’un tableau et de créer des colonnes calculées à utiliser dans les rapports.

Cette rubrique traite des sujets suivants :

* [Apprendre à contourner le problème](#learning)
* [Synchronisation des tableaux et des colonnes](#syncing)
* [Créer des colonnes calculées](#calculated)
* [Suppression de tableaux et de colonnes](#delete)
* [Synchronisation de nouveaux tableaux en arrière-plan](#syncnew)
* [Alors, quand puis-je utiliser mes nouvelles colonnes ?](#when)

## Apprendre à contourner le problème {#learning}

Le côté gauche de la page `Data Warehouse Manager` contient la liste des tables, ce qui vous permet de basculer facilement d’une table à l’autre. Lorsque vous sélectionnez un tableau dans la liste, la zone de gestion du tableau s’affiche avec le schéma de la table dans lequel vous pouvez modifier le tableau sélectionné.

Dans la liste des tableaux, les tableaux sont regroupés par source de connexion. Ces sources sont ajoutées sous [!UICONTROL Manage Data > Integrations] et peuvent être soit une base de données, soit une [API](https://developer.adobe.com/commerce/services/reporting/), soit un connecteur tiers. En haut de la liste des tableaux se trouve une zone de recherche qui vous permet de trouver facilement les tableaux de votre choix.

Deux options s’affichent sous la zone de recherche : `All Tables` et `Synced Tables`. L’option `All Tables` répertorie toutes les tables que vous avez mises à la disposition de votre Data Warehouse, qui comprennent les tables synchronisées et non synchronisées.

L’option `Synced Tables` affiche toutes les tables qui ont déjà été ajoutées à votre Data Warehouse et dont les données sont répliquées à partir des colonnes sélectionnées.

Ne voyez-vous pas la table que vous recherchez dans la liste `All Tables` ? Il existe plusieurs raisons à cela :

* La source de données n’a pas encore été ajoutée
* La source de données est une base de données et l’utilisateur [!DNL Commerce Intelligence] que vous avez créé n’a pas accès. Dans ce cas, vous ou votre administrateur de base de données devez accorder l’accès.
* La source de données ou le tableau a récemment été ajouté et n’a pas encore été synchronisé.

## Synchronisation des tableaux et des colonnes {#syncing}

### Synchronisation de nouveaux tableaux et de colonnes natives

Le Gestionnaire de Data Warehouse vous permet non seulement d’afficher et de gérer facilement vos sources de données, mais aussi de sélectionner les tables et colonnes individuelles à synchroniser.

1. Cliquez sur l’option `All Tables` et localisez la table que vous souhaitez synchroniser.
1. Cliquez sur le nom de la table pour prévisualiser le schéma. Si le tableau est nouveau, toutes les colonnes s’affichent sous la forme `Unsynced`.
1. Vérifiez les colonnes à synchroniser.

   >[!NOTE]
   >
   >Les colonnes natives d’un tableau sont de la base de données dans la colonne `Location`.

1. Assurez-vous de vérifier les colonnes `Primary Key` : ces colonnes comportent un symbole clé en regard du nom de la colonne. Un `Primary Key` est nécessaire pour synchroniser correctement les données dans le Data Warehouse.

   Si vous synchronisez une table qui provient directement de votre base de données, il est possible que `Primary Keys` ne soit pas indiqué. Dans ce cas, contactez votre administrateur de base de données pour demander qu’une ou plusieurs clés primaires soient ajoutées à la table.
1. Lorsque vous avez terminé, cliquez sur le bouton ![button](../../assets/button.png) .

Un *Succès !Le message* s’affiche et l’état devient `Pending` pour les colonnes sélectionnées. Une fois la prochaine mise à jour complète terminée, les tableaux et colonnes nouvellement synchronisés pourront être utilisés dans les rapports. Vous pouvez également définir de nouvelles [méthodes de réplication](./cfg-replication-methods.md) après la synchronisation initiale.

Voici un aperçu rapide de l’ensemble du processus :

![Ajout de colonnes à votre entrepôt de données](../../assets/DW_sync.gif)

### Synchronisation de nouveaux tableaux en arrière-plan {#syncnew}

Lorsque vous synchronisez une table volumineuse pour la première fois, votre Data Warehouse doit capturer rétroactivement tous les points de données du tableau avant de capturer de nouvelles données de manière continue. Si votre table est volumineuse, il se peut que vous ne souhaitiez pas que cette synchronisation initiale s’exécute de manière séquentielle avec votre **cycle de mise à jour**. Dans ce cas, vous souhaitez que la synchronisation initiale se produise en arrière-plan, dans *parallel* avec toute mise à jour en cours d’exécution.

Pour vous assurer que cela se produit, vous devez sélectionner l’option `Save and Sync Data Immediately` synchronisant cette table pour la première fois.

### Recherche de nouveaux tableaux et colonnes {#forceupdate}

Votre Data Warehouse ne détecte pas automatiquement les nouvelles sources, tables ou colonnes au moment de leur ajout. Un processus de synchronisation s’exécute toute la semaine pour rechercher de nouveaux ajouts et les rendre disponibles, mais vous pouvez forcer la synchronisation d’une structure si vous souhaitez accéder aux tables et colonnes nouvellement ajoutées avant l’exécution du processus.

Sous la barre de recherche de la liste du tableau se trouve un lien `Check for new tables and columns`. Cliquez sur ce lien pour forcer le démarrage du processus de synchronisation de la structure. Les nouveaux ajouts sont généralement disponibles au bout de 10 minutes. Actualisez la page pour afficher la nouvelle source, le nouveau tableau ou la nouvelle colonne.

## Création de colonnes calculées {#calculated}

Il est beaucoup plus facile d’obtenir des informations sur votre entreprise en étant simplement en mesure de consulter et de gérer les données provenant de toutes vos sources. Mais dans le Gestionnaire de Data Warehouse, vous pouvez aller plus loin en créant des colonnes calculées dans vos tableaux. Les colonnes `Calculated` obtiennent de nouvelles informations de vos données existantes.

Supposons que vous souhaitiez ajouter `user's lifetime revenue` à votre table `users` pour rechercher des utilisateurs de grande valeur. Ou, si vous souhaitez segmenter les recettes par sexe, vous pouvez ajouter `customer's gender` à votre table `orders`.

Pour plus d’informations, consultez ce [tutoriel](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

## Déposer des tableaux et supprimer des colonnes {#delete}

De la même manière que vous pouvez sélectionner des tableaux et des colonnes à synchroniser avec votre Data Warehouse, vous pouvez également les déposer ou les supprimer.

>[!NOTE]
>
>Le fait de déposer un tableau ou de supprimer des colonnes supprime tous les rapports, mesures, ensembles de filtres et colonnes dépendants une fois que vous avez confirmé la suppression. Assurez-vous que vous souhaitez effectuer cette opération : **cette action ne peut pas être annulée.**

Ne vous inquiétez pas si vous cliquez sur **[!UICONTROL Delete]** par accident. Une vérification de dépendance s’exécute avant que tout élément ne soit supprimé. Vous avez donc la possibilité de vérifier tout avant de confirmer.

Pour supprimer des colonnes, cliquez sur le tableau auquel appartient la colonne. Vérifiez les colonnes à supprimer et cliquez sur le bouton ![button\_1.png](../../assets/button_1.png) .

Pour supprimer une table synchronisée, sélectionnez toutes les colonnes de la table, puis cliquez de nouveau sur le bouton ![button](../../assets/button_1.png). Cette opération supprime de votre Data Warehouse toutes les colonnes natives et calculées qui utilisent ce tableau.

### Confirmation des modifications

Que vous déposiez un tableau ou supprimiez des colonnes, une vérification de dépendance s’exécute avant la fin du processus de suppression. Les dépendances sont des colonnes calculées, des mesures, des ensembles de filtres et des rapports qui utilisent le tableau ou les colonnes supprimés. Toutes les dépendances découvertes s’affichent : à ce stade, vous pouvez annuler le processus ou cliquer sur **[!UICONTROL Confirm Changes]** pour déposer la table/supprimer la ou les colonnes.

Bien que les dépendances supprimées ne puissent pas être restaurées, les tableaux et les colonnes seront toujours disponibles si vous devez resynchroniser des colonnes natives à l’avenir.

Voici un aperçu rapide de la suppression d’une colonne :

![Suppression d’une colonne de votre entrepôt de données](../../assets/DW_delete.gif)

## Alors, quand puis-je utiliser mes nouvelles colonnes ? {#when}

De nouvelles colonnes synchronisées et de nouvelles colonnes calculées/mises à jour seront prêtes à être utilisées une fois la prochaine mise à jour complète terminée. Si une mise à jour n&#39;est pas déjà en cours, vous pouvez forcer une mise à jour en cliquant sur **[!UICONTROL Force update]** affiché en haut de la page `Data Warehouse` ou `Integrations`. Vous pouvez également planifier une notification par courrier électronique une fois la mise à jour terminée en cliquant sur **[!UICONTROL Email me when complete]**.

Lorsque vous êtes prêt à utiliser vos nouvelles colonnes dans les rapports, [vous devez d’abord les ajouter aux mesures ](../data-warehouse-mgr/manage-data-dimensions-metrics.md). Bien que les données ne soient pas disponibles tant qu’une mise à jour n’est pas terminée, vous pouvez tout de même utiliser de nouvelles colonnes dans les rapports. Les données du rapport s’affichent lorsque la mise à jour est terminée.

## Remplissage

Cet article a couvert beaucoup de contenu. À l’heure actuelle, vous devez avoir une bonne compréhension de ce qu’est une base de données, de la manière dont les données sont organisées, de la manière dont les tableaux sont interconnectés et de ce que vous pouvez faire avec Data Warehouse Manager.

Testez vos connaissances en [créant une colonne calculée](../data-warehouse-mgr/creating-calculated-columns.md) ou en [ effectuant des rapports intéressants](../../tutorials/using-visual-report-builder.md).
