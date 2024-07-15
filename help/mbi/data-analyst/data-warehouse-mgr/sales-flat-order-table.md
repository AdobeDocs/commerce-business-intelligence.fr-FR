---
title: table sales_order
description: Découvrez comment utiliser la table sales_order.
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 0%

---

# `sales_order` Table

La table `sales_order` (`sales_flat_order` sur M1) est l’endroit où chaque commande est capturée. En règle générale, chaque ligne représente un ordre unique, bien qu’il existe des mises en oeuvre personnalisées de Commerce qui entraînent le fractionnement d’une commande en lignes distinctes.

Ce tableau comprend toutes les commandes client, que cette commande ait été traitée lors du passage en caisse de l’invité. Si votre boutique accepte le passage en caisse des invités, vous trouverez plus d’informations sur ce [cas d’utilisation](../data-warehouse-mgr/guest-orders.md).

## Colonnes communes

| **Nom de colonne** | **Description** |
|---|---|
| `base_currency_code` | Devise pour toutes les valeurs capturées dans les champs `base_*` (c’est-à-dire `base_grand_total`, `base_subtotal`, etc.). Cela reflète généralement la devise par défaut du magasin Commerce. |
| `base_discount_amount` | Valeur de remise appliquée à la commande |
| `base_grand_total` | Prix final payé par le client sur la commande, après application de toutes les taxes, frais d’expédition et remises. Bien que le calcul précis soit personnalisable, en général, le `base_grand_total` est calculé comme suit : `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | Valeur brute de la marchandise de tous les articles inclus dans la commande. Les taxes, les frais d’expédition, les remises, etc. ne sont pas inclus |
| `base_shipping_amount` | Valeur de livraison appliquée à la commande |
| `base_tax_amount` | Valeur de taxe appliquée à la commande |
| `billing_address_id` | `Foreign key` associé à la table `sales_order_address`. Rejoignez `sales_order_address.entity_id` pour déterminer les détails des adresses de facturation associés à la commande. |
| `coupon_code` | Bon appliqué à la commande. Si aucun coupon n&#39;est appliqué, ce champ est `NULL` |
| `created_at` | Horodatage de création de la commande, stocké localement en UTC. Selon votre configuration dans [!DNL Commerce Intelligence], cet horodatage peut être converti en fuseau horaire de création de rapports dans [!DNL Commerce Intelligence] qui diffère du fuseau horaire de votre base de données. |
| `customer_email` | Adresse électronique du client qui commande. Cela est renseigné dans toutes les situations, y compris les commandes traitées lors du passage en caisse de l’invité. |
| `customer_group_id` | Clé étrangère associée à la table `customer_group`. Rejoindre `customer_group.customer_group_id` pour déterminer le groupe de clients associé à la commande |
| `customer_id` | `Foreign key` associé à la table `customer_entity`, si le client est enregistré. Rejoignez `customer_entity.entity_id` pour déterminer les attributs du client associés à la commande. Si la commande a été passée par le biais de l’extraction d’invité, ce champ est `NULL` |
| `entity_id` (PK) | Identifiant unique de la table, généralement utilisé dans les jointures à d’autres tables dans l’instance Commerce. |
| `increment_id` | Identifiant unique d’une commande, communément appelé `order_id` dans Adobe Commerce. Le `increment_id` est le plus souvent utilisé pour les jointures à des sources externes, telles que [!DNL Google Ecommerce] |
| `shipping_address_id` | Clé étrangère associée à la table `sales_order_address`. Rejoignez `sales_order_address.entity_id` pour déterminer les détails des adresses de livraison associés à la commande. |
| `status` | État de la commande. Peut renvoyer des valeurs telles que &quot;complete&quot;, &quot;processing&quot;, &quot;cancelled&quot;, &quot;refinancé&quot; et tout état personnalisé implémenté sur l’instance Commerce. Sujet aux modifications lorsque la commande est traitée |
| `store_id` | `Foreign key` associé à la table `store`. Rejoignez `store`.`store_id` pour déterminer quelle vue de magasin Commerce est associée à la commande |

{style="table-layout:auto"}

## Colonnes calculées courantes

| **Nom de colonne** | **Description** |
|---|---|
| `Billing address city` | Ville de facturation de la commande. Calculé en rejoignant `sales_order`.`billing_address_id` à `sales_order_address`.`entity_id` et renvoi du champ `city` |
| `Billing address country` | Code pays de facturation de la commande. Calculé en rejoignant `sales_order`.`billing_address_id` à `sales_order_address`.`entity_id` et renvoyer l’ `country_id` |
| `Billing address region` | Région de facturation (état ou province le plus souvent) de la commande. Calculé en rejoignant `sales_order`.`billing_address_id` à `sales_order_address`.`entity_id` et renvoi du champ `region` |
| `Customer's first order date` | Horodatage de la première commande passée par ce client. Souvent considérée comme la &quot;date d’acquisition&quot; d’un client. Calculé en renvoyant le `sales_order` minimum.valeur `created_at` pour chaque client unique |
| `Customer's first order's billing region` | Région de facturation d’acquisition pour le client qui a passé la commande. Calculé en renvoyant le `Billing address region` associé à la première commande du client |
| `Customer's first order's coupon_code` | Code du coupon d’acquisition pour le client qui a passé cette commande. Calculé en renvoyant le `coupon_code` associé à la première commande du client |
| `Customer's group code` | Nom de groupe du client qui a passé cette commande. Calculé en rejoignant `sales_order`.`customer_group_id` à `customer_group`.`customer_group_id` et renvoi du champ `customer_group_code` |
| `Customer's lifetime number of coupons` | Nombre total de coupons appliqués à toutes les commandes passées par ce client. Calculé en comptant le nombre de commandes pour lesquelles `coupon_code` n’est pas `NULL` pour chaque client unique |
| `Customer's lifetime number of orders` | Nombre total de commandes passées par ce client. Calculé en comptant le nombre de lignes dans le tableau `sales_order` pour chaque client unique |
| `Customer's lifetime revenue` | Somme du total des recettes de toutes les commandes passées par ce client. Calculé en totalisant le champ `base_grand_total` pour toutes les commandes pour chaque client unique |
| `Customer's order number` | Classement séquentiel de la commande de ce client. Calculé en identifiant toutes les commandes passées par un client, en les triant par ordre croissant selon l’horodatage `created_at` et en attribuant une valeur entière incrémentée à chaque commande. Par exemple, la première commande du client renvoie `Customer's order number` de 1, la deuxième commande du client renvoie `Customer's order number` de 2, etc. |
| `Customer's order number (previous-current)` | Classement de la commande précédente du client concaténé avec le classement de cette commande, séparé par un caractère `-`. Calculé par concaténation (&quot;`Customer's order number` - 1&quot;) avec &quot;`-`&quot; suivi de &quot;`Customer's order number`&quot;. Par exemple, pour la commande associée au deuxième achat du client, cette colonne renvoie la valeur `1-2`. Le plus souvent utilisé lors de la représentation du temps entre deux événements de commande (c’est-à-dire dans le graphique &quot;Durée entre les commandes&quot;) |
| `Is customer's last order?` | Détermine si la commande correspond à la dernière commande du client, ou la plus récente. Calculé en comparant la valeur `Customer's order number` à `Customer's lifetime number of orders`. Lorsque ces deux champs sont égaux pour l’ordre donné, cette colonne renvoie `Yes` ; sinon elle renvoie `No` |
| `Number of items in order` | Nombre total d’articles inclus dans la commande. Calculé en rejoignant `sales_order`.`entity_id` à `sales_order_item`.`order_id` et totalisant `sales_order_item`.Champ `qty_ordered` |
| `Seconds between customer's first order date and this order` | Délai écoulé entre cette commande et la première commande du client. Calculé en soustrayant `Customer's first order date` de `created_at` pour chaque commande, renvoyé sous la forme d’un nombre entier de secondes. |
| `Seconds since previous order` | Délai écoulé entre cette commande et la commande précédente du client. Calculé en soustrayant le `created_at` de l’ordre précédent de l’ `created_at` de cet ordre, renvoyé sous la forme d’un nombre entier de secondes. Par exemple, pour l’enregistrement de commande correspondant à la troisième commande d’un client, cette colonne renvoie le nombre de secondes entre la deuxième et la troisième commande du client. Pour la première commande du client, ce champ renvoie `NULL` |
| `Shipping address city` | Ville de livraison de la commande. Calculé en rejoignant `sales_order`.`shipping_address_id` à `sales_order_address`.`entity_id` et renvoi du champ `city` |
| `Shipping address country` | Code du pays d’expédition pour la commande. Calculé en rejoignant `sales_order`.`Shipping_address_id` à `sales_order_address`.`entity_id` et renvoyer l’ `country_id` |
| `Shipping address region` | Région d’expédition (le plus souvent état ou province) pour la commande. Calculé en rejoignant `sales_order`.`shipping_address_id` à `sales_order_address`.`entity_id` et renvoi du champ `region` |
| `Store name` | Nom de la boutique Commerce associée à cette commande. Calculé en rejoignant `sales_order`.`store_id` à `store`.`store_id` et renvoi du champ `name` |

