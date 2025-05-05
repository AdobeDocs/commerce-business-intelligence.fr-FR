---
title: Analyse du code de bon (de base)
description: Découvrez les performances des coupons de votre entreprise est un moyen intéressant de segmenter vos commandes et de mieux comprendre les habitudes des clients.
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: d8fc96a58b72c601a5700f35ea1f3dc982d76571
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# Analyse de base du code de bon

Comprendre les performances des coupons de votre entreprise est un moyen intéressant de segmenter vos commandes et de mieux comprendre les habitudes des clients.

Cette rubrique décrit les étapes nécessaires à la création de cette analyse pour comprendre les performances des clients achetés par coupon, afficher les tendances et suivre l’utilisation du code de coupon individuel.

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## Prise en main

Tout d’abord, une note sur le suivi des codes de coupon. Si un client a appliqué un coupon à une commande, trois choses se produisent :

* Une remise est répercutée dans le montant `base_grand_total` (votre mesure `Revenue` dans Commerce Intelligence)
* Le code de coupon est stocké dans le champ `coupon_code` . Si ce champ est NULL (vide), aucun coupon n’est associé à la commande.
* La valeur actualisée est stockée dans `base_discount_amount`. Selon votre configuration, cette valeur peut apparaître négative ou positive.

Depuis Commerce 2.4.7, un client peut appliquer plusieurs codes de bon à une commande. Dans ce cas :

* Tous les codes de coupon appliqués sont stockés dans le champ `coupon_code` de `sales_order_coupons`. Le premier code de coupon appliqué est également stocké dans le champ `coupon_code` de `sales_order`. Si ce champ est NULL (vide), aucun coupon n’est associé à la commande.

## Création d’une mesure

La première étape consiste à créer une mesure en procédant comme suit :

* Accédez à **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* Sélectionnez le `sales_order`.
* Cette mesure exécute une **Somme** sur la colonne **base_discount_amount**, triée par **created_at**.
   * [!UICONTROL Filters] :
      * Ajouter le `Orders we count` (jeu de filtres enregistrés)
      * Ajoutez ce qui suit :
         * `coupon_code`**IS NOT**`[NULL]`
      * Attribuez un nom à la mesure, par exemple `Coupon discount amount`.

## Création de votre tableau de bord

