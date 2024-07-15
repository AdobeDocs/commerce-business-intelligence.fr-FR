---
title: ROI marketing
description: Découvrez comment configurer un tableau de bord qui effectue le suivi de l’analyse de vos canaux, y compris le retour sur investissement dans l’agrégat et par campagne.
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
role: Admin,  User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# ROI marketing

>[!NOTE]
>
>Cette rubrique contient des instructions destinées aux clients qui utilisent l’architecture d’origine et la nouvelle architecture. Vous vous trouvez sur la [nouvelle architecture](../../administrator/account-management/new-architecture.md) si la section &quot;Data Warehouse Views&quot; est disponible après avoir sélectionné &quot;Manage Data&quot; (Gérer les données) dans la barre d’outils principale.

Si vous dépensez de l’argent dans la publicité en ligne, vous souhaitez suivre votre retour sur cette dépense et prendre des décisions basées sur les données sur d’autres investissements. Cette rubrique explique comment configurer un tableau de bord qui effectue le suivi de l’analyse de vos canaux, y compris le retour sur investissement agrégé et par campagne.

![](../../assets/Marketing_dashboard_example.png)

Avant de commencer, vous souhaitez connecter vos comptes [!DNL [Facebook Ads]](../importing-data/integrations/facebook-ads.md), [!DNL [Adwords]](../importing-data/integrations/google-adwords.md) et [!DNL [Google Ecommerce]](../importing-data/integrations/google-ecommerce.md) et importer toutes les données supplémentaires de dépenses publicitaires en ligne. Cette analyse contient [des colonnes calculées avancées](../data-warehouse-mgr/adv-calc-columns.md).

## Tables consolidées

**Architecture d&#39;origine :** Pour rassembler vos dépenses provenant de diverses sources, telles que [!DNL Facebook Ads] ou [!DNL Google Adwords], Adobe recommande de créer une **table consolidée** de toutes vos dépenses publicitaires. Pour vous, un analyste est nécessaire. Si ce n&#39;est pas le cas, [envoyez une demande d&#39;assistance](../../guide-overview.md#Submitting-a-Support-Ticket) avec l&#39;objet `[MARKETING ROI ANALYSIS]`, et un analyste crée cette table.

**Nouvelle architecture :** Vous pouvez suivre l’exemple de la rubrique [cette bibliothèque d’analyses](../../data-analyst/data-warehouse-mgr/create-dw-views.md). Les tableaux consolidés sont désormais appelés vues Data Warehouse sur la nouvelle architecture.

## Colonnes calculées

Colonnes à créer

* **`Consolidated Digital Ad Spend`** table
* **`Campaign name`** est créé par un analyste d’Adobe dans le cadre de votre ticket **[ANALYSE DU ROI MARKETING]**

**Architectures originales et nouvelles :**

* **`sales_flat_order`** table
   * **`Order's GA campaign`**
      * Sélectionnez une définition : `Joined Column`
      * [!UICONTROL Create Path] :
      * 
        [!UICONTROL Many]: `sales_flat_order.increment_id`
      * 
        [!UICONTROL One]: `ecommerce####.transaction_id`

      * Sélectionnez un [!UICONTROL table] : `ecommerce####`
      * Sélectionnez un [!UICONTROL column] : `campaign`
      * [!UICONTROL Path] : `sales_flat_order.increment_id = ecommerce#####.transactionID`

   * **`Order's GA medium`**
      * Sélectionner une définition : Colonne jointe
      * Sélectionnez un [!UICONTROL table] : `ecommerce####`
      * Sélectionnez un [!UICONTROL column] : `medium`
      * [!UICONTROL Path] : sales_plat_order.incrément_id = ecommerce####.transactionId

   * **`Order's GA source`**
      * Sélectionner une définition : Colonne jointe
      * Sélectionnez un [!UICONTROL table] : `ecommerce####`
      * Sélectionnez un [!UICONTROL column] : `source`
      * [!UICONTROL Path] : sales_plat_order.incrément_id = ecommerce####.transactionId
^

* **`customer_entity`** table
* **`Customer's first order GA campaign`**
   * Sélectionnez une définition : `Max`
   * Sélectionnez un [!UICONTROL table] : `sales_flat_order`
   * Sélectionnez un [!UICONTROL column] : `Order's GA campaign`
   * [!UICONTROL Path] : `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter] :
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA source`**
   * Sélectionnez une définition : `Max`
   * Sélectionnez un [!UICONTROL table] : `sales_flat_order`
   * Sélectionnez un [!UICONTROL column] : `Order's GA source`
   * [!UICONTROL Path] : sales_plat_order.customer_id = customer_entity.entity_id
   * [!UICONTROL Filter] :
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA medium`**
   * Sélectionnez une définition : `Max`
   * Sélectionnez un [!UICONTROL table] : `sales_flat_order`
   * Sélectionnez un [!UICONTROL column] : `Order's GA medium`
   * [!UICONTROL Path] : `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter] :
      * `Orders we count`
      * `Customer's order number = 1`