## Mesures courantes

| **Nom de mesure** | **Description** | **Construction** |
|---|---|---|
| `Avg order value` | Les recettes moyennes par commande, où les recettes sont définies comme `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | Durée moyenne entre la commande (n-1) d’un client et la énième commande, pour tous les clients et commandes. | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | Somme de la valeur brute de la marchandise pour toutes les commandes, où GMV est défini comme le sous-total, avant l’application de toutes les taxes et remises | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | Durée médiane entre la commande (n-1) d’un client et la énième commande, pour tous les clients et commandes. | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | Le nombre total de commandes passées | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | La somme des recettes pour toutes les commandes, où les recettes sont définies comme le prix final payé par le client, après l’application de toutes les taxes, remises, frais d’expédition, etc. | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | Somme du montant des frais de livraison pour toutes les commandes | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | La somme des taxes appliquées à toutes les commandes | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | Nombre de clients uniques qui passent une commande dans l’intervalle de temps de création de rapports donné. Si, par exemple, l’intervalle du rapport est hebdomadaire, chaque client qui commande au moins une fois par semaine est comptabilisé une seule fois, indépendamment du nombre de commandes passées cette semaine. | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` Chemins de jointure

`customer_entity`

* Rejoignez la table `customer_entity` pour créer de nouvelles colonnes au niveau du client associées au client qui a passé la commande.
   * Chemin : `sales_order.customer_id` (plusieurs) => `customer_entity.entity_id` (un)

`customer_group`

* Rejoignez la table `customer_group` pour créer des colonnes qui renvoient le nom du groupe de clients du client qui a passé la commande.
   * Chemin : `sales_order.customer_group_id` (plusieurs) => `customer_group.customer_group_id` (un)

`sales_order_address`

* Rejoignez la table `sales_order_address` pour créer des colonnes qui renvoient les emplacements de facturation et d’expédition associés à la commande. Deux chemins de jointure sont possibles, selon que les détails de facturation ou de livraison sont requis.
   * Chemins :
      * Expédition : `sales_order.shipping_address_id`(plusieurs) => `sales_order_address.entity_id` (un)
      * Facturation : `sales_order.billing_address_id`(plusieurs) => `sales_order_address.entity_id` (un)

`store`

* Rejoignez la table `store` pour créer des colonnes qui renvoient les détails liés au magasin Commerce associé à la commande.
   * Chemin : `sales_order.store_id` (plusieurs) => `store.store_id` (un)
