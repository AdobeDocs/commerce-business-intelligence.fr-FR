---
title: Traduction de requêtes SQL dans des rapports Commerce Intelligence
description: Découvrez comment les requêtes SQL sont traduites dans les colonnes calculées, les mesures que vous utilisez dans Commerce Intelligence.
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
source-git-commit: 3bf4829543579d939d959753eb3017364c6465bd
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Traduire les requêtes SQL dans Commerce Intelligence

Vous êtes déjà demandé comment les requêtes SQL sont traduites dans [colonnes calculées](../data-warehouse-mgr/creating-calculated-columns.md), [mesures](../../data-user/reports/ess-manage-data-metrics.md), et [rapports](../../tutorials/using-visual-report-builder.md) vous utilisez dans [!DNL Commerce Intelligence]? Si vous êtes un utilisateur SQL lourd, comprenez comment SQL est traduit dans [!DNL Commerce Intelligence] vous permet de travailler plus intelligemment dans le [Gestionnaire de Data Warehouse](../data-warehouse-mgr/tour-dwm.md) et tirez le meilleur parti de [!DNL Commerce Intelligence] plateforme.

À la fin de cette rubrique, vous trouverez un **matrice de traduction** pour les clauses de requête SQL et [!DNL Commerce Intelligence] éléments .

Commencez par examiner une requête générale :

|  |  |
|--- |--- |
| `SELECT` |  |
| `a,` | Rapport `group by` |
| `SUM(b)` | `Aggregate function` (colonne) |
| `FROM c` | `Source` table |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | Rapport `time frame` |
| `GROUP BY a` | Rapport `group by` |

Cet exemple couvre la plupart des cas de traduction, mais il existe certaines exceptions. Explorez, en commençant par la façon dont la variable `aggregate` est traduite.

## Fonctions d’agrégation

Fonctions d’agrégation (par exemple, `count`, `sum`, `average`, `max`, `min`) dans les requêtes sous la forme **agrégations de mesures** ou **agrégations de colonnes** in [!DNL Commerce Intelligence]. Le facteur de différenciation est de savoir si une jointure est nécessaire pour effectuer l’agrégation.

Consultez un exemple pour chacun des cas ci-dessus.

## Agrégation des mesures {#aggregate}

Une mesure est requise lors de l’agrégation `within a single table`. Par exemple, la variable `SUM(b)` la fonction d’agrégat de la requête ci-dessus serait probablement représentée par une mesure qui additionne les colonnes `B`. 

Examinez un exemple spécifique de la manière dont une `Total Revenue` peut être définie dans [!DNL Commerce Intelligence]. Examinez la requête ci-dessous que vous essayez de traduire :

|  |  |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` (colonne) |
| `FROM orders` | `Metric source` table |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Mesure `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | Mesure `timestamp` (et création de rapports) `time range`) |

Accédez au créateur de mesures en cliquant sur **[!UICONTROL Manage Data** > ** Mesures **> **Créer une mesure]**, vous devez d’abord sélectionner la `source` qui, dans ce cas, correspond à la variable `orders` table. La mesure est ensuite configurée comme illustré ci-dessous :

![Agrégation des mesures](../../assets/Metric_aggregation.png)

## Agrégation des colonnes

Une colonne calculée est requise lors de l’agrégation d’une colonne qui est associée à partir d’un autre tableau. Par exemple, une colonne peut être créée dans votre `customer` table appelée `Customer LTV`, qui additionne la valeur totale de toutes les commandes associées à ce client dans la variable `orders` table.

La requête de cette agrégation peut ressembler à ce qui suit :

|  |  |
|--- |--- |
| `Select` |  |
| `c.customer_id` | Propriétaire de l’agrégat |
| `SUM(o.order_total) as "Customer LTV"` | Opération agrégée(colonne) |
| `FROM customers c` | Table du propriétaire agrégé |
| `JOIN orders o` | Table source d&#39;agrégation |
| `ON c.customer_id = o.customer_id` | Chemin |
| `WHERE o.status = 'success'` | Filtre agrégé |

Configuration de [!DNL Commerce Intelligence] nécessite l’utilisation de votre gestionnaire de Data Warehouse, où vous créez un chemin entre vos `orders` et `customers` puis créer une colonne appelée `Customer LTV` dans la table de votre client.

Découvrez comment établir un nouveau chemin entre les `customers` et `orders`. L’objectif final est de créer une colonne agrégée dans la variable `customers` , accédez donc d’abord à la `customers` dans votre Data Warehouse, puis cliquez sur **[!UICONTROL Create a Column** > ** Sélectionner une définition **> **SUM]**.

Vous devez ensuite sélectionner la table source. S’il existe un chemin d’accès à votre `orders` , sélectionnez-la simplement dans la liste déroulante. Cependant, si vous créez un chemin, cliquez sur **[!UICONTROL Create new path]** et l’écran ci-dessous s’affiche :

![Créer un chemin](../../assets/Create_new_path.png)

