---
title: Rapport Probabilité des commandes répétées
description: Découvrez et comprenez le rapport Probabilité des commandes répétées .
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# Rapport Probabilité des commandes répétées

## Lorsque est `Incremental Event Probability` perspective disponible ?

Le `incremental event probability` La perspective n’est disponible que lorsque les filtres utilisent des dimensions égales pour toutes les commandes (par exemple, celle de l’utilisateur `gender`, de l’utilisateur `age` ou de l’utilisateur `source`).

En effet, cette perspective repose sur une dimension appelée `User's order number` pour la segmentation, qui comptabilise les achats d’un utilisateur (par exemple, les 1re, 2e et 3e commandes de John).

Si vous avez ajouté un filtre qui utilise une dimension différente de toutes les commandes (par exemple, `Order's Region`), la variable `User's order number` ne serait plus exacte. Cela est dû au fait qu’il ne tient pas compte de régions spécifiques lors de la numérotation des commandes d’un utilisateur (par exemple, les 1er, 2e, 3e commandes de John sont toujours les mêmes, quelle que soit leur région).

## Transformer une dimension spécifique à une commande en dimension spécifique à l’utilisateur

Dans certains cas, vous pouvez activer une `order-specific` dans une `user-specific` dimension à ajouter en tant que filtre dans `Repeat Order Probability` graphique. Dans ce cas, vous renvoyez l’attribut de commande de la première commande ou de la dernière commande d’un utilisateur (par exemple, le nom de la région de première commande de l’utilisateur).

Si vous souhaitez créer une telle dimension, [support technique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## Comparaison de la probabilité de répétition des commandes avec différents attributs

Pour comparer le nombre d’achats répétés pour différents attributs de commande (par exemple, la variable `region`), Adobe recommande de créer un graphique semblable à `Users by lifetime number of orders`. Vous affichez ainsi le nombre d’utilisateurs qui ont effectué 1, 2, 3, etc. Nombre total de commandes, et ajoutez le filtre au niveau de la commande. (en d’autres termes, Cela peut vous indiquer si les utilisateurs effectuent plus ou moins des achats répétés dans une région ou une autre.)

Les nombres qui constituent un tel graphique peuvent ensuite être exportés pour excel afin de calculer le ratio de probabilité de l’ordre de répétition. Pour connaître la probabilité des clients qui ont effectué `(x)` commandes à effectuer `(x+1)` commandes, simplement` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` achats.

### Exemple :

| Catégorie | Valeur |
|---|---|
| Nombre de clients qui ont effectué un achat au cours de leur vie | `90` |
| Nombre de clients qui ont effectué deux achats au cours de leur vie | `30` |
| Nombre de clients ayant effectué trois achats au cours de leur vie | `10` |
| Probabilité des commandes répétées pour les clients qui ont effectué un achat au cours de leur vie afin d’effectuer un second achat. | `(30 + 10) / (30+10+90) = 30.77%` |
