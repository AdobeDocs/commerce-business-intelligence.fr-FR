---
title: Performances des coupons
description: Découvrez comment analyser les performances de vos coupons.
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 0%

---

# Analyse avancée du code de bon

Comprendre les performances des coupons de votre entreprise est un moyen intéressant de segmenter vos commandes et de mieux comprendre vos clients. Cet article décrit les étapes à suivre pour créer des analyses afin de comprendre quels clients vous acquérez grâce à l’utilisation de coupons, leurs performances et le suivi de l’utilisation générale des coupons.

![](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

Cette analyse contient [colonnes calculées avancées](../data-warehouse-mgr/adv-calc-columns.md).

## Prise en main

Dans un premier temps, vous devez vous assurer que les colonnes suivantes sont synchronisées avec votre Data Warehouse. Dans le cas contraire, effectuez-en le suivi en accédant à &quot;Gérer les données&quot; > &quot;Data Warehouse&quot; et en synchronisant les éléments suivants :

* **sales\_plat\_order** table
* **coupon\_code**
* **base\_discount\_amount**

## Colonnes calculées

Colonnes à créer, quelle que soit la stratégie de commandes d’invités :

* `sales\_flat\_order` table
* **Bon de commande appliqué ?**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `coupon\_code`
   * [!UICONTROL Datatype]:: `String`
   * [!UICONTROL Calculation]: Cas lorsque `A` est nul alors `No coupon` else `Coupon` end


* **\[INPUT\] customer\_id - code de coupon**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `customer\_id`
      * `B`: `coupon\_code`
   * [!UICONTROL Datatype]: Chaîne
   * [!UICONTROL Calculation]:: `concat(A,' - ',B)`


* **Nombre de commandes avec ce coupon**
   * [!UICONTROL Column type]: `Same Table => EVENT\_NUMBER`
   * Propriétaire de l’événement :`INPUT customer_id - coupon code`
   * Classement des événements : `created\_at`
   * [!UICONTROL Filters]: `Orders we count` ensemble de filtres

Colonnes supplémentaires à créer si les commandes d’invités NE SONT PAS prises en charge :

* `customer\_entity` table
   * **La première commande du client comprenait un coupon ? (Bon/Aucun coupon)**
   * [!UICONTROL Column type]: `Many to One => MAX`
   * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
   * Sélectionnez une [!UICONTROL column]: `Order has coupon applied? (Coupon/No coupon)`
   * [!UICONTROL Filters]:
      * `A`: `Orders we count`
      * `B`: `Customer's order number = 1`
   * **Coupon de première commande du client**
      * [!UICONTROL Column type]: `Many to One => MAX`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Sélectionnez une [!UICONTROL column]: `coupon\_code`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Customer's order number = 1`
   * **Nombre de coupons utilisés sur la durée de vie du client**
      * [!UICONTROL Column type]: `Many to One => COUNT`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Order has coupon applied? (Coupon/No coupon) = Coupon`
   * **Client ayant acheté un coupon ou client ayant acheté un autre coupon**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`
      * [!UICONTROL Datatype]:: `String`
      * [!UICONTROL Calculation]: **Cas où A=&#39;Coupon&#39; alors &#39;Client d&#39;acquisition de coupon&#39; else &#39;Client d&#39;acquisition de coupon&#39;**
   * **Pourcentage des commandes du client avec coupon**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `User's lifetime number of coupons used`
         * `B`: `User's lifetime number of orders`
      * [!UICONTROL Datatype]:: `Decimal`
      * [!UICONTROL Calculation]: **cas où A est nul ou B est nul ou B=0 alors nul autre fin A/B**
   * **Utilisation des coupons du client**
      * [!UICONTROL Column type]: `Same Table => Calculation`
      * [!UICONTROL Inputs]:
         * `A`: `Percent of customer's orders with coupon`
      * [!UICONTROL Datatype]:: `String`
      * [!UICONTROL Calculation]: **Cas où A est nul puis nul lorsque A=0 alors &quot;Coupon jamais utilisé&quot; lorsque A&lt;0.5 alors &quot;Prix le plus souvent plein&quot; quand A=0.5 puis &quot;50/50&quot; quand A=1 puis &quot;Coupons seulement&quot; quand A>0.5 puis &quot;Coupon principalement&quot; else &quot;Indéfini&quot;**









* `sales\_flat\_order` table
   * **Coupon inclus dans la première commande du client ? (Bon/Aucun coupon)**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Sélectionnez une [!UICONTROL column]: `Customer's first order included a coupon? (Coupon/No coupon)`
^
   * **Coupon de première commande du client**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Sélectionnez une [!UICONTROL column]: `Customer's first order coupon?`


Colonnes supplémentaires à créer si les commandes d’invités NE SONT PAS prises en charge :

* `sales\_flat\_order` table
   * **La première commande du client comprenait un coupon ? (Bon/Aucun coupon)** **-** créé par analyste dans le cadre de votre ticket \[ANALYSE COUPON\]
   * **Coupon de première commande du client**{:}**-** créé par analyste dans le cadre de votre ticket \[ANALYSE COUPON\]

* **Nombre de coupons utilisés sur la durée de vie du client**{:}**-** créé par analyste dans le cadre de votre ticket \[ANALYSE COUPON\]
* **Client ayant acheté un coupon ou client ayant acheté un autre coupon**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`
   * [!UICONTROL Datatype]:: `String`
   * [!UICONTROL Calculation]: **Cas où A=&#39;Coupon&#39; alors &#39;Client d&#39;acquisition de coupon&#39; else &#39;Client d&#39;acquisition de coupon&#39;**


* **Pourcentage des commandes du client avec coupon**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `User's lifetime number of coupons used`
      * `B`: `User's lifetime number of orders`
   * [!UICONTROL Datatype]:: `Decimal`
   * [!UICONTROL Calculation]: **cas où A est nul ou B est nul ou B=0 alors nul autre fin A/B**


* **Utilisation des coupons du client**
   * [!UICONTROL Column type]: `Same Table => Calculation`
   * [!UICONTROL Inputs]:
      * `A`: `Percent of customer's orders with coupon`
   * [!UICONTROL Datatype]:: `String`
   * [!UICONTROL Calculation]: **Cas où A est nul puis nul lorsque A=0 alors &quot;Coupon jamais utilisé&quot; lorsque A&lt;0.5 alors &quot;Prix le plus souvent plein&quot; quand A=0.5 puis &quot;50/50&quot; quand A=1 puis &quot;Coupons seulement&quot; quand A>0.5 puis &quot;Coupon principalement&quot; else &quot;Indéfini&quot;**


## Mesures

* **Montant de la remise sur le coupon**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* Dans le `sales\_flat\_order` table
* Cette mesure effectue une **Somme**
* Sur le `discount\_amount` column
* Commandé par le `created\_at` timestamp
* [!UICONTROL Filter]:

* **Nombre de coupons utilisés**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* Dans le `sales\_flat\_order` table
* Cette mesure effectue une **Count**
* Sur le `entity\_id` column
* Commandé par le `created\_at` timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures ;](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Rapports

* **% des clients ayant souscrit un bon ou n’ayant pas obtenu un bon**
   * [!UICONTROL Metric]: `New customers`

* Mesure `A`: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by]: `Coupon acquisitions customer` ou `Non coupon acquisition customer`
* 

   [!UICONTROL Type de graphique]: `Pie`

