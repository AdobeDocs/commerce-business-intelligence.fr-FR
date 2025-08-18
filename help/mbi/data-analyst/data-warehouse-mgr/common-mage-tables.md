---
title: Tableaux Commerce courants
description: Découvrez quelques-uns des tableaux les plus courants que  [!DNL Commerce Intelligence]  clients et clientes utilisent.
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# Tableaux Commerce courants

Lorsque vous connectez une instance [!DNL Adobe Commerce] à [[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md) pour la première fois, [!DNL Commerce Intelligence] réplique automatiquement les données de certaines de vos tables de commerce (généralement 4 à 6 tables) pour configurer l’ensemble initial de tableaux de bord et de rapports. Bien qu’il s’agisse d’un excellent point de départ, la plupart des instances de boutique génèrent des dizaines, voire des centaines, de tables supplémentaires qui peuvent fournir des insight essentielles aux performances de votre entreprise.

Vous trouverez ci-dessous une liste de certains des tableaux les plus courants que [!DNL Commerce Intelligence] clients utilisent. Après avoir [connecté votre instance Commerce à Commerce Intelligence](../../data-analyst/importing-data/integrations/magento.md), vous pouvez utiliser le [gestionnaire Data Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) pour effectuer le suivi des champs de données pertinents.

| Nom de la table | Description |
|---|---|
| `catalog_category_entity` | Chaque ligne du tableau `catalog_category_entity` décrit une catégorie spécifique. Grâce à la table de `catalog_category_entity_varchar` associée et à la table de mappage `catalog_category_product`, vous pouvez obtenir des informations sur la catégorie de chaque produit. |
| `catalog_category_product` | Chaque ligne du tableau `catalog_category_product` répertorie une combinaison d’un produit et d’une catégorie. Par conséquent, un produit donné peut exister plusieurs fois dans ce tableau avec différentes catégories, et une catégorie donnée peut exister plusieurs fois dans ce tableau avec différents produits. Cette table indexe la table `catalog_category_entity` (qui contient des détails au niveau de la catégorie) et la table `catalog_product_entity` (qui contient des détails au niveau du produit). |
| `catalog_product_entity` | Chaque ligne du tableau `catalog_product_entity` représente un produit spécifique. Cela inclut la date de création de ce produit dans votre compte Commerce et son SKU. |
| `customer_entity` | Chaque ligne du tableau [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) représente un utilisateur enregistré sur votre site web. Des informations de base au niveau du client, telles que sa date d’enregistrement et son adresse e-mail, sont disponibles sur cette table. |
| `quote` | Chaque ligne du tableau [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) représente un panier qui a été créé lors du processus de passage en caisse, que ce panier ait été converti ou non en commande. En raison de la taille potentielle de cette table, Adobe vous recommande de supprimer régulièrement des enregistrements si certains critères sont remplis, par exemple s’il existe des paniers non convertis de plus de 60 jours. |
| `quote_item` | Chaque ligne du tableau [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) représente un article ajouté à un panier, que le panier ait été converti en commande ou non. En raison de la taille potentielle de cette table, Adobe vous recommande de supprimer régulièrement des enregistrements si certains critères sont remplis, par exemple s’il existe des paniers non convertis de plus de 60 jours. |
| `sales_order` | Chaque ligne du tableau [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) représente une commande passée sur votre site. Cette table contient des informations au niveau de la commande, telles que la date de la commande, le client qui a passé la commande, le total de la commande, ainsi que l&#39;utilisation du code de remise et de coupon. |
| `sales_order_address` | Chaque ligne de la table `sales_order_address` contient des informations d&#39;expédition et de facturation pour une commande spécifique. Dans le tableau `sales_order`, les `billing_address_id` et les `shipping_address_id` d’un ordre donné font référence à une ligne spécifique (identifiée par `entity_id`) du tableau `sales_order_address`. |
| `sales_order_item` | Chaque ligne du tableau [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) identifie un article spécifique à partir d&#39;une commande spécifique. Chaque ligne contient des détails tels que le produit, la quantité achetée et la commande à laquelle l’article donné est associé. |

{style="table-layout:auto"}

## Documentation connexe

[Diagrammes de relation d’entité](../data-warehouse-mgr/entity-rel-diag.md)
