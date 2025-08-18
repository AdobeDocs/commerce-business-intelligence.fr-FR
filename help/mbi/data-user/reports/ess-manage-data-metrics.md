---
title: Création de mesures
description: Découvrez comment utiliser des mesures pour créer des graphiques.
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# Création de mesures

>[!NOTE]
>
>Nécessite des [autorisations d’administrateur](../../administrator/user-management/user-management.md).

Une mesure est une mesure. Dans les structures SQL et de base de données, une mesure est comme une requête stockée sur une période variable.

Dans [!DNL Commerce Intelligence], vous pouvez utiliser des mesures pour [créer des graphiques](../../data-user/reports/ess-rpt-build-visual.md). Par exemple, la mesure `revenue` correspond au nombre total de commandes. La mesure `average customer revenue per order` correspond à ce que dépense le client moyen par commande.

Lorsqu’elles sont utilisées dans des rapports, les mesures peuvent être analysées sur une période spécifiée et [filtrées ou segmentées](../../best-practices/segment-filter.md) par différentes catégories. Pensez à analyser les recettes moyennes des clients regroupées par genre : dans ce cas, `average customer revenue per order` est la mesure et genre est le regroupement.

## Définition de la mesure {#define}

1. Pour créer une mesure, cliquez sur **[!UICONTROL Data** > **Metrics]**.

1. Cliquez sur **[!UICONTROL Create New Metric]**.

1. Dans la liste déroulante, cliquez sur le tableau qui comprend la colonne native ou calculée que vous souhaitez utiliser pour votre mesure.

1. Nommez votre mesure.

   Adobe recommande un nom qui, en un coup d’œil, vous indique quelle est la mesure. Par exemple : `Average Order Revenue`.

1. L’étape suivante consiste à définir la fonction de votre mesure. À l’aide des menus déroulants, définissez l’opération de la mesure, la colonne `operation` et une dimension `date` :

   * Choisissez une opération :
      * `Count` - Cette opération compte le nombre de lignes dans une table de données
      * `Max` - Max renvoie la valeur maximale d’une colonne de données spécifique
      * `Min` - Min renvoie la valeur minimale d’une colonne de données spécifique
      * `Sum` - Cette opération additionne les valeurs d’une colonne de données spécifique
      * `Average` - Cette opération calcule la moyenne des valeurs des colonnes de données
      * `Count Distinct Value` - Compte le nombre unique de valeurs dans une colonne de données spécifique
      * `Median` - Cette opération calcule la médiane des valeurs de la colonne de données
      * `First and Third Quartiles` - Ces opérations calculent respectivement le 25e et le 75e centile des valeurs de la colonne de données
      * `Tenth and Ninetieth Percentiles` - Ces opérations calculent respectivement le 10e et le 90e centile des valeurs de la colonne de données

   * Choisissez une colonne sur laquelle effectuer l’opération. Par exemple, si vous souhaitez trouver votre chiffre d’affaires total, vous devez effectuer une opération de somme sur la colonne `order total`.

     Si vous modifiez une mesure existante, vous pouvez également [modifier le tableau opérationnel de la mesure](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) dans cette section.

   * Choisissez une dimension de date qui peut être utilisée pour suivre la tendance de la mesure. Par exemple, `order date`.

## Ajout de filtres {#filters}

La section `Filter` vous permet de créer un filtre ou d’appliquer un jeu de filtres [enregistré](../../data-user/reports/ess-manage-data-filters.md) à votre mesure.

Pour la mesure `average order revenue`, vous ne souhaitez pas inclure les commandes de test qui ont pu être effectuées lors de la configuration de votre boutique, car le résultat serait inexact. Peut appliquer un jeu de filtres pour supprimer ces commandes du jeu de données. Une fois le filtre créé, il s’applique à tous les graphiques créés à l’aide de cette mesure.

La section `Filter Logic` vous permet de définir plus en détail le comportement d’une mesure.

* « \[`A`\] ou \[`B`\] » autorise toutes les données qui répondent aux filtres \[`A`\] OU \[`B`\]
* « \[`A`\] et \[`B`\] » autorise uniquement les données qui répondent aux deux filtres \[`A`\] et \[`B`\]
* « (\[`A`\] et \[`B`\]) OU \[`C`\] » autorise uniquement les données qui répondent aux deux filtres \[`A`\] et \[`B`\], ou qui répondent aux seuls filtres \[`C`\]

## Ajout de dimensions {#dimensions}

La section [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) affiche toutes les dimensions de données disponibles pour le filtrage ou le regroupement ; par défaut, toutes les colonnes de données disponibles sont répertoriées en tant que dimensions. Pour poursuivre l’exemple, si vous souhaitez segmenter vos revenus par source de recommandation, vous pouvez le faire ici.

En plus de répertorier toutes les colonnes de données disponibles en tant que dimensions, [!DNL Commerce Intelligence] devine dans quelles colonnes les données peuvent être regroupées. *Pour segmenter ou regrouper des données dans des rapports*, les colonnes doivent être marquées comme pouvant être regroupées.

## Achèvement {#finish}

Outre la définition du comportement de votre mesure, vous pouvez définir des niveaux d’autorisation dans la section `User Rights`. Bien que `Admin` utilisateurs aient accès à toutes les mesures, vous devez indiquer les utilisateurs qui peuvent utiliser cette mesure en cochant la case en regard du groupe approprié.

Si vous modifiez une mesure existante, vous pouvez afficher la liste des graphiques (et leurs propriétaires) qui utilisent cette mesure dans la section `Dependent Charts`.

Les modifications sont enregistrées automatiquement et votre mesure est maintenant prête.
