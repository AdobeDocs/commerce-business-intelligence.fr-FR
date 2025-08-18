---
title: Définir l’attrition client
description: Découvrez comment configurer un tableau de bord qui vous aide à définir l’attrition pour vos clients transactionnels.
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Attrition client transactionnelle

Cette rubrique explique comment configurer un tableau de bord qui vous aide à définir l’attrition pour vos clients transactionnels.

![](../../assets/churn-deashboard.png)

Cette analyse contient [colonnes calculées avancées](../data-warehouse-mgr/adv-calc-columns.md).

## Colonnes calculées

Colonnes à créer

* `customer_entity` table
* `Customer's lifetime number of orders`
* Sélectionnez une définition : `Count`
* Sélectionner un [!UICONTROL table] : `sales_flat_order`
* Sélectionner un [!UICONTROL column] : **`entity_id`**
* [!UICONTROL Path] : sales_flat_order.customer_id = customer_entity.entity_id
* [!UICONTROL Filter] :
* Commandes comptabilisées

* `sales_flat_order` table
* `Customer's lifetime number of orders`
* Sélectionner une définition : Colonne jointe
* Sélectionner un [!UICONTROL table] : `customer_entity`
* Sélectionner un [!UICONTROL column] : `Customer's lifetime number of orders`
* [!UICONTROL Path] : `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter] : `Orders we count`

* `Seconds since created_at`
* Sélectionnez une définition : `Age`
* Sélectionner un [!UICONTROL column] : `created_at`

* **`Customer's order number`** est créé par un analyste dans le cadre de votre ticket **[DEFINING CHURN]**
* **`Is customer's last order`** est créé par un analyste dans le cadre de votre ticket **[DEFINING CHURN]**
* **`Seconds since previous order`** est créé par un analyste dans le cadre de votre ticket **[DEFINING CHURN]**
* **`Months since order`** est créé par un analyste dans le cadre de votre ticket **[DEFINING CHURN]**
* **`Months since previous order`** est créé par un analyste dans le cadre de votre ticket **[DEFINING CHURN]**

## Mesures

Aucune nouvelle mesure!

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Rapports

* **Probabilité d’ordre de répétition initiale**
* Mesure A : ordres de répétition en tout temps
* [!UICONTROL Metric] : `Number of orders`
* [!UICONTROL Filter] : `Customer's order number greater than 1`

* Mesure B : Commandes à tout moment
* [!UICONTROL Metric] : nombre de commandes

* [!UICONTROL Formula] : probabilité d’ordre de répétition initiale
* &#x200B;
  [!UICONTROL Formule]: `A/B`
* &#x200B;
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart type]: `Scalar`

* **Probabilité de répétition de l’ordre donnée en mois depuis l’ordre**
* Mesure A : commandes répétées par mois depuis la commande précédente (masquer)
* [!UICONTROL Metric] : `Number of orders`
* &#x200B;
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter] : `Customer's order number greater than 1`

* Mesure B : dernières commandes par mois depuis la commande (masquer)
* [!UICONTROL Metric] : `Number of orders`
* &#x200B;
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter] : `Is customer's last order? (Yes/No) = Yes`

* Mesure C : ordres de répétition en tout temps (masquer)
* [!UICONTROL Metric] : `Number of orders`
* [!UICONTROL Filter] : `Customer's order number greater than 1`

* &#x200B;
  [!UICONTROL Regrouper par]: `Independent`

* ID de mesure : toutes les dernières commandes (masquer)
* [!UICONTROL Metric] : `Number of orders`
* [!UICONTROL Filter] : `Is customer's last order? (Yes/No) = Yes`

* &#x200B;
  [!UICONTROL Regrouper par]: `Independent`

* [!UICONTROL Formula] : probabilité d’ordre de répétition initiale
* &#x200B;
  [!UICONTROL Formule]: `(C-A)/(C+D-A-B)`
* &#x200B;
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by] : `Months since previous order`
* Afficher top.bottom : Top 24 des catégories, triées par nom de catégorie

* &#x200B;
  [!UICONTROL Chart type]: `Line`

L&#39;état de probabilité des ordres de répétition initial représente le total des ordres de répétition / total des ordres. Chaque ordre est une occasion de faire un ordre de répétition ; le nombre d&#39;ordres de répétition est le sous-ensemble de ceux qui le font réellement.

La formule que vous utilisez se simplifie en (Nombre total de commandes répétées qui se sont produites après X mois)/ (Nombre total de commandes qui ont au moins X mois). Cela nous montre que historiquement, étant donné qu&#39;il y a X mois depuis une commande, il y a une probabilité de Y% que l&#39;utilisateur passe une autre commande.

Une fois que vous avez créé votre tableau de bord, la question la plus courante est la suivante : Comment puis-je utiliser ceci pour déterminer un seuil d’attrition ?

**Il n’existe pas de « réponse unique » à cette question.** Cependant, Adobe recommande de trouver le point où la ligne traverse la valeur qui représente la moitié du taux de probabilité de répétition initial. C’est à ce stade que vous pouvez dire « Si un utilisateur va effectuer une commande de répétition, il l’aurait probablement déjà fait ». En fin de compte, l’objectif est de sélectionner le seuil où il est logique de passer des efforts de « rétention » aux efforts de « réactivation ».

Après avoir compilé tous les rapports, vous pouvez les organiser selon vos besoins dans le tableau de bord. Le résultat peut ressembler à l’image en haut de la page

Si vous avez des questions lors de la création de cette analyse ou si vous souhaitez simplement contacter l’équipe des services professionnels, [contactez l’assistance ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr).
