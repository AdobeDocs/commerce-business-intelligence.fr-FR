---
title: Retour sur investissement marketing
description: Découvrez comment configurer un tableau de bord qui effectue le suivi de votre analyse des canaux, y compris le retour sur investissement global et par campagne.
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
role: Admin,  User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Retour sur investissement marketing

>[!NOTE]
>
>Cette rubrique contient des instructions pour les clients qui utilisent l’architecture d’origine et la nouvelle architecture. Vous passez à la [nouvelle architecture](../../administrator/account-management/new-architecture.md) si la section « Vues Data Warehouse » est disponible après avoir sélectionné « Gérer les données » dans la barre d’outils principale.

Si vous dépensez de l&#39;argent dans la publicité en ligne, vous voulez suivre le rendement de ces dépenses et prendre des décisions fondées sur des données pour d&#39;autres investissements. Cette rubrique explique comment configurer un tableau de bord qui effectue le suivi de votre analyse des canaux, y compris le retour sur investissement global et par campagne.

![](../../assets/Marketing_dashboard_example.png)

Avant de commencer, vous devez connecter vos comptes [!DNL [Facebook Ads]](../importing-data/integrations/facebook-ads.md), [!DNL [Adwords]](../importing-data/integrations/google-adwords.md) et [!DNL [Google Ecommerce]](../importing-data/integrations/google-ecommerce.md) et importer des données supplémentaires sur les dépenses publicitaires en ligne. Cette analyse contient [colonnes calculées avancées](../data-warehouse-mgr/adv-calc-columns.md).

## Tables consolidées

