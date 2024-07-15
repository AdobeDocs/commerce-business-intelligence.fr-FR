---
title: Création de mesures
description: Découvrez comment utiliser les mesures pour créer des graphiques.
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
>Nécessite [Autorisations d’administrateur](../../administrator/user-management/user-management.md).

Une mesure est une mesure. Dans les structures SQL et de base de données, une mesure est comme une requête stockée sur une période variable.

Dans [!DNL Commerce Intelligence], vous pouvez utiliser des mesures pour [créer des graphiques](../../data-user/reports/ess-rpt-build-visual.md). Par exemple, la mesure `revenue` est le nombre total de commandes. La mesure `average customer revenue per order` correspond à ce que le client moyen dépense par commande.

Lorsqu’elles sont utilisées dans des rapports, les mesures peuvent être analysées sur une période spécifiée et [filtrées ou segmentées](../../best-practices/segment-filter.md) par différentes catégories. Envisagez d’analyser la moyenne des recettes client regroupées par sexe. Dans ce cas, `average customer revenue per order` est la mesure et le genre est le regroupement.

## Définition de la mesure {#define}

1. Pour créer une mesure, cliquez sur **[!UICONTROL Data** > **Metrics]**.

1. Cliquez sur **[!UICONTROL Create New Metric]**.

1. Dans la liste déroulante, cliquez sur le tableau contenant la colonne native ou calculée que vous souhaitez utiliser pour votre mesure.

1. Nommez votre mesure.

   Adobe recommande un nom qui, d’un coup d’oeil, vous indique la mesure. Par exemple : `Average Order Revenue`.

1. L’étape suivante consiste à définir l’action de votre mesure. À l’aide des menus déroulants, définissez l’opération de la mesure, la colonne `operation` et une dimension `date` :

   * Choisissez une opération :
      * `Count` - Cette opération comptabilise le nombre de lignes dans un tableau de données
      * `Max` - Max renvoie la valeur maximale d’une colonne de données spécifique
      * `Min` - Min renvoie la valeur minimale d’une colonne de données spécifique
      * `Sum` - Cette opération additionne les valeurs d’une colonne de données spécifique
      * `Average` - Cette opération calcule la moyenne des valeurs de colonne de données
      * `Count Distinct Value` - Cela comptabilise le nombre unique de valeurs dans une colonne de données spécifique
      * `Median` - Cette opération calcule la médiane des valeurs de colonne de données
      * `First and Third Quartiles` - Ces opérations calculent respectivement le 25e et le 75e percentiles des valeurs de colonne de données.
      * `Tenth and Ninetieth Percentiles` - Ces opérations calculent respectivement les 10e et 90e percentiles des valeurs de colonne de données.

   * Sélectionnez une colonne sur laquelle effectuer l’opération. Par exemple, si vous souhaitez obtenir vos recettes totales, vous effectuez une opération de somme sur la colonne `order total`.

     Si vous modifiez une mesure existante, vous pouvez également [modifier la table opérationnelle de la mesure](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) dans cette section.

   * Sélectionnez une dimension de date pouvant être utilisée pour suivre la tendance de la mesure. Par exemple, `order date`.

## Ajout de filtres {#filters}

La section `Filter` vous permet de créer un filtre ou d’appliquer un [ensemble de filtres enregistrés](../../data-user/reports/ess-manage-data-filters.md) à votre mesure.

Pour la mesure `average order revenue`, vous ne souhaitez pas inclure de commandes de test qui auraient pu être effectuées lors de la configuration de votre boutique. Cela nous donnerait un résultat inexact. Peut appliquer un jeu de filtres pour supprimer ces commandes du jeu de données. Une fois le filtre créé, il s’applique à tous les graphiques créés à l’aide de cette mesure.

La section `Filter Logic` vous permet de définir plus précisément le comportement d’une mesure.

* &quot;\[`A`\] ou \[`B`\]&quot; autorise les données qui répondent aux filtres \[`A`\] OU \[`B`\]
* &quot;\[`A`\] et \[`B`\]&quot; autorisent uniquement les données qui répondent aux deux filtres \[`A`\] et \[`B`\]
* &quot;(\[`A`\] et \[`B`\]) OU \[`C`\]&quot; autorise uniquement les données qui répondent aux deux filtres \[`A`\] et \[`B`\], ou qui répondent seules au filtre \[`C`\]

## Ajout de Dimensions {#dimensions}

La section [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) présente toutes les dimensions de données disponibles pour le filtrage ou le regroupement. Par défaut, toutes les colonnes de données disponibles sont répertoriées comme dimensions. Si vous souhaitez segmenter vos recettes par source de référence dans l’exemple suivant, vous pouvez le faire ici.

Outre la liste de toutes les colonnes de données disponibles sous forme de dimensions, [!DNL Commerce Intelligence] détermine à quelles colonnes peuvent être regroupées. *Pour segmenter ou regrouper des données sur des rapports*, les colonnes doivent être marquées comme pouvant être regroupées.

## Finalisation {#finish}

Outre la définition du comportement de votre mesure, vous pouvez définir des niveaux d’autorisation dans la section `User Rights` . Bien que les utilisateurs de `Admin` aient accès à toutes les mesures, vous devez indiquer les utilisateurs qui peuvent utiliser cette mesure en cochant la case en regard du groupe approprié.

Si vous modifiez une mesure existante, vous pouvez afficher la liste des graphiques (et des propriétaires) qui utilisent cette mesure dans la section `Dependent Charts`.

Les modifications sont enregistrées automatiquement et votre mesure est désormais prête à l’emploi.
