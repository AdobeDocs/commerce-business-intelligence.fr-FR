---
title: Rapport sur la probabilité des commandes répétées
description: Découvrez et comprenez le rapport de probabilité des commandes répétées.
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# Rapport sur la probabilité des commandes répétées

## Quand la perspective `Incremental Event Probability` est-elle disponible ?

La perspective `incremental event probability` n’est disponible que lorsque les filtres utilisent des dimensions égales pour toutes les commandes (par exemple, le `gender` de l’utilisateur, le `age` de l’utilisateur ou le `source` de l’utilisateur).

En effet, cette perspective repose sur une dimension appelée `User's order number` pour la segmentation, qui chiffre les achats d’un utilisateur (par exemple, les 1ère, 2e et 3e commandes de John).

Si vous ajoutez un filtre qui utilise une dimension différente pour toutes les commandes (par exemple, `Order's Region`), la dimension `User's order number` ne sera plus précise. Cela est dû au fait qu’il ne prend pas en compte des régions spécifiques lors de la numérotation des commandes d’un utilisateur ou d’une utilisatrice (par exemple, les 1ère, 2e et 3e commandes de Jean sont toujours les mêmes, quelle que soit leur région).

## Transformation d’une dimension spécifique à une commande en une dimension spécifique à un utilisateur

Dans certains cas, vous pouvez transformer une dimension `order-specific` en une dimension `user-specific` à ajouter comme filtre dans le graphique `Repeat Order Probability`. Dans ces cas, vous renvoyez l’attribut de commande de la première commande ou de la dernière commande d’un utilisateur (par exemple, le nom de la région de première commande de l’utilisateur).

Si vous souhaitez créer une telle dimension, [contactez l’assistance ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr).

## Comparaison de la probabilité de répétition des commandes avec des attributs différents

Pour comparer le nombre d’achats répétés pour différents attributs de commande (par exemple, le `region` de la commande), Adobe recommande de créer un graphique similaire à `Users by lifetime number of orders`. Vous voyez ici le nombre d’utilisateurs qui ont passé 1, 2, 3,... nombre de commandes au cours de la durée de vie, et ajoutez le filtre au niveau de la commande. (en d’autres termes, cela peut vous montrer si les utilisateurs effectuent plus ou moins d’achats répétés dans une région ou une autre.)

Les nombres qui constituent un tel graphique peuvent ensuite être exportés vers Excel pour calculer le rapport de probabilité d’ordre de répétition. Pour voir la probabilité que les clients qui ont passé des commandes `(x)` passent des commandes `(x+1)`, il suffit ` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)`’acheter.

### Exemple :

| Catégorie | Valeur |
|---|---|
| Nombre de clients qui ont effectué 1 achat au cours de leur vie | `90` |
| Nombre de clients ayant effectué 2 achats au cours de leur durée de vie | `30` |
| Nombre de clients ayant effectué 3 achats au cours de leur durée de vie | `10` |
| Probabilité de commande répétée des clients qui ont effectué un achat au cours de leur durée de vie pour effectuer un deuxième achat | `(30 + 10) / (30+10+90) = 30.77%` |
