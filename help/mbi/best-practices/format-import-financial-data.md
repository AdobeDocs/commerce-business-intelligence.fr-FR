---
title: Formatage et importation de données financières
description: Découvrez comment formater et importer des données financières.
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
role: Admin, Developer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
TQID: https://experienceleague.adobe.com/O1WKa98rRVw1dcgNQPsORit2gmZNn1Wi7H-Q4J7KcA0
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 278
ht-degree: 0%

---

# Formater et importer des données financières

Cette rubrique décrit le meilleur moyen d&#39;importer des données financières pour les analyser dans [!DNL Adobe Commerce Intelligence].

Un tableau de données bidimensionnel et à onglets croisés est souvent le format utilisé pour les données financières. Avec des valeurs classées par libellés à la fois dans les colonnes et les lignes, ce type de mise en page peut être facile à voir pour les yeux humains et les tableurs, mais il n&#39;est pas adapté aux bases de données.

![Format Matrice affichant les données dans une disposition de tableau croisé dynamique](../../mbi/assets/crosstab.png)

Pour importer et analyser ces données dans [!DNL Commerce Intelligence], le tableau doit être aplati en une liste unidimensionnelle. Lorsqu’elle est aplatie, chaque valeur de données est classée par plusieurs libellés qui se trouvent tous dans une seule ligne, où chaque ligne est unique ou aurait un identifiant unique, par exemple une colonne de clé primaire.

![Format aplati affichant les données en colonnes](../../mbi/assets/flattened.png)

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
   ![Liste de champs de tableau croisé dynamique Excel affichant un double-clic pour développer](../../mbi/assets/pivot-table-double-click.png)
1. Enregistrez-le en tant que fichier `CSV`.

## Conclusion

Le tableau de données a été converti au format liste, conservant toutes ses informations d’origine, et peut désormais être [importé dans [!DNL Commerce Intelligence]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) pour analyse.
