---
title: Performances des coupons
description: Découvrez comment analyser les performances de vos coupons.
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: d8fc96a58b72c601a5700f35ea1f3dc982d76571
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 0%

---

# Analyse avancée du code de bon

Comprendre les performances des coupons de votre entreprise est un moyen intéressant de segmenter vos commandes et de mieux comprendre vos clients. Cette rubrique vous guide tout au long des étapes nécessaires à la création d’analyses afin de comprendre quels clients vous acquérez à l’aide de bons, leurs performances et le suivi de l’utilisation générale des bons.

![](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

Cette analyse contient [des colonnes calculées avancées](../data-warehouse-mgr/adv-calc-columns.md).

## Prise en main

Dans un premier temps, vous devez vous assurer que les colonnes suivantes sont synchronisées avec votre Data Warehouse. Si ce n’est pas le cas, effectuez-en le suivi en accédant à `Manage Data` > `Data Warehouse` et en synchronisant les éléments suivants :

* Table **sales\_plat\_order**
* **coupon\_code**
* **base\_discount\_amount**

## Colonnes calculées

Colonnes à créer, quelle que soit la stratégie de commandes d’invités :

* `sales\_flat\_order` table
* **Le coupon de commande est-il appliqué ?**
   * [!UICONTROL Column type] : `Same Table => CALCULATION`
   * [!UICONTROL Inputs] :
      * `A` : `coupon\_code`

   * &#x200B;

     [!UICONTROL Type de données]: `String`
   * [!UICONTROL Calculation] : cas où `A` est nul puis `No coupon` autre `Coupon` se termine

* **\[INPUT\] customer\_id - code de coupon**
   * [!UICONTROL Column type] : `Same Table => CALCULATION`
   * [!UICONTROL Inputs] :
      * `A` : `customer\_id`
      * `B` : `coupon\_code`

   * [!UICONTROL Datatype] String
   * [!UICONTROL Calculation] : `concat(A,' - ',B)`

* **Nombre de commandes avec ce coupon**
   * [!UICONTROL Column type] : `Same Table => EVENT\_NUMBER`
   * Propriétaire de l’événement :`INPUT customer_id - coupon code`
   * Classement d’événement : `created\_at`
   * [!UICONTROL Filters] : `Orders we count` jeu de filtres

Colonnes supplémentaires à créer si les commandes d’invités NE SONT PAS prises en charge :

* `customer\_entity` table
   * **La première commande du client comprenait un bon ? (Bon/Aucun coupon)**
   * [!UICONTROL Column type] : `Many to One => MAX`
   * [!UICONTROL Path] : `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
   * Sélectionnez un [!UICONTROL column] : `Order has coupon applied? (Coupon/No coupon)`
   * [!UICONTROL Filters] :
      * `A` : `Orders we count`
      * `B` : `Customer's order number = 1`

   * **Coupon de première commande du client**
      * [!UICONTROL Column type] : `Many to One => MAX`
      * [!UICONTROL Path] : `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Sélectionnez un [!UICONTROL column] : `coupon\_code`
      * [!UICONTROL Filter] :
         * `A` : `Orders we count`
         * `B` : `Customer's order number = 1`

   * **Nombre de coupons pendant toute la durée de vie du client utilisés**
      * [!UICONTROL Column type] : `Many to One => COUNT`
      * [!UICONTROL Path] : `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter] :
         * `A` : `Orders we count`
         * `B` : `Order has coupon applied? (Coupon/No coupon) = Coupon`

   * **Client d&#39;acquisition de coupons ou client d&#39;acquisition de coupons**
      * [!UICONTROL Column type] : `Same Table => CALCULATION`
      * [!UICONTROL Inputs] :
         * `A` : `Customer's first order included a coupon? (Coupon/No coupon)`

      * &#x200B;

        [!UICONTROL Type de données]: `String`
      * [!UICONTROL Calculation] : **cas où A=&#39;Coupon&#39; puis &#39;client d&#39;acquisition de coupon&#39; else &#39;client d&#39;acquisition de coupon&#39; end**

   * **Pourcentage des commandes du client avec coupon**
      * [!UICONTROL Column type] : `Same Table => CALCULATION`
      * [!UICONTROL Inputs] :
         * `A` : `User's lifetime number of coupons used`
         * `B` : `User's lifetime number of orders`

      * &#x200B;

        [!UICONTROL Type de données]: `Decimal`
      * [!UICONTROL Calculation] : **cas où A est nul ou B est nul ou B=0 alors nul autre A/B end**

   * **Utilisation des coupons du client**
      * [!UICONTROL Column type] : `Same Table => Calculation`
      * [!UICONTROL Inputs] :
         * `A` : `Percent of customer's orders with coupon`

      * &#x200B;

        [!UICONTROL Type de données]: `String`
      * [!UICONTROL Calculation] : **cas où A est nul puis nul lorsque A=0 puis &#39;coupon jamais utilisé&#39; quand A&lt;0.5 puis &#39;Surtout plein prix&#39; quand A=0.5 puis &#39;50/50&#39; quand A=1 puis &#39;Coupons uniquement&#39; quand A>0.5 puis &#39;Coupon principalement&#39; else &#39;Non défini&#39; end**

* `sales\_flat\_order` table
   * **La première commande du client comprenait-elle un coupon ? (Bon/Aucun coupon)**
      * [!UICONTROL Column type] : `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path] : `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Sélectionnez un [!UICONTROL column] : `Customer's first order included a coupon? (Coupon/No coupon)`
^

   * **Coupon de première commande du client**
      * [!UICONTROL Column type] : `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path] : `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Sélectionnez un [!UICONTROL column] : `Customer's first order coupon?`

Colonnes supplémentaires à créer si les commandes d’invités NE SONT PAS prises en charge :

* `sales\_flat\_order` table
   * **La première commande du client comprenait un bon ? (Bon/Aucun coupon)** **-** créé par l’analyste dans le cadre de votre ticket \[ANALYSE DU COUPON\]
   * **Coupon de première commande du client**{:}**-** créé par l’analyste dans le cadre de votre ticket \[ANALYSE COUPON\]

* **Nombre de coupons sur toute la durée de vie du client utilisés**{:}**-** créés par l’analyste dans le cadre de votre ticket \[ANALYSE COUPON\]
* **Client d&#39;acquisition de coupons ou client d&#39;acquisition de coupons**
   * [!UICONTROL Column type] : `Same Table => CALCULATION`
   * [!UICONTROL Inputs] :
      * `A` : `Customer's first order included a coupon? (Coupon/No coupon)`

   * &#x200B;

     [!UICONTROL Type de données]: `String`
   * [!UICONTROL Calculation] : **cas où A=&#39;Coupon&#39; puis &#39;client d&#39;acquisition de coupon&#39; else &#39;client d&#39;acquisition de coupon&#39; end**

* **Pourcentage des commandes du client avec coupon**
   * [!UICONTROL Column type] : `Same Table => CALCULATION`
   * [!UICONTROL Inputs] :
      * `A` : `User's lifetime number of coupons used`
      * `B` : `User's lifetime number of orders`

   * &#x200B;

     [!UICONTROL Type de données]: `Decimal`
   * [!UICONTROL Calculation] : **cas où A est nul ou B est nul ou B=0 alors nul autre A/B end**

* **Utilisation des coupons du client**
   * [!UICONTROL Column type] : `Same Table => Calculation`
   * [!UICONTROL Inputs] :
      * `A` : `Percent of customer's orders with coupon`

   * &#x200B;

     [!UICONTROL Type de données]: `String`
   * [!UICONTROL Calculation] : **cas où A est nul puis nul lorsque A=0 puis &#39;coupon jamais utilisé&#39; quand A&lt;0.5 puis &#39;Surtout plein prix&#39; quand A=0.5 puis &#39;50/50&#39; quand A=1 puis &#39;Coupons uniquement&#39; quand A>0.5 puis &#39;Coupon principalement&#39; else &#39;Non défini&#39; end**

## Mesures

* **Montant de réduction sur le coupon**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* Dans la table `sales\_flat\_order`
* Cette mesure exécute une **Somme**
* Sur la colonne `discount\_amount`
* Ordonné par l’horodatage `created\_at`
* [!UICONTROL Filter] :

* **Nombre de coupons utilisés**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* Dans la table `sales\_flat\_order`
* Cette mesure exécute un **décompte**
* Sur la colonne `entity\_id`
* Ordonné par l’horodatage `created\_at`
* [!UICONTROL Filter] :

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Rapports

* **% des clients non-coupon et non-acquis**
   * [!UICONTROL Metric] : `New customers`

* Mesure `A` : `Coupon acquisitions`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by] : `Coupon acquisitions customer` ou `Non coupon acquisition customer`
* &#x200B;
  [!UICONTROL Type de graphique]: `Pie`

