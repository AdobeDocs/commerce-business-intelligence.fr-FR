---
title: Data Warehouse Manager
description: Découvrez comment gérer les paramètres de synchronisation des tableaux et des colonnes, analyser en profondeur le schéma d’un tableau et créer des colonnes calculées à utiliser dans les rapports.
exl-id: b9577919-0db0-47f1-a426-1abe48443ac0
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 0%

---

# Data Warehouse Manager

>[!NOTE]
>
>Nécessite des [autorisations d’administrateur](../../administrator/user-management/user-management.md)

Data Warehouse Manager, accessible en cliquant sur **[!UICONTROL Manage Data > Data Warehouse]**, est le portail de votre Data Warehouse [!DNL Adobe Commerce Intelligence]. À l’aide du gestionnaire Data Warehouse, vous pouvez gérer les paramètres de synchronisation des tableaux et des colonnes, explorer le schéma d’un tableau et créer des colonnes calculées à utiliser dans les rapports.

Cette rubrique aborde les sujets suivants :

* [Apprendre à vous y retrouver](#learning)
* [Synchroniser les tableaux et les colonnes](#syncing)
* [Créer des colonnes calculées](#calculated)
* [Déposer des tableaux et supprimer des colonnes](#delete)
* [Synchronisation de nouvelles tables en arrière-plan](#syncnew)
* [Alors, quand puis-je utiliser mes nouvelles colonnes ?](#when)

## Apprendre à vous y retrouver {#learning}

Le côté gauche de `Data Warehouse Manager` page contient la liste des tableaux, ce qui vous permet de basculer facilement entre les tableaux. Lorsque vous sélectionnez une table dans la liste, la zone de gestion des tables est renseignée avec le schéma de la table dans laquelle vous pouvez modifier la table sélectionnée.

Dans la liste des tableaux, les tableaux sont regroupés selon leur source de connexion. Ces sources sont ajoutées sous [!UICONTROL Manage Data > Integrations] et peuvent être une base de données, une [API](https://developer.adobe.com/commerce/services/reporting/) ou un connecteur tiers. En haut de la liste des tableaux se trouve une zone de recherche qui permet de trouver facilement les tableaux souhaités.

Sous la zone de recherche, vous voyez deux options : `All Tables` et `Synced Tables`. L’option `All Tables` répertorie toutes les tables que vous avez mises à la disposition de votre Data Warehouse, ce qui inclut les tables synchronisées et non synchronisées.

L’option `Synced Tables` affiche toutes les tables qui ont déjà été ajoutées à votre Data Warehouse et dont les données sont répliquées à partir des colonnes sélectionnées.

Le tableau que vous recherchez n’apparaît-il pas dans la liste `All Tables` ? Il existe plusieurs raisons possibles à cela :

* La source de données n’a pas encore été ajoutée
* La source de données est une base de données et l’utilisateur [!DNL Commerce Intelligence] que vous avez créé n’a pas accès à cette dernière. Dans ce cas, vous ou votre administrateur de base de données devez accorder l’accès.
* La source de données ou la table a été ajoutée récemment et n&#39;a pas encore été synchronisée

## Synchroniser les tableaux et les colonnes {#syncing}

### Synchronisation des nouvelles tables et des colonnes natives

Data Warehouse Manager vous permet non seulement d’afficher et de gérer facilement vos sources de données, mais également de sélectionner librement les tables et colonnes individuelles à synchroniser.

1. Cliquez sur l’option `All Tables` et recherchez la table que vous souhaitez synchroniser.
1. Cliquez sur le nom de la table pour prévisualiser le schéma. Si le tableau est nouveau, toutes les colonnes s’affichent sous la forme `Unsynced`.
1. Cochez les colonnes à synchroniser.

   >[!NOTE]
   >
   >Les colonnes natives d&#39;une table ont De votre base de données dans la colonne `Location`.

1. Veillez à vérifier les colonnes `Primary Key` : ces colonnes comportent un symbole de clé en regard du nom de la colonne. Un `Primary Key` est nécessaire pour synchroniser correctement les données dans le Data Warehouse.

   Si vous synchronisez une table qui provient directement de votre base de données, il est possible que `Primary Keys` ne soit pas indiqué. Dans ce cas, contactez votre administrateur de base de données pour demander qu&#39;une ou plusieurs clés primaires soient ajoutées à la table.
1. Lorsque vous avez terminé, cliquez sur le bouton ![button](../../assets/button.png).

Un *Succès !* message s’affiche et le statut passe à `Pending` pour les colonnes sélectionnées. Une fois la prochaine mise à jour complète terminée, les tableaux et colonnes nouvellement synchronisés pourront être utilisés dans les rapports. Vous pouvez également définir de nouvelles [méthodes de réplication](./cfg-replication-methods.md) après la synchronisation initiale.

Voici un aperçu rapide de l’ensemble du processus :

![Ajout de colonnes à votre entrepôt de données](../../assets/DW_sync.gif)

### Synchronisation de nouvelles tables en arrière-plan {#syncnew}

Lorsque vous synchronisez une table volumineuse pour la première fois, votre Data Warehouse doit capturer rétroactivement tous les points de données de la table avant de capturer de nouvelles données de manière continue. Si votre tableau est volumineux, il se peut que vous ne souhaitiez pas que cette synchronisation initiale s’exécute en séquence avec votre **cycle de mise à jour**. Dans ce cas, vous souhaitez que la synchronisation initiale se produise en arrière-plan, en *parallèle* avec toute mise à jour en cours d’exécution.

Pour ce faire, sélectionnez l’option `Save and Sync Data Immediately` la synchronisation de ce tableau pour la première fois.

### Recherche de nouveaux tableaux et colonnes {#forceupdate}

Votre Data Warehouse ne détecte pas automatiquement les nouvelles sources, tableaux ou colonnes au moment de leur ajout. Un processus de synchronisation s&#39;exécute toute la semaine pour rechercher de nouveaux ajouts et les rendre disponibles, mais vous pouvez forcer une synchronisation de structure si vous souhaitez accéder aux nouvelles tables et colonnes ajoutées avant l&#39;exécution du processus.

Sous la barre de recherche de la liste du tableau se trouve un lien `Check for new tables and columns` . Cliquer sur ce lien force le démarrage du processus de synchronisation de la structure. Les nouveaux ajouts sont généralement disponibles après 10 minutes. Actualisez la page pour afficher la nouvelle source, le nouveau tableau ou la nouvelle colonne.

## Création de colonnes calculées {#calculated}

Le simple fait d’être en mesure d’afficher et de gérer les données provenant de toutes vos sources facilite d’autant plus l’obtention d’informations sur votre entreprise. Mais dans Data Warehouse Manager, vous pouvez aller plus loin en créant des colonnes calculées dans vos tableaux. `Calculated` colonnes obtiennent de nouvelles informations à partir de vos données existantes.

Supposons que vous souhaitiez ajouter des `user's lifetime revenue` à votre tableau de `users` pour trouver des utilisateurs à forte valeur ajoutée. Ou, si vous souhaitez segmenter les revenus par genre, vous pouvez ajouter des `customer's gender` à votre tableau de `orders`.

Pour plus d’informations, consultez ce [tutoriel](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

## Déposer des tableaux et supprimer des colonnes {#delete}

Tout comme vous pouvez sélectionner des tableaux et des colonnes à synchroniser avec votre Data Warehouse, vous pouvez également les déposer ou les supprimer.

>[!NOTE]
>
>Le fait de déposer un tableau ou de supprimer des colonnes supprime tous les rapports, mesures, ensembles de filtres et colonnes dépendants une fois que vous avez confirmé la suppression. Assurez-vous de vouloir procéder comme suit : **cette action ne peut pas être annulée.**

Ne vous inquiétez pas si vous cliquez sur **[!UICONTROL Delete]** par accident. Une vérification des dépendances s’exécute avant la suppression de quoi que ce soit, vous avez donc la possibilité de tout examiner avant de confirmer.

Pour supprimer des colonnes, cliquez sur le tableau auquel la colonne appartient. Vérifiez les colonnes à supprimer, puis cliquez sur le bouton ![button\_1.png](../../assets/button_1.png).

Pour supprimer un tableau synchronisé, sélectionnez toutes les colonnes du tableau, puis cliquez de nouveau sur le bouton ![bouton](../../assets/button_1.png). Toutes les colonnes natives et calculées qui utilisent ce tableau sont ainsi supprimées de votre Data Warehouse.

### Confirmation des modifications

Que vous supprimiez une table ou des colonnes, une vérification des dépendances s’exécute avant la fin du processus de suppression. Les dépendances sont des colonnes calculées, des mesures, des ensembles de filtres et des rapports qui utilisent le tableau ou les colonnes supprimés. Toutes les dépendances découvertes s’affichent. À ce stade, vous pouvez soit annuler le processus, soit cliquer sur **[!UICONTROL Confirm Changes]** pour supprimer le tableau ou les colonnes.

Bien que les dépendances supprimées ne puissent pas être restaurées, les tableaux et colonnes seront toujours disponibles si vous devez resynchroniser des colonnes natives à l’avenir.

Voici un aperçu rapide de la suppression d’une colonne :

![Supprimer une colonne de votre entrepôt de données](../../assets/DW_delete.gif)

## Alors, quand puis-je utiliser mes nouvelles colonnes ? {#when}

Les nouvelles colonnes synchronisées et les colonnes calculées nouvelles/mises à jour seront prêtes à l’emploi une fois la prochaine mise à jour complète terminée. Si une mise à jour n’est pas déjà en cours, vous pouvez forcer une mise à jour en cliquant sur **[!UICONTROL Force update]** affiché en haut de la page de `Data Warehouse` ou de `Integrations`. Vous pouvez également planifier une notification par e-mail à la fin de la mise à jour en cliquant sur **[!UICONTROL Email me when complete]**.

Lorsque vous êtes prêt à utiliser vos nouvelles colonnes dans les rapports, [vous devez d’abord les ajouter aux mesures](../data-warehouse-mgr/manage-data-dimensions-metrics.md). Bien que les données ne soient pas disponibles avant la fin de la mise à jour, vous pouvez toujours utiliser de nouvelles colonnes dans les rapports. Les données du rapport s’affichent une fois la mise à jour terminée.

## Conclusion

Cet article couvrait beaucoup de sujets. Vous devriez avoir une bonne compréhension de ce qu&#39;est une base de données, de l&#39;organisation des données, de la relation entre les tables et de ce que vous pouvez faire avec Data Warehouse Manager.

Testez vos connaissances en [créant une colonne calculée](../data-warehouse-mgr/creating-calculated-columns.md) ou [en créant des rapports intéressants](../../tutorials/using-visual-report-builder.md).
