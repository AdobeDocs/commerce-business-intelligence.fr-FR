---
title: Création ou suppression de chemins d’accès pour les colonnes calculées
description: Découvrez comment définir un chemin d’accès décrivant comment le tableau sur lequel vous créez une colonne est lié au tableau à partir duquel vous extrayez des informations.
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Création ou suppression de chemins d’accès pour les colonnes calculées

## Actualiseur des colonnes calculées

Lors de la [création de colonnes calculées](../data-warehouse-mgr/creating-calculated-columns.md) dans votre Data Warehouse, vous êtes invité à définir un chemin d’accès décrivant comment le tableau sur lequel vous créez une colonne est lié au tableau à partir duquel vous extrayez des informations. Pour réussir la création d’un chemin d’accès, vous devez savoir deux choses :

1. Relation entre les tables de vos bases de données
1. Les clés primaires et étrangères qui définissent cette relation

Si vous connaissez ces informations, vous pouvez facilement créer un chemin d’accès en suivant les instructions de cette rubrique. Vous pouvez demander l’avis d’un expert technique de votre entreprise ou contacter l’équipe [Services professionnels](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr).

## Actualisations des relations entre les tables et des types de clés {#refresher}

### Relations entre les tables {#relationships}

Ce concept est traité dans l’article [ Comprendre et évaluer les relations entre les tables ](../../data-analyst/data-warehouse-mgr/table-relationships.md), mais un résumé rapide ne fait de mal à personne, n’est-ce pas ?

Les tables peuvent être liées les unes aux autres de trois manières :

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | La relation entre les personnes et les numéros de permis de conduire. Une personne ne peut avoir qu&#39;un seul numéro de permis de conduire, et un numéro de permis de conduire appartient à une seule personne. |
| **`one-to-many`** | La relation entre les commandes et les articles : une commande peut contenir de nombreux articles, mais un article appartient à une seule commande. Dans ce cas, la table des commandes est le côté « un » et la table des articles le côté « plusieurs ». |
| **`many-to-many`** | Relation entre les produits et les catégories : un produit peut appartenir à de nombreuses catégories, et une catégorie peut contenir de nombreux produits. |

{style="table-layout:auto"}

Lorsqu&#39;une relation entre deux tables est comprise, elle peut être utilisée pour déterminer le chemin d&#39;accès à créer pour importer des informations d&#39;une table à une autre. Cette étape suivante nécessite de connaître les clés primaires et étrangères qui facilitent une relation de table.

### Principal et clés étrangères {#keys}

Une `Primary Key` est une colonne ou un ensemble de colonnes immuable qui produit des valeurs uniques dans un tableau. Par exemple, lorsqu’un client passe une commande sur un site web, une nouvelle ligne est ajoutée au tableau `orders` de votre panier, avec une nouvelle `order_id`. Cette `order_id` permet au client et à l’entreprise de suivre l’avancement de cette commande spécifique. L’ID de commande étant unique, il s’agit généralement de la `Primary Key` d’une table `orders`.

Une `Foreign Key` est une colonne créée dans un tableau qui est liée à la colonne `Primary Key` d&#39;un autre tableau. Les clés étrangères créent des références entre les tables, ce qui permet aux analystes de rechercher et de lier facilement des enregistrements. Supposons que vous souhaitiez savoir quelles commandes appartenaient à chacun de vos clients. La colonne `customer id` (`Primary Key` de la table `customers`) et la colonne `order_id` (`Foreign Key` dans la table `customers`, référençant la `Primary Key` de la table `orders`) permettent de relier et d&#39;analyser ces informations. Lors de la création d’un chemin d’accès, vous êtes invité à définir les `Primary Key` et les `Foreign Key`.

## Création d’un chemin {#createpath}

Lors de la création d’une colonne dans votre Data Warehouse, vous devez définir le chemin qui transfère les informations d’une table vers une autre. Parfois, les chemins d’accès sont préremplis, car un chemin d’accès existe entre les tables, mais si ce n’est pas le cas, vous devez en créer un.

Utilisez la relation entre **clients** et **commandes** pour vous montrer comment procéder. En panne :

* La relation est `one-to-many` : un client peut avoir plusieurs commandes, mais une commande ne peut avoir qu’un seul client. Elle indique la direction de la relation ou l’emplacement de création de la colonne calculée. Dans ce cas, cela signifie que les informations de la table `orders` peuvent être introduites dans la table `customers`.
* La `primary key` que vous souhaitez utiliser est `customers.customerid` ou la colonne `customer ID` du tableau `customers`.
* La `foreign key` que vous souhaitez utiliser est `orders.customerid` ou la colonne `customer ID` du tableau `orders`.

