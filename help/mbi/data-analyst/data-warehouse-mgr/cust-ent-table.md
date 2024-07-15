---
title: table customer_entity
description: Découvrez comment accéder aux enregistrements de tous les comptes enregistrés.
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# table customer_entity

La table `customer_entity` contient les enregistrements de tous les comptes enregistrés. Un compte est considéré comme enregistré s’il s’inscrit à un compte, qu’il effectue un achat ou non. Chaque ligne correspond à un compte enregistré unique, identifié par `entity_id` de ce compte.

Cette table ne contient pas d&#39;enregistrement des clients qui passent une commande via le passage en caisse des invités. Si votre boutique accepte le passage en caisse des invités, reportez-vous à la section [Comment tenir compte des commandes d’invités](../data-warehouse-mgr/guest-orders.md) pour ces commandes.

## Colonnes communes

| **Nom de colonne** | **Description** |
|---|---|
| `created_at` | Horodatage correspondant à la date d’enregistrement du compte, stocké localement en UTC. Selon votre configuration dans [!DNL Commerce Intelligence], cet horodatage peut être converti en fuseau horaire de création de rapports dans [!DNL Commerce Intelligence] qui diffère du fuseau horaire de votre base de données. |
| `email` | Adresse électronique associée au compte |
| `entity_id` (PK) | Identifiant unique de la table, généralement utilisé dans les jointures à l’ `customer_id` dans d’autres tables de l’instance. |
| `group_id` | Clé étrangère associée à la table `customer_group`. Rejoindre `customer_group.customer_group_id` pour déterminer le groupe de clients associé au compte enregistré |
| `store_id` | Clé étrangère associée à la table `store`. Rejoignez `store`.`store_id` pour déterminer quelle vue de magasin Commerce est associée au compte enregistré |

{style="table-layout:auto"}

## Colonnes calculées courantes

| **Nom de colonne** | **Description** |
|---|---|
| `Customer's first 30 day revenue` | Somme du total des recettes de toutes les commandes passées par ce client dans les 30 jours suivant la date de première commande du client. Calculé en associant `customer_entity.entity_id` à `sales_order.customer_id` et en totalisant le champ `base_grand_total` pour toutes les commandes où `sales_order.Seconds between customer's first order date and this order` ≤ 2592000, qui est le nombre de secondes en 30 jours |
| `Customer's first order date` | Horodatage de la première commande passée par ce client. Calculé en associant `customer_entity.entity_id` à `sales_order.customer_id` et en renvoyant le `sales_order` minimum.`created_at` value |
| `Customer's first order's billing region` | Région de facturation associée à la première commande du client. Calculé en associant `customer_entity.entity_id` à `sales_order.customer_id` et en renvoyant le `Billing address region` où `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | Code coupon associé à la première commande du client. Calculé en associant `customer_entity.entity_id` à `sales_order.customer_id` et en renvoyant le `sales_order.coupon_code` où `sales_order.Customer's order number` = 1 |
| `Customer's group code` | Nom de groupe du client enregistré. Calculé en associant `customer_entity.group_id` à `customer_group`.`customer_group_id` et renvoi du champ `customer_group_code` |
| `Customer's lifetime number of coupons` | Nombre total de coupons appliqués à toutes les commandes passées par ce client. Calculé en associant `customer_entity.entity_id` à `sales_order.customer_id` et en comptant le nombre de commandes pour lesquelles le `sales_order.coupon_code` n&#39;est pas `NULL` |
| `Customer's lifetime number of orders` | Nombre total de commandes passées par ce client. Calculé en associant `customer_entity.entity_id` à `sales_order.customer_id` et en comptant le nombre de lignes dans la table `sales_order` |
| `Customer's lifetime revenue` | Somme du total des recettes de toutes les commandes passées par ce client. Calculé en associant `customer_entity.entity_id` à `sales_order.customer_id` et en totalisant le champ `base_grand_total` pour toutes les commandes passées par ce client |
| `Seconds since customer's first order date` | Délai écoulé entre la date de première commande du client et maintenant. Calculé en soustrayant `Customer's first order date` de l’horodatage du serveur au moment de l’exécution de la requête, renvoyé sous la forme d’un nombre entier de secondes. |
| `Store name` | Nom de la boutique Commerce associée à ce compte enregistré. Calculé en associant `customer_entity.store_id` à `store.store_id` et en renvoyant le champ `name` |

{style="table-layout:auto"}

## Mesures courantes

| **Nom de mesure** | **Description** | **Construction** |
|---|---|---|
| `Avg first 30 day revenue` | Chiffre d’affaires moyen des commandes passées dans les 30 jours suivant la première commande du client | Opération : Moyenne<br/>Opérateur : `Customer's first 30 day revenue`<br/>Horodatage : `created_at`<br/>Filtres :<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000 (exclut les clients qui n’ont pas encore atteint 30 jours depuis leur première commande) |
| `Avg lifetime coupons` | Nombre moyen de coupons appliqués aux commandes par client au cours de sa durée de vie | Opération : Moyenne<br/>Opérateur : `Customer's lifetime number of coupons`<br/>Horodatage : `created_at` |
| `Avg lifetime orders` | Le nombre moyen de commandes passées par client au cours de sa durée de vie | Opération : Moyenne<br/>Opérateur : `Customer's lifetime number of orders`<br/>Horodatage : `created_at` |
| `Avg lifetime revenue` | Chiffre d’affaires total moyen par client pour toutes les commandes passées sur leur durée de vie | Opération : Moyenne<br/>Opérateur : `Customer's lifetime revenue`<br/>Horodatage : `created_at` |
| `New customers` | Nombre de clients avec au moins une commande, comptabilisé à la date de leur première commande. Exclut les comptes qui s’enregistrent mais ne passent jamais de commande | Opération : Count<br/>Operand : `entity_id`<br/>Horodatage : `Customer's first order date` |
| `Registered accounts` | Nombre de comptes enregistrés. Inclut tous les comptes enregistrés, qu’un compte ait passé une commande ou non | Opération : Count<br/>Operand : `entity_id`<br/>Horodatage : `created_at` |

{style="table-layout:auto"}

## Chemins de jointure de clés étrangères

`customer_group`

* Rejoignez la table `customer_group` pour créer des colonnes qui renvoient le nom du groupe de clients du compte enregistré.
   * Chemin : `customer_entity.group_id` (plusieurs) => `customer_group.customer_group_id` (un)

`store`

* Rejoignez la table `store` pour créer des colonnes qui renvoient les détails relatifs au magasin associé au compte enregistré.
   * Chemin : `customer_entity.store_id` (plusieurs) => `store.store_id` (un)
