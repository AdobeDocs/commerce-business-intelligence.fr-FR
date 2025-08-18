---
title: Importation des données marketing de l'affilié CJ (Commission Junction)
description: Découvrez comment importer des données d’affilié CJ (Commission Junction) dans  [!DNL Commerce Intelligence].L Commerce Intelligence&rbrack;.
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Importer les données [!DNL CJ Affiliate]

Pour importer [!DNL CJ Affiliate (Commission Junction)] données dans [!DNL Adobe Commerce Intelligence], procédez simplement comme suit et joignez le fichier obtenu à un ticket d’assistance [&#128279;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html). Adobe configure la table de données de votre compte et vous permet de continuer à charger des données indépendamment.

## Exporter les données [!DNL CJ Affiliate]

1. Dans votre compte [!DNL CJ Affiliate], accédez à l’onglet `Reports` .

1. Dans l’onglet `Performance` , sélectionnez `Report Options`.

1. Définissez `Performance By` égal à `Program`, `Trend` égal à `Daily` et `Date Range` égal à la période contrôlée.

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Sélectionnez `Run Report`.

1. Dans la liste déroulante `File Format`, sélectionnez `CSV`.  Cliquez sur **[!UICONTROL Download]**.

   ![exporter les données d&#39;affiliation cj](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Une fois le fichier téléchargé, vous pouvez [télécharger le fichier](../connecting-data/using-file-uploader.md) vers votre Data Warehouse [!DNL Commerce Intelligence].

   Vous créez ainsi une table dans votre Data Warehouse [!DNL Commerce Intelligence] dans laquelle vous pouvez continuer à charger régulièrement des données actualisées. Lors du téléchargement du fichier, suivez les exigences de formatage répertoriées dans [Utilisation du téléchargeur de fichier](../connecting-data/using-file-uploader.md).
