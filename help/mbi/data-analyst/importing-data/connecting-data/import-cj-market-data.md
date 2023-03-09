---
title: Importation des données marketing des affiliés CJ (Commission Junction)
description: Découvrez comment importer des données d’affilié CJ (Commission Junction) dans [!DNL MBI].L MBI].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Importer `CJ Affiliate` data

Pour importer `CJ Affiliate` Données (Commission Junction) dans [!DNL MBI], suivez simplement les étapes ci-dessous et joignez le fichier obtenu à un ticket d’assistance. Adobe configure le tableau de données de votre compte et vous permet de continuer à charger les données indépendamment.

## Exporter `CJ Affiliate` Données

1. Dans votre `CJ Affiliate` , accédez au `Reports` .

1. Dans le `Performance` onglet, sélectionnez `Report Options`.

1. Définir `Performance By` égal à `Program`, `Trend` égal à `Daily`, et `Date Range` égal à la période faisant l’objet d’un audit.

   ![export-cj-affilié-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Sélectionner `Run Report`.

1. Dans le `File Format` menu déroulant, sélectionnez `CSV`.  Cliquez sur **[!UICONTROL Download]**.

   ![exportation des données affiliées cj](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Une fois le fichier téléchargé, vous pouvez : [télécharger le fichier](../connecting-data/using-file-uploader.md) à [!DNL MBI] Data Warehouse.

   Cela crée un tableau dans votre [!DNL MBI] Data Warehouse que vous pouvez continuer à charger des données actualisées périodiquement dans . Lors du téléchargement du fichier, veillez à respecter les exigences de formatage répertoriées dans la section [Utilisation du téléchargeur de fichiers](../connecting-data/using-file-uploader.md).
