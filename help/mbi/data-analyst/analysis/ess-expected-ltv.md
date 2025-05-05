---
title: Analyse de base de la valeur de durée de vie attendue (LTV)
description: Découvrez comment créer des analyses pour comprendre la valeur de durée de vie de vos clients actuels et comment la valeur de durée de vie augmente avec plus de commandes.
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Analyse de la valeur de durée de vie attendue

Prévoir la valeur de durée de vie des clients lorsqu’ils passent plus de commandes est l’un des aspects les plus importants de toute entreprise de toute taille.

Vous trouverez ci-dessous les étapes nécessaires à la création d’analyses afin de comprendre la valeur de durée de vie de vos clients actuels et de prévoir l’augmentation de la valeur de durée de vie avec davantage de commandes.

![valeur de durée de vie attendue](../../assets/expected_ltv_720.png)

## Création d’une mesure

La première étape consiste à créer une mesure en procédant comme suit :
* Accédez à **[!UICONTROL Manage Data > Metrics]**
   * Affichez le **[!UICONTROL Avg lifetime revenue]** existant.

  >[!NOTE]
  >
  >Le tableau sur lequel cette mesure est construite (probablement `customer_entity` ou `sales_order` selon la capacité de votre boutique à accepter le passage en caisse des invités).

   * Cliquez sur **[!UICONTROL Create New Metric]** et sélectionnez le tableau ci-dessus.
   * Cette mesure exécute une **médiane** sur la colonne `Customer's lifetime revenue`, triée par `created_at`.
      * [!UICONTROL Filters] :
         * Ajoutez le `Customers we count (Saved Filter Set)` (ou `Registered accounts we count`)

   * Attribuez un nom à la mesure, par exemple `Median lifetime revenue`.

## Création de votre tableau de bord

Une fois la mesure créée, vous pouvez **créer un tableau de bord** en procédant comme suit :
* Accédez à **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* Attribuez au tableau de bord un nom tel que `Expected LTV`.

* C’est là que vous créez et ajoutez tous les rapports.

## Création de rapports

>[!NOTE]
>
>Sur **[!UICONTROL Time Period:]**, la période de chaque rapport est répertoriée comme `All-time`. N’hésitez pas à modifier ce paramètre en fonction de vos besoins d’analyse. Adobe recommande que tous les rapports de ce tableau de bord couvrent la même période, par exemple `All time`, `Year-to-date` ou `Last 365 days`.

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric] : `Avg lifetime revenue`
   * [!UICONTROL Time period] : `All time`
   * &#x200B;

     [!UICONTROL Intervalle]: `None`
   * [!UICONTROL Chart Type] : `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric] : `Avg lifetime revenue`
      * Ajoutez [!UICONTROL filters] :
         * [`A`] `Customer's group code` **Not Equal To** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **Supérieur à**`0`

   * [!UICONTROL Time period] : `All time`
   * &#x200B;

     [!UICONTROL Intervalle]: `None`
   * [!UICONTROL Chart Type] : `Number (scalar)`

* **[!UICONTROL Average and Median LTV]**
   * Mesure `1` : `Avg lifetime revenue`
   * Mesure `2` : `Median lifetime revenue`
   * [!UICONTROL Time period] : `All time`
   * [!UICONTROL Interval] : `By Month`
   * &#x200B;

     [!UICONTROL Type de graphique]: `Line`
   * Décochez `Multiple Y-Axes`

* **LTV par nombre de commandes sur toute la durée de vie**
   * Mesure `1` : `Avg lifetime revenue`
   * Mesure `2` : `New customers`
   * [!UICONTROL Time period] : `All time`
   * &#x200B;

     [!UICONTROL Intervalle]: `None`
   * [!UICONTROL Group by] : `Customer's lifetime number of orders`
   * &#x200B;

     [!UICONTROL Type de graphique]: `Line`

  >[!NOTE]
  >
  >N’ajoutez pas toutes les valeurs pour `Customer's lifetime number of orders`. Au lieu de cela, observez un point où le nombre de Nouveaux clients atteint un petit nombre et ajoutez manuellement le nombre de commandes de durée de vie de chaque client à ce point. Par exemple, s&#39;il y a 200 clients dans une commande, 75 à deux, 15 à trois et 3 à quatre, ajoutez *1, 2 et 3*.

* Ajoutez le rapport [!UICONTROL Avg customer lifetime revenue by cohort] existant.

Une fois les rapports créés, reportez-vous à l’image dans la partie supérieure de cette rubrique pour savoir comment organiser les rapports sur votre tableau de bord.
