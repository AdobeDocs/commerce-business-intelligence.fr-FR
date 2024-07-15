---
title: Diagrammes de relation d’entité
description: Apprenez-en plus sur quelques diagrammes ER pour vous aider à visualiser la relation entre une poignée de tables de base de données Commerce courantes.
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Diagramme de relation d’entité

Qu’est-ce qu’un **[!UICONTROL entity relationship (ER) diagram]** ? Un diagramme [!UICONTROL ER] est une visualisation de tableaux dans une base de données et de la manière dont ils se relient les uns aux autres. Cette rubrique contient quelques diagrammes [!UICONTROL ER] pour vous aider à visualiser la relation entre quelques tables de base de données Adobe Commerce courantes.

>[!NOTE]
>
>Dans cette rubrique, vous voyez les mots **join**, **relation** et **path**. Ces mots sont tous utilisés pour décrire comment deux tableaux sont connectés.

## Diagramme Commerce principal [!UICONTROL ER]

![4_DB_Chart](../../assets/4_DB_Chart.png)

Ce diagramme `ER` représente les relations entre les tables principales dans une base de données Commerce. En affichant plusieurs relations à la fois, vous pouvez voir comment les données se relient à de nombreuses tables.

Les sections ci-dessous contiennent `ER` diagrammes spécifiques à deux tableaux à la fois. Pour afficher un diagramme et sa description, cliquez sur l’en-tête de cette section.

## `customer\_entity & sales\_flat\_order`

![Un client de plusieurs commandes](../../assets/2_OneCustomerManyOrders.png)

Un client peut passer de nombreuses commandes. La relation entre ces deux tables est `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` n&#39;est pas égal à `sales\_flat\_order.entity\_id`. Le premier peut être considéré comme `customer\_id` et le second comme `order\_id.`

Dans [!DNL Commerce Intelligence], si le chemin entre ces deux tables n&#39;existe pas, vous pouvez [créer le chemin](../data-warehouse-mgr/create-paths-calc-columns.md) dans l&#39;onglet Data Warehouse. Lorsque vous êtes prêt à créer le chemin, il est défini comme suit :

![](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

Une commande peut contenir de nombreux éléments. La relation entre ces deux tables est `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`.

Dans [!DNL Commerce Intelligence], si le chemin entre ces deux tables n&#39;existe pas, vous pouvez [créer le chemin](../data-warehouse-mgr/create-paths-calc-columns.md) dans l&#39;onglet Data Warehouse. Lorsque vous êtes prêt à créer le chemin, définissez-le comme illustré ci-dessous.

![](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

Un produit peut être acheté avec de nombreux articles. La relation entre ces deux tables est `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`.

Dans [!DNL Commerce Intelligence], si le chemin entre ces deux tables n&#39;existe pas, vous pouvez [créer le chemin](../data-warehouse-mgr/create-paths-calc-columns.md) dans l&#39;onglet Data Warehouse. Lorsque vous êtes prêt à créer le chemin, définissez-le comme illustré ci-dessous.

![](../../assets/SFOI___CPE_path.png)
