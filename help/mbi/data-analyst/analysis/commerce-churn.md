---
title: Commerce Churn
description: Découvrez comment générer et analyser votre taux de perte de clientèle Commerce.
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# Taux de perte de clientèle

Cette rubrique explique comment calculer une **taux de perte de clientèle** pour votre **clients commerciaux**. Contrairement aux SaaS ou aux sociétés d’abonnement traditionnelles, les clients commerciaux n’ont généralement pas de clients concrets. **&quot;churn event&quot;** pour vous montrer qu’ils ne doivent plus compter pour vos principaux clients. Pour cette raison, les instructions ci-dessous vous permettent de définir un client comme &quot;généré&quot; en fonction d’un temps déterminé écoulé depuis sa dernière commande.

![](../../assets/Churn_rate_image.png)

De nombreux clients souhaitent obtenir de l’aide pour commencer à conceptualiser ce qui **délai** ils doivent utiliser en fonction de leurs données. Si vous souhaitez utiliser l’historique du comportement du client pour définir ceci **délai d’exécution**, vous souhaitez peut-être vous familiariser avec le [définition de la perte de clientèle](../analysis/define-cust-churn.md) article. Vous pouvez ensuite utiliser les résultats de la formule pour le taux de perte de clientèle dans les instructions ci-dessous.

## Colonnes calculées

Colonnes à créer

* **`customer_entity`** table
* **`Customer's last order date`**
   * Sélectionnez une [!UICONTROL definition]: `Max`
   * Sélectionner [!UICONTROL table]: `sales_flat_order`
   * Sélectionner [!UICONTROL column]: `created_at`
   * `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]: `Orders we count`

* **`Seconds since customer's last order date`**
   * Sélectionnez une [!UICONTROL definition]: `Age`
   * Sélectionner [!UICONTROL column]: `Customer's last order date`

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures ;](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Mesures

* **Nouveaux clients (par date de première commande)**
   * Clients comptabilisés

>[!NOTE]
>
>Cette mesure peut exister sur votre compte.

* Dans le **`customer_entity`** table
* Cette mesure effectue une **Count**
* Sur le **`entity_id`** column
* Commandé par le **`Customer's first order date`** timestamp
* [!UICONTROL Filter]:

* **Nouveaux clients (par date de dernière commande)**
   * Clients comptabilisés

>[!NOTE]
>
>Cette mesure peut exister sur votre compte.

* Dans le **`customer_entity`** table
* Cette mesure effectue une **Count**
* Sur le **`entity_id`** column
* Commandé par le **`Customer's last order date`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures ;](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Rapports

* **Taux de perte de clientèle**
   * [!UICONTROL Metric]: Nouveaux clients (par date de première commande)
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
      [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]:
   * Secondes depuis la date de dernière commande du client >= [Votre auto-définition de coupure pour les clients connectés ]**`^`**
   * `Lifetime number of orders Greater Than 0`

   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
      [!UICONTROL Perspective]: Cumulative
   * [!UICONTROL Formula]: `(B / ((A + B) - C)`
   * 

      [!UICONTROL Format]: Percentage

* *Mesure `A`:`New customers cumulative`*
* *Mesure `B`:`Churned customers by last order date`*
* *Mesure `C`:`Customers by last order date cumulative`*
* *`Formula`:`Repeat order probability`*
* *`Time period`:`All time (or custom range)`*
* *`Group by`:`Customer's order number`*
* *`Chart Type`:`Column`*

Vous trouverez ci-dessous quelques conversions mensuelles > secondes courantes, mais Google fournit d’autres valeurs, y compris les conversions semaine > secondes pour toutes les valeurs personnalisées que vous recherchez.

| **Mois** | **Secondes** |
|---|---|
| 3 | 7,776,000 |
| 6 | 15,552,000 |
| 9 | 23,328,000 |
| 12 | 31,104,000 |

Après avoir compilé tous les rapports, vous pouvez les organiser dans le tableau de bord suivant vos besoins. Le résultat peut ressembler à l’exemple de tableau de bord ci-dessus.
