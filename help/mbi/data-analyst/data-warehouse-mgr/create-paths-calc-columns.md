---
title: Création ou suppression de chemins d’accès pour les colonnes calculées
description: Découvrez comment définir un chemin décrivant la relation entre le tableau sur lequel vous créez une colonne et le tableau à partir duquel vous extrayez des informations.
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Création ou suppression de chemins pour les colonnes calculées

## Actualisation des colonnes calculées

Lorsque vous [ créez des colonnes calculées ](../data-warehouse-mgr/creating-calculated-columns.md) dans votre Data Warehouse, vous êtes invité à définir un chemin décrivant la façon dont le tableau sur lequel vous créez une colonne est associé à la table à partir de laquelle vous extrayez des informations. Pour créer un chemin, vous devez connaître deux éléments :

1. Comment les tables de vos bases de données se relient les unes aux autres
1. Clés primaire et étrangère qui définissent cette relation

Si vous connaissez ces informations, vous pouvez facilement créer un chemin suivant les instructions de cette rubrique. Vous pouvez demander à un expert technique de votre entreprise ou contacter l&#39;[équipe des services professionnels](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr).

## Rafraîchissements sur les relations de table et les types clés {#refresher}

### Relations entre les tables {#relationships}

Ce concept est traité dans l&#39; [article Comprendre et évaluer les relations de table](../../data-analyst/data-warehouse-mgr/table-relationships.md), mais un résumé rapide n&#39;a jamais fait de mal à personne, n&#39;est-ce pas ?

Les tableaux peuvent être associés les uns aux autres de trois façons :

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | La relation entre les gens et les numéros de permis de conduire. Une personne ne peut avoir qu&#39;un seul numéro de permis de conduire, et un numéro de permis de conduire appartient à une seule personne. |
| **`one-to-many`** | La relation entre les commandes et les éléments : une commande peut contenir de nombreux éléments, mais un élément appartient à une seule commande. Dans ce cas, le tableau des commandes est le côté et le tableau des éléments le côté multiple. |
| **`many-to-many`** | La relation entre les produits et les catégories : un produit peut appartenir à de nombreuses catégories et une catégorie peut contenir de nombreux produits. |

{style="table-layout:auto"}

Lorsqu’une relation entre deux tables est comprise, elle peut être utilisée pour déterminer le chemin à créer afin d’apporter des informations d’une table à une autre. Cette étape suivante nécessite de connaître les clés primaires et étrangères qui facilitent une relation de tableau.

### Principal et clés étrangères {#keys}

Un `Primary Key` est une colonne ou un ensemble de colonnes immuable qui produit des valeurs uniques dans un tableau. Par exemple, lorsqu’un client effectue une commande sur un site web, une nouvelle ligne est ajoutée à la table `orders` de votre panier, avec un nouveau `order_id`. Ce `order_id` permet au client et à l’entreprise de suivre l’avancement de cette commande spécifique. Comme l’ID de commande est unique, il s’agit généralement de la `Primary Key` d’une table `orders`.

Un `Foreign Key` est une colonne créée dans une table qui est liée à la colonne `Primary Key` d’une autre table. Les clés étrangères créent des références entre les tables, ce qui permet aux analystes de rechercher et de lier facilement des enregistrements. Dites que vous vouliez savoir quelles commandes appartiennent à chacun de vos clients. La colonne `customer id` (`Primary Key` de la table `customers`) et la colonne `order_id` (`Foreign Key` dans la table `customers`, référençant le `Primary Key` de la table `orders`) nous permettent de lier et d’analyser ces informations. Lors de la création d’un chemin d’accès, vous êtes invité à définir les `Primary Key` et `Foreign Key`.

## Création d’un chemin {#createpath}

Lors de la création d’une colonne dans votre Data Warehouse, vous devez définir le chemin qui amène les informations d’un tableau dans un autre. Parfois, les chemins sont prérenseignés car il existe un chemin entre les tableaux, mais si cela ne se produit pas, vous devez en créer un.

Utilisez la relation entre **clients** et **commandes** pour vous montrer comment procéder. Répartition :

* La relation est `one-to-many` : un client peut avoir plusieurs commandes, mais une commande ne peut avoir qu’un seul client. Cela nous indique l’orientation de la relation ou l’endroit où la colonne calculée doit être créée. Dans ce cas, cela signifie que les informations de la table `orders` peuvent être importées dans la table `customers`.
* `primary key` que vous souhaitez utiliser est `customers.customerid`, ou la colonne `customer ID` de la table `customers`.
* `foreign key` que vous souhaitez utiliser est `orders.customerid`, ou la colonne `customer ID` de la table `orders`.

