---
title: Seuil de livraison gratuite
description: Découvrez comment configurer un tableau de bord qui suit les performances de votre seuil d’expédition gratuite.
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
role: Admin,  User
feature: Data Warehouse Manager, Dashboards, Reports
TQID: 'https://experienceleague.adobe.com/dh7Ep6xzBaaeO5LAnsUogg0jSCIXMjv-faBsPyGXpcg'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: 06e518d4-11ae-5c20-98b0-ce8ab05d7166
    internal-label: Dashboards
  - id: f842eedf-96a8-52c7-891d-4e56f7441a7e
    internal-label: Reports
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 17%
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
  * [!UICONTROL Calculation]&#x200B;: `case when A >= 0 and A<=200 then 0 - 200`
    si `A< 200` et `A <= 250` alors `201 - 250`
    si `A<251` et `A<= 300` alors `251 - 300`
    si `A<301` et `A<= 350` alors `301 - 350`
    si `A<351` et `A<=400` alors `351 - 400`
    si `A<401` et `A<=450` alors `401 - 450`
    sinon &#39;plus de 450&#39;
    fin


## Mesures

Aucune nouvelle mesure!!!

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Rapports

* **Valeur de commande moyenne avec règle d’expédition A**
  * [!UICONTROL Metric]&#x200B;: `Average order value`

* `A` de mesure : `Average Order Value`
* [!UICONTROL Time period]&#x200B;: `Time period with shipping rule A`
* &#x200B;
  [!UICONTROL Interval]&#x200B;: `None`
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Scalar`

* **Nombre de commandes par regroupement de sous-total avec règle d&#39;expédition A**
  * [!UICONTROL Metric]&#x200B;: `Number of orders`

  >[!NOTE]
  >
  >Vous pouvez couper l’extrémité arrière en affichant le `X` supérieur `sorted by` `Order subtotal` (compartiments) dans le `Show top/bottom`.

* `A` de mesure : `Number of orders`
* [!UICONTROL Time period]&#x200B;: `Time period with shipping rule A`
* &#x200B;
  [!UICONTROL Interval]&#x200B;: `None`
* [!UICONTROL Group by]&#x200B;: `Order subtotal (buckets)`
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Column`

* **Pourcentage de commandes par sous-total avec la règle d&#39;expédition A**
  * [!UICONTROL Metric]&#x200B;: `Number of orders`

  * [!UICONTROL Metric]&#x200B;: `Number of orders`
  * &#x200B;
    [!UICONTROL Regrouper par]&#x200B;: `Independent`
  * [!UICONTROL Formula]&#x200B;: `(A / B)`
  * &#x200B;
    [!UICONTROL Format]&#x200B;: `%`

* `A` de mesure : `Number of orders by subtotal (hide)`
* `B` de mesure : `Total number of orders (hide)`
* [!UICONTROL Formula]&#x200B;: `% of orders`
* [!UICONTROL Time period]&#x200B;: `Time period with shipping rule A`
* &#x200B;
  [!UICONTROL Interval]&#x200B;: `None`
* [!UICONTROL Group by]&#x200B;: `Order subtotal (buckets)`
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Line`

* **Pourcentage de commandes dont le sous-total dépasse la règle d&#39;expédition A**
  * [!UICONTROL Metric]&#x200B;: `Number of orders`
  * &#x200B;
    [!UICONTROL Perspective]&#x200B;: `Cumulative`

  * [!UICONTROL Metric]&#x200B;: `Number of orders`
  * &#x200B;
    [!UICONTROL Regrouper par]&#x200B;: `Independent`

  * [!UICONTROL Formula]&#x200B;: `1- (A / B)`
  * &#x200B;
    [!UICONTROL Format]&#x200B;: `%`

* `A` de mesure : `Number of orders by subtotal`
* `B` de mesure : `Total number of orders (hide)`
* [!UICONTROL Formula]&#x200B;: `% of orders`
* [!UICONTROL Time period]&#x200B;: `Time period with shipping rule A`
* &#x200B;
  [!UICONTROL Interval]&#x200B;: `None`
* [!UICONTROL Group by]&#x200B;: `Order subtotal (buckets)`
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Line`


Répétez les étapes et les états ci-dessus pour l&#39;expédition B et la période associée à la règle d&#39;expédition B.

Après avoir compilé tous les rapports, vous pouvez les organiser selon vos besoins dans le tableau de bord. Le résultat peut ressembler à l’image en haut de cette page.
