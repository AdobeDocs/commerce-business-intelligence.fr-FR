---
title: Traduire les requêtes SQL dans des rapports Commerce Intelligence
description: Découvrez comment les requêtes SQL sont traduites dans les colonnes calculées, les mesures que vous utilisez dans Commerce Intelligence.
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# Traduire les requêtes SQL dans Commerce Intelligence

Vous êtes-vous déjà demandé comment les requêtes SQL sont converties dans les [colonnes calculées](../data-warehouse-mgr/creating-calculated-columns.md), [mesures](../../data-user/reports/ess-manage-data-metrics.md) et les [rapports](../../tutorials/using-visual-report-builder.md) que vous utilisez dans [!DNL Commerce Intelligence] ? Si vous êtes un utilisateur SQL lourd, comprendre comment SQL est traduit dans [!DNL Commerce Intelligence] vous permet de travailler plus intelligemment dans le [Gestionnaire de Data Warehouse](../data-warehouse-mgr/tour-dwm.md) et de tirer le meilleur parti de la plateforme [!DNL Commerce Intelligence].

À la fin de cette rubrique, vous trouverez une **matrice de traduction** pour les clauses de requête SQL et des éléments [!DNL Commerce Intelligence] .

Commencez par examiner une requête générale :

| | |
|--- |--- |
| `SELECT` |  |
| `a,` | Rapport `group by` |
| `SUM(b)` | `Aggregate function` (colonne) |
| `FROM c` | `Source` table |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | Rapport `time frame` |
| `GROUP BY a` | Rapport `group by` |

Cet exemple couvre la plupart des cas de traduction, mais il existe certaines exceptions. Explorez, en commençant par la manière dont la fonction `aggregate` est traduite.

## Fonctions d’agrégation

Les fonctions d’agrégation (par exemple, `count`, `sum`, `average`, `max`, `min`) dans les requêtes prennent la forme d’ **agrégations de mesures** ou d’ **agrégations de colonnes** dans [!DNL Commerce Intelligence]. Le facteur de différenciation est de savoir si une jointure est nécessaire pour effectuer l’agrégation.

Consultez un exemple pour chacun des cas ci-dessus.

## Agrégation des mesures {#aggregate}

Une mesure est requise lors de l&#39;agrégation de `within a single table`. Par exemple, la fonction d’agrégat `SUM(b)` de la requête ci-dessus serait probablement représentée par une mesure qui additionne la colonne `B`. 

Examinez un exemple spécifique de la manière dont une mesure `Total Revenue` peut être définie dans [!DNL Commerce Intelligence]. Examinez la requête ci-dessous que vous tentez de traduire :

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` (colonne) |
| `FROM orders` | `Metric source` table |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Mesure `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | Mesure `timestamp` (et rapport `time range`) |

