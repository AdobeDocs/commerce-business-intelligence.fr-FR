---
title: Utilisation du téléchargement de fichier
description: Découvrez comment placer toutes vos données dans un seul Data Warehouse.
exl-id: 28db0e78-0222-431d-bbb9-6ef133686603
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 0%

---

# Utilisation du téléchargement de fichier

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

[!DNL Adobe Commerce Intelligence] est puissant non seulement en raison de ses fonctionnalités de visualisation, mais également parce qu’il vous permet de placer toutes vos données dans un seul Data Warehouse. Même les données qui résident en dehors de vos bases de données et intégrations peuvent être introduites dans [!DNL Commerce Intelligence] à l’aide de l’outil de téléchargement de fichiers dans le Gestionnaire de Data Warehouse.

Utilisez les campagnes publicitaires comme exemple. Si vous exécutez des campagnes en ligne et hors ligne, vous ne pouvez pas obtenir une vue d’ensemble si vous analysez uniquement les données d’une intégration en ligne. Le téléchargement d’une feuille de calcul avec les données de campagne hors ligne vous permet d’analyser les deux ensembles de données et de mieux comprendre les performances de votre campagne.

## Restrictions et exigences {#require}

1. **Le seul format pris en charge pour les téléchargements de fichiers est `CSV` ou`comma separated values`**. Si vous travaillez dans Excel, vous pouvez utiliser la fonction Enregistrer sous pour enregistrer le fichier au format `.csv`.
1. Les fichiers **`CSV`doivent utiliser`UTF-8 encoding`**. La plupart du temps, ce n&#39;est pas un problème. Si vous rencontrez cette erreur lors du téléchargement d’un fichier, [consultez cet article de support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolving-utf-8-errors-for-csv-file-uploads.html).
1. **Les fichiers ne peuvent pas dépasser 100 Mo**. Si le fichier est plus volumineux, séparez le tableau en blocs et enregistrez-le sous forme de fichiers individuels. Vous pouvez ajouter les données après le chargement du fichier initial.
1. **Toutes les tables doivent avoir un`primary key`**. Votre table doit comporter au moins une colonne pouvant être utilisée comme `primary key` ou un identifiant unique pour chaque ligne du tableau. Toute colonne désignée comme `primary key` peut *never* être nulle. Un `primary key` peut être aussi simple que l’ajout d’une colonne qui donne un nombre à chaque ligne ou peut être deux colonnes concaténées pour créer une colonne de valeurs uniques (par exemple, `campaign name` et `date`).

   Si une ou plusieurs colonnes sont désignées comme uniques, mais qu’il existe des doublons, les lignes en double ne sont pas importées.

## Formatage des données à charger {#formatting}

Avant de pouvoir charger vos données dans [!DNL Commerce Intelligence], vérifiez qu&#39;elles sont formatées conformément aux instructions de cette section.

### Rangée d’en-tête {#header}

Pour vous assurer que les colonnes sont correctement étiquetées et importées, assurez-vous que la première ligne de votre feuille de calcul est un en-tête qui décrit les données de chaque colonne.

Les noms de colonne doivent être uniques et contenir uniquement des lettres, des chiffres, des espaces et ces symboles : `$ % # /`. Si un nom de colonne contient une virgule, il est divisé en deux colonnes lors du chargement du fichier. Adobe recommande également qu’il y ait moins de 85 colonnes dans le fichier pour optimiser la vitesse de mise à jour.

### Données avec virgules {#commas}

Comme les fichiers doivent être au format `CSV`, l’utilisation de virgules peut entraîner des problèmes lors du transfert des données. Les fichiers `CSV` utilisent des virgules pour indiquer de nouvelles valeurs. Par conséquent, une colonne portant le nom `Campaigns`, `August` est lue sous la forme de deux colonnes (`Campaigns` et `August`) au lieu d’une seule, déplaçant toutes vos données sur une seule ligne. Adobe recommande d’éviter les virgules chaque fois que possible. Vous pouvez utiliser `Data Preview` pour vérifier si vos données s’affichent correctement une fois une mise à jour terminée.

### Dates

