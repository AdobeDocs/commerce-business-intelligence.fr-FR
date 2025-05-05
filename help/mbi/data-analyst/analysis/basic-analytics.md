---
title: Comprendre et créer des analyses de base
description: Découvrez comment comprendre et créer des analyses de base.
exl-id: 23cea7b3-2e66-40c3-b4bd-d197237782e3
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Dashboards, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '3120'
ht-degree: 0%

---

# Analyses de base

Une fois que vous connaissez la plate-forme [!DNL Adobe Commerce Intelligence] et que vous avez une compréhension de base de l’outil, vous allez commencer à créer des rapports. Une des questions les plus courantes que vous avez est : &quot;Que dois-je regarder ?&quot;

Les informations ci-dessous décrivent certaines des mesures et rapports courants qui peuvent vous être utiles. Certains de ces rapports existent dans votre compte. Dès lors, veillez à consulter les mesures et rapports qui existent dans votre compte afin d’éviter de créer des doublons.

## Tableaux et colonnes à comprendre

Lors de la création d’une mesure, vous devez connaître quatre éléments d’information :

1. Le tableau dans lequel se trouvent les données,
1. L’action spécifique que vous souhaitez effectuer,
1. La colonne sur laquelle vous souhaitez effectuer cette action, et
1. Horodatage que vous souhaitez utiliser pour le suivi de ces données.

Les noms des tables utilisées dans ces exemples sont très probablement légèrement différents des noms des colonnes et des tables de votre base de données, car chaque base de données est unique. Référencez les définitions ci-dessous si vous avez besoin d’aide pour identifier une table ou une colonne correspondante dans votre base de données.

## Table des clients

Ce tableau contient des informations clés sur chaque client, telles qu’un ID de client unique, une adresse électronique, etc. Les exemples ci-dessous utilisent **[!UICONTROL customer_entity]** comme nom d’un exemple de tableau de clients.

Si certains de ces calculs n’existent pas actuellement dans votre base de données, tout utilisateur administrateur de votre compte peut les créer. Vous souhaitez également vous assurer que ces dimensions sont regroupables pour toutes les mesures applicables.

**Dimensions**

