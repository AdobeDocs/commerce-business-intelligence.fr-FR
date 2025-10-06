---
title: Performance des coupons
description: Découvrez comment analyser les performances de votre coupon.
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1243'
ht-degree: 0%

---

# Analyse avancée du code de coupon

Comprendre le rendement des coupons de votre entreprise est une façon intéressante de segmenter vos commandes et de mieux comprendre vos clients. Cette rubrique vous guide à travers les étapes pour créer des analyses afin de comprendre quels clients vous achetez à l’aide de coupons, comment ils se comportent et de suivre l’utilisation générale des coupons.

![Analyse du code promotionnel de la bibliothèque d’analyse présentant les mesures clés](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

Cette analyse contient [colonnes calculées avancées](../data-warehouse-mgr/adv-calc-columns.md).

## Prise en main

Pour commencer, vous devez vous assurer que les colonnes ci-dessous sont synchronisées avec votre Data Warehouse. Si ce n’est pas le cas, effectuez leur suivi en accédant à `Manage Data` > `Data Warehouse` et en synchronisant les éléments suivants :

* table **sales\_flat\_order**
* **coupon\_code**
* **base\_discount\_amount**

## Colonnes calculées

Colonnes à créer, quelle que soit la politique de commandes des invités :

* `sales\_flat\_order` table
* **La commande a-t-elle appliqué un coupon ?**
   * [!UICONTROL Column type] : `Same Table => CALCULATION`
   * [!UICONTROL Inputs] :
      * `A` : `coupon\_code`

   * &#x200B;
     [!UICONTROL , type de données]: `String`
   * [!UICONTROL Calculation] : casse lorsque la `A` est nulle, `No coupon` sinon `Coupon` fin

* **\[INPUT\] customer\_id - code de coupon**
   * [!UICONTROL Column type] : `Same Table => CALCULATION`
   * [!UICONTROL Inputs] :
      * `A` : `customer\_id`
      * `B` : `coupon\_code`

   * Chaîne [!UICONTROL Datatype]
   * [!UICONTROL Calculation] : `concat(A,' - ',B)`

* **Nombre de commandes avec ce coupon**
   * [!UICONTROL Column type] : `Same Table => EVENT\_NUMBER`
   * Propriétaire de l’événement :`INPUT customer_id - coupon code`
   * Classement des événements : `created\_at`
   * [!UICONTROL Filters] : jeu `Orders we count` filtres

Colonnes supplémentaires à créer si les commandes de produits invités NE sont PAS prises en charge :

* `customer\_entity` table
   * **La première commande du client comportait un coupon ? (Coupon/Pas de coupon)**
   * [!UICONTROL Column type] : `Many to One => MAX`
   * [!UICONTROL Path] : `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
   * Sélectionner un [!UICONTROL column] : `Order has coupon applied? (Coupon/No coupon)`
   * [!UICONTROL Filters] :
      * `A` : `Orders we count`
      * `B` : `Customer's order number = 1`

   * **Bon de première commande du client**
      * [!UICONTROL Column type] : `Many to One => MAX`
      * [!UICONTROL Path] : `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Sélectionner un [!UICONTROL column] : `coupon\_code`
      * [!UICONTROL Filter] :
         * `A` : `Orders we count`
         * `B` : `Customer's order number = 1`

   * **Nombre de coupons utilisés au cours de la durée de vie du client**
      * [!UICONTROL Column type] : `Many to One => COUNT`
      * [!UICONTROL Path] : `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter] :
         * `A` : `Orders we count`
         * `B` : `Order has coupon applied? (Coupon/No coupon) = Coupon`

   * **Client d’acquisition de coupon ou Client d’acquisition hors coupon**
      * [!UICONTROL Column type] : `Same Table => CALCULATION`
      * [!UICONTROL Inputs] :
         * `A` : `Customer's first order included a coupon? (Coupon/No coupon)`

      * &#x200B;
        [!UICONTROL , type de données]: `String`
      * [!UICONTROL Calculation] : **cas où A=&#39;Coupon&#39; puis &#39;Client acquisition de coupon&#39; sinon &#39;Client acquisition hors coupon&#39; fin**

   * **Pourcentage des commandes client avec coupon**
      * [!UICONTROL Column type] : `Same Table => CALCULATION`
      * [!UICONTROL Inputs] :
         * `A` : `User's lifetime number of coupons used`
         * `B` : `User's lifetime number of orders`

      * &#x200B;
        [!UICONTROL , type de données]: `Decimal`
      * [!UICONTROL Calculation] : **cas où A est nul ou B est nul ou B=0 puis null Autrement extrémité A/B**

   * **Utilisation des coupons du client**
      * [!UICONTROL Column type] : `Same Table => Calculation`
      * [!UICONTROL Inputs] :
         * `A` : `Percent of customer's orders with coupon`

      * &#x200B;
        [!UICONTROL , type de données]: `String`
      * [!UICONTROL Calculation] : **cas où A est nul puis nul quand A=0 puis &#39;Coupon jamais utilisé&#39; quand A&lt;0.5 puis &#39;Prix majoritairement complet&#39; quand A=0.5 puis &#39;50/50&#39; quand A=1 puis &#39;Coupons seulement&#39; quand A>0.5 puis &#39;Coupon majoritaire&#39; sinon fin &#39;Non défini&#39;**

* `sales\_flat\_order` table
   * **La première commande du client incluait un coupon ? (Coupon/Pas de coupon)**
      * [!UICONTROL Column type] : `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path] : `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Sélectionner un [!UICONTROL column] : `Customer's first order included a coupon? (Coupon/No coupon)`
^

   * **Bon de première commande du client**
      * [!UICONTROL Column type] : `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path] : `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Sélectionner un [!UICONTROL column] : `Customer's first order coupon?`

Colonnes supplémentaires à créer si les commandes de produits invités NE sont PAS prises en charge :

* `sales\_flat\_order` table
   * **La première commande du client comportait un coupon ? (Coupon/Pas de coupon)** **-** créé par l’analyste dans le cadre de votre ticket \[COUPON ANALYSIS\]
   * **&#x200B;**{::}**-** du coupon de la première commande du client créé par l’analyste dans le cadre de votre ticket \[ANALYSE DES COUPONS\]

* **Nombre à vie du client de coupons utilisés &#x200B;**{::}**-** créés par l’analyste dans le cadre de votre ticket \[ANALYSE DES COUPONS\]
* **Client d’acquisition de coupon ou Client d’acquisition hors coupon**
   * [!UICONTROL Column type] : `Same Table => CALCULATION`
   * [!UICONTROL Inputs] :
      * `A` : `Customer's first order included a coupon? (Coupon/No coupon)`

   * &#x200B;
     [!UICONTROL , type de données]: `String`
   * [!UICONTROL Calculation] : **cas où A=&#39;Coupon&#39; puis &#39;Client acquisition de coupon&#39; sinon &#39;Client acquisition hors coupon&#39; fin**

* **Pourcentage des commandes client avec coupon**
   * [!UICONTROL Column type] : `Same Table => CALCULATION`
   * [!UICONTROL Inputs] :
      * `A` : `User's lifetime number of coupons used`
      * `B` : `User's lifetime number of orders`

   * &#x200B;
     [!UICONTROL , type de données]: `Decimal`
   * [!UICONTROL Calculation] : **cas où A est nul ou B est nul ou B=0 puis null Autrement extrémité A/B**

* **Utilisation des coupons du client**
   * [!UICONTROL Column type] : `Same Table => Calculation`
   * [!UICONTROL Inputs] :
      * `A` : `Percent of customer's orders with coupon`

   * &#x200B;
     [!UICONTROL , type de données]: `String`
   * [!UICONTROL Calculation] : **cas où A est nul puis nul quand A=0 puis &#39;Coupon jamais utilisé&#39; quand A&lt;0.5 puis &#39;Prix majoritairement complet&#39; quand A=0.5 puis &#39;50/50&#39; quand A=1 puis &#39;Coupons seulement&#39; quand A>0.5 puis &#39;Coupon majoritaire&#39; sinon fin &#39;Non défini&#39;**

## Mesures

* **Montant de la remise du coupon**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* Dans le tableau `sales\_flat\_order`
* Cette mesure effectue une **Somme**
* Dans la colonne `discount\_amount`
* Classé par l’horodatage `created\_at`
* [!UICONTROL Filter] :

* **Nombre de coupons utilisés**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* Dans le tableau `sales\_flat\_order`
* Cette mesure effectue un **Nombre**
* Dans la colonne `entity\_id`
* Classé par l’horodatage `created\_at`
* [!UICONTROL Filter] :

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Rapports

* **% des clients avec ou sans coupon**
   * [!UICONTROL Metric] : `New customers`

* `A` de mesure : `Coupon acquisitions`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by] : `Coupon acquisitions customer` ou `Non coupon acquisition customer`
* &#x200B;
  [!UICONTROL Type de graphique]: `Pie`

