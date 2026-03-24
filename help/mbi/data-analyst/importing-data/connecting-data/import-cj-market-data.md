---
title: Importation des données marketing de l'affilié CJ (Commission Junction)
description: Découvrez comment importer des données d’affilié CJ (Commission Junction) dans  [!DNL Commerce Intelligence].L Commerce Intelligence].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
TQID: https://experienceleague.adobe.com/tZ2fzAKou0fBmkmKD5zdLFBNCSiAGpT3GNgkHp9ptx4
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 141
ht-degree: 0%

---

# Importer les données [!DNL CJ Affiliate]

Pour importer [!DNL CJ Affiliate (Commission Junction)] données dans [!DNL Adobe Commerce Intelligence], procédez simplement comme suit et joignez le fichier obtenu à un ticket d’assistance [](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html). Adobe configure la table de données de votre compte et vous permet de continuer à charger des données indépendamment.

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
