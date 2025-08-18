---
title: Table Enterprise_Rma_Item_Entity
description: Découvrez comment analyser les informations relatives à un article spécifique à partir d'un retour demandé.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# table enterprise_rma_item_entity

Chaque ligne du tableau `enterprise_rma_item_entity` (souvent appelée `magento_rma_item_entity` dans Commerce 2.x, mais son nom peut être personnalisé) contient des informations sur un élément spécifique d’un retour demandé.

>[!NOTE]
>
>Ce tableau n’est fourni de série avec votre compte Commerce que si vous êtes un client `Enterprise Edition` ou `Enterprise Cloud Edition`.

## Colonnes natives courantes

| **Nom de la colonne** | **Description** |
|---|---|
| `entity\_id` | Identifiant unique de la table. Chaque `entity\_id` représente un élément dont le retour a été demandé. |
| `rma\_entity\_id` | Clé étrangère associée à la table `enterprise\_rma`. |
| `status` | Statut du retour de l&#39;article. Les valeurs incluent &#39;received&#39;, &#39;pending&#39;, &#39;authorized&#39;, entre autres. Les valeurs de ce statut peuvent ne pas correspondre à la valeur du statut du retour global. |
| `qty\_requested` | Quantité demandée par le client pour le retour. |
| `qty\_approved` | Quantité approuvée pour le retour. |
| `qty\_returned` | Quantité renvoyée. |
| `order\_item\_id` | Clé étrangère associée à la table `sales\_flat\_order\_item`. |
| `product\_sku` | SKU renvoyé. |

{style="table-layout:auto"}

## Colonnes calculées courantes

| **Nom de la colonne** | **Description** |
|---|---|
| `Return date\_requested` | Il s&#39;agit de la date à laquelle le client a demandé le retour. |
| `Item price` | Prix de l’article. |
| `Return item's total value (qty\_returned * price)` | Il s&#39;agit de la valeur monétaire totale des articles retournés. Permet de calculer le montant total des retours dans la table des `enterprise\_rma`. |

{style="table-layout:auto"}

## Mesures courantes

| **Nom de la mesure** | **Description** | **Construction** |
|---|---|---|
| `Number of items returned` | Nombre d’éléments renvoyés. | Colonne d&#39;opération : quantité renvoyée<br>Opération : Somme<br>Horodatage Colonne : Date de retour demandée |
| `Returned items' total value` | Montant monétaire renvoyé. | Colonne Opération : Valeur totale de l&#39;article renvoyé (quantité renvoyée * prix)<br>Opération : Somme<br>Horodatage Colonne : Date de retour demandée |

{style="table-layout:auto"}

## Connexions à d’autres tables

`enterprise_rma`

* Créez des colonnes jointes telles que des `Return date\_requested` sur la table `enterprise_rma_item_entity` via la jointure suivante :
* Commerce 1.x : `enterprise_rma_item_entity.rma_entity_id ` (plusieurs) => `enterprise_rma.entity_id` (un)
* Commerce 2.x : `magento_rma_item_entity.rma_entity_id ` (plusieurs) => `magento_rma.entity_id` (un)

`sales_flat_order_item`

* Créer des colonnes jointes sur le  `enterprise_rma_item_entity` la table via la jointure suivante :

* Commerce 1.x : `enterprise_rma_item_entity.order_item_id ` (plusieurs) => `sales_flat_order_item.item_id` (un)
* Commerce 2.x : `magento_rma_item_entity.order_item_id ` (plusieurs) => `sales_order_item.item_id` (un)
