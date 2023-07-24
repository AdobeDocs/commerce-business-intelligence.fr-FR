---
title: table sales_order_item
description: Découvrez comment utiliser la table sales_order_item .
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---

# `sales_order_item` Tableau

Le `sales_order_item` tableau (`sales_flat_order_item` sur M1) contient des enregistrements de tous les produits achetés dans une commande. Chaque ligne représente une `sku` inclus dans une commande. La quantité d’unités achetées pour un `sku` est le plus souvent représenté par la variable `qty_ordered` champ .

## Types de produits

Le `sales_order_item` capture les détails sur tous les [types de produits](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) qui ont été achetés. Une pratique courante [!DNL Adobe Commerce] est d’offrir des produits configurables, ou en d’autres termes, un produit qui peut être personnalisé en fonction de la taille, de la couleur et d’autres attributs de produit. Bien qu’un produit configurable possède sa propre `sku`, il peut s’agir de plusieurs produits simples, où chaque produit simple représente une configuration de produit unique. Voir [configuration des produits](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) pour plus d’informations.

Prenons l’exemple d’un produit configurable tel qu’un T-shirt. Lorsqu’un client procède à l’extraction, il sélectionne les options permettant de modifier la couleur et la taille. Si le client sélectionne une couleur de `blue`et une taille de `small`, ils finissent par acheter un produit simple comme `t-shirt-blue-small` qui se rapporte au produit parent de `t-shirt`.

