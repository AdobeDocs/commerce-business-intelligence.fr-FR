---
title: Importation de données Linkshare
description: Découvrez comment importer des données Linkshare dans [!DNL Commerce Intelligence].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 2%

---

# Importer [!DNL Linkshare] data

Pour apporter votre [!DNL Linkshare] données dans [!DNL Adobe Commerce Intelligence], vous devez effectuer deux opérations :

1. [Exportation des données Linkshare dans ](#export)
1. [Chargement de la feuille de calcul [!DNL Commerce Intelligence]](../connecting-data/using-file-uploader.md)

## Exporter des données depuis Linkshare {#export}

1. Dans votre [!DNL Linkshare] compte, accédez à **[!UICONTROL Reports** > **Run Reports].**

1. Dans le `Report` menu déroulant, sélectionnez **[!UICONTROL Sales & Activity Report]**.

1. Conservez toutes les autres options de liste déroulante comme sélection par défaut.

1. Dans le `Date Range` dans la liste déroulante, sélectionnez n’importe quelle option (`Sun - Sat`, `Mon - Sun`) correspond à votre `Start of Week` paramètres dans [!DNL Commerce Intelligence].

1. Effacez la variable `Compare Year-Over-Year Data` .

1. Sous `Data Type`, sélectionnez `Transaction Date`.

   ![import\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. Cliquez sur **[!UICONTROL View Report]**.

1. Cliquez sur **[!UICONTROL Download]**.

   À ce stade, une `.csv` et téléchargé.

Une fois le fichier téléchargé, vous pouvez le charger dans [!DNL Commerce Intelligence] en utilisant la variable [`File Upload` fonctionnalité](../connecting-data/using-file-uploader.md).
