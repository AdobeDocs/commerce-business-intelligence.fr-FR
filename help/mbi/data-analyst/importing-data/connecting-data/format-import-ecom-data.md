---
title: Formatage et importation de données eCommerce
description: Découvrez les formats de données idéaux à utiliser pour charger des données eCommerce.
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/3Aa9DgQL0H9cNeJOJ7-qHkROOkphjzpQkDvJ0KwOIwY
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 460
ht-degree: 0%

---

# Formatage et importation de données

Si vous utilisez une intégration qui n’est actuellement pas prise en charge par [!DNL Adobe Commerce Intelligence], vous pouvez tout de même utiliser la fonctionnalité [Chargement de fichier](using-file-uploader.md) pour intégrer vos données dans votre Data Warehouse. Cette rubrique couvre les formats de données idéaux à utiliser pour charger des données d’e-commerce.

## `Orders` table

Le tableau `orders` doit contenir une ligne pour chaque transaction effectuée par l&#39;entreprise. Les colonnes potentielles sont les suivantes :

| Nom de la colonne | Description |
|----|----|
| `Order ID` | L’ID de commande doit être unique pour chaque ligne du tableau. En outre, il s’agit généralement de la clé primaire de la table. |
| `Customer` | Client qui a passé la commande. |
| `Order total` | Total de la commande. Il peut s&#39;agir d&#39;une colonne basée sur des calculs, où les valeurs d&#39;autres colonnes, telles que sous-total et expédition, constituent le total de cette colonne. |
| `Currency` | Devise dans laquelle la commande a été payée. Inclure si pertinent. |
| ` Order status` | Statut de la commande, tel que `In Progress`, `Refunded` ou `Complete`. La valeur de cette colonne change (si elle est incomplète). Les données nouvelles et mises à jour peuvent être importées à l’aide de la fonction [Ajouter des données](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) sur la page `File Uploads`. |
| `Acquisition/marketing channel` | Canal d’acquisition ou de marketing auprès duquel le client qui a passé la commande a été référencé. |
| `Order datetime` | Date et heure de création de la commande. |
| `Order updated at` | Date et heure de la dernière modification de l&#39;enregistrement de commande. |

{style="table-layout:auto"}

## `Order detail/items` table {#itemstable}

Le tableau `order_detail / items` doit contenir une ligne pour chaque élément distinct dans chaque ordre. Les colonnes potentielles sont les suivantes :

| Nom de la colonne | Description |
|----|----|
| `Order item ID` | L’ID d’élément de commande doit être unique pour chaque ligne du tableau. En outre, il s’agit généralement de la `primary key` du tableau. |
| `Order ID` | Identifiant de la commande. |
| `Product ID` | Identifiant du produit. |
| `Product name` | Nom du produit. |
| `Product's unit price` | Prix d’une seule unité du produit. |
| `Quantity` | Quantité du produit dans la commande. |

## `Customers` table {#customerstable}

Le tableau `customers` doit contenir une ligne pour chaque compte client. Les colonnes potentielles sont les suivantes :

| Nom de la colonne | Description |
|----|----|
| `Customer ID` | L’ID de client doit être unique pour chaque ligne du tableau. En outre, il s’agit généralement de la clé primaire de la table. |
| `Customer created at` | Date et heure de création du compte du client. |
| `Customer modified at` | Date et heure de la dernière modification du compte du client. |
| `Acquisition/marketing channel source` | Canal d’acquisition ou de marketing duquel le client a été référencé. |
| `Demographic info` | Des informations démographiques telles que la tranche d’âge et le sexe peuvent être utilisées pour segmenter vos rapports. |
| `Acquisition/marketing channel` | Canal d’acquisition ou de marketing auprès duquel le client qui a passé la commande a été référencé. |

## `Subscription payments` table

La table `subscriptions` doit contenir une ligne pour chaque paiement d&#39;abonnement. Les colonnes potentielles sont les suivantes :

| Nom de la colonne | Description |
|----|----|
| `Subscription ID` | L’ID d’abonnement doit être unique pour chaque ligne du tableau. En outre, il s’agit généralement de la clé primaire de la table. |
| `Customer ID` | Identifiant du client qui a effectué le paiement. |
| `Payment amount` | Montant du paiement de l’abonnement. |
| `Start date` | Date et heure de début de la période couverte par le paiement. |
| `End date` | Date et heure de fin de la période couverte par le paiement. |
