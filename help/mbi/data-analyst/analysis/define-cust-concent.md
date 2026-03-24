---
title: Définir la concentration des clients
description: Découvrez comment configurer un tableau de bord qui vous aide à mesurer la répartition du chiffre d’affaires total entre vos clients.
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
role: Admin, Developer, User
feature: Data Warehouse Manager, Reports, Dashboards
TQID: https://experienceleague.adobe.com/kayq-ci-AiHHgNoaX09h6dqKQX14MudLvEqFmos3hQE
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 472
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

Si vous avez des questions lors de la création de cette analyse ou si vous souhaitez simplement contacter l’équipe des services professionnels, [contactez l’assistance &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