Tout jeu de données contenant des dates doit utiliser le [format de date standard](https://dev.mysql.com/doc/refman/5.7/en/datetime.html) `YYYY-MM-DD HH:MM:SS` ou `MM/DD/YYYY`.

### Caractères spéciaux

Certains caractères spéciaux ne sont pas acceptés. Par exemple, la barre verticale `& # 1 2 4` est interprétée comme la création d’une colonne et entraîne des erreurs lors du téléchargement d’un fichier.

### Nombre décimal

Le type de données `Decimal Number` doit être sélectionné pour les valeurs de devise et ces colonnes sont automatiquement arrondies à deux décimales dans votre Data Warehouse. Si vous ne souhaitez pas arrondir vos nombres décimaux ou avoir un degré de précision supérieur à celui-ci, vous devez sélectionner le type de données `Non-Currency Decimal Number`.

### Pourcentages

Les pourcentages doivent être renseignés en tant que décimales. Par exemple :

| **Droite :** | **Mal :** |
|-----|-----|
| `.05` | `5%` |
| `.23` | `23` |

{style="table-layout:auto"}

### Valeurs avec zéros de début et/ou de fin {#zeroes}

Certaines valeurs de votre fichier, telles que les codes postaux et les identifiants, peuvent commencer ou se terminer par des zéros. Pour vous assurer que les zéros sont correctement conservés et téléchargés, vous pouvez modifier le type de formatage (par exemple, [ du nombre au texte](https://support.microsoft.com/en-us/office/format-numbers-as-text-583160db-936b-4e52-bdff-6f1863518ba4?ui=en-us&amp;rs=en-us&amp;ad=us)) ou appliquer le formatage des nombres.

Utilisez `US ZIP codes` comme exemple de modification du formatage des nombres. Dans [!DNL Excel], mettez en surbrillance la colonne contenant `ZIP codes` et [remplacez le format de nombre](https://support.microsoft.com/en-us/office/display-numbers-as-postal-codes-61b55c9f-6fe3-4e54-96ca-9e85c38a5a1d?ui=en-us&amp;rs=en-us&amp;ad=us) par `ZIP code`. Vous pouvez également sélectionner un format de nombre personnalisé et, dans la fenêtre `Type`, saisir `00000`. Gardez à l’esprit que cette méthode peut poser des problèmes si certains codes sont formatés sous la forme `00000` et d’autres sous la forme `00000-0000`.

Le `Type` peut être [ formaté différemment selon les autres types de données ](https://support.microsoft.com/en-us/office/keeping-leading-zeros-and-large-numbers-1bf7b935-36e1-4985-842f-5dfa51f85fe7?correlationid=e1d4c2d3-cd5d-4a14-999d-437800274a90&amp;ui=en-us&amp;rs=en-us&amp;ad=us), tels que les identifiants. Si un `ID` contient neuf chiffres de long, par exemple, le `Type` peut être `000000000` ou `000-000-000`. Cela changerait `123456` en `000-123-456`.

Pour les ressources [!DNL Google Docs] et [!DNL Apple Numbers], reportez-vous à la liste [Related](#related) située au bas de cette page.

## Chargement de données {#uploading}

Maintenant que votre feuille de calcul est correctement formatée et [!DNL Commerce Intelligence] compatible, ajoutez-la à votre Data Warehouse.

1. Pour commencer, accédez à **[!UICONTROL Data** > **File Uploads]**.

1. Cliquez sur l’onglet **[!UICONTROL Upload to New Table]** .

1. Cliquez sur **[!UICONTROL Choose File]** et sélectionnez le fichier. Cliquez sur **[!UICONTROL Open]** pour lancer le téléchargement.

   Une fois le chargement terminé, une liste des colonnes [!DNL Commerce Intelligence] présentes dans votre fichier s’affiche.

1. Vérifiez que les noms des colonnes et les types de données sont corrects. Plus précisément, vérifiez que les colonnes de dates sont lues comme des dates et non comme des nombres.

   >[!NOTE]
   >
   >Le `datatype` est important. N’ignorez donc pas cette étape !

1. Sélectionnez la ou les colonnes qui composent le `primary key` du tableau à l’aide des cases à cocher situées sous l’icône de clé.

1. Nommez la table.

1. Cliquez sur **[!UICONTROL Save Table]**.

Un *Succès !Le message* s’affiche en haut de l’écran une fois votre tableau enregistré.

Si vous avez besoin d’un visuel, examinez l’ensemble du processus :

![](../../../assets/fileupload.gif)

Les tableaux téléchargés s’affichent sous la section **Téléchargements de fichiers** de la liste des tableaux (dans les options Toutes les tables et Tableaux synchronisés) dans le Gestionnaire de Data Warehouse :

![](../../../assets/upload-tables.png)

## Mettre à jour ou ajouter des données à une table existante {#appending}

Vous avez de nouvelles données à ajouter à un fichier que vous avez déjà chargé ? Aucun problème : vous pouvez facilement mettre à jour et ajouter des données dans [!DNL Commerce Intelligence].

1. Pour commencer, accédez à **[!UICONTROL Manage Data** > **File Uploads]**.

1. Cliquez sur l’onglet **[!UICONTROL Edit/Upload `.csv`vers les tables existantes]** .

1. Dans la liste déroulante, cliquez sur le nom de la table à mettre à jour ou à ajouter.

1. Utilisez la liste déroulante pour sélectionner l’option de gestion des lignes dupliquées :

   | Option | Description |
   |---|---|
   | `Overwrite old row with new row` | Cela remplace les données existantes par de nouvelles données si une ligne possède la même clé primaire dans le tableau existant et le nouveau fichier. Il s’agit de la méthode à utiliser pour les colonnes dont les valeurs changent au fil du temps, par exemple, une colonne État. Les données existantes sont écrasées et mises à jour avec les nouvelles données. Les lignes dont les clés primaires ne figurent pas dans le tableau existant sont ajoutées en tant que nouvelles lignes. |
   | `Retain old row; discard new row` | De nouvelles données sont alors ignorées si une ligne possède la même clé primaire dans le tableau existant et le nouveau fichier. |
   | `Purge all existing rows first and ignore duplicate keys within the file` | Cela supprime toutes les données existantes et les remplace par les nouvelles données du fichier. N&#39;utilisez cette option que si vous n&#39;avez pas besoin des données de la table existante. |

1. Cliquez sur **[!UICONTROL Choose File]** et sélectionnez le fichier.

1. Cliquez sur **[!UICONTROL Open]** pour lancer le téléchargement.

   Une fois le transfert terminé, [!DNL Commerce Intelligence] valide la structure de données dans le fichier. Un *Succès !Le message* s’affiche en haut de l’écran une fois votre tableau enregistré.

## Disponibilité des données {#availability}

Tout comme les colonnes calculées, les données issues des téléchargements de fichiers sont disponibles une fois le cycle de mise à jour suivant terminé. Si une mise à jour était en cours au cours du chargement du fichier, les données ne seront disponibles qu’après la prochaine mise à jour. Une fois le cycle de mise à jour terminé, vous pouvez accéder à l’onglet `Data Preview` de votre Data Warehouse pour vous assurer que le fichier a été correctement chargé et que les données s’affichent comme prévu.

## Remplissage {#wrapup}

Cette rubrique ne traitait que des principes de base de l’utilisation de l’importation de données, mais vous souhaiteriez peut-être faire quelque chose de plus avancé. Consultez les articles connexes pour en savoir plus sur le formatage et l’importation de données financières, d’e-commerce, de dépenses publicitaires et d’autres types de données.

En outre, le chargement de fichier n’est pas le seul moyen de récupérer vos données dans [!DNL Commerce Intelligence]. Les fonctions [API d&#39;import de données](https://developer.adobe.com/commerce/services/reporting/import-api/) vous permettent de pousser des données arbitraires vers votre Data Warehouse [!DNL Commerce Intelligence].

## Associé {#related}

* [Formatage et import de données financières](../../../best-practices/format-import-financial-data.md)
* [Importation de données de dépenses publicitaires hors ligne/autres](../connecting-data/import-offline-ad-data.md)
* [Données [!DNL Google ECommerce] attendues](../integrations/google-ecommerce-data.md)

## Ressources tierces

* [Guide de formatage des données numériques](http://www.dummies.com/how-to/content/how-to-choose-a-number-format-in-your-numbers-spre.html)
* [[!DNL Google Docs] Guide de formatage des données](https://support.google.com/docs/answer/56470?hl=en)
