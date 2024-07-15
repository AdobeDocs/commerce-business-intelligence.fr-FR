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

Lors de l’analyse de vos données, il est utile de consolider des données provenant de différentes sources. Vous souhaitez regrouper les recettes par source d’acquisition, en liant les données de votre table `orders` et les données [!DNL Google Analytics] ? Vous souhaitez peut-être regrouper les recettes par sexe de client ou associer un attribut du client aux données de transaction pour la segmentation. Cette rubrique explique comment faire précisément cela.

Avant de commencer, Adobe vous recommande de consulter le [Guide des types de colonnes calculées](../../data-analyst/data-warehouse-mgr/calc-column-types.md) pour plus d’informations sur les types de colonnes que vous pouvez créer dans le Gestionnaire de Data Warehouse, ainsi que leurs définitions et leurs exemples.

1. Pour commencer, cliquez sur **[!DNL Manage Data > Data Warehouse]**.

1. Cliquez sur le tableau dans lequel vous souhaitez créer une colonne. Par exemple, si vous souhaitez créer une colonne `Customer Gender` pour la segmentation des recettes, sélectionnez la table `sales_flat_order`.

1. Le modèle de tableau s’affiche. Cliquez sur **[!UICONTROL Create New Column]**.

1. Attribuez un nom à votre colonne. Par exemple, `Customer Gender`.

1. Sélectionnez la définition de la colonne. C’est là que le [guide sur les types de colonnes calculées](../data-warehouse-mgr/calc-column-types.md) s’avère pratique !

1. Pour certains types de colonnes, un peu plus d’informations est nécessaire pour créer correctement la colonne :

   * Pour les colonnes `One to Many` (unies) et `Many to One` (agrégées), vous devez sélectionner les tables et les colonnes.

   * Pour un `Same Table calculation`, vous devez sélectionner le champ de date souhaité dans la liste déroulante.

Si vous créez une colonne `One to Many` (jointe) ou `Many to One` (agrégée), vous devez sélectionner un chemin pour connecter les deux tables. Au cours de cette étape, vous pouvez utiliser un chemin existant ou en créer un.

>[!NOTE]
>
>N’oubliez pas de définir correctement le tableau comme plusieurs ou un seul !

* Si vous le souhaitez, vous pouvez appliquer des [filtres](../../data-user/reports/ess-manage-data-filters.md) à la nouvelle colonne.

* Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save]**.

Votre nouvelle colonne apparaît dans la table actuelle avec l’état `Pending`. Une fois la prochaine mise à jour terminée, votre colonne sera disponible dans les mesures et les rapports.

## Carte de référence pratique {#map}

Si vous rencontrez des difficultés à vous souvenir de toutes les entrées lors de la création d’une colonne calculée, essayez de conserver cette carte de référence pratique lorsque vous créez :

![](../../assets/Calculated_Columns_Example.png)

## Documentation connexe

* [Types de colonne calculés](../data-warehouse-mgr/calc-column-types.md)
* [Types de colonne calculés avancés](../data-warehouse-mgr/adv-calc-columns.md)
* [Construire des dimensions avec des données de commande et de client [!DNL Google ECommerce] ](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