Accédez au créateur de mesures en cliquant sur **[!UICONTROL Manage Data** > **&#x200B; Mesures &#x200B;**> **Créer une mesure]**, vous devez d’abord sélectionner la table `source` appropriée, qui dans ce cas est la table `orders`. La mesure est ensuite configurée comme illustré ci-dessous :

![Agrégation des mesures](../../assets/Metric_aggregation.png)

## Agrégation des colonnes

Une colonne calculée est requise lors de l’agrégation d’une colonne qui est associée à partir d’un autre tableau. Par exemple, une colonne peut être créée dans votre table `customer` appelée `Customer LTV`, qui additionne la valeur totale de toutes les commandes associées à ce client dans la table `orders`.

La requête de cette agrégation peut ressembler à ce qui suit :

|  |  |
|--- |--- |
| `Select` | |
| `c.customer_id` | Propriétaire de l’agrégat |
| `SUM(o.order_total) as "Customer LTV"` | Opération agrégée(colonne) |
| `FROM customers c` | Table du propriétaire agrégé |
| `JOIN orders o` | Table source d&#39;agrégation |
| `ON c.customer_id = o.customer_id` | Chemin |
| `WHERE o.status = 'success'` | Filtre agrégé |

La configuration de cette fonctionnalité dans [!DNL Commerce Intelligence] nécessite l’utilisation de votre gestionnaire de Data Warehouse, où vous créez un chemin entre votre table `orders` et `customers`, puis créez une colonne appelée `Customer LTV` dans la table de votre client.

Découvrez comment établir un nouveau chemin entre `customers` et `orders`. L’objectif final est de créer une nouvelle colonne agrégée dans la table `customers`. Vous devez donc d’abord accéder à la table `customers` de votre Data Warehouse, puis cliquer sur **[!UICONTROL Create a Column** > **&#x200B; Sélectionner une définition &#x200B;**> **SUM]**.

Vous devez ensuite sélectionner la table source. S’il existe un chemin d’accès à votre table `orders`, sélectionnez-le simplement dans la liste déroulante. Cependant, si vous créez un chemin d’accès, cliquez sur **[!UICONTROL Create new path]** et l’écran ci-dessous s’affiche :

![Créer un chemin](../../assets/Create_new_path.png)

Ici, vous devez examiner attentivement la relation entre les deux tables auxquelles vous essayez de vous joindre. Dans ce cas, il existe potentiellement `Many` commandes associées au client `One`. Par conséquent, la table `orders` est répertoriée du côté `Many`, tandis que la table `customers` sélectionnée du côté `One`.

>[!NOTE]
>
>Dans [!DNL Commerce Intelligence], un `path` équivaut à un `Join` dans SQL.

Une fois le chemin enregistré, vous pouvez créer la colonne `Customer LTV` ! Voir ci-dessous :

![](../../assets/Customer_LTV.gif)

Maintenant que vous avez créé la nouvelle colonne `Customer LTV` dans votre table `customers`, vous êtes prêt à créer une [agrégation de mesures](#aggregate) à l’aide de cette colonne (par exemple, pour trouver la moyenne LTV par client). Vous pouvez également `group by` ou `filter` en fonction de la colonne calculée dans un rapport à l’aide de mesures existantes créées sur la table `customers`.

>[!NOTE]
>
>Pour cette dernière, chaque fois que vous créez une colonne calculée, vous devez [ajouter la dimension aux mesures existantes](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant qu’elle ne soit disponible sous la forme `filter` ou `group by`.

Voir [création de colonnes calculées](../data-warehouse-mgr/creating-calculated-columns.md) avec votre Gestionnaire de Data Warehouse.

## `Group By` clauses

Les fonctions `Group By` des requêtes sont souvent représentées dans [!DNL Commerce Intelligence] sous la forme d’une colonne utilisée pour segmenter ou filtrer un rapport visuel. À titre d’exemple, nous allons revoir la requête `Total Revenue` que vous avez explorée précédemment, mais segmentons cette fois les recettes par le `coupon\_code` pour mieux comprendre quels coupons génèrent le plus de recettes.

Commencez par la requête ci-dessous :

| | |
|--- |--- |
| `SELECT coupon_code,` | Rapport `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`(column) |
| `FROM orders` | `Metric source` table |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Mesure `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | Mesure `timestamp` (et rapport `time range`) |
| `GROUP BY coupon_code` | Rapport `group by` |

>[!NOTE]
>
>La seule différence par rapport à la requête que vous avez lancée précédemment est l’ajout du &quot;coupon\_code&quot; comme groupe par ._

En utilisant la même mesure `Total Revenue` que celle que vous avez créée précédemment, vous êtes maintenant prêt à créer votre rapport de recettes segmenté par code de coupon ! Regardez l’gif ci-dessous qui indique comment configurer ce rapport visuel qui examine les données de septembre à novembre :

![ Recettes par code de coupon](../../assets/Revenue_by_coupon_code.gif)

## Formules

Parfois, une requête peut impliquer plusieurs agrégations afin de calculer la relation entre des colonnes distinctes. Par exemple, vous pouvez calculer la valeur de commande moyenne dans une requête de l’une des deux façons suivantes :

* `AVG('order\_total')` OU
* `SUM('order\_total')/COUNT('order\_id')`

La première méthode impliquerait la création d’une nouvelle mesure qui effectue une moyenne sur la colonne `order\_total`. Toutefois, la dernière méthode peut être créée directement dans le créateur de rapports en supposant que des mesures soient déjà configurées pour calculer les `Total Revenue` et `Number of orders`.

Revenez en arrière et examinez la requête globale pour `Average order value` :

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | Mesure `operation` (colonne) |
| `COUNT(order_id) as "Number of orders"` | Mesure `operation` (colonne) |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | Mesure `operation` (colonne) / Opération de mesure (colonne) |
| `FROM orders` | Table de mesures `source` |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Mesure `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | Horodatage des mesures (et période des rapports) |

Supposons maintenant que des mesures soient déjà configurées pour calculer les `Total Revenue` et `Number of orders`. Comme ces mesures existent, vous pouvez simplement ouvrir le `Report Builder` et créer un calcul à la demande à l’aide de la fonction `Formula` :

![Forumula AOV](../../assets/AOV_forumula.gif)

## Remplissage

Si vous êtes un utilisateur SQL lourd, penser à la façon dont les requêtes se traduisent dans [!DNL Commerce Intelligence] vous permet de créer des colonnes, des mesures et des rapports calculés.

Pour une référence rapide, consultez le tableau ci-dessous. Cela affiche l’élément [!DNL Commerce Intelligence] équivalent d’une clause SQL et la manière dont elle peut mapper à plusieurs éléments, selon la manière dont elle est utilisée dans la requête.

## Éléments Commerce Intelligence

| **`SQL Clause`** | **`Metric`** | **`Filter`** | **`Report group by`** | **`Report time frame`** | **`Path`** | **`Calculated column inputs`** | **`Source table`** |
|---|---|---|---|---|---|---|---|
| `SELECT` | X | - | X | - | - | X | - |
| `FROM` | - | - | - | - | - | - | X |
| `WHERE` | - | X | - | - | - | - | - |
| `WHERE` (avec éléments de temps) | - | - | - | X | - | - | - |
| `JOIN...ON` | - | X | - | - | X | X | - |
| `GROUP BY` | - | - | X | - | - | - | - |
