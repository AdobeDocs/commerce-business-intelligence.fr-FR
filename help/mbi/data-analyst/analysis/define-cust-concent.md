---
title: Définir la concentration des clients
description: Découvrez comment configurer un tableau de bord qui vous aide à mesurer la répartition du chiffre d’affaires total entre vos clients.
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# Concentration des clients

Cette rubrique explique comment configurer un tableau de bord qui vous aide à mesurer la répartition du chiffre d’affaires total entre vos clients. Identifiez le pourcentage de clients qui contribue au chiffre d’affaires et créez des listes segmentées pour mieux cibler et fidéliser vos clients qui contribuent le plus.

Cette analyse contient [colonnes calculées avancées](../data-warehouse-mgr/adv-calc-columns.md).

## Prise en main

Vous devez d’abord charger un fichier contenant uniquement une clé primaire avec la valeur d’un. Cela permet la création de certaines colonnes calculées nécessaires à l’analyse.

Vous pouvez utiliser [le téléchargeur de fichier](../importing-data/connecting-data/using-file-uploader.md) et l’image ci-dessous pour formater votre fichier.

## Colonnes calculées

Si vous utilisez l’architecture d’origine (par exemple, si vous n’avez pas l’option `Data Warehouse Views` dans le menu `Manage Data` ), vous devez contacter l’équipe d’assistance pour créer les colonnes ci-dessous. Sur la nouvelle architecture, ces colonnes peuvent être créées à partir de la page `Manage Data > Data Warehouse` . Des instructions détaillées sont données ci-dessous.

Une distinction supplémentaire est faite si votre entreprise autorise les commandes d&#39;invités. Si tel est le cas, vous pouvez ignorer toutes les étapes du tableau `customer_entity`. Si les commandes d&#39;invités ne sont pas autorisées, ignorez toutes les étapes pour la table `sales_flat_order`.

Colonnes à créer

* `Sales_flat_order/customer_entity` table
* (entrée) `reference`
* [!UICONTROL Column type] : - `Same table > Calculation`
* [!UICONTROL Inputs] : - `entity_id`
* [!UICONTROL Calculation] : - **cas où A est nul puis nul Autrement 1 fin**
* [!UICONTROL Datatype] : - `Integer`

* `Customer concentration` table (il s&#39;agit du fichier que vous avez chargé avec le numéro `1`)
* Nombre de clients
* [!UICONTROL Column type] : - `Many to One > Count Distinct`
* Chemin - `sales_flat_order.(input) reference > Customer Concentration.Primary Key` OU `customer_entity.(input)reference > Customer Concentration.Primary Key`
* Colonne sélectionnée - `sales_flat_order.customer_email` OU `customer_entity.entity_id`

* `customer_entity` table
* Nombre de clients
* [!UICONTROL Column type] : - `One to Many > JOINED_COLUMN`
* Chemin - `customer_entity.(input) reference > Customer Concentration. Primary Key`
* Colonne sélectionnée - `Number of customers`

* (entrée) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type] : - `Same table > Event Number`
* Propriétaire de l’événement - `Number of customers`
* Classement des événements - `Customer's lifetime revenue`

* Centile de chiffre d’affaires du client
* [!UICONTROL Column type] : - `Same table > Calculation`
* [!UICONTROL Inputs] : - `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation] : - **cas où A est nul puis nul else (A/B)* fin 100 &#x200B;**
* [!UICONTROL Datatype] : - `Decimal`

* `Sales_flat_order` table
* Nombre de clients
* [!UICONTROL Column type] : - `One to Many > JOINED_COLUMN`
* Chemin - `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* Colonne sélectionnée - `Number of customers`

* (entrée) Classement par chiffre d’affaires cumulé du client
* [!UICONTROL Column type] : - `Same table > Event Number`
* Propriétaire de l’événement - `Number of customers`
* Classement des événements - `Customer's lifetime revenue`
* Filtre - `Customer's order number = 1`

* Centile de chiffre d’affaires du client
* [!UICONTROL Column type] : - `Same table > Calculation`
* [!UICONTROL Inputs] : - `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation] : - **cas où A est nul puis nul else (A/B)* fin 100 &#x200B;**
* [!UICONTROL Datatype] : - `Decimal`

>[!NOTE]
>
>Les centiles utilisés sont des divisions paires de clients, représentant le Xe centile de votre base de clients. Chaque client est associé à un nombre entier compris entre 1 et 100, qui peut être considéré comme son chiffre d’affaires *rang*. Par exemple, si le centile du chiffre d’affaires du client pour un client spécifique est de **5**, ce client se situe dans le ***cinquième centile*** de tous les clients en termes de chiffre d’affaires cumulé.

## Mesures

* **Valeur totale de la durée de vie du client**
* Dans le tableau `customer_entity`
* Cette mesure effectue une **Somme**
* Dans la colonne `Customer's lifetime revenue`
* Classé par l’horodatage `Customer's first order date`

## Rapports

* **Concentration client**
* [!UICONTROL Metric] : `Total customer lifetime value`
* [!UICONTROL Filter] : `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric] : `Total customer lifetime value`
* [!UICONTROL Filter] : `Customer's revenue percentile IS NOT NULL`

* &#x200B;
  [!UICONTROL Regrouper par]: `Independent`
* `A` de mesure : `Total customer lifetime revenue by percentile`
* `B` de mesure : `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by] : `Customer's revenue percentile`
* Afficher en haut/en bas : `100% of Customer's revenue percentile Name`
* &#x200B;
  [!UICONTROL Chart type]: `Line`

* **Top 10% de concentration**
* [!UICONTROL Filter] : `Customer's revenue percentile <= 10`

* `A` de mesure : `Total customer lifetime revenue`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* Masquer le graphique
* &#x200B;
  [!UICONTROL Regrouper par]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **Concentration inférieure de 50 % avec un seul achat**

* `A` de mesure : `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter] :

* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* Masquer le graphique
* &#x200B;
  [!UICONTROL Regrouper par]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **Concentration inférieure de 10 %**
* [!UICONTROL Filter] : `Customer's revenue percentile > 90`

* `A` de mesure : `Total customer lifetime revenue`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* Masquer le graphique
* &#x200B;
  [!UICONTROL Regrouper par]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

Après avoir compilé tous les rapports, vous pouvez les organiser selon vos besoins dans le tableau de bord. Le résultat peut ressembler à l’exemple de tableau de bord ci-dessus.

Si vous avez des questions lors de la création de cette analyse ou si vous souhaitez simplement contacter l’équipe des services professionnels, [contactez l’assistance ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
