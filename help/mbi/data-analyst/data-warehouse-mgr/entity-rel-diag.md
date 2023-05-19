---
title: Diagrammes de relation d’entité
description: Découvrez quelques diagrammes d’E/S pour vous aider à visualiser la relation entre une poignée de tableaux de base de données Commerce courants.
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# Diagramme de relation d’entité

Qu’est-ce qu’une **[!UICONTROL entity relationship (ER) diagram]**? Un [!UICONTROL ER] diagramme est une visualisation des tableaux dans une base de données et de la manière dont ils sont liés les uns aux autres. Cette rubrique contient quelques [!UICONTROL ER] des diagrammes pour vous aider à visualiser la relation entre quelques tables de base de données Adobe Commerce courantes.

>[!NOTE]
>
>Dans cette rubrique, vous voyez les mots **join**, **relation**, et **path**. Ces mots sont tous utilisés pour décrire comment deux tableaux sont connectés.

## Commerce de base [!UICONTROL ER] Diagramme

![4_DB_Chart](../../assets/4_DB_Chart.png)

Ceci `ER` diagramme représente les relations entre les tables principales dans une base de données Commerce. En affichant plusieurs relations à la fois, vous pouvez voir comment les données se relient à de nombreuses tables.

Les sections ci-dessous contiennent `ER` des diagrammes spécifiques à deux tableaux à la fois. Pour afficher un diagramme et sa description, cliquez sur l’en-tête de cette section.

## `customer\_entity & sales\_flat\_order`

![Un client et plusieurs commandes](../../assets/2_OneCustomerManyOrders.png)

Un client peut passer de nombreuses commandes. La relation entre ces deux tables est la suivante : `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` n’est pas égal à `sales\_flat\_order.entity\_id`. Le premier peut être considéré comme un `customer\_id` et le second peut être considéré comme un `order\_id.`

Within [!DNL Commerce Intelligence], si le chemin entre ces deux tables n’existe pas, vous pouvez [création du chemin](../data-warehouse-mgr/create-paths-calc-columns.md) dans l’onglet Data Warehouse. Lorsque vous êtes prêt à créer le chemin, il est défini comme suit :

![](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

Une commande peut contenir de nombreux éléments. La relation entre ces deux tables est la suivante : `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`.

Within [!DNL Commerce Intelligence], si le chemin entre ces deux tables n’existe pas, vous pouvez [création du chemin](../data-warehouse-mgr/create-paths-calc-columns.md) dans l’onglet Data Warehouse. Lorsque vous êtes prêt à créer le chemin, définissez-le comme illustré ci-dessous.

![](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

Un produit peut être acheté avec de nombreux articles. La relation entre ces deux tables est la suivante : `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`.

Within [!DNL Commerce Intelligence], si le chemin entre ces deux tables n’existe pas, vous pouvez [création du chemin](../data-warehouse-mgr/create-paths-calc-columns.md) dans l’onglet Data Warehouse. Lorsque vous êtes prêt à créer le chemin, définissez-le comme illustré ci-dessous.

![](../../assets/SFOI___CPE_path.png)
