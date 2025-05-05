---
title: Commerce Churn
description: Découvrez comment générer et analyser votre taux de perte de clientèle Commerce.
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# Taux de perte de clientèle

Cette rubrique explique comment calculer un **taux d’attrition** pour vos **clients commerciaux**. Contrairement aux SaaS ou aux sociétés d’abonnement traditionnelles, les clients de commerce n’ont généralement pas d’ **&quot;événement d’attrition&quot;** concret pour vous montrer qu’ils ne doivent plus compter pour vos clients actifs. Pour cette raison, les instructions ci-dessous vous permettent de définir un client comme &quot;généré&quot; en fonction d’un délai déterminé écoulé depuis sa dernière commande.

![](../../assets/Churn_rate_image.png)

De nombreux clients souhaitent obtenir de l’aide pour commencer à conceptualiser la **période** qu’ils doivent utiliser en fonction de leurs données. Si vous souhaitez utiliser l’historique du comportement des clients pour définir cette **période d’attrition**, vous pouvez vous familiariser avec la rubrique [définition de l’attrition](../analysis/define-cust-churn.md) . Vous pouvez ensuite utiliser les résultats de la formule pour le taux de perte de clientèle dans les instructions ci-dessous.

## Colonnes calculées

Colonnes à créer

* **`customer_entity`** table
* **`Customer's last order date`**
   * Sélectionnez un [!UICONTROL definition] : `Max`
   * Sélectionner [!UICONTROL table] : `sales_flat_order`
   * Sélectionner [!UICONTROL column] : `created_at`
   * `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter] : `Orders we count`

* **`Seconds since customer's last order date`**
   * Sélectionnez un [!UICONTROL definition] : `Age`
   * Sélectionner [!UICONTROL column] : `Customer's last order date`

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Mesures

* **Nouveaux clients (par date de première commande)**
   * Clients comptabilisés

>[!NOTE]
>
>Cette mesure peut exister sur votre compte.

* Dans la table **`customer_entity`**
* Cette mesure exécute un **décompte**
* Sur la colonne **`entity_id`**
* Ordonné par l’horodatage **`Customer's first order date`**
* [!UICONTROL Filter] :

* **Nouveaux clients (par date de dernière commande)**
   * Clients comptabilisés

  >[!NOTE]
  >
  >Cette mesure peut exister sur votre compte.

* Dans la table **`customer_entity`**
* Cette mesure exécute un **décompte**
* Sur la colonne **`entity_id`**
* Ordonné par l’horodatage **`Customer's last order date`**
* [!UICONTROL Filter] :

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Rapports

* **Taux de perte de clientèle**
   * [!UICONTROL Metric] : Nouveaux clients (par date de première commande)
   * [!UICONTROL Filter] : `Lifetime number of orders Greater Than 0`
   * &#x200B;

     [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric] : `New customers (by last order date)`
   * [!UICONTROL Filter] :
   * Secondes depuis la date de la dernière commande du client >= [Votre coupure auto-définie pour les clients connectés ]&#x200B;**`^`**
   * `Lifetime number of orders Greater Than 0`

   * [!UICONTROL Metric] : `New customers (by last order date)`
   * [!UICONTROL Filter] : `Lifetime number of orders Greater Than 0`
   * &#x200B;

     [!UICONTROL Perspective]: Cumulative
   * [!UICONTROL Formula] : `(B / ((A + B) - C)`
   * &#x200B;

     [!UICONTROL Format]: Percentage

* *Mesure `A` :`New customers cumulative`*
* *Mesure `B` :`Churned customers by last order date`*
* *Mesure `C` :`Customers by last order date cumulative`*
* *`Formula`:`Repeat order probability`*
* *`Time period`:`All time (or custom range)`*
* *`Group by`:`Customer's order number`*
* *`Chart Type`:`Column`*

Vous trouverez ci-dessous quelques conversions mensuelles > secondes courantes, mais Google fournit d’autres valeurs, y compris les conversions semaine > secondes pour toutes les valeurs personnalisées que vous recherchez.

| **Months** | **Secondes** |
|---|---|
| 3 | 7 776 000 |
| 6 | 15 552 000 |
| 9 | 23 328 000 |
| 12 | 31 104 000 |

Après avoir compilé tous les rapports, vous pouvez les organiser dans le tableau de bord suivant vos besoins. Le résultat peut ressembler à l’exemple de tableau de bord ci-dessus.