* **Nombre de clients ayant obtenu un bon ou n’ayant pas obtenu un bon**
   * [!UICONTROL Metric] : `New customers`

* Mesure A : `Coupon acquisitions`
* [!UICONTROL Time period] : `All time`
* [!UICONTROL Interval] : `By Month`
* [!UICONTROL Group by] : `Coupon acquisitions customer` ou `Non coupon acquisition customer`
* [!UICONTROL Chart type] : `Stacked column`

* **Chiffre d’affaires moyen de la durée de vie : Bons Acq. (90 jours ou plus)**
   * [!UICONTROL Metric] : `Average lifetime revenue`
   * [!UICONTROL Filter] :
      * La première commande du client comprenait un coupon (Bon/Aucun coupon) = Bon

* Mesure `A` : `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period] : `X years ago to 90 days ago`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* &#x200B;
  [!UICONTROL Type de graphique]: `Scalar`

* **Chiffre d’affaires moyen de la durée de vie : Acq non-coupon. (90 jours ou plus)**
   * [!UICONTROL Metric] : Chiffre d’affaires moyen de la durée de vie
   * [!UICONTROL Filter] :
      * La première commande du client comprenait un coupon (Bon/Aucun coupon) = Aucun coupon

* Mesure `A` : `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period] : `X years ago to 90 days ago`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* &#x200B;
  [!UICONTROL Type de graphique]: `Scalar`

