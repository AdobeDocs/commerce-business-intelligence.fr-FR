---
title: Analyse des niveaux de stock
description: Découvrez comment analyser les niveaux d’inventaire.
exl-id: 620156c5-7bea-4b36-84c7-e0cb4b5cc8be
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Analyse des niveaux de stock

Cette rubrique explique comment configurer un tableau de bord qui fournira des informations sur votre inventaire actuel. Cette rubrique contient des instructions destinées aux clients sur l’architecture héritée ou la nouvelle architecture. Vous utilisez l’architecture héritée si vous ne disposez pas de la variable **[!UICONTROL Data Warehouse Views]** sous l’option **[!UICONTROL Manage Data]** ). Si vous utilisez l’architecture héritée, envoyez une [nouvelle demande d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) avec le sujet **[!UICONTROL INVENTORY ANALYSIS]** une fois que vous avez atteint la section désignée dans la variable _Colonnes calculées_ instructions ci-dessous.

## Colonnes à suivre :

### Colonnes pour suivre les instructions

* **[!UICONTROL cataloginventory_stock_item]** table :
   * **`item_id`**
   * **`product_id`**
   * **`qty`**

* **[!UICONTROL catalog_product_entity]** table :
   * **`entity_id`**
   * **`sku`**
   * **`created_at`**

## Colonnes calculées :

### Nouvelle architecture

* **[!UICONTROL catalog_product_entity]** table :
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez une [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez une [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `AGE`
      * Sélectionner [!UICONTROL DATETIME column]: `Product's most recent order date`
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez une [!UICONTROL column]: `qty_ordered`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] entrées :
         * A : `Product's lifetime number of items sold`
         * B : `Product's first order date`
      * 
         [!UICONTROL Datatype]: `Decimal`
      * Définition :
         * Cas où A est nul ou B est nul puis nul autre arrondi(A::decimal/(extract(epoch from (current_timestamp - B)))::decimal/604800.0),2).





* **[!UICONTROL cataloginventory_stock_item]** table :
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez une [!UICONTROL column]: `sku`
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez une [!UICONTROL column]: `Product's lifetime number of items sold`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez une [!UICONTROL column]: `Seconds since product's most recent order date`
   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez une [!UICONTROL column]: `Avg products sold per week (all time)`
   * **`Weeks on hand`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] entrées :
         * A : `qty`
         * B : `Avg products sold per week (all time)`
      * 
         [!UICONTROL Datatype]: `Decimal`
      * Définition :
         * Cas où A est nul ou B est nul ou B = 0,0 alors nul autre arrondi (A ::décimal/B,2)





### Architecture héritée

* **[!UICONTROL catalog_product_entity]** table :
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez une [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez une [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `AGE`
      * Sélectionnez la colonne DATETIME : **`Product's most recent order date`**
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
      * Sélectionnez une [!UICONTROL column]: **`qty_ordered`**
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Avg products sold per week (all time)`**
      * sera créé par un analyste lorsque vous envoyez votre fichier **[ANALYSE DES INVENTAIRES]** demande d’assistance





* **[!UICONTROL cataloginventory_stock_item]** table :
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez une [!UICONTROL column]: `sku`
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez une [!UICONTROL column]: `Product's lifetime number of items sold`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez une [!UICONTROL column]: `Seconds since product's most recent order date`
   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez une [!UICONTROL column]: `Avg products sold per week (all time)`
   * **`Weeks on hand`**
      * sera créé par un analyste lorsque vous envoyez votre fichier **[!UICONTROL INVENTORY ANALYSIS]** demande d’assistance





## Mesures

### Instructions sur les mesures

* **[!UICONTROL cataloginventory_stock_item]** table :
   * **`Inventory on hand`**: cette mesure effectue une
      * **Somme** sur le
      * **`qty`** colonne triée par
      * [Aucun] column

## Rapports

### Instructions du rapport

* **`Inventory on hand by sku`**
   * [!UICONTROL Metric]: `Inventory on hand`
   * [!UICONTROL Time period]: `All time`
   * Intervalle temporel : `None`
   * [!UICONTROL Group by]:
      * `Sku`
      * `Weeks on hand`
   * 

      [!UICONTROL Chart type]: `Table`

* **`Inventory with less than 2 weeks on hand (order now)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `< 2`
   * [!UICONTROL Time period]: `All time`
   * Intervalle temporel : `None`
   * 
      [!UICONTROL Groupe par]: `Sku`
   * 

      [!UICONTROL Chart type]: `Table`


* **`Inventory with more than 26 weeks on hand (put on sale)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `> 26`
   * [!UICONTROL Time period]: `All time`
   * Intervalle temporel : `None`
   * 
      [!UICONTROL Groupe par]: `Sku`
   * 

      [!UICONTROL Chart type]: `Table`


Si vous rencontrez des questions lors de la création de cette analyse ou si vous souhaitez simplement faire appel à notre équipe de services professionnels, [support technique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
