---
title: Formatage et importation de données financières
description: Découvrez comment formater et importer des données financières.
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Format et importation des données financières

Cette rubrique décrit le meilleur moyen d’importer des données financières pour une analyse dans [!DNL MBI].

Un tableau de données à deux dimensions sur plusieurs onglets est souvent le format utilisé pour les données financières. Avec des valeurs classées par libellé dans les colonnes et les lignes, ce type de disposition peut être facile à visualiser à l’aide des yeux d’un humain et des outils de tableur, mais il n’est pas très adapté aux bases de données.

![](../../mbi/assets/crosstab.png)

Pour importer et analyser ces données dans [!DNL MBI], le tableau doit être aplati dans une liste unidimensionnelle. Une fois aplatie, chaque valeur de données est classée par plusieurs libellés qui se trouvent tous dans une seule ligne, où chaque ligne est unique ou aurait un identifiant unique, par exemple une Principale colonne de clé.

![](../../mbi/assets/flattened.png)

## Formatage de fichiers Excel pour l’importation

Pour aplatir un tableau bidimensionnel à l’aide d’un tableau croisé dynamique Excel :

1. Ouvrez le fichier avec le tableau de données bidimensionnel.
1. Ouvrez l’Assistant Tableau croisé dynamique. Sous Windows, le raccourci est `Alt-D`. Dans Mac OSX, saisissez `Command-Option-P`.
1. Sélectionner **[!UICONTROL Multiple consolidated ranges]** et cliquez sur **[!UICONTROL Next]**.
1. Sélectionner **[!UICONTROL I will create the page fields]** et cliquez sur **[!UICONTROL Next]**.
1. Sélectionnez l’ensemble des données du tableau bidimensionnel, y compris les libellés. Assurez-vous que `0` est sélectionné pour le nombre de champs de page de votre choix, puis cliquez sur **[!UICONTROL Next]**.
1. Créez un tableau croisé dynamique dans une nouvelle feuille et cliquez sur **[!UICONTROL Finish]**.
1. Désélectionnez les champs de colonne et de ligne dans la liste des champs.
1. Double-cliquez sur la valeur numérique obtenue pour afficher les données source aplaties dans une nouvelle feuille.
   ![](../../mbi/assets/pivot-table-double-click.png)
1. Enregistrer en tant que `CSV` fichier .

C&#39;est tout ! Le tableau de données a été converti en liste, conservant toutes ses informations d’origine, et peut désormais être [importé dans [!DNL MBI]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) pour l’analyse.
