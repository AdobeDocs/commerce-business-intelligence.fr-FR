---
title: Importation de données MailChimp
description: Découvrez comment importer des données MailChimp dans [!DNL Commerce Intelligence].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Importer [!DNL Mailchimp] data

Pour obtenir une vue d’ensemble complète de vos efforts de campagne, vous pouvez importer votre [!DNL Mailchimp] données de campagne par e-mail dans [!DNL Commerce Intelligence]. Pour terminer l&#39;import, vous devez effectuer les opérations suivantes pour chaque [!DNL Mailchimp] campagne que vous avez :

## Exporter les données Ouvertures {#opens}

1. Après vous être connecté à [!DNL Mailchimp], accédez au `Campaigns` .

   ![import mailchimp 1](../../../assets/import-mailchimp-1.png)

1. Cliquez sur **[!UICONTROL View Report]**, en regard du nom de la campagne.

   ![import mailchimp 2](../../../assets/import-mailchimp-2.png)

1. Cliquez sur le bouton **[!UICONTROL Opened]** Nombre.

   ![import mailchimp 3](../../../assets/import-mailchimp-3.png)

1. Cliquez sur **[!UICONTROL Export]** et enregistrez la variable `.csv` fichier .

   Vous devez ajouter `primary key`, `date (mm/dd/yyyy)`, et `campaign name` à ce fichier. Assurez-vous que la variable `primary keys` sont propres à chaque ligne.

   ![import mailchimp 4](../../../assets/import-mailchimp-4.png)

## Exporter les données Clics {#clicks}

1. Revenez au `View Report` écran de la campagne.

1. Cliquez sur le nombre `Clicked`.

   ![import mailchimp 5](../../../assets/import-mailchimp-5.png)

1. Cliquez sur l’un des nombres sous la propriété `Total Clicks` OU `Unique Clicks` colonne .

   ![import mailchimp 6](../../../assets/import-mailchimp-6.png)

1. Cliquez sur **[!UICONTROL Export]** et enregistrez la variable `.csv` fichier .

   Vous devez ajouter `Primary Key`, `date (mm/dd/yyyy)`, `campaign name`, et `URL` à ce fichier. Vous n’avez pas besoin d’ajouter l’URL complète, simplement un élément qui vous permet de savoir ce qui a fait l’objet d’un clic.

   ![import mailchimp 7](../../../assets/import-mailchimp-7.png)

1. Répétez les étapes 3 et 4 pour chaque URL cliquée dans votre email, en combinant toutes les données dans le même `.csv` une fois terminé.

## Exporter les données envoyées {#sent}

1. Accédez au `Campaigns` de [!DNL Mailchimp].

1. Cliquez sur **[!UICONTROL View Report]** en regard du nom de la campagne.

1. Cliquez sur le numéro en regard de `Recipients`.

   ![import mailchimp 8](../../../assets/import-mailchimp-8.png)

1. Cliquez sur **[!UICONTROL Export]** et enregistrez la variable `.csv` fichier .

   Vous devez ajouter `Primary Key`, `date (mm/dd/yyyy)`, et `campaign name` à ce fichier.

   ![import mailchimp 9](../../../assets/import-mailchimp-9.png)

## Préparation du chargement de fichiers dans [!DNL Commerce Intelligence] {#upload}

Chaque fichier - `Opens`, `Clicks`, et `Sent` - doit être chargé dans [!DNL Commerce Intelligence] comme un fichier distinct. Adobe vous recommande de nommer les fichiers selon cette convention d’affectation des noms : `MailChimp\_ACTION\_DATE`. Remplacer `ACTION` avec `Open`, `Click`ou `Sent`et remplacez `DATE` avec la date d&#39;export.

Lorsque vous êtes prêt à charger les fichiers, utilisez la variable [`File Upload` fonctionnalité](../connecting-data/using-file-uploader.md) pour importer les données dans votre Data Warehouse.
