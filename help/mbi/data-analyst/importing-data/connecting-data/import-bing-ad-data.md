---
title: Importer les données de dépenses publicitaires Bing
description: Découvrez comment importer des données de dépenses publicitaires Bing dans [!DNL Commerce Intelligence] pour analyse.
exl-id: c8dec4b4-74ce-41b2-a77d-403fe44e2816
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: 'https://experienceleague.adobe.com/66UAmNWDCkiflHxsq9X1MlkwEgzC5Cl1HfRirNd8AHM'
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
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%
---
# Importer les données [!DNL Bing]

Pour importer [!DNL Bing] données sur les dépenses publicitaires dans [!DNL Adobe Commerce Intelligence] pour analyse, il vous suffit d’exporter les données de [!DNL Bing Ads Editor] dans un format `.csv` et de les charger dans [!DNL Commerce Intelligence] comme indiqué ci-dessous.

## [!DNL Bing Ads Editor]

Pour exporter vos données [!DNL Bing Ads], des [!DNL Bing Ads Editor] doivent être installés. Tu peux trouver un téléchargement gratuit de [[!DNL Bing Ads Editor]](https://about.ads.microsoft.com/en-us/solutions/tools/editor).

## Exportation de données [!DNL Bing Ads]

1. Dans le volet de `Browser` d’[!DNL Bing Ads Editor], cliquez avec le bouton droit sur la campagne ou le groupe publicitaire à exporter, puis cliquez sur **[!UICONTROL Export]**.
1. Dans la boîte de dialogue `Export`, cliquez sur **[!UICONTROL Export]**.
1. Dans la boîte de dialogue `Save As`, cliquez sur le dossier dans lequel vous souhaitez enregistrer votre fichier d’exportation.
1. Dans la zone de `File name`, choisissez un nom pour votre exportation de fichier.
1. Cliquez sur **[!UICONTROL Save]**.
1. Une fois le fichier téléchargé, [contactez l’assistance technique](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies) pour effectuer un premier chargement en votre nom et configurer les dimensions back-end nécessaires.
