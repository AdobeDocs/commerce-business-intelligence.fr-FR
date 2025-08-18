---
title: table sales_order_item
description: Découvrez comment utiliser la table sales_order_item.
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# `sales_order_item` Table

La table `sales_order_item` (`sales_flat_order_item` sur M1) contient des enregistrements de tous les produits achetés dans une commande. Chaque ligne représente un `sku` unique inclus dans une commande. La quantité d’unités achetées pour un `sku` spécifique est le plus souvent représentée par le champ `qty_ordered` .

## Types de produits

Le `sales_order_item` capture les détails de tous les [types de produits](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) achetés. Une pratique courante dans [!DNL Adobe Commerce] consiste à proposer des produits configurables, ou en d’autres termes, un produit qui peut être personnalisé en fonction de la taille, de la couleur et d’autres attributs du produit. Bien qu’un produit configurable ait ses propres `sku`, il peut se rapporter à plusieurs produits simples, où chaque produit simple représente une configuration de produit unique. Pour plus d’informations, voir [configuration des produits](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/).

Prenons l’exemple d’un produit configurable tel qu’un t-shirt. Lorsqu’un client extrait, il sélectionne des options pour modifier la couleur et la taille. Si le client sélectionne une couleur de `blue` et une taille de `small`, il finit par acheter un produit simple comme `t-shirt-blue-small` qui renvoie au produit parent de `t-shirt`.

Lorsqu&#39;un produit configurable est inclus dans une commande, deux lignes sont générées dans le tableau de `sales_order_item` : une pour le [&#128279;](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html)simple`sku` et une pour le parent [configurable](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html). Ces deux enregistrements de la table `sales_order_item` peuvent être mis en relation l&#39;un avec l&#39;autre à travers la jointure suivante :

* (simple) `sales_order_item.parent_item_id` => (configurable) `sales_order_item.item_id`

Il est donc possible de générer des rapports sur les ventes de produits soit au niveau simple, soit au niveau configurable. Par défaut, toutes les mesures de `order-item-level` standard dans [!DNL Commerce Intelligence] sont configurées pour exclure les produits simples et *uniquement* générer des rapports sur les versions configurables. Pour ce faire, utilisez le jeu de filtres `Ordered products we count`, qui filtre la condition où `parent_item_id` est `NULL`.

## Colonnes communes

