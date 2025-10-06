---
title: Analyse des commandes renvoyées
description: Découvrez comment configurer un tableau de bord qui fournit une analyse détaillée des retours de votre boutique.
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Commandes retournées

Cette rubrique explique comment configurer un tableau de bord qui fournit une analyse détaillée des retours de votre magasin.

![Tableau de bord détaillé des retours indiquant les taux de retour et les raisons](../../assets/detailed-returns-dboard.png)

Avant de commencer, vous devez être un client [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) et vous assurer que votre société utilise la table `enterprise\_rma` pour les retours.

Cette analyse contient [colonnes calculées avancées](../data-warehouse-mgr/adv-calc-columns.md).

## Prise en main

Colonnes à suivre

* **`enterprise_rma`** ou tableau **`rma`**
* **`entity_id`**
* **`status`**
* **`order_id`**
* **`customer_id`**
* **`date_requested`**

* **`enterprise_rma_item_entity`** ou tableau **`rma_item_entity`**
* **`entity_id`**
* **`rma_entity_id`**
* **`qty_returned`**
* **`status`**
* **`order_item_id`**
* **`product_name`**
* **`product_sku`**

Jeux de filtres à créer

* **`enterprise_rma`** table
* Nom du jeu de filtres : `Returns we count`
* Logique du jeu de filtres :
   * Espace réservé - Saisissez votre logique personnalisée ici

* **`enterprise_rma_item_entity`** table
* Nom du jeu de filtres : `Returns items we count`
* Logique du jeu de filtres :
   * Espace réservé - Saisissez votre logique personnalisée ici

### Colonnes calculées

Colonnes à créer

* **`enterprise_rma`** table
* **`Order's created at`**
* Sélectionnez une définition : `Joined Column`
* [!UICONTROL Create Path] :
* &#x200B;
  [!UICONTROL Many]: `enterprise_rma.order_id`
* &#x200B;
  [!UICONTROL One]: `sales_flat_order.entity_id`

* Sélectionner un [!UICONTROL table] : `sales_flat_order`
* Sélectionner un [!UICONTROL column] : `created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* Sélectionnez une définition : `Joined Column`
* Sélectionner un [!UICONTROL table] : `sales_flat_order`
* Sélectionner un [!UICONTROL column] : `Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Time between order's created_at and date_requested`** est créé par un analyste dans le cadre de votre ticket `[RETURNS ANALYSIS]`

* **`enterprise_rma_item_entity`** table
* **`return_date_requested`**
* Sélectionnez une définition : `Joined Column`
* [!UICONTROL Create Path] :
   * &#x200B;
     [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
   * &#x200B;
     [!UICONTROL One]: `enterprise_rma.entity_id`

* Sélectionner un [!UICONTROL table] : `enterprise_rma`
* Sélectionner un [!UICONTROL column] : `date_requested`
   * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* **`Return item total value (qty_returned * price)`** est créé par un analyste dans le cadre de votre ticket `[RETURNS ANALYSIS]`

* **`sales_flat_order`** table
* **`Order contains a return? (1=yes/0=No)`**
* Sélectionnez une définition : `Exists`
* Sélectionner un [!UICONTROL table] : `enterprise_rma`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's previous order number`** est créé par un analyste dans le cadre de votre ticket `[RETURNS ANALYSIS]`
* **`Customer's previous order contains return? (1=yes/0=no)`** est créé par un analyste dans le cadre de votre ticket `[RETURNS ANALYSIS]`

>[!NOTE]
>
>Si vous souhaitez analyser uniquement les heures ouvrées pour les Secondes avant la résolution ou les Secondes avant la première réponse, informez l’analyste lors de la demande du ticket.

### Mesures

* **Renvoie**
* Dans le tableau **`enterprise_rma`**
* Cette mesure effectue un **Nombre**
* Dans la colonne **`entity_id`**
* Commandé par le **`date_requested`**
* [!UICONTROL Filter] : `Returns we count`

* **Éléments renvoyés**
* Dans le tableau **`enterprise_rma_item_entity`**
* Cette mesure effectue une **Somme**
* Dans la colonne **`qty_approved`**
* Commandé par le **`return date_requested`**
* [!UICONTROL Filter] : `Returns we count`

* **Valeur totale de l’élément renvoyé**
* Dans le tableau **`enterprise_rma_item_entity`**
* Cette mesure effectue une **Somme**
* Dans la colonne **`Returned item total value (qty_returned * price)`**
* Commandé par le **`return date_requested`**
* [!UICONTROL Filter] : `Returns we count`

* **Temps moyen entre la commande et le retour**
* Dans le tableau **`enterprise_rma`**
* Cette mesure effectue une **Moyenne**
* Dans la colonne **`Time between order's created_at and date_requested`**
* Commandé par le **`date_requested`**
* [!UICONTROL Filter] : `Returns we count`

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

### Rapports

* **Probabilité de commande répétée après un retour**
* `A` de mesure : `Number of orders with returns`
* [!UICONTROL Metric] : `Number of orders`
* [!UICONTROL Filter] :
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is in current month? = No`

* `B` de mesure : `Non-last orders with returns`
* [!UICONTROL Metric] : `Number of orders`
* [!UICONTROL Filter] :
   * `Is customer's last order? (1=yes/0=no) = 0`
   * `Order contains a return? (1=yes/0=No) = 1`

* Formule : probabilité d’ordre de répétition
* [!UICONTROL Formula] : `B / A`
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by] : `Customer's order number`
* &#x200B;
  [!UICONTROL Type de graphique]: `Bar`

