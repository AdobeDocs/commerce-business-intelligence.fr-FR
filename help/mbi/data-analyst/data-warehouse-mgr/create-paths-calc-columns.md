---
title: Création ou suppression de chemins d’accès pour les colonnes calculées
description: Découvrez comment définir un chemin décrivant la relation entre le tableau sur lequel vous créez une colonne et le tableau à partir duquel vous extrayez des informations.
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# Création ou suppression de chemins pour les colonnes calculées

## Actualisation des colonnes calculées

When [création de colonnes calculées](../data-warehouse-mgr/creating-calculated-columns.md) dans votre Data Warehouse, vous serez invité à définir un chemin décrivant la manière dont le tableau sur lequel vous créez une colonne est associé au tableau à partir duquel vous extrayez des informations. Pour créer un chemin, vous devez connaître deux éléments :

1. Comment les tables de vos bases de données se relient les unes aux autres
1. Clés Principale et étrangère qui définissent cette relation

Si vous connaissez ces informations, vous pourrez facilement créer un chemin suivant les instructions de cet article. Nous avons fourni un aperçu de ces concepts si vous n’êtes pas certain, mais que vous souhaitez peut-être demander à un expert technique de votre entreprise ou contacter notre équipe d’assistance.

## Rafraîchissements sur les relations de table et les types clés {#refresher}

### Relations entre les tables {#relationships}

