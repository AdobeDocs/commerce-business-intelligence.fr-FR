---
title: Seuil de livraison gratuite
description: Découvrez comment configurer un tableau de bord qui suit les performances de votre seuil d’expédition gratuite.
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
role: Admin,  User
feature: Data Warehouse Manager, Dashboards, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Livraison gratuite

>[!NOTE]
>
>Cette rubrique contient des instructions pour les clients qui utilisent l’architecture d’origine et la nouvelle architecture. Vous passez à la nouvelle architecture si la section `Data Warehouse Views` est disponible après avoir sélectionné `Manage Data` dans la barre d’outils principale.

Cette rubrique explique comment configurer un tableau de bord qui suit les performances de votre seuil d’expédition gratuite. Ce tableau de bord, illustré ci-dessous, est un excellent moyen de tester A/B deux seuils d’expédition gratuite. Par exemple, votre entreprise peut ne pas savoir si vous devez offrir la livraison gratuite à 50 $ ou 100 $. Vous devez effectuer un test A/B de deux sous-ensembles aléatoires de vos clients et effectuer l’analyse dans [!DNL Commerce Intelligence].

Avant de commencer, vous devez identifier deux périodes distinctes pendant lesquelles vous avez défini des valeurs différentes pour le seuil d’expédition gratuite de votre magasin.

![Graphique présentant l’analyse du seuil d’expédition gratuite et la répartition de la valeur de commande](../../assets/free_shipping_threshold.png)

Cette analyse contient [colonnes calculées avancées](../data-warehouse-mgr/adv-calc-columns.md).

## Colonnes calculées

Si vous utilisez l’architecture d’origine (par exemple, si vous n’avez pas l’option `Data Warehouse Views` sous le menu `Manage Data` ), vous devez contacter l’équipe d’assistance pour créer les colonnes ci-dessous. Sur la nouvelle architecture, ces colonnes peuvent être créées à partir de la page `Manage Data > Data Warehouse` . Des instructions détaillées sont données ci-dessous.

* **`sales_flat_order`** table
   * Ce calcul crée des regroupements par incréments par rapport à vos tailles de panier standard. Elle peut être comprise entre 5, 10, 50 et 100

* **`Order subtotal (buckets)`** Architecture originale : créée par un analyste dans le cadre de votre ticket `[FREE SHIPPING ANALYSIS]`
* **`Order subtotal (buckets)`** nouvelle architecture :
   * Comme mentionné ci-dessus, ce calcul crée des compartiments par incréments par rapport à vos tailles de panier standard. Si vous avez une colonne de sous-total native telle que `base_subtotal`, elle peut être utilisée comme base de cette nouvelle colonne. Dans le cas contraire, il peut s’agir d’une colonne calculée qui exclut les frais d’expédition et les remises du chiffre d’affaires.

  >[!NOTE]
  >
  >Les tailles des « compartiments » dépendent de ce qui est approprié pour vous en tant que client. Vous pouvez commencer par votre `average order value` et créer des regroupements inférieurs ou supérieurs à ce montant. Lorsque vous examinez le calcul ci-dessous, vous voyez comment copier facilement une partie de la requête, la modifier et créer des regroupements supplémentaires. L’exemple est réalisé par incréments de 50.

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal` ou `calculated column` `Datatype` : `Integer`
   * [!UICONTROL Calculation] : `case when A >= 0 and A<=200 then 0 - 200`
lorsque `A< 200` et `A <= 250` puis `201 - 250`
lorsque `A<251` et `A<= 300` puis `251 - 300`
lorsque `A<301` et `A<= 350` puis `301 - 350`
lorsque `A<351` et `A<=400` puis `351 - 400`
lorsque `A<401` et `A<=450` puis `401 - 450`
sinon &#39;plus de 450&#39;
fin


## Mesures

Aucune nouvelle mesure!!!

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Rapports

* **Valeur de commande moyenne avec règle d’expédition A**
   * [!UICONTROL Metric] : `Average order value`

* `A` de mesure : `Average Order Value`
* [!UICONTROL Time period] : `Time period with shipping rule A`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`

* **Nombre de commandes par regroupement de sous-total avec règle d&#39;expédition A**
   * [!UICONTROL Metric] : `Number of orders`

  >[!NOTE]
  >
  >Vous pouvez couper l’extrémité arrière en affichant le `X` supérieur `sorted by` `Order subtotal` (compartiments) dans le `Show top/bottom`.

* `A` de mesure : `Number of orders`
* [!UICONTROL Time period] : `Time period with shipping rule A`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by] : `Order subtotal (buckets)`
* &#x200B;
  [!UICONTROL Chart Type]: `Column`

* **Pourcentage de commandes par sous-total avec la règle d&#39;expédition A**
   * [!UICONTROL Metric] : `Number of orders`

   * [!UICONTROL Metric] : `Number of orders`
   * &#x200B;
     [!UICONTROL Regrouper par]: `Independent`
   * [!UICONTROL Formula] : `(A / B)`
   * &#x200B;
     [!UICONTROL Format]: `%`

* `A` de mesure : `Number of orders by subtotal (hide)`
* `B` de mesure : `Total number of orders (hide)`
* [!UICONTROL Formula] : `% of orders`
* [!UICONTROL Time period] : `Time period with shipping rule A`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by] : `Order subtotal (buckets)`
* &#x200B;
  [!UICONTROL Chart Type]: `Line`

* **Pourcentage de commandes dont le sous-total dépasse la règle d&#39;expédition A**
   * [!UICONTROL Metric] : `Number of orders`
   * &#x200B;
     [!UICONTROL Perspective]: `Cumulative`

   * [!UICONTROL Metric] : `Number of orders`
   * &#x200B;
     [!UICONTROL Regrouper par]: `Independent`

   * [!UICONTROL Formula] : `1- (A / B)`
   * &#x200B;
     [!UICONTROL Format]: `%`

* `A` de mesure : `Number of orders by subtotal`
* `B` de mesure : `Total number of orders (hide)`
* [!UICONTROL Formula] : `% of orders`
* [!UICONTROL Time period] : `Time period with shipping rule A`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by] : `Order subtotal (buckets)`
* &#x200B;
  [!UICONTROL Chart Type]: `Line`


Répétez les étapes et les états ci-dessus pour l&#39;expédition B et la période associée à la règle d&#39;expédition B.

Après avoir compilé tous les rapports, vous pouvez les organiser selon vos besoins dans le tableau de bord. Le résultat peut ressembler à l’image en haut de cette page.
