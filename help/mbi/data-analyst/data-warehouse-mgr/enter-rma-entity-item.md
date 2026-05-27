---
title: Table Enterprise_Rma_Item_Entity
description: Découvrez comment analyser les informations relatives à un article spécifique à partir d'un retour demandé.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/jBMtEluq3XNIzItebuvDQ43PAuW6mAsyG7RkHn8URJ4
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 08a466710b782238003c6bdb8cefacd07134291c
workflow-type: tm+mt
source-wordcount: 271
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
| `entity_id` | Identifiant unique de la table. Chaque `entity_id` représente un élément dont le retour a été demandé. |
| `rma_entity_id` | Clé étrangère associée à la table `enterprise_rma`. |
| `status` | Statut du retour de l&#39;article. Les valeurs incluent &#39;received&#39;, &#39;pending&#39;, &#39;authorized&#39;, entre autres. Les valeurs de ce statut peuvent ne pas correspondre à la valeur du statut du retour global. |
| `qty_requested` | Quantité demandée par le client pour le retour. |
| `qty_approved` | Quantité approuvée pour le retour. |
| `qty_returned` | Quantité renvoyée. |
| `order_item_id` | Clé étrangère associée à la table `sales_flat_order_item`. |
| `product_sku` | SKU renvoyé. |

{style="table-layout:auto"}

## Colonnes calculées courantes

| **Nom de la colonne** | **Description** |
|---|---|
| `Return date_requested` | Il s&#39;agit de la date à laquelle le client a demandé le retour. |
| `Item price` | Prix de l’article. |
| `Return item's total value (qty_returned * price)` | Il s&#39;agit de la valeur monétaire totale des articles retournés. Permet de calculer le montant total des retours dans la table des `enterprise_rma`. |

{style="table-layout:auto"}

## Mesures courantes

| **Nom de la mesure** | **Description** | **Construction** |
|---|---|---|
| `Number of items returned` | Nombre d’éléments renvoyés. | Colonne d&#39;opération : quantité renvoyée<br>Opération : Somme<br>Horodatage Colonne : Date de retour demandée |
| `Returned items' total value` | Montant monétaire renvoyé. | Colonne Opération : Valeur totale de l&#39;article renvoyé (quantité renvoyée * prix)<br>Opération : Somme<br>Horodatage Colonne : Date de retour demandée |

{style="table-layout:auto"}

## Connexions à d’autres tables

`enterprise_rma`

* Créez des colonnes jointes telles que des `Return date_requested` sur la table `enterprise_rma_item_entity` via la jointure suivante :
* Commerce 1.x : `enterprise_rma_item_entity.rma_entity_id ` (plusieurs) => `enterprise_rma.entity_id` (un)
* Commerce 2.x : `magento_rma_item_entity.rma_entity_id ` (plusieurs) => `magento_rma.entity_id` (un)

`sales_flat_order_item`

* Créez des colonnes jointes sur la table `enterprise_rma_item_entity` via la jointure suivante :

* Commerce 1.x : `enterprise_rma_item_entity.order_item_id ` (plusieurs) => `sales_flat_order_item.item_id` (un)
* Commerce 2.x : `magento_rma_item_entity.order_item_id ` (plusieurs) => `sales_order_item.item_id` (un)
