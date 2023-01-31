---
title: Commande des données à l’aide de la fonction Afficher le haut/bas
description: Découvrez comment classer vos données à l’aide de la fonction Afficher le haut/bas.
exl-id: d47119f4-cdc5-4fa7-a606-d4b8555a8843
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Commande des données à l’aide de `Show Top/Bottom` fonctionnalité

Vous pouvez en faire plus dans la section `Visual Report Builder` plutôt que de créer des analyses qui suivent cette tendance au fil du temps. Vous pouvez, par exemple, créer un rapport qui indique la valeur de vos canaux d’acquisition et marketing, mais vous pouvez également créer un rapport qui ne présente que les cinq premiers performants. De même, vous pouvez recentrer vos efforts marketing en créant un rapport qui vous indique les états qui génèrent le plus de recettes.

Ce type de tri et d’ordre des données peut être effectué dans des rapports qui utilisent à la fois une `Group By` et un `Time Interval of None`. Lorsque ces deux éléments figurent dans un rapport, la variable `Show Top/Bottom` s’affiche au-dessus de l’aperçu du graphique. Cette fonctionnalité vous permet d’afficher les points de données de haut (du plus haut au plus bas) et de bas (du plus bas au plus haut) en fonction des paramètres que vous avez définis.

![Afficher la fonction Haut/Bas dans le Report Builder visuel.](../../assets/Show_Top_Bottom.png)

## Comment puis-je utiliser ceci ? {#how}

Après avoir cliqué sur le bouton **[!UICONTROL Show Top/Bottom link]**, une fenêtre s’affiche dans laquelle vous pouvez définir les paramètres d’affichage et de tri. Le nombre dans la zone de texte peut être un nombre entier (comme `5`) ou `ALL`. Vous pouvez ensuite choisir de trier le rapport par mesure OU par groupement.

Par exemple, si nous voulions afficher les cinq sources de référence qui ont généré le plus de recettes, voici comment nous le faisons :

1. Ajoutez la variable `Revenue` au rapport.

1. Ajouter un `Group By` pour segmenter la mesure par source de référence.

1. Définir `Time Interval` to `None`.

1. Dans le `Show Top/Bottom` paramètres, définissez l’affichage sur `5` ainsi, seules les sources de référence comportant les cinq montants de recettes totaux les plus élevés sont incluses dans le rapport.

>[!NOTE]
>
>Parce que le rapport n’a pas de `Time Interval`, les valeurs - dans ce cas, les cinq premières sources de référence - peuvent changer au fil du temps. Si une source de référence dépasse une autre en termes de recettes, l’ordre dans lequel les sources s’affichent change.

## Qu’en est-il de l’utilisation de plusieurs mesures ? {#multiplemetrics}

L’utilisation de cette fonctionnalité devient complexe lorsque il existe plusieurs mesures dans un rapport, car chaque mesure ne peut être triée que par elle-même ou par l’un des regroupements.

Disons que nous avons créé un rapport avec les deux `Revenue` et `Number of orders` mesures, regroupées par source de référence. `Revenue` ne peut être trié que par `Revenue` ou source de référence ; `Number of orders` ne peut être trié que par `Number of orders` ou source de référence.

Cela signifie que pendant que nous pouvons afficher la variable `Revenue` en haut uniquement `5` sources de référence générant des recettes, nous ne pouvons pas afficher le nombre de commandes également en haut `5` sources de référence générant des recettes. En termes simples : s’il existe plusieurs mesures, il est préférable de les trier en fonction du regroupement.

Voici un exemple de graphique dans lequel nous avons trié la variable `Revenue` mesure par elle-même plutôt que par le regroupement. Comme vous pouvez le constater, le fait de ne pas trier la mesure par groupement a créé un rapport étrange (et, en fin de compte, inutile) :

![Résultats de rapports étranges et peu utiles.](../../assets/strange-report-results.png)

Si nous avions trié les deux mesures par regroupement, le graphique ressemblerait à ceci :

![Tri des deux mesures par regroupement.](../../assets/sort-metrics-by-grouping.png)

## Comment les valeurs sont-elles triées par défaut ? {#defaultsorting}

Lorsqu’une seule mesure est incluse dans un rapport avec une `Group by` et un `Time Interval` de `None`, l’ordre par défaut dans le `Visual Report Builder` est pour afficher les valeurs principales en fonction de la mesure. Dans ce cas, la variable `Show Top/Bottom` Cette fonctionnalité peut ne pas être nécessaire si elle répond à vos besoins.

Dans cet exemple, nous examinons le nombre d’opportunités que nos représentants commerciaux ont saisies. Ce tableau est automatiquement trié du plus haut au plus bas en fonction de la mesure, dans ce cas `Won Opportunities`.

![Classement par mesure.](../../assets/Ordered_by_metric.png)

Cependant, lorsqu’une seconde mesure est ajoutée, la valeur par défaut est de classer la première selon le regroupement. À mesure que des mesures et des regroupements sont ajoutés, le tri par défaut est basé sur le premier groupe, puis sur le second, et ainsi de suite.

![Classement par groupement.](../../assets/Ordered_by_grouping.png)

## Remplissage {#wrapup}

Nous l&#39;avons mentionné au début de l&#39;article, mais nous le répétons : bien que nous ayons présenté quelques exemples de base, cette fonctionnalité a de nombreux usages intéressants.

Pensez à l’exemple de notre représentant commercial précédent et à nos opportunités. Suppression de la variable `Time Interval`, en appliquant une `Group By`, et le tri des données selon le groupement nous a permis d&#39;obtenir une image détaillée du nombre d&#39;opportunités gagnées par chaque rep. En outre, l’utilisation de la variable `Show Top/Bottom` nous permet de découvrir qui sont les plus performants.
