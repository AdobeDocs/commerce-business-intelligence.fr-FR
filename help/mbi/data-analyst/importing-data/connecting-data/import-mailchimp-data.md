---
title: Importer les données MailChimp
description: Découvrez comment importer des données MailChimp dans  [!DNL Commerce Intelligence].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Importer les données [!DNL Mailchimp]

Pour obtenir une vue d’ensemble complète de vos efforts de campagne, vous pouvez importer vos données de campagne par e-mail [!DNL Mailchimp] dans [!DNL Commerce Intelligence]. Pour terminer l’importation, vous devez effectuer les opérations suivantes pour chaque campagne [!DNL Mailchimp] en cours :

## Exporter les données d&#39;ouvertures {#opens}

1. Après vous être connecté à [!DNL Mailchimp], accédez à l’onglet `Campaigns` .

   ![importer mailchimp 1](../../../assets/import-mailchimp-1.png)

1. Cliquez sur **[!UICONTROL View Report]**, en regard du nom de la campagne.

   ![importer mailchimp 2](../../../assets/import-mailchimp-2.png)

1. Cliquez sur le numéro de **[!UICONTROL Opened]**.

   ![importer mailchimp 3](../../../assets/import-mailchimp-3.png)

1. Cliquez sur **[!UICONTROL Export]** et enregistrez le fichier `.csv`.

   Vous devez ajouter des colonnes `primary key`, `date (mm/dd/yyyy)` et `campaign name` à ce fichier. Assurez-vous que les `primary keys` sont propres à chaque ligne.

   ![importer mailchimp 4](../../../assets/import-mailchimp-4.png)

## Exporter les données de clics {#clicks}

1. Revenez à l’écran `View Report` de la campagne.

1. Cliquez sur le numéro qui `Clicked`.

   ![importer mailchimp 5](../../../assets/import-mailchimp-5.png)

1. Cliquez sur le nombre sous la colonne `Total Clicks` OU `Unique Clicks`.

   ![importer mailchimp 6](../../../assets/import-mailchimp-6.png)

1. Cliquez sur **[!UICONTROL Export]** et enregistrez le fichier `.csv`.

   Vous devez ajouter des colonnes `Primary Key`, `date (mm/dd/yyyy)`, `campaign name` et `URL` à ce fichier. Vous n’avez pas besoin d’ajouter l’URL complète, simplement quelque chose qui vous permet de savoir ce qui a été cliqué.

   ![importer mailchimp 7](../../../assets/import-mailchimp-7.png)

1. Répétez les étapes 3 et 4 pour chaque URL sur laquelle vous avez cliqué dans votre e-mail, en combinant toutes les données dans le même fichier `.csv` une fois l’opération terminée.

## Exporter les données envoyées {#sent}

1. Accédez à l’onglet `Campaigns` de [!DNL Mailchimp].

1. Cliquez sur **[!UICONTROL View Report]** en regard du nom de la campagne.

1. Cliquez sur le nombre en regard de `Recipients`.

   ![importer mailchimp 8](../../../assets/import-mailchimp-8.png)

1. Cliquez sur **[!UICONTROL Export]** et enregistrez le fichier `.csv`.

   Vous devez ajouter des colonnes `Primary Key`, `date (mm/dd/yyyy)` et `campaign name` à ce fichier.

   ![importer mailchimp 9](../../../assets/import-mailchimp-9.png)

## Préparation des fichiers à charger dans [!DNL Commerce Intelligence] {#upload}

Chaque fichier (`Opens`, `Clicks` et `Sent`) doit être téléchargé vers [!DNL Commerce Intelligence] en tant que fichier distinct. Adobe vous recommande de nommer les fichiers à l’aide de la convention de nommage suivante : `MailChimp\_ACTION\_DATE`. Remplacez `ACTION` par `Open`, `Click` ou `Sent`, puis remplacez `DATE` par la date d’exportation.

Lorsque vous êtes prêt à charger les fichiers, utilisez la fonction [`File Upload` pour &#x200B;](../connecting-data/using-file-uploader.md) les données dans votre Data Warehouse.
