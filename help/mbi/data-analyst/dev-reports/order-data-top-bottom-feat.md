---
title: Commande des données à l’aide de la fonction Afficher le haut/bas
description: Découvrez comment classer vos données à l’aide de la fonction Afficher le haut/bas.
exl-id: d47119f4-cdc5-4fa7-a606-d4b8555a8843
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# Commande des données à l’aide de la fonction `Show Top/Bottom`

Vous pouvez en faire plus dans le `Visual Report Builder` que de créer des analyses qui suivent les tendances au fil du temps. Vous pouvez, par exemple, créer un rapport qui indique la valeur de vos canaux d’acquisition et marketing, mais vous pouvez également créer un rapport qui ne présente que les cinq premiers performants. De même, vous pouvez recentrer vos efforts marketing en créant un rapport qui vous indique les états qui génèrent le plus de recettes.

Ce type de tri et d’ordre des données peut être effectué dans les rapports qui utilisent à la fois un `Group By` et un `Time Interval of None`. Lorsque ces deux éléments figurent dans un rapport, la fonction `Show Top/Bottom` s’affiche au-dessus de l’aperçu du graphique. Cette fonctionnalité vous permet d’afficher les points de données de haut (du plus haut au plus bas) et de bas (du plus bas au plus haut) en fonction des paramètres que vous avez définis.

![Afficher la fonction Haut/Bas dans le Report Builder visuel.](../../assets/Show_Top_Bottom.png)

## Comment puis-je utiliser ceci ? {#how}

Cliquez sur le **[!UICONTROL Show Top/Bottom link]** pour définir les paramètres d&#39;affichage et de tri. Le nombre dans la zone de texte peut être un nombre entier (comme `5`) ou `ALL`. Vous pouvez ensuite choisir de trier le rapport par mesure OU par groupement.

Par exemple, si vous souhaitez afficher les cinq sources de référence qui ont généré le plus de recettes, procédez comme suit :

1. Ajoutez la mesure `Revenue` au rapport.

1. Ajoutez un `Group By` pour segmenter la mesure par source de référence.

1. Définissez `Time Interval` sur `None`.

1. Dans les paramètres `Show Top/Bottom`, définissez l’affichage sur `5` afin que seules les sources de référence avec les cinq premières recettes totales soient incluses dans le rapport.

>[!NOTE]
>
>Étant donné que le rapport ne comporte pas de `Time Interval`, les valeurs - dans ce cas, les cinq premières sources de référence - peuvent changer au fil du temps. Si une source de référence dépasse une autre en termes de recettes, l’ordre dans lequel les sources s’affichent change.

## Qu’en est-il de l’utilisation de plusieurs mesures ? {#multiplemetrics}

L’utilisation de cette fonctionnalité devient complexe lorsque il existe plusieurs mesures dans un rapport, car chaque mesure ne peut être triée que par elle-même ou par l’un des regroupements.

Supposons que vous ayez créé un rapport avec les mesures `Revenue` et `Number of orders`, regroupées par source de référence. `Revenue` ne peut être trié que par `Revenue` ou source de référence et `Number of orders` ne peut être trié que par `Number of orders` ou source de référence.

Cela signifie que même si vous pouvez afficher le `Revenue` à partir des `5` premières sources de référence génératrices de recettes, vous ne pouvez pas afficher le nombre de commandes également par les `5` premières sources de référence génératrices de recettes. En d’autres termes : lorsqu’il existe plusieurs mesures, il est préférable de trier chaque mesure par regroupement.

Vous trouverez ci-dessous un exemple de graphique qui a trié la mesure `Revenue` par elle-même au lieu de par le regroupement. Comme vous pouvez le constater, le fait de ne pas trier la mesure par groupement a créé un rapport étrange (et, en fin de compte, inutile) :

![Résultats de rapports étranges et peu utiles.](../../assets/strange-report-results.png)

Si vous aviez trié les deux mesures par groupement, le graphique ressemblerait à ceci :

![Tri des deux mesures par regroupement.](../../assets/sort-metrics-by-grouping.png)

## Comment les valeurs sont-elles triées par défaut ? {#defaultsorting}

Lorsqu’une seule mesure est incluse dans un rapport avec un `Group by` et un `Time Interval` de `None`, l’ordre par défaut dans le `Visual Report Builder` consiste à afficher les valeurs principales en fonction de la mesure. Dans cette instance, la fonction `Show Top/Bottom` peut ne pas être nécessaire si elle répond à vos besoins.

Cet exemple montre le nombre d&#39;opportunités que vos représentants commerciaux ont clôturées. Ce tableau est automatiquement trié du plus haut au plus bas en fonction de la mesure, dans ce cas `Won Opportunities`.

![Classement par mesure.](../../assets/Ordered_by_metric.png)

Cependant, lorsqu’une seconde mesure est ajoutée, la valeur par défaut est de classer la première selon le regroupement. À mesure que des mesures et des regroupements sont ajoutés, le tri par défaut est basé sur le premier regroupement, puis sur le second, et ainsi de suite.

![Classement par groupement.](../../assets/Ordered_by_grouping.png)

## Remplissage {#wrapup}

Bien que certaines fonctions de base soient abordées ici, cette fonctionnalité présente de nombreux usages intéressants.

Pensez à l’exemple de représentant commercial et d’opportunité précédent. La suppression de `Time Interval`, l&#39;application d&#39;un `Group By` et le tri des données en fonction du groupement nous ont permis d&#39;obtenir une image détaillée du nombre d&#39;opportunités gagnées par chaque représentant. En outre, l’utilisation de la fonction `Show Top/Bottom` nous permet de découvrir qui sont les plus performants.