* Une fois la mesure créée :
   * Accédez à [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
   * Attribuez au tableau de bord un nom tel que `_Coupon Analysis_`.

* C’est là que vous créez et ajoutez tous les rapports.

## Création de rapports

* **Nouveaux rapports :**

>[!NOTE]
>
>Le [!UICONTROL Time Period]** pour chaque rapport est répertorié comme `All-time`. N’hésitez pas à modifier ce paramètre en fonction de vos besoins d’analyse. Adobe recommande que tous les rapports de ce tableau de bord couvrent la même période, par exemple `All time`, `Year-to-date` ou `Last 365 days`.

* **Commandes avec coupons**
   * &#x200B;

     [!UICONTROL Mesure]: `Orders`
      * Ajouter un filtre :
         * [`A`] `coupon_code` **IS NOT** `[NULL]`

   * [!UICONTROL Time period] : `All time`
   * &#x200B;

     [!UICONTROL Intervalle]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **Commandes sans coupons**
   * &#x200B;

     [!UICONTROL Mesure]: `Orders`
      * Ajouter un filtre :
         * [`A`] `coupon_code` **IS** `[NULL]`

   * [!UICONTROL Time period] : `All time`
   * &#x200B;

     [!UICONTROL Intervalle]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **Chiffre d&#39;affaires net des commandes avec coupons**
   * &#x200B;

     [!UICONTROL Mesure]: `Revenue`
      * Ajouter un filtre :
         * [`A`] `coupon_code` **IS NOT** `[NULL]`

   * [!UICONTROL Time period] : `All time`
   * &#x200B;

     [!UICONTROL Intervalle]: `None`
   * [!UICONTROL Chart type] : `Number (scalar)`

* **Remises sur les coupons**
   * [!UICONTROL Metric] : `Coupon discount amount`
   * [!UICONTROL Time period] : `All time`
   * &#x200B;

     [!UICONTROL Intervalle]: `None`
   * [!UICONTROL Chart type] : `Number (scalar)`

* **Chiffre d&#39;affaires moyen de la durée de vie : clients acquis par un bon**
   * [!UICONTROL Metric] : `Avg lifetime revenue`
      * Ajouter un filtre :
         * [`A`] `Customer's first order's coupon_code` **IS NOT** `[NULL]`

   * [!UICONTROL Time period] : `All time`
   * &#x200B;

     [!UICONTROL Intervalle]: `None`
   * [!UICONTROL Chart type] : `Number (scalar)`

* **Chiffre d&#39;affaires moyen de la durée de vie : clients non-coupons acquis**
   * [!UICONTROL Metric] : `Avg lifetime revenue`
      * Ajouter un filtre :
         * [A] `Customer's first order's coupon_code` **IS**`[NULL]`

   * [!UICONTROL Time period] : `All time`
   * &#x200B;

     [!UICONTROL Intervalle]: `None`
   * [!UICONTROL Chart type] : `Number (scalar)`

* **Détails de l’utilisation du coupon (premières commandes)**
   * Mesure `1` : `Orders`
      * Ajouter un filtre :
         * [`A`] `coupon_code` **IS NOT**`[NULL]`
         * [`B`] `Customer's order number` **Égal à** `1`

   * Mesure `2` : `Revenue`
      * Ajouter un filtre :
         * [`A`] `coupon_code` **IS NOT**`[NULL]`
         * [`B`] `Customer's order number` **Égal à** `1`

      * Renommer : `Net revenue`

   * Mesure `3` : `Coupon discount amount`
      * Ajouter un filtre :
         * [`A`] `coupon_code` **IS NOT**`[NULL]`
         * [`B`] `Customer's order number` **Égal à** `1`

   * Créer une formule : `Gross revenue`
      * [!UICONTROL Formula] : `(B – C)`
      * &#x200B;

        [!UICONTROL Format]: `Currency`

   * Créer une formule :**% réduits**
      * Formule : `(C / (B - C))`
      * &#x200B;

        [!UICONTROL Format]: `Percentage`

   * Créer une formule : `Average order discount`
      * [!UICONTROL Formula] : `(C / A)`
      * &#x200B;

        [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Time period] : `All time`
   * &#x200B;

     [!UICONTROL Intervalle]: `None`
   * &#x200B;

     [!UICONTROL Type de graphique]: `Table`

* **Chiffre d&#39;affaires moyen de la durée de vie par coupon de première commande**
   * [!UICONTROL Metric] : **Chiffre d’affaires moyen de la durée de vie**
      * Ajouter un filtre :
         * [`A`] `coupon_code` **IS**`[NULL]`

   * [!UICONTROL Time period] : `All time`
   * &#x200B;

     [!UICONTROL Intervalle]: `None`
   * [!UICONTROL Chart type] : `Number (scalar)`

* **Détails de l’utilisation du coupon (premières commandes)**
   * [!UICONTROL Metric] : `Avg lifetime revenue`
      * Ajouter un filtre :
         * [`A`] `Customer's first order's coupon_code` **IS NOT** `[NULL]`

   * [!UICONTROL Time period] : `All time`
   * &#x200B;

     [!UICONTROL Intervalle]: `None`
   * [!UICONTROL Group by] : `Customer's first order's coupon_code`
   * &#x200B;

     [!UICONTROL Type de graphique]: **Column**

* **Nouveaux clients par acquisition de coupon/non-coupon**
   * Mesure `1` : `New customers`
      * Ajouter un filtre :
         * [`A`] `Customer's first order's coupon_code` **IS NOT** `[NULL]`

      * [!UICONTROL Rename] : `Coupon acquisition customer`

   * Mesure `2` : `New customers`
      * Ajouter un filtre :
         * [`A`] `coupon_code` **IS**`[NULL]`

      * [!UICONTROL Rename] : `Non-coupon acquisition customer`

   * [!UICONTROL Time period] : `All time`
   * [!UICONTROL Interval] : `By Month`
   * [!UICONTROL Chart type] : `Stacked Column`

Une fois les rapports créés, reportez-vous à l’image dans la partie supérieure de cette rubrique pour savoir comment organiser les rapports sur votre tableau de bord.

>[!NOTE]
>
>Depuis Adobe Commerce 2.4.7, les clients peuvent utiliser les tables **quote_coupons** et **ventes_order_coupons** pour obtenir des informations sur la manière dont les clients utilisent plusieurs coupons.

![](../../assets/multicoupon_relationship_tables.png)
