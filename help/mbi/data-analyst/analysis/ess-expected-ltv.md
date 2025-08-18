---
title: Analyse de la valeur de durée de vie prévue (VVC) (de base)
description: Découvrez comment créer des analyses pour comprendre la valeur de durée de vie de vos clients actuels et prévoir la façon dont la valeur de durée de vie augmente avec le nombre de commandes.
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Analyse de la valeur de durée de vie attendue

Prévoir la valeur à vie des clients lorsqu&#39;ils passent plus de commandes est l&#39;un des aspects les plus importants de toute entreprise, quelle que soit sa taille.

Vous trouverez ci-dessous les étapes de création d&#39;analyses pour comprendre la valeur de durée de vie de vos clients actuels et prévoir comment la valeur de durée de vie augmente avec le nombre de commandes.

![valeur de durée de vie attendue](../../assets/expected_ltv_720.png)

## Création d’une mesure

La première étape consiste à créer une mesure en procédant comme suit :
* Accéder à **[!UICONTROL Manage Data > Metrics]**
   * Affichez le **[!UICONTROL Avg lifetime revenue]** existant.

  >[!NOTE]
  >
  >Le tableau sur lequel cette mesure est construite (probablement `customer_entity` ou `sales_order` selon la capacité de votre magasin à accepter le passage en caisse des invités).

   * Cliquez sur **[!UICONTROL Create New Metric]** et sélectionnez le tableau ci-dessus.
   * Cette mesure effectue une **Médiane** sur la colonne `Customer's lifetime revenue`, classée par `created_at`.
      * [!UICONTROL Filters] :
         * Ajouter le `Customers we count (Saved Filter Set)` (ou la `Registered accounts we count`)

   * Attribuez un nom à la mesure, par exemple `Median lifetime revenue`.

## Création de votre tableau de bord

Une fois la mesure créée, vous pouvez **créer un tableau de bord** en procédant comme suit :
* Accédez à **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* Attribuez un nom tel que `Expected LTV` au tableau de bord.

* C’est là que vous créez et ajoutez tous les rapports.

## Création de rapports

>[!NOTE]
>
>Au **[!UICONTROL Time Period:]**, la période de chaque rapport est répertoriée comme `All-time`. N’hésitez pas à modifier ce paramètre en fonction de vos besoins d’analyse. Adobe recommande que tous les rapports de ce tableau de bord couvrent la même période, par exemple `All time`, `Year-to-date` ou `Last 365 days`.

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric] : `Avg lifetime revenue`
   * [!UICONTROL Time period] : `All time`
   * &#x200B;
     [!UICONTROL Intervalle]: `None`
   * [!UICONTROL Chart Type] : `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric] : `Avg lifetime revenue`
      * Ajouter un [!UICONTROL filters] :
         * [`A`] `Customer's group code` **Différent De** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **Supérieur À**`0`

   * [!UICONTROL Time period] : `All time`
   * &#x200B;
     [!UICONTROL Intervalle]: `None`
   * [!UICONTROL Chart Type] : `Number (scalar)`

* **[!UICONTROL Average and Median LTV]**
   * `1` de mesure : `Avg lifetime revenue`
   * `2` de mesure : `Median lifetime revenue`
   * [!UICONTROL Time period] : `All time`
   * [!UICONTROL Interval] : `By Month`
   * &#x200B;
     [!UICONTROL Type de graphique]: `Line`
   * Décocher la `Multiple Y-Axes`

* **LTV par nombre de commandes sur la durée de vie**
   * `1` de mesure : `Avg lifetime revenue`
   * `2` de mesure : `New customers`
   * [!UICONTROL Time period] : `All time`
   * &#x200B;
     [!UICONTROL Intervalle]: `None`
   * [!UICONTROL Group by] : `Customer's lifetime number of orders`
   * &#x200B;
     [!UICONTROL Type de graphique]: `Line`

  >[!NOTE]
  >
  >N’ajoutez pas toutes les valeurs de `Customer's lifetime number of orders`. Examinez plutôt un point où le nombre de nouveaux clients atteint un petit nombre et ajoutez manuellement à ce point le nombre de commandes correspondant à la durée de vie de chaque client. Par exemple, s’il y a 200 clients à une commande, 75 à deux, 15 à trois et 3 à quatre, ajoutez *1, 2 et 3*.

* Ajoutez le rapport de [!UICONTROL Avg customer lifetime revenue by cohort] existant.

Une fois les rapports créés, reportez-vous à l’image en haut de cette rubrique pour savoir comment organiser les rapports sur votre tableau de bord.
