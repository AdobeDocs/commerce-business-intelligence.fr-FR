---
title: Formatage et importation de données eCommerce
description: Découvrez les formats de données idéaux à utiliser pour charger des données eCommerce.
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '459'
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
