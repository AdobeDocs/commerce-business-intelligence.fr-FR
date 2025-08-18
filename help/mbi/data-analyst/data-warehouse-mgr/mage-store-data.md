---
title: Stockage de données dans Adobe Commerce
description: Découvrez comment les données sont générées, ce qui entraîne l’insertion d’une nouvelle ligne et comment les actions sont enregistrées dans la base de données Adobe Commerce.
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 2%

---

# Stockage des données dans [!DNL Adobe Commerce]

La plateforme [!DNL Adobe Commerce] enregistre et organise une grande variété de données commerciales précieuses sur des centaines de tables. Cette rubrique décrit :

* comment ces données sont générées ;
* ce qui entraîne l’insertion d’une nouvelle ligne dans l’un des [ Tableaux Commerce principaux ](../data-warehouse-mgr/common-mage-tables.md)
* comment les actions telles que l’achat ou la création d’un compte sont enregistrées dans la base de données [!DNL Adobe Commerce]

Pour discuter de ces concepts, reportez-vous à l’exemple suivant :

`Clothes4U` est un retailer de vêtements avec des présences en ligne et en brique et mortier. Il utilise les [!DNL Magento Open Source] de son site Web pour recueillir et organiser des données.

## `catalog\_product\_entity`

Nous sommes le 22 septembre et `Clothes4U` déploie trois nouveaux éléments sur sa ligne d&#39;automne : `Throwback Bellbottoms`, `Straight Leg Jeans` et `V-Neck T-Shirts`. Un employé `Clothes4U` ouvre son administrateur Commerce, clique sur **[!UICONTROL Add Product]** et saisit toutes les informations à `Throwback Bellbottoms`.

Satisfait de tous les paramètres de `Throwback Bellbottoms`, l&#39;employé clique sur **[!UICONTROL Save]**, ce qui insère la première ligne ci-dessous dans le tableau `catalog_product_entity`. L’employé répète le processus, en créant un autre produit Commerce pour `Straight Leg Jeans`, puis un troisième pour `V-Neck T-Shirt`, en insérant les deuxième et troisième lignes ci-dessous dans le tableau `catalog_product_entity` :

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pantalon10 | 22/09/2016 09:15:43 |
| 206 | 4 | 8 | Pantalon11 | 22/09/2016 09:18:17 |
| 207 | 4 | 12 | Chemises6 | 22/09/2016 09:24:02 |

* `entity_id` - Il s’agit de la clé primaire de la table `catalog_product_entity`, ce qui signifie que chaque ligne de la table doit avoir une `entity_id` différente. Chaque `entity_id` de ce tableau ne peut être associé qu’à un seul produit et chaque produit ne peut être associé qu’à un seul `entity_id`
   * La ligne supérieure du tableau ci-dessus, `entity_id` = 205, est la nouvelle ligne créée pour « Throwback Bellbottoms ». Lorsque `entity_id` = 205 apparaît sur la plateforme Commerce, il fait référence au produit « Throwback Bellbottoms »
* `entity_type_id` - Commerce comporte plusieurs catégories d’objets (tels que les clients, les adresses et les produits, pour n’en citer que quelques-uns) et cette colonne est utilisée pour indiquer la catégorie dans laquelle se trouve cette ligne particulière.
   * Comme il s’agit de la table `catalog_product_entity`, chaque ligne possède le même type d’entité : product. Dans Adobe Commerce, la `entity_type_id` du produit est de 4. C’est pourquoi les trois nouveaux produits créés renvoient 4 pour cette colonne.
* `attribute_set_id` - Les jeux d’attributs sont utilisés pour identifier les produits qui ont le même nombre de descripteurs.
   * Les deux premières rangées du tableau sont les produits `Throwback Bellbottoms` et `Straight Leg Jeans`, qui sont tous deux des pantalons. Ces produits auraient les mêmes descripteurs (par exemple, nom, couture, tour de taille), et donc les mêmes `attribute_set_id`. Le troisième article, `V-Neck T-Shirt` a un `attribute_set_id` différent parce qu&#39;il n&#39;aurait pas les mêmes descripteurs que le pantalon ; les chemises n&#39;ont pas de taille ou d&#39;inseams.
* `sku` - Il s’agit de valeurs uniques attribuées à chaque produit par l’utilisateur ou l’utilisatrice lors de la création d’un produit dans Adobe Commerce.
* `created_at` - Cette colonne renvoie la date et l’heure de création de chaque produit

## `customer\_entity`

