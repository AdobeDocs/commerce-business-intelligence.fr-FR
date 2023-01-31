---
title: Définition de la perte de clientèle
description: Découvrez comment configurer un tableau de bord qui vous aidera à définir l’attrition de vos clients transactionnels.
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
source-git-commit: 3557e6370fae637cd74550b2806847bebe61d5d3
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# Perte de clientèle transactionnelle

Dans cet article, nous vous montrons comment configurer un tableau de bord qui vous aidera à définir la perte de clientèle de vos clients transactionnels.

![](../../assets/churn-deashboard.png)

Cette analyse contient [colonnes calculées avancées](../data-warehouse-mgr/adv-calc-columns.md).

## Colonnes calculées

Colonnes à créer

* `customer_entity` table
* `Customer's lifetime number of orders`
* Sélectionnez une définition : `Count`
* Sélectionnez une [!UICONTROL table]: `sales_flat_order`
* Sélectionnez une [!UICONTROL column]: **`entity_id`**
* [!UICONTROL Path]: sales_plat_order.customer_id = customer_entity.entity_id
* [!UICONTROL Filter]:
* Commandes comptabilisées

* `sales_flat_order` table
* `Customer's lifetime number of orders`
* Sélectionnez une définition : Colonne liée
* Sélectionnez une [!UICONTROL table]: `customer_entity`
* Sélectionnez une [!UICONTROL column]: `Customer's lifetime number of orders`
* [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter]: `Orders we count`

* `Seconds since created_at`
* Sélectionnez une définition : `Age`
* Sélectionnez une [!UICONTROL column]: `created_at`

* **`Customer's order number`** sera créé par un analyste dans le cadre de votre **[DÉFINITION DE L’URL]** ticket
* **`Is customer's last order`** sera créé par un analyste dans le cadre de votre **[DÉFINITION DE L’URL]** ticket
* **`Seconds since previous order`** sera créé par un analyste dans le cadre de votre **[DÉFINITION DE L’URL]** ticket
* **`Months since order`** sera créé par un analyste dans le cadre de votre **[DÉFINITION DE L’URL]** ticket
* **`Months since previous order`** sera créé par un analyste dans le cadre de votre **[DÉFINITION DE L’URL]** ticket

## Mesures

Aucune nouvelle mesure !

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures ;](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Rapports

* **Probabilité initiale de l’ordre de répétition**
* Mesure A : Toutes les commandes répétées
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Mesure B : Toutes les commandes
* [!UICONTROL Metric]: Nombre de commandes

* [!UICONTROL Formula]: Probabilité initiale de l’ordre de répétition
* 
   [!UICONTROL Formule]: `A/B`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart type]: `Scalar`

* **Probabilité de répétition de l’ordre exprimée en mois depuis la commande**
* Mesure A : Répéter les commandes par mois depuis la commande précédente (masquer)
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Mesure B : Dernières commandes par mois depuis la commande (masquer)
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* Mesure C : Toutes les commandes répétées (masquer)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 

   [!UICONTROL Groupe par]: `Independent`

* Mesure D : Toutes les dernières commandes (masquer)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 

   [!UICONTROL Groupe par]: `Independent`

* [!UICONTROL Formula]: Probabilité initiale de l’ordre de répétition
* 
   [!UICONTROL Formule]: `(C-A)/(C+D-A-B)`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Months since previous order`
* Afficher top.bottom : 24 premières catégories, triées par nom de catégorie

* 

   [!UICONTROL Chart type]: `Line`

Le rapport de probabilité d’ordre de répétition initial représente le total des commandes répétées / total des commandes. Chaque commande est l’occasion d’effectuer une commande répétée. le nombre de commandes répétées est le sous-ensemble de celles qui le font réellement.

La formule que nous utilisons simplifie les commandes à (Total des commandes répétées survenues après X mois)/ (Total des commandes qui ont au moins X mois). Il nous montre qu’historiquement, étant donné que cela fait X mois qu’une commande a été passée, il y a une chance sur Y % que l’utilisateur passe une autre commande.

Une fois que vous avez créé votre tableau de bord, la question la plus courante que nous recevons est la suivante : Comment puis-je l’utiliser pour déterminer un seuil de perte de clientèle ?

**Il n&#39;y a pas de &quot;réponse juste&quot; à cela.** Cependant, nous vous recommandons de trouver le point où la ligne traverse la valeur correspondant à la moitié du taux de probabilité de répétition initial. C’est à ce stade que nous pouvons dire : &quot;Si un utilisateur devait effectuer une commande répétée, il l’aurait probablement fait maintenant.&quot; En fin de compte, l’objectif est de sélectionner le seuil où il est logique de passer des efforts de &quot;rétention&quot; aux efforts de &quot;réactivation&quot;.

Après avoir compilé tous les rapports, vous pouvez les organiser dans le tableau de bord suivant vos besoins. Le résultat final peut ressembler à l’image en haut de la page.

Si vous rencontrez des questions lors de la création de cette analyse ou si vous souhaitez simplement faire appel à notre équipe de services professionnels, [support technique](../../guide-overview.md).
