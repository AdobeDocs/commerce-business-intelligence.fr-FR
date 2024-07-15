---
title: Table Enterprise_Rma_Item_Entity
description: Découvrez comment analyser les informations relatives à un élément spécifique à partir d’un retour demandé.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# enterprise_rma_item_entity Table

Chaque ligne de la table `enterprise_rma_item_entity` (souvent appelée `magento_rma_item_entity` dans Commerce 2.x, mais le nom peut être personnalisé) contient des informations sur un élément spécifique d’un retour demandé.

>[!NOTE]
>
>Cette table n’est fournie en standard avec votre compte Commerce que si vous êtes un client `Enterprise Edition` ou `Enterprise Cloud Edition`.

## Colonnes natives communes

| **Nom de colonne** | **Description** |
|---|---|
| `entity\_id` | Identifiant unique de la table. Chaque `entity\_id` représente un élément qui a été demandé pour être renvoyé. |
| `rma\_entity\_id` | Clé étrangère associée à la table `enterprise\_rma`. |
| `status` | État du retour de l’élément. Les valeurs comprennent &quot;reçu&quot;, &quot;en attente&quot;, &quot;autorisé&quot;, entre autres. Les valeurs de cet état peuvent ne pas correspondre à la valeur de l’état global du retour. |
| `qty\_requested` | Quantité que le client demande de retour. |
| `qty\_approved` | La quantité validée pour le retour. |
| `qty\_returned` | Quantité renvoyée. |
| `order\_item\_id` | Clé étrangère associée à la table `sales\_flat\_order\_item`. |
| `product\_sku` | Le sku en cours de retour. |

{style="table-layout:auto"}

## Colonnes calculées courantes

| **Nom de colonne** | **Description** |
|---|---|
| `Return date\_requested` | Il s’agit de la date à laquelle le client a demandé le retour. |
| `Item price` | Le prix de l’article. |
| `Return item's total value (qty\_returned * price)` | Il s’agit de la valeur monétaire totale des éléments renvoyés. Ceci est utilisé pour calculer le montant total du retour sur la table `enterprise\_rma`. |

{style="table-layout:auto"}

## Mesures courantes

| **Nom de mesure** | **Description** | **Construction** |
|---|---|---|
| `Number of items returned` | Nombre d’éléments renvoyés. | Colonne d’opération : qty renvoyée<br>Opération : Somme<br>Colonne d’horodatage : date de retour demandée |
| `Returned items' total value` | Le montant monétaire renvoyé. | Colonne d’opération : valeur totale de l’élément de retour (quantité renvoyée * prix)<br>Opération : Somme<br>Colonne d’horodatage : date de retour demandée |

{style="table-layout:auto"}

## Connexions à d’autres tableaux

`enterprise_rma`

* Créez des colonnes jointes telles que `Return date\_requested` sur la table `enterprise_rma_item_entity` via la jointure suivante :
* Commerce 1.x : `enterprise_rma_item_entity.rma_entity_id ` (nombreux) => `enterprise_rma.entity_id` (un)
* Commerce 2.x : `magento_rma_item_entity.rma_entity_id ` (nombreux) => `magento_rma.entity_id` (un)

`sales_flat_order_item`

* Créez des colonnes jointes sur la  `enterprise_rma_item_entity` table via la jointure suivante :

* Commerce 1.x : `enterprise_rma_item_entity.order_item_id ` (nombreux) => `sales_flat_order_item.item_id` (un)
* Commerce 2.x : `magento_rma_item_entity.order_item_id ` (nombreux) => `sales_order_item.item_id` (un)
