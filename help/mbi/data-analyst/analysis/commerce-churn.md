---
title: Attrition du Commerce
description: Découvrez comment générer et analyser votre taux de résiliation Commerce.
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# Taux de résiliation

Cette rubrique explique comment calculer un **taux de résiliation** pour vos clients **Commerce**. Contrairement aux SaaS ou aux sociétés d’abonnement traditionnelles, les clients commerciaux ne disposent généralement pas d’un **concret « événement de perte de clientèle »** pour vous montrer qu’ils ne doivent plus compter parmi vos clients actifs. Pour cette raison, les instructions ci-dessous vous permettent de définir un client comme « résilié » en fonction d’un temps déterminé écoulé depuis sa dernière commande.

![](../../assets/Churn_rate_image.png)

De nombreux clients souhaitent obtenir de l’aide pour commencer à conceptualiser le **délai** qu’ils doivent utiliser en fonction de leurs données. Si vous souhaitez utiliser l’historique du comportement des clients pour définir ce **délai d’attrition**, vous pouvez vous familiariser avec la rubrique [définition de l’attrition](../analysis/define-cust-churn.md). Vous pouvez ensuite utiliser les résultats dans la formule pour le taux de résiliation dans les instructions ci-dessous.

## Colonnes calculées

Colonnes à créer

* **`customer_entity`** table
* **`Customer's last order date`**
   * Sélectionner un [!UICONTROL definition] : `Max`
   * Sélectionner un [!UICONTROL table] : `sales_flat_order`
   * Sélectionner un [!UICONTROL column] : `created_at`
   * `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter] : `Orders we count`

* **`Seconds since customer's last order date`**
   * Sélectionner un [!UICONTROL definition] : `Age`
   * Sélectionner un [!UICONTROL column] : `Customer's last order date`

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Mesures

* **Nouveaux clients (par date de première commande)**
   * Clients comptabilisés

>[!NOTE]
>
>Cette mesure existe peut-être sur votre compte.

* Dans le tableau **`customer_entity`**
* Cette mesure effectue un **Nombre**
* Dans la colonne **`entity_id`**
* Classé par l’horodatage **`Customer's first order date`**
* [!UICONTROL Filter] :

* **Nouveaux clients (par date de dernière commande)**
   * Clients comptabilisés

  >[!NOTE]
  >
  >Cette mesure existe peut-être sur votre compte.

* Dans le tableau **`customer_entity`**
* Cette mesure effectue un **Nombre**
* Dans la colonne **`entity_id`**
* Classé par l’horodatage **`Customer's last order date`**
* [!UICONTROL Filter] :

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Rapports

* **Taux de résiliation**
   * [!UICONTROL Metric] : Nouveaux clients (par date de première commande)
   * [!UICONTROL Filter] : `Lifetime number of orders Greater Than 0`
   * &#x200B;
     [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric] : `New customers (by last order date)`
   * [!UICONTROL Filter] :
   * Secondes écoulées depuis la date de la dernière commande du client >= [Votre limite auto-définie pour les clients résiliés ]&#x200B;**`^`**
   * `Lifetime number of orders Greater Than 0`

   * [!UICONTROL Metric] : `New customers (by last order date)`
   * [!UICONTROL Filter] : `Lifetime number of orders Greater Than 0`
   * &#x200B;
     [!UICONTROL Perspective]: Cumulative
   * [!UICONTROL Formula] : `(B / ((A + B) - C)`
   * &#x200B;
     [!UICONTROL Format]: Percentage

* *`A` de mesure :`New customers cumulative`*
* *`B` de mesure :`Churned customers by last order date`*
* *`C` de mesure :`Customers by last order date cumulative`*
* *`Formula`:`Repeat order probability`*
* *`Time period`:`All time (or custom range)`*
* *`Group by`:`Customer's order number`*
* *`Chart Type`:`Column`*

Vous trouverez ci-dessous quelques conversions mois > seconde courantes, mais Google fournit d’autres valeurs, y compris des conversions semaine > secondes pour toutes les valeurs personnalisées que vous recherchez.

| **Mois** | **Secondes** |
|---|---|
| 3 | 7 776 000 |
| 6 | 15 552 000 |
| 9 | 23 328 000 |
| 12 | 31 104 000 |

Après avoir compilé tous les rapports, vous pouvez les organiser selon vos besoins dans le tableau de bord. Le résultat peut ressembler à l’exemple de tableau de bord ci-dessus.
