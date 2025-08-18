---
title: Rapports annuels, mensuels et hebdomadaires
description: Découvrez comment voir facilement les tendances au fil du temps et changer de perspective pour les périodes que vous souhaitez comparer.
exl-id: 74cf11c3-7ce0-477f-9a28-9d782e5da3d9
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Rapports sur des périodes de temps

>[!NOTE]
>
>Cette rubrique contient des instructions pour les clients qui utilisent l’architecture d’origine et la nouvelle architecture. Vous passez à la [nouvelle architecture](../../administrator/account-management/new-architecture.md) si la section [!DNL _Vues Data Warehouse_] est disponible après avoir sélectionné [!DNL Manage Data] dans la barre d’outils principale.

Report Builder vous permet d’afficher facilement les tendances au fil du temps et de modifier la perspective pour les périodes que vous souhaitez comparer. Cette rubrique explique comment configurer un tableau de bord pour qu’il aille plus loin et vous permette de créer des rapports pour une analyse semaine par semaine, mois par mois et année par année.

![](../../assets/Wow__mom__yoy.png)

Avant de commencer, vous devez examiner les perspectives de manière plus détaillée [ici](../../tutorials/using-visual-report-builder.md) et les options de temps indépendantes [ici](../../tutorials/time-options-visual-rpt-bldr.md).

Cette analyse contient [colonnes calculées avancées](../data-warehouse-mgr/adv-calc-columns.md).

## Colonnes calculées

* **`Sales_flat_order`** table
* **Architecture d’origine :** les colonnes ci-dessous sont créées par un analyste dans le cadre de votre ticket de `[YoY WoW MoM ANALYSIS]`
* `created_at (month-day)`
* `created_at (month)`
* `created_at (day of the month)`
* `created_at (day of the week)`
* `created_at (hour of the day)`

* **Nouvelle architecture :** SQL répertorié ci-dessous avec une photo d’un exemple de création de ce calcul
   * `created_at (month-day)` [!UICONTROL Calculation] : **to_char(A, &#39;mm-jj&#39;)**
   * `created_at (month)` [!UICONTROL Calculation] : **to_char(A, &#39;mm-month&#39;)**
   * `created_at (day of the month)`&lt; [!UICONTROL Calculation] : **to_char(A, &#39;dd&#39;)**
   * `created_at (day of the week)` [!UICONTROL Calculation] : **to_char(A, &#39;d-Day&#39;)**
   * **`created_at (hour of the day)` [!UICONTROL Calculation] : **to_char(A, &#39;hh24&#39;)**
     ![](../../assets/new-arch-create-calc.png)

## Mesures

Aucune.

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Rapports

* Graphique **YoY**
   * [!UICONTROL Metric] : `Number of orders`

   * [!UICONTROL Metric] : `Number of orders`
   * [!UICONTROL Time options] : `Time range (Custom)` : `2 years ago to 1 year ago`

   * [!UICONTROL Show top/bottom] : les plus triés à 100 % par **`created_at (month-day)`***

* `A` de mesure : `This year`
* `B` de mesure : `Last year`
* [!UICONTROL Time period] : `1 year ago to 0 years ago`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by] : `created_at (month-day)`
* 
  [!UICONTROL Chart Type]: `Line`

* **Graphique MoM**
   * [!UICONTROL Metric] : `Number of orders`

   * [!UICONTROL Metric] : `Number of orders`
   * Options de temps : `Time range (Custom)` : `2 months ago to 1 month ago`

   * Afficher en haut/en bas : 100 % les plus populaires, triés par **`created_at (day of month)`***

* `A` de mesure : ce mois-ci*
* `B` de mesure : mois dernier*
* [!UICONTROL Time period] : il y a 1 mois à 0 mois
* 
  [!UICONTROL Interval]: None
* [!UICONTROL Group by] : `created_at (day of month)`
* 
  [!UICONTROL Chart Type]: Line

* **Graphique WoW**
   * [!UICONTROL Metric] : `Number of orders`

   * [!UICONTROL Metric] : `Number of orders`
   * [!UICONTROL Time options] : `Time range (Custom)` : `2 weeks ago to 1 week ago`

   * [!UICONTROL Show top/bottom] : 100 % les plus triés par `created_at (day of week)`

* `A` de mesure : `This week`
* `B` de mesure : `Last week`
* [!UICONTROL Time period] : `1 week ago to 0 weeks ago`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by] : `created_at (day of week)`
* 
  [!UICONTROL Chart Type]: `Line`

* **Graphique DoD**
   * [!UICONTROL Metric] : `Number of orders`

   * [!UICONTROL Metric] : `Number of orders`
   * [!UICONTROL Time options] : `Time range (Custom)` : `2 days ago to 1 day ago`

   * [!UICONTROL Show top/bottom] : 100 % les plus triés par `created_at (hour of day)`

* `A` de mesure : `Today`
* Mesure B : `Yesterday`
* [!UICONTROL Time period] : `1 day ago to 0 days ago`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by] : `created_at (hour of day)`
* 
  [!UICONTROL Chart Type]: `Line`

Après avoir compilé tous les rapports, vous pouvez les organiser selon vos besoins dans le tableau de bord. Le résultat peut ressembler à l’image en haut de cette page.
