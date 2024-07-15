---
title: Seuil de livraison gratuit
description: Découvrez comment configurer un tableau de bord qui suit les performances de votre seuil de livraison gratuite.
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
role: Admin,  User
feature: Data Warehouse Manager, Dashboards, Reports
source-git-commit: 6bdbdbcc652d476fa2a22589ac99678d5855e6fe
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# Livraison gratuite

>[!NOTE]
>
>Cette rubrique contient des instructions destinées aux clients qui utilisent l’architecture d’origine et la nouvelle architecture. Vous utilisez la nouvelle architecture si la section `Data Warehouse Views` est disponible après avoir sélectionné `Manage Data` dans la barre d’outils principale.

Cette rubrique explique comment configurer un tableau de bord qui suit les performances de votre seuil de livraison gratuite. Ce tableau de bord, illustré ci-dessous, est un excellent moyen de tester A/B deux seuils de livraison gratuits. Par exemple, votre société peut ne pas savoir si vous devez proposer la livraison gratuite à 50 ou 100 $. Vous devez effectuer un test A/B de deux sous-ensembles aléatoires de vos clients et effectuer l’analyse dans [!DNL Commerce Intelligence].

Avant de commencer, vous souhaitez identifier deux périodes distinctes au cours desquelles vous disposez de valeurs différentes pour le seuil de livraison gratuite de votre magasin.

![](../../assets/free_shipping_threshold.png)

Cette analyse contient [des colonnes calculées avancées](../data-warehouse-mgr/adv-calc-columns.md).

## Colonnes calculées

Si vous utilisez l’architecture d’origine (par exemple, si vous ne disposez pas de l’option `Data Warehouse Views` dans le menu `Manage Data`), contactez l’équipe de support pour créer les colonnes ci-dessous. Sur la nouvelle architecture, ces colonnes peuvent être créées à partir de la page `Manage Data > Data Warehouse`. Vous trouverez ci-dessous des instructions détaillées.

* **`sales_flat_order`** table
   * Ce calcul crée des intervalles par incréments par rapport aux tailles de panier standard. Cela peut être compris entre 5, 10, 50 et 100.

* **`Order subtotal (buckets)`** Architecture d’origine : créée par un analyste dans le cadre de votre ticket `[FREE SHIPPING ANALYSIS]`
* **`Order subtotal (buckets)`** Nouvelle architecture :
   * Comme mentionné ci-dessus, ce calcul crée des intervalles par incréments par rapport aux tailles de panier standard. Si vous disposez d’une colonne de sous-total native telle que `base_subtotal`, elle peut être utilisée comme base de cette nouvelle colonne. Dans le cas contraire, il peut s’agir d’une colonne calculée qui exclut les frais d’expédition et les remises des recettes.

  >[!NOTE]
  >
  >Les tailles de &quot;compartiment&quot; dépendent de ce qui vous convient en tant que client. Vous pouvez commencer par votre `average order value` et créer des intervalles inférieurs ou supérieurs à cette valeur. Lorsque vous regardez le calcul ci-dessous, vous pouvez facilement copier une partie de la requête, la modifier et créer des intervalles supplémentaires. L’exemple est effectué par incréments de 50.

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal`, ou `calculated column`, `Datatype` : `Integer`
   * [!UICONTROL Calculation] : `case when A >= 0 and A<=200 then 0 - 200`
quand `A< 200` et `A <= 250` puis `201 - 250`
quand `A<251` et `A<= 300` alors `251 - 300`
quand `A<301` et `A<= 350` alors `301 - 350`
quand `A<351` et `A<=400` alors `351 - 400`
quand `A<401` et `A<=450` alors `401 - 450`
else &quot;over 450&quot;
end


## Mesures

Aucune nouvelle mesure!!!

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Rapports

* **Valeur de commande moyenne avec règle de livraison A**
   * [!UICONTROL Metric] : `Average order value`

* Mesure `A` : `Average Order Value`
* [!UICONTROL Time period] : `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **Nombre de commandes par sous-total de lots avec la règle d’expédition A**
   * [!UICONTROL Metric] : `Number of orders`

  >[!NOTE]
  >
  >Vous pouvez couper la fin de la queue en affichant les `X` `sorted by` `Order subtotal` supérieurs (intervalles) dans le `Show top/bottom`.

* Mesure `A` : `Number of orders`
* [!UICONTROL Time period] : `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by] : `Order subtotal (buckets)`
* 
  [!UICONTROL Chart Type]: `Column`

* **Pourcentage de commandes par sous-total avec la règle d’expédition A**
   * [!UICONTROL Metric] : `Number of orders`

   * [!UICONTROL Metric] : `Number of orders`
   * 
     [!UICONTROL Groupe par]: `Independent`
   * [!UICONTROL Formula] : `(A / B)`
   * 
     [!UICONTROL Format]: `%`

* Mesure `A` : `Number of orders by subtotal (hide)`
* Mesure `B` : `Total number of orders (hide)`
* [!UICONTROL Formula] : `% of orders`
* [!UICONTROL Time period] : `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by] : `Order subtotal (buckets)`
* 
  [!UICONTROL Chart Type]: `Line`

* **Pourcentage de commandes dont le sous-total dépasse la règle d’expédition A**
   * [!UICONTROL Metric] : `Number of orders`
   * 
     [!UICONTROL Perspective]: `Cumulative`

   * [!UICONTROL Metric] : `Number of orders`
   * 
     [!UICONTROL Groupe par]: `Independent`

   * [!UICONTROL Formula] : `1- (A / B)`
   * 
     [!UICONTROL Format]: `%`

* Mesure `A` : `Number of orders by subtotal`
* Mesure `B` : `Total number of orders (hide)`
* [!UICONTROL Formula] : `% of orders`
* [!UICONTROL Time period] : `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by] : `Order subtotal (buckets)`
* 
  [!UICONTROL Chart Type]: `Line`


Répétez les étapes et les rapports ci-dessus pour l’expédition B et la période avec la règle d’expédition B.

Après avoir compilé tous les rapports, vous pouvez les organiser dans le tableau de bord suivant vos besoins. Le résultat peut ressembler à l’image en haut de cette page.
