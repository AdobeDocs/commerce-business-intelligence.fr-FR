---
title: Types de colonnes calculées
description: Découvrez comment créer des colonnes pour augmenter et optimiser vos données à analyser.
exl-id: 1af79b9e-77ff-4fc6-917a-4e6743b95035
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---

# Types de colonnes calculées

* [Mêmes calculs de table](#sametable)
* [Calculs un à plusieurs](#onetomany)
* [Calculs plusieurs à un](#manytoone)
* [Carte de référence pratique](#map)
* [Colonnes calculées avancées](#advanced)

Dans [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md), vous pouvez créer des colonnes pour augmenter et optimiser vos données pour l&#39;analyse. [Cette fonctionnalité](../data-warehouse-mgr/creating-calculated-columns.md) est accessible en sélectionnant n’importe quel tableau dans le gestionnaire Data Warehouse et en cliquant sur **[!UICONTROL Create New Column]**.

Cette rubrique décrit les types de colonnes que vous pouvez créer avec Data Warehouse Manager. Elle comprend également la description, une présentation visuelle de cette colonne et un [mappage de référence](#map) de toutes les entrées requises pour créer une colonne. Vous pouvez créer des colonnes calculées de trois manières différentes :

1. [Mêmes colonnes calculées dans le tableau](#sametable)
1. [Colonnes calculées de type « un à plusieurs »](#onetomany)
1. [Colonnes calculées multiples-à-un](#manytoone)

## Mêmes colonnes calculées dans le tableau {#sametable}

Ces colonnes sont créées à partir des colonnes d’entrée du même tableau.

### Âge {#age}

Une colonne calculée sur l’âge renvoie le nombre de secondes entre l’heure actuelle et une heure d’entrée.

L’exemple ci-dessous crée des `Seconds since customer's most recent order` dans le tableau `customers` . Vous pouvez l’utiliser pour créer des listes d’utilisateurs et d’utilisatrices de clients et clientes qui n’ont pas effectué d’achats (parfois appelées résiliation) dans `X days`.

![](../../assets/age.gif)

### Convertisseur de devises

Une colonne calculée du convertisseur de devises convertit la devise native d’une colonne en une nouvelle devise souhaitée.

L’exemple ci-dessous crée des `base\_grand\_total In AED`, en convertissant la `base\_grand\_total` de sa devise native en AED dans le tableau `sales\_flat\_order` . Cette colonne fonctionne bien pour les magasins qui utilisent plusieurs devises et qui souhaitent générer des rapports dans leur devise locale.

Pour les clients Commerce, le champ `base\_currency\_code` stocke généralement les devises natives. Le champ `Spot Time` doit correspondre à la date utilisée dans vos mesures.

![](../../assets/currency_converter.png)

## Colonnes calculées de type « un à plusieurs » {#onetomany}

`One-to-Many` colonnes [utilisez un chemin entre deux tableaux](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md). Ce chemin d’accès implique toujours une table unique, où réside un attribut, et une table multiple, où cet attribut est « déplacé » vers le bas. Le chemin d’accès peut être décrit comme une relation `foreign key--primary key`.

### Colonne jointe {#joined}

Une colonne jointe déplace un attribut sur une table *vers* la table multiple. L’exemple classique de un/plusieurs est clients (un) et commandes (plusieurs).

Dans l’exemple ci-dessous, la dimension `Customer's group\_id` est intégrée dans le tableau `orders`.

![](../../assets/joined_column.gif)

## Colonnes calculées multiples-à-un {#manytoone}

Ces colonnes utilisent les mêmes chemins que les colonnes de type « un à plusieurs », mais elles orientent les données dans la direction opposée. La colonne est créée d’un côté du chemin, par opposition au côté « plusieurs ». En raison de cette relation, la valeur de la colonne doit être une agrégation, c’est-à-dire une opération mathématique effectuée sur les points de données du côté multiple. Il existe de nombreux cas d’utilisation à cet effet, dont certains sont répertoriés ci-dessous.

### Nombre {#count}

Ce type de colonne calculée renvoie le nombre de valeurs sur le tableau multiple *sur* le seul tableau.

Dans l’exemple ci-dessous, la dimension `Customer's lifetime number of canceled orders` est créée dans le tableau `customers` (avec un filtre pour les `orders.status`).

![](../../assets/many_to_one.gif){: width="699" height="351"}

### Somme {#sum}

Une colonne calculée de somme est la somme des valeurs du tableau `many` sur le tableau unique.

Vous pouvez l’utiliser pour créer des dimensions au niveau du client comme `Customer's lifetime revenue`.

### Min ou Max {#minmax}

Une colonne calculée min ou max renvoie l’enregistrement le plus petit ou le plus grand qui existe sur le côté « plusieurs ».

Vous pouvez l’utiliser pour créer des dimensions au niveau du client comme `Customer's first order date`.

### Existe {#exists}

Une colonne calculée est un test binaire déterminant la présence d’un enregistrement du côté « plusieurs ». En d’autres termes, la nouvelle colonne renvoie une `1` si le chemin d’accès connecte au moins une ligne dans chaque tableau, et `0` si aucune connexion ne peut être établie.

Ce type de dimension peut déterminer, par exemple, si un client a déjà acheté un produit particulier. En utilisant une jointure entre une table de `customers` et `orders` table, un filtre pour un produit spécifique, un `Customer has purchased Product X?` de dimension peut être créé.

## Carte de référence pratique {#map}

Si vous avez des difficultés à vous souvenir de toutes les entrées lors de la création d’une colonne calculée, gardez cette carte de référence à portée de main lorsque vous créez :

![](../../assets/merged_reference_map.png)

## Colonnes calculées avancées {#advanced}

Dans votre quête d&#39;analyse et de réponses aux questions sur votre entreprise, vous pourriez être confronté à une situation où vous ne pouvez pas créer la colonne exacte que vous voulez.

Pour garantir une exécution rapide, Adobe recommande de consulter le guide [Types de colonnes calculées avancés](../../data-analyst/data-warehouse-mgr/adv-calc-columns.md) pour voir quels types de colonnes l’équipe d’assistance d’Adobe peut créer. Cette rubrique couvre également les informations dont vous avez besoin pour créer la colonne - incluez-la avec votre demande.

## Documentation connexe

* [Créer des colonnes calculées](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)
* [Création/suppression de chemins d’accès pour les colonnes calculées](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)
* [Compréhension et évaluation des relations entre les tables](../../data-analyst/data-warehouse-mgr/table-relationships.md)
