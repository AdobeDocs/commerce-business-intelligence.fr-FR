---
title: table enterprise_rma
description: Découvrez comment analyser les informations relatives à une demande de retour spécifique.
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# table enterprise_rma

Chaque ligne du tableau `enterprise_rma` (souvent appelée `magento_rma` dans Adobe Commerce 2.x, mais son nom peut être personnalisé) contient des informations sur une requête de retour spécifique.

>[!NOTE]
>
>Ce tableau n’est fourni de série avec votre compte Adobe Commerce que si vous êtes un client `Enterprise Edition` ou `Enterprise Cloud Edition`.

## Colonnes natives courantes

| **Nom de la colonne** | **Description** |
|---|---|
| `entity\_id` | Identifiant unique de la table. Chaque `entity\_id` représente une demande de retour. |
| `date\_requested` | Date à laquelle le retour a été demandé. |
| `status` | Statut du retour. Les valeurs incluent &#39;received&#39;, &#39;pending&#39;, &#39;authorized&#39;, entre autres. |
| `order\_id` | Clé étrangère associée à la table `sales\_flat\_order`. |
| `customer\_id` | Clé étrangère associée à la table `customer\_entity`. |

{style="table-layout:auto"}

## Colonnes calculées courantes

| **Nom de la colonne** | **Description** |
|---|---|
| `Order's created\_at` | Il s’agit de la date de la commande d’origine. Vous pouvez l’utiliser pour obtenir le temps entre la commande et la demande de retour. |
| `Customer's order number` | Numéro de commande du client associé à la commande d&#39;origine. |
| `Seconds between order's created\_at and return's date\_requested` | Nombre de secondes écoulées entre la date de commande et la demande de retour. |
| `Return's total value` | Il s&#39;agit du montant monétaire total qui est renvoyé. Il s&#39;agit de la somme du montant de retour individuel de chaque article retourné. |

{style="table-layout:auto"}

## Mesures courantes

| **Nom de la mesure** | **Description** | **Construction** |
|---|---|---|
| `Number of returns` | Nombre de retours demandés. | `Operation` colonne : `entity id`<br>`Operation` : `Count`<br>`Timestamp` Colonne : `date requested` |
| `Total returned amount` | Montant monétaire total renvoyé. | `Operation `Colonne : `Return's total value`<br>`Operation` : Somme <br>`Timestamp` Colonne : date demandée |
| `Average returned amount` | Montant monétaire moyen renvoyé. | `Operation`` Column: Return's total value`<br>`Operation` : `Average`<br>`Timestamp` Colonne : `date requested` |
| `Average time to return` | Durée moyenne entre la commande et le retour. | `Operation` Colonne : secondes entre la date de création de la commande et la date de retour demandée<br>`Operation` : `Average`<br>`Timestamp` Colonne : `date requested` |

{style="table-layout:auto"}

## Connexions à d’autres tables

`sale_flat_order`

* Créez des colonnes jointes pour segmenter et filtrer par attributs au niveau de l&#39;ordre sur la table `enterprise_rma` via la jointure suivante :
   * Commerce 1.x : `enterprise_rma.order_id` (plusieurs) => `sales_flat_order.entity_id` (un)
   * Commerce 2.x : `magento_rma.order_id` (plusieurs) => `sales_order.entity_id` (un)

`enterprise_rma_item_entity`

* Créez des colonnes multiples-à-un telles que des `Return's total value` sur la table `enterprise_rma` via la jointure suivante :
   * Commerce 1.x : `enterprise_rma_item_entity.rma_entity_id` (plusieurs) => `enterprise_rma.entity_id` (un)
   * Commerce 2.x : `magento_rma_item_entity.rma_entity_id ` (plusieurs) => `magento_rma.entity_id` (un)
