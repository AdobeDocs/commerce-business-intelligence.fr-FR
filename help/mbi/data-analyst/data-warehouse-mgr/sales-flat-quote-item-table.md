---
title: table du guillemet_élément
description: Découvrez comment utiliser la table quote_élément .
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 0%

---

# Guillemet_élément Table

Le `quote_item` tableau (`sales_flat_quote_item` sur M1) 1) contient des enregistrements sur chaque article ajouté à un panier, que le panier ait été abandonné ou converti en achat. Chaque ligne représente un article de panier. En raison de la taille potentielle de ce tableau, nous vous recommandons de supprimer régulièrement les enregistrements si certains critères sont respectés, par exemple s’il existe des paniers non convertis de plus de 60 jours.

>[!NOTE]
>
>L’analyse de l’historique des paniers abandonnés n’est possible que si vous ne supprimez pas les enregistrements du `quote` et `quote_item` table. Si vous supprimez des enregistrements, vous ne pourrez voir que les paniers qui n’ont pas encore été supprimés de votre base de données.

## Colonnes natives communes

| **Nom de la colonne** | **Description** |
|---|---|
| `base_price` | Prix d’une unité individuelle d’un produit au moment de l’ajout de l’article dans un panier, après [catalogue des règles de prix, remises échelonnées et prix spécial](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) sont appliquées et avant toute application de taxes, de frais d’expédition ou de remises sur le panier, représentées dans la devise de base du magasin ; |
| `created_at` | Horodatage de création de l’article de panier, généralement stocké localement en UTC. Selon votre configuration dans [!DNL MBI], cet horodatage peut être converti en fuseau horaire de création de rapports dans [!DNL MBI] qui diffère du fuseau horaire de votre base de données |
| `item_id` (PK) | Identifiant unique du tableau |
| `name` | Nom de texte de l’élément de commande. |
| `parent_item_id` | `Foreign key` qui associe un produit simple à son lot parent ou à un produit configurable. Rejoindre à `quote_item.item_id` pour déterminer les attributs de produit parents associés à un produit simple. Pour les éléments de panier parents (c’est-à-dire les types de produits regroupés ou configurables), la variable `parent_item_id` sera `NULL` |
| `product_id` | `Foreign key` associé à la propriété `catalog_product_entity` table. Rejoindre à `catalog_product_entity.entity_id` pour déterminer les attributs de produit associés à l’article de commande |
| `product_type` | Type de produit ajouté au panier. Potentiel [types de produits](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) inclure : simple, configurable, groupé, virtuel, groupé et téléchargeable |
| `qty` | Nombre d’unités incluses dans le panier pour l’article particulier du panier |
| `quote_id` | `Foreign key` associé à la propriété `quote` table. Rejoindre à `quote.entity_id` pour déterminer les attributs de panier associés à l’élément de panier |
| `sku` | Identifiant unique de l’élément de panier |
| `store_id` | Clé étrangère associée à la variable `store` table. Rejoindre à `store.store_id` pour déterminer quelle vue de magasin Commerce est associée à l’élément de panier |

{style=&quot;table-layout:auto&quot;}

## Colonnes calculées courantes

| **Nom de la colonne** | **Description** |
|---|---|
| `Cart creation date` | Horodatage associé à la date de création du panier. Calculé par la jointure `quote_item.quote_id` to `quote.entity_id` et le renvoi de la variable `created_at` timestamp |
| `Cart is active? (1/0)` | Champ booléen qui renvoie &quot;1&quot; si le panier a été créé par un client et n’a pas encore été converti en commande. Renvoie &quot;0&quot; pour les paniers convertis ou les paniers créés via l’administrateur. Calculé par la jointure `quote_item.quote_id` to `quote.entity_id` et le renvoi de la variable `is_active` field |
| `Cart item total value (qty * base_price)` | Valeur totale d’un élément au moment où il a été ajouté à un panier, après [catalogue des règles de prix, remises échelonnées et prix spécial](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) sont appliquées et avant toute application des taxes, des frais d’expédition ou des remises sur le panier. Calculé en multipliant la variable `qty` par le `base_price` |
| `Seconds since cart creation` | Délai écoulé entre la date de création du panier et maintenant. Calculé par la jointure `quote_item.quote_id` to `quote.entity_id` et le renvoi de la variable `Seconds since cart creation` field |
| `Store name` | Nom de la boutique Commerce associée à l’élément de commande. Calculé par la jointure `sales_order_item.store_id` to `store.store_id` et le renvoi de la variable `name` field |

{style=&quot;table-layout:auto&quot;}

## Mesures courantes

| **Nom de la mesure** | **Description** | **Construction** |
|---|---|---|
| `Number of abandoned cart items` | Nombre total d’articles ajoutés aux paniers qui répondent à des conditions d’&quot;abandon&quot; spécifiques | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>Filtres :<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, où &quot;x&quot; correspond au temps écoulé (en secondes) depuis la création du panier au-delà duquel un panier est considéré comme abandonné |
| `Abandoned cart item value` | Somme du total des recettes associées aux paniers répondant à des conditions d’&quot;abandon&quot; spécifiques | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>Filtres :<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, où &quot;x&quot; correspond au temps écoulé (en secondes) depuis la création du panier au-delà duquel un panier est considéré comme abandonné |

{style=&quot;table-layout:auto&quot;}

## Chemins de jointure de clés étrangères

`catalog_product_entity`

* Rejoindre à `catalog_product_entity` tableau pour créer de nouvelles colonnes qui renvoient les attributs de produit associés à l’élément de panier.
   * Chemin : `quote_item.product_id` (nombreux) => `catalog_product_entity.entity_id` (1)

`quote`

* Rejoindre à `quote` pour créer des colonnes au niveau du panier associées à l’élément du panier.
   * Chemin : `quote_item.quote_id` (nombreux) => `quote.entity_id` (1)

`quote_item`

* Rejoindre à `quote_item` pour créer de nouvelles colonnes qui associent les détails du SKU configurable parent ou du bundle au produit simple. Notez que vous devrez [support technique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) pour plus d’informations sur la configuration de ces calculs, si vous créez dans Data Warehouse manager.
   * Chemin : `quote_item.parent_item_id` (nombreux) => `quote_item.item_id` (1)

`store`

* Rejoindre à `store` pour créer de nouvelles colonnes qui renvoient des détails relatifs à la boutique Commerce associée à l’élément de panier.
   * Chemin : `quote_item.store_id` (nombreux) => `store.store_id` (1)
