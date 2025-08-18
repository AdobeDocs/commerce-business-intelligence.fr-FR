---
title: Classer les données à l’aide de la fonction Afficher le haut/bas
description: Découvrez comment classer vos données à l’aide de la fonction Afficher le haut/bas .
exl-id: d47119f4-cdc5-4fa7-a606-d4b8555a8843
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# Données de commande à l’aide de `Show Top/Bottom` fonctionnalité

Vous pouvez faire plus dans le `Visual Report Builder` que de créer des analyses qui affichent cette tendance au fil du temps. Par exemple, vous pouvez créer un rapport pour montrer la valeur de vos canaux d’acquisition et de marketing, mais vous pouvez également créer un rapport qui n’affiche que les cinq meilleures performances. De même, vous pouvez recentrer vos efforts marketing en créant un rapport qui vous indique les états qui génèrent le plus de chiffre d’affaires.

Ce type de tri et d’ordre des données peut être effectué dans les rapports qui utilisent à la fois un `Group By` et un `Time Interval of None`. Lorsque ces deux éléments se trouvent dans un rapport, la fonction `Show Top/Bottom` s’affiche au-dessus de l’aperçu du graphique. Cette fonctionnalité vous permet d’afficher les points de données supérieur (du plus haut au plus bas) et inférieur (du plus bas au plus haut) en fonction des paramètres que vous avez définis.

![Afficher la fonction Haut/Bas dans Visual Report Builder.](../../assets/Show_Top_Bottom.png)

## Comment puis-je utiliser ceci ? {#how}

Cliquez sur le **[!UICONTROL Show Top/Bottom link]** pour définir les paramètres d&#39;affichage et de tri. Le nombre dans la zone de texte peut être un nombre entier (comme `5`) ou `ALL`. Vous pouvez ensuite choisir de trier le rapport selon la mesure OU selon le regroupement.

Par exemple, si vous souhaitez afficher les cinq sources de référence qui ont généré le plus de chiffre d’affaires, procédez comme suit :

1. Ajoutez la mesure `Revenue` au rapport.

1. Ajoutez une `Group By` pour segmenter la mesure par source de référence.

1. Définissez `Time Interval` sur `None`.

1. Dans les paramètres de `Show Top/Bottom`, définissez l’affichage sur `5` afin que seules les sources de recommandation avec les cinq premiers montants de revenus totaux soient incluses dans le rapport.

>[!NOTE]
>
>Comme le rapport ne comporte pas de `Time Interval`, les valeurs (dans ce cas, les cinq principales sources de référence) peuvent changer au fil du temps. Si une source de référence dépasse une autre en termes de chiffre d’affaires, l’ordre dans lequel les sources s’affichent change.

## Qu’en est-il de l’utilisation de plusieurs mesures ? {#multiplemetrics}

L’utilisation de cette fonctionnalité se complique lorsqu’il existe plusieurs mesures dans un rapport, car chaque mesure ne peut être triée que par elle-même ou par l’un des regroupements.

Supposons que vous ayez créé un rapport avec les mesures `Revenue` et `Number of orders`, regroupées par source de référence. `Revenue` ne peut être trié que par `Revenue` ou source de référence et `Number of orders` ne peut être trié que par `Number of orders` ou source de référence.

Cela signifie que si vous pouvez afficher les `Revenue` à partir des seules principales sources de référence génératrices `5` revenus, vous ne pouvez pas afficher le nombre de commandes également par les principales sources de référence génératrices de revenus `5`. En d’autres termes, lorsqu’il existe plusieurs mesures, la meilleure solution est de trier chaque mesure par groupe.

Vous trouverez ci-dessous un exemple de graphique qui a trié la mesure `Revenue` par elle-même plutôt que par le regroupement. Comme vous pouvez le constater, le fait de ne pas trier les mesures en fonction du regroupement a créé un rapport étrange (et finalement inutile) :

![Résultats de rapports étranges et inutiles.](../../assets/strange-report-results.png)

Si vous aviez trié les deux mesures par regroupement, le graphique aurait l’aspect suivant :

![Tri des deux mesures par regroupement.](../../assets/sort-metrics-by-grouping.png)

## Comment les valeurs sont-elles triées par défaut ? {#defaultsorting}

Lorsqu’une seule mesure est incluse dans un rapport avec une `Group by` et une `Time Interval` de `None`, l’ordre par défaut dans le `Visual Report Builder` consiste à afficher les principales valeurs en fonction de la mesure. Dans ce cas, la fonction `Show Top/Bottom` peut ne pas être nécessaire si elle répond à vos besoins.

Cet exemple montre le nombre d&#39;opportunités que vos représentants ont clôturées. Ce tableau est automatiquement trié du plus élevé au plus bas en fonction de la mesure, dans ce cas `Won Opportunities`.

![Classement par la mesure.](../../assets/Ordered_by_metric.png)

Cependant, lorsqu’une deuxième mesure est ajoutée, le classement par défaut du haut en fonction du regroupement est effectué. À mesure que des mesures et des regroupements sont ajoutés, le tri par défaut est basé sur le premier regroupement, puis sur le deuxième, et ainsi de suite.

![Classement par le regroupement.](../../assets/Ordered_by_grouping.png)

## Conclusion {#wrapup}

Bien que certaines fonctionnalités de base soient abordées ici, cette fonctionnalité a de nombreuses utilisations intéressantes.

Pensez à l’exemple précédent du représentant commercial et des opportunités . La suppression des `Time Interval`, l’application d’un `Group By` et le tri des données en fonction du regroupement nous ont permis d’obtenir une vue détaillée du nombre d’opportunités gagnées par chaque représentant. En outre, en utilisant la fonctionnalité `Show Top/Bottom`, nous découvrons qui sont les meilleurs.