Lorsqu’un produit configurable est inclus dans une commande, deux lignes sont générées dans la variable `sales_order_item` table : un pour le [simple](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku` et un pour le [configurable](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) parent. Ces deux enregistrements dans la variable `sales_order_item` peut être associée l’une à l’autre via la jointure suivante :

* (simple) `sales_order_item.parent_item_id` => (configurable) `sales_order_item.item_id`

Il est donc possible de créer des rapports sur les ventes de produits, soit au niveau simple, soit au niveau configurable. Par défaut, toutes les valeurs standard `order-item-level` mesures dans [!DNL Commerce Intelligence] sont configurés pour exclure les produits simples ; et *only* rapport sur les versions configurables. Pour ce faire, vous devez : `Ordered products we count` filtre , qui filtre sur la condition où `parent_item_id` is `NULL`.

## Colonnes communes

| **Nom de la colonne** | **Description** |
|----|----|
| `base_price` | Prix d’une unité individuelle d’un produit au moment de la vente après vente [catalogue des règles de prix, remises échelonnées et prix spécial](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) sont appliquées et avant toute application des taxes, des frais d’expédition ou des remises sur le panier. Il est représenté dans la devise de base du magasin. |
| `created_at` | Horodatage de création de l’élément de commande, stocké localement en UTC. Selon votre configuration dans [!DNL Commerce Intelligence], cet horodatage peut être converti en fuseau horaire de création de rapports dans [!DNL Commerce Intelligence] qui diffère du fuseau horaire de votre base de données. |
| `item_id` (PK) | Identifiant unique du tableau. |
| `name` | Nom textuel de l’élément de commande. |
| `order_id` | `Foreign key` associé à la propriété `sales_order` table. Rejoindre à `sales_order.entity_id` pour déterminer les attributs de commande associés à l’élément de commande. |
| `parent_item_id` | `Foreign key` qui associe un produit simple à son lot parent ou à un produit configurable. Rejoindre à `sales_order_item.item_id` pour déterminer les attributs de produit parents associés à un produit simple. Pour les éléments de commande parents (c’est-à-dire les types de produit regroupés ou configurables), la variable `parent_item_id` is `NULL`. |
| `product_id` | `Foreign key` associé à la propriété `catalog_product_entity` table. Rejoindre à `catalog_product_entity.entity_id` pour déterminer les attributs de produit associés à l’article de commande. |
| `product_type` | Type de produit vendu. Potentiel [types de produits](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) inclure : simple, configurable, groupé, virtuel, groupé et téléchargeable. |
| `qty_ordered` | Nombre d’unités incluses dans le panier pour l’article de commande spécifique au moment de la vente. |
| `sku` | Identifiant unique de l’article de commande qui a été acheté. |
| `store_id` | `Foreign key` associé à la propriété `store` table. Rejoindre à `store.store_id` pour déterminer la vue de magasin Commerce associée à l’élément de commande. |

{style="table-layout:auto"}

## Colonnes calculées courantes

| **Nom de la colonne** | **Description** |
|---|---|
| `Customer's email` | Adresse électronique du client qui passe la commande. Calculé par la jointure `sales_order_item.order_id` to `sales_order.entity_id` et le renvoi de la variable `customer_email` champ . |
| `Customer's lifetime number of orders` | Nombre total de commandes passées par ce client. Calculé par la jointure `sales_order_item.order_id` to `sales_order.entity_id` et le renvoi de la variable `Customer's lifetime number of orders` champ . |
| `Customer's lifetime revenue` | Somme du total des recettes de toutes les commandes passées par ce client. Calculé par la jointure `sales_order_item.order_id` to `sales_order.entity_id` et le renvoi de la variable `Customer's lifetime revenue` champ . |
| `Customer's order number` | Classement séquentiel de la commande de ce client. Calculé par la jointure `sales_order_item.order_id` to `sales_order.entity_id` et le renvoi de la variable `Customer's order number` champ . |
| `Order item total value (quantity * price)` | Valeur totale d’un article de commande au moment de la vente après [catalogue des règles de prix, remises échelonnées et prix spécial](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) sont appliquées et avant toute application des taxes, des frais d’expédition ou des remises sur le panier. Calculé en multipliant la variable `qty_ordered` par le `base_price`. |
| `Order's coupon_code` | Bon appliqué à la commande. Calculé par la jointure `sales_order_item.order_id` to `sales_order.entity_id` et le renvoi de la variable `coupon_code` champ . |
| `Order's increment_id` | Identifiant unique de la commande. Calculé par la jointure `sales_order_item.order_id` to `sales_order.entity_id` et le renvoi de la variable `increment_id` champ . |
| `Order's status` | État de la commande. Calculé par la jointure `sales_order_item.order_id` to `sales_order.entity_id` et le renvoi de la variable `status` champ . |
| `Store name` | Nom de la boutique Commerce associée à l’élément de commande. Calculé par la jointure `sales_order_item.store_id` to `store.store_id` et le renvoi de la variable `name` champ . |

{style="table-layout:auto"}

## Mesures courantes

| **Nom de la mesure** | **Description** | **Construction** |
|---|---|---|
| `Products ordered` | La quantité totale de produits inclus dans les paniers au moment de la vente | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | Valeur totale des produits inclus dans les paniers au moment de la vente après l’application des règles de prix du catalogue, des remises à niveau et des prix spéciaux, et avant l’application des taxes, de l’expédition ou des remises au panier. | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key` Association des chemins

`catalog_product_entity`

* Rejoindre à `catalog_product_entity` tableau pour créer des colonnes qui renvoient les attributs de produit associés à l’élément de commande.
   * Chemin : `sales_order_item.product_id` (nombreux) => `catalog_product_entity.entity_id` (1)

`sales_order`

* Rejoindre à `sales_order` pour créer de nouvelles colonnes au niveau de la commande associées à l’élément de commande.
   * Chemin : `sales_order_item.order_id` (nombreux) => `sales_order.entity_id` (1)

`sales_order_item`

* Rejoindre à `sales_order_item` pour créer des colonnes qui associent les détails du SKU configurable parent ou du bundle au produit simple. [Contacter le support technique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) pour plus d’informations sur la configuration de ces calculs, si vous créez dans Data Warehouse manager.
   * Chemin : `sales_order_item.parent_item_id` (nombreux) => `sales_order_item.item_id` (1)

`store`

* Rejoindre à `store` pour créer des colonnes qui renvoient des détails relatifs à la boutique Commerce associée à l’élément de commande.
   * Chemin : `sales_order_item.store_id` (nombreux) => `store.store_id` (1)
