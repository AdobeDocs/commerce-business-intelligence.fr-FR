---
title: Définition de la concentration des clients
description: Découvrez comment configurer un tableau de bord qui vous aide à mesurer la manière dont le total des recettes est réparti entre votre base de clients.
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# Concentration de la clientèle

Cette rubrique explique comment configurer un tableau de bord qui vous aide à mesurer la répartition du total des recettes entre votre base de clients. Identifiez le pourcentage de clients qui contribuent aux recettes et créez des listes segmentées afin de mieux commercialiser et de conserver vos clients ayant un fort taux de contribution.

Cette analyse contient [des colonnes calculées avancées](../data-warehouse-mgr/adv-calc-columns.md).

## Prise en main

Vous devez d’abord télécharger un fichier contenant uniquement une clé primaire dont la valeur est de 1. Cela permet de créer certaines colonnes calculées nécessaires à l’analyse.

Vous pouvez utiliser [le téléchargeur de fichiers](../importing-data/connecting-data/using-file-uploader.md) et l’image ci-dessous pour formater votre fichier.

## Colonnes calculées

Si vous utilisez l’architecture d’origine (par exemple, si vous ne disposez pas de l’option `Data Warehouse Views` dans le menu `Manage Data`), vous souhaitez contacter l’équipe de support pour créer les colonnes ci-dessous. Sur la nouvelle architecture, ces colonnes peuvent être créées à partir de la page `Manage Data > Data Warehouse`. Vous trouverez ci-dessous des instructions détaillées.

Une autre distinction est faite si votre entreprise autorise les commandes d’invités. Si tel est le cas, vous pouvez ignorer toutes les étapes de la table `customer_entity`. Si les commandes d’invités ne sont pas autorisées, ignorez toutes les étapes de la table `sales_flat_order`.

Colonnes à créer

* `Sales_flat_order/customer_entity` table
* (entrée) `reference`
* [!UICONTROL Column type] : - `Same table > Calculation`
* [!UICONTROL Inputs] : - `entity_id`
* [!UICONTROL Calculation] : - **cas où A est nul puis null else 1 end**
* [!UICONTROL Datatype] : - `Integer`

* Table `Customer concentration` (il s&#39;agit du fichier que vous avez téléchargé avec le numéro `1`)
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

* centile des recettes du client
* [!UICONTROL Column type] : - `Same table > Calculation`
* [!UICONTROL Inputs] : - `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation] : - **cas où A est nul puis null else (A/B)* 100 end &#x200B;**
* [!UICONTROL Datatype] : - `Decimal`

* `Sales_flat_order` table
* Nombre de clients
* [!UICONTROL Column type] : - `One to Many > JOINED_COLUMN`
* Chemin - `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* Colonne sélectionnée - `Number of customers`

* (entrée) Classement par chiffre d’affaires sur la durée de vie du client
* [!UICONTROL Column type] : - `Same table > Event Number`
* Propriétaire de l’événement - `Number of customers`
* Classement d’événements - `Customer's lifetime revenue`
* Filtre - `Customer's order number = 1`

* centile des recettes du client
* [!UICONTROL Column type] : - `Same table > Calculation`
* [!UICONTROL Inputs] : - `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation] : - **cas où A est nul puis null else (A/B)* 100 end &#x200B;**
* [!UICONTROL Datatype] : - `Decimal`

>[!NOTE]
>
>Les centiles utilisés sont des divisions d’événements, représentant le centile Xème de votre base de clients. Chaque client est associé à un entier compris entre 1 et 100, qui peut être considéré comme le chiffre d’affaires de sa durée de vie *rank*. Par exemple, si le centile de recettes du client pour un client spécifique est de **5**, ce client se trouve dans le ***cinquième centile*** de tous les clients en termes de recettes sur la durée de vie.

## Mesures

* **Valeur totale de durée de vie du client**
* Dans la table `customer_entity`
* Cette mesure exécute une **Somme**
* Sur la colonne `Customer's lifetime revenue`
* Ordonné par l’horodatage `Customer's first order date`

## Rapports

* **Concentration des clients**
* [!UICONTROL Metric] : `Total customer lifetime value`
* [!UICONTROL Filter] : `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric] : `Total customer lifetime value`
* [!UICONTROL Filter] : `Customer's revenue percentile IS NOT NULL`

* &#x200B;
  [!UICONTROL Groupe par]: `Independent`
* Mesure `A` : `Total customer lifetime revenue by percentile`
* Mesure `B` : `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by] : `Customer's revenue percentile`
* Afficher en haut/en bas : `100% of Customer's revenue percentile Name`
* &#x200B;
  [!UICONTROL Chart type]: `Line`

* **Principale concentration de 10 %**
* [!UICONTROL Filter] : `Customer's revenue percentile <= 10`

* Mesure `A` : `Total customer lifetime revenue`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* Masquer le graphique
* &#x200B;
  [!UICONTROL Groupe par]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **Concentration inférieure de 50 % avec un seul achat**

* Mesure `A` : `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter] :

* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* Masquer le graphique
* &#x200B;
  [!UICONTROL Groupe par]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **Densité inférieure de 10 %**
* [!UICONTROL Filter] : `Customer's revenue percentile > 90`

* Mesure `A` : `Total customer lifetime revenue`
* [!UICONTROL Time period] : `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* Masquer le graphique
* &#x200B;
  [!UICONTROL Groupe par]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

Après avoir compilé tous les rapports, vous pouvez les organiser dans le tableau de bord suivant vos besoins. Le résultat peut ressembler à l’exemple de tableau de bord ci-dessus.

Si vous rencontrez des questions lors de la création de cette analyse ou si vous souhaitez simplement contacter l’équipe des services professionnels, [contactez l’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