* **Nombre de clients avec et sans coupon**
   * [!UICONTROL Metric] : `New customers`

* Mesure A : `Coupon acquisitions`
* [!UICONTROL Time period] : `All time`
* [!UICONTROL Interval] : `By Month`
* [!UICONTROL Group by] : `Coupon acquisitions customer` ou `Non coupon acquisition customer`
* [!UICONTROL Chart type] : `Stacked column`

* **Chiffre d’affaires moyen sur la durée de vie : coupon Acq. (90 ans et plus)**
   * [!UICONTROL Metric] : `Average lifetime revenue`
   * [!UICONTROL Filter] :
      * La première commande du client incluait un coupon (coupon/sans coupon) = coupon

* `A` de mesure : `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period] : `X years ago to 90 days ago`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* &#x200B;
  [!UICONTROL Type de graphique]: `Scalar`

* **Chiffre d’affaires moyen sur la durée de vie : Acq. non coupon. (90 ans et plus)**
   * [!UICONTROL Metric] : revenu moyen sur la durée de vie
   * [!UICONTROL Filter] :
      * La première commande du client incluait un coupon (Coupon/Aucun coupon) = Aucun coupon

* `A` de mesure : `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period] : `X years ago to 90 days ago`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* &#x200B;
  [!UICONTROL Type de graphique]: `Scalar`

