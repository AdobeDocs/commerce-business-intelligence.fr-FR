---
title: Rapports annuels, mensuels et hebdomadaires
description: Découvrez comment afficher facilement les tendances au fil du temps et modifier la perspective pour les périodes que vous souhaitez comparer.
exl-id: 74cf11c3-7ce0-477f-9a28-9d782e5da3d9
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Création de rapports au fil du temps

>[!NOTE]
>
>Cette rubrique contient des instructions destinées aux clients qui utilisent l’architecture d’origine et la nouvelle architecture. Vous êtes sur la page [nouvelle architecture](../../administrator/account-management/new-architecture.md) si vous disposez de la variable [!DNL _Vues Data Warehouse_] section disponible après sélection [!DNL Manage Data] dans la barre d’outils principale.

Le Créateur de rapports vous permet d’afficher facilement les tendances au fil du temps et de modifier la perspective pour les périodes que vous souhaitez comparer. Cette rubrique explique comment configurer un tableau de bord pour qu’il s’approfondisse afin que vous puissiez créer des rapports pour une analyse d’une semaine à l’autre, d’un mois à l’autre et d’une année à l’autre.

![](../../assets/Wow__mom__yoy.png)

Avant de commencer, vous devez examiner les perspectives plus en détail. [here](../../tutorials/using-visual-report-builder.md) et options d’heure indépendantes [here](../../tutorials/time-options-visual-rpt-bldr.md).

Cette analyse contient [colonnes calculées avancées](../data-warehouse-mgr/adv-calc-columns.md).

## Colonnes calculées

* **`Sales_flat_order`** table
* **Architecture originale :** les colonnes ci-dessous sont créées par un analyste dans le cadre de votre `[YoY WoW MoM ANALYSIS]` ticket
* `created_at (month-day)`
* `created_at (month)`
* `created_at (day of the month)`
* `created_at (day of the week)`
* `created_at (hour of the day)`

* **Nouvelle architecture :** SQL répertorié ci-dessous avec la photo d’un exemple pour créer ce calcul
   * `created_at (month-day)` [!UICONTROL Calculation]: **to_char(A, &#39;mm-dd&#39;)**
   * `created_at (month)` [!UICONTROL Calculation]: **to_char(A, &#39;mm-month&#39;)**
   * `created_at (day of the month)`&lt; [!UICONTROL Calculation]: **to_char(A, &#39;dd&#39;)**
   * `created_at (day of the week)` [!UICONTROL Calculation]: **to_char(A, &#39;d-Day&#39;)**
   * **`created_at (hour of the day)` [!UICONTROL Calculation]: **to_char(A, &#39;hh24&#39;)**
     ![](../../assets/new-arch-create-calc.png)

## Mesures

Aucun.

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes comme dimensions aux mesures ;](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Rapports

* **Graphique YoY**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 years ago to 1 year ago`

   * [!UICONTROL Show top/bottom]: 100 % supérieurs triés par **`created_at (month-day)`***

* Mesure `A`: `This year`
* Mesure `B`: `Last year`
* [!UICONTROL Time period]: `1 year ago to 0 years ago`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (month-day)`
* 
  [!UICONTROL Chart Type]: `Line`

* **Graphique MoM**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * Options d’heure : `Time range (Custom)`: `2 months ago to 1 month ago`

   * Afficher en haut/en bas : les 100 % supérieurs triés par **`created_at (day of month)`***

* Mesure `A`: ce mois*
* Mesure `B`: mois dernier*
* [!UICONTROL Time period]: il y a un mois à 0 mois
* 
  [!UICONTROL Interval]: None
* [!UICONTROL Group by]: `created_at (day of month)`
* 
  [!UICONTROL Chart Type]: Line

* **Graphique W**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 weeks ago to 1 week ago`

   * [!UICONTROL Show top/bottom]: 100 % supérieurs triés par `created_at (day of week)`

* Mesure `A`: `This week`
* Mesure `B`: `Last week`
* [!UICONTROL Time period]: `1 week ago to 0 weeks ago`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (day of week)`
* 
  [!UICONTROL Chart Type]: `Line`

* **Graphique DoD**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 days ago to 1 day ago`

   * [!UICONTROL Show top/bottom]: 100 % supérieurs triés par `created_at (hour of day)`

* Mesure `A`: `Today`
* Mesure B : `Yesterday`
* [!UICONTROL Time period]: `1 day ago to 0 days ago`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (hour of day)`
* 
  [!UICONTROL Chart Type]: `Line`

Après avoir compilé tous les rapports, vous pouvez les organiser dans le tableau de bord suivant vos besoins. Le résultat peut ressembler à l’image en haut de cette page.
