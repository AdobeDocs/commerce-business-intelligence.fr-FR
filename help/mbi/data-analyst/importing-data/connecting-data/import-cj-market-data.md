---
title: Importation des données marketing des affiliés CJ (Commission Junction)
description: Découvrez comment importer des données d’affilié CJ (Commission Junction) dans  [!DNL Commerce Intelligence].L Commerce Intelligence&rbrack;.
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Importer les données [!DNL CJ Affiliate]

Pour importer des données [!DNL CJ Affiliate (Commission Junction)] dans [!DNL Adobe Commerce Intelligence], suivez les étapes ci-dessous et joignez le fichier obtenu à un [ ticket de support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr). Adobe configure le tableau de données de votre compte et vous permet de continuer à charger les données indépendamment.

## Exporter les données [!DNL CJ Affiliate]

1. Dans votre compte [!DNL CJ Affiliate], accédez à l’onglet `Reports` .

1. Dans l&#39;onglet `Performance`, sélectionnez `Report Options`.

1. Définissez `Performance By` sur `Program`, `Trend` sur `Daily` et `Date Range` sur la plage de dates faisant l’objet d’un audit.

   ![export-cj-affilié-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Sélectionnez `Run Report`.

1. Dans la liste déroulante `File Format`, sélectionnez `CSV`.  Cliquez sur **[!UICONTROL Download]**.

   ![exporter des données affiliées cj](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Après avoir téléchargé le fichier, vous pouvez [télécharger le fichier](../connecting-data/using-file-uploader.md) vers votre Data Warehouse [!DNL Commerce Intelligence].

   Cela crée un tableau dans votre Data Warehouse [!DNL Commerce Intelligence] dans lequel vous pouvez continuer à charger régulièrement des données nouvelles. Lors du téléchargement du fichier, respectez les exigences de formatage répertoriées dans [Utilisation du téléchargeur de fichiers](../connecting-data/using-file-uploader.md).
