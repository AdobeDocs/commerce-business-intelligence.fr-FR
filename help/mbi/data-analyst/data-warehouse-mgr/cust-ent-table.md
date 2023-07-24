---
title: table customer_entity
description: Découvrez comment accéder aux enregistrements de tous les comptes enregistrés.
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# table customer_entity

Le `customer_entity` contient les enregistrements de tous les comptes enregistrés. Un compte est considéré comme enregistré s’il s’inscrit à un compte, qu’il effectue un achat ou non. Chaque ligne correspond à un compte enregistré unique, identifié par le compte en question. `entity_id`.

Cette table ne contient pas d&#39;enregistrement des clients qui passent une commande via le passage en caisse des invités. Si votre boutique accepte le passage en caisse des invités, reportez-vous à la section [Comment tenir compte des commandes d’invités](../data-warehouse-mgr/guest-orders.md) pour ces commandes.

## Colonnes communes

| **Nom de la colonne** | **Description** |
|---|---|
| `created_at` | Horodatage correspondant à la date d’enregistrement du compte, stocké localement en UTC. Selon votre configuration dans [!DNL Commerce Intelligence], cet horodatage peut être converti en fuseau horaire de création de rapports dans [!DNL Commerce Intelligence] qui diffère du fuseau horaire de votre base de données |
| `email` | Adresse électronique associée au compte |
| `entity_id` (PK) | Identifiant unique de la table, généralement utilisé dans les jointures au `customer_id` dans d’autres tables de l’instance. |
| `group_id` | Clé étrangère associée à la variable `customer_group` table. Rejoindre à `customer_group.customer_group_id` pour déterminer le groupe de clients associé au compte enregistré |
| `store_id` | Clé étrangère associée à la variable `store` table. Rejoindre à `store`.`store_id` pour déterminer quelle vue de magasin Commerce est associée au compte enregistré |

{style="table-layout:auto"}

## Colonnes calculées courantes

| **Nom de la colonne** | **Description** |
|---|---|
| `Customer's first 30 day revenue` | Somme du total des recettes de toutes les commandes passées par ce client dans les 30 jours suivant la date de première commande du client. Calculé par la jointure `customer_entity.entity_id` to `sales_order.customer_id` et additionner les `base_grand_total` champ pour toutes les commandes où `sales_order.Seconds between customer's first order date and this order` ≤ 2592000, qui est le nombre de secondes en 30 jours |
| `Customer's first order date` | Horodatage de la première commande passée par ce client. Calculé par la jointure `customer_entity.entity_id` to `sales_order.customer_id` et renvoyer le minimum `sales_order`.`created_at` value |
| `Customer's first order's billing region` | Région de facturation associée à la première commande du client. Calculé par la jointure `customer_entity.entity_id` to `sales_order.customer_id` et le renvoi de la variable `Billing address region` where `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | Code coupon associé à la première commande du client. Calculé par la jointure `customer_entity.entity_id` to `sales_order.customer_id` et le renvoi de la variable `sales_order.coupon_code` where `sales_order.Customer's order number` = 1 |
| `Customer's group code` | Nom de groupe du client enregistré. Calculé par la jointure `customer_entity.group_id` to `customer_group`.`customer_group_id` et le renvoi de la variable `customer_group_code` field |
| `Customer's lifetime number of coupons` | Nombre total de coupons appliqués à toutes les commandes passées par ce client. Calculé par la jointure `customer_entity.entity_id` to `sales_order.customer_id` et compter le nombre de commandes où la variable `sales_order.coupon_code` n’est pas `NULL` |
| `Customer's lifetime number of orders` | Nombre total de commandes passées par ce client. Calculé par la jointure `customer_entity.entity_id` to `sales_order.customer_id` et le comptage du nombre de lignes dans la variable `sales_order` table |
| `Customer's lifetime revenue` | Somme du total des recettes de toutes les commandes passées par ce client. Calculé par la jointure `customer_entity.entity_id` to `sales_order.customer_id` et additionner les `base_grand_total` champ pour toutes les commandes passées par ce client |
| `Seconds since customer's first order date` | Délai écoulé entre la date de première commande du client et maintenant. Calculé par soustraction `Customer's first order date` de l’horodatage du serveur au moment de l’exécution de la requête, renvoyé sous la forme d’un nombre entier de secondes. |
| `Store name` | Nom de la boutique Commerce associée à ce compte enregistré. Calculé par la jointure `customer_entity.store_id` to `store.store_id` et le renvoi de la variable `name` field |

{style="table-layout:auto"}

## Mesures courantes

| **Nom de la mesure** | **Description** | **Construction** |
|---|---|---|
| `Avg first 30 day revenue` | Chiffre d’affaires moyen des commandes passées dans les 30 jours suivant la première commande du client | Opération : Moyenne<br/>Operand : `Customer's first 30 day revenue`<br/>Horodatage : `created_at`<br/>Filtres :<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000 (exclut les clients qui n’ont pas encore atteint 30 jours depuis leur première commande) |
| `Avg lifetime coupons` | Nombre moyen de coupons appliqués aux commandes par client au cours de sa durée de vie | Opération : Moyenne<br/>Operand : `Customer's lifetime number of coupons`<br/>Horodatage : `created_at` |
| `Avg lifetime orders` | Le nombre moyen de commandes passées par client au cours de sa durée de vie | Opération : Moyenne<br/>Operand : `Customer's lifetime number of orders`<br/>Horodatage : `created_at` |
| `Avg lifetime revenue` | Chiffre d’affaires total moyen par client pour toutes les commandes passées sur leur durée de vie | Opération : Moyenne<br/>Operand : `Customer's lifetime revenue`<br/>Horodatage : `created_at` |
| `New customers` | Nombre de clients avec au moins une commande, comptabilisé à la date de leur première commande. Exclut les comptes qui s’enregistrent mais ne passent jamais de commande | Opération : Count<br/>Operand : `entity_id`<br/>Horodatage : `Customer's first order date` |
| `Registered accounts` | Nombre de comptes enregistrés. Inclut tous les comptes enregistrés, qu’un compte ait passé une commande ou non | Opération : Count<br/>Operand : `entity_id`<br/>Horodatage : `created_at` |

{style="table-layout:auto"}

## Chemins de jointure de clés étrangères

`customer_group`

* Rejoindre à `customer_group` tableau pour créer des colonnes qui renvoient le nom du groupe de clients du compte enregistré.
   * Chemin : `customer_entity.group_id` (nombreux) => `customer_group.customer_group_id` (1)

`store`

* Rejoindre à `store` pour créer des colonnes qui renvoient des détails relatifs au magasin associé au compte enregistré.
   * Chemin : `customer_entity.store_id` (nombreux) => `store.store_id` (1)
