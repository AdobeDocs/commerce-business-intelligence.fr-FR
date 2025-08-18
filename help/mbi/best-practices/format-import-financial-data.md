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

# Formater et importer des données financières

Cette rubrique décrit le meilleur moyen d&#39;importer des données financières pour les analyser dans [!DNL Adobe Commerce Intelligence].

Un tableau de données bidimensionnel et à onglets croisés est souvent le format utilisé pour les données financières. Avec des valeurs classées par libellés à la fois dans les colonnes et les lignes, ce type de mise en page peut être facile à voir pour les yeux humains et les tableurs, mais il n&#39;est pas adapté aux bases de données.

![](../../mbi/assets/crosstab.png)

Pour importer et analyser ces données dans [!DNL Commerce Intelligence], le tableau doit être aplati en une liste unidimensionnelle. Lorsqu’elle est aplatie, chaque valeur de données est classée par plusieurs libellés qui se trouvent tous dans une seule ligne, où chaque ligne est unique ou aurait un identifiant unique, par exemple une colonne de clé primaire.

![](../../mbi/assets/flattened.png)

## Formatage de fichiers Excel pour l’importation

Pour aplatir un tableau bidimensionnel à l’aide d’un tableau croisé dynamique [!DNL Excel] :

1. Ouvrez le fichier avec le tableau de données bidimensionnel.
1. Ouvrez l&#39;Assistant Tableau croisé dynamique. En [!DNL Windows], le raccourci est `Alt-D`. Dans [!DNL Mac OS], saisissez `Command-Option-P`.
1. Sélectionnez **[!UICONTROL Multiple consolidated ranges]** et cliquez sur **[!UICONTROL Next]**.
1. Sélectionnez **[!UICONTROL I will create the page fields]** et cliquez sur **[!UICONTROL Next]**.
1. Sélectionnez l’ensemble du jeu de données dans le tableau bidimensionnel, y compris les libellés. Assurez-vous que `0` est sélectionné pour le nombre de champs de page souhaité, puis cliquez sur **[!UICONTROL Next]**.
1. Créez le tableau croisé dynamique dans une nouvelle feuille et cliquez sur **[!UICONTROL Finish]**.
1. Désélectionnez les champs de colonne et de ligne dans la liste des champs.
1. Double-cliquez sur la valeur numérique résultante pour afficher les données source aplaties dans une nouvelle feuille.
   ![](../../mbi/assets/pivot-table-double-click.png)
1. Enregistrez-le en tant que fichier `CSV`.

## Conclusion

Le tableau de données a été converti au format liste, conservant toutes ses informations d’origine, et peut désormais être [importé dans [!DNL Commerce Intelligence]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) pour analyse.