* **Nombre de clients ayant souscrit un bon ou n’ayant pas obtenu un bon**
   * [!UICONTROL Metric]: `New customers`

* Mesure A : `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Coupon acquisitions customer` ou `Non coupon acquisition customer`
* [!UICONTROL Chart type]: `Stacked column`

* **Chiffre d’affaires moyen de la durée de vie : Bons Acq. (90 jours ou plus)**
   * [!UICONTROL Metric]: `Average lifetime revenue`
   * [!UICONTROL Filter]:
      * La première commande du client comprenait un coupon (coupon/aucun coupon) = coupon

* Mesure `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
   [!UICONTROL Intervalle]: `None`
* 

   [!UICONTROL Type de graphique]: `Scalar`

* **Chiffre d’affaires moyen de la durée de vie : Acq non coupon. (90 jours ou plus)**
   * [!UICONTROL Metric]: Chiffre d’affaires moyen
   * [!UICONTROL Filter]:
      * La première commande du client comprenait un coupon (Bon/Aucun coupon) = Aucun coupon

* Mesure `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
   [!UICONTROL Intervalle]: `None`
* 

   [!UICONTROL Type de graphique]: `Scalar`

* **Chiffre d’affaires moyen de la durée de vie par coupon de première commande**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* Mesure `A`: `Average lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by]: `Customer's first order's coupon`
* 

   [!UICONTROL Type de graphique]: `Column`

>[!NOTE]
>
>Si vous disposez d’un grand nombre de codes de bon, comme le font de nombreux clients, vous souhaiterez appliquer un Top/Bottom tel que Top 10 trié par les recettes Durée de vie moyenne.

* **Probabilité de commande répétée : Acquisitions de coupons**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * La première commande du client comprenait un coupon (coupon/aucun coupon) = coupon
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * La première commande du client comprenait un coupon (coupon/aucun coupon) = coupon
      * La dernière commande du client ? = Non
   * 
      [!UICONTROL Formule]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * Sélectionnez un nombre statistiquement significatif parmi `Customer's by lifetime orders` graphique. Lorsque vous observez le graphique, nous recherchons généralement les numéros de commande avec 30 clients ou plus dans l’intervalle. En fonction de votre jeu de données, il peut s’agir d’un grand nombre. Vous pouvez donc ajouter 1 à 10.


