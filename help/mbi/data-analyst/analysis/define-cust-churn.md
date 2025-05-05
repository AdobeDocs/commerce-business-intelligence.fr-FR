---
title: Définition de la perte de clientèle
description: Découvrez comment configurer un tableau de bord qui vous aide à définir l’attrition de vos clients transactionnels.
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Perte de clientèle transactionnelle

Cette rubrique explique comment configurer un tableau de bord qui vous aide à définir l’attrition de vos clients transactionnels.

![](../../assets/churn-deashboard.png)

Cette analyse contient [des colonnes calculées avancées](../data-warehouse-mgr/adv-calc-columns.md).

## Colonnes calculées

Colonnes à créer

* `customer_entity` table
* `Customer's lifetime number of orders`
* Sélectionnez une définition : `Count`
* Sélectionnez un [!UICONTROL table] : `sales_flat_order`
* Sélectionnez un [!UICONTROL column] : **`entity_id`**
* [!UICONTROL Path] : sales_plat_order.customer_id = customer_entity.entity_id
* [!UICONTROL Filter] :
* Commandes comptabilisées

* `sales_flat_order` table
* `Customer's lifetime number of orders`
* Sélectionner une définition : Colonne associée
* Sélectionnez un [!UICONTROL table] : `customer_entity`
* Sélectionnez un [!UICONTROL column] : `Customer's lifetime number of orders`
* [!UICONTROL Path] : `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter] : `Orders we count`

* `Seconds since created_at`
* Sélectionnez une définition : `Age`
* Sélectionnez un [!UICONTROL column] : `created_at`

* **`Customer's order number`** est créé par un analyste dans le cadre de votre ticket **[DEFINING CHURN]**
* **`Is customer's last order`** est créé par un analyste dans le cadre de votre ticket **[DEFINING CHURN]**
* **`Seconds since previous order`** est créé par un analyste dans le cadre de votre ticket **[DEFINING CHURN]**
* **`Months since order`** est créé par un analyste dans le cadre de votre ticket **[DEFINING CHURN]**
* **`Months since previous order`** est créé par un analyste dans le cadre de votre ticket **[DEFINING CHURN]**

## Mesures

Aucune nouvelle mesure !

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Rapports

* **Probabilité initiale de répétition**
* Mesure A : commandes répétées toutes les heures
* [!UICONTROL Metric] : `Number of orders`
* [!UICONTROL Filter] : `Customer's order number greater than 1`

* Mesure B : Commandes en temps réel
* [!UICONTROL Metric] : nombre de commandes

* [!UICONTROL Formula] : probabilité initiale de l’ordre de répétition
* &#x200B;
  [!UICONTROL Formule]: `A/B`
* &#x200B;
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart type]: `Scalar`

* **Probabilité de répétition de l’ordre exprimée en mois depuis la commande**
* Mesure A : commandes répétées par mois depuis la commande précédente (masquer)
* [!UICONTROL Metric] : `Number of orders`
* &#x200B;
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter] : `Customer's order number greater than 1`

* Mesure B : Dernières commandes par mois depuis la commande (masquer)
* [!UICONTROL Metric] : `Number of orders`
* &#x200B;
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter] : `Is customer's last order? (Yes/No) = Yes`

* Mesure C : commandes répétées toutes les heures (masquer)
* [!UICONTROL Metric] : `Number of orders`
* [!UICONTROL Filter] : `Customer's order number greater than 1`

* &#x200B;
  [!UICONTROL Groupe par]: `Independent`

* Mesure D : Dernières commandes toutes les heures (masquer)
* [!UICONTROL Metric] : `Number of orders`
* [!UICONTROL Filter] : `Is customer's last order? (Yes/No) = Yes`

* &#x200B;
  [!UICONTROL Groupe par]: `Independent`

* [!UICONTROL Formula] : probabilité initiale de l’ordre de répétition
* &#x200B;
  [!UICONTROL Formule]: `(C-A)/(C+D-A-B)`
* &#x200B;
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by] : `Months since previous order`
* Afficher top.bottom : 24 premières catégories, triées par nom de catégorie

* &#x200B;
  [!UICONTROL Chart type]: `Line`

Le rapport de probabilité d’ordre de répétition initial représente le total des commandes répétées / total des commandes. Chaque commande est une opportunité d’effectuer une commande répétée ; le nombre de commandes répétées est le sous-ensemble de celles qui le font réellement.

La formule que vous utilisez simplifie les commandes à (Total des commandes répétées survenues après X mois)/ (Total des commandes qui ont au moins X mois). Elle nous montre qu’historiquement, étant donné que cela fait X mois qu’une commande a été passée, il y a une chance sur Y % que l’utilisateur passe une autre commande.

Une fois que vous avez créé votre tableau de bord, la question la plus courante est : comment l’utiliser pour déterminer un seuil de perte de clientèle ?

**Il n&#39;y a pas de &quot;réponse juste&quot; à cela.** Cependant, Adobe recommande de trouver le point où la ligne traverse la valeur qui correspond à la moitié du taux de probabilité de répétition initial. C’est à ce stade que vous pouvez dire &quot;Si un utilisateur doit effectuer une commande de répétition, il l’aura probablement fait à ce stade.&quot; En fin de compte, l’objectif est de sélectionner le seuil où il est logique de passer des efforts de &quot;rétention&quot; aux efforts de &quot;réactivation&quot;.

Après avoir compilé tous les rapports, vous pouvez les organiser dans le tableau de bord suivant vos besoins. Le résultat peut ressembler à l’image en haut de la page.

Si vous rencontrez des questions lors de la création de cette analyse ou si vous souhaitez simplement contacter l’équipe des services professionnels, [contactez l’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
