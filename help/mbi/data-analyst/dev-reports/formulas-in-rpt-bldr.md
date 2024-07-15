---
title: Formules dans le Report Builder
description: Découvrez comment les formules peuvent être utilisées dans le Report Builder.
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---

# Formules dans le `Report Builder`

Dans [`Report Builder`](../../tutorials/using-visual-report-builder.md), vous pouvez créer de puissantes visualisations à l’aide des [mesures définies](../../data-user/reports/ess-manage-data-metrics.md) de votre compte. La combinaison de ces mesures dans une formule vous permet d’obtenir des informations supplémentaires sur vos données. Cette rubrique explique comment les formules peuvent être utilisées dans le `Report Builder` - Sautons dedans !

## Qu’est-ce qu’un `formula` ? {#what}

Dans le `Report Builder`, un `formula` n’est qu’une combinaison d’une ou de plusieurs mesures basées sur une logique mathématique. Voici un exemple type :

![](../../assets/formula-example.png)

Dans cet exemple, vous utilisez un `Number of orders metric (A)` et un `Distinct buyers metric (B)`, et l’objectif est de répondre à la question : quel est le nombre moyen de commandes que mes acheteurs font chaque mois ? Les paramètres de la formule sont les suivants :

* `Definition` : ici, vous appliquez des maths sur les mesures d’entrée. Dans cet exemple, diviser le nombre de commandes par le nombre d’acheteurs distincts indique le nombre moyen de commandes. Par conséquent, la définition est (A/B).

* `Format` : votre formule renvoie-t-elle un nombre, une période ou un montant en devise ? Une liste déroulante se trouve à côté de la définition de la formule, que vous pouvez utiliser pour spécifier le format du retour. Dans ce cas, il s’agit d’un nombre.

* `Miscellaneous` : l’horodatage, les regroupements, les perspectives et les filtres de la formule sont tous hérités par ses mesures d’entrée. Il n&#39;y a rien à faire ici !

## Comment utiliser `formulas` dans mes rapports ? {#how}

Maintenant que vous avez couvert les bases, regardez quelques exemples.

### Exemple : je veux savoir quel pourcentage de mes recettes peut être attribué aux premières commandes.

![Utilisation de formules pour trouver le pourcentage de recettes attribué aux premières commandes](../../assets/first_time_orders.gif)

Dans cet exemple, vous avez utilisé les mesures `Revenue` et `Revenue (first time orders)` . En divisant la mesure `Revenue (first time orders)(B)` par `Revenue metric (A)` et en définissant le format de retour sur `Percent`, vous pouvez obtenir le pourcentage de recettes pouvant être attribué aux premières commandes.

### Exemple : je veux connaître les recettes moyennes par commande lorsque je propose et ne propose pas de `promo code`.

![Utilisation de formules pour trouver les recettes moyennes par commande avec et sans code promotion](../../assets/promo_code.gif)

Dans cet exemple, vous avez utilisé les mesures `Revenue` et `Number of orders` . La réponse à cette question implique deux étapes : diviser `Revenue (A)` par `Number of orders (B)` et définir le format de retour sur `Currency`. Ensuite, vous avez uniquement autorisé le résultat de la formule (`Avg. Revenue per order`) à afficher et à regrouper les résultats par `Promo code`.

### Exemple : je veux connaître la distribution des sources UTM de mes nouveaux clients.

![Utilisation de formules pour trouver la distribution des sources UTM des nouveaux clients](../../assets/distro.gif)

Pour trouver la réponse à cette question, procédez comme suit :

1. Vous avez d’abord ajouté la mesure `New Customers`, puis vous l’avez groupée par `utm_source - all`. Il s’agit de la mesure `A` ou `New Customers (grouped)`.

1. Ensuite, vous avez dupliqué la mesure `New Customers (grouped)` et l’avez définie pour utiliser une dimension indépendante. La mesure `B` - `New customers (ungrouped)` - indique le nombre total de nouveaux clients.

1. Après avoir masqué les deux mesures, vous définissez la définition de formule sur `A/B`. Cela divise le `New customers (grouped)` par le `New Customers (ungrouped)`.

1. Ensuite, vous définissez le format des résultats sur `Percent`.

Dans cet exemple, vous avez utilisé la perspective `Stacked Columns` pour afficher les résultats par mois. Cela nous permet de comparer la distribution des nouveaux clients sur une base mensuelle.

## Remplissage {#wrapup}

Avez-vous remarqué dans les exemples ci-dessus que les `timestamp`, `groupings`, `perspectives` et `filters` de la formule sont hérités de ses mesures d’entrée ? Gardez à l’esprit que les formules peuvent être utilisées pour utiliser `perspectives` et les [options d’heure indépendantes](../../tutorials/time-options-visual-rpt-bldr.md){: target=&quot;_blank&quot;}, comme le peuvent les mesures.

Si vous avez des questions supplémentaires sur l&#39;utilisation des formules dans `Report Builder`, [contactez le support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
