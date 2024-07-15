---
title: Analyse des commandes retournées
description: Découvrez comment configurer un tableau de bord qui fournit une analyse détaillée des retours de votre boutique.
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Commandes renvoyées

Cette rubrique explique comment configurer un tableau de bord qui fournit une analyse détaillée des retours de votre magasin.

![](../../assets/detailed-returns-dboard.png)

Avant de commencer, vous devez être un client [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) et vous assurer que votre société utilise la table `enterprise\_rma` pour les retours.

Cette analyse contient [des colonnes calculées avancées](../data-warehouse-mgr/adv-calc-columns.md).

## Prise en main

Colonnes à suivre

* **`enterprise_rma`** ou **`rma`** table
* **`entity_id`**
* **`status`**
* **`order_id`**
* **`customer_id`**
* **`date_requested`**

* **`enterprise_rma_item_entity`** ou **`rma_item_entity`** table
* **`entity_id`**
* **`rma_entity_id`**
* **`qty_returned`**
* **`status`**
* **`order_item_id`**
* **`product_name`**
* **`product_sku`**

Filtrer les ensembles à créer

* **`enterprise_rma`** table
* Nom du jeu de filtres : `Returns we count`
* Filtrer la logique du jeu :
   * Espace réservé : entrez votre logique personnalisée ici

* **`enterprise_rma_item_entity`** table
* Nom du jeu de filtres : `Returns items we count`
* Filtrer la logique du jeu :
   * Espace réservé : entrez votre logique personnalisée ici

### Colonnes calculées

Colonnes à créer

* **`enterprise_rma`** table
* **`Order's created at`**
* Sélectionnez une définition : `Joined Column`
* [!UICONTROL Create Path] :
* 
  [!UICONTROL Many]: `enterprise_rma.order_id`
* 
  [!UICONTROL One]: `sales_flat_order.entity_id`

* Sélectionnez un [!UICONTROL table] : `sales_flat_order`
* Sélectionnez un [!UICONTROL column] : `created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* Sélectionnez une définition : `Joined Column`
* Sélectionnez un [!UICONTROL table] : `sales_flat_order`
* Sélectionnez un [!UICONTROL column] : `Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Time between order's created_at and date_requested`** est créé par un analyste dans le cadre de votre ticket `[RETURNS ANALYSIS]`

* **`enterprise_rma_item_entity`** table
* **`return_date_requested`**
* Sélectionnez une définition : `Joined Column`
* [!UICONTROL Create Path] :
   * 
     [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
   * 
     [!UICONTROL One]: `enterprise_rma.entity_id`

* Sélectionnez un [!UICONTROL table] : `enterprise_rma`
* Sélectionnez un [!UICONTROL column] : `date_requested`
   * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* **`Return item total value (qty_returned * price)`** est créé par un analyste dans le cadre de votre ticket `[RETURNS ANALYSIS]`

* **`sales_flat_order`** table
* **`Order contains a return? (1=yes/0=No)`**
* Sélectionnez une définition : `Exists`
* Sélectionnez un [!UICONTROL table] : `enterprise_rma`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's previous order number`** est créé par un analyste dans le cadre de votre ticket `[RETURNS ANALYSIS]`
* **`Customer's previous order contains return? (1=yes/0=no)`** est créé par un analyste dans le cadre de votre ticket `[RETURNS ANALYSIS]`

>[!NOTE]
>
>Si vous souhaitez analyser uniquement les heures ouvrables pour la résolution Secondes jusqu’à la première réponse ou Secondes jusqu’à la première réponse, faites-le savoir à l’analyste lors de la demande du ticket.

### Mesures

* **Renvoie**
* Dans la table **`enterprise_rma`**
* Cette mesure exécute un **décompte**
* Sur la colonne **`entity_id`**
* Commandé par le **`date_requested`**
* [!UICONTROL Filter] : `Returns we count`

* **Éléments retournés**
* Dans la table **`enterprise_rma_item_entity`**
* Cette mesure exécute une **Somme**
* Sur la colonne **`qty_approved`**
* Commandé par le **`return date_requested`**
* [!UICONTROL Filter] : `Returns we count`

* **Valeur totale de l’élément renvoyé**
* Dans la table **`enterprise_rma_item_entity`**
* Cette mesure exécute une **Somme**
* Sur la colonne **`Returned item total value (qty_returned * price)`**
* Commandé par le **`return date_requested`**
* [!UICONTROL Filter] : `Returns we count`

* **Durée moyenne entre la commande et le retour**
* Dans la table **`enterprise_rma`**
* Cette mesure exécute une **moyenne**
* Sur la colonne **`Time between order's created_at and date_requested`**
* Commandé par le **`date_requested`**
* [!UICONTROL Filter] : `Returns we count`

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

### Rapports

* **Probabilité de répétition de l’ordre après avoir effectué un retour**
* Mesure `A` : `Number of orders with returns`
* [!UICONTROL Metric] : `Number of orders`
* [!UICONTROL Filter] :
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is in current month? = No`

* Mesure `B` : `Non-last orders with returns`
* [!UICONTROL Metric] : `Number of orders`
* [!UICONTROL Filter] :
   * `Is customer's last order? (1=yes/0=no) = 0`
   * `Order contains a return? (1=yes/0=No) = 1`

* Formule : probabilité de répétition de l&#39;ordre
* [!UICONTROL Formula] : `B / A`
* 
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period] : `All time`
* 
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by] : `Customer's order number`
* 
  [!UICONTROL Type de graphique]: `Bar`