* **Temps moyen de retour (toute heure)**
* `A` de mesure : `Avg time between order and return`
* [!UICONTROL Metric] : `Avg time between order and return`

* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* &#x200B;
  [!UICONTROL Type de graphique]: `Number`

* **Pourcentage de commandes avec retour**
* `A` de mesure : `Number of orders`
* [!UICONTROL Metric] : `Number of orders`

* `B` de mesure : `Orders w/ return`
* [!UICONTROL Metric] : `Number of orders`
* [!UICONTROL Filter] :
   * `Order contains a return? (1=yes/0=No) = 1`

* Formule : % de commandes avec retour
* [!UICONTROL Formula] : `B / A`
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Chart Type] : `Number - % of orders with return`

* **Chiffre d’affaires renvoyé par mois**
* `A` de mesure : `Returned item total value`
* [!UICONTROL Metric] : `Returned item total value`

* [!UICONTROL Time period] : `All time`
* [!UICONTROL Interval] : `By month`
* &#x200B;
  [!UICONTROL Type de graphique]: `Line`

* **Clients ayant effectué un retour et n’ayant pas effectué de nouvel achat**
* `A` de mesure : `Number of orders with returns`
* [!UICONTROL Metric] : `Number of orders`
* [!UICONTROL Filter] :
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is customer's last order? (1=yes/0=no) = 1`

* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* &#x200B;
  [!UICONTROL Regrouper par]: `Customer_email`
* &#x200B;
  [!UICONTROL Type de graphique]: `Table`

* **Taux de retour par article**
* `A` de mesure : `Returned items` (masquer)
* [!UICONTROL Metric] : éléments renvoyés

* `B` de mesure : `Items sold` (masquer)
* [!UICONTROL Metric] : `Number of orders`
* [!UICONTROL Filter] :

* [!UICONTROL Formula] : `Return %`
* [!UICONTROL Formula] : `B / A`
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Intervalle]: `None`
* [!UICONTROL Group by] : `product_sku AND/OR product_name`
* &#x200B;
  [!UICONTROL Type de graphique]: `Table`

Après avoir compilé tous les rapports, vous pouvez les organiser selon vos besoins dans le tableau de bord. Le résultat peut ressembler à l’exemple de tableau de bord ci-dessus.

Si vous avez des questions lors de la création de cette analyse ou si vous souhaitez contacter l’équipe des services professionnels, [contactez l’assistance technique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
