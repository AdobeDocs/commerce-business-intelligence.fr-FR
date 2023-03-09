---
title: ROI marketing
description: Découvrez comment configurer un tableau de bord qui effectue le suivi de l’analyse de vos canaux, y compris le retour sur investissement dans l’agrégat et par campagne.
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# ROI marketing

>[!NOTE]
>
>Cet article contient des instructions destinées aux clients qui utilisent l’architecture d’origine et la nouvelle architecture. Vous êtes sur la [nouvelle architecture](../../administrator/account-management/new-architecture.md) Si la section &quot;Vues Data Warehouse&quot; est disponible après avoir sélectionné &quot;Gérer les données&quot; dans la barre d’outils principale.

Si vous dépensez de l’argent dans la publicité en ligne, vous souhaitez suivre votre retour sur cette dépense et prendre des décisions basées sur les données sur d’autres investissements. Cet article explique comment configurer un tableau de bord qui effectue le suivi de l’analyse de vos canaux, y compris le retour sur investissement agrégé et par campagne.

![](../../assets/Marketing_dashboard_example.png)

Avant de commencer, vous souhaitez connecter votre [!DNL [Facebook Ads]](../importing-data/integrations/facebook-ads.md), [!DNL [Adwords]](../importing-data/integrations/google-adwords.md), et [!DNL [Google Ecommerce]](../importing-data/integrations/google-ecommerce.md) et d’importer toutes les données supplémentaires relatives aux dépenses publicitaires en ligne. Cette analyse contient [colonnes calculées avancées](../data-warehouse-mgr/adv-calc-columns.md).

## Tables consolidées

**Architecture originale :** Pour rassembler vos dépenses à partir de diverses sources (comme [!DNL Facebook Ads] ou [!DNL Google Adwords]), Adobe recommande de créer une **table consolidée** de toutes vos dépenses publicitaires. Pour vous, un analyste est nécessaire. Si ce n’est pas le cas, [enregistrer une demande d’assistance ;](../../guide-overview.md) avec le sujet `[MARKETING ROI ANALYSIS]`et un analyste crée ce tableau.

**Nouvelle architecture :** Vous pouvez suivre l’exemple de la section [cette bibliothèque d’analyses](../../data-analyst/data-warehouse-mgr/create-dw-views.md) rubrique. Les tableaux consolidés sont désormais appelés vues Data Warehouse sur la nouvelle architecture.

## Colonnes calculées

Colonnes à créer

* **`Consolidated Digital Ad Spend`** table
* **`Campaign name`** est créé par un analyste dans le cadre de votre **[ANALYSE DU ROI MARKETING]** ticket

>[!NOTE]
>
>Voir ci-dessus pour connaître les nouvelles différences d’architecture.

**Architectures originales et nouvelles :**

* **`sales_flat_order`** table
   * **`Order's GA campaign`**
      * Sélectionnez une définition : `Joined Column`
      * [!UICONTROL Create Path]:
      * 
         [!UICONTROL Many]: `sales_flat_order.increment_id`
      * 

         [!UICONTROL One]: `ecommerce####.transaction_id`

      * Sélectionnez une [!UICONTROL table]: `ecommerce####`
      * Sélectionnez une [!UICONTROL column]: `campaign`
      * [!UICONTROL Path]: `sales_flat_order.increment_id = ecommerce#####.transactionID`
   * **`Order's GA medium`**
      * Sélectionnez une définition : Colonne jointe
      * Sélectionnez une [!UICONTROL table]: `ecommerce####`
      * Sélectionnez une [!UICONTROL column]: `medium`
      * [!UICONTROL Path]: sales_plat_order.incrément_id = ecommerce####.transactionId
   * **`Order's GA source`**
      * Sélectionnez une définition : Colonne jointe
      * Sélectionnez une [!UICONTROL table]: `ecommerce####`
      * Sélectionnez une [!UICONTROL column]: `source`
      * [!UICONTROL Path]: sales_plat_order.incrément_id = ecommerce#####.transactionId ^




* **`customer_entity`** table
* **`Customer's first order GA campaign`**
   * Sélectionnez une définition : `Max`
   * Sélectionnez une [!UICONTROL table]: `sales_flat_order`
   * Sélectionnez une [!UICONTROL column]: `Order's GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA source`**
   * Sélectionnez une définition : `Max`
   * Sélectionnez une [!UICONTROL table]: `sales_flat_order`
   * Sélectionnez une [!UICONTROL column]: `Order's GA source`
   * [!UICONTROL Path]: sales_plat_order.customer_id = customer_entity.entity_id
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA medium`**
   * Sélectionnez une définition : `Max`
   * Sélectionnez une [!UICONTROL table]: `sales_flat_order`
   * Sélectionnez une [!UICONTROL column]: `Order's GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`sales_flat_order`** table
