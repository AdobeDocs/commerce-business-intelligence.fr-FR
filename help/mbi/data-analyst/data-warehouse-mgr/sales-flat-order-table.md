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

La table `sales_order` (`sales_flat_order` sur M1) est l’endroit où chaque ordre est capturé. En règle générale, chaque ligne représente un ordre unique, bien qu’il existe certaines implémentations personnalisées de Commerce qui entraînent le fractionnement d’un ordre en lignes distinctes.

Ce tableau inclut toutes les commandes client, que ces commandes aient été traitées ou non par le biais de la commande client. Si votre boutique accepte le passage en caisse des invités, vous trouverez plus d’informations sur ce [cas d’utilisation](../data-warehouse-mgr/guest-orders.md).

## Colonnes communes

| **Nom de la colonne** | **Description** |
|---|---|
| `base_currency_code` | Devise pour toutes les valeurs capturées dans `base_*` champs (à savoir `base_grand_total`, `base_subtotal`, etc.). Cela reflète généralement la devise par défaut du magasin Commerce |
| `base_discount_amount` | Valeur de remise appliquée à la commande |
| `base_grand_total` | Prix final payé par le client sur la commande, après application de toutes les taxes, frais d&#39;expédition et remises. Bien que le calcul précis soit personnalisable, en général le `base_grand_total` est calculé comme `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | Valeur brute de tous les articles inclus dans la commande. Les taxes, les frais d’expédition, les remises, etc. ne sont pas inclus |
| `base_shipping_amount` | Valeur d&#39;expédition appliquée à la commande |
| `base_tax_amount` | Valeur de taxe appliquée à la commande |
| `billing_address_id` | `Foreign key` associé à la table `sales_order_address`. Rejoignez `sales_order_address.entity_id` pour déterminer les détails de l’adresse de facturation associés à la commande |
| `coupon_code` | Bon appliqué à la commande. Si aucun coupon n’est appliqué, ce champ est `NULL` |
| `created_at` | Date et heure de création de la commande, stockée localement en UTC. Selon votre configuration dans [!DNL Commerce Intelligence], cet horodatage peut être converti en fuseau horaire de création de rapports dans [!DNL Commerce Intelligence] différent de celui de votre base de données |
| `customer_email` | Adresse électronique du client qui passe la commande. Elle est renseignée dans toutes les situations, y compris les commandes traitées par passage en caisse des invités |
| `customer_group_id` | Clé étrangère associée à la table `customer_group`. Rejoignez-`customer_group.customer_group_id` pour déterminer le groupe de clients associé à la commande |
| `customer_id` | `Foreign key` associé à la table `customer_entity`, si le client est enregistré. Rejoignez `customer_entity.entity_id` pour déterminer les attributs du client associés à la commande. Si la commande a été passée par passage en caisse des invités, ce champ est `NULL` |
| `entity_id` (PC) | Identifiant unique de la table. Généralement utilisé dans les jointures avec d&#39;autres tables de l&#39;instance Commerce |
| `increment_id` | Identifiant unique d’une commande, communément appelé `order_id` dans Adobe Commerce. Le `increment_id` est le plus souvent utilisé pour les jointures à des sources externes, telles que les [!DNL Google Ecommerce] |
| `shipping_address_id` | Clé étrangère associée à la table `sales_order_address`. Rejoignez `sales_order_address.entity_id` pour déterminer les détails de l’adresse d’expédition associés à la commande |
| `status` | Statut de la commande. Peut renvoyer des valeurs telles que « terminé », « traitement », « annulé », « remboursé », ainsi que tout statut personnalisé implémenté sur l’instance Commerce. Sujet à des modifications au fur et à mesure du traitement de la commande |
| `store_id` | `Foreign key` associé à la table `store`. Rejoignez `store`.`store_id` de déterminer quelle vue de magasin Commerce est associée à la commande |

{style="table-layout:auto"}

## Colonnes calculées courantes

