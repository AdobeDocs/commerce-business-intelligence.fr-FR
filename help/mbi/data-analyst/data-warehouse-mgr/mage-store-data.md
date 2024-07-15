---
title: Stockage des données dans Adobe Commerce
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

La plateforme [!DNL Adobe Commerce] enregistre et organise une grande variété de données commerciales importantes sur des centaines de tables. Cette rubrique décrit :

* comment ces données sont générées
* ce qui entraîne l’insertion d’une nouvelle ligne dans l’une des [tables Commerce principales](../data-warehouse-mgr/common-mage-tables.md)
* comment les actions telles que faire un achat ou créer un compte sont enregistrées dans la base de données [!DNL Adobe Commerce]

Pour discuter de ces concepts, reportez-vous à l&#39;exemple suivant :

`Clothes4U` est un détaillant de vêtements avec des présences en ligne et en brique et mortier. Il utilise [!DNL Magento Open Source] derrière son site web pour collecter et organiser des données.

## `catalog\_product\_entity`

Nous sommes le 22 septembre et `Clothes4U` déploie trois nouveaux éléments sur sa ligne d&#39;automne : `Throwback Bellbottoms`, `Straight Leg Jeans` et `V-Neck T-Shirts`. Un employé `Clothes4U` ouvre son administrateur Commerce, clique sur **[!UICONTROL Add Product]** et saisit toutes les informations pour `Throwback Bellbottoms`.

Satisfait de tous les paramètres pour `Throwback Bellbottoms`, l’employé clique sur **[!UICONTROL Save]**, ce qui insère la première ligne ci-dessous dans la table `catalog_product_entity`. L’employé répète le processus, en créant un autre produit Commerce pour `Straight Leg Jeans`, puis un troisième pour `V-Neck T-Shirt`, en insérant les deuxième et troisième lignes ci-dessous dans le tableau `catalog_product_entity` :

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pants10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pants11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Chemises6 | 2016/09/22 09:24:02 |

* `entity_id` - Il s’agit de la clé primaire de la table `catalog_product_entity`, ce qui signifie que chaque ligne de la table doit avoir un `entity_id` différent. Chaque `entity_id` sur cette table ne peut être associé qu&#39;à un seul produit, et chaque produit ne peut être associé qu&#39;à un seul `entity_id`.
   * La ligne supérieure du tableau ci-dessus, `entity_id` = 205, correspond à la nouvelle ligne créée pour &quot;Retour en arrière dans les chambres.&quot; Où `entity_id` = 205 apparaît dans la plateforme Commerce, il fait référence au produit &quot;Throwback Bellbas&quot;
* `entity_type_id` - Commerce comporte plusieurs catégories d’objets (comme les clients, les adresses et les produits pour n’en nommer que quelques-unes), et cette colonne est utilisée pour indiquer la catégorie dans laquelle se trouve cette ligne particulière.
   * Comme il s’agit de la table `catalog_product_entity`, chaque ligne possède le même type d’entité : produit. Dans Adobe Commerce, le `entity_type_id` du produit est 4, c’est pourquoi les trois nouveaux produits créés renvoient 4 pour cette colonne.
* `attribute_set_id` - Les ensembles d’attributs sont utilisés pour identifier les produits ayant le même type de descripteurs.
   * Les deux premières lignes du tableau sont les produits `Throwback Bellbottoms` et `Straight Leg Jeans`, qui sont tous deux des pantalons. Ces produits auraient les mêmes descripteurs (par exemple, nom, insertion, ligne de style) et auraient donc le même `attribute_set_id`. Le troisième élément, `V-Neck T-Shirt`, a un `attribute_set_id` différent, car il n&#39;aurait pas les mêmes descripteurs que le pantalon ; les chemises n&#39;ont pas de linge ni d&#39;encre.
* `sku` - Il s’agit de valeurs uniques attribuées à chaque produit par l’utilisateur lors de la création d’un produit dans Adobe Commerce.
* `created_at` - Cette colonne renvoie l’horodatage de la création de chaque produit.

## `customer\_entity`

