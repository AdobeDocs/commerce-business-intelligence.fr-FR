---
title: Citation en table
description: Découvrez comment utiliser la table des devis.
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/Q-46fusr2IS4ZQDrR8IjHEttueSBpT2-LQBtsejMEC4
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 613
ht-degree: 0%

---

# Citation en table

La table `quote` (`sales_flat_quote` sur M1) contient des enregistrements sur chaque panier créé dans votre magasin, qu’il ait été abandonné ou converti en achat. Chaque ligne représente un panier. En raison de la taille potentielle de cette table, Adobe vous recommande de supprimer régulièrement des enregistrements si certains critères sont remplis, par exemple s’il existe des paniers non convertis de plus de 60 jours.

>[!NOTE]
>
>L’analyse des paniers abandonnés et historiques n’est possible que si vous ne supprimez pas d’enregistrements de la table `quote`. Si vous supprimez des enregistrements, vous ne pourrez voir que les paniers qui n’ont pas encore été supprimés de votre base de données.

## Colonnes natives courantes

| **Nom de la colonne** | **Description** |
|---|---|
| `base_currency_code` | Devise pour toutes les valeurs capturées dans `base_*` champs (à savoir `base_grand_total`, `base_subtotal`, etc.). Cela reflète généralement la devise par défaut du magasin Commerce |
| `base_grand_total` | Prix final proposé au client pour le panier, après application de toutes les taxes, frais d’expédition et remises. Bien que le calcul précis soit personnalisable, en général le `base_grand_total` est calculé comme `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | Valeur brute de tous les articles inclus dans le panier. Les taxes, les frais d’expédition, les remises, etc. ne sont pas inclus |
| `created_at` | Date et heure de création du panier, stockées localement en UTC. Selon votre configuration dans [!DNL Commerce Intelligence], cet horodatage peut être converti en fuseau horaire de création de rapports dans [!DNL Commerce Intelligence] différent de celui de votre base de données |
| `customer_email` | Adresse électronique du client qui a créé le panier |
| `customer_id` | `Foreign key` associé à la table `customer_entity`, si le client est enregistré. Rejoignez `customer_entity.entity_id` pour déterminer les attributs du client associés à l’utilisateur qui a créé le panier. Si le panier a été créé lors du passage en caisse des invités, ce champ est `NULL` |
| `entity_id` (PC) | Identifiant unique de la table. Généralement utilisé dans les jointures avec d&#39;autres tables de l&#39;instance Commerce |
| `is_active` | Champ booléen qui renvoie « 1 » si le panier a été créé par un client et n’a pas encore été converti en commande. Renvoie « 0 » pour les paniers convertis ou les paniers créés via l’administration |
| `items_qty` | Somme de la quantité totale de tous les articles inclus dans le panier |
| `reserved_order_id` | `Foreign key` associé à la table `sales_order`. Rejoignez `sales_order.increment_id` pour déterminer les détails de commande associés à un panier converti. Pour les paniers qui ne sont pas associés à une commande convertie, la `reserved_order_id` reste `NULL` |
| `store_id` | `Foreign key` associé à la table `store`. Rejoindre à `store`.`store_id` pour déterminer quelle vue de magasin Commerce est associée au panier |

{style="table-layout:auto"}

## Colonnes calculées courantes

| **Nom de la colonne** | **Description** |
|---|---|
| `Order date` | Date et heure reflétant la date de création de la commande pour les paniers convertis. Calculé en joignant `quote.reserved_order_id` à `sales_order.increment_id` et en renvoyant le champ `sales_order.created_at` |
| `Seconds between cart creation and order` | Temps écoulé entre la création du panier et la création de la commande. Calculé en soustrayant `created_at` de `Order date`, renvoyé sous la forme d’un nombre entier de secondes |
| `Seconds since cart creation` | Temps écoulé entre la date de création du panier et maintenant. Calculé en soustrayant `created_at` de l’horodatage du serveur au moment de l’exécution de la requête, renvoyé sous la forme d’un nombre entier de secondes. Le plus souvent utilisé pour identifier l’âge d’un panier |
| `Store name` | Nom du magasin Commerce associé à cette commande. Calculé en joignant `quote.store_id` à `store.store_id` et en renvoyant le champ `name` |

{style="table-layout:auto"}

## Mesures courantes

| **Nom de la mesure** | **Description** | **Construction** |
|---|---|---|
| `Number of abandoned carts` | Nombre de paniers répondant à des conditions d’« abandon » spécifiques | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>Filtres :<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, où « x » correspond au temps écoulé (en secondes) depuis la création du panier au-delà duquel un panier est considéré comme abandonné |
| `Avg time to cart conversion` | Temps moyen entre la création du panier et la création de la commande pour les paniers convertis | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | Somme des revenus potentiels totaux du panier abandonné, où le revenu est défini comme le champ `base_grand_total` | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>Filtres :<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, où « x » correspond au temps écoulé (en secondes) depuis la création du panier au-delà duquel un panier est considéré comme abandonné |

{style="table-layout:auto"}

## Chemins d’accès de jointure des clés étrangères

`customer_entity`

* Rejoignez `customer_entity` tableau pour créer des colonnes au niveau du client associées au client qui a créé le panier.
   * Chemin : `quote.customer_id` (plusieurs) => `customer_entity.entity_id` (un)

`sales_order`

* Rejoignez `sales_order` tableau pour créer des colonnes qui renvoient les détails des commandes associés à un panier converti.
   * Chemin : `quote.reserved_order_id` (plusieurs) => `sales_order.increment_id` (un)

`store`

* Rejoignez `store` tableau pour créer des colonnes qui renvoient des détails liés à la boutique Commerce associée au panier.
   * Chemin : `quote.store_id` (plusieurs) => `store.store_id` (un)
