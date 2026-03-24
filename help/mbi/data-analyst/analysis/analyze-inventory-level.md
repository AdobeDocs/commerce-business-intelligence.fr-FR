---
title: Analyse des niveaux de stock
description: Découvrez comment analyser les niveaux d’inventaire.
exl-id: 620156c5-7bea-4b36-84c7-e0cb4b5cc8be
role: Admin, Developer, User
feature: Dashboards, Reports
TQID: https://experienceleague.adobe.com/z2NS33cMO3wETk6FFyI-rkbPkWxxw2zYxUUjdC4zRa4
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 274
ht-degree: 0%

---

# Analyser les niveaux de stock

Cette rubrique explique comment configurer un tableau de bord qui fournit des informations sur votre inventaire actuel et contient des instructions pour les clients sur l’architecture héritée ou la nouvelle architecture. Vous accédez à l’architecture héritée si vous ne disposez pas de l’option **[!UICONTROL Data Warehouse Views]** dans le menu **[!UICONTROL Manage Data]** . Si vous utilisez l’architecture héritée, envoyez une [nouvelle demande d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) avec l’objet **[!UICONTROL INVENTORY ANALYSIS]** une fois que vous avez atteint la section désignée dans les instructions _Colonnes calculées_ ci-dessous.

## Colonnes à suivre :

### Colonnes pour le suivi des instructions

* **[!UICONTROL cataloginventory_stock_item]** table :
   * **`item_id`**
   * **`product_id`**
   * **`qty`**

* **[!UICONTROL catalog_product_entity]** table :
   * **`entity_id`**
   * **`sku`**
   * **`created_at`**

## Colonnes calculées :

+++ Nouvelle architecture

* **[!UICONTROL catalog_product_entity]** table :
   * **`Product's most recent order date`**
      * [!UICONTROL Column type] : `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path] : `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Sélectionner un [!UICONTROL column] : `created_at`
      * [!UICONTROL Filters] :
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type] : `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path] : `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Sélectionner un [!UICONTROL column] : `created_at`
      * [!UICONTROL Filters] :
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type] : `Same Table`
      * &#x200B;
        [!UICONTROL Column equation]: `AGE`
      * Sélectionner un [!UICONTROL DATETIME column] : `Product's most recent order date`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type] : `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path] : `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Sélectionner un [!UICONTROL column] : `qty_ordered`
      * [!UICONTROL Filters] :
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type] : `Same Table`
      * &#x200B;
        [!UICONTROL Column equation]: `CALCULATION`
      * Entrées [!UICONTROL Column] :
         * A : `Product's lifetime number of items sold`
         * B : `Product's first order date`
      * &#x200B;
        [!UICONTROL Datatype]: `Decimal`
      * Définition :
         * Cas où A est nul ou B est nul alors null else round(A::decimal/(extract(epoch from (current_timestamp - B))::decimal/604800.0),2) end

* **[!UICONTROL cataloginventory_stock_item]** table :
   * **`Sku`**
      * [!UICONTROL Column type] : `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path] : `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionner un [!UICONTROL column] : `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type] : `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path] : `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionner un [!UICONTROL column] : `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type] : `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path] : `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionner un [!UICONTROL column] : `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type] : `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path] : `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionner un [!UICONTROL column] : `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * [!UICONTROL Column type] : `Same Table`
      * &#x200B;
        [!UICONTROL Column equation]: `CALCULATION`
      * Entrées [!UICONTROL Column] :
         * A : `qty`
         * B : `Avg products sold per week (all time)`
      * &#x200B;
        [!UICONTROL Datatype]: `Decimal`
      * Définition :
         * Cas où A est nul ou B est nul ou B = 0,0 puis null else round(A::decimal/B,2) end

+++
+++ Architecture héritée

* **[!UICONTROL catalog_product_entity]** table :
   * **`Product's most recent order date`**
      * [!UICONTROL Column type] : `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path] : `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Sélectionner un [!UICONTROL column] : `created_at`
      * [!UICONTROL Filters] :
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type] : `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path] : `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Sélectionner un [!UICONTROL column] : `created_at`
      * [!UICONTROL Filters] :
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type] : `Same Table`
      * &#x200B;
        [!UICONTROL Column equation]: `AGE`
      * Sélectionner la colonne DATETIME : **`Product's most recent order date`**

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type] : `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path] : **`sales_order_item.product_id => catalog_product_entity.entity_id`**
      * Sélectionner un [!UICONTROL column] : **`qty_ordered`**
      * [!UICONTROL Filters] :
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * Créé par un analyste au moment de l’envoi de votre demande d’assistance **[ANALYSE DES STOCKS]**

* **[!UICONTROL cataloginventory_stock_item]** table :
   * **`Sku`**
      * [!UICONTROL Column type] : `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path] : `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionner un [!UICONTROL column] : `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type] : `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path] : `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionner un [!UICONTROL column] : `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type] : `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path] : `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionner un [!UICONTROL column] : `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type] : `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path] : `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Sélectionner un [!UICONTROL column] : `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * Créé par un analyste au moment de l’envoi de votre demande d’assistance **[!UICONTROL INVENTORY ANALYSIS]**

+++

## Mesures

### Instructions relatives aux mesures

* **[!UICONTROL cataloginventory_stock_item]** table :
   * **`Inventory on hand`** : cette mesure effectue une
      * **Somme** sur le
      * **`qty`** colonne triée par
      * [Aucune] colonne

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
     [!UICONTROL Regrouper par]: `Sku`
   * &#x200B;
     [!UICONTROL Chart type]: `Table`

* **`Inventory with more than 26 weeks on hand (put on sale)`**
   * [!UICONTROL Metric] : `Inventory on hand`
      * [!UICONTROL Filters] :
         * [A] `Weeks on hand` `> 26`

   * [!UICONTROL Time period] : `All time`
   * Intervalle de temps : `None`
   * &#x200B;
     [!UICONTROL Regrouper par]: `Sku`
   * &#x200B;
     [!UICONTROL Chart type]: `Table`

Si vous avez des questions lors de la création de cette analyse ou si vous souhaitez simplement contacter l’équipe des services professionnels, [contactez l’assistance &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr).
