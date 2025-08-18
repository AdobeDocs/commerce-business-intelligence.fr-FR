---
title: table quote_item
description: Découvrez comment utiliser la table quote_item.
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# table quote_item

La table `quote_item` (`sales_flat_quote_item` sur M1) contient des enregistrements sur chaque article ajouté à un panier, que le panier ait été abandonné ou converti en achat. Chaque ligne représente un article du panier. En raison de la taille potentielle de cette table, Adobe vous recommande de supprimer régulièrement des enregistrements si certains critères sont remplis, par exemple s’il existe des paniers non convertis de plus de 60 jours.

>[!NOTE]
>
>L’analyse des paniers abandonnés et historiques n’est possible que si vous ne supprimez pas d’enregistrements des tables `quote` et `quote_item`. Si vous supprimez des enregistrements, vous ne pourrez voir que les paniers qui n’ont pas encore été supprimés de votre base de données.

## Colonnes natives courantes

| **Nom de la colonne** | **Description** |
|---|---|
| `base_price` | Prix d&#39;une unité individuelle d&#39;un produit au moment de l&#39;ajout de l&#39;article à un panier, après application des [règles de prix de catalogue, remises échelonnées et prix spéciaux](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=fr) et avant application des remises sur les taxes, les frais d&#39;expédition ou le panier. Elle est représentée dans la devise de base du magasin. |
| `created_at` | Date et heure de création de l’article du panier, stocké localement en UTC. Selon votre configuration dans [!DNL Commerce Intelligence], cet horodatage peut être converti en fuseau horaire de création de rapports dans [!DNL Commerce Intelligence] différent de celui de votre base de données |
| `item_id` (PC) | Identifiant unique de la table |
| `name` | Nom textuel de l’élément de commande |
| `parent_item_id` | `Foreign key` qui associe un produit simple à son lot parent ou à un produit configurable. Rejoignez `quote_item.item_id` pour déterminer les attributs de produit parent associés au produit simple. Pour les articles du panier parent (c’est-à-dire les types de produits groupés ou configurables), la `parent_item_id` est `NULL` |
| `product_id` | `Foreign key` associé à la table `catalog_product_entity`. Rejoindre à `catalog_product_entity.entity_id` pour déterminer les attributs de produit associés à l&#39;article de commande |
| `product_type` | Type de produit qui a été ajouté au panier. Les [types de produits](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html?lang=fr#product-types) potentiels sont les suivants : simple, configurable, groupé, virtuel, groupé et téléchargeable |
| `qty` | Quantité d’unités incluses dans le panier pour l’article de panier particulier |
| `quote_id` | `Foreign key` associé à la table `quote`. Rejoindre à `quote.entity_id` pour déterminer les attributs de panier associés à l’article de panier |
| `sku` | Identifiant unique de l’article du panier |
| `store_id` | Clé étrangère associée à la table `store`. Rejoignez `store.store_id` pour déterminer quelle vue de magasin Commerce est associée à l’article du panier. |

{style="table-layout:auto"}

## Colonnes calculées courantes

| **Nom de la colonne** | **Description** |
|---|---|
| `Cart creation date` | Horodatage associé à la date de création du panier. Calculé en joignant `quote_item.quote_id` à `quote.entity_id` et en renvoyant la date et l’heure `created_at` |
| `Cart is active? (1/0)` | Champ booléen qui renvoie « 1 » si le panier a été créé par un client et n’a pas encore été converti en commande. Renvoie « 0 » pour les paniers convertis ou les paniers créés par l’intermédiaire de l’administrateur. Calculé en joignant `quote_item.quote_id` à `quote.entity_id` et en renvoyant le champ `is_active` |
| `Cart item total value (qty * base_price)` | Valeur totale d&#39;un article au moment où il a été ajouté à un panier, après l&#39;application des [règles de prix de catalogue, remises échelonnées et prix spéciaux](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=fr) et avant l&#39;application des remises sur les taxes, les frais d&#39;expédition ou le panier. Calculé en multipliant le `qty` par le `base_price` |
| `Seconds since cart creation` | Temps écoulé entre la date de création du panier et maintenant. Calculé en joignant `quote_item.quote_id` à `quote.entity_id` et en renvoyant le champ `Seconds since cart creation` |
| `Store name` | Nom du magasin Commerce associé à l’élément de commande. Calculé en joignant `sales_order_item.store_id` à `store.store_id` et en renvoyant le champ `name` |

{style="table-layout:auto"}

## Mesures courantes

| **Nom de la mesure** | **Description** | **Construction** |
|---|---|---|
| `Number of abandoned cart items` | Quantité totale d’articles ajoutés aux paniers qui répondent à des conditions spécifiques d’« abandon » | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>Filtres :<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, où « x » correspond au temps écoulé (en secondes) depuis la création du panier au-delà duquel un panier est considéré comme abandonné |
| `Abandoned cart item value` | Somme des revenus totaux associés aux paniers répondant à des conditions spécifiques d’« abandon » | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>Filtres :<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, où « x » correspond au temps écoulé (en secondes) depuis la création du panier au-delà duquel un panier est considéré comme abandonné |

{style="table-layout:auto"}

## Chemins d’accès de jointure des clés étrangères

`catalog_product_entity`

* Rejoignez `catalog_product_entity` tableau pour créer des colonnes qui renvoient les attributs de produit associés à l’article du panier.
   * Chemin : `quote_item.product_id` (plusieurs) => `catalog_product_entity.entity_id` (un)

`quote`

* Rejoignez `quote` tableau pour créer des colonnes au niveau du panier associées à l’article du panier.
   * Chemin : `quote_item.quote_id` (plusieurs) => `quote.entity_id` (un)

`quote_item`

* Rejoignez les `quote_item` pour créer des colonnes qui associent les détails du SKU parent configurable ou groupé au produit simple. [Contactez l’assistance ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) pour obtenir de l’aide sur la configuration de ces calculs, si vous créez dans le gestionnaire Data Warehouse.
   * Chemin : `quote_item.parent_item_id` (plusieurs) => `quote_item.item_id` (un)

`store`

* Rejoignez `store` tableau pour créer des colonnes qui renvoient des détails liés à la boutique Commerce associée à l’article du panier.
   * Chemin : `quote_item.store_id` (plusieurs) => `store.store_id` (un)
