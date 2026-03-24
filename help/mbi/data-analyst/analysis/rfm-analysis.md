---
title: Analyse Récence, Fréquence, Monétaire (RFM)
description: Découvrez comment configurer un tableau de bord qui vous permet de segmenter vos clients par récence, fréquence et classement monétaire.
exl-id: 8f0f08fd-710b-4810-9faf-3d0c3cc0a25d
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
TQID: https://experienceleague.adobe.com/AaRzdTdV7-a4ApO-TA5jbyaJ3sr6sqP9HCToKG--uQ0
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: bd989d82-1e15-4534-88db-f1f51dd77ffaid: c1256247-af4b-46d8-9dca-0c654ecfa157id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 542
ht-degree: 0%

---

# Analyse RFM

Cette rubrique explique comment configurer un tableau de bord qui vous permet de segmenter vos clients en fonction de leur récence, fréquence et classement monétaire. L’analyse RFM est une technique marketing qui prend en compte les comportements des clients pour vous aider à déterminer la segmentation pour la diffusion externe. Il tient compte de trois aspects :

1. Récence de la date à laquelle un client a acheté des produits dans votre boutique
1. Fréquence à laquelle ils effectuent leurs achats chez vous
1. Montant monétaire des dépenses du client

![Tableau de bord d’analyse RFM affichant les segments de récence, de fréquence et de valeur monétaire](../../assets/blobid0.png)

L&#39;analyse RFM ne peut être configurée que si vous disposez du plan [!DNL Adobe Commerce Intelligence] Pro sur la nouvelle architecture (par exemple, si vous avez l&#39;option `Data Warehouse Views` sous le menu `Manage Data`). Ces colonnes peuvent être créées à partir de la page **[!DNL Manage Data > Data Warehouse]**. Des instructions détaillées sont fournies ci-dessous.

## Prise en main

Vous devez d’abord charger un fichier contenant uniquement une clé primaire avec la valeur d’un. Cela permet la création de certaines colonnes calculées nécessaires à l’analyse.

Vous pouvez utiliser cet [article](../importing-data/connecting-data/using-file-uploader.md) et l’image ci-dessous pour formater votre fichier.

## Colonnes calculées

Une distinction supplémentaire est faite si votre entreprise autorise les commandes d&#39;invités. Si tel est le cas, vous pouvez ignorer toutes les étapes du tableau `customer_entity`. Si les commandes d&#39;invités ne sont pas autorisées, ignorez toutes les étapes pour la table `sales_flat_order`.

Colonnes à créer

* **`Sales_flat_order/customer_entity`** table
* `Customer's last order date`
* [!UICONTROL Column type] : `Many to one > Max`
* [!UICONTROL Pat] : `sales_flat_order.customer_id > customer_entity.entity_id`
* [!UICONTROL column] sélectionné : `created_at`
* [!UICONTROL Filter] : `Orders we count`

* 
      Secondes écoulées depuis la date de la dernière commande du client
  * [!UICONTROL Column type] : -     « Même tableau > Âge
* [!UICONTROL column] sélectionné : `Customer's last order date`

* (entrée) Référence du nombre
* [!UICONTROL Column type] : `Same table > Calculation`
* 
  [!UICONTROL Entrées]: `entity_id`
* [!UICONTROL Calculation] : `**case when A is null then null else 1 end**`
* 
  [!UICONTROL, type de données]: `Integer`

* **Référence du nombre** table (il s&#39;agit du fichier que vous avez chargé avec le numéro « 1 »)
* Nombre de clients
* [!UICONTROL Column type] : `Many to One > Count Distinct`
* [!UICONTROL Path] : `ales_flat_order.(input) reference > Count reference.Primary Key` OU `customer_entity.(input)reference > Count Reference`. `Primary Key`
* [!UICONTROL column] sélectionné : `sales_flat_order.customer_email` OU `customer_entity.entity_id`

* Table **Customer_entity**
* Nombre de clients
* [!UICONTROL Column type] : `One to Many > JOINED_COLUMN`
* [!UICONTROL Path] : `customer_entity`.(entrée) référence > Concentration des clients. `Primary Key`
* [!UICONTROL column] sélectionné : `Number of customers`

* (entrée) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type] : `Same table > Event Number`
* [!UICONTROL Event owner] : `(input) reference for count`
* [!UICONTROL Event rank] : `Customer's lifetime revenue`

* Classement par chiffre d’affaires cumulé du client
* [!UICONTROL Column type] : `Same table > Calculation`
* [!UICONTROL Inputs] : `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation] : `case when A is null then null else (B-(A-1)) end`
* 
  [!UICONTROL, type de données]: `Integer`

* Score monétaire du client (en centiles)
* [!UICONTROL Column type] : `Same table > Calculation`
* [!UICONTROL Inputs] : `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation] : `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* 
  [!UICONTROL, type de données]: `Integer`

* (entrée) Classement par nombre de commandes sur la durée de vie du client
* [!UICONTROL Column type] : `Same table > Event Number`
* [!UICONTROL Event owner] : `(input) reference for count`
* [!UICONTROL Event rank] : `Customer's lifetime number of orders`

* Classement par nombre de commandes sur la durée de vie du client
* 
  [!UICONTROL Type de colonne]: – "Même tableau > Calcul"
* [!UICONTROL Inputs] : - **(entrée) Classement par nombre de commandes sur la durée de vie du client**, **nombre de clients**
* [!UICONTROL Calculation] : - **cas où A est nul puis nul autrement (B-(A-1)) fin**
* [!UICONTROL Datatype] : - Entier

* Score de fréquence du client (par centiles)
* [!UICONTROL Column type] : `Same table > Calculation`
* [!UICONTROL Inputs] : `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation] : `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* 
  [!UICONTROL, type de données]: `Integer`