* Mesure `A`: `Number of orders`
* Mesure `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **Probabilité de l’ordre de répétition : Acquisitions sans coupon**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * La première commande du client comprenait un bon (bon/pas de bon) = Aucun bon
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * La première commande du client comprenait un bon (bon/pas de bon) = Aucun bon
      * La dernière commande du client ? = Non
   * 
      [!UICONTROL Formule]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * Sélectionnez un nombre statistiquement significatif parmi `Customer's by lifetime orders` ou 1-5.



* Mesure `A`: `Number of orders`
* Mesure `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **Taux d&#39;utilisation des coupons des clients achetés par coupon (commandes répétées)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Client d&#39;acquisition de coupons ou client d&#39;acquisition de coupons = Acquisition de coupons
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Numéro de commande du client > 1
      * La première commande du client comprenait un coupon ? (Coupon/Aucun coupon) = Coupon
   * [!UICONTROL Metric]:`Number of orders`
   * [!UICONTROL Filter]:
      * Numéro de commande du client > 1
      * La première commande du client comprenait un coupon ? (Coupon/Aucun coupon) = Coupon
      * Bon de commande appliqué ? (Coupon/Aucun coupon) = Coupon
   * 
      [!UICONTROL Formule]: `C/B`
   * [!UICONTROL Format]: `Percentage %`




* Mesure `A`: `Coupon-acquired customers`
* Mesure `B`: `Number of repeat orders`
* Mesure `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalle]: `None`
* 

   [!UICONTROL Type de graphique]: `Table` (peut transposer ce tableau pour une meilleure visualisation)

* **Taux d&#39;utilisation des coupons des clients non-coupons acquis (commandes répétées)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Client ayant acheté un bon ou client n’ayant pas acheté de bon = Acquisition de bons
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Numéro de commande du client > 1
      * La première commande du client comprenait un coupon ? (Coupon/Aucun coupon) = Aucun coupon
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Numéro de commande du client > 1
      * La première commande du client comprenait un coupon ? (Coupon/Aucun coupon) = Aucun coupon
      * Bon de commande appliqué ? (Coupon/Aucun coupon) = Coupon
   * 
      [!UICONTROL Formule]: `C/B`
   * [!UICONTROL Format]: `Percentage %`




