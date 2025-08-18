---
title: Utiliser le téléchargeur de fichier
description: Découvrez comment placer toutes vos données dans un seul Data Warehouse.
exl-id: 28db0e78-0222-431d-bbb9-6ef133686603
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 0%

---

# Utiliser le téléchargeur de fichier

>[!NOTE]
>
>Nécessite des [autorisations d’administrateur](../../../administrator/user-management/user-management.md).

[!DNL Adobe Commerce Intelligence] est puissant non seulement en raison de ses fonctionnalités de visualisation, mais aussi parce qu’il vous permet de placer toutes vos données dans un seul Data Warehouse. Même les données qui se trouvent en dehors de vos bases de données et intégrations peuvent être importées dans [!DNL Commerce Intelligence] à l’aide de l’outil de chargement de fichier dans le gestionnaire Data Warehouse.

Utilisez les campagnes publicitaires comme exemple. Si vous exécutez des campagnes en ligne et hors ligne, vous ne pouvez pas obtenir une vue d’ensemble si vous analysez uniquement les données d’une intégration en ligne. Le chargement d’une feuille de calcul avec les données de campagne hors ligne vous permet d’analyser les deux ensembles de données et de mieux comprendre les performances de votre campagne.

## Restrictions et exigences {#require}

1. **Le seul format pris en charge pour les chargements de fichiers est `CSV` ou`comma separated values`**. Si vous travaillez dans Excel, vous pouvez utiliser la fonction Enregistrer sous pour enregistrer le fichier au format `.csv`.
1. Les fichiers **`CSV`doivent utiliser`UTF-8 encoding`**. La plupart du temps, ce n&#39;est pas un problème. Si vous rencontrez cette erreur lors du chargement d’un fichier, [consultez cet article de support technique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolving-utf-8-errors-for-csv-file-uploads.html).
1. **La taille des fichiers ne peut pas dépasser 100MB**. Si le fichier est plus volumineux que cette taille, séparez le tableau en blocs et enregistrez-les en tant que fichiers individuels. Vous pouvez ajouter les données après le chargement du fichier initial.
1. **Toutes les tables doivent avoir un`primary key`**. Il doit y avoir au moins une colonne dans votre tableau qui peut être utilisée comme `primary key`, ou un identifiant unique pour chaque ligne du tableau. Toute colonne désignée comme `primary key` ne peut *jamais* être nulle. Un `primary key` peut être aussi simple que l’ajout d’une colonne qui donne un nombre à chaque ligne, ou peut être constitué de deux colonnes concaténées pour former une colonne de valeurs uniques (par exemple, `campaign name` et `date`).

   Si une ou plusieurs colonnes sont désignées comme uniques mais qu&#39;il existe des doublons, les lignes en double ne sont pas importées.

## Formatage des données pour le chargement {#formatting}

Avant de télécharger vos données dans [!DNL Commerce Intelligence], vérifiez qu’elles sont formatées conformément aux instructions de cette section.

### Ligne d’en-tête {#header}

Pour vous assurer que les colonnes sont correctement étiquetées et importées, veillez à ce que la première ligne de votre feuille de calcul soit un en-tête qui décrit les données de chaque colonne.

Les noms des colonnes doivent être uniques et contenir uniquement des lettres, des chiffres, des espaces et les symboles suivants : `$ % # /`. Si un nom de colonne contient une virgule, il est divisé en deux colonnes lors du chargement du fichier. En outre, Adobe recommande que le fichier contienne moins de 85 colonnes pour optimiser la vitesse de mise à jour.

### Données avec virgules {#commas}

Comme les fichiers doivent être au format `CSV`, l’utilisation de virgules peut entraîner des problèmes lors du chargement des données. `CSV` fichiers utilisent des virgules pour indiquer les nouvelles valeurs. Par conséquent, une colonne portant un nom tel que `Campaigns` `August` est lue comme deux colonnes (`Campaigns` et `August`) au lieu d’une, déplaçant toutes vos données sur une seule ligne. Adobe recommande d’éviter les virgules dans la mesure du possible. Vous pouvez utiliser `Data Preview` pour vérifier si vos données s’affichent correctement une fois la mise à jour terminée.

### Dates

