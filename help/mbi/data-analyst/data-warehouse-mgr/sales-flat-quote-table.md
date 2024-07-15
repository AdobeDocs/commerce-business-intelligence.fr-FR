---
title: Tableau de citations
description: Découvrez comment utiliser la table des guillemets.
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# Tableau de citations

La table `quote` (`sales_flat_quote` sur M1) contient des enregistrements sur chaque panier créé dans votre boutique, qu’ils aient été abandonnés ou convertis en achat. Chaque ligne représente un panier. En raison de la taille potentielle de ce tableau, Adobe vous recommande de supprimer régulièrement les enregistrements si certains critères sont remplis, par exemple s’il existe des paniers non convertis de plus de 60 jours.

>[!NOTE]
>
>L’analyse de l’historique des paniers abandonnés n’est possible que si vous ne supprimez pas les enregistrements de la table `quote`. Si vous supprimez des enregistrements, vous ne pourrez voir que les paniers qui n’ont pas encore été supprimés de votre base de données.

## Colonnes natives communes

| **Nom de colonne** | **Description** |
|---|---|
| `base_currency_code` | Devise pour toutes les valeurs capturées dans les champs `base_*` (c’est-à-dire `base_grand_total`, `base_subtotal`, etc.). Cela reflète généralement la devise par défaut du magasin Commerce. |
| `base_grand_total` | Prix final cité au client pour le panier, après l’application de toutes les taxes, les frais d’expédition et les remises. Bien que le calcul précis soit personnalisable, en général, le `base_grand_total` est calculé comme suit : `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | Valeur brute de la marchandise de tous les articles inclus dans le panier. Les taxes, les frais d’expédition, les remises, etc. ne sont pas inclus |
| `created_at` | Horodatage de création du panier, stocké localement en UTC. Selon votre configuration dans [!DNL Commerce Intelligence], cet horodatage peut être converti en fuseau horaire de création de rapports dans [!DNL Commerce Intelligence] qui diffère du fuseau horaire de votre base de données. |
| `customer_email` | Adresse électronique du client qui a créé le panier |
| `customer_id` | `Foreign key` associé à la table `customer_entity`, si le client est enregistré. Rejoignez `customer_entity.entity_id` pour déterminer les attributs du client associés à l’utilisateur qui a créé le panier. Si le panier a été créé lors de l’extraction de l’invité, ce champ est `NULL` |
| `entity_id` (PK) | Identifiant unique de la table, généralement utilisé dans les jointures à d’autres tables dans l’instance Commerce. |
| `is_active` | Champ booléen qui renvoie &quot;1&quot; si le panier a été créé par un client et n’a pas encore été converti en commande. Renvoie &quot;0&quot; pour les paniers convertis ou les paniers créés via l’administrateur |
| `items_qty` | Somme de la quantité totale de tous les articles du panier |
| `reserved_order_id` | `Foreign key` associé à la table `sales_order`. Rejoignez `sales_order.increment_id` pour déterminer les détails de commande associés à un panier converti. Pour les paniers qui ne sont pas associés à une commande convertie, le `reserved_order_id` reste `NULL` |
| `store_id` | `Foreign key` associé à la table `store`. Rejoignez `store`.`store_id` pour déterminer quelle vue de magasin Commerce est associée au panier |

{style="table-layout:auto"}

## Colonnes calculées courantes

| **Nom de colonne** | **Description** |
|---|---|
| `Order date` | Horodatage reflétant la date de création des commandes pour les paniers convertis. Calculé en associant `quote.reserved_order_id` à `sales_order.increment_id` et en renvoyant le champ `sales_order.created_at` |
| `Seconds between cart creation and order` | Délai écoulé entre la création du panier et la création de la commande. Calculé en soustrayant `created_at` de `Order date`, renvoyé sous la forme d&#39;un nombre entier de secondes |
| `Seconds since cart creation` | Délai écoulé entre la date de création du panier et maintenant. Calculé en soustrayant `created_at` de l’horodatage du serveur au moment de l’exécution de la requête, renvoyé sous la forme d’un nombre entier de secondes. Le plus souvent utilisé pour identifier l’âge d’un panier |
| `Store name` | Nom de la boutique Commerce associée à cette commande. Calculé en associant `quote.store_id` à `store.store_id` et en renvoyant le champ `name` |

{style="table-layout:auto"}

## Mesures courantes

| **Nom de mesure** | **Description** | **Construction** |
|---|---|---|
| `Number of abandoned carts` | Nombre de paniers répondant à des conditions d’&quot;abandon&quot; spécifiques | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>Filtres :<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, où &quot;x&quot; correspond au temps écoulé (en secondes) depuis la création d’un panier au-delà duquel un panier est considéré comme abandonné |
| `Avg time to cart conversion` | Durée moyenne entre la création de panier et la création de commande pour les paniers convertis | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | Somme du total des recettes potentielles du panier abandonné, où les recettes sont définies comme le champ `base_grand_total` | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>Filtres :<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, où &quot;x&quot; correspond au temps écoulé (en secondes) depuis la création d’un panier au-delà duquel un panier est considéré comme abandonné |

{style="table-layout:auto"}

## Chemins de jointure de clés étrangères

`customer_entity`

* Rejoignez la table `customer_entity` pour créer de nouvelles colonnes au niveau du client associées au client qui a créé le panier.
   * Chemin : `quote.customer_id` (plusieurs) => `customer_entity.entity_id` (un)

`sales_order`

* Rejoignez la table `sales_order` pour créer des colonnes qui renvoient les détails de commande associés à un panier converti.
   * Chemin :`quote.reserved_order_id` (plusieurs) => `sales_order.increment_id` (un)

`store`

* Rejoignez la table `store` pour créer des colonnes qui renvoient les détails relatifs au magasin Commerce associé au panier.
   * Chemin : `quote.store_id` (plusieurs) => `store.store_id` (un)