* **Chiffre d’affaires moyen sur la durée de vie par coupon de première commande**
   * [!UICONTROL Metric] : `Average lifetime revenue`

* `A` de mesure : `Average lifetime revenue`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by] : `Customer's first order's coupon`
* &#x200B;
  [!UICONTROL Type de graphique]: `Column`

>[!NOTE]
>
>Si vous disposez de nombreux codes de coupon, comme le font de nombreux clients, vous devez appliquer un classement Haut/Bas tel que Top 10 trié par Revenu moyen sur la durée de vie

* **Probabilité de commande répétée : acquisitions de coupons**
   * [!UICONTROL Metric] : `Number of orders`
   * [!UICONTROL Filter] :
      * La première commande du client incluait un coupon (coupon/sans coupon) = coupon

   * [!UICONTROL Metric] : `Number of orders`
   * [!UICONTROL Filter] :
      * La première commande du client incluait un coupon (coupon/sans coupon) = coupon
      * Est la dernière commande du client ? = Non
   * &#x200B;
     [!UICONTROL Formule]: `B/A`
   * [!UICONTROL Format] : `Percentage %`

   * Sélectionnez un nombre statistiquement significatif dans `Customer's by lifetime orders` graphique. Lorsque vous examinez le graphique, il est recommandé de rechercher les numéros de commande avec 30 clients ou plus dans l’intervalle. En fonction de votre jeu de données, il peut s’agir d’un grand nombre. N’hésitez donc pas à ajouter 1 à 10.

* `A` de mesure : `Number of orders`
* `B` de mesure : `Number of non last orders`
* [!UICONTROL Formula] : `Repeat order probability`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by] : `Customer's order number`
* [!UICONTROL Chart type] : `Bar chart`

* **Probabilité de commande répétée : acquisitions hors coupon**
   * [!UICONTROL Metric] : `Number of orders`
   * [!UICONTROL Filter] :
      * La première commande du client incluait un coupon (coupon/sans coupon) = Aucun coupon

   * [!UICONTROL Metric] : `Number of orders`
   * [!UICONTROL Filter] :
      * La première commande du client incluait un coupon (coupon/sans coupon) = Aucun coupon
      * Est la dernière commande du client ? = Non

   * &#x200B;
     [!UICONTROL Formule]: `B/A`
   * [!UICONTROL Format] : `Percentage %`

   * Sélectionnez un nombre statistiquement significatif dans `Customer's by lifetime orders` graphique ou 1-5.

