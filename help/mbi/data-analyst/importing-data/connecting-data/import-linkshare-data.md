---
title: Importer des données Linkshare
description: Découvrez comment importer des données Linkshare dans [!DNL Commerce Intelligence].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: 'https://experienceleague.adobe.com/TsQYXEwH-8m1rpKg6It8wa-B2eQH0oqDkLcgx-tRBWU'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 2%
---
# Importer les données [!DNL Linkshare]

Pour importer vos données [!DNL Linkshare] dans [!DNL Adobe Commerce Intelligence], vous devez effectuer deux opérations :

1. [Exporter les données Linkshare au format `.csv`](#export)
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