* **`sales_flat_order`** table
* **`Customer's first order GA campaign`**
   * Sélectionnez une définition : `Joined Column`
   * Sélectionnez un [!UICONTROL table] : `customer_entity`
   * Sélectionnez un [!UICONTROL column] : `Customer's first order GA campaign`
   * [!UICONTROL Path] : `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
   * Sélectionner une définition : Colonne jointe
   * Sélectionnez un [!UICONTROL table] : `customer_entity`
   * Sélectionnez un [!UICONTROL column] : `Customer's first order GA source`
   * [!UICONTROL Path] : `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
   * Sélectionnez une définition : `Joined Column`
   * Sélectionnez un [!UICONTROL table] : `customer_entity`
   * Sélectionnez un [!UICONTROL column] : `Customer's first order GA medium`
   * [!UICONTROL Path] : `sales_flat_order.customer_id = customer_entity.entity_id`

## Mesures

* **Dépense publicitaire**
* Dans la table **`Consolidated Digital Ad Spend`**
* Cette mesure exécute une **Somme**
* Sur la colonne **`adCost`**
* Ordonné par l’horodatage **`date`**

* **Impressions de publicité**
* Dans la table **`Consolidated Digital Ad Spend`**
* Cette mesure exécute une **Somme**
* Sur la colonne **`Impressions`**
* Ordonné par l’horodatage **`Month`**

* **Clics publicitaires**
* Dans la table **`Consolidated Digital Ad Spend`**
* Cette mesure exécute une **Somme**
* Sur la colonne **`adClicks`**
* Ordonné par l’horodatage **`Month`**

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Rapports

* **Dépenses publicitaires (tout le temps)**
   * [!UICONTROL Metric] : dépenses publicitaires

* Mesure `A` : dépenses publicitaires
* [!UICONTROL Time period] : `All time`
* 
  [!UICONTROL Intervalle]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **Ajoutez des acquisitions de clients (tout le temps)**
   * [!UICONTROL Metric] : `New customers`
   * [!UICONTROL Filters] :
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logique de filtre : ([`A`] OU [`B`] OU [`C`]) ET [`D`]

* Mesure `A` : `Ad customer acquisitions`
* [!UICONTROL Time period] : `All time`
* 
  [!UICONTROL Intervalle]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **ROI publicitaire**
   * [!UICONTROL Metric] : dépenses publicitaires

   * [!UICONTROL Metric] : `New customers`
   * [!UICONTROL Filters] :
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logique de filtre : ([`A`] OU [`B`] OU [`C`]) ET [`D`]

   * [!UICONTROL Metric] : Chiffre d’affaires moyen de la durée de vie
   * [!UICONTROL Filters] :
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logique de filtre : ([`A`] OU [`B`] OU [`C`]) ET [`D`]

   * [!UICONTROL Formula] : `((C - (A / B)) / (A / B))`
   * 
     [!UICONTROL Format]: `Percentage`

* Mesure `A` : `Ad Spend (hide)`
* Mesure `B` : `Ad customer acquisitions (hide)`
* Mesure `C` : `Average LTV (hide)`
* [!UICONTROL Formula] : `Ads ROI`
* [!UICONTROL Time period] : `All time`
* 
  [!UICONTROL Intervalle]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **Commandes par ga medium**
   * 
     [!UICONTROL Mesure]: `Orders`

* Mesure `A` : `Orders`
* [!UICONTROL Time period] : `All time`
* [!UICONTROL Interval] : `By Month`
* [!UICONTROL Group by] : `Order's medium`
* 
  [!UICONTROL Chart Type]: `Area`

* **ROI publicitaire par campagne**
   * [!UICONTROL Metric] : `Ad Spend`

   * [!UICONTROL Metric]:`New customers`
   * [!UICONTROL Filters] :
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logique de filtre : ([`A`] OU [`B`] OU [`C`]) ET [`D`]

   * [!UICONTROL Metric] : Chiffre d’affaires moyen de la durée de vie
   * [!UICONTROL Filters] :
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logique de filtre : ([`A`] OU [`B`] OU [`C`]) ET [`D`]

   * [!UICONTROL Metric] : Nombre moyen de commandes pendant la durée de vie
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

* Mesure `A` : `Ad Spend` (masquer)
* Mesure `B` : `Ad customer acquisitions`
* Mesure `C` : `Average LTV`
* Mesure `D` : `Average lifetime # of orders`
* 
  [!UICONTROL Formule]: `CAC`
* [!UICONTROL Formula] : `Avg return`
* [!UICONTROL Formula] : `Ads ROI`
* Mesure `H` : `adClicks`
* Mesure `I` : `Impressions`
* 
  [!UICONTROL Formule]: `CTR`
* 
  [!UICONTROL Formule]: `CPC`
* [!UICONTROL Time period] : `All time`
* 
  [!UICONTROL Intervalle]: `None`
* 
  [!UICONTROL Groupe par]: `campaign` (Utiliser la campagne &quot;Première commande du client&quot; pour les mesures de tableau de dépenses non publicitaires)
* 
  [!UICONTROL Chart Type]: `Table`

Si vous rencontrez des questions lors de la création de cette analyse ou si vous souhaitez simplement contacter l’équipe des services professionnels, [contactez l’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

### Associé

* [Bonnes pratiques relatives au balisage UTM dans [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [Comment fonctionne l’attribution de [!DNL Google Analytics] UTM ?](../analysis/utm-attributes.md)