Peu de temps après l’ajout des trois nouveaux produits, un nouveau client, `Sammy Customer`, consulte pour la première fois le site web de `Clothes4U`. `Clothes4U` n&#39;autorisant pas les commandes d&#39;invités, `Sammy Customer` doit d&#39;abord créer un compte sur le site web. Le client saisit les informations d’identification requises et clique sur l’envoi, ce qui entraîne la nouvelle entrée suivante sur le [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md) :

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` - Tout comme la table précédente, `entity_id` est la clé primaire de la table `customer_entity`.
   * Lorsque `Sammy Customer` a créé un compte et que la ligne ci-dessus a été écrite dans la table `customer_entity`, le client a été affecté `entity_id` = 214. Dans tous les tableaux, le client identifié comme `entity_id` = 214 fait toujours référence à l’utilisateur Sammy Customer
* `entity_type_id` - Cette colonne identifie le type d’entité répertorié dans cette table et fonctionne de la même manière que dans la table `catalog_product_entity`.
   * Chaque ligne de la table `customer_entity` est un client et Commerce définit les clients comme `entity_type_id` 1 par défaut.
* `email` : ce champ est renseigné par le courrier électronique qu’un nouveau client saisit lors de l’établissement de son compte
* `created_at` - Cette colonne renvoie l’horodatage du moment où chaque utilisateur a rejoint

## `sales\_flat\_order (or Sales\_order` si vous avez [!DNL Adobe Commerce 2.x]

Une fois la création du compte terminée, `Sammy Customer` est prêt à commencer un achat. Sur le site web, le client ajoute deux paires `Throwback Bellbottoms` et une `V-Neck T-Shirt` au panier. Satisfait par les sélections, le client passe à l’extraction et envoie la commande, créant l’entrée suivante sur la [ table de commandes plats ](../data-warehouse-mgr/sales-flat-order-table.md) :

| **`entity id`** | **`customer id**` | **`subtotal`** | **`created at`** |
|---|---|---|---|
| 227 | 214 | 94,85 | 2016/09/23 15:41:39 |

* `entity_id` : il s’agit de la clé primaire de la table `sales_flat_order`.
   * Lorsque Sammy Customer a passé cette commande et que la ligne ci-dessus a été écrite dans la table `sales_flat_order`, la commande a été affectée `entity_id` = 227.
* `customer_id` - Cette colonne est l’identifiant unique du client qui a passé cette commande particulière
   * `customer_id` associé à cette commande est 214, qui est le `entity_id` de Sammy Customer sur la table `customer_entity`.
* `subtotal` - Cette colonne est le montant total imputé à un client pour la commande.
   * Les deux paires &quot;Throwback Bellbouteilles&quot; et &quot;V-Neck T-Shirt&quot; coûtent 94,85 dollars au total.
* `created_at` - Cette colonne renvoie l’horodatage du moment où chaque commande a été créée.

## `sales\_flat\_order\_item ( or Sales\_order\_item`

(si vous disposez de Commerce 2.0 ou version ultérieure)

Outre la seule ligne de la table `Sales\_flat\_order`, lorsque `Sammy Customer` envoie la commande, une ligne pour chaque élément unique de cet ordre est insérée dans la [`sales\_flat\_order\_item` table](../data-warehouse-mgr/sales-flat-order-item-table.md) :

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39,95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14,95 |

* `item_id` - Cette colonne est la clé primaire de la table `sales_flat_order_item`
   * La commande de `Sammy Customer` a créé deux lignes sur cette table, car elle contenait deux produits distincts.
* `name` - Cette colonne est le nom du produit
* `product_id` - Cette colonne est l’identifiant unique du produit auquel cette ligne fait référence.
   * La première ligne ci-dessus contient `product_id` = 205 car `Throwback Bellbottoms` a un `entity_id` de 205 sur la table `catalog_product_entity`
* `order_id` - Cette colonne correspond au `entity_id` de l’ordre contenant ces éléments de commande spécifiques.
   * Les deux lignes ci-dessus ont `order_id` = 227 car elles font toutes deux partie de l’ordre placé par `Sammy Customer`, qui a `entity_id` = 227 sur la table `sales_flat_order`.
* `qty_ordered` - Cette colonne correspond au nombre d’unités du produit incluses dans cet ordre spécifique.
   * L’ordre de `Sammy Customer` contenait deux paires de `Throwback Bellbottoms`
* `price` - Cette colonne est le prix d’une seule unité de l’article de commande
   * La `subtotal` de la commande de `Sammy Customer` dans la table `sales_flat_order` était de 94,85, ce qui est la somme de deux paires de `Throwback Bellbottoms` à 39,95 $ chacune et 1 `V-Neck T-Shirt` à 14,95 $.