* `A` de mesure : `Number of orders`
* `B` de mesure : `Number of non last orders`
* [!UICONTROL Formula] : `Repeat order probability`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by] : `Customer's order number`
* [!UICONTROL Chart type] : `Bar chart`

* **Taux d&#39;utilisation des coupons des clients acquis par coupon (commandes répétées)**
   * [!UICONTROL Metric] : `New customers`
   * [!UICONTROL Filter] :
      * Client d’acquisition de coupons ou Client d’acquisition hors coupons = Acquisition de coupons

   * [!UICONTROL Metric] : `Number of orders`
   * [!UICONTROL Filter] :
      * Numéro de commande du client > 1
      * La première commande du client comprenait un coupon ? (Coupon/Pas de coupon) = Coupon

   * [!UICONTROL Metric]:`Number of orders`
   * [!UICONTROL Filter] :
      * Numéro de commande du client > 1
      * La première commande du client comprenait un coupon ? (Coupon/Pas de coupon) = Coupon
      * La commande a-t-elle appliqué un bon ? (Coupon/Pas de coupon) = Coupon

   * &#x200B;
     [!UICONTROL Formule]: `C/B`
   * [!UICONTROL Format] : `Percentage %`

* `A` de mesure : `Coupon-acquired customers`
* `B` de mesure : `Number of repeat orders`
* `C` de mesure : `Number of repeat orders with coupon`
* [!UICONTROL Formula] : `% of repeat orders with coupon`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* &#x200B;
  [!UICONTROL Type de graphique]: `Table` (peut transposer ce tableau pour une meilleure visualisation)

* **Taux d&#39;utilisation des coupons des clients non-coupons acquis (commandes répétées)**
   * [!UICONTROL Metric] : `New customers`
   * [!UICONTROL Filter] :
      * Achat de coupon client ou Achat sans coupon client = Achat sans coupon

   * [!UICONTROL Metric] : `Number of orders`
   * [!UICONTROL Filter] :
      * Numéro de commande du client > 1
      * La première commande du client comprenait un coupon ? (Coupon/Aucun coupon) = Aucun coupon

   * [!UICONTROL Metric] : `Number of orders`
   * [!UICONTROL Filter] :
      * Numéro de commande du client > 1
      * La première commande du client comprenait un coupon ? (Coupon/Pas de coupon) = Pas de coupon
      * La commande a-t-elle appliqué un bon ? (Coupon/Pas de coupon) = Coupon

   * &#x200B;
     [!UICONTROL Formule]: `C/B`
   * [!UICONTROL Format] : `Percentage %`

* `A` de mesure : `Non-coupon-acquired customers`
* `B` de mesure : `Number of repeat orders`
* `C` de mesure : `Number of repeat orders with coupon`
* [!UICONTROL Formula] : `% of repeat orders with coupon`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* &#x200B;
  [!UICONTROL Type de graphique]: `Table` (peut transposer ce tableau pour une meilleure visualisation)

* **Informations sur l’utilisation des coupons (premières commandes)**
   * [!UICONTROL Metric] : `Number of orders`
   * [!UICONTROL Filter] :
      * Numéro de commande du client = 1
      * Nombre de commandes avec ce coupon > 10

   * &#x200B;
     [!UICONTROL Metric]: `Revenue`
   * [!UICONTROL Filter] :
      * Numéro de commande du client = 1
      * Nombre de commandes avec ce coupon > 10

   * [!UICONTROL Metric] : `Coupon discount amount`
   * [!UICONTROL Filter] :
      * Numéro de commande du client = 1
      * Nombre de commandes avec ce coupon > 10

   * [!UICONTROL Formula] : `B-C` (si C est négatif); B+C (si C est positif)
   * &#x200B;
     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Metric] : `Average order value`
   * [!UICONTROL Filter] :
      * Numéro de commande du client = 1
      * Nombre de commandes avec ce coupon > 10

* `A` de mesure : `First time orders (FTO)`
* `B` de mesure : `Revenue from FTO`
* `C` de mesure : `Discounts applied to FTO`
* [!UICONTROL Formula] : `Gross revenue from FTO`
* `E` de mesure : `Average order value for FTO`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by] : `coupon code`
* &#x200B;
  [!UICONTROL Type de graphique]: `Table`
