---
title: Analyse de base de la valeur de durée de vie attendue (LTV)
description: Découvrez comment créer des analyses pour comprendre la valeur de durée de vie de vos clients actuels et prévoir comment la valeur de durée de vie augmente avec plus de commandes.
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# Analyse de la valeur de durée de vie attendue

Prévoir la valeur de durée de vie des clients lorsqu’ils passent plus de commandes est l’un des aspects les plus importants de toute entreprise de toute taille.

Vous trouverez ci-dessous les étapes nécessaires à la création d’analyses afin de comprendre la valeur de durée de vie de vos clients actuels et de prévoir l’augmentation de la valeur de durée de vie avec davantage de commandes.

![valeur attendue](../../assets/expected_ltv_720.png)

## Création d’une mesure

La première étape consiste à créer une mesure en procédant comme suit :
* Accédez à **[!UICONTROL Manage Data > Metrics]**
   * Afficher les **[!UICONTROL Avg lifetime revenue]**.

   >[!NOTE]
   >
   >Le tableau sur lequel cette mesure est construite (probablement `customer_entity` ou `sales_order` selon la capacité de votre boutique à accepter le passage en caisse de l’invité.)

   * Cliquez sur **[!UICONTROL Create New Metric]** et sélectionnez le tableau ci-dessus.
   * Cette mesure effectue une **Médiane** sur le `Customer's lifetime revenue` colonne, triée par `created_at`.
      * [!UICONTROL Filters]:
         * Ajoutez la variable `Customers we count (Saved Filter Set)` (ou `Registered accounts we count`)
   * Attribuez un nom à la mesure, par exemple `Median lifetime revenue`.



## Création de votre tableau de bord

Une fois la mesure créée, vous pouvez **création d’un tableau de bord** en procédant comme suit :
* Accédez à **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* Attribuez au tableau de bord un nom tel que `Expected LTV`.

* C’est là que vous créez et ajoutez tous les rapports.

## Création de rapports

>[!NOTE]
>
>Activé **[!UICONTROL Time Period:]**, la période de chaque rapport est répertoriée comme `All-time`. N’hésitez pas à modifier ce paramètre en fonction de vos besoins d’analyse. Adobe recommande que tous les rapports de ce tableau de bord couvrent la même période, comme par exemple `All time`, `Year-to-date`ou `Last 365 days`.

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Intervalle]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Ajouter [!UICONTROL filters]:
         * [`A`] `Customer's group code` **Différent de** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **Supérieur à**`0`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Intervalle]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`


* **[!UICONTROL Average and Median LTV]**
   * Mesure `1`: `Avg lifetime revenue`
   * Mesure `2`: `Median lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * 
      [!UICONTROL Type de graphique]: `Line`
   * Décocher `Multiple Y-Axes`

* **LTV par nombre de commandes au cours de la durée de vie**
   * Mesure `1`: `Avg lifetime revenue`
   * Mesure `2`: `New customers`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Intervalle]: `None`
   * [!UICONTROL Group by]: `Customer's lifetime number of orders`
   * 

      [!UICONTROL Type de graphique]: `Line`
   >[!NOTE]
   >
   >N’ajoutez pas toutes les valeurs pour `Customer's lifetime number of orders`. Au lieu de cela, observez un point où le nombre de Nouveaux clients atteint un petit nombre et ajoutez manuellement le nombre de commandes de durée de vie de chaque client à ce point. Par exemple, s’il y a 200 clients à une commande, 75 à deux, 15 à trois et 3 à quatre, ajoutez *1, 2 et 3*.

* Ajoutez le [!UICONTROL Avg customer lifetime revenue by cohort] rapport.

Une fois les rapports créés, reportez-vous à l’image en haut de cette rubrique pour savoir comment organiser les rapports sur votre tableau de bord.