* **Chiffre d&#39;affaires moyen de la durée de vie par coupon de première commande**
   * [!UICONTROL Metric] : `Average lifetime revenue`

* Mesure `A` : `Average lifetime revenue`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by] : `Customer's first order's coupon`
* &#x200B;
  [!UICONTROL Type de graphique]: `Column`

>[!NOTE]
>
>Si vous avez de nombreux codes de bon, comme le font de nombreux clients, vous souhaitez appliquer un Top/Bottom tel que Top 10 trié par les recettes de durée de vie moyenne.

* **Probabilité de commande répétée : Acquisitions de coupons**
   * [!UICONTROL Metric] : `Number of orders`
   * [!UICONTROL Filter] :
      * La première commande du client comprenait un coupon (Bon/Aucun coupon) = Bon

   * [!UICONTROL Metric] : `Number of orders`
   * [!UICONTROL Filter] :
      * La première commande du client comprenait un coupon (Bon/Aucun coupon) = Bon
      * La dernière commande du client ? = Non
   * &#x200B;

     [!UICONTROL Formule]: `B/A`
   * [!UICONTROL Format] : `Percentage %`

   * Sélectionnez un nombre statistiquement significatif dans le graphique `Customer's by lifetime orders`. Lorsque vous consultez le graphique, il est préférable de rechercher les numéros de commande avec 30 clients ou plus dans le compartiment. En fonction de votre jeu de données, il peut s’agir d’un grand nombre. Vous pouvez donc ajouter 1 à 10.

* Mesure `A` : `Number of orders`
* Mesure `B` : `Number of non last orders`
* [!UICONTROL Formula] : `Repeat order probability`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by] : `Customer's order number`
* [!UICONTROL Chart type] : `Bar chart`

