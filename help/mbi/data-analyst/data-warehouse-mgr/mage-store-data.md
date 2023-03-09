---
title: Stockage des données dans Commerce
description: Découvrez comment les données sont générées, ce qui entraîne l’insertion d’une nouvelle ligne et comment les actions sont enregistrées dans la base de données Commerce.
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 3%

---

# Stockage des données dans [!DNL Adobe Commerce]

La plateforme Adobe Commerce enregistre et organise un large éventail de données commerciales importantes sur des centaines de tables. Cette rubrique décrit :

* comment ces données sont générées
* ce qui entraîne exactement l’insertion d’une nouvelle ligne dans l’une des [Tables de commerce principales](../data-warehouse-mgr/common-mage-tables.md)
* comment les actions telles que réaliser un achat ou créer un compte sont enregistrées dans la base de données Commerce

Pour expliquer ces concepts, reportez-vous à l&#39;exemple suivant :

`Clothes4U` est un détaillant de vêtements disposant d’une présence en ligne et d’une présence en briques et mortiers. Il utilise le Magento Open Source derrière son site web pour collecter et organiser des données.

## `catalog\_product\_entity`

Nous sommes le 22 septembre et `Clothes4U` est en train de déployer trois nouveaux éléments à sa ligne d’automne : `Throwback Bellbottoms`, `Straight Leg Jeans`, et `V-Neck T-Shirts`. A `Clothes4U` L’employé ouvre son administrateur Commerce, clique sur **[!UICONTROL Add Product]** et saisit toutes les informations pour `Throwback Bellbottoms`.

Satisfait à tous les paramètres pour `Throwback Bellbottoms`, l’employé clique **[!UICONTROL Save]**, qui insère la première ligne ci-dessous dans le `catalog_product_entity` table. L’employé répète le processus, en créant un autre produit Commerce pour `Straight Leg Jeans`, puis un troisième pour `V-Neck T-Shirt`, insérant les deuxième et troisième lignes ci-dessous dans le `catalog_product_entity` table :

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pants10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pants11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Shirts6 | 2016/09/22 09:24:02 |

* `entity_id` - Il s’agit de la clé Principale de la variable `catalog_product_entity` , ce qui signifie que chaque ligne du tableau doit avoir une `entity_id`. Chaque `entity_id` sur cette table ne peut être associé qu’à un seul produit et chaque produit ne peut être associé qu’à un seul. `entity_id`
   * La ligne supérieure du tableau ci-dessus, `entity_id` = 205, est la nouvelle ligne créée pour &quot;Throwback Bellbouteilles.&quot; Partout `entity_id` = 205 apparaît dans la plateforme Commerce, il fait référence au produit &quot;Throwback Bellbas&quot;
* `entity_type_id` - Commerce possède plusieurs catégories d’objets (comme des clients, des adresses et des produits pour n’en nommer que quelques-unes). Cette colonne est utilisée pour indiquer la catégorie dans laquelle se trouve cette ligne particulière.
   * Il s’agit du `catalog_product_entity` , chaque ligne possède le même type d’entité : produit. Dans Adobe Commerce, la variable `entity_type_id` pour le produit est 4, c’est pourquoi les trois nouveaux produits créés renvoient 4 pour cette colonne.
* `attribute_set_id` - Les ensembles d’attributs sont utilisés pour identifier les produits qui ont le même type de descripteurs.
   * Les deux premières lignes du tableau sont les suivantes : `Throwback Bellbottoms` et `Straight Leg Jeans` les produits, qui sont tous deux des pantalons. Ces produits auraient les mêmes descripteurs (par exemple, nom, insertion, ligne de style) et, par conséquent, auraient les mêmes `attribute_set_id`. Le troisième élément, `V-Neck T-Shirt` a une variable `attribute_set_id` parce qu&#39;il n&#39;aurait pas les mêmes descripteurs que le pantalon; les chemises n&#39;ont ni lingettes ni crayons.
* `sku` - Il s’agit de valeurs uniques attribuées à chaque produit par l’utilisateur lors de la création d’un produit dans Adobe Commerce.
* `created_at` - Cette colonne renvoie l’horodatage de la création de chaque produit.

## `customer\_entity`

