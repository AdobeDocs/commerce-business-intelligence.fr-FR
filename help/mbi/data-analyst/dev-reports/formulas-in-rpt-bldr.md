---
title: Formules dans le Report Builder
description: Découvrez comment les formules peuvent être utilisées dans le Report Builder.
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Formules dans le `Report Builder`

Dans le [`Report Builder`](../../tutorials/using-visual-report-builder.md), vous pouvez créer de puissantes visualisations à l’aide de la variable [mesures définies](../../data-user/reports/ess-manage-data-metrics.md) dans votre compte. La combinaison de ces mesures dans une formule vous permet d’obtenir des informations supplémentaires sur vos données. Cette rubrique explique comment les formules peuvent être utilisées dans la variable `Report Builder` - allons-y !

## Qu’est-ce qu’une `formula`? {#what}

Dans le `Report Builder`, un `formula` n’est qu’une combinaison d’une ou de plusieurs mesures basées sur une logique mathématique. Voici un exemple type :

![](../../assets/formula-example.png)

Dans cet exemple, vous utilisez une `Number of orders metric (A)` et un `Distinct buyers metric (B)`, et l’objectif est de répondre à la question : quel est le nombre moyen de commandes que mes acheteurs font chaque mois ? Les paramètres de la formule sont les suivants :

* `Definition`: Ici, vous appliquez des maths aux mesures d’entrée. Dans cet exemple, diviser le nombre de commandes par le nombre d’acheteurs distincts indique le nombre moyen de commandes. Par conséquent, la définition est (A/B).

* `Format`: Votre formule renvoie-t-elle un nombre, une période ou un montant en devise ? Une liste déroulante se trouve à côté de la définition de la formule, que vous pouvez utiliser pour spécifier le format du retour. Dans ce cas, il s’agit d’un nombre.

* `Miscellaneous`: L’horodatage, les regroupements, les perspectives et les filtres de la formule sont tous hérités par ses mesures d’entrée. Il n&#39;y a rien à faire ici !

## Comment utiliser `formulas` dans mes rapports ? {#how}

Maintenant que vous avez couvert les bases, regardez quelques exemples.

### Exemple : Je veux découvrir quel pourcentage de mes recettes peut être attribué aux premières commandes.

![Utilisation de formules pour rechercher le pourcentage de recettes attribué aux premières commandes](../../assets/first_time_orders.gif)

Dans cet exemple, vous avez utilisé la méthode `Revenue` et `Revenue (first time orders)` mesures. En divisant la variable `Revenue (first time orders)(B)` par la mesure `Revenue metric (A)` et définir le format de retour sur `Percent`, vous pouvez trouver le pourcentage de recettes pouvant être attribué aux premières commandes.

### Exemple : Je veux savoir quel est le chiffre d’affaires moyen par commande lorsque j’offre et ne propose pas de `promo code`.

![Utilisation de formules pour trouver les recettes moyennes par commande avec et sans code promotion](../../assets/promo_code.gif)

Dans cet exemple, vous avez utilisé la méthode `Revenue` et `Number of orders` mesures. La réponse à cette question comporte deux étapes : `Revenue (A)` par le `Number of orders (B)` et définir le format de retour sur `Currency`. Ensuite, vous avez uniquement autorisé le résultat de la formule (`Avg. Revenue per order`) pour afficher et regrouper les résultats par `Promo code`.

### Exemple : Je veux connaître la distribution des sources de gestion dynamique des balises de mes nouveaux clients.

![Utilisation de formules pour trouver la distribution des sources UTM des nouveaux clients](../../assets/distro.gif)

La réponse à cette question comporte quelques étapes :

1. Tout d’abord, vous avez ajouté la variable `New Customers` puis regroupées par `utm_source - all`. Cette mesure `A`ou `New Customers (grouped)`.

1. Ensuite, vous avez dupliqué le `New Customers (grouped)` et définissez-la pour utiliser une dimension indépendante. Mesure `B` - `New customers (ungrouped)` - indique le nombre total de nouveaux clients.

1. Après avoir masqué les deux mesures, vous définissez la définition de formule sur `A/B`. Cela divise le `New customers (grouped)` par le `New Customers (ungrouped)`.

1. Ensuite, vous définissez le format des résultats sur `Percent`.

Dans cet exemple, vous avez utilisé la méthode `Stacked Columns` perspective pour afficher les résultats par mois. Cela nous permet de comparer la distribution des nouveaux clients sur une base mensuelle.

## Remplissage {#wrapup}

Avez-vous remarqué dans les exemples ci-dessus que la variable `timestamp`, `groupings`, `perspectives`, et `filters` sont-elles héritées de ses mesures d’entrée ? Gardez à l’esprit que les formules peuvent être utilisées `perspectives` et [options d’heure indépendantes](../../tutorials/time-options-visual-rpt-bldr.md){ : target=&quot;_blank&quot;}, comme le peuvent les mesures.

Si vous avez d’autres questions sur l’utilisation des formules dans la variable `Report Builder`, [support technique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
