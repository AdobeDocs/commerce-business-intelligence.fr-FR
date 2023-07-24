---
title: Créer des colonnes calculées
description: Découvrez comment consolider des données provenant de différentes sources.
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# Créer des colonnes calculées

Lors de l’analyse de vos données, il est utile de consolider des données provenant de différentes sources. Souhaitez regrouper les recettes par source d’acquisition, en liant les données de votre `orders` table et [!DNL Google Analytics] données ? Vous souhaitez peut-être regrouper les recettes par sexe de client ou associer un attribut du client aux données de transaction pour la segmentation. Cette rubrique explique comment le faire.

Avant de commencer, Adobe vous recommande de consulter la section [Guide sur les types de colonne calculés](../../data-analyst/data-warehouse-mgr/calc-column-types.md) pour plus d’informations sur les types de colonnes que vous pouvez créer dans Data Warehouse Manager, ainsi que leurs définitions et exemples.

1. Pour commencer, cliquez sur **[!DNL Manage Data > Data Warehouse]**.

1. Cliquez sur le tableau dans lequel vous souhaitez créer une colonne. Par exemple, si vous souhaitez créer une `Customer Gender` pour la segmentation des recettes, vous devez sélectionner la variable `sales_flat_order` table.

1. Le modèle de tableau s’affiche. Cliquez sur **[!UICONTROL Create New Column]**.

1. Attribuez un nom à votre colonne. Par exemple : `Customer Gender`.

1. Sélectionnez la définition de la colonne. C’est là que le [Guide sur les types de colonne calculés](../data-warehouse-mgr/calc-column-types.md) c&#39;est pratique !

1. Pour certains types de colonnes, un peu plus d’informations est nécessaire pour créer correctement la colonne :

   * Pour `One to Many` (joint) et `Many to One` (agrégé) , vous devez sélectionner les tableaux et les colonnes.

   * Pour un `Same Table calculation`, vous devez sélectionner le champ de date de votre choix dans la liste déroulante.

Si vous créez une `One to Many` (joint) ou `Many to One` (agrégé) , vous devez sélectionner un chemin pour connecter les deux tables. Au cours de cette étape, vous pouvez utiliser un chemin existant ou en créer un.

>[!NOTE]
>
>Pensez à définir correctement le tableau comme plusieurs ou un seul !

* Si vous le souhaitez, vous pouvez appliquer des [filtres](../../data-user/reports/ess-manage-data-filters.md) à la nouvelle colonne.

* Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save]**.

La nouvelle colonne apparaît dans le tableau actuel avec un `Pending` statut. Une fois la prochaine mise à jour terminée, votre colonne sera disponible dans les mesures et les rapports.

## Carte de référence pratique {#map}

Si vous rencontrez des difficultés à vous souvenir de toutes les entrées lors de la création d’une colonne calculée, essayez de conserver cette carte de référence pratique lorsque vous créez :

![](../../assets/Calculated_Columns_Example.png)

## Documentation connexe

* [Types de colonne calculés](../data-warehouse-mgr/calc-column-types.md)
* [Types de colonne calculés avancés](../data-warehouse-mgr/adv-calc-columns.md)
* [Création [!DNL Google ECommerce] dimensions avec les données de commande et de client ;](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
