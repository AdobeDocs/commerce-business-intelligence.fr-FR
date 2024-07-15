---
title: Tableaux Commerce courants
description: Découvrez certaines des tables les plus courantes que les clients utilisent  [!DNL Commerce Intelligence] .
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# Tableaux Commerce courants

Lorsque vous connectez une instance [!DNL Adobe Commerce] pour la première fois à [[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md), [!DNL Commerce Intelligence] réplique automatiquement les données de certaines de vos tables commerciales (généralement 4 à 6 tables) pour configurer l’ensemble initial de tableaux de bord et de rapports. Bien que cela constitue un excellent point de départ, la plupart des instances de magasin génèrent des dizaines, voire des centaines de tables supplémentaires, ce qui peut fournir des informations essentielles sur les performances de votre entreprise.

Vous trouverez ci-dessous une liste de certaines des tables les plus courantes utilisées par les clients [!DNL Commerce Intelligence]. Après avoir [connecté votre instance Commerce à Commerce Intelligence](../../data-analyst/importing-data/integrations/magento.md), vous pouvez utiliser le [Gestionnaire de Data Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) pour effectuer le suivi des champs de données appropriés.

| Nom de la table | Description |
|---|---|
| `catalog_category_entity` | Chaque ligne du tableau `catalog_category_entity` décrit une catégorie spécifique. Avec la table `catalog_category_entity_varchar` associée et la table de mappage `catalog_category_product`, vous pouvez obtenir des informations de catégorie pour chaque produit. |
| `catalog_category_product` | Chaque ligne du tableau `catalog_category_product` répertorie une combinaison d’un produit et d’une catégorie. Par conséquent, un produit donné peut exister sur ce tableau plusieurs fois avec différentes catégories, et une catégorie donnée peut exister sur ce tableau plusieurs fois associée à différents produits. Cette table indexe la table `catalog_category_entity` (qui contient les détails au niveau de la catégorie) et la table `catalog_product_entity` (qui contient les détails au niveau du produit). |
| `catalog_product_entity` | Chaque ligne de la table `catalog_product_entity` représente un produit spécifique. Cela inclut le moment où ce produit a été créé dans votre compte Commerce et son SKU. |
| `customer_entity` | Chaque ligne de la table [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) représente un utilisateur enregistré sur votre site web. Des informations de base au niveau du client, telles que sa date d’enregistrement et son adresse électronique, sont disponibles sur cette table. |
| `quote` | Chaque ligne de la table [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) représente un panier créé lors du processus de passage en caisse, que ce panier ait finalement été converti en commande. En raison de la taille potentielle de ce tableau, Adobe vous recommande de supprimer régulièrement les enregistrements si certains critères sont remplis, par exemple s’il existe des paniers non convertis de plus de 60 jours. |
| `quote_item` | Chaque ligne de la table [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) représente un élément ajouté à un panier, que le panier ait finalement été converti en commande. En raison de la taille potentielle de ce tableau, Adobe vous recommande de supprimer régulièrement les enregistrements si certains critères sont remplis, par exemple s’il existe des paniers non convertis de plus de 60 jours. |
| `sales_order` | Chaque ligne de la table [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) représente une commande placée sur votre site. Ce tableau contient des informations au niveau de la commande, telles que la date de la commande, le client qui a passé la commande, le total de la commande et l’utilisation du code de réduction et de coupon. |
| `sales_order_address` | Chaque ligne de la table `sales_order_address` contient des informations d’expédition et de facturation pour une commande spécifique. Sur la table `sales_order`, les `billing_address_id` et `shipping_address_id` pour un ordre donné font référence à une ligne spécifique (identifiée par `entity_id`) sur la table `sales_order_address`. |
| `sales_order_item` | Chaque ligne du tableau [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) identifie un élément spécifique dans un ordre spécifique. Chaque ligne contient des détails tels que le produit, la quantité achetée et la commande à laquelle l’article donné est associé. |

{style="table-layout:auto"}

## Documentation connexe

[Diagrammes de relation d’entité](../data-warehouse-mgr/entity-rel-diag.md)