| **Nom de la colonne** | **Description** |
|----|----|
| `base_price` | Prix d&#39;une unité individuelle d&#39;un produit au moment de la vente après l&#39;application des [règles de prix de catalogue, remises échelonnées et prix spéciaux](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) et avant l&#39;application des remises sur les taxes, les frais d&#39;expédition ou le panier. Elle est représentée dans la devise de base du magasin. |
| `created_at` | Date et heure de création de l’élément de commande, stockées localement en UTC. Selon votre configuration dans [!DNL Commerce Intelligence], cet horodatage peut être converti en fuseau horaire de création de rapports dans [!DNL Commerce Intelligence] différent de celui de votre base de données. |
| `item_id` (PC) | Identifiant unique de la table. |
| `name` | Nom textuel de l’élément de commande. |
| `order_id` | `Foreign key` associé à la table `sales_order`. Joignez-vous à `sales_order.entity_id` pour déterminer les attributs de commande associés à l’élément de commande. |
| `parent_item_id` | `Foreign key` qui associe un produit simple à son lot parent ou à un produit configurable. Rejoignez `sales_order_item.item_id` pour déterminer les attributs de produit parent associés au produit simple. Pour les articles de commande parent (c&#39;est-à-dire les types de produits groupés ou configurables), le `parent_item_id` est `NULL`. |
| `product_id` | `Foreign key` associé à la table `catalog_product_entity`. Joignez-vous à `catalog_product_entity.entity_id` pour déterminer les attributs de produit associés à l’article de commande. |
| `product_type` | Type de produit qui a été vendu. Les [types de produits](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) potentiels sont les suivants : simple, configurable, groupé, virtuel, groupé et téléchargeable. |
| `qty_ordered` | Quantité d&#39;unités incluses dans le panier pour l&#39;article de commande particulier au moment de la vente. |
| `sku` | Identifiant unique de l’article de commande acheté. |
| `store_id` | `Foreign key` associé à la table `store`. Rejoignez `store.store_id` pour déterminer la vue de magasin Commerce associée à l’élément de commande. |

{style="table-layout:auto"}

## Colonnes calculées courantes

| **Nom de la colonne** | **Description** |
|---|---|
| `Customer's email` | Adresse électronique du client qui passe la commande. Calculé en joignant `sales_order_item.order_id` à `sales_order.entity_id` et en renvoyant le champ `customer_email` . |
| `Customer's lifetime number of orders` | Nombre total de commandes passées par ce client. Calculé en joignant `sales_order_item.order_id` à `sales_order.entity_id` et en renvoyant le champ `Customer's lifetime number of orders` . |
| `Customer's lifetime revenue` | Somme du chiffre d&#39;affaires total pour toutes les commandes passées par ce client. Calculé en joignant `sales_order_item.order_id` à `sales_order.entity_id` et en renvoyant le champ `Customer's lifetime revenue` . |
| `Customer's order number` | Classement séquentiel de la commande de ce client. Calculé en joignant `sales_order_item.order_id` à `sales_order.entity_id` et en renvoyant le champ `Customer's order number` . |
| `Order item total value (quantity * price)` | Valeur totale d&#39;un article de commande au moment de la vente après l&#39;application des [règles de prix de catalogue, remises échelonnées et prix spéciaux](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) et avant l&#39;application des remises sur les taxes, les frais d&#39;expédition ou le panier. Calculé en multipliant le `qty_ordered` par le `base_price`. |
| `Order's coupon_code` | Bon appliqué à la commande. Calculé en joignant `sales_order_item.order_id` à `sales_order.entity_id` et en renvoyant le champ `coupon_code` . |
| `Order's increment_id` | Identifiant unique de la commande. Calculé en joignant `sales_order_item.order_id` à `sales_order.entity_id` et en renvoyant le champ `increment_id` . |
| `Order's status` | Statut de la commande. Calculé en joignant `sales_order_item.order_id` à `sales_order.entity_id` et en renvoyant le champ `status` . |
| `Store name` | Nom du magasin Commerce associé à l’élément de commande. Calculé en joignant `sales_order_item.store_id` à `store.store_id` et en renvoyant le champ `name` . |

{style="table-layout:auto"}

## Mesures courantes

| **Nom de la mesure** | **Description** | **Construction** |
|---|---|---|
| `Products ordered` | La quantité totale de produits inclus dans les paniers au moment de la vente | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | Valeur totale des produits inclus dans les paniers au moment de la vente après application des règles de prix de catalogue, des remises échelonnées et des prix spéciaux, et avant application des taxes, des frais d’expédition ou des remises sur les paniers | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key` Chemins d’accès de jonction

`catalog_product_entity`

* Rejoignez `catalog_product_entity` tableau pour créer des colonnes qui renvoient les attributs de produit associés à l’élément de commande.
   * Chemin : `sales_order_item.product_id` (plusieurs) => `catalog_product_entity.entity_id` (un)

`sales_order`

* Rejoignez `sales_order` tableau pour créer de nouvelles colonnes au niveau de la commande associées à l’élément de commande.
   * Chemin : `sales_order_item.order_id` (plusieurs) => `sales_order.entity_id` (un)

`sales_order_item`

* Rejoignez les `sales_order_item` pour créer des colonnes qui associent les détails du SKU parent configurable ou groupé au produit simple. [Contactez l’assistance ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) pour obtenir de l’aide sur la configuration de ces calculs, si vous créez dans le gestionnaire Data Warehouse.
   * Chemin : `sales_order_item.parent_item_id` (plusieurs) => `sales_order_item.item_id` (un)

`store`

* Rejoignez `store` tableau pour créer des colonnes qui renvoient des détails liés au magasin Commerce associé à l’élément de commande.
   * Chemin : `sales_order_item.store_id` (plusieurs) => `store.store_id` (un)
