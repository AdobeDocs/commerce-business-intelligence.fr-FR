---
title: table du guillemet_élément
description: Découvrez comment utiliser la table quote_élément .
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Guillemet_élément Table

La table `quote_item` (`sales_flat_quote_item` sur M1) contient des enregistrements sur chaque article ajouté à un panier, que le panier ait été abandonné ou converti en achat. Chaque ligne représente un article de panier. En raison de la taille potentielle de ce tableau, Adobe vous recommande de supprimer régulièrement les enregistrements si certains critères sont remplis, par exemple s’il existe des paniers non convertis de plus de 60 jours.

>[!NOTE]
>
>L&#39;analyse de l&#39;historique des paniers abandonnés n&#39;est possible que si vous ne supprimez pas les enregistrements de la table `quote` et `quote_item`. Si vous supprimez des enregistrements, vous ne pourrez voir que les paniers qui n’ont pas encore été supprimés de votre base de données.

## Colonnes natives communes

| **Nom de colonne** | **Description** |
|---|---|
| `base_price` | Le prix d’une unité individuelle d’un produit au moment de l’ajout de l’article dans un panier, après l’application des [règles de prix catalogue, remises à niveau et prix spécial](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) et avant l’application des taxes, frais de livraison ou remises sur le panier. Il est représenté dans la devise de base du magasin. |
| `created_at` | Horodatage de création de l’article de panier, stocké localement en UTC. Selon votre configuration dans [!DNL Commerce Intelligence], cet horodatage peut être converti en fuseau horaire de création de rapports dans [!DNL Commerce Intelligence] qui diffère du fuseau horaire de votre base de données. |
| `item_id` (PK) | Identifiant unique du tableau |
| `name` | Nom de texte de l’élément de commande. |
| `parent_item_id` | `Foreign key` qui associe un produit simple à son lot parent ou à un produit configurable. Rejoignez `quote_item.item_id` pour déterminer les attributs de produit parents associés à un produit simple. Pour les éléments de panier parent (c’est-à-dire, les types de produits regroupés ou configurables), le `parent_item_id` est `NULL` |
| `product_id` | `Foreign key` associé à la table `catalog_product_entity`. Rejoignez `catalog_product_entity.entity_id` pour déterminer les attributs de produit associés à l’élément de commande |
| `product_type` | Type de produit ajouté au panier. Les [ types de produits potentiels](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) incluent : simple, configurable, groupé, virtuel, groupé et téléchargeable. |
| `qty` | Nombre d’unités incluses dans le panier pour l’article particulier du panier |
| `quote_id` | `Foreign key` associé à la table `quote`. Rejoindre `quote.entity_id` pour déterminer les attributs de panier associés à l’élément de panier |
| `sku` | Identifiant unique de l’élément de panier |
| `store_id` | Clé étrangère associée à la table `store`. Rejoindre `store.store_id` pour déterminer quelle vue de magasin Commerce est associée à l’élément de panier |

{style="table-layout:auto"}

## Colonnes calculées courantes

| **Nom de colonne** | **Description** |
|---|---|
| `Cart creation date` | Horodatage associé à la date de création du panier. Calculé en associant `quote_item.quote_id` à `quote.entity_id` et en renvoyant l’horodatage `created_at` |
| `Cart is active? (1/0)` | Champ booléen qui renvoie &quot;1&quot; si le panier a été créé par un client et n’a pas encore été converti en commande. Renvoie &quot;0&quot; pour les paniers convertis ou les paniers créés via l’administrateur. Calculé en associant `quote_item.quote_id` à `quote.entity_id` et en renvoyant le champ `is_active` |
| `Cart item total value (qty * base_price)` | Valeur totale d’un article au moment de son ajout dans un panier, après l’application des [règles de prix du catalogue, des remises à niveau et des prix spéciaux](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) et avant l’application des taxes, des frais d’expédition ou des remises sur le panier. Calculé en multipliant le `qty` par le `base_price` |
| `Seconds since cart creation` | Délai écoulé entre la date de création du panier et maintenant. Calculé en associant `quote_item.quote_id` à `quote.entity_id` et en renvoyant le champ `Seconds since cart creation` |
| `Store name` | Nom de la boutique Commerce associée à l’élément de commande. Calculé en associant `sales_order_item.store_id` à `store.store_id` et en renvoyant le champ `name` |

{style="table-layout:auto"}

## Mesures courantes

| **Nom de mesure** | **Description** | **Construction** |
|---|---|---|
| `Number of abandoned cart items` | Nombre total d’articles ajoutés aux paniers qui répondent à des conditions d’&quot;abandon&quot; spécifiques | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>Filtres :<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, où &quot;x&quot; correspond au temps écoulé (en secondes) depuis la création du panier au-delà duquel un panier est considéré comme abandonné |
| `Abandoned cart item value` | Somme du total des recettes associées aux paniers répondant à des conditions d’&quot;abandon&quot; spécifiques | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>Filtres :<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, où &quot;x&quot; correspond au temps écoulé (en secondes) depuis la création du panier au-delà duquel un panier est considéré comme abandonné |

{style="table-layout:auto"}

## Chemins de jointure de clés étrangères

`catalog_product_entity`

* Rejoignez la table `catalog_product_entity` pour créer des colonnes qui renvoient les attributs de produit associés à l’élément de panier.
   * Chemin : `quote_item.product_id` (plusieurs) => `catalog_product_entity.entity_id` (un)

`quote`

* Rejoignez la table `quote` pour créer de nouvelles colonnes au niveau du panier associées à l’élément du panier.
   * Chemin : `quote_item.quote_id` (plusieurs) => `quote.entity_id` (un)

`quote_item`

* Rejoignez `quote_item` pour créer des colonnes qui associent les détails du SKU configurable parent ou du bundle au produit simple. [Contactez l’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) pour obtenir de l’aide sur la configuration de ces calculs, en cas de création dans le gestionnaire de Data Warehouse.
   * Chemin : `quote_item.parent_item_id` (plusieurs) => `quote_item.item_id` (un)

`store`

* Rejoignez la table `store` pour créer des colonnes qui renvoient les détails liés au magasin Commerce associé à l’élément de panier.
   * Chemin : `quote_item.store_id` (plusieurs) => `store.store_id` (un)
