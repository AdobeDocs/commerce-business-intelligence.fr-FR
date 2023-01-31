---
title: Création de mesures
description: Découvrez comment utiliser les mesures pour créer des graphiques.
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# Création de mesures

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../administrator/user-management/user-management.md).

Autrement dit, une mesure est une mesure. Dans les structures SQL et de base de données, une mesure est comme une requête stockée sur une période variable.

Dans [!DNL MBI], vous pouvez utiliser des mesures pour [créer des graphiques](../../data-user/reports/ess-rpt-build-visual.md). Par exemple, la mesure `revenue` est le montant total des commandes. La mesure `average customer revenue per order` est ce que le client moyen dépense par commande.

Lorsqu’elles sont utilisées dans des rapports, les mesures peuvent être analysées sur une période spécifiée et [filtré ou segmenté](../../best-practices/segment-filter.md) par différentes catégories. Envisagez d’analyser les recettes moyennes des clients regroupées par sexe, dans ce cas, `average customer revenue per order` est la mesure et le genre est le regroupement.

## Définition de la mesure {#define}

1. Pour créer une mesure, cliquez sur **[!UICONTROL Data** > **Metrics]**.

1. Cliquez sur **[!UICONTROL Create New Metric]**.

1. Dans la liste déroulante, cliquez sur le tableau contenant la colonne native ou calculée que vous souhaitez utiliser pour votre mesure.

1. Nommez votre mesure.

   Nous vous recommandons un nom qui, d’un seul coup d’oeil, vous indique la mesure. Par exemple : `Average Order Revenue`.

1. L’étape suivante consiste à définir l’action de votre mesure. À l’aide des menus déroulants, définissez l’opération de la mesure, la variable `operation` et une `date` dimension :

   * Choisissez une opération :
      * `Count` - Cette opération comptabilise le nombre de lignes dans un tableau de données.
      * `Max` - Max. renvoie la valeur maximale d’une colonne de données spécifique
      * `Min` - Min renvoie la valeur minimale d’une colonne de données spécifique
      * `Sum` - Cette opération additionne les valeurs d’une colonne de données spécifique
      * `Average` - Cette opération calcule la moyenne des valeurs des colonnes de données.
      * `Count Distinct Value` : cela comptabilise le nombre unique de valeurs dans une colonne de données spécifique.
      * `Median` - Cette opération calcule la médiane des valeurs de colonne de données.
      * `First and Third Quartiles` - Ces opérations calculent respectivement les 25e et 75e percentiles des valeurs de colonne de données.
      * `Tenth and Ninetieth Percentiles` - Ces opérations calculent respectivement les 10e et 90e percentiles des valeurs de colonne de données.
   * Sélectionnez une colonne sur laquelle effectuer l’opération. Par exemple, si vous souhaitez obtenir le total de vos recettes, vous devez effectuer une opération de somme sur la variable `order total` colonne .

      Si vous modifiez une mesure existante, vous pouvez également [modifier le tableau opérationnel de la mesure ;](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) dans cette section.

   * Sélectionnez une dimension de date pouvant être utilisée pour suivre la tendance de la mesure. Par exemple : `order date`.


## Ajout de filtres {#filters}

Le `Filter` vous permet de créer un filtre ou d’appliquer un [jeu de filtres enregistré](../../data-user/reports/ess-manage-data-filters.md) à votre mesure.

Pour notre `average order revenue` , nous ne souhaitons pas inclure de commandes de test qui auraient pu être effectuées lors de la configuration de notre magasin ; cela nous donnerait un résultat inexact. Nous pouvons appliquer un ensemble de filtres pour supprimer ces commandes du jeu de données. Une fois le filtre créé, il s’applique à tous les graphiques créés à l’aide de cette mesure.

Le `Filter Logic` vous permet de définir plus précisément le comportement d’une mesure.

* &quot;\[`A`\] ou \[`B`\]&quot; autorise toutes les données qui répondent aux filtres \[`A`\] OU \[`B`\]
* &quot;\[`A`\] et \[`B`\]&quot; autorise uniquement les données qui répondent aux deux filtres \[`A`\] et \[`B`\]
* &quot;(\[`A`\] et \[`B`\]) OU \[`C`\]&quot; autorise uniquement les données qui répondent aux deux filtres \[`A`\] et \[`B`\] ou satisfait le filtre \[`C`\] seul

## Ajout de Dimensions {#dimensions}

Le [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) présente toutes les dimensions de données disponibles pour le filtrage ou le regroupement ; par défaut, toutes les colonnes de données disponibles sont répertoriées en tant que dimensions. Dans notre exemple, si nous voulions segmenter nos recettes par source de référence, nous pourrions le faire ici.

En plus de répertorier toutes les colonnes de données disponibles sous forme de dimensions, [!DNL MBI] Vous allez également deviner quelles colonnes peuvent être regroupées. *Pour segmenter ou regrouper des données dans des rapports*, les colonnes doivent être marquées comme pouvant être regroupées.

## Finalisation {#finish}

Outre la définition du comportement de votre mesure, vous pouvez définir des niveaux d’autorisation dans la variable `User Rights` . while `Admin` les utilisateurs ont accès à toutes les mesures. vous devez indiquer les utilisateurs qui peuvent utiliser cette mesure en cochant la case en regard du groupe approprié.

Si vous modifiez une mesure existante, vous pouvez afficher la liste des graphiques (et des propriétaires) qui utilisent cette mesure dans la variable `Dependent Charts` .

Les modifications sont enregistrées automatiquement et votre mesure est désormais prête à l’emploi.