**Architecture originale :** pour rassembler vos dépenses à partir de diverses sources, telles que les [!DNL Facebook Ads] ou les [!DNL Google Adwords], Adobe recommande de créer un **tableau consolidé** de toutes vos dépenses publicitaires. Vous avez besoin d’un analyste pour effectuer cette étape. Si ce n’est pas le cas, [envoyez une demande d’assistance](../../guide-overview.md#Submitting-a-Support-Ticket) à l’`[MARKETING ROI ANALYSIS]` concernée et un analyste crée cette table.

**Nouvelle architecture :** vous pouvez suivre l’exemple dans [cette rubrique Bibliothèque d’analyses](../../data-analyst/data-warehouse-mgr/create-dw-views.md). Dans la nouvelle architecture, les tableaux consolidés sont désormais appelés Vues Data Warehouse.

## Colonnes calculées

Colonnes à créer

* **`Consolidated Digital Ad Spend`** table
* **`Campaign name`** est créé par un analyste Adobe dans le cadre de votre ticket **[ANALYSE DU RSI MARKETING]**

**Architectures originales et nouvelles :**

* **`sales_flat_order`** table
   * **`Order's GA campaign`**
      * Sélectionnez une définition : `Joined Column`
      * [!UICONTROL Create Path] :
      * 
        [!UICONTROL Many]: `sales_flat_order.increment_id`
      * 
        [!UICONTROL One]: `ecommerce####.transaction_id`

      * Sélectionner un [!UICONTROL table] : `ecommerce####`
      * Sélectionner un [!UICONTROL column] : `campaign`
      * [!UICONTROL Path] : `sales_flat_order.increment_id = ecommerce#####.transactionID`

   * **`Order's GA medium`**
      * Sélectionner une définition : Colonne jointe
      * Sélectionner un [!UICONTROL table] : `ecommerce####`
      * Sélectionner un [!UICONTROL column] : `medium`
      * [!UICONTROL Path] : sales_flat_order.increment_id = ecommerce#####.transactionId

   * **`Order's GA source`**
      * Sélectionner une définition : Colonne jointe
      * Sélectionner un [!UICONTROL table] : `ecommerce####`
      * Sélectionner un [!UICONTROL column] : `source`
      * [!UICONTROL Path] : sales_flat_order.increment_id = ecommerce#####.transactionId
^

* **`customer_entity`** table
* **`Customer's first order GA campaign`**
   * Sélectionnez une définition : `Max`
   * Sélectionner un [!UICONTROL table] : `sales_flat_order`
   * Sélectionner un [!UICONTROL column] : `Order's GA campaign`
   * [!UICONTROL Path] : `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter] :
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA source`**
   * Sélectionnez une définition : `Max`
   * Sélectionner un [!UICONTROL table] : `sales_flat_order`
   * Sélectionner un [!UICONTROL column] : `Order's GA source`
   * [!UICONTROL Path] : sales_flat_order.customer_id = customer_entity.entity_id
   * [!UICONTROL Filter] :
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA medium`**
   * Sélectionnez une définition : `Max`
   * Sélectionner un [!UICONTROL table] : `sales_flat_order`
   * Sélectionner un [!UICONTROL column] : `Order's GA medium`
   * [!UICONTROL Path] : `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter] :
      * `Orders we count`
      * `Customer's order number = 1`

* **`sales_flat_order`** table
* **`Customer's first order GA campaign`**
   * Sélectionnez une définition : `Joined Column`
   * Sélectionner un [!UICONTROL table] : `customer_entity`
   * Sélectionner un [!UICONTROL column] : `Customer's first order GA campaign`
   * [!UICONTROL Path] : `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
   * Sélectionner une définition : Colonne jointe
   * Sélectionner un [!UICONTROL table] : `customer_entity`
   * Sélectionner un [!UICONTROL column] : `Customer's first order GA source`
   * [!UICONTROL Path] : `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
   * Sélectionnez une définition : `Joined Column`
   * Sélectionner un [!UICONTROL table] : `customer_entity`
   * Sélectionner un [!UICONTROL column] : `Customer's first order GA medium`
   * [!UICONTROL Path] : `sales_flat_order.customer_id = customer_entity.entity_id`

## Mesures

* **Dépenses publicitaires**
* Dans le tableau **`Consolidated Digital Ad Spend`**
* Cette mesure effectue une **Somme**
* Dans la colonne **`adCost`**
* Classé par l’horodatage **`date`**

* **Impressions publicitaires**
* Dans le tableau **`Consolidated Digital Ad Spend`**
* Cette mesure effectue une **Somme**
* Dans la colonne **`Impressions`**
* Classé par l’horodatage **`Month`**

* **Clics publicitaires**
* Dans le tableau **`Consolidated Digital Ad Spend`**
* Cette mesure effectue une **Somme**
* Dans la colonne **`adClicks`**
* Classé par l’horodatage **`Month`**

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Rapports

* **Dépenses publicitaires (tout le temps)**
   * [!UICONTROL Metric] : dépenses publicitaires

* `A` de mesure : dépenses publicitaires
* [!UICONTROL Time period] : `All time`
* 
  [!UICONTROL Intervalle]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **Ajouter des acquisitions de clients (à tout moment)**
   * [!UICONTROL Metric] : `New customers`
   * [!UICONTROL Filters] :
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logique de filtre : ([`A`] OU [`B`] OU [`C`]) ET [`D`]

* `A` de mesure : `Ad customer acquisitions`
* [!UICONTROL Time period] : `All time`
* 
  [!UICONTROL Intervalle]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **Ajouter un retour sur investissement**
   * [!UICONTROL Metric] : dépenses publicitaires

   * [!UICONTROL Metric] : `New customers`
   * [!UICONTROL Filters] :
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logique de filtre : ([`A`] OU [`B`] OU [`C`]) ET [`D`]

   * [!UICONTROL Metric] : revenu moyen sur la durée de vie
   * [!UICONTROL Filters] :
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logique de filtre : ([`A`] OU [`B`] OU [`C`]) ET [`D`]

   * [!UICONTROL Formula] : `((C - (A / B)) / (A / B))`
   * 
     [!UICONTROL Format]: `Percentage`

* `A` de mesure : `Ad Spend (hide)`
* `B` de mesure : `Ad customer acquisitions (hide)`
* `C` de mesure : `Average LTV (hide)`
* [!UICONTROL Formula] : `Ads ROI`
* [!UICONTROL Time period] : `All time`
* 
  [!UICONTROL Intervalle]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **Commandes par support ga**
   * 
     [!UICONTROL Metric]: `Orders`

* `A` de mesure : `Orders`
* [!UICONTROL Time period] : `All time`
* [!UICONTROL Interval] : `By Month`
* [!UICONTROL Group by] : `Order's medium`
* 
  [!UICONTROL Chart Type]: `Area`

* **Retour sur investissement publicitaire par campagne**
   * [!UICONTROL Metric] : `Ad Spend`

   * [!UICONTROL Metric]:`New customers`
   * [!UICONTROL Filters] :
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logique de filtre : ([`A`] OU [`B`] OU [`C`]) ET [`D`]

   * [!UICONTROL Metric] : revenu moyen sur la durée de vie
   * [!UICONTROL Filters] :
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logique de filtre : ([`A`] OU [`B`] OU [`C`]) ET [`D`]

   * [!UICONTROL Metric] : nombre moyen de commandes au cours de la durée de vie
   * [!UICONTROL Filters] :
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logique de filtre : ([`A`] OU [`B`] OU [`C`]) ET [`D`]

   * [!UICONTROL Formula] : `(A / B)`
   * 
     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula] : `(C - (A / B))`
   * 
     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula] : `((C - (A / B)) / (A / B))`
   * 
     [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Metric] : `Ad Clicks`

   * [!UICONTROL Metric] : `Ad Impressions`

   * [!UICONTROL Formula] : `(H / I)`
   * 
     [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Formula] : `(A / H)`
   * 
     [!UICONTROL Format]: `Currency`

* `A` de mesure : `Ad Spend` (masquer)
* `B` de mesure : `Ad customer acquisitions`
* `C` de mesure : `Average LTV`
* `D` de mesure : `Average lifetime # of orders`
* 
  [!UICONTROL Formule]: `CAC`
* [!UICONTROL Formula] : `Avg return`
* [!UICONTROL Formula] : `Ads ROI`
* `H` de mesure : `adClicks`
* `I` de mesure : `Impressions`
* 
  [!UICONTROL Formule]: `CTR`
* 
  [!UICONTROL Formule]: `CPC`
* [!UICONTROL Time period] : `All time`
* 
  [!UICONTROL Intervalle]: `None`
* 
  [!UICONTROL Regrouper par]: `campaign` (Utiliser la campagne « Première commande du client » pour les mesures du tableau des dépenses non publicitaires)
* 
  [!UICONTROL Chart Type]: `Table`

Si vous avez des questions lors de la création de cette analyse ou si vous souhaitez simplement contacter l’équipe des services professionnels, [contactez l’assistance ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

### Connexe

* [Bonnes pratiques relatives au balisage UTM dans  [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [Comment fonctionne  [!DNL Google Analytics] ’attribution UTM ?](../analysis/utm-attributes.md)
