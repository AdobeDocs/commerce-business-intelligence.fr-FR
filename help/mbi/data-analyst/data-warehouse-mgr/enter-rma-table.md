---
title: table enterprise_rma
description: Découvrez comment analyser les informations relatives à une demande de retour spécifique.
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/ofPlk5xNr8aspjFlpzEtDtjcOPm9DrQFYX9-vPDfK6w
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: ad4dda927f0b1b2eba9596d7adfd1419676cf03d
workflow-type: tm+mt
source-wordcount: 275
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
| `entity_id` | Identifiant unique de la table. Chaque `entity_id` représente une demande de retour. |
| `date_requested` | Date à laquelle le retour a été demandé. |
| `status` | Statut du retour. Les valeurs incluent &#39;received&#39;, &#39;pending&#39;, &#39;authorized&#39;, entre autres. |
| `order_id` | Clé étrangère associée à la table `sales_flat_order`. |
| `customer_id` | Clé étrangère associée à la table `customer_entity`. |

{style="table-layout:auto"}

## Colonnes calculées courantes

| **Nom de la colonne** | **Description** |
|---|---|
| `Order's created_at` | Il s’agit de la date de la commande d’origine. Vous pouvez l’utiliser pour obtenir le temps entre la commande et la demande de retour. |
| `Customer's order number` | Numéro de commande du client associé à la commande d&#39;origine. |
| `Seconds between order's created_at and return's date_requested` | Nombre de secondes écoulées entre la date de commande et la demande de retour. |
| `Return's total value` | Il s&#39;agit du montant monétaire total qui est renvoyé. Il s&#39;agit de la somme du montant de retour individuel de chaque article retourné. |

{style="table-layout:auto"}

## Mesures courantes

| **Nom de la mesure** | **Description** | **Construction** |
|---|---|---|
| `Number of returns` | Nombre de retours demandés. | `Operation` colonne : `entity_id`<br>`Operation` : `Count`<br>`Timestamp` Colonne : `date requested` |
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