* **Probabilité de commande répétée : acquisitions sans coupon**
   * [!UICONTROL Metric] : `Number of orders`
   * [!UICONTROL Filter] :
      * La première commande du client comprenait un coupon (coupon/aucun coupon) = Aucun coupon

   * [!UICONTROL Metric] : `Number of orders`
   * [!UICONTROL Filter] :
      * La première commande du client comprenait un coupon (coupon/aucun coupon) = Aucun coupon
      * La dernière commande du client ? = Non

   * &#x200B;

     [!UICONTROL Formule]: `B/A`
   * [!UICONTROL Format] : `Percentage %`

   * Sélectionnez un nombre statistiquement significatif dans le graphique `Customer's by lifetime orders` ou 1-5.

* Mesure `A` : `Number of orders`
* Mesure `B` : `Number of non last orders`
* [!UICONTROL Formula] : `Repeat order probability`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by] : `Customer's order number`
* [!UICONTROL Chart type] : `Bar chart`

* **Taux d’utilisation des coupons des clients achetés par coupon (commandes répétées)**
   * [!UICONTROL Metric] : `New customers`
   * [!UICONTROL Filter] :
      * Client d&#39;acquisition de coupon ou client d&#39;acquisition de non-coupon = Acquisition de coupons

   * [!UICONTROL Metric] : `Number of orders`
   * [!UICONTROL Filter] :
      * Numéro de commande du client > 1
      * La première commande du client comprenait un coupon ? (Bon/Aucun coupon) = Bon

   * [!UICONTROL Metric]:`Number of orders`
   * [!UICONTROL Filter] :
      * Numéro de commande du client > 1
      * La première commande du client comprenait un coupon ? (Bon/Aucun coupon) = Bon
      * Bon de commande appliqué ? (Bon/Aucun coupon) = Bon

   * &#x200B;

     [!UICONTROL Formule]: `C/B`
   * [!UICONTROL Format] : `Percentage %`

* Mesure `A` : `Coupon-acquired customers`
* Mesure `B` : `Number of repeat orders`
* Mesure `C` : `Number of repeat orders with coupon`
* [!UICONTROL Formula] : `% of repeat orders with coupon`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* &#x200B;
  [!UICONTROL Type de graphique]: `Table` (peut transposer ce tableau pour une meilleure visualisation)

* **Taux d’utilisation des coupons des clients non-coupons acquis (commandes répétées)**
   * [!UICONTROL Metric] : `New customers`
   * [!UICONTROL Filter] :
      * Client d&#39;acquisition de coupons ou client d&#39;acquisition de coupons = Acquisition de coupons non

   * [!UICONTROL Metric] : `Number of orders`
   * [!UICONTROL Filter] :
      * Numéro de commande du client > 1
      * La première commande du client comprenait un coupon ? (Bon/Aucun coupon) = Aucun coupon

   * [!UICONTROL Metric] : `Number of orders`
   * [!UICONTROL Filter] :
      * Numéro de commande du client > 1
      * La première commande du client comprenait un coupon ? (Bon/Aucun coupon) = Aucun coupon
      * Bon de commande appliqué ? (Bon/Aucun coupon) = Bon

   * &#x200B;

     [!UICONTROL Formule]: `C/B`
   * [!UICONTROL Format] : `Percentage %`

* Mesure `A` : `Non-coupon-acquired customers`
* Mesure `B` : `Number of repeat orders`
* Mesure `C` : `Number of repeat orders with coupon`
* [!UICONTROL Formula] : `% of repeat orders with coupon`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* &#x200B;
  [!UICONTROL Type de graphique]: `Table` (peut transposer ce tableau pour une meilleure visualisation)

* **Détails de l’utilisation du coupon (premières commandes)**
   * [!UICONTROL Metric] : `Number of orders`
   * [!UICONTROL Filter] :
      * Numéro de commande du client = 1
      * Nombre de commandes avec ce coupon > 10

   * &#x200B;

     [!UICONTROL Mesure]: `Revenue`
   * [!UICONTROL Filter] :
      * Numéro de commande du client = 1
      * Nombre de commandes avec ce coupon > 10

   * [!UICONTROL Metric] : `Coupon discount amount`
   * [!UICONTROL Filter] :
      * Numéro de commande du client = 1
      * Nombre de commandes avec ce coupon > 10

   * [!UICONTROL Formula] : `B-C` (si C est négatif) ; B+C (si C est positif)
   * &#x200B;

     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Metric] : `Average order value`
   * [!UICONTROL Filter] :
      * Numéro de commande du client = 1
      * Nombre de commandes avec ce coupon > 10