Vous pouvez maintenant créer le chemin.

1. Cliquez sur **[!UICONTROL Data > Data Warehouse]**.
1. Dans la liste des tableaux, cliquez sur le tableau dans lequel vous souhaitez créer la colonne. Dans cet exemple, il s’agit de la table `customers`.
1. Le schéma du tableau s’affiche. Cliquez sur **[!UICONTROL Create New Column]**.
1. Donnez un nom à votre colonne, par exemple, `Customer's orders`.
1. Sélectionnez la définition de la colonne. Consultez le [Guide des colonnes calculées](../data-warehouse-mgr/creating-calculated-columns.md) pour obtenir une aide-mémoire pratique.
1. Dans la liste déroulante [!UICONTROL Select table and column], cliquez sur l’option **[!UICONTROL Create new path]** .

   ![Création de chemins pour les colonnes calculées modale](../../assets/Creating_Paths_modal.png)

1. Dans les listes déroulantes, sélectionnez les clés primaire et étrangère pour chaque table.

   Du côté `Many`, vous sélectionnez `orders.customerid` - Souvenez-vous que les clients peuvent avoir de nombreuses commandes.

   Du côté `One`, vous sélectionnez `customers.customerid` : une commande ne peut avoir qu&#39;un seul client.

1. Cliquez sur **[!UICONTROL Save]** pour enregistrer le chemin et terminer la création de la colonne.

### Limites de la création de chemins {#limits}

* **[!DNL Commerce Intelligence]ne peut pas deviner les relations de clé primaire/étrangère**. Vous ne souhaitez pas introduire des données incorrectes dans votre compte. Par conséquent, la création de chemins d’accès doit être effectuée manuellement.

* **Actuellement, les chemins ne peuvent être spécifiés que entre deux tables différentes**. La logique que vous essayez de recréer implique-t-elle plus de deux tables ? Il peut alors être logique (1) de joindre d&#39;abord les colonnes à une table intermédiaire, puis à la table &quot;destination finale&quot;, ou (2) de consulter l&#39;[équipe des services professionnels](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) pour trouver la meilleure approche pour vos objectifs.

* **Une colonne ne peut être que la référence de clé étrangère pour UN chemin à la fois**. Par exemple, si `order_items.order_id` pointe vers `orders.id`, alors `order_items.order_id` ne peut pointer vers rien d’autre.

* **`Many-to-many`chemins d’accès peuvent techniquement être créés, mais produisent souvent des données incorrectes car aucun des côtés n’est une `one-to-many` clé étrangère** vraie. La meilleure façon d’aborder ces chemins dépend toujours de l’analyse spécifique souhaitée. Consultez l’équipe d’analystes RJ pour découvrir la meilleure solution.

Si vous ne pouvez pas créer de colonne calculée en raison d’une ou de plusieurs des restrictions ci-dessus, contactez l’assistance technique avec une description de la colonne que vous êtes.

## Suppression d’un chemin de colonne calculé {#delete}

Création d’un chemin incorrect dans votre Data Warehouse ? Ou peut-être que vous faites un petit ménage de printemps et que vous voulez ranger ? Si vous devez supprimer un chemin d’accès de votre compte, vous pouvez [envoyer un ticket à des analystes de support d’Adobe](../../guide-overview.md#Submitting-a-Support-Ticket). **Veillez à inclure le nom du chemin !**

## Remplissage {#wrapup}

Maintenant que vous êtes à l’aise avec la création de chemins pour les colonnes calculées dans votre Data Warehouse. Si vous n’êtes toujours pas sûr d’un chemin particulier, n’oubliez pas que vous pouvez toujours cliquer sur **[!UICONTROL Support]** dans votre compte [!DNL Commerce Intelligence] pour obtenir de l’aide.

## Associé

* [Comprendre et évaluer les relations entre les tables](../data-warehouse-mgr/table-relationships.md)
* [Création de chemins pour les colonnes calculées](../data-warehouse-mgr/create-paths-calc-columns.md)
* [Types de colonne calculés](../data-warehouse-mgr/calc-column-types.md) en tentant de créer.