| **Nom de la colonne** | **Description** |
|---|---|
| `Billing address city` | Ville de facturation de la commande. Calculé par `sales_order` de jointure.`billing_address_id` à `sales_order_address`.`entity_id` et renvoi du champ `city` |
| `Billing address country` | Code pays de facturation de la commande. Calculé par `sales_order` de jointure.`billing_address_id` à `sales_order_address`.`entity_id` et retour de la `country_id` |
| `Billing address region` | Région de facturation (le plus souvent État ou province) de la commande. Calculé par `sales_order` de jointure.`billing_address_id` à `sales_order_address`.`entity_id` et renvoi du champ `region` |
| `Customer's first order date` | Date et heure de la première commande passée par ce client. Souvent considérée comme la « date d’acquisition » d’un client. Calculé en renvoyant la `sales_order` minimale.`created_at` valeur pour chaque client unique |
| `Customer's first order's billing region` | Région de facturation d&#39;acquisition pour le client qui a passé la commande. Calculé en retournant la `Billing address region` associée à la première commande du client |
| `Customer's first order's coupon_code` | Code bon d&#39;achat pour le client qui a passé cette commande. Calculé en retournant la `coupon_code` associée à la première commande du client |
| `Customer's group code` | Nom du groupe du client qui a passé cette commande. Calculé par `sales_order` de jointure.`customer_group_id` à `customer_group`.`customer_group_id` et renvoi du champ `customer_group_code` |
| `Customer's lifetime number of coupons` | Quantité totale de coupons appliquée à toutes les commandes passées par ce client. Calculé en comptant le nombre de commandes pour lesquelles le `coupon_code` n&#39;est pas `NULL` pour chaque client unique |
| `Customer's lifetime number of orders` | Nombre total de commandes passées par ce client. Calculé en comptant le nombre de lignes du tableau de `sales_order` pour chaque client unique |
| `Customer's lifetime revenue` | Somme du chiffre d&#39;affaires total pour toutes les commandes passées par ce client. Calculé en additionnant le champ `base_grand_total` pour toutes les commandes de chaque client unique |
| `Customer's order number` | Classement séquentiel de la commande de ce client. Calculé en identifiant toutes les commandes passées par un client, en les triant par ordre croissant selon l’horodatage `created_at` et en attribuant une valeur entière incrémentée à chaque commande. Par exemple, la première commande du client renvoie une `Customer's order number` de 1, la deuxième commande du client renvoie une `Customer's order number` de 2, etc. |
| `Customer's order number (previous-current)` | Classement de la commande précédente du client concaténé avec le classement de cette commande, séparé par un caractère `-`. Calculé par concaténation (« `Customer's order number` - 1 ») avec « `-` » suivi de « `Customer's order number` ». Par exemple, pour la commande associée au deuxième achat du client, cette colonne renvoie une valeur de `1-2`. Utilisé le plus souvent lors de la représentation du temps entre deux événements de commande (c’est-à-dire, dans le graphique « Temps entre les commandes ») |
| `Is customer's last order?` | Détermine si la commande correspond à la dernière commande ou à la plus récente du client. Calculé en comparant la valeur `Customer's order number` avec `Customer's lifetime number of orders`. Lorsque ces deux champs sont égaux pour l’ordre donné, cette colonne renvoie `Yes` ; sinon elle renvoie `No` |
| `Number of items in order` | Quantité totale d&#39;articles inclus dans la commande. Calculé par `sales_order` de jointure.`entity_id` à `sales_order_item`.`order_id` et résumer les `sales_order_item`.champ `qty_ordered` |
| `Seconds between customer's first order date and this order` | Temps écoulé entre cette commande et la première commande du client. Calculé en soustrayant `Customer's first order date` de la `created_at` pour chaque commande, renvoyé sous la forme d’un nombre entier de secondes |
| `Seconds since previous order` | Temps écoulé entre cette commande et la commande immédiatement précédente du client. Calculé en soustrayant la `created_at` de la commande précédente de la `created_at` de cette commande, renvoyé sous la forme d’un nombre entier de secondes. Par exemple, pour l’enregistrement de commande correspondant à la troisième commande d’un client, cette colonne renvoie le nombre de secondes entre la deuxième commande du client et la troisième commande. Pour la première commande du client, ce champ renvoie `NULL` |
| `Shipping address city` | Ville d’expédition de la commande. Calculé par `sales_order` de jointure.`shipping_address_id` à `sales_order_address`.`entity_id` et renvoi du champ `city` |
| `Shipping address country` | Code du pays d’expédition de la commande. Calculé par `sales_order` de jointure.`Shipping_address_id` à `sales_order_address`.`entity_id` et retour de la `country_id` |
| `Shipping address region` | Région d’expédition (le plus souvent État ou province) de la commande. Calculé par `sales_order` de jointure.`shipping_address_id` à `sales_order_address`.`entity_id` et renvoi du champ `region` |
| `Store name` | Nom du magasin Commerce associé à cette commande. Calculé par `sales_order` de jointure.`store_id` à `store`.`store_id` et renvoi du champ `name` |

## Mesures courantes

| **Nom de la mesure** | **Description** | **Construction** |
|---|---|---|
| `Avg order value` | Chiffre d’affaires moyen par commande, où le chiffre d’affaires est défini comme le `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | Temps moyen entre la commande d&#39;un client (n-1) et la énième commande, pour tous les clients et commandes | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | Somme de la valeur brute de la marchandise pour toutes les commandes, où le MVM est défini comme le sous-total, avant que toutes les taxes et remises ne soient appliquées | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | Temps médian entre la commande d&#39;un client (n-1) et la énième commande, pour tous les clients et commandes | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | Nombre total de commandes passées | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | Somme du produit pour toutes les commandes, où le produit est défini comme le prix final payé par le client, après application de toutes les taxes, remises, frais d’expédition, etc | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | Somme des frais de livraison pour toutes les commandes | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | Somme des taxes appliquées à toutes les commandes | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | Nombre de clients et de clientes uniques qui passent une commande dans l’intervalle de temps de création de rapports donné. Par exemple, si l&#39;intervalle du rapport était hebdomadaire, chaque client qui passe au moins une commande au cours d&#39;une semaine donnée est comptabilisé exactement une fois, quel que soit le nombre de commandes passées au cours de cette semaine | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` Chemins d’accès de jonction

`customer_entity`

* Rejoignez `customer_entity` tableau pour créer de nouvelles colonnes au niveau du client associées au client qui a passé la commande.
   * Chemin : `sales_order.customer_id` (plusieurs) => `customer_entity.entity_id` (un)

`customer_group`

* Rejoignez `customer_group` tableau pour créer des colonnes qui renvoient le nom du groupe de clients du client qui a passé la commande.
   * Chemin : `sales_order.customer_group_id` (plusieurs) => `customer_group.customer_group_id` (un)

`sales_order_address`

* Rejoignez `sales_order_address` tableau pour créer des colonnes qui renvoient les emplacements de facturation et d’expédition associés à la commande. Deux chemins de jonction sont possibles, selon que les informations de facturation ou d’expédition sont requises.
   * Chemins d’accès :
      * Expédition : `sales_order.shipping_address_id`(plusieurs) => `sales_order_address.entity_id` (un)
      * Facturation : `sales_order.billing_address_id`(plusieurs) => `sales_order_address.entity_id` (un)

`store`

* Rejoignez `store` tableau pour créer des colonnes qui renvoient des détails liés au magasin Commerce associé à la commande.
   * Chemin : `sales_order.store_id` (plusieurs) => `store.store_id` (un)
