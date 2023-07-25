---
title: Formatage et importation de données eCommerce
description: Découvrez les formats de données idéaux à utiliser pour le transfert de données eCommerce.
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# Formatage et import de données

Si vous utilisez une intégration qui n’est actuellement pas prise en charge par [!DNL Adobe Commerce Intelligence], vous pouvez toujours utiliser la variable [Fonction de téléchargement de fichier](using-file-uploader.md) pour intégrer vos données dans votre Data Warehouse. Cette rubrique couvre les formats de données idéaux à utiliser pour le transfert de données de commerce électronique.

## `Orders` table

Le `orders` La table doit contenir une ligne pour chaque transaction effectuée par l’entreprise. Les colonnes potentielles sont les suivantes :

| Nom de la colonne | Description |
|----|----|
| `Order ID` | L’identifiant de commande doit être unique pour chaque ligne du tableau. En outre, il s’agit généralement de la clé Principale du tableau. |
| `Customer` | Le client qui a passé la commande. |
| `Order total` | Total de la commande. Il peut s’agir d’une colonne basée sur des calculs, dans laquelle les valeurs d’autres colonnes, telles que le sous-total et l’expédition, constituent le total de cette colonne. |
| `Currency` | Devise dans laquelle la commande a été payée. Inclure si nécessaire. |
| ` Order status` | État de la commande, tel que `In Progress`, `Refunded`ou `Complete`. La valeur de cette colonne change (si elle n’est pas terminée). Les données nouvelles et mises à jour peuvent être importées à l’aide de la variable [Fonction d’ajout de données](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) sur le `File Uploads` page. |
| `Acquisition/marketing channel` | Canal d’acquisition ou marketing duquel le client qui a passé la commande a été référencé. |
| `Order datetime` | Date et heure de création de la commande. |
| `Order updated at` | Date et heure de la dernière modification de l’enregistrement de commande. |

{style="table-layout:auto"}

## `Order detail/items` table {#itemstable}

Le `order_detail / items` Le tableau doit contenir une ligne pour chaque élément distinct dans chaque ordre. Les colonnes potentielles sont les suivantes :

| Nom de la colonne | Description |
|----|----|
| `Order item ID` | L’identifiant de l’élément de commande doit être unique pour chaque ligne du tableau. En outre, il s’agit généralement de la variable `primary key` pour la table. |
| `Order ID` | L’identifiant de la commande. |
| `Product ID` | ID du produit. |
| `Product name` | Nom du produit. |
| `Product's unit price` | Le prix d’une seule unité du produit. |
| `Quantity` | La quantité du produit dans la commande. |

## `Customers` table {#customerstable}

Le `customers` Le tableau doit contenir une ligne pour chaque compte client. Les colonnes potentielles sont les suivantes :

| Nom de la colonne | Description |
|----|----|
| `Customer ID` | L’ID de client doit être unique pour chaque ligne du tableau. En outre, il s’agit généralement de la clé Principale du tableau. |
| `Customer created at` | Date et heure de création du compte du client. |
| `Customer modified at` | Date et heure de la dernière modification du compte du client. |
| `Acquisition/marketing channel source` | Canal d’acquisition ou marketing à partir duquel le client a été référencé. |
| `Demographic info` | Les informations démographiques telles que la tranche d’âge et le sexe peuvent être utilisées pour segmenter vos rapports. |
| `Acquisition/marketing channel` | Canal d’acquisition ou marketing duquel le client qui a passé la commande a été référencé. |

## `Subscription payments` table

Le `subscriptions` le tableau doit contenir une ligne pour chaque paiement d’abonnement. Les colonnes potentielles sont les suivantes :

| Nom de la colonne | Description |
|----|----|
| `Subscription ID` | L’ID d’abonnement doit être unique pour chaque ligne du tableau. En outre, il s’agit généralement de la clé Principale du tableau. |
| `Customer ID` | L’identifiant du client qui a effectué le paiement. |
| `Payment amount` | Le montant du paiement d’abonnement. |
| `Start date` | Date et heure de début de la période couverte par le paiement. |
| `End date` | Date et heure de fin de la période couverte par le paiement. |
