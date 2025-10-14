---
title: Importer des données Linkshare
description: Découvrez comment importer des données Linkshare dans [!DNL Commerce Intelligence].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 2%

---

# Importer les données [!DNL Linkshare]

Pour importer vos données [!DNL Linkshare] dans [!DNL Adobe Commerce Intelligence], vous devez effectuer deux opérations :

1. [Exporter les données Linkshare dans &#x200B;](#export)
1. [Chargez la feuille de calcul dans  [!DNL Commerce Intelligence]](../connecting-data/using-file-uploader.md)

## Exporter des données depuis Linkshare {#export}

1. Dans votre compte [!DNL Linkshare], accédez à **[!UICONTROL Reports** > **Run Reports].**

1. Dans la liste déroulante `Report`, sélectionnez **[!UICONTROL Sales & Activity Report]**.

1. Laissez toutes les autres options de liste déroulante comme sélection par défaut.

1. Dans la liste déroulante `Date Range` , sélectionnez l’option (`Sun - Sat`, `Mon - Sun`) qui correspond à vos paramètres `Start of Week` dans [!DNL Commerce Intelligence].

1. Décochez la case `Compare Year-Over-Year Data` .

1. Sous `Data Type`, sélectionnez `Transaction Date`.

   ![import\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. Cliquez sur **[!UICONTROL View Report]**.

1. Cliquez sur **[!UICONTROL Download]**.

   À ce stade, un fichier `.csv` et téléchargé.

Une fois le fichier téléchargé, vous pouvez le charger dans [!DNL Commerce Intelligence] à l’aide de la fonction [`File Upload`](../connecting-data/using-file-uploader.md).
