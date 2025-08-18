---
title: Analyse du comportement de rachat des clients
description: Découvrez comment analyser le comportement de rachat des clients.
exl-id: 62666d08-5240-4f19-bf8e-e5b2d79a25c4
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Comportement de rachat des clients

Si vous proposez plusieurs produits, vous vous demandez probablement comment les clients qui achètent un produit spécifique se comportent différemment au fil du temps par rapport aux autres clients. Cette rubrique explore les analyses qui peuvent vous aider à répondre aux questions suivantes.

Parmi les clients qui achètent un *article spécifique*,

* Quelle est la probabilité qu’ils effectuent un autre achat ?
* Combien de temps faut-il pour qu&#39;ils fassent un autre achat ?
* Quel est le nombre moyen de commandes passées par les clients à court/long terme ?
* Quel est le chiffre d’affaires moyen généré par les clients à court/long terme ?

## Mesures recommandées

Lors de la création d’analyses d’activité de rachat de clients, Adobe recommande d’utiliser les mesures suivantes :

### Probabilité d’ordre de répétition

Cette mesure correspond au nombre total de commandes répétées, exprimé en pourcentage du total des commandes. Autrement dit, il s’agit de la probabilité qu’un ordre soit suivi d’un autre ordre. Cette mesure identifie les articles susceptibles d’inciter les clients à revenir dans votre magasin.

### Nombre moyen de commandes passées

Cela expose le comportement d’achat de vos clients, en particulier le nombre de commandes que vos clients ont passées au cours d’une période donnée. Vous pouvez choisir de limiter cette mesure pour afficher le comportement des clients à court, moyen ou long terme. Certains produits peuvent encourager les clients à effectuer des achats fréquents à court terme, tandis que d&#39;autres peuvent influencer la fidélité à long terme d&#39;un client. Si ce nombre est plus élevé pour un article que pour d&#39;autres, cela suggère que les personnes qui achètent cet article sont celles qui reviennent dans votre magasin.

### Chiffre d’affaires moyen du client sur la durée de vie

Cette mesure vous permet de comprendre si les clients qui achètent des articles spécifiques ont plus de valeur au cours de leur durée de vie. Si ce nombre est plus élevé pour un article par rapport à d&#39;autres articles à prix similaire, cela suggère que vos clients à valeur élevée ont tendance à acheter cet article.

### Heure de la prochaine commande

Cette mesure indique la fréquence des commandes du client ou le temps nécessaire au client pour passer une nouvelle commande. Si le délai de la prochaine commande est plus court pour un article que pour d&#39;autres, cela suggère que les gens qui achètent cet article ont tendance à revenir plus tôt.

## Exemple d’aujourd’hui : produits de café

En gardant à l’esprit les mesures ci-dessus, examinez un exemple impliquant des produits à base de café.

| **Nom du produit** | **Probabilité de répétition** | **Nombre de commandes au cours de la durée de vie moyenne** | **Chiffre d’affaires moyen sur la durée de vie** | **Délai médian jusqu’à la prochaine commande** |
|-----|-----|-----|-----|-----|
| Brasseur de café à tasse unique | 94,98 % | 7,92 | 549,82 $ | 57,01 jours |
| Capsules de café | 93,82 % | 8,68 | 479,98 $ | 63,48 jours |
| Grains de café | 41,92 % | 6,07 | 99,82 $ | 27,31 jours |

{style="table-layout:auto"}

Maintenant que vous disposez de vos données, qu’est-ce que cela signifie pour chacune de vos mesures ?

### Probabilité d’ordre de répétition

Dans cet exemple, la probabilité de répétition de l’ordre - ou la probabilité qu’un ordre soit suivi d’un autre ordre - est beaucoup plus élevée pour les brasseurs de café et les capsules de café à une tasse que pour les grains de café.

Puisque les clients qui achètent le brasseur sont « engagés » à acheter les capsules associées à l&#39;avenir, cela est logique. De même, les clients ayant acheté des capsules disposent d&#39;un brasseur compatible avec les capsules. Cependant, les grains de café ne sont pas spécifiques à un brasseur particulier.

### Nombre moyen de commandes sur la durée de vie

D&#39;après les données ci-dessus, vous pouvez constater que les personnes qui achètent le brasseur ou les capsules ont fait plus d&#39;achats au cours de leur vie, en moyenne, par rapport aux clients qui ont acheté des grains de café.

### Chiffre d’affaires moyen du client sur la durée de vie

Les clients qui achètent le brasseur ont les revenus moyens les plus élevés au cours de leur vie, ce qui est logique, étant donné que le coût du brasseur est inclus dans cette mesure. En revanche, les clients qui achètent des grains de café n’achètent généralement que des articles à faible coût.

### Heure de la prochaine commande

Parmi les clients qui ont acheté des capsules de café, la moitié font une commande répétée en environ deux mois. Cependant, la moitié des clients qui ont acheté des grains de café passent une nouvelle commande en un mois environ. Cela peut être dû au fait que les personnes qui commandent des gélules (1) ne boivent pas autant de café ou (2) passent des commandes en vrac (par exemple, en achetant deux mois de café en une seule commande).

## Quelles autres analyses puis-je créer ?

En utilisant les mesures décrites dans cette rubrique, vous pouvez également créer d’autres analyses de rachat utiles. Par exemple, vous pouvez également voir comment les clients rachètent **le même article**, par exemple s’ils achètent des recharges régulièrement. Les capsules et les grains de café peuvent être rachetés régulièrement, mais il serait inattendu de voir les clients faire des achats répétés du brasseur de café. Si votre entreprise se concentre sur les renouvellements ou le réapprovisionnement, cette analyse serait utile.

Outre l’analyse du comportement de rachat de vos clients, vous pouvez également créer des analyses qui examinent la fidélisation de la clientèle. Pensez à analyser les schémas de perte de clientèle : où vos clients quittent-ils votre site et ne reviennent-ils pas ? À quel rythme cela se produit-il ?

Une fois que vous avez identifié la raison de l’attrition, vous pouvez utiliser votre analyse pour créer une campagne `reactivation`. Grâce à ces données, vous pouvez identifier les utilisateurs qui sont devenus inactifs, le temps écoulé depuis leur dernière visite, leur dernier achat, etc. Cela vous permet de prendre des décisions exploitables qui incitent vos clients à revenir.

Pour obtenir de l’aide sur l’analyse, [contactez l’assistance technique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr).
