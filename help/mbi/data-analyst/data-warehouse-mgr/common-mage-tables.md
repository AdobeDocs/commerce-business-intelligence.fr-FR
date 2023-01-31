---
title: Tableaux de commerce courants
description: Découvrez certaines des tables les plus courantes qui [!DNL MBI] les clients utilisent .
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# Tableaux de commerce courants

Lors de la première connexion d’une instance Commerce à [[!DNL MBI]](../importing-data/integrations/magento.md), [!DNL MBI] réplique automatiquement les données de certaines de vos tables commerciales (généralement 4 à 6 tables) afin de configurer l’ensemble initial de tableaux de bord et de rapports. Bien que cela constitue un excellent point de départ, la plupart des instances de magasin génèrent des dizaines, voire des centaines de tables supplémentaires, ce qui peut fournir des informations essentielles sur les performances de votre entreprise.

Vous trouverez ci-dessous une liste des tables les plus courantes qui [!DNL MBI] les clients utilisent . Après vous [Connecter votre instance Commerce à MBI](../../data-analyst/importing-data/integrations/magento.md), vous pouvez utiliser la variable [Gestionnaire de Data Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) pour effectuer le suivi des champs de données pertinents.

| Nom de la table | Description |
|---|---|
| `catalog_category_entity` | Chaque ligne du `catalog_category_entity` décrit une catégorie spécifique. Avec l’objet `catalog_category_entity_varchar` et le `catalog_category_product` table de mappage, vous pouvez obtenir des informations sur les catégories pour chaque produit. |
| `catalog_category_product` | Chaque ligne du `catalog_category_product` Le tableau répertorie une combinaison d’un produit et d’une catégorie. Par conséquent, un produit donné peut exister sur ce tableau plusieurs fois avec différentes catégories, et une catégorie donnée peut exister sur ce tableau plusieurs fois associée à différents produits. Cette table indexe la variable `catalog_category_entity` (qui contient les détails au niveau de la catégorie) et la variable `catalog_product_entity` table (contenant les détails au niveau du produit). |
| `catalog_product_entity` | Chaque ligne du `catalog_product_entity` représente un produit spécifique. Cela inclut le moment où ce produit a été créé dans votre compte Commerce et son SKU. |
| `customer_entity` | Chaque ligne du [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) représente un utilisateur enregistré sur votre site web. Des informations de base au niveau du client, telles que sa date d’enregistrement et son adresse électronique, sont disponibles sur cette table. |
| `quote` | Chaque ligne du [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) représente un panier créé lors du processus de passage en caisse, que ce panier ait été converti ou non en commande. En raison de la taille potentielle de ce tableau, nous vous recommandons de supprimer régulièrement les enregistrements si certains critères sont respectés, par exemple s’il existe des paniers non convertis de plus de 60 jours. |
| `quote_item` | Chaque ligne du [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) représente un élément ajouté à un panier, que le panier ait été converti ou non en commande. En raison de la taille potentielle de ce tableau, nous vous recommandons de supprimer régulièrement les enregistrements si certains critères sont respectés, par exemple s’il existe des paniers non convertis de plus de 60 jours. |
| `sales_order` | Chaque ligne du [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) représente une commande passée sur votre site. Ce tableau contient des informations au niveau de la commande, telles que la date de la commande, le client qui a passé la commande, le total de la commande et l’utilisation du code de réduction et de coupon. |
| `sales_order_address` | Chaque ligne du `sales_order_address` Le tableau contient des informations d’expédition et de facturation pour une commande spécifique. Sur le `sales_order` , la variable `billing_address_id` et le `shipping_address_id` pour un ordre donné, fait référence à une ligne spécifique (identifiée par `entity_id`) sur le `sales_order_address` table. |
| `sales_order_item` | Chaque ligne du [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) identifie un élément spécifique dans un ordre spécifique. Chaque ligne contient des détails tels que le produit, la quantité achetée et la commande à laquelle l’article donné est associé. |

{style=&quot;table-layout:auto&quot;}

## Documentation connexe

[[!DNL Magento] Diagrammes de relation d’entité](../data-warehouse-mgr/entity-rel-diag.md)