Ici, vous devez examiner attentivement la relation entre les deux tables auxquelles vous essayez de vous joindre. Dans ce cas, il existe des `Many` commandes associées à `One` , par conséquent la variable `orders` est répertoriée dans la `Many` , tandis que la variable `customers` sélectionnée sur la `One` côté.

>[!NOTE]
>
>Dans [!DNL Commerce Intelligence], un `path` équivaut à un `Join` dans SQL.

Une fois le chemin enregistré, vous pouvez créer la variable `Customer LTV` colonne ! Voir ci-dessous :

![](../../assets/Customer_LTV.gif)

Maintenant que vous avez construit le nouveau `Customer LTV` dans votre `customers` , vous êtes prêt à créer une [agrégation des mesures](#aggregate) en utilisant cette colonne (par exemple, pour trouver la moyenne LTV par client). Vous pouvez également `group by` ou `filter` par la colonne calculée d’un rapport en utilisant des mesures existantes créées sur la variable `customers` table.

>[!NOTE]
>
>Pour ce dernier, chaque fois que vous créez une colonne calculée, vous devez [ajouter la dimension aux mesures existantes ;](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant d’être disponible en tant que `filter` ou `group by`.

Voir [création de colonnes calculées](../data-warehouse-mgr/creating-calculated-columns.md) avec votre gestionnaire de Data Warehouse.

## `Group By` clauses

`Group By` les fonctions des requêtes sont souvent représentées dans [!DNL Commerce Intelligence] comme colonne utilisée pour segmenter ou filtrer un rapport visuel. À titre d’exemple, nous allons revoir la `Total Revenue` requête que vous avez explorée précédemment, mais segmentez cette fois les recettes par la variable `coupon\_code` pour mieux comprendre quels coupons génèrent le plus de recettes.

Commencez par la requête ci-dessous :

|  |  |
|--- |--- |
| `SELECT coupon_code,` | Rapport `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`(colonne) |
| `FROM orders` | `Metric source` table |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Mesure `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | Mesure `timestamp` (et création de rapports) `time range`) |
| `GROUP BY coupon_code` | Rapport `group by` |

>[!NOTE]
>
>La seule différence par rapport à la requête que vous avez lancée précédemment est l’ajout du &quot;coupon\_code&quot; comme groupe par ._

En utilisant la même `Total Revenue` que vous avez créé précédemment, vous êtes maintenant prêt à créer votre rapport des recettes segmentées par code de coupon ! Regardez l’gif ci-dessous qui indique comment configurer ce rapport visuel qui examine les données de septembre à novembre :

![Recettes par code de coupon](../../assets/Revenue_by_coupon_code.gif)

## Formules

Parfois, une requête peut impliquer plusieurs agrégations afin de calculer la relation entre des colonnes distinctes. Par exemple, vous pouvez calculer la valeur de commande moyenne dans une requête de l’une des deux façons suivantes :

* `AVG('order\_total')` OU
* `SUM('order\_total')/COUNT('order\_id')`

La première méthode impliquerait la création d’une nouvelle mesure qui effectue une moyenne sur la variable `order\_total` colonne . Toutefois, la dernière méthode peut être créée directement dans le créateur de rapports en supposant que des mesures soient déjà configurées pour calculer la variable `Total Revenue` et `Number of orders`.

Revenez en arrière et examinez la requête globale pour `Average order value`:

|  |  |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | Mesure `operation` (colonne) |
| `COUNT(order_id) as "Number of orders"` | Mesure `operation` (colonne) |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | Mesure `operation` (colonne) / Opération de mesure(colonne) |
| `FROM orders` | Mesure `source` table |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Mesure `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | Horodatage des mesures (et période de création de rapports) |

Maintenant, supposons que des mesures sont déjà configurées pour calculer la variable `Total Revenue` et `Number of orders`. Comme ces mesures existent, vous pouvez simplement ouvrir la variable `Report Builder` et créer un calcul à la demande à l’aide du `Formula` fonctionnalité :

![Forumula de AOV](../../assets/AOV_forumula.gif)

## Remplissage

Si vous êtes un utilisateur SQL lourd, pensez à la façon dont les requêtes se traduisent en [!DNL Commerce Intelligence] vous permet de créer des colonnes, des mesures et des rapports calculés.

Pour une référence rapide, consultez le tableau ci-dessous. Ceci affiche l’équivalent d’une clause SQL [!DNL Commerce Intelligence] et la façon dont il peut mapper à plusieurs éléments, selon la manière dont il est utilisé dans la requête.

## Éléments d’intelligence de commerce

|**`SQL Clause`**|**`Metric`**|**`Filter`**|**`Report group by`**|**`Report time frame`**|**`Path`**|**`Calculated column inputs`**|**`Source table`**| |—|—|—|—|—|—|—|—|—|— |`SELECT`|X|-|X|-|-|X|-| |`FROM`|-|-|-|-|-|-|-|X| |`WHERE`|-|X|-|-|-|-|-|-| |`WHERE` (avec des éléments temporels)|-|-|-|X|-|-|-| |`JOIN...ON`|-|X|-|-|X|X|-| |`GROUP BY`|-|-|X|-|-|-|-|-|