Nous avons abordé ce concept en profondeur dans notre [Comprendre et évaluer l&#39;article sur les relations entre les tables](../../data-analyst/data-warehouse-mgr/table-relationships.md)mais un résumé rapide n&#39;a jamais fait de mal à personne, n&#39;est-ce pas ?

Les tableaux peuvent être associés les uns aux autres de trois façons :

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | La relation entre les gens et les numéros de permis de conduire. Une personne peut avoir un et un seul numéro de permis de conduire, et un numéro de permis de conduire appartient à une seule et même personne. |
| **`one-to-many`** | La relation entre les commandes et les éléments : une commande peut contenir de nombreux éléments, mais un élément appartient à une seule commande. Dans ce cas, le tableau des commandes est le côté et le tableau des éléments le côté multiple. |
| **`many-to-many`** | La relation entre les produits et les catégories : un produit peut appartenir à de nombreuses catégories et une catégorie peut contenir de nombreux produits. |

{style=&quot;table-layout:auto&quot;}

Une fois qu’une relation entre deux tables est comprise, elle peut être utilisée pour déterminer le chemin à créer afin d’apporter des informations d’une table à une autre. Cette étape suivante nécessite de connaître les clés Principales et étrangères qui facilitent une relation de tableau.

### Principale et clés étrangères {#keys}

A `Primary Key` est une colonne ou un ensemble de colonnes immuable qui produit des valeurs uniques dans un tableau. Par exemple, lorsqu’un client effectue une commande sur un site web, une nouvelle ligne est ajoutée à la variable `orders` dans votre panier, avec une nouvelle `order_id`. Ceci `order_id` permet au client et à l’entreprise de suivre l’avancement de cette commande spécifique. Comme l’ID de commande est unique, il s’agit généralement de la variable `Primary Key` de `orders` table.

A `Foreign Key` est une colonne créée dans un tableau lié à la variable `Primary Key` d’une autre table. Les clés étrangères créent des références entre les tables, ce qui permet aux analystes de rechercher facilement des enregistrements et de les lier. Disons que nous voulions savoir quelles commandes appartiennent à chacun de nos clients. Le `customer id` column (`Primary Key` de `customers` ) et la variable `order_id` column (`Foreign Key` dans le `customers` table, référençant la variable `Primary Key` de `orders` ) nous permet de lier et d&#39;analyser ces informations. Lors de la création d’un chemin, vous serez invité à définir les deux `Primary Key` et `Foreign Key`.

## Création d’un chemin {#createpath}

Lors de la création d’une colonne dans l’entrepôt de données, vous devez définir le chemin qui amène les informations d’un tableau dans un autre. Parfois, les chemins sont prérenseignés car il existe déjà un chemin entre les tableaux, mais si cela ne se produit pas, vous devrez en créer un.

Nous utilisons la relation entre **clients** et **commandes** pour vous montrer comment c’est fait. Répartition :

* La relation est `one-to-many` - un client peut avoir plusieurs commandes, mais une commande ne peut avoir qu’un seul client. Cela nous indique l’orientation de la relation ou l’endroit où la colonne calculée doit être créée. Dans ce cas, cela signifie que des informations provenant de la variable `orders` peut être placé dans la table `customers` table.
* Le `primary key` Nous voulons utiliser : `customers.customerid`, ou la variable `customer ID` dans la colonne `customers` table.
* Le `foreign key` Nous voulons utiliser : `orders.customerid`, ou la variable `customer ID` dans la colonne `orders` table.

Maintenant, nous vous guidons pour créer le chemin.

1. Cliquez sur **[!UICONTROL Data > Data Warehouse]**.
1. Dans la liste des tableaux, cliquez sur le tableau dans lequel vous souhaitez créer la colonne. Dans notre exemple, il s’agit de la variable `customers` table.
1. Le schéma du tableau s’affiche. Cliquez sur **[!UICONTROL Create New Column]**.
1. Attribuez un nom à votre colonne, par exemple : `Customer's orders`.
1. Sélectionnez la définition de la colonne. Consultez la section [Guide des colonnes calculées](../data-warehouse-mgr/creating-calculated-columns.md) pour un aide-mémoire pratique.
1. Dans le [!UICONTROL Select table and column] dans la liste déroulante, cliquez sur **[!UICONTROL Create new path]** .

   ![Création de chemins pour le modal de colonnes calculées](../../assets/Creating_Paths_modal.png)

1. Dans les listes déroulantes, sélectionnez les clés Principale et étrangère pour chaque table.

   Sur le `Many` côté, sélectionnez `orders.customerid` - souvenez-vous que les clients peuvent avoir de nombreuses commandes.

   Sur le `One` côté, sélectionnez `customers.customerid` - une commande ne peut avoir qu’un seul client.

1. Cliquez sur **[!UICONTROL Save]** pour enregistrer le chemin et terminer la création de la colonne.

### Limites de la création de chemins {#limits}

* **[!DNL MBI]ne peut pas deviner les relations de clé Principale/étrangère**. Nous ne souhaitons pas introduire de données incorrectes dans votre compte. Par conséquent, la création de chemins d’accès doit être effectuée manuellement.
* **Actuellement, les chemins ne peuvent être spécifiés que entre deux tables différentes.**. La logique que vous essayez de recréer implique-t-elle plus de deux tables ? Il peut alors être logique (1) de joindre d’abord les colonnes à une table intermédiaire, puis à la table &quot;destination finale&quot;, ou (2) de consulter notre équipe pour trouver la meilleure approche pour vos objectifs.
* **Une colonne ne peut être la référence de clé étrangère que pour un seul chemin à la fois.**. Par exemple, si `order_items.order_id` pointe vers `orders.id`, puis `order_items.order_id` ne peut pointer vers rien d’autre.
* **`Many-to-many`les chemins peuvent techniquement être créés, mais produisent très souvent des données incorrectes, car aucun côté n’est un vrai `one-to-many` clé étrangère**. La meilleure façon d’aborder ces chemins dépend toujours de l’analyse spécifique souhaitée. Consultez l’équipe d’analystes RJ pour découvrir la meilleure solution.

Si vous ne pouvez pas créer de colonne calculée en raison d’une ou de plusieurs des restrictions ci-dessus, contactez l’assistance avec une description de la colonne que vous êtes.

## Suppression d’un chemin de colonne calculé {#delete}

Création d’un chemin d’accès incorrect dans votre Data Warehouse ? Ou peut-être que vous faites un petit ménage de printemps et que vous voulez ranger ? Si vous devez supprimer un chemin d’accès de votre compte, vous pouvez [envoyer un ticket à nos analystes de support](../../guide-overview.md). **Veillez à inclure le nom du chemin.**

## Remplissage {#wrapup}

Vous devez maintenant vous sentir à l’aise lors de la création de chemins pour les colonnes calculées dans votre Data Warehouse. Si vous n’êtes toujours pas sûr d’un chemin particulier, n’oubliez pas que vous pouvez toujours cliquer sur **[!UICONTROL Support]** dans votre [!DNL MBI] pour obtenir de l’aide.

## Associé

* [Comprendre et évaluer les relations entre les tables](../data-warehouse-mgr/table-relationships.md)
* [Création de chemins pour les colonnes calculées](../data-warehouse-mgr/create-paths-calc-columns.md)
* [Types de colonne calculés](../data-warehouse-mgr/calc-column-types.md) tentative de création.