* Mesure `A` : `First time orders (FTO)`
* Mesure `B` : `Revenue from FTO`
* Mesure `C` : `Discounts applied to FTO`
* [!UICONTROL Formula] : `Gross revenue from FTO`
* Mesure `E` : `Average order value for FTO`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by] : `coupon code`
* &#x200B;
  [!UICONTROL Type de graphique]: `Table`
>[!NOTE]
>
>La quantité de 10 pour &quot;Nombre de commandes avec ce coupon&quot; est arbitraire. N’hésitez pas à utiliser la quantité la plus appropriée pour ce filtre.

* **Nombre de commandes avec coupon (tout le temps)**
   * [!UICONTROL Metric] : `Number of coupons used`

* Mesure `A` : `Number or orders with coupon`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* &#x200B;
  [!UICONTROL Type de graphique]: `Scalar`

* **Chiffre d&#39;affaires net des commandes avec coupons (tout le temps)**
   * &#x200B;

     [!UICONTROL Mesure]: `Revenue`
   * [!UICONTROL Filter] :
      * Bon de commande appliqué ? (Bon/Aucun coupon) = Bon

* Mesure `A` : `Net revenue from orders with coupons`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* &#x200B;
  [!UICONTROL Type de graphique]: `Scalar`

* **Remises sur les coupons (tout le temps)**
   * [!UICONTROL Metric] : `Number of coupons used`

* Mesure `A` : `Coupon discount amount`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* &#x200B;
  [!UICONTROL Type de graphique]: `Scalar`

* **Nombre de commandes avec et sans coupons**
   * [!UICONTROL Metric] : `Number of orders`

* Mesure `A` : `Number of orders`
* [!UICONTROL Time period] : `Last 24 months`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by] : `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type] : `Stacked column`

* **Utilisation de coupon parmi les utilisateurs réguliers**
   * [!UICONTROL Metric] : `New customers`
   * [!UICONTROL Filter] :
      * Nombre de commandes sur toute la durée de vie du client > 1

* Mesure `A` : `New customers`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by] : `Customer's coupon usage`
* &#x200B;
  [!UICONTROL Type de graphique]: `Pie`

* **Détails de l’utilisation du coupon**
   * [!UICONTROL Metric] : `Number of orders with coupon`
   * [!UICONTROL Filter] :
      * Nombre de commandes avec ce coupon > 10

   * &#x200B;

     [!UICONTROL Mesure]: `Revenue`
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

* Mesure `A` : `Number of orders`
* Mesure `B` : `Net revenue from orders`
* Mesure `C` : `Total discounts applied`
* [!UICONTROL Formula] : `Gross revenue`
* [!UICONTROL Formula] : `% discounted`
* Mesure `F` : `Average net order value`
* [!UICONTROL Formula] : `Average order discount`
* Mesure `H` : `Distinct buyers`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by] : `coupon code`
* &#x200B;
  [!UICONTROL Type de graphique]: `Table`

>[!NOTE]
>
>La quantité de 10 pour &quot;Nombre de commandes avec ce coupon&quot; est arbitraire. N’hésitez pas à utiliser la quantité la plus appropriée pour ce filtre.

Après avoir compilé tous les rapports, vous pouvez les organiser dans le tableau de bord suivant vos besoins. Le résultat peut ressembler à l’image en haut de la page.

Si vous rencontrez des questions lors de la création de cette analyse ou si vous souhaitez simplement contacter l’équipe des services professionnels, [contactez l’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

>[!NOTE]
>
>Depuis Adobe Commerce 2.4.7, les clients peuvent utiliser les tables **quote_coupons** et **ventes_order_coupons** pour obtenir des informations sur la manière dont les clients utilisent plusieurs coupons.

![](../../assets/multicoupon_relationship_tables.png)