* **`Customer's first order GA campaign`**
   * Sélectionnez une définition : `Joined Column`
   * Sélectionnez une [!UICONTROL table]: `customer_entity`
   * Sélectionnez une [!UICONTROL column]: `Customer's first order GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
   * Sélectionnez une définition : Colonne jointe
   * Sélectionnez une [!UICONTROL table]: `customer_entity`
   * Sélectionnez une [!UICONTROL column]: `Customer's first order GA source`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
   * Sélectionnez une définition : `Joined Column`
   * Sélectionnez une [!UICONTROL table]: `customer_entity`
   * Sélectionnez une [!UICONTROL column]: `Customer's first order GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

## Mesures

* **Dépenses publicitaires**
* Dans le **`Consolidated Digital Ad Spend`** table
* Cette mesure effectue une **Somme**
* Sur le **`adCost`** column
* Commandé par le **`date`** timestamp

* **Impressions publicitaires**
* Dans le **`Consolidated Digital Ad Spend`** table
* Cette mesure effectue une **Somme**
* Sur le **`Impressions`** column
* Commandé par le **`Month`** timestamp

* **Clics publicitaires**
* Dans le **`Consolidated Digital Ad Spend`** table
* Cette mesure effectue une **Somme**
* Sur le **`adClicks`** column
* Commandé par le **`Month`** timestamp

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures ;](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Rapports

* **Dépense publicitaire (tout le temps)**
   * [!UICONTROL Metric]: Dépenses publicitaires

* Mesure `A`: Dépenses publicitaires
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalle]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **Acquisitions des clients des publicités (tout le temps)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logique de filtre : ([`A`] OU [`B`] OU [`C`]) ET [`D`]

* Mesure `A`: `Ad customer acquisitions`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalle]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **ROI publicitaire**
   * [!UICONTROL Metric]: Dépenses publicitaires

   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logique de filtre : ([`A`] OU [`B`] OU [`C`]) ET [`D`]
   * [!UICONTROL Metric]: Chiffre d’affaires moyen
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logique de filtre : ([`A`] OU [`B`] OU [`C`]) ET [`D`]
   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 

      [!UICONTROL Format]: `Percentage`



* Mesure `A`: `Ad Spend (hide)`
* Mesure `B`: `Ad customer acquisitions (hide)`
* Mesure `C`: `Average LTV (hide)`
* [!UICONTROL Formula]: `Ads ROI`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalle]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **Commandes par ga moyen**
   * 

      [!UICONTROL Mesure]: `Orders`

* Mesure `A`: `Orders`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Order's medium`
* 

   [!UICONTROL Chart Type]: `Area`

* **RSI de la publicité par campagne**
   * [!UICONTROL Metric]: `Ad Spend`

   * [!UICONTROL Metric]:`New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logique de filtre : ([`A`] OU [`B`] OU [`C`]) ET [`D`]
   * [!UICONTROL Metric]: Chiffre d’affaires moyen
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logique de filtre : ([`A`] OU [`B`] OU [`C`]) ET [`D`]
   * [!UICONTROL Metric]: Durée de vie moyenne des commandes
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logique de filtre : ([`A`] OU [`B`] OU [`C`]) ET [`D`]
   * [!UICONTROL Formula]: `(A / B)`
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `(C - (A / B))`
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 

      [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Metric]: `Ad Clicks`

   * [!UICONTROL Metric]: `Ad Impressions`

   * [!UICONTROL Formula]: `(H / I)`
   * 

      [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Formula]: `(A / H)`
   * 

      [!UICONTROL Format]: `Currency`




* Mesure `A`: `Ad Spend` (masquer)
* Mesure `B`: `Ad customer acquisitions`
* Mesure `C`: `Average LTV`
* Mesure `D`: `Average lifetime # of orders`
* 
   [!UICONTROL Formule]: `CAC`
* [!UICONTROL Formula]: `Avg return`
* [!UICONTROL Formula]: `Ads ROI`
* Mesure `H`: `adClicks`
* Mesure `I`: `Impressions`
* 
   [!UICONTROL Formule]: `CTR`
* 
   [!UICONTROL Formule]: `CPC`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalle]: `None`
* 
   [!UICONTROL Groupe par]: `campaign` (Utiliser la campagne &quot;Première commande du client&quot; pour les mesures de tableau de dépenses non publicitaires)
* 

   [!UICONTROL Chart Type]: `Table`

Si vous rencontrez des questions lors de la création de cette analyse ou si vous souhaitez simplement faire appel à l&#39;équipe des services professionnels, [support technique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

### Associé

* [Bonnes pratiques relatives au balisage UTM dans [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [Comment [!DNL Google Analytics] Fonctionnement de l’attribution UTM ?](../analysis/utm-attributes.md)