* **[!UICONTROL Entity_id]** : identifiant unique de chaque client. Il peut également s’agir d’un numéro de client unique ou d’une adresse électronique du client. Il doit servir de clé de référence à la table de votre commande.
* **[!UICONTROL Created_at]** : date à laquelle le compte du client a été créé et ajouté à votre base de données.
* **[!UICONTROL Customer's lifetime revenue]** : chiffre d’affaires total sur la durée de vie généré par un client.
* **[!UICONTROL Customer's first 30-day revenue]** : montant total des recettes générées par un client au cours de ses 30 premiers jours.
* **[!UICONTROL Customer's lifetime number of orders]** : nombre de commandes passées par un client au cours de sa vie.
* **[!UICONTROL Customer's lifetime number of coupons]** : nombre total de bons utilisés par un client au cours de sa durée de vie.
* **[!UICONTROL Customer's first order date]** : date de la première commande d’un client. Cela peut différer de la date created_at si un client n’a pas passé de commande au moment de sa création.

**Acceptez-vous les commandes d’invités ?**

*Si tel est le cas, ce tableau peut ne pas contenir tous vos clients. Contactez l&#39;[équipe d&#39;assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) pour vous assurer que vos analyses client incluent tous les clients.*

*Vous n&#39;êtes pas sûr d&#39;accepter les commandes d&#39;invités ? Pour en savoir plus, reportez-vous à [cette rubrique](../data-warehouse-mgr/guest-orders.md) !*

## Table des commandes

Dans ce tableau, chaque ligne représente un ordre. Les colonnes de ce tableau contiennent des informations de base sur chaque commande, telles que l’identifiant de la commande, la date de création, l’état, l’identifiant du client qui a passé la commande, etc. Les exemples ci-dessous utilisent **[!UICONTROL sales_flat_order]** comme nom d’un exemple de table de commandes.

**Dimensions**

* **[!UICONTROL Customer_id]** : identifiant unique du client qui a passé la commande. Cette opération est souvent utilisée pour déplacer des informations entre les tables du client et des commandes. Dans ces exemples, vous vous attendez à ce que customer_id sur la table **[!UICONTROL sales_flat_order]** s’aligne sur **[!UICONTROL entitiy_id]** sur la table **[!UICONTROL customer_entity]**.
* **[!UICONTROL Created_at]** : date à laquelle la commande a été créée ou placée.
* **[!UICONTROL Customer_email]** : adresse électronique du client qui a passé la commande. Il peut également s’agir de l’identifiant unique du client.
* **[!UICONTROL Customer's lifetime number of orders]** : copie de la colonne portant le même nom sur votre table `Customers`.
* **[!UICONTROL Customer's order number]** : numéro de commande séquentielle du client associé à la commande. Par exemple, si la ligne que vous observez est la première commande d’un client, cette colonne est &quot;1&quot; ; mais, s’il s’agissait de la 15e commande du client, cette colonne indique &quot;15&quot; pour cette commande. Si cette dimension n’existe pas sur votre table `Customers`, demandez à l’ [équipe d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) de vous aider à la créer.
* **[!UICONTROL Customer's order number (previous-current)]** : concaténation de deux valeurs dans la colonne **[!UICONTROL Customer's order number]**. Il est utilisé dans un exemple de rapport ci-dessous pour afficher le temps écoulé entre deux commandes. Par exemple, l’intervalle entre la date de première commande d’un client et sa date de deuxième commande est représenté sous la forme &quot;1-2&quot; avec ce calcul.
* **[!UICONTROL Coupon_code]** : indique les bons utilisés pour chaque commande.
* **[!UICONTROL Seconds since previous order]** : temps (en secondes) entre les commandes d’un client.

## Tableau des éléments de commande

Dans ce tableau, chaque ligne représente un article vendu. Ce tableau contient des informations sur les articles vendus dans chaque commande, telles que le numéro de référence de la commande, le numéro du produit, la quantité, etc. Les exemples ci-dessous utilisent `sales_flat_order_item` comme nom d’un exemple de tableau d’éléments de commande.

**Dimensions**

* **[!UICONTROL Item_id]** : identifiant unique de chaque ligne du tableau.
* **[!UICONTROL Order_id]** : clé de référence de votre table `Orders` qui vous indique les articles achetés dans la même commande. Si une commande contient plusieurs éléments, cette valeur est répétée.
* **[!UICONTROL Product_id]** : si vous souhaitez des informations sur le produit spécifique acheté (couleur, taille, etc.), utilisez cette colonne pour extraire ces informations de la table de produits.
* **[!UICONTROL Order's created_at]** : horodatage de la commande, généralement copié dans la table `order line items` de la table `Orders`.
* **[!UICONTROL Order's coupon_code]** : à l’instar de la dimension `Order's created_at`, cette colonne est copiée à partir de votre table de commandes.

## Table des abonnements

Ce tableau permet de gérer vos informations d’abonnement, telles que l’ID d’abonnement, l’adresse électronique de l’abonné, la date de début de l’abonnement, etc.

**Dimensions**

* **[!UICONTROL Customer_id]** : identifiant unique du client qui a passé la commande. Il s’agit d’une méthode courante pour créer un chemin entre la table Clients et la table Commandes. Dans ces exemples, vous vous attendez à ce que le customer_id de la table **sales_plat_order** s&#39;aligne sur le `entitiy_id` de la table `customer_entity`.
* **[!UICONTROL Start date]** : date de début de l’abonnement d’un client.

## Tableau des dépenses marketing

Lors de l’analyse de vos dépenses marketing, vous pouvez inclure [!DNL Facebook], [!DNL Google AdWords] ou d’autres sources dans vos analyses. Si vous disposez de plusieurs sources de dépenses marketing, contactez l’ [équipe Managed Services](https://business.adobe.com/products/magento/fully-managed-service.html) pour obtenir de l’aide sur la configuration d’un tableau consolidé pour vos campagnes marketing.

**Dimensions**

* **[!UICONTROL Spend]** : somme des dépenses publicitaires. Dans [!DNL Facebook], il s’agit de la colonne des dépenses de la table `facebook_ads_insights_####`. Pour [!DNL Google AdWords], il s’agit de la colonne `adCost` de la table `campaigns####`.
* Le `####` ajouté à chacune de ces tables correspond à l’ID de compte spécifique pour votre compte [!DNL Facebook] ou [!DNL Google AdWords].
* **[!UICONTROL Clicks]** : nombre total de clics. Dans [!DNL Facebook], il s’agit de la colonne des clics dans la table `facebook_ads_insights_####`. Dans [!DNL Google AdWords], il s’agit de la colonne adClicks de la table `campaigns####`.
* **[!UICONTROL Impressions]** : nombre total d’impressions. Dans [!DNL Facebook], il s’agit des impressions de la table `facebook_ads_insights_####`. Dans [!DNL Google AdWords], il s’agit des impressions de la table `campaigns####`.
* **[!UICONTROL Campaign]** : nombre total de clics. Dans [!DNL Facebook], il s’agit de la colonne campaign_name de la table `facebook_ads_insights_####`. Dans [!DNL Google AdWords], il s’agit de la colonne de campagne dans la table `campaigns####`.
* **[!UICONTROL Date]** : heure et date auxquelles l’activité (dépenses, clics ou impressions) s’est produite pour une campagne spécifique. Dans [!DNL Facebook], il s’agit de la colonne `date_start` de la table `facebook_ads_insights_####`. Dans [!DNL Google AdWords], il s’agit de la colonne de dates dans la table `campaigns####`.
* **[!UICONTROL Customer's first order's source]** : source de la commande issue de la première commande d’un client. Tout d’abord, vérifiez si votre compte contient une colonne nommée `customer's first order's source`. Si vous ne voyez pas cette colonne, vous pouvez créer la colonne de votre choix en suivant ces instructions.
* **[!UICONTROL Customer's first order's medium]** : support de la commande issue de la première commande d’un client. Tout d’abord, vérifiez si votre compte contient une colonne nommée `customer's first order's source`. Si vous ne voyez pas cette colonne, vous pouvez créer la colonne de votre choix en suivant ces instructions.
* **[!UICONTROL Customer's first order's campaign]** : campagne de la commande issue de la première commande d’un client. Tout d’abord, vérifiez si votre compte contient une colonne nommée `customer's first order's source`. Si vous ne voyez pas cette colonne, vous pouvez créer la colonne de votre choix en suivant ces instructions.

## Rapports et mesures courants

Voici quelques exemples courants de rapports et de mesures que vous trouverez utiles :

* [Customer Analytics](#customeranalytics)
* [Analyses de commande](#orderanalytics)
* [Analyses des dépenses marketing](#mktgspendanalytics)

## Customer Analytics {#customeranalytics}

### Nouveaux utilisateurs

* **Description** : nombre total d’utilisateurs nouvellement acquis sur une période donnée. `New Users` est différent de `Unique Customers`, car `New Users` dispose de l’horodatage selon lequel un compte a été créé avec votre service (cela ne signifie pas qu’ils ont nécessairement passé une commande) tandis que `Unique Customers` ont passé au moins une commande.
* **Définition de mesure** : cette mesure exécute un **décompte** de `entity_id` à partir de la table `customer_entity` triée par `created_at`.
* **Exemple de rapport** : nombre de nouveaux utilisateurs créés le mois dernier
   * **[!UICONTROL Metric]** : `New Users`
   * **[!UICONTROL Time Range]** : `Last Month`
   * **[!UICONTROL Time Interval]** : `By Day`

![Nouveaux utilisateurs](../../assets/New_Users_Last_Month.png)<!--{: width="929"}-->

### Clients uniques

* **Description** : comptage du nombre total de clients distincts sur une période donnée. Différent de `New Users`, car il effectue uniquement le suivi des clients qui ont passé au moins une commande. Le rapport d’un client distinct effectue uniquement le suivi d’un client une fois dans un intervalle de temps donné. Si vous définissez l’intervalle de temps sur `By Day` et qu’un client effectue plusieurs achats ce jour-là, le client n’est comptabilisé qu’une seule fois. Si vous souhaitez afficher un nombre total d’achats en général, regardez `Number of Orders`.
* **Définition de mesure** : cette mesure exécute un **Comptage distinct** de `customer_id` à partir de la table `sales_flat_order` triée par `created_at`.
* **Exemple de rapport** : clients distincts par semaine au cours des 90 derniers jours
   * **[!UICONTROL Metric]** : `Distinct Customers`
   * **[!UICONTROL Time Range]** : `Moving range > Last 90 Days`
   * **[!UICONTROL Time Interval]** : `By Day`

![Clients uniques.](../../assets/Unique_customers_last_7_days.png)<!--{: width="929"}-->

### Nouveaux abonnés

* **Description** : nombre total de nouveaux abonnés acquis sur une période donnée.
* **Définition de mesure** : cette mesure exécute un **Comptage distinct** de `customer_id` à partir de la table `subscriptions` triée par `start_date`.
* **Exemple de rapport** : nouveaux abonnés cette année par mois
   * **[!UICONTROL Metric]** : `New Subscribers`
   * **[!UICONTROL Time Range]** : `1 Year Ago to 0 Days Ago`
   * **[!UICONTROL Time Interval]** : `By Month`

![Abonnés](../../assets/New_Subscribers_This_Year_by_Month.png)<!--{: width="929"}-->

### Clients réguliers

* **Description** : nombre total de clients qui ont passé plusieurs commandes sur une période. Dans un rapport de clients réguliers, vous pouvez utiliser la mesure `Distinct Customers` et la dimension `Customer's Order Number` de votre table `orders`.
* **Mesure utilisée** : `Distinct Customers`
* **Exemple de rapport** : nombre de 2e et 3e achats effectués l’année dernière
   * **[!UICONTROL Metric]** : `Distinct Customers`
   * **[!UICONTROL Time Range]** : `Moving Range > Last Year`
   * **[!UICONTROL Time Interval]** : `By Month`
   * **[!UICONTROL Group By]** : `Customer's Order Number`, puis sélectionnez `2` et `3`

  ![](../../assets/2nd_and_3rd_purchases_last_year.png)

* **Exemple de rapport 2** : nombre de clients réguliers les dernières années
   * **[!UICONTROL Metric]** : `Distinct Customers`
   * **[!UICONTROL Filters]** : `Customer's Order Number Greater Than 1`
   * **[!UICONTROL Time Range]** : `Moving range > Last Year`
   * **[!UICONTROL Time Interval]** : `By Month`

  ![Clients Répétés L’Année Dernière](../../assets/Repeat_customers_last_year.png)<!--{: width="929"}-->

### Clients principaux par nombre de commandes au cours de la durée de vie

* **Description** : liste des principaux clients selon leur nombre total de commandes. Vous obtenez ainsi une liste directe de vos acheteurs les plus fréquents.
* **Mesure utilisée** : `Orders`
* **Exemple de rapport** : 25 premiers clients par nombre de commandes sur toute la durée de vie
   * **[!UICONTROL Metric]** : `Orders`
   * **[!UICONTROL Time Range]** : `All Time`
   * **[!UICONTROL Time Interval]** : `None`
   * **[!UICONTROL Group By]** : `customer_email`
   * **[!UICONTROL Show Top/Bottom]** : 25 premiers triés par commandes

  ![25 premiers clients par commande](../../assets/Top_25_customers_by_lifetime_orders.png)<!--{: width="929"}-->

### Meilleurs clients par chiffre d’affaires sur la durée de vie

* **Description** : liste des principaux clients en fonction des recettes sur la durée de vie.
* **Mesure utilisée** : `Average Lifetime Revenue`
* **Exemple de rapport** : 25 premiers clients par revenu sur la durée de vie
   * **[!UICONTROL Metric]** : `Average Lifetime Revenue`
   * **[!UICONTROL Time Range]** : `All time`
   * **[!UICONTROL Time Interval]** : `None`
   * **[!UICONTROL Group By]** : `customer_email`
   * **[!UICONTROL Show Top Bottom]** : 25 premiers triés par recettes sur la durée de vie

  ![25 premiers clients par chiffre d’affaires](../../assets/top_25_customers_by_lifetime_revneue.png)<!--{: width="929"}-->

### Chiffre d’affaires moyen par cohorte

* **Description** : effectuez le suivi des [recettes de durée de vie moyenne des cohortes distinctes](../dev-reports/lifetime-rev-cohort-analysis.md) d’utilisateurs au fil du temps pour identifier les cohortes les plus performantes. Les cohortes sont regroupées par date courante, comme la date de première commande ou la date de création.
* **Mesure utilisée** : `Revenue`
* **Exemple de rapport** : revenu moyen sur la durée de vie des clients par cohorte
   * **[!UICONTROL Metric]** : `Revenue`
   * **[!UICONTROL Cohort Date]** : `Customer's first order date`
   * **[!UICONTROL Time Interval]** : `Month`
   * **[!UICONTROL Time Period]** : Déplacement d’un ensemble de cohortes des huit cohortes les plus récentes avec au moins quatre mois de données
   * **[!UICONTROL Duration]** : `12 Month(s)`
   * **[!UICONTROL Table]** : `Customer_entity`
   * **[!UICONTROL Perspective]** : Valeur moyenne cumulée par membre de cohorte

  ![ Recettes de la durée de vie client par cohorte](../../assets/Avg_customer_lifetime_revenue_by_cohort.png)<!--{: width="929"}-->

### Clients par utilisation des coupons

* **Description** : nombre de clients acquis qui ont utilisé un code de coupon/réduction. Cela peut vous aider à obtenir une vue claire de vos demandeurs de réduction par rapport aux acheteurs à prix plein.
* **Mesure utilisée** : `New Users`
* **Exemple de rapport** : clients coupon et non-coupon par mois
   * **[!UICONTROL Metric A]** : `Non coupon customers`
   * **[!UICONTROL Metric]** : `New Users`
   * **[!UICONTROL Filters]** : Nombre de commandes de durée de vie du client supérieur à 0 et Nombre de bons de durée de vie du client égal à 0
   * **[!UICONTROL Metric B]** : `Coupon customers`
   * **[!UICONTROL Metric]** : `New Users`
   * **[!UICONTROL Filters]** : nombre de commandes supérieures à 0 de la durée de vie des clients et nombre de bons supérieurs à 0 de la durée de vie des clients
   * **[!UICONTROL Time range]** : `All Time`
   * **[!UICONTROL Time interval]** : `By Month`

  ![Clients par utilisation de coupon](../../assets/Customers_by_coupon_usage.png)<!--{: width="929"}-->

* **Exemple de rapport 2** : pourcentage de clients Bon et non-bons par mois
   * **[!UICONTROL Metric A]** : `Non coupon customers` (masquer la mesure)
      * **[!UICONTROL Metric]** : `New Users`
      * **[!UICONTROL Filters]** : `Customer's Lifetime Number of Orders Greater Than 0` et `Customer's Lifetime Number of Coupons Equal to 0`
   * **[!UICONTROL Metric B]** : `Coupon customers`
      * **[!UICONTROL Metric]** : `New Users`
      * **[!UICONTROL Filters]** : `Customers Lifetime Number of Orders Greater Than 0` et `Customer's Lifetime Number of Coupons Greater Than 0`
   * **[!UICONTROL Time Range]** : `All Time`
   * **[!UICONTROL Time Interval]** : `By Month`
   * **[!UICONTROL Formula]** : `B/(A+B)`

>[!NOTE]
>
> **Masquer toutes les mesures**

![Utilisation du coupon](../../assets/Customers_by_coupon_usage_formula.png)<!--{: width="929"}-->

### Chiffre d’affaires moyen des 30 premiers jours

* **Description** : Moyenne du montant des recettes générées par les clients au cours de leurs 30 premiers jours en tant que client.
* **Description de mesure** : cette mesure exécute une **moyenne** de `Customer's First 30 Day Revenue` à partir de la table `customer_entity` triée par `created_at`.
* **Description du rapport** : moyenne sur tout le temps des 30 premiers jours du chiffre d’affaires du client
* **[!UICONTROL Metric]** : `Average First 30 Day Revenue`
* **[!UICONTROL Time Range]** : `All Time`
* **[!UICONTROL Time Interval]** : `None`

![Chiffre d’affaires moyen des 30 premiers jours](../../assets/Avg_first_30_day_revenue.png)<!--{: width="929"}-->

### Chiffre d’affaires moyen des clients

* **Description** : montant moyen des recettes générées par vos clients au cours de leur vie.
* **Description de la mesure** : cette mesure exécute une **moyenne** de la colonne `Customer's Lifetime Revenue` sur la table `customer_entity` basée sur `created_at`.
* **Description du rapport** : moyenne sur tout le temps des recettes de durée de vie du client
   * **[!UICONTROL Metric]** : `Average Customer Lifetime Revenue`
   * **[!UICONTROL Time Range]** : `All Time`
   * **[!UICONTROL Time Interval]** : `None`

![ Recettes sur la durée de vie du client ](../../assets/Avd_customer_lifetime_revenue_.png)<!--{: width="929"}-->

## Analyse des commandes {#orderanalytics}

### Recettes

* **Description** : la mesure des recettes affiche le total des recettes générées sur une période donnée.
* Cette mesure exécute une **somme** de `grand_total` à partir de la table `sales_flat_order` triée par `created_at`.
* **Exemple de rapport** : Recettes par mois, YTD
   * **[!UICONTROL Metric]** : `Revenue`
   * **[!UICONTROL Time Range]** : `1 Year Ago to 1 Month Ago`
   * **Intervalle de temps** : `By Month`

>[!TIP]
>
>Assurez-vous que le calcul de votre mesure des recettes est cohérent avec la définition dont vous discutez en interne. Par exemple, vous pouvez comptabiliser les recettes provenant des commandes expédiées, convertir les devises de différentes régions ou exclure les taxes. Vous pouvez également utiliser les [ensembles de filtres](../../data-user/reports/ess-manage-data-filters.md) pour assurer la cohérence de toutes les mesures créées sur le même tableau.

![Recettes](../../assets/revenue.png)<!--{: width="929"}-->

### Commandes

* **Description** : nombre total de commandes sur une période donnée. Un rapport Commandes effectue le suivi des modifications du volume des commandes provoquées par les nouvelles offres de produits, les promotions ou tout autre élément susceptible d’augmenter (ou de diminuer) le volume des transactions. Vous voudrez peut-être souvent segmenter cette mesure en fonction de certaines variables pour répondre à vos questions.
* **Définition de mesure** : cette mesure exécute un **décompte** de `entity_id` à partir de la table `sales_flat_order` triée par `created_at`.
* **Exemple de rapport** : commandes par mois, YTD
   * **[!UICONTROL Metric]** : `number of orders`
   * **[!UICONTROL Time Range]** : `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]** : `By Month`

>[!TIP]
>
>Tout comme la mesure des recettes, vous devez avoir [Visionneuses de filtres](../../data-user/reports/ess-manage-data-filters.md) pour exclure les commandes incomplètes, de test ou renvoyées.

![Commandes](../../assets/orders_pic.png)<!--{: width="929"}-->

### Produits commandés

* **Description** : La mesure des produits commandés indique la quantité d’articles vendus sur une période donnée.
* **Définition de mesure** : cette mesure exécute une **somme** de `qty_ordered` à partir de la table `sales_flat_order_item` triée par `created_at`.
* **Exemple de rapport** : articles vendus par mois, YTD
   * **[!UICONTROL Metric]** : `Products ordered`
   * **[!UICONTROL Time Range]** : `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]** : `By Month`

  ![Produits commandés](../../assets/products_ordered_pic1.png)<!--{: width="929"}-->

* Combinez cette mesure à la mesure du nombre de commandes pour calculer le nombre d’articles par commande. Ajoutez ensuite des codes de coupon au rapport afin de déterminer l’impact de vos promotions sur la taille du panier, ou segmentez-les par nouvelles commandes par rapport aux commandes répétées, afin de mieux comprendre le comportement de vos clients.
* **Exemple de rapport** : produits par commande : première commande ou commandes répétées
   * **[!UICONTROL Metric A]** : Produits commandés : première commande
      * **[!UICONTROL Metric]** : `Products ordered`
      * **[!UICONTROL Filter]** : `Customer's order number = 1`
   * **[!UICONTROL Metric B]** : Commandes : première commande
      * **[!UICONTROL Metric]** : `Orders`
      * **[!UICONTROL Filter]** : `Customer's order number = 1`
   * **[!UICONTROL Metric C]** : produits commandés : commandes répétées
      * **[!UICONTROL Metric]** : `Products ordered`
      * **[!UICONTROL Filter]** : `Customer's order number > 1`
   * **[!UICONTROL Metric D]** : Commandes : commandes répétées
      * **[!UICONTROL Metric]** : `Orders`
      * **[!UICONTROL Filter]** : `Customer's order number > 1`
   * **[!UICONTROL Time Range]** : `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]** : `By Week`
   * **[!UICONTROL Formula 1]** : `A/B`
   * **[!UICONTROL Formula 2]** : `C/D`

>[!NOTE]
>
>Décochez toutes les mesures `Multiple Y-Axes box` et `Hide` .

![Produits commandés 2](../../assets/products_ordered_pic2.png)<!--{: width="929"}-->

### Valeur de commande moyenne

* **Description** : Trackez la valeur moyenne des commandes passées sur une période. Utilisez cette mesure pour déterminer rapidement la manière dont la valeur de commande moyenne (AOV) a fluctué en raison de vos efforts marketing, de votre offre de produits et/ou d’autres changements survenus dans votre entreprise.
* **Définition de mesure** : cette mesure exécute une **moyenne** de `grand_total` à partir de la table `sales_flat_order` triée par `created_at`.
* **Exemple de rapport** : AOV par rapport à l’année précédente, YTD
   * **[!UICONTROL Metric]** : `Average order value`
   * **[!UICONTROL Time Range]** : `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]** : `By Month`
   * **[!UICONTROL Perspective]** : `Amount Change vs Previous Year`

  ![AOV](../../assets/aov_pic.png)<!--{: width="929"}-->

### Produits les plus achetés avec des bons

* **Description** : ce rapport fournit des informations sur les produits vendus lorsque vous proposez des promotions ou des bons.
* **Mesure utilisée** : produits commandés
* **Exemple de rapport** : produits les plus achetés avec des coupons
   * **[!UICONTROL Metric]** : `Products ordered`
   * **[!UICONTROL Filter]** : `Order's coupon_code Is Not \[NULL\]`
   * **[!UICONTROL Time Range]** : `All-Time`
   * **[!UICONTROL Time Interval]** : `None`
   * **[!UICONTROL Group By**] : `name` (ou `SKU`, ou tout autre identifiant de produit)
   * **[!UICONTROL Show top/bottom]** : 25 premiers triés par produits commandés

  ![Produits avec coupons](../../assets/prod_coupons_pic.png)<!--{: width="929"}-->

### Durée entre les commandes

* **Description** : testez vos hypothèses et attentes concernant les cycles d’achat de vos clients avec une analyse **durée entre les commandes** qui examine la moyenne (ou la médiane !) durée entre les achats. Dans le graphique ci-dessous, vous pouvez constater que vos meilleurs clients - ceux qui passent plus de trois commandes - effectuent leur deuxième achat en moins de six mois. Les clients qui n’ont pas passé de quatrième commande attendent 14 mois avant d’effectuer un deuxième achat.
* **Définition de mesure** : cette mesure exécute une **moyenne** de `Time since previous order` à partir de `sales_flat_order` ordonnée par `created_at`.
* **Exemple de rapport** :
   * **Mesure 1** : ≤ 3 commandes
      * **[!UICONTROL Metric]** : `Average time between orders`
      * **[!UICONTROL Filter]** : `Customer's lifetime number of orders ≤ 3`
   * **Mesure 2** : > 3 commandes
      * **[!UICONTROL Metric]** : `Average time between orders`
      * **[!UICONTROL Filter]** : `Customer's lifetime number of orders > 3`
   * **[!UICONTROL Time Range]** : `All-Time`
   * **[!UICONTROL Time Interval]** : `None`
   * **[!UICONTROL Group By]**:` Customer's order number (previous-current)`

>[!NOTE]
>
>Décochez la case `Multiple Y-Axes` .

![Intervalle entre les commandes](../../assets/time_bw_orders_pic.png)<!--{: width="929"}-->

## Analyse des dépenses marketing {#mktgspendanalytics}

### Dépenses publicitaires

* **Description** : vous pouvez analyser vos dépenses marketing sur plusieurs périodes et intervalles, par campagnes ou ensembles de publicités, ou sur d’autres segments.
* **Définition de mesure** : cette mesure exécute une Somme sur la colonne des dépenses dans la table `Marketing Spend` triée par la colonne `date`.
* **Exemple de rapport** : dépenses publicitaires par campagne
   * **[!UICONTROL Metric]** : `Ad spend`
   * **[!UICONTROL Time Range]** : `All-Time`
   * **[!UICONTROL Time Interval]** : `None`
   * **[!UICONTROL Group By]** : `campaign`

![Dépenses publicitaires](../../assets/ad_spend.png)<!--{: width="929"}-->

### Impressions publicitaires et clics publicitaires

* **Description** : Outre l’analyse des dépenses publicitaires, vous pouvez analyser vos impressions publicitaires et vos clics publicitaires.
* **Définition de mesure** : cette mesure exécute une Somme sur la colonne des impressions (ou clics) dans la table `Marketing Spend` triée par colonne de date.
* **Exemple de rapport** : ajout d’impressions et de clics publicitaires par jour
   * **[!UICONTROL Metric A]** : `Ad impressions`
   * **[!UICONTROL Metric B]** : `Ad clicks`
   * **[!UICONTROL Time Range]** : `1 Year Ago to 3 Months Ago`
   * **[!UICONTROL Time Interval]** : `By Day`

  ![Impressions de publicité](../../assets/ad_impressions.png)<!--{: width="929"}-->

### Taux de clics (CTR)

* **Description** : à l’aide des mesures d’impressions de publicité et de clics publicitaires que vous avez créées ci-dessus, vous pouvez analyser votre taux de clics publicitaires en fonction de différentes campagnes au fil du temps.
* **Exemple de rapport** : CTR par campagne
   * **[!UICONTROL Metric A]** : `Ad impressions`
   * **[!UICONTROL Metric B]** : `Ad clicks`
   * **[!UICONTROL Time Range]**:`All-Time`
   * **[!UICONTROL Time Interval]** : `None`
   * **[!UICONTROL Formula]** : `B/A`
   * Sélectionnez l’option `%` .
   * **[!UICONTROL Group By]** : `campaign`

>[!NOTE]
>
>Vous pouvez **title** de la formule comme `CTR` et **masquer** toutes les mesures.

![CTR](../../assets/CTR.png)<!--{: width="929"}-->

### Coût par clic (CPC)

* **Description** : à l’aide des mesures de dépenses publicitaires et de clics publicitaires que vous avez créées ci-dessus, vous pouvez analyser votre coût par clic selon différentes campagnes au fil du temps.
* **Exemple de rapport** : CPC par campagne
   * **[!UICONTROL Metric A]** : `Ad spend`
   * **[!UICONTROL Metric B]** : `Ad clicks`
   * **[!UICONTROL Time Range]** : `All-Time`
   * **[!UICONTROL Time Interval]** : `None`
   * **[!UICONTROL Formula]** : `A/B`
   * Sélectionnez l’option `currency` .
   * **[!UICONTROL Group By]** : `campaign`

>[!NOTE]
>
>Vous pouvez **title** de la formule comme `CPC` et **masquer** toutes les mesures.

![CPC](../../assets/CPC.png)<!--{: width="929"}-->

### Clients par source d’acquisition

* **Description** : si vous effectuez le suivi de la source, du support et de la campagne d’une commande à l’aide de [!DNL Google eCommerce], vous pouvez analyser vos clients en fonction de leur source d’acquisition. Cela vous permet d’identifier les sources marketing qui acquièrent des clients et de répondre à des questions telles que &quot;La plupart de vos clients passent-ils leurs premières commandes via [!DNL Google], [!DNL Facebook] ou une autre source ?&quot;
* **Exemple de rapport** : clients par source d’acquisition
   * **[!UICONTROL Metric Used]** : `New Customers`
   * **[!UICONTROL Time Range]** : `All-Time`
   * **[!UICONTROL Time Interval]** : `By Month`
   * **[!UICONTROL Group By]** : `Customer's first order's source`

>[!NOTE]
>
>Consultez [cet article](../analysis/most-value-source-channel.md) pour plus d’exemples de rapports utilisant la source d’acquisition.

![Source d’acquisition](../../assets/acquisition_source.png)<!--{: width="929"}-->

### Clients par moyen d’acquisition et campagne d’acquisition

* **Description** : tout comme vous analysez les clients par source d’acquisition, vous pouvez également analyser vos clients selon le support et la campagne de leur première commande. Cela peut vous aider à répondre à des questions telles que &quot;Quelles campagnes attirent de nouveaux clients ?&quot;
* **Exemple de rapport** : clients par campagne d’acquisition avec support payant
   * **[!UICONTROL Metric Used]** : `New customers`
   * **[!UICONTROL Filter]** : `Customer's first order's medium IN ppc`
   * **[!UICONTROL Time Range]** : `All-Time`
   * **[!UICONTROL Time Interval]** : `None`
   * **[!UICONTROL Group By]** : `Customer's first order's campaign`

>[!NOTE]
>
>Pour le filtre de votre mesure `New Customers`, vous pouvez ajouter tout autre média considéré comme &quot;payant&quot; pour votre entreprise, par exemple le CPC ou le référencement payant.

![Medium d’acquisition](../../assets/acquisition_medium.png)<!--{: width="929"}-->

### Coût d’acquisition client (CAC) ou coût par acquisition (CPA)

* **Description** : Pour analyser le coût d’une campagne, une méthode consiste à n’attribuer tous les coûts qu’aux clients que vous avez acquis au moyen de la campagne.
* **Exemple de rapport** : CAC par campagne
   * **[!UICONTROL Metric A]** : `New customers`
   * **[!UICONTROL Filter]** : `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]** : `Ad Spend`
   * **[!UICONTROL Time Range]** : `All-Time`
   * **[!UICONTROL Time Interval]** : `None`
   * **[!UICONTROL Formula]** : `B/A`
   * Sélectionnez l’option `currency` .
   * **[!UICONTROL Group By]** :
      * Pour la mesure `A`, sélectionnez `Customer's first order's campaign`
      * Pour la mesure `B`, sélectionnez `campaign`

  ![Nouveaux utilisateurs.](../../assets/New_Users_Last_Month.png)

>[!NOTE]
>
>Vous pouvez **title** de la formule comme `CTR` et **masquer** toutes les mesures. Consultez également [cet article](../analysis/roi-ad-camp.md) pour plus d’informations.

![CAC 1](../../assets/New_Users_Last_Month.png)

![CAC 2](../../assets/cac-2.png)

### Valeur de durée de vie par source d’acquisition, moyenne et campagne

* **Description** : tout en analysant le nombre de clients acquis par chaque campagne, vous pouvez analyser le chiffre d’affaires moyen de la durée de vie de ces clients. Vous pouvez ainsi identifier :
   * Si certaines campagnes attirent un grand volume de clients, mais que ces clients ont une faible valeur de durée de vie.
   * Si certaines campagnes attirent un faible volume de clients, mais que ces clients ont une valeur de durée de vie élevée.
* **Exemple de rapport** : commencez par ajouter la mesure `New customers`. Ajoutez ensuite la mesure `Average lifetime revenue`. Sélectionnez la période souhaitée et choisissez `interval` comme `None`. Enfin, sélectionnez l’option `group by` comme `Customer's first order's campaign`.
   * **[!UICONTROL Metric A]** : `New Customers`
   * **[!UICONTROL Filter A]** : `Customer's first order's source` COMME &#39;%google%&#39;
   * **[!UICONTROL Filter B]** : `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]** : `Average lifetime revenue`
   * **[!UICONTROL Filter A]** : `Customer's first order's source` COMME &#39;%google%&#39;
   * **[!UICONTROL Filter B]** : `Customer's first order's medium IN ppc`
   * **[!UICONTROL Time Range]** : `All-Time`
   * **[!UICONTROL Time Interval]** : `None`
   * **[!UICONTROL Group By]** : `Customer's first order's campaign`

>[!NOTE]
>
>Pour les deux filtres, vous pouvez ajouter tout autre média qui est considéré comme étant &quot;payant&quot; pour votre entreprise (par exemple, le CPC ou le référencement payant). Vous pouvez également ajouter toutes les autres sources que vous souhaitez analyser, telles que Facebook. Consultez [cet article](../analysis/roi-ad-camp.md) pour plus d’informations sur CAC, LTV et ROI.

![Valeur de durée de vie par source d’acquisition, moyenne et campagne](../../assets/LTV_2.png)<!--{: width="929"}-->

### Retour sur investissement (ROI)

* **Description** : Pour calculer le ROI par campagne, une méthode consiste à analyser toutes les commandes passées dans la campagne. Cependant, une autre méthode consiste à analyser la valeur de durée de vie des clients acquis par le biais d’une campagne. Pour analyser le ROI, il est important que les noms des campagnes soient cohérents entre vos données de dépenses et vos données transactionnelles. Si vous créez le rapport suivant et qu’il n’existe aucune valeur de ROI en raison de noms de campagne incohérents, vous devrez peut-être examiner le [balisage UTM](../../best-practices/utm-tagging-google.md) que vous avez implémenté.
* **Exemple de rapport** : ROI par campagne
   * **[!UICONTROL Metric A]** : `New Customers`
   * **[!UICONTROL Filter A]** : `Customer's first order's source` COMME &#39;%google%&#39;
   * **[!UICONTROL Filter B]** : `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]** : `Average lifetime revenue`
   * **[!UICONTROL Filter A]** : `Customer's first order's source` COMME &#39;%google%&#39;
   * **[!UICONTROL Filter B]** : `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric C]** : `Ad spend`
   * **[!UICONTROL Time Range]** : `All-Time`
   * **[!UICONTROL Time Interval]** : `None`
   * **[!UICONTROL Formula]** : `(B-(C/A))/(C/A)`
   * Sélectionnez l&#39;option `% `.
   * **[!UICONTROL Group By]** :
      * Pour les mesures `A` et `B`, sélectionnez `Customer's first order's campaign`
      * Pour la mesure `C`, sélectionnez `campaign`

>[!NOTE]
>
>Vous pouvez appeler la formule &quot;ROI&quot; et masquer toutes les mesures. Vous pouvez, en outre, ajuster les filtres dans les mesures afin d’analyser d’autres sources et supports. Consultez également [cette rubrique](../analysis/roi-ad-camp.md) pour plus d’informations sur CAC, LTV et le retour sur investissement.

![ROI 1](../../assets/ROI_1.png)<!--{: width="929"}-->

![ROI 2](../../assets/ROI_2.png)<!--{: width="929"}-->
