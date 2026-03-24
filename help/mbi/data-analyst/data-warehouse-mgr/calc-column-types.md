---
title: Types de colonnes calculées
description: Découvrez comment créer des colonnes pour augmenter et optimiser vos données à analyser.
exl-id: 1af79b9e-77ff-4fc6-917a-4e6743b95035
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
TQID: https://experienceleague.adobe.com/41EjlLtffc-ZE-LO6oKMyXcs9Lnv35yxj8BgM6iIWsQ
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 741
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

![Démonstration animée de la création de la colonne de calcul de l&#39;âge](../../assets/age.gif)

### Convertisseur de devises

Une colonne calculée du convertisseur de devises convertit la devise native d’une colonne en une nouvelle devise souhaitée.

L’exemple ci-dessous crée des `base\_grand\_total In AED`, en convertissant la `base\_grand\_total` de sa devise native en AED dans le tableau `sales\_flat\_order` . Cette colonne fonctionne bien pour les magasins qui utilisent plusieurs devises et qui souhaitent générer des rapports dans leur devise locale.

Pour les clients Commerce, le champ `base\_currency\_code` stocke généralement les devises natives. Le champ `Spot Time` doit correspondre à la date utilisée dans vos mesures.

![Configuration de la colonne calculée du convertisseur de devises](../../assets/currency_converter.png)

## Colonnes calculées de type « un à plusieurs » {#onetomany}

`One-to-Many` colonnes [utilisez un chemin entre deux tableaux](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md). Ce chemin d’accès implique toujours une table unique, où réside un attribut, et une table multiple, où cet attribut est « déplacé » vers le bas. Le chemin d’accès peut être décrit comme une relation `foreign key--primary key`.

### Colonne jointe {#joined}

Une colonne jointe déplace un attribut sur une table *vers* la table multiple. L’exemple classique de un/plusieurs est clients (un) et commandes (plusieurs).

Dans l’exemple ci-dessous, la dimension `Customer's group\_id` est intégrée dans le tableau `orders`.

![Démonstration animée de la création de tables de liaison de colonnes jointes](../../assets/joined_column.gif)

## Colonnes calculées multiples-à-un {#manytoone}

Ces colonnes utilisent les mêmes chemins que les colonnes de type « un à plusieurs », mais elles orientent les données dans la direction opposée. La colonne est créée d’un côté du chemin, par opposition au côté « plusieurs ». En raison de cette relation, la valeur de la colonne doit être une agrégation, c’est-à-dire une opération mathématique effectuée sur les points de données du côté multiple. Il existe de nombreux cas d’utilisation à cet effet, dont certains sont répertoriés ci-dessous.

### Nombre {#count}

Ce type de colonne calculée renvoie le nombre de valeurs sur le tableau multiple *sur* le seul tableau.

Dans l’exemple ci-dessous, la dimension `Customer's lifetime number of canceled orders` est créée dans le tableau `customers` (avec un filtre pour les `orders.status`).

![Démonstration animée de l’agrégation de plusieurs colonnes à une](../../assets/many_to_one.gif){: width="699" height="351"}

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

![Mappage de référence montrant la configuration des colonnes calculées fusionnées](../../assets/merged_reference_map.png)

## Colonnes calculées avancées {#advanced}

Dans votre quête d&#39;analyse et de réponses aux questions sur votre entreprise, vous pourriez être confronté à une situation où vous ne pouvez pas créer la colonne exacte que vous voulez.

Pour garantir une exécution rapide, Adobe recommande de consulter le guide [Types de colonnes calculées avancés](../../data-analyst/data-warehouse-mgr/adv-calc-columns.md) pour voir quels types de colonnes l’équipe d’assistance d’Adobe peut créer. Cette rubrique couvre également les informations dont vous avez besoin pour créer la colonne - incluez-la avec votre demande.

## Documentation connexe

* [Créer des colonnes calculées](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)
* [Création/suppression de chemins d’accès pour les colonnes calculées](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)
* [Compréhension et évaluation des relations entre les tables](../../data-analyst/data-warehouse-mgr/table-relationships.md)