* Mesure `A`: `Non-coupon-acquired customers`
* Mesure `B`: `Number of repeat orders`
* Mesure `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalle]: `None`
* 

   [!UICONTROL Type de graphique]: `Table` (peut transposer ce tableau pour une meilleure visualisation)

* **Détails d’utilisation du coupon (premières commandes)**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Numéro de commande du client = 1
      * Nombre de commandes avec ce coupon > 10
   * 
      [!UICONTROL Mesure]: `Revenue`
   * [!UICONTROL Filter]:
      * Numéro de commande du client = 1
      * Nombre de commandes avec ce coupon > 10
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * Numéro de commande du client = 1
      * Nombre de commandes avec ce coupon > 10
   * [!UICONTROL Formula]: `B-C` (si C est négatif); B+C (si C est positif)
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * Numéro de commande du client = 1
      * Nombre de commandes avec ce coupon > 10




* Mesure `A`: `First time orders (FTO)`
* Mesure `B`: `Revenue from FTO`
* Mesure `C`: `Discounts applied to FTO`
* [!UICONTROL Formula]: `Gross revenue from FTO`
* Mesure `E`: `Average order value for FTO`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by]: `coupon code`
* 

   [!UICONTROL Type de graphique]: `Table`
>[!NOTE]
>
>La quantité de 10 pour &quot;Nombre de commandes avec ce coupon&quot; est arbitraire. N’hésitez pas à utiliser la quantité la plus appropriée pour ce filtre.

* **Nombre de commandes avec coupon (toutes les heures)**
   * [!UICONTROL Metric]: `Number of coupons used`

* Mesure `A`: `Number or orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalle]: `None`
* 

   [!UICONTROL Type de graphique]: `Scalar`

* **Chiffre d’affaires net des commandes avec coupons (tout le temps)**
   * 
      [!UICONTROL Mesure]: `Revenue`
   * [!UICONTROL Filter]:
      * Bon de commande appliqué ? (Coupon/Aucun coupon) = Coupon

* Mesure `A`: `Net revenue from orders with coupons`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalle]: `None`
* 

   [!UICONTROL Type de graphique]: `Scalar`

* **Remises sur les coupons (tout le temps)**
   * [!UICONTROL Metric]: `Number of coupons used`

* Mesure `A`: `Coupon discount amount`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalle]: `None`
* 

   [!UICONTROL Type de graphique]: `Scalar`

* **Nombre de commandes avec et sans coupons**
   * [!UICONTROL Metric]: `Number of orders`

* Mesure `A`: `Number of orders`
* [!UICONTROL Time period]: `Last 24 months`
* 
   [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by]: `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type]: `Stacked column`

* **Utilisation des coupons parmi les utilisateurs récurrents**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Nombre de commandes sur toute la durée de vie du client > 1

* Mesure `A`: `New customers`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by]: `Customer's coupon usage`
* 

   [!UICONTROL Type de graphique]: `Pie`

* **Détails de l’utilisation du coupon**
   * [!UICONTROL Metric]: `Number of orders with coupon`
   * [!UICONTROL Filter]:
      * Nombre de commandes avec ce coupon > 10
   * 
      [!UICONTROL Mesure]: `Revenue`
   * [!UICONTROL Filter]:
      * Nombre de commandes avec ce coupon > 10
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * Nombre de commandes avec ce coupon > 10
   * [!UICONTROL Formula]: `B-C` (if `C` est négatif); `B+C` (if `C` est positif)
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `C/(B-C)` (if `C` est négatif); `C/(B+C)` (if `C` est positif)
   * 

      [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * Nombre de commandes avec ce coupon > 10
   * 
      [!UICONTROL Formule]: `C/A`
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Metric]: `Distinct buyers`
   * [!UICONTROL Filter]:
      * Nombre de commandes avec ce coupon > 10





* Mesure `A`: `Number of orders`
* Mesure `B`: `Net revenue from orders`
* Mesure `C`: `Total discounts applied`
* [!UICONTROL Formula]: `Gross revenue`
* [!UICONTROL Formula]: `% discounted`
* Mesure `F`: `Average net order value`
* [!UICONTROL Formula]: `Average order discount`
* Mesure `H`: `Distinct buyers`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by]: `coupon code`
* 
   [!UICONTROL Type de graphique]: `Table`

>[!NOTE]
>
>La quantité de 10 pour &quot;Nombre de commandes avec ce coupon&quot; est arbitraire. N’hésitez pas à utiliser la quantité la plus appropriée pour ce filtre.

Après avoir compilé tous les rapports, vous pouvez les organiser dans le tableau de bord suivant vos besoins. Le résultat final peut ressembler à l’image en haut de la page.

Si vous rencontrez des questions lors de la création de cette analyse ou si vous souhaitez simplement faire appel à notre équipe de services professionnels, [support technique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
