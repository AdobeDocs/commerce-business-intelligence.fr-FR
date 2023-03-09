---
title: Table Enterprise_Rma_Item_Entity
description: Découvrez comment analyser les informations relatives à un élément spécifique à partir d’un retour demandé.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# enterprise_rma_item_entity Table

Chaque ligne du `enterprise_rma_item_entity` table (souvent appelée `magento_rma_item_entity` dans Commerce 2.x, mais le nom peut être personnalisé) contient des informations sur un élément spécifique d’un retour demandé.

>[!NOTE]
>
>Ce tableau est fourni avec votre compte Commerce uniquement si vous êtes un `Enterprise Edition` ou `Enterprise Cloud Edition` client.

## Colonnes natives communes

| **Nom de la colonne** | **Description** |
|---|---|
| `entity\_id` | Identifiant unique du tableau. Chaque `entity\_id` représente un élément qui a été demandé pour renvoi. |
| `rma\_entity\_id` | Clé étrangère associée à la variable `enterprise\_rma` table. |
| `status` | État du retour de l’élément. Les valeurs comprennent &quot;reçu&quot;, &quot;en attente&quot;, &quot;autorisé&quot;, entre autres. Les valeurs de cet état peuvent ne pas correspondre à la valeur de l’état global du retour. |
| `qty\_requested` | Quantité que le client demande de retour. |
| `qty\_approved` | La quantité validée pour le retour. |
| `qty\_returned` | Quantité renvoyée. |
| `order\_item\_id` | Clé étrangère associée à la variable `sales\_flat\_order\_item` table. |
| `product\_sku` | Le sku en cours de retour. |

{style="table-layout:auto"}

## Colonnes calculées courantes

| **Nom de la colonne** | **Description** |
|---|---|
| `Return date\_requested` | Il s’agit de la date à laquelle le client a demandé le retour. |
| `Item price` | Le prix de l’article. |
| `Return item's total value (qty\_returned * price)` | Il s’agit de la valeur monétaire totale des éléments renvoyés. Elle sert à calculer le montant total du retour sur la variable `enterprise\_rma` table. |

{style="table-layout:auto"}

## Mesures courantes

| **Nom de la mesure** | **Description** | **Construction** |
|---|---|---|
| `Number of items returned` | Nombre d’éléments renvoyés. | Colonne de l’opération : quantité renvoyée<br>Opération : Somme<br>Colonne Horodatage : Date de retour demandée |
| `Returned items' total value` | Le montant monétaire renvoyé. | Colonne de l’opération : Valeur totale de l’élément de retour (quantité renvoyée * prix)<br>Opération : Somme<br>Colonne Horodatage : Date de retour demandée |

{style="table-layout:auto"}

## Connexions à d’autres tableaux

`enterprise_rma`

* Créez des colonnes jointes, telles que `Return date\_requested` sur le `enterprise_rma_item_entity` via la jointure suivante :
* Commerce 1.x : `enterprise_rma_item_entity.rma_entity_id ` (nombreux) => `enterprise_rma.entity_id` (1)
* Commerce 2.x : `magento_rma_item_entity.rma_entity_id ` (nombreux) => `magento_rma.entity_id` (1)

`sales_flat_order_item`

* Créez des colonnes jointes sur la  `enterprise_rma_item_entity` via la jointure suivante :

* Commerce 1.x : `enterprise_rma_item_entity.order_item_id ` (nombreux) => `sales_flat_order_item.item_id` (1)
* Commerce 2.x : `magento_rma_item_entity.order_item_id ` (nombreux) => `sales_order_item.item_id` (1)