* **Temps moyen pour revenir (tout le temps)**
* Mesure `A` : `Avg time between order and return`
* [!UICONTROL Metric] : `Avg time between order and return`

* [!UICONTROL Time period] : `All time`
* 
  [!UICONTROL Intervalle]: `None`
* 
  [!UICONTROL Type de graphique]: `Number`

* **Pourcentage de commandes avec un retour**
* Mesure `A` : `Number of orders`
* [!UICONTROL Metric] : `Number of orders`

* Mesure `B` : `Orders w/ return`
* [!UICONTROL Metric] : `Number of orders`
* [!UICONTROL Filter] :
   * `Order contains a return? (1=yes/0=No) = 1`

* Formule : % des commandes avec retour
* [!UICONTROL Formula] : `B / A`
* 
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period] : `All time`
* 
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Chart Type] : `Number - % of orders with return`

* **Recettes retournées par mois**
* Mesure `A` : `Returned item total value`
* [!UICONTROL Metric] : `Returned item total value`

* [!UICONTROL Time period] : `All time`
* [!UICONTROL Interval] : `By month`
* 
  [!UICONTROL Type de graphique]: `Line`

* **Clients ayant effectué un retour et n’ayant pas acheté à nouveau**
* Mesure `A` : `Number of orders with returns`
* [!UICONTROL Metric] : `Number of orders`
* [!UICONTROL Filter] :
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is customer's last order? (1=yes/0=no) = 1`

* [!UICONTROL Time period] : `All time`
* 
  [!UICONTROL Intervalle]: `None`
* 
  [!UICONTROL Groupe par]: `Customer_email`
* 
  [!UICONTROL Type de graphique]: `Table`

* **Taux de retour par élément**
* Mesure `A` : `Returned items` (Masquer)
* [!UICONTROL Metric] : éléments renvoyés

* Mesure `B` : `Items sold` (Masquer)
* [!UICONTROL Metric] : `Number of orders`
* [!UICONTROL Filter] :

* [!UICONTROL Formula] : `Return %`
* [!UICONTROL Formula] : `B / A`
* 
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period] : `All time`
* 
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by] : `product_sku AND/OR product_name`
* 
  [!UICONTROL Type de graphique]: `Table`

Après avoir compilé tous les rapports, vous pouvez les organiser dans le tableau de bord suivant vos besoins. Le résultat peut ressembler à l’exemple de tableau de bord ci-dessus.

Si vous rencontrez des questions lors de la création de cette analyse ou si vous souhaitez contacter l’équipe des services professionnels, [contactez l’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
