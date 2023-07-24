---
title: Types de colonne calculés
description: Découvrez comment créer des colonnes afin d’augmenter et d’optimiser vos données d’analyse.
exl-id: 1af79b9e-77ff-4fc6-917a-4e6743b95035
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 0%

---

# Types de colonne calculés

* [Mêmes calculs de tableau](#sametable)
* [Un ou plusieurs calculs](#onetomany)
* [Plusieurs à un calcul](#manytoone)
* [Carte de référence pratique](#map)
* [Colonnes calculées avancées](#advanced)

Dans le [Gestionnaire de Data Warehouse](../data-warehouse-mgr/tour-dwm.md), vous pouvez créer des colonnes afin d’augmenter et d’optimiser vos données d’analyse. [Cette fonctionnalité](../data-warehouse-mgr/creating-calculated-columns.md) pour y accéder, sélectionnez n’importe quel tableau dans le Gestionnaire de Data Warehouse et cliquez sur **[!UICONTROL Create New Column]**.

Cette rubrique décrit les types de colonnes que vous pouvez créer à l’aide du Gestionnaire de Data Warehouse. Elle couvre également la description, une présentation visuelle de cette colonne et une [table de référence](#map) de toutes les entrées requises pour créer une colonne. Il existe trois manières de créer des colonnes calculées :

1. [Même tableau que les colonnes calculées](#sametable)
1. [Colonnes calculées de type &quot;un à plusieurs&quot;](#onetomany)
1. [Colonnes calculées multiples-à-un](#manytoone)

## Même tableau que les colonnes calculées {#sametable}

Ces colonnes sont construites à l’aide de colonnes d’entrée du même tableau.

### Age {#age}

Une colonne calculée d’âge renvoie le nombre de secondes entre l’heure actuelle et une heure d’entrée.

L’exemple ci-dessous crée `Seconds since customer's most recent order` dans le `customers` table. Cela peut être utilisé pour créer des listes d’utilisateurs de clients qui n’ont pas effectué d’achats (parfois appelés &quot;perte&quot;) dans `X days`.

![](../../assets/age.gif)

### Convertisseur de devises

Une colonne calculée de conversion de devise convertit la devise native d’une colonne en la nouvelle devise souhaitée.

L’exemple ci-dessous crée `base\_grand\_total In AED`, en convertissant le `base\_grand\_total` Il s’agit de la devise native vers AED dans la variable `sales\_flat\_order` table. Cette colonne fonctionne bien pour les magasins avec plusieurs devises qui souhaitent générer des rapports dans leur devise locale.

Pour les clients Commerce, la variable `base\_currency\_code` stocke généralement les devises natives. Le `Spot Time` doit correspondre à la date utilisée dans vos mesures.

![](../../assets/currency_converter.png)

## Colonnes calculées de type &quot;un à plusieurs&quot; {#onetomany}

`One-to-Many` colonnes [utiliser un chemin entre deux tableaux ;](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md). Ce chemin implique toujours une table, où réside un attribut, et une table, où cet attribut est &quot;déplacé&quot; vers. Le chemin peut être décrit comme une `foreign key--primary key` relation.

### Colonne liée {#joined}

Une colonne jointe relocalise un attribut sur une table. *to* la table multiple. L’exemple classique d’un/de plusieurs est le nombre de clients (un) et de commandes (plusieurs).

Dans l’exemple ci-dessous, la variable `Customer's group\_id` est associée à la dimension `orders` table.

![](../../assets/joined_column.gif)

## Colonnes calculées multiples-à-un {#manytoone}

Ces colonnes utilisent les mêmes chemins que les colonnes de type &quot;un à plusieurs&quot;, mais elles pointent les données dans la direction opposée. La colonne est créée d’un côté du chemin, par opposition au côté multiple. En raison de cette relation, la valeur de la colonne doit être une agrégation, c’est-à-dire une opération mathématique effectuée sur les points de données du côté multiple. Il existe de nombreux cas d’utilisation à cet effet. Quelques-uns sont répertoriés ci-dessous.

### Count {#count}

Ce type de colonne calculée renvoie le nombre de valeurs sur le tableau de nombreuses *onto* la seule table.

Dans l’exemple ci-dessous, la dimension `Customer's lifetime number of canceled orders` est créé sur le `customers` tableau (avec filtre pour `orders.status`).

![](../../assets/many_to_one.gif){ : width=&quot;699&quot; height=&quot;351&quot;}

### Somme {#sum}

Une colonne de somme calculée est la somme des valeurs de la variable `many` sur la seule table.

Vous pouvez l’utiliser pour créer des dimensions au niveau du client, telles que `Customer's lifetime revenue`.

### Min. ou Max. {#minmax}

Une colonne calculée min. ou max. renvoie le plus petit ou le plus grand enregistrement existant de plusieurs côtés.

Vous pouvez l’utiliser pour créer des dimensions au niveau du client, telles que `Customer's first order date`.

### Existe {#exists}

Une colonne calculée est un test binaire déterminant la présence d’un enregistrement du côté multiple. En d’autres termes, la nouvelle colonne renvoie un `1` si le chemin connecte au moins une ligne dans chaque tableau, et `0` si aucune connexion ne peut être établie.

Ce type de dimension peut déterminer, par exemple, si un client a déjà acheté un produit particulier. Utiliser une jointure entre une `customers` table et `orders` tableau, filtre d’un produit spécifique, dimension `Customer has purchased Product X?` peuvent être créés.

## Carte de référence pratique {#map}

Si vous rencontrez des difficultés à vous souvenir de toutes les entrées lors de la création d’une colonne calculée, conservez cette carte de référence pratique lorsque vous créez :

![](../../assets/merged_reference_map.png)

## Colonnes calculées avancées {#advanced}

Dans votre quête d’analyse et de réponse aux questions sur votre entreprise, vous pouvez rencontrer une situation dans laquelle vous ne pouvez pas créer la colonne exacte que vous souhaitez.

Pour garantir un retour rapide, Adobe recommande d’extraire le [Types de colonne calculés avancés](../../data-analyst/data-warehouse-mgr/adv-calc-columns.md) pour voir le type de colonnes que l’équipe d’assistance Adobe peut créer. Cette rubrique couvre également les informations dont vous avez besoin pour créer la colonne, en les incluant avec votre requête.

## Documentation connexe

* [Créer des colonnes calculées](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)
* [Création/suppression de chemins pour les colonnes calculées](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)
* [Comprendre et évaluer les relations entre les tables](../../data-analyst/data-warehouse-mgr/table-relationships.md)
