---
title: table sales_order_item
description: Découvrez comment utiliser la table sales_order_item .
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# `sales_order_item` Table

La table `sales_order_item` (`sales_flat_order_item` sur M1) contient des enregistrements de tous les produits achetés dans une commande. Chaque ligne représente un `sku` unique inclus dans une commande. La quantité d&#39;unités achetées pour un `sku` spécifique est le plus souvent représentée par le champ `qty_ordered`.

## Types de produits

Le `sales_order_item` capture les détails sur tous les [types de produits](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) achetés. Une pratique courante dans [!DNL Adobe Commerce] consiste à offrir des produits configurables, ou en d’autres termes, un produit qui peut être personnalisé en fonction de la taille, de la couleur et d’autres attributs de produit. Bien qu’un produit configurable possède son propre `sku`, il peut être associé à plusieurs produits simples, où chaque produit simple représente une configuration de produit unique. Pour plus d’informations, voir [Configuration des produits](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) .

Prenons l’exemple d’un produit configurable tel qu’un T-shirt. Lorsqu’un client procède à l’extraction, il sélectionne les options permettant de modifier la couleur et la taille. Si le client sélectionne une couleur `blue` et une taille de `small`, il finit par acheter un produit simple comme `t-shirt-blue-small` qui se rapporte au produit parent de `t-shirt`.

