---
title: Importation de données MailChimp
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

Pour obtenir une vue d&#39;ensemble complète de vos efforts de campagne, vous pouvez importer vos données de campagne par courrier électronique [!DNL Mailchimp] dans [!DNL Commerce Intelligence]. Pour terminer l&#39;import, vous devez effectuer les opérations suivantes pour chaque campagne [!DNL Mailchimp] que vous avez :

## Exporter les données Ouvertures {#opens}

1. Après vous être connecté à [!DNL Mailchimp], accédez à l’onglet `Campaigns` .

   ![import mailchimp 1](../../../assets/import-mailchimp-1.png)

1. Cliquez sur **[!UICONTROL View Report]** en regard du nom de la campagne.

   ![import mailchimp 2](../../../assets/import-mailchimp-2.png)

1. Cliquez sur le numéro **[!UICONTROL Opened]**.

   ![import mailchimp 3](../../../assets/import-mailchimp-3.png)

1. Cliquez sur **[!UICONTROL Export]** et enregistrez le fichier `.csv`.

   Vous devez ajouter des colonnes `primary key`, `date (mm/dd/yyyy)` et `campaign name` à ce fichier. Assurez-vous que les `primary keys` sont uniques à chaque ligne.

   ![import mailchimp 4](../../../assets/import-mailchimp-4.png)

## Exporter les données Clics {#clicks}

1. Revenez à l’écran `View Report` de la campagne.

1. Cliquez sur le nombre `Clicked`.

   ![import mailchimp 5](../../../assets/import-mailchimp-5.png)

1. Cliquez sur le nombre situé sous la colonne `Total Clicks` OU `Unique Clicks`.

   ![import mailchimp 6](../../../assets/import-mailchimp-6.png)

1. Cliquez sur **[!UICONTROL Export]** et enregistrez le fichier `.csv`.

   Vous devez ajouter des colonnes `Primary Key`, `date (mm/dd/yyyy)`, `campaign name` et `URL` à ce fichier. Vous n’avez pas besoin d’ajouter l’URL complète, simplement un élément qui vous permet de savoir ce qui a été cliqué.

   ![import mailchimp 7](../../../assets/import-mailchimp-7.png)

1. Répétez les étapes 3 et 4 pour chaque URL cliquée dans votre email, en combinant toutes les données dans le même fichier `.csv` une fois terminé.

## Exporter les données envoyées {#sent}

1. Accédez à l’onglet `Campaigns` de [!DNL Mailchimp].

1. Cliquez sur **[!UICONTROL View Report]** en regard du nom de la campagne.

1. Cliquez sur le numéro en regard de `Recipients`.

   ![import mailchimp 8](../../../assets/import-mailchimp-8.png)

1. Cliquez sur **[!UICONTROL Export]** et enregistrez le fichier `.csv`.

   Vous devez ajouter des colonnes `Primary Key`, `date (mm/dd/yyyy)` et `campaign name` à ce fichier.

   ![import mailchimp 9](../../../assets/import-mailchimp-9.png)

## Préparer le chargement des fichiers dans [!DNL Commerce Intelligence] {#upload}

Chaque fichier - `Opens`, `Clicks` et `Sent` - doit être chargé dans [!DNL Commerce Intelligence] en tant que fichier distinct. Adobe vous recommande de nommer les fichiers en utilisant cette convention d’affectation des noms : `MailChimp\_ACTION\_DATE`. Remplacez `ACTION` par `Open`, `Click` ou `Sent`, puis remplacez `DATE` par la date d’exportation.

Lorsque vous êtes prêt à charger les fichiers, utilisez la fonction [`File Upload`](../connecting-data/using-file-uploader.md) pour importer les données dans votre Data Warehouse.
