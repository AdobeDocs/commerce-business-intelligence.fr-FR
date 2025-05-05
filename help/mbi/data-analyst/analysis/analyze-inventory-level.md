---
title: Analyse des niveaux de stock
description: Découvrez comment analyser les niveaux d’inventaire.
exl-id: 620156c5-7bea-4b36-84c7-e0cb4b5cc8be
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Analyse des niveaux de stock

Cette rubrique explique comment configurer un tableau de bord qui fournit des informations sur votre inventaire actuel et contient des instructions destinées aux clients sur l’architecture héritée ou la nouvelle architecture. Vous vous trouvez sur l’architecture héritée si vous ne disposez pas de l’option **[!UICONTROL Data Warehouse Views]** sous le menu **[!UICONTROL Manage Data]**. Si vous utilisez l’architecture héritée, envoyez une [nouvelle demande d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) avec l’objet **[!UICONTROL INVENTORY ANALYSIS]** une fois que vous avez atteint la section désignée dans les instructions _Colonnes calculées_ ci-dessous.

## Colonnes à suivre :

### Colonnes pour suivre les instructions

* table **[!UICONTROL cataloginventory_stock_item]** :
   * **`item_id`**
   * **`product_id`**
   * **`qty`**

* table **[!UICONTROL catalog_product_entity]** :
   * **`entity_id`**
   * **`sku`**
   * **`created_at`**

## Colonnes calculées :

+++ Nouvelle architecture

* table **[!UICONTROL catalog_product_entity]** :
   * **`Product's most recent order date`**
      * [!UICONTROL Column type] : `Many to One`
      * &#x200B;

        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path] : `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez un [!UICONTROL column] : `created_at`
      * [!UICONTROL Filters] :
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type] : `Many to One`
      * &#x200B;

        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path] : `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez un [!UICONTROL column] : `created_at`
      * [!UICONTROL Filters] :
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type] : `Same Table`
      * &#x200B;

        [!UICONTROL Column equation]: `AGE`
      * Sélectionner [!UICONTROL DATETIME column] : `Product's most recent order date`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type] : `Many to One`
      * &#x200B;

        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path] : `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez un [!UICONTROL column] : `qty_ordered`
      * [!UICONTROL Filters] :
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type] : `Same Table`
      * &#x200B;

        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] entrées :
         * A : `Product's lifetime number of items sold`
         * B : `Product's first order date`
      * &#x200B;

        [!UICONTROL Datatype]: `Decimal`
      * Définition :
         * Cas où A est nul ou B est nul puis nul autre arrondi(A::decimal/(extract(epoch from (current_timestamp - B)))::decimal/604800.0),2).

* table **[!UICONTROL cataloginventory_stock_item]** :
   * **`Sku`**
      * [!UICONTROL Column type] : `One to Many`
      * &#x200B;

        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path] : `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez un [!UICONTROL column] : `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type] : `One to Many`
      * &#x200B;

        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path] : `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez un [!UICONTROL column] : `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type] : `One to Many`
      * &#x200B;

        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path] : `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez un [!UICONTROL column] : `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type] : `One to Many`
      * &#x200B;

        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path] : `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez un [!UICONTROL column] : `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * [!UICONTROL Column type] : `Same Table`
      * &#x200B;

        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] entrées :
         * A : `qty`
         * B : `Avg products sold per week (all time)`
      * &#x200B;

        [!UICONTROL Datatype]: `Decimal`
      * Définition :
         * Cas où A est nul ou B est nul ou B = 0,0 alors nul autre arrondi (A ::décimal/B,2)

+++
+++ Architecture héritée

* table **[!UICONTROL catalog_product_entity]** :
   * **`Product's most recent order date`**
      * [!UICONTROL Column type] : `Many to One`
      * &#x200B;

        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path] : `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez un [!UICONTROL column] : `created_at`
      * [!UICONTROL Filters] :
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type] : `Many to One`
      * &#x200B;

        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path] : `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez un [!UICONTROL column] : `created_at`
      * [!UICONTROL Filters] :
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type] : `Same Table`
      * &#x200B;

        [!UICONTROL Column equation]: `AGE`
      * Sélectionnez la colonne DATETIME : **`Product's most recent order date`**

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type] : `Many to One`
      * &#x200B;

        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path] : **`sales_order_item.product_id => catalog_product_entity.entity_id`**
      * Sélectionnez un [!UICONTROL column] : **`qty_ordered`**
      * [!UICONTROL Filters] :
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * Créé par un analyste lorsque vous envoyez votre demande de prise en charge **[INVENTORY ANALYSIS]**

* table **[!UICONTROL cataloginventory_stock_item]** :
   * **`Sku`**
      * [!UICONTROL Column type] : `One to Many`
      * &#x200B;

        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path] : `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez un [!UICONTROL column] : `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type] : `One to Many`
      * &#x200B;

        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path] : `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez un [!UICONTROL column] : `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type] : `One to Many`
      * &#x200B;

        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path] : `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez un [!UICONTROL column] : `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type] : `One to Many`
      * &#x200B;

        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path] : `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionnez un [!UICONTROL column] : `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * Créé par un analyste lorsque vous envoyez votre demande d’assistance **[!UICONTROL INVENTORY ANALYSIS]**

+++

## Mesures

### Instructions sur les mesures

* table **[!UICONTROL cataloginventory_stock_item]** :
   * **`Inventory on hand`** : cette mesure exécute une
      * **Somme** sur la
      * **`qty`** colonne classée par
      * Colonne [Aucun]

## Rapports

### Instructions du rapport

* **`Inventory on hand by sku`**
   * [!UICONTROL Metric] : `Inventory on hand`
   * [!UICONTROL Time period] : `All time`
   * Intervalle de temps : `None`
   * [!UICONTROL Group by] :
      * `Sku`
      * `Weeks on hand`
   * &#x200B;

     [!UICONTROL Chart type]: `Table`

* **`Inventory with less than 2 weeks on hand (order now)`**
   * [!UICONTROL Metric] : `Inventory on hand`
      * [!UICONTROL Filters] :
         * [A] `Weeks on hand` `< 2`

   * [!UICONTROL Time period] : `All time`
   * Intervalle de temps : `None`
   * &#x200B;

     [!UICONTROL Groupe par]: `Sku`
   * &#x200B;

     [!UICONTROL Chart type]: `Table`

* **`Inventory with more than 26 weeks on hand (put on sale)`**
   * [!UICONTROL Metric] : `Inventory on hand`
      * [!UICONTROL Filters] :
         * [A] `Weeks on hand` `> 26`

   * [!UICONTROL Time period] : `All time`
   * Intervalle de temps : `None`
   * &#x200B;

     [!UICONTROL Groupe par]: `Sku`
   * &#x200B;

     [!UICONTROL Chart type]: `Table`

Si vous rencontrez des questions lors de la création de cette analyse ou si vous souhaitez simplement contacter l’équipe des services professionnels, [contactez l’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr).