>[!NOTE]
>
>La quantité de 10 pour « Nombre de commandes avec ce coupon » est arbitraire. N&#39;hésitez pas à utiliser la quantité la plus appropriée pour ce filtre.

* **Nombre de commandes avec coupon (à toute heure)**
   * [!UICONTROL Metric] : `Number of coupons used`

* `A` de mesure : `Number or orders with coupon`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* &#x200B;
  [!UICONTROL Type de graphique]: `Scalar`

* **Chiffre d’affaires net des commandes avec coupons (à tout moment)**
   * &#x200B;
     [!UICONTROL Metric]: `Revenue`
   * [!UICONTROL Filter] :
      * La commande a-t-elle appliqué un bon ? (Coupon/Pas de coupon) = Coupon

* `A` de mesure : `Net revenue from orders with coupons`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* &#x200B;
  [!UICONTROL Type de graphique]: `Scalar`

* **Remises sur coupons (à tout moment)**
   * [!UICONTROL Metric] : `Number of coupons used`

* `A` de mesure : `Coupon discount amount`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* &#x200B;
  [!UICONTROL Type de graphique]: `Scalar`

* **Nombre de commandes avec et sans coupons**
   * [!UICONTROL Metric] : `Number of orders`

* `A` de mesure : `Number of orders`
* [!UICONTROL Time period] : `Last 24 months`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by] : `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type] : `Stacked column`

* **Utilisation des coupons parmi les utilisateurs réguliers**
   * [!UICONTROL Metric] : `New customers`
   * [!UICONTROL Filter] :
      * Nombre de commandes du client sur la durée de vie > 1

* `A` de mesure : `New customers`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by] : `Customer's coupon usage`
* &#x200B;
  [!UICONTROL Type de graphique]: `Pie`

* **Informations sur l’utilisation des coupons**
   * [!UICONTROL Metric] : `Number of orders with coupon`
   * [!UICONTROL Filter] :
      * Nombre de commandes avec ce coupon > 10

   * &#x200B;
     [!UICONTROL Metric]: `Revenue`
   * [!UICONTROL Filter] :
      * Nombre de commandes avec ce coupon > 10

   * [!UICONTROL Metric] : `Coupon discount amount`
   * [!UICONTROL Filter] :
      * Nombre de commandes avec ce coupon > 10

   * [!UICONTROL Formula] : `B-C` (si `C` est négatif) ; `B+C` (si `C` est positif)
   * &#x200B;
     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula] : `C/(B-C)` (si `C` est négatif) ; `C/(B+C)` (si `C` est positif)
   * &#x200B;
     [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Metric] : `Average order value`
   * [!UICONTROL Filter] :
      * Nombre de commandes avec ce coupon > 10

   * &#x200B;
     [!UICONTROL Formule]: `C/A`
   * &#x200B;
     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Metric] : `Distinct buyers`
   * [!UICONTROL Filter] :
      * Nombre de commandes avec ce coupon > 10

* `A` de mesure : `Number of orders`
* `B` de mesure : `Net revenue from orders`
* `C` de mesure : `Total discounts applied`
* [!UICONTROL Formula] : `Gross revenue`
* [!UICONTROL Formula] : `% discounted`
* `F` de mesure : `Average net order value`
* [!UICONTROL Formula] : `Average order discount`
* `H` de mesure : `Distinct buyers`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by] : `coupon code`
* &#x200B;
  [!UICONTROL Type de graphique]: `Table`

>[!NOTE]
>
>La quantité de 10 pour « Nombre de commandes avec ce coupon » est arbitraire. N&#39;hésitez pas à utiliser la quantité la plus appropriée pour ce filtre.

Après avoir compilé tous les rapports, vous pouvez les organiser selon vos besoins dans le tableau de bord. Le résultat peut ressembler à l’image en haut de la page.

Si vous avez des questions lors de la création de cette analyse ou si vous souhaitez simplement contacter l’équipe des services professionnels, [contactez l’assistance &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

>[!NOTE]
>
>Depuis Adobe Commerce 2.4.7, les clients peuvent utiliser les tables **quote_coupons** et **sales_order_coupons** pour obtenir des informations sur la manière dont les clients utilisent plusieurs coupons.

![Diagramme de relation de table pour l’analyse multi-coupon](../../assets/multicoupon_relationship_tables.png)