Tout jeu de données contenant des dates doit utiliser le [format de date standard](https://dev.mysql.com/doc/refman/5.7/en/datetime.html) `YYYY-MM-DD HH:MM:SS` ou `MM/DD/YYYY`.

### Caractères spéciaux

Certains caractères spéciaux ne sont pas acceptés. Par exemple, le symbole de barre verticale `& # 1 2 4` est interprété comme créant une colonne et provoque des erreurs lors du chargement d’un fichier.

### Nombres Décimaux

Le type de données des valeurs monétaires doit être `Decimal Number` sélectionné, et ces colonnes arrondies automatiquement à deux décimales dans votre Data Warehouse. Si vous ne souhaitez pas arrondir vos nombres décimaux ou avoir un degré de précision supérieur à cette valeur, vous devez sélectionner le type de données `Non-Currency Decimal Number`.

### Pourcentages

Les pourcentages doivent être saisis sous forme de décimales. Par exemple :

| **Droite :** | **Faux:** |
|-----|-----|
| `.05` | `5%` |
| `.23` | `23` |

{style="table-layout:auto"}

### Valeurs avec des zéros au début et/ou à la fin {#zeroes}

Certaines valeurs de votre fichier, telles que les codes postaux et les identifiants, peuvent commencer ou se terminer par des zéros. Pour vous assurer que les zéros sont correctement conservés et chargés, vous pouvez modifier le type de mise en forme (par exemple, [de nombre à texte](https://support.microsoft.com/en-us/office/format-numbers-as-text-583160db-936b-4e52-bdff-6f1863518ba4?ui=en-us&rs=en-us&ad=us)) ou appliquer la mise en forme des nombres.

Utilisez `US ZIP codes` comme exemple de modification de la mise en forme des nombres. Dans [!DNL Excel], mettez en surbrillance la colonne contenant `ZIP codes` et [modifiez le format des nombres](https://support.microsoft.com/en-us/office/display-numbers-as-postal-codes-61b55c9f-6fe3-4e54-96ca-9e85c38a5a1d?ui=en-us&rs=en-us&ad=us) en `ZIP code`. Vous pouvez également sélectionner un format de nombre personnalisé, puis saisir des `Type` dans la fenêtre `00000`. Gardez à l&#39;esprit que cette méthode peut présenter des problèmes si certains codes sont formatés en `00000` et d&#39;autres en `00000-0000`.

Le `Type` peut être [ formaté différemment pour s’adapter à d’autres types de données](https://support.microsoft.com/en-us/office/keeping-leading-zeros-and-large-numbers-1bf7b935-36e1-4985-842f-5dfa51f85fe7?correlationid=e1d4c2d3-cd5d-4a14-999d-437800274a90&ui=en-us&rs=en-us&ad=us) tels que les identifiants. Si un `ID` comporte neuf chiffres, par exemple, le `Type` peut être `000000000` ou `000-000-000`. Cela changerait `123456` en `000-123-456`.

Pour obtenir des ressources [!DNL Google Docs] et [!DNL Apple Numbers], reportez-vous à la liste [connexes](#related) au bas de cette page.

## Chargement des données {#uploading}

Maintenant que votre feuille de calcul est correctement formatée et [!DNL Commerce Intelligence], ajoutez-la à votre Data Warehouse.

1. Pour commencer, rendez-vous sur **[!UICONTROL Data** > **File Uploads]**.

1. Cliquez sur l’onglet **[!UICONTROL Upload to New Table]** .

1. Cliquez sur **[!UICONTROL Choose File]** et sélectionnez le fichier. Cliquez sur **[!UICONTROL Open]** pour démarrer le chargement.

   Une fois le chargement terminé, une liste des colonnes [!DNL Commerce Intelligence] dans votre fichier s’affiche.

1. Vérifiez que les noms des colonnes et les types de données sont corrects. Plus précisément, vérifiez que toutes les colonnes de date sont lues comme des dates et non des nombres.

   >[!NOTE]
   >
   >Le `datatype` est important, alors ne passez pas cette étape !

1. Sélectionnez la ou les colonnes qui constituent la `primary key` du tableau à l’aide des cases à cocher situées sous l’icône clé.

1. Nommez la table.

1. Cliquez sur **[!UICONTROL Save Table]**.

Un *Succès !* message s’affiche en haut de l’écran une fois le tableau enregistré.

Si vous avez besoin d’un visuel, examinez l’ensemble du processus :

![](../../../assets/fileupload.gif)

Les tableaux chargés s’affichent sous la section **Chargements de fichiers** de la liste des tableaux (dans les options Toutes les tables et Tables synchronisées) dans le gestionnaire Data Warehouse :

![](../../../assets/upload-tables.png)

## Mise à jour ou ajout de données à une table existante {#appending}

Vous avez de nouvelles données à ajouter à un fichier que vous avez déjà chargé ? Aucun problème : vous pouvez facilement mettre à jour et ajouter des données dans [!DNL Commerce Intelligence].

1. Pour commencer, rendez-vous sur **[!UICONTROL Manage Data** > **File Uploads]**.

1. Cliquez sur l’onglet **[!UICONTROL Edit/Upload `.csv`aux tables existantes]**.

1. Dans la liste déroulante, cliquez sur le nom du tableau à mettre à jour ou à ajouter.

1. Utilisez la liste déroulante pour sélectionner l’option de gestion des lignes en double :

   | Option | Description |
   |---|---|
   | `Overwrite old row with new row` | Les données existantes sont remplacées par les nouvelles données si une ligne possède la même clé primaire dans la table existante et le nouveau fichier. Il s’agit de la méthode à utiliser pour les colonnes dont les valeurs changent au fil du temps, par exemple, une colonne Statut . Les données existantes sont remplacées et mises à jour avec les nouvelles données. Les lignes contenant des clés primaires qui ne figurent pas dans le tableau existant sont ajoutées en tant que nouvelles lignes. |
   | `Retain old row; discard new row` | Les nouvelles données sont alors ignorées si une ligne possède la même clé primaire à la fois dans la table existante et dans le nouveau fichier. |
   | `Purge all existing rows first and ignore duplicate keys within the file` | Cela supprime toutes les données existantes et les remplace par les nouvelles données du fichier. N&#39;utilisez cette option que si vous n&#39;avez besoin d&#39;aucune des données de la table existante. |

1. Cliquez sur **[!UICONTROL Choose File]** et sélectionnez le fichier.

1. Cliquez sur **[!UICONTROL Open]** pour démarrer le chargement.

   Une fois le chargement terminé, [!DNL Commerce Intelligence] validera la structure de données dans le fichier . Un *Succès !* message s’affiche en haut de l’écran une fois le tableau enregistré.

## Disponibilité des données {#availability}

Tout comme les colonnes calculées, les données des chargements de fichiers sont disponibles une fois le cycle de mise à jour suivant terminé. Si une mise à jour était en cours pendant le chargement du fichier, les données ne seront pas disponibles avant la prochaine mise à jour. Une fois le cycle de mise à jour terminé, vous pouvez accéder à l’onglet `Data Preview` dans votre Data Warehouse pour vous assurer que le fichier chargé et les données s’affichent correctement.

## Conclusion {#wrapup}

Cette rubrique ne couvrait que les principes de base de l’utilisation de l’importation de données, mais vous souhaiterez peut-être faire quelque chose de plus avancé. Consultez les articles connexes pour obtenir des conseils sur le formatage et l’importation de données financières, d’e-commerce, de dépenses et d’autres types de données.

En outre, le téléchargement de fichiers n’est pas le seul moyen d’importer vos données dans [!DNL Commerce Intelligence]. Les fonctions [API d’importation de données](https://developer.adobe.com/commerce/services/reporting/import-api/) vous permettent d’envoyer des données arbitraires dans votre Data Warehouse [!DNL Commerce Intelligence].

## Connexe {#related}

* [Formater et importer des données financières](../../../best-practices/format-import-financial-data.md)
* [Importation de données hors ligne/autres données de dépenses publicitaires](../connecting-data/import-offline-ad-data.md)
* [Données attendues[!DNL Google ECommerce]](../integrations/google-ecommerce-data.md)

## Ressources Tierces

* [Guide de formatage des données numériques](http://www.dummies.com/how-to/content/how-to-choose-a-number-format-in-your-numbers-spre.html)
* [[!DNL Google Docs]  Guide de formatage des données ](https://support.google.com/docs/answer/56470?hl=en)