Lorsqu’un produit configurable est inclus dans une commande, deux lignes sont générées dans la table `sales_order_item` : une pour le [simple](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku` et une pour le parent [configurable](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html). Ces deux enregistrements de la table `sales_order_item` peuvent être associés les uns aux autres via la jointure suivante :

* (simple) `sales_order_item.parent_item_id` => (configurable) `sales_order_item.item_id`

Il est donc possible de créer des rapports sur les ventes de produits, soit au niveau simple, soit au niveau configurable. Par défaut, toutes les mesures `order-item-level` standard dans [!DNL Commerce Intelligence] sont configurées pour exclure les produits simples et le rapport *uniquement* sur les versions configurables. Pour ce faire, utilisez l’ensemble de filtres `Ordered products we count`, qui filtre sur la condition où `parent_item_id` est `NULL`.

## Colonnes communes

| **Nom de colonne** | **Description** |
|----|----|
| `base_price` | Prix d’une unité individuelle d’un produit au moment de la vente après l’application des [règles de prix catalogue, remises à niveau et prix spécial](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) et avant toute imposition, livraison ou remise au panier. Il est représenté dans la devise de base du magasin. |
| `created_at` | Horodatage de création de l’élément de commande, stocké localement en UTC. Selon votre configuration dans [!DNL Commerce Intelligence], cet horodatage peut être converti en fuseau horaire de création de rapports dans [!DNL Commerce Intelligence] qui diffère du fuseau horaire de votre base de données. |
| `item_id` (PK) | Identifiant unique de la table. |
| `name` | Nom textuel de l’élément de commande. |
| `order_id` | `Foreign key` associé à la table `sales_order`. Rejoignez `sales_order.entity_id` pour déterminer les attributs de commande associés à l’élément de commande. |
| `parent_item_id` | `Foreign key` qui associe un produit simple à son lot parent ou à un produit configurable. Rejoignez `sales_order_item.item_id` pour déterminer les attributs de produit parents associés à un produit simple. Pour les éléments de commande parents (c’est-à-dire les types de produit groupés ou configurables), l’ `parent_item_id` est `NULL`. |
| `product_id` | `Foreign key` associé à la table `catalog_product_entity`. Rejoignez `catalog_product_entity.entity_id` pour déterminer les attributs de produit associés à l’élément de commande. |
| `product_type` | Type de produit vendu. Les [types de produits](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) potentiels incluent : simple, configurable, groupé, virtuel, groupé et téléchargeable. |
| `qty_ordered` | Quantité d’unités incluses dans le panier pour l’article de commande spécifique au moment de la vente. |
| `sku` | Identifiant unique de l’article de commande qui a été acheté. |
| `store_id` | `Foreign key` associé à la table `store`. Rejoignez `store.store_id` pour déterminer la vue de magasin Commerce associée à l’élément de commande. |

{style="table-layout:auto"}

## Colonnes calculées courantes

| **Nom de colonne** | **Description** |
|---|---|
| `Customer's email` | Adresse électronique du client qui commande. Calculé en associant `sales_order_item.order_id` à `sales_order.entity_id` et en renvoyant le champ `customer_email`. |
| `Customer's lifetime number of orders` | Nombre total de commandes passées par ce client. Calculé en associant `sales_order_item.order_id` à `sales_order.entity_id` et en renvoyant le champ `Customer's lifetime number of orders`. |
| `Customer's lifetime revenue` | Somme du total des recettes de toutes les commandes passées par ce client. Calculé en associant `sales_order_item.order_id` à `sales_order.entity_id` et en renvoyant le champ `Customer's lifetime revenue`. |
| `Customer's order number` | Classement séquentiel de la commande de ce client. Calculé en associant `sales_order_item.order_id` à `sales_order.entity_id` et en renvoyant le champ `Customer's order number`. |
| `Order item total value (quantity * price)` | La valeur totale d’un article de commande au moment de la vente après [les règles de prix du catalogue, les remises à niveau et les prix spéciaux](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) sont appliquées et avant toute imposition, livraison ou remise au panier. Calculé en multipliant le `qty_ordered` par le `base_price`. |
| `Order's coupon_code` | Bon appliqué à la commande. Calculé en associant `sales_order_item.order_id` à `sales_order.entity_id` et en renvoyant le champ `coupon_code`. |
| `Order's increment_id` | Identifiant unique de la commande. Calculé en associant `sales_order_item.order_id` à `sales_order.entity_id` et en renvoyant le champ `increment_id`. |
| `Order's status` | État de la commande. Calculé en associant `sales_order_item.order_id` à `sales_order.entity_id` et en renvoyant le champ `status`. |
| `Store name` | Nom de la boutique Commerce associée à l’élément de commande. Calculé en associant `sales_order_item.store_id` à `store.store_id` et en renvoyant le champ `name`. |

{style="table-layout:auto"}

## Mesures courantes

| **Nom de mesure** | **Description** | **Construction** |
|---|---|---|
| `Products ordered` | La quantité totale de produits inclus dans les paniers au moment de la vente | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | Valeur totale des produits inclus dans les paniers au moment de la vente après l’application des règles de prix du catalogue, des remises à niveau et des prix spéciaux, et avant l’application des taxes, de l’expédition ou des remises au panier. | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key` Chemins de jointure

`catalog_product_entity`

* Rejoignez la table `catalog_product_entity` pour créer des colonnes qui renvoient les attributs de produit associés à l’élément de commande.
   * Chemin : `sales_order_item.product_id` (plusieurs) => `catalog_product_entity.entity_id` (un)

`sales_order`

* Rejoignez la table `sales_order` pour créer de nouvelles colonnes au niveau de la commande associées à l’élément de commande.
   * Chemin : `sales_order_item.order_id` (plusieurs) => `sales_order.entity_id` (un)

`sales_order_item`

* Rejoignez `sales_order_item` pour créer des colonnes qui associent les détails du SKU configurable parent ou du bundle au produit simple. [Contactez l’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) pour obtenir de l’aide sur la configuration de ces calculs, en cas de création dans le gestionnaire de Data Warehouse.
   * Chemin : `sales_order_item.parent_item_id` (plusieurs) => `sales_order_item.item_id` (un)

`store`

* Rejoignez la table `store` pour créer des colonnes qui renvoient les détails liés au magasin Commerce associé à l’élément de commande.
   * Chemin : `sales_order_item.store_id` (plusieurs) => `store.store_id` (un)