Peu après l&#39;ajout des trois nouveaux produits, un nouveau client, `Sammy Customer`, visites `Clothes4U`pour la première fois. Depuis `Clothes4U` n’autorise pas les commandes d’invités, `Sammy Customer` doit d’abord créer un compte sur le site web. Le client saisit les informations d’identification requises et clique sur l’envoi, ce qui entraîne la nouvelle entrée suivante sur le [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` - Tout comme la table précédente, `entity_id` est la clé Principale de la variable `customer_entity` table.
   * When `Sammy Customer` a créé un compte et la ligne ci-dessus a été écrite dans la variable `customer_entity` table, le client a été affecté `entity_id` = 214. Dans tous les tableaux, le client s’est identifié comme `entity_id` = 214 fait toujours référence à l’utilisateur Sammy Customer
* `entity_type_id` - Cette colonne identifie le type d’entité répertorié dans ce tableau et fonctionne de la même manière que dans la variable `catalog_product_entity` table
   * Chaque ligne du `customer_entity` est un client et Commerce définit les clients comme `entity_type_id` 1 par défaut
* `email` - ce champ est renseigné par le courrier électronique qu’un nouveau client saisit lors de l’établissement de son compte
* `created_at` - Cette colonne renvoie l’horodatage du moment où chaque utilisateur a rejoint

## `sales\_flat\_order (or Sales\_order` si vous disposez de Commerce 2.0 ou version ultérieure)

Une fois la création du compte terminée, `Sammy Customer` est prêt à commencer à effectuer un achat. Sur le site web, le client ajoute deux paires de la variable `Throwback Bellbottoms` et un `V-Neck T-Shirt` au panier. Satisfait par les sélections, le client passe à l’extraction et envoie la commande, créant ainsi l’entrée suivante sur la page [table des commandes plats](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**`**`subtotal`****`created at`** |
|---|---|---|---|
| 227 | 214 | 94.85 | 2016/09/23 15:41:39 |

* `entity_id` - il s’agit de la clé Principale de la variable `sales_flat_order` table.
   * Lorsque Sammy Customer a passé cette commande, la ligne ci-dessus a été écrite dans la variable `sales_flat_order` table, la commande a été affectée. `entity_id` = 227.
* `customer_id` - Cette colonne est l’identifiant unique du client qui a passé cette commande particulière.
   * Le `customer_id` associé à cette commande est 214, qui est la variable `entity_id` sur le `customer_entity` table.
* `subtotal` - Cette colonne est le montant total imputé à un client pour la commande.
   * Les deux paires &quot;Throwback Bellbouteilles&quot; et &quot;V-Neck T-Shirt&quot; coûtent 94,85 dollars au total.
* `created_at` - Cette colonne renvoie l’horodatage de la création de chaque commande.

## `sales\_flat\_order\_item ( or Sales\_order\_item` si vous disposez de Commerce 2.0 ou version ultérieure)

En plus de la seule ligne de la `Sales\_flat\_order` table, lorsque `Sammy Customer` envoie la commande, une ligne pour chaque élément unique dans cet ordre est insérée dans la variable [`sales\_flat\_order\_item` table](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39.95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14.95 |

* `item_id` - Cette colonne est la clé Principale de la variable `sales_flat_order_item` table
   * `Sammy Customer`La commande de a créé deux lignes sur cette table, car elle contenait deux produits distincts.
* `name` - Cette colonne correspond au nom du produit.
* `product_id` - Cette colonne est l’identifiant unique du produit auquel cette ligne fait référence.
   * La première ligne ci-dessus comporte `product_id` = 205 car `Throwback Bellbottoms` avoir une `entity_id` de 2005 sur la `catalog_product_entity` table
* `order_id` - Cette colonne correspond à la variable `entity_id` de l’ordre contenant ces éléments de commande spécifiques ;
   * Les deux lignes ci-dessus comportent `order_id` = 227, car elles font toutes deux partie de la commande placée par `Sammy Customer`, qui a `entity_id` = 227 sur la `sales_flat_order` table
* `qty_ordered` - Cette colonne correspond au nombre d’unités du produit incluses dans cet ordre spécifique.
   * `Sammy Customer`L’ordre de contient deux paires `Throwback Bellbottoms`
* `price` - Cette colonne est le prix d’une unité de l’article de commande
   * Le `subtotal` de `Sammy Customer`dans l’ordre `sales_flat_order` était de 94,85, ce qui représente la somme de deux paires de `Throwback Bellbottoms` à 39,95 $ chacune et 1 `V-Neck T-Shirt` à 14,95 $.
