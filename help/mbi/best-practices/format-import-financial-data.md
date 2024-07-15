---
title: Formatage et importation de données financières
description: Découvrez comment formater et importer des données financières.
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Format et importation des données financières

Cette rubrique décrit la meilleure manière d’importer des données financières pour une analyse dans [!DNL Adobe Commerce Intelligence].

Un tableau de données à deux dimensions sur plusieurs onglets est souvent le format utilisé pour les données financières. Avec des valeurs classées par libellé à la fois dans les colonnes et les lignes, ce type de disposition peut être facile à visualiser à l’aide des yeux humains et des outils de tableur, mais il n’est pas adapté aux bases de données.

![](../../mbi/assets/crosstab.png)

Pour importer et analyser ces données dans [!DNL Commerce Intelligence], la table doit être aplatie dans une liste unidimensionnelle. Une fois aplatie, chaque valeur de données est classée par plusieurs libellés qui se trouvent tous dans une seule ligne, où chaque ligne est unique ou aurait un identifiant unique, par exemple une colonne de clé primaire.

![](../../mbi/assets/flattened.png)

## Formatage de fichiers Excel pour l’importation

Pour aplatir un tableau bidimensionnel à l’aide d’un tableau croisé dynamique [!DNL Excel] :

1. Ouvrez le fichier avec le tableau de données bidimensionnel.
1. Ouvrez l’Assistant Tableau croisé dynamique. Dans [!DNL Windows], le raccourci est `Alt-D`. Dans [!DNL Mac OS], saisissez `Command-Option-P`.
1. Sélectionnez **[!UICONTROL Multiple consolidated ranges]** et cliquez sur **[!UICONTROL Next]**.
1. Sélectionnez **[!UICONTROL I will create the page fields]** et cliquez sur **[!UICONTROL Next]**.
1. Sélectionnez l’ensemble des données du tableau bidimensionnel, y compris les libellés. Vérifiez que `0` est sélectionné pour le nombre de champs de page de votre choix et cliquez sur **[!UICONTROL Next]**.
1. Créez le tableau croisé dynamique dans une nouvelle feuille et cliquez sur **[!UICONTROL Finish]**.
1. Désélectionnez les champs de colonne et de ligne dans la liste des champs.
1. Double-cliquez sur la valeur numérique obtenue pour afficher les données source aplaties dans une nouvelle feuille.
   ![](../../mbi/assets/pivot-table-double-click.png)
1. Enregistrez en tant que fichier `CSV`.

## Remplissage

Le tableau de données a été converti au format liste, conservant toutes ses informations d’origine, et peut désormais être [importé dans [!DNL Commerce Intelligence]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) pour analyse.