* Classement par secondes depuis la date de la dernière commande du client
* [!UICONTROL Column type] : `Same table > Event Number`
* [!UICONTROL Event owner] : `(input) reference for count`
* [!UICONTROL Event rank] : `Seconds since customer's last order date`

* Score de récence du client (par centiles)
* [!UICONTROL Column type] : `Same table > Calculation`
* [!UICONTROL Inputs] : `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation] : `Case when (A * 100/B,0) <= 20 then 5 when (A * 100/B,0) <= 40 then 4 when (A * 100/B,0) <= 60 then 3 when (A * 100/B,0) <= 80 then 2 when (A * 100/B,0) <= 100 then 1 else 0 end`
* 
  [!UICONTROL, type de données]: `Integer`

* Score de récence du client (par centiles)
* [!UICONTROL Column type] : `Same table > Calculation`
* [!UICONTROL Inputs] : `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation] : `case when (A IS NULL or B IS NULL or C IS NULL) then null else concat(A,B,C) end`
* 
  [!UICONTROL, type de données]: String

* **Référence du nombre** tableau
* [!UICONTROL Number of customers] : `(RFM > 0)`
* [!UICONTROL Column type] : `Many to One > Count Distinct`
* [!UICONTROL Path] : `sales_flat_order.(input) reference > Customer Concentration. Primary Key` OU `customer_entity.(input)reference > Customer Concentration.Primary Key`
* [!UICONTROL column] sélectionné : `sales_flat_order.customer_email` OU `customer_entity.entity_id`
* [!UICONTROL Filter] : `Customer's RFM score (by percentile)` Est Différent De 000

* Table **Customer_entity**
* [!UICONTROL Number of customers] : `(RFM > 0)`
* [!UICONTROL Column type] : `One to Many > JOINED_COLUMN`
* [!UICONTROL Path] : `customer_entity.(input) reference > Customer Concentration.Primary Key`
* [!UICONTROL column] sélectionnés : - `Number of customers`

* `(R+F+M)` du score de récence du client
* [!UICONTROL Column type] : `Same table > Calculation`
* [!UICONTROL Inputs] : - `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation] : `case when (A IS NULL or B IS NULL or C IS NULL) then null else A+B+C end`
* 
  [!UICONTROL, type de données]: `Integer`

* (input) Classement par score RFM global du client
* [!UICONTROL Column type] : `Same table > Event Number`
* [!UICONTROL Event owner] : `(input) reference for count`
* [!UICONTROL Event rank] : `Customer's recency score (R+F+M)`
* [!UICONTROL Filter] : `Customer's RFM score (by percentile)` Est Différent De 000

* Classement par score RFM global du client
* [!UICONTROL Column type] : `Same table > Calculation`
* [!UICONTROL Inputs] : `(input) Ranking by customer's overall RFM score`, `Number of customers (RFM > 0)`
* [!UICONTROL Calculation] : `case when A is null then null else (B-(A-1)) end`
* 
  [!UICONTROL, type de données]: `Integer`

* Groupe RFM du client
* [!UICONTROL Column type] : `Same table > Calculation`
* [!UICONTROL Inputs] : `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation] : `Case when round(A * 100/B,0) <= 20 then '5. copper' when round(A * 100/B,0) <= 40 then '4. bronze' when round(A * 100/B,0) <= 60 then '3. silver' when round(A * 100/B,0)<= 80 then '2. gold' else '1. Platinum' end`
* 
  [!UICONTROL, type de données]: `Integer`

>[!NOTE]
>
>Les centiles utilisés sont des divisions paires de clients (par exemple, des intervalles de 20 % pour renvoyer 1 à 5). Si vous avez une méthode personnalisée de pondération, informez l&#39;analyste lorsque vous soumettez le ticket.

## Mesures

Aucune nouvelle mesure!

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Rapports

* **Clients par regroupement RFM**
* `A` de mesure : `New customers`
* [!UICONTROL Metric] : `New customers`
* [!UICONTROL Filter] : `Customer's RFM score (by percentiles) Not Equal to 000`

* [!UICONTROL Time period] : `All time`
* 
  [!UICONTROL Interval]: `None`
* Masquer le graphique
* [!UICONTROL Group by] : `Customer's RFM group`
* 
  [!UICONTROL Regrouper par]: `Email`
* 
  [!UICONTROL Chart type]: `Table`

* **Clients avec cinq scores de récence**
* `A` de mesure : `New customers`
* [!UICONTROL Metric] : `New customers`
* [!UICONTROL Filter] : `Customer's recency score (by percentiles) Equal to 5`

* [!UICONTROL Time period] : `All time`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`
* Masquer le graphique
* 
  [!UICONTROL Regrouper par]: `Email`
* [!UICONTROL Group by] : `Customer's RFM score (R+F+M)`
* 
  [!UICONTROL Chart type]: `Table`

* **Clients avec un score de récence**
* `A` de mesure : `New customers`
* [!UICONTROL Metric] : `New customers`
* [!UICONTROL Filter] : `Customer's recency score (by percentiles) Equal to 1`

* [!UICONTROL Time period] : `All time`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`
* Masquer le graphique
* 
  [!UICONTROL Regrouper par]: `Email`
* [!UICONTROL Group by] : `Customer's RFM score (R+F+M)`
* 
  [!UICONTROL Chart type]: `Table`

Après avoir compilé tous les rapports, vous pouvez les organiser selon vos besoins dans le tableau de bord. Le résultat peut ressembler à l’exemple de tableau de bord ci-dessus, mais les trois tableaux générés ne sont que des exemples des types de segmentation de clients que vous pouvez effectuer.
