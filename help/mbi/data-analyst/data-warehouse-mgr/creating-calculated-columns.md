---
title: Créer des colonnes calculées
description: Découvrez comment consolider des données provenant de différentes sources.
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# Créer des colonnes calculées

Lors de l’analyse de vos données, il est utile de consolider les données provenant de différentes sources. Vous souhaitez regrouper les revenus par source d’acquisition, en liant les données de votre table `orders` et les données [!DNL Google Analytics] ? Vous souhaitez peut-être regrouper le chiffre d’affaires par genre de client ou associer un attribut de client aux données de transaction pour la segmentation. Cette rubrique explique comment procéder.

Avant de commencer, Adobe vous recommande de consulter le [Guide des types de colonnes calculés](../../data-analyst/data-warehouse-mgr/calc-column-types.md) pour plus d’informations sur les types de colonnes que vous pouvez créer dans Data Warehouse Manager, ainsi que leurs définitions et exemples.

1. Pour commencer, cliquez sur **[!DNL Manage Data > Data Warehouse]**.

1. Cliquez sur le tableau dans lequel vous souhaitez créer une colonne. Par exemple, si vous souhaitez créer une colonne de `Customer Gender` pour la segmentation des revenus, vous devez sélectionner la table des `sales_flat_order`.

1. Le schéma de tableau s’affiche. Cliquez sur **[!UICONTROL Create New Column]**.

1. Attribuez un nom à votre colonne. Par exemple, `Customer Gender`.

1. Sélectionnez la définition de la colonne. C’est là que le guide [Types de colonnes calculées](../data-warehouse-mgr/calc-column-types.md) s’avère utile !

1. Pour certains types de colonnes, un peu plus d’informations sont nécessaires pour créer correctement la colonne :

   * Pour les colonnes `One to Many` (jointes) et `Many to One` (agrégées), vous devez sélectionner les tableaux et les colonnes.

   * Pour une `Same Table calculation`, vous devez sélectionner le champ de date de votre choix dans la liste déroulante.

Si vous créez une colonne `One to Many` (jointe) ou `Many to One` (agrégée), vous devez sélectionner un chemin d’accès pour connecter les deux tables. Au cours de cette étape, vous pouvez utiliser un chemin existant ou en créer un.

>[!NOTE]
>
>N&#39;oubliez pas de définir correctement le tableau comme plusieurs ou un seul.

* Si vous le souhaitez, vous pouvez appliquer des [filtres](../../data-user/reports/ess-manage-data-filters.md) à la nouvelle colonne.

* Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save]**.

Votre nouvelle colonne apparaît dans le tableau actuel avec un statut `Pending`. Une fois la prochaine mise à jour terminée, votre colonne pourra être utilisée dans les mesures et les rapports.

## Carte de référence pratique {#map}

Si vous avez des difficultés à vous souvenir de toutes les entrées lors de la création d’une colonne calculée, essayez de garder cette carte de référence à portée de main lorsque vous créez :

![Exemple de configuration de colonne calculée dans Data Warehouse Manager](../../assets/Calculated_Columns_Example.png)

## Documentation connexe

* [Types de colonnes calculées](../data-warehouse-mgr/calc-column-types.md)
* [Types de colonnes calculées avancés](../data-warehouse-mgr/adv-calc-columns.md)
* [Création [!DNL Google ECommerce] dimensions avec des données de commande et de client](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
