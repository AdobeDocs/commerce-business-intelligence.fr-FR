---
title: Retour sur investissement marketing
description: Découvrez comment configurer un tableau de bord qui effectue le suivi de votre analyse des canaux, y compris le retour sur investissement global et par campagne.
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
role: Admin,  User
feature: Reports, Dashboards
TQID: https://experienceleague.adobe.com/TJ0KsU551M5PkQcY-Ic0PuExtC9SCkO0MhZGdHL4N6g
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 529
ht-degree: 0%

---

# Retour sur investissement marketing

>[!NOTE]
>
>Cette rubrique contient des instructions pour les clients qui utilisent l’architecture d’origine et la nouvelle architecture. Vous passez à la [nouvelle architecture](../../administrator/account-management/new-architecture.md) si la section « Vues Data Warehouse » est disponible après avoir sélectionné « Gérer les données » dans la barre d’outils principale.

Si vous dépensez de l&#39;argent dans la publicité en ligne, vous voulez suivre le rendement de ces dépenses et prendre des décisions fondées sur des données pour d&#39;autres investissements. Cette rubrique explique comment configurer un tableau de bord qui effectue le suivi de votre analyse des canaux, y compris le retour sur investissement global et par campagne.

![Tableau de bord marketing présentant les mesures de RSI et les performances des campagnes](../../assets/Marketing_dashboard_example.png)

Avant de commencer, vous devez connecter vos comptes [[!DNL [Facebook Ads]]](../importing-data/integrations/facebook-ads.md), [[!DNL [Adwords]]](../importing-data/integrations/google-adwords.md) et [[!DNL [Google Ecommerce]]](../importing-data/integrations/google-ecommerce.md) et importer des données supplémentaires sur les dépenses publicitaires en ligne. Cette analyse contient [colonnes calculées avancées](../data-warehouse-mgr/adv-calc-columns.md).

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
      * &#x200B;
        [!UICONTROL Many]: `sales_flat_order.increment_id`
      * &#x200B;
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
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* &#x200B;
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
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* &#x200B;
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
   * &#x200B;
     [!UICONTROL Format]: `Percentage`

* `A` de mesure : `Ad Spend (hide)`
* `B` de mesure : `Ad customer acquisitions (hide)`
* `C` de mesure : `Average LTV (hide)`
* [!UICONTROL Formula] : `Ads ROI`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`

* **Commandes par support ga**
   * &#x200B;
     [!UICONTROL Metric]: `Orders`

* `A` de mesure : `Orders`
* [!UICONTROL Time period] : `All time`
* [!UICONTROL Interval] : `By Month`
* [!UICONTROL Group by] : `Order's medium`
* &#x200B;
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
   * &#x200B;
     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula] : `(C - (A / B))`
   * &#x200B;
     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula] : `((C - (A / B)) / (A / B))`
   * &#x200B;
     [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Metric] : `Ad Clicks`

   * [!UICONTROL Metric] : `Ad Impressions`

   * [!UICONTROL Formula] : `(H / I)`
   * &#x200B;
     [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Formula] : `(A / H)`
   * &#x200B;
     [!UICONTROL Format]: `Currency`

* `A` de mesure : `Ad Spend` (masquer)
* `B` de mesure : `Ad customer acquisitions`
* `C` de mesure : `Average LTV`
* `D` de mesure : `Average lifetime # of orders`
* &#x200B;
  [!UICONTROL Formule]: `CAC`
* [!UICONTROL Formula] : `Avg return`
* [!UICONTROL Formula] : `Ads ROI`
* `H` de mesure : `adClicks`
* `I` de mesure : `Impressions`
* &#x200B;
  [!UICONTROL Formule]: `CTR`
* &#x200B;
  [!UICONTROL Formule]: `CPC`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* &#x200B;
  [!UICONTROL Regrouper par]: `campaign` (Utiliser la campagne « Première commande du client » pour les mesures du tableau des dépenses non publicitaires)
* &#x200B;
  [!UICONTROL Chart Type]: `Table`

Si vous avez des questions lors de la création de cette analyse ou si vous souhaitez simplement contacter l’équipe des services professionnels, [contactez l’assistance &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

### Connexe

* [Bonnes pratiques relatives au balisage UTM dans  [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [Comment fonctionne  [!DNL Google Analytics] ’attribution UTM ?](../analysis/utm-attributes.md)