Peu après l&#39;ajout des trois nouveaux produits, un nouveau client, `Sammy Customer`, visite le site Web de `Clothes4U` pour la première fois. Comme `Clothes4U` n’autorise pas les commandes de clients, `Sammy Customer` devez d’abord créer un compte sur le site web. Le client saisit les informations d’identification requises et clique sur Envoyer, ce qui entraîne la nouvelle entrée suivante sur le [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md) :

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` - Tout comme la table précédente, `entity_id` est la clé primaire de la table `customer_entity`.
   * Lorsque `Sammy Customer` avez créé un compte et que la ligne ci-dessus a été écrite dans le tableau `customer_entity`, le client a été affecté `entity_id` = 214. Dans toutes les tables, le client identifié comme `entity_id` = 214 fait toujours référence à l’utilisateur Sammy Customer
* `entity_type_id` - Cette colonne identifie le type d&#39;entité répertorié dans ce tableau et fonctionne de la même manière que dans le tableau `catalog_product_entity`
   * Chaque ligne du tableau `customer_entity` est un client, et Commerce définit les clients sur `entity_type_id` 1 par défaut
* `email` - ce champ est renseigné par l’e-mail qu’un nouveau client saisit lors de l’ouverture de son compte
* `created_at` - Cette colonne renvoie la date et l’heure de l’inscription de chaque utilisateur

## `sales\_flat\_order (or Sales\_order` si vous avez [!DNL Adobe Commerce 2.x]

Une fois la création du compte terminée, `Sammy Customer` est prêt à commencer à effectuer un achat. Sur le site web, le client ajoute deux paires de `Throwback Bellbottoms` et une `V-Neck T-Shirt` au panier. Satisfait des sélections, le client passe en caisse et soumet la commande, créant ainsi l&#39;entrée suivante dans le tableau [commande client à commandes fixes](../data-warehouse-mgr/sales-flat-order-table.md) :

| **`entity id`** | **`customer id**` | **`subtotal`** | **`created at`** |
|---|---|---|---|
| 227 | 214 | 94,85 | 23/09/2016 15:41:39 |

* `entity_id` : il s’agit de la clé primaire de la table `sales_flat_order`.
   * Lorsque Sammy Customer a passé cette commande et que la ligne ci-dessus a été écrite dans la table `sales_flat_order`, la commande a été affectée `entity_id` = 227.
* `customer_id` - Cette colonne est l&#39;identifiant unique du client qui a passé cette commande particulière
   * Le `customer_id` associé à cette commande est le 214, qui est le `entity_id` de Sammy Customer sur la table `customer_entity`.
* `subtotal` - Cette colonne représente le montant total facturé au client pour la commande
   * Les deux paires de « Throwback Bellbottoms » et le « V-Neck T-Shirt » ont coûté 94,85 dollars au total
* `created_at` - Cette colonne renvoie la date et l’heure de création de chaque commande

## `sales\_flat\_order\_item ( or Sales\_order\_item`

(si vous disposez de Commerce 2.0 ou d’une version ultérieure)

Outre la ligne unique de la table `Sales\_flat\_order`, lorsque `Sammy Customer` soumettez la commande, une ligne pour chaque élément unique de cet ordre est insérée dans la table [`sales\_flat\_order\_item` : ](../data-warehouse-mgr/sales-flat-order-item-table.md)

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39,95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14,95 |

* `item_id` - Cette colonne est la clé primaire de la table `sales_flat_order_item`
   * La commande de `Sammy Customer` a créé deux lignes sur cette table, car elle contenait deux produits distincts
* `name` - Cette colonne correspond au nom du produit
* `product_id` - Cette colonne est l’identifiant unique du produit auquel cette ligne fait référence
   * La première ligne ci-dessus a une `product_id` = 205, car `Throwback Bellbottoms` avez une `entity_id` de 205 sur le tableau `catalog_product_entity`
* `order_id` - Cette colonne est la `entity_id` de la commande qui contient ces éléments de commande spécifiques
   * Les deux lignes ci-dessus ont `order_id` = 227 car elles font toutes deux partie de la commande passée par `Sammy Customer`, qui a `entity_id` = 227 dans le tableau `sales_flat_order`
* `qty_ordered` - Cette colonne indique le nombre d&#39;unités du produit incluses dans cet ordre spécifique
   * L&#39;ordre de `Sammy Customer` contenait deux paires de `Throwback Bellbottoms`
* `price` - Cette colonne représente le prix d&#39;une seule unité de l&#39;article de commande
   * Le `subtotal` de la commande de `Sammy Customer` dans le tableau `sales_flat_order` était de 94,85, soit la somme de deux paires de `Throwback Bellbottoms` à 39,95 $ chacune et d&#39;un `V-Neck T-Shirt` à 14,95 $.
