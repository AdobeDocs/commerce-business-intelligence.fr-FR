---
title: Analyse du comportement d’achat des clients
description: Découvrez comment analyser le comportement de rachat des clients.
exl-id: 62666d08-5240-4f19-bf8e-e5b2d79a25c4
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 1%

---

# Comportement de rachat des clients

Si vous proposez plusieurs produits, vous vous demandez probablement comment les clients qui achètent un produit spécifique se comportent différemment au fil du temps par rapport aux autres clients. Cette rubrique explore les analyses qui peuvent vous aider à répondre aux questions suivantes.

Parmi les clients qui achètent une *élément spécifique*,

* Quelle est la probabilité qu&#39;ils effectuent un autre achat ?
* Combien de temps leur faut-il pour faire un autre achat ?
* Quel est le nombre moyen de commandes passées par les clients à court/long terme ?
* Quelles sont les recettes moyennes à court/long terme générées par les clients ?

## Mesures recommandées

Lors de la création d’analyses de l’activité de réachat des clients, Adobe recommande d’utiliser les mesures suivantes :

### Probabilité de répétition de l’ordre

Cette mesure est définie comme le nombre total de commandes répétées, en pourcentage du total des commandes. En d’autres termes, il s’agit de la probabilité qu’une commande soit suivie d’une autre commande. Cette mesure identifie les éléments susceptibles d’inciter les clients à revenir dans votre boutique.

### Nombre moyen de commandes passées

Cela expose le comportement d’achat de vos clients, en particulier le nombre de commandes passées par vos clients sur une période donnée. Vous pouvez choisir de limiter cette mesure pour visualiser le comportement des clients à court, moyen ou long terme. Certains produits peuvent encourager les clients à effectuer des achats fréquents à court terme, tandis que d’autres peuvent influencer la fidélité à long terme d’un client. Si ce nombre est plus élevé pour un article que pour d’autres articles, cela signifie que les personnes qui achètent cet article sont celles qui reviennent dans votre boutique.

### Chiffre d’affaires moyen des clients

Cette mesure vous permet de déterminer si les clients qui achètent des articles spécifiques ont plus de valeur au cours de leur vie. Si ce nombre est plus élevé pour un article par rapport à d’autres articles au prix similaire, cela signifie que vos clients à plus forte valeur ont tendance à l’acheter.

### Temps jusqu’à la commande suivante

Cette mesure indique la fréquence de commande du client ou le temps nécessaire pour que le client effectue une nouvelle commande. Si le délai de la prochaine commande est plus court pour un article que pour d’autres, cela signifie que les personnes qui achètent cet article ont tendance à revenir plus tôt.

## Exemple d’aujourd’hui : produits du café

En gardant à l’esprit les mesures ci-dessus, prenez un exemple concernant les produits à base de café.

| **Nom du produit** | **Probabilité de répétition de l’ordre** | **Nombre moyen de commandes pendant la durée de vie** | **Chiffre d’affaires moyen de la durée de vie** | **Temps moyen jusqu’à la commande suivante** |
|-----|-----|-----|-----|-----|
| Petit-déjeuner | 94.98% | 7.92 | $549.82 | 57,01 jours |
| Capsules de café | 93.82% | 8.68 | $479.98 | 63,48 jours |
| Les fèves de café | 41.92% | 6.07 | $99.82 | 27,31 jours |

{style="table-layout:auto"}

Maintenant que vous disposez de vos données, qu’est-ce que cela signifie pour chacune de vos mesures ?

### Probabilité de répétition de l’ordre

Dans cet exemple, la probabilité de répétition de l&#39;ordre - ou la probabilité qu&#39;une commande soit suivie d&#39;une autre commande - est beaucoup plus élevée pour les brasseurs de café et les gélules de café que pour les grains de café.

Comme les clients qui achètent le brasseur s&#39;engagent à acheter à l&#39;avenir les capsules associées, cela a du sens. De même, les clients qui ont acheté des capsules ont un brasseur compatible avec les capsules. Cependant, les grains de café ne sont pas spécifiques à un brasseur particulier.

### Durée de vie moyenne des commandes

D&#39;après les données ci-dessus, vous pouvez constater que les personnes qui achètent le brasseur ou les gélules ont fait plus d&#39;achats au cours de leur vie, en moyenne, par rapport aux clients qui ont acheté des grains de café.

### Chiffre d’affaires moyen des clients

Les clients qui achètent le brasseur ont les recettes de durée de vie moyennes les plus élevées, ce qui est logique, étant donné que le coût du brasseur est inclus dans cette mesure. En revanche, les clients qui achètent des grains de café n’achètent généralement que des produits à bas prix.

### Temps jusqu’à la commande suivante

Parmi les clients qui ont acheté des capsules de café, la moitié font une commande répétée dans environ deux mois. Cependant, parmi les clients qui ont acheté des grains de café, la moitié passent une commande renouvelée en un mois environ. Cela peut être dû au fait que les personnes qui commandent des capsules (1) ne boivent pas autant de café, ou (2) passent des commandes en bloc (par exemple, en achetant en une seule commande pour deux mois de café).

## Quelles autres analyses puis-je construire ?

En utilisant les mesures décrites dans cette rubrique, vous pouvez également créer d’autres analyses de réachat utiles. Par exemple, vous pouvez également voir comment les clients effectuent un rachat **le même élément ;** - par exemple, s’ils achètent des renforts régulièrement. Les capsules et les haricots peuvent être achetés régulièrement, mais il serait inattendu que les clients effectuent des achats répétés du brasseur de café. Si votre entreprise se concentre sur les rechargements ou le redémarrage, cette analyse serait utile.

Outre l’analyse du comportement de réachat de vos clients, vous pouvez également créer des analyses portant sur la fidélité de vos clients. Envisagez d’analyser les schémas de perte de clientèle : où vos clients quittent votre site et ne reviennent pas ? À quelle vitesse cela se produit-il ?

Une fois que vous avez identifié les raisons de l’attrition, vous pouvez utiliser votre analyse pour créer une `reactivation` campaign. Grâce à ces données, vous pouvez identifier les utilisateurs devenus inactifs, la durée écoulée depuis leur dernière visite, le dernier achat effectué, etc. Cela vous permet de prendre des décisions pratiques qui incitent vos clients à revenir.

Pour obtenir de l’aide sur l’analyse, [support technique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
