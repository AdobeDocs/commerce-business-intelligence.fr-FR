---
title: Rapport sur la probabilité des commandes répétées
description: Découvrez et comprenez le rapport de probabilité des commandes répétées.
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/MW9jxiwitZyjc6-woelN-FOAmvEFPCWDt01wyTOX16k
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 343
ht-degree: 0%

---

# Rapport sur la probabilité des commandes répétées

## Quand la perspective `Incremental Event Probability` est-elle disponible ?

La perspective `incremental event probability` n’est disponible que lorsque les filtres utilisent des dimensions égales pour toutes les commandes (par exemple, le `gender` de l’utilisateur, le `age` de l’utilisateur ou le `source` de l’utilisateur).

En effet, cette perspective repose sur une dimension appelée `User's order number` pour la segmentation, qui chiffre les achats d’un utilisateur (par exemple, les 1ère, 2e et 3e commandes de John).

Si vous ajoutez un filtre qui utilise une dimension différente pour toutes les commandes (par exemple, `Order's Region`), la dimension `User's order number` ne sera plus précise. Cela est dû au fait qu’il ne prend pas en compte des régions spécifiques lors de la numérotation des commandes d’un utilisateur ou d’une utilisatrice (par exemple, les 1ère, 2e et 3e commandes de Jean sont toujours les mêmes, quelle que soit leur région).

## Transformation d’une dimension spécifique à une commande en une dimension spécifique à un utilisateur

Dans certains cas, vous pouvez transformer une dimension `order-specific` en une dimension `user-specific` à ajouter comme filtre dans le graphique `Repeat Order Probability`. Dans ces cas, vous renvoyez l’attribut de commande de la première commande ou de la dernière commande d’un utilisateur (par exemple, le nom de la région de première commande de l’utilisateur).

Si vous souhaitez créer une telle dimension, [contactez l’assistance ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

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