Vous pouvez maintenant créer le chemin d’accès .

1. Cliquez sur **[!UICONTROL Data > Data Warehouse]**.
1. Dans la liste Tableau, cliquez sur le tableau dans lequel vous souhaitez créer la colonne. Dans cet exemple, il s’agit de la table `customers`.
1. Le schéma du tableau s’affiche. Cliquez sur **[!UICONTROL Create New Column]**.
1. Attribuez un nom à votre colonne, par exemple `Customer's orders`.
1. Sélectionnez la définition de la colonne. Consultez le [Guide des colonnes calculées](../data-warehouse-mgr/creating-calculated-columns.md) pour obtenir un aide-mémoire pratique.
1. Dans la liste déroulante [!UICONTROL Select table and column], cliquez sur l’option **[!UICONTROL Create new path]** .

   ![Boîte de dialogue modale Création de chemins pour les colonnes calculées](../../assets/Creating_Paths_modal.png)

1. À l’aide des listes déroulantes, sélectionnez les clés primaire et étrangère de chaque tableau.

   Du côté `Many`, vous sélectionnez `orders.customerid` : souvenez-vous que les clients peuvent passer de nombreuses commandes.

   Sur le côté `One`, vous sélectionnez `customers.customerid` - une commande ne peut avoir qu’un seul client.

1. Cliquez sur **[!UICONTROL Save]** pour enregistrer le chemin d’accès et terminer la création de la colonne.

### Limites de la création de chemins d’accès {#limits}

* **[!DNL Commerce Intelligence]ne peut pas deviner les relations clé primaire/clé étrangère**. Vous ne souhaitez pas introduire de données incorrectes dans votre compte. Par conséquent, la création de chemins d’accès doit être effectuée manuellement.

* **Actuellement, les chemins ne peuvent être spécifiés qu’entre deux tables différentes**. La logique que vous essayez de recréer implique-t-elle plus de deux tables ? Il peut alors être judicieux de (1) joindre les colonnes à une table intermédiaire d’abord, puis à la table « destination finale », ou (2) consulter l’équipe [Services professionnels](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) pour trouver la meilleure approche pour atteindre vos objectifs.

* **Une colonne ne peut être que la référence de clé étrangère d’UN chemin à la fois**. Par exemple, si `order_items.order_id` pointe vers `orders.id`, `order_items.order_id` ne pouvez pas pointer vers autre chose.

* Techniquement, il est possible de créer des chemins d’accès **`Many-to-many`, mais ils produisent souvent des données erronées, car aucun des deux côtés n’est une véritable clé `one-to-many` étrangère**. La meilleure façon d’aborder ces chemins dépend toujours de l’analyse spécifique souhaitée. Consultez l&#39;équipe d&#39;analystes RJ pour découvrir la meilleure solution.

Si vous ne pouvez pas créer de colonne calculée en raison d’une ou de plusieurs des limitations ci-dessus, contactez l’assistance en fournissant une description de la colonne en question

## Suppression d’un chemin d’accès de colonne calculé {#delete}

Un chemin d’accès incorrect a-t-il été créé dans votre Data Warehouse ? Ou peut-être que vous faites un peu de nettoyage de printemps et que vous voulez faire le ménage ? Si vous devez supprimer un chemin d’accès de votre compte, vous pouvez [envoyer un ticket aux analystes de l’assistance Adobe](../../guide-overview.md#Submitting-a-Support-Ticket). **Veillez à inclure le nom du chemin d’accès !**

## Conclusion {#wrapup}

Maintenant que vous êtes à l’aise avec la création de chemins d’accès pour les colonnes calculées dans votre Data Warehouse. Si vous n’êtes toujours pas sûr d’un chemin en particulier, souvenez-vous que vous pouvez toujours cliquer sur **[!UICONTROL Support]** dans votre compte [!DNL Commerce Intelligence] pour obtenir de l’aide.

## Connexe

* [Compréhension et évaluation des relations entre les tables](../data-warehouse-mgr/table-relationships.md)
* [Création de chemins d’accès pour les colonnes calculées](../data-warehouse-mgr/create-paths-calc-columns.md)
* [Types de colonnes calculées](../data-warehouse-mgr/calc-column-types.md) tentative de création.
