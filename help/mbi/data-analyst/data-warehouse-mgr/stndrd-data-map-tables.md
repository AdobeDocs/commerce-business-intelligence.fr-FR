---
title: Normalisation des données avec les tableaux de mappage
description: Découvrez comment utiliser les tables de mappage.
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# Normalisation des données avec les tableaux de mappage

Imaginez que vous êtes en train de créer un rapport `Report Builder` `Revenue by State`. Tout va bien jusqu&#39;à ce que vous essayiez d&#39;ajouter un groupement `billing state` à votre rapport et que vous voyiez ceci :

![](../../assets/Messy_State_Segments.png)

## Comment cela pourrait-il se produire ?

Malheureusement, l’absence de normalisation peut parfois entraîner des problèmes de données et de têtes lors de la création de rapports. Dans cet exemple, il se peut qu’il n’y ait pas eu de menu déroulant ni de méthode normalisée permettant à vos clients de saisir les informations d’état de facturation. Cela conduit à diverses valeurs - `pa`, `PA`, `penna`, `pennsylvania` et `Pennsylvania` - toutes pour le même état, ce qui entraîne des résultats étranges dans le `Report Builder`.

Il est possible qu’une ressource technique vous aide à nettoyer les données ou à insérer les colonnes dont vous avez besoin directement dans votre base de données. Si ce n&#39;est pas le cas, il existe une autre solution : **la table de mappage**. Un tableau de mappage vous permet de nettoyer et de normaliser rapidement et facilement les données désordonnées en mappant les données à une seule sortie.

>[!NOTE]
>
>Vous ne pouvez pas créer de tableau de mappage pour les tables consolidées sans l’aide de l’équipe d’assistance Adobe.

## Comment puis-je le créer ? {#how}

**Actualisation de la mise en forme des données :**

* Assurez-vous que votre feuille de calcul comporte une rangée d’en-tête.
* Évitez d’utiliser des virgules ! Cela entraîne des problèmes lorsque vous téléchargez le fichier.
* Utilisez le format de date standard `(YYYY-MM-DD HH:MM:SS)` pour les dates.
* Les pourcentages doivent être renseignés en tant que décimales.
* Assurez-vous que tous les zéros de début ou de fin sont correctement conservés.

Avant de vous plonger, Adobe vous recommande [d&#39;exporter les données de la table brute](../../tutorials/export-raw-data.md). En examinant d’abord les données brutes, vous pouvez explorer toutes les combinaisons possibles pour les données à nettoyer, ce qui garantit que le tableau de mappage couvre tout.

Pour créer un tableau de mappage, vous devez créer une feuille de calcul de deux colonnes qui suit les [règles de formatage pour les chargements de fichiers](../../data-analyst/importing-data/connecting-data/using-file-uploader.md).

Dans la première colonne, saisissez les valeurs stockées dans votre base de données avec **une seule valeur par ligne**. Par exemple, `pa` et `PA` ne peuvent pas se trouver sur la même ligne ; chaque entrée doit avoir sa propre ligne. Voir ci-dessous pour obtenir un exemple.

Dans la seconde colonne, entrez les valeurs **qui doivent être**. Si vous continuez avec l’exemple d’état de facturation, si vous souhaitez que `pa`, `PA`, `Pennsylvania` et `pennsylvania` soient simplement `PA`, vous devez saisir `PA` dans cette colonne pour chaque valeur d’entrée.

![](../../assets/Mapping_table_examples.jpg)

## Que dois-je faire dans [!DNL Commerce Intelligence] pour l’utiliser ? {#use}

Une fois la création de la table de mappage terminée, vous devez [charger le fichier](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) dans [!DNL Commerce Intelligence] et [créer une colonne jointe](../../data-analyst/data-warehouse-mgr/calc-column-types.md) qui relocalise le nouveau champ dans la table souhaitée. Vous pouvez effectuer cette opération une fois que le fichier a été synchronisé avec votre Data Warehouse.

Cet exemple déplace la colonne que vous avez créée sur la table `mapping_state` (`state_input`) vers la table `customer_address` à l’aide d’une colonne associée. Cela nous permet de regrouper par colonne `state_input` propre dans vos rapports au lieu de la colonne `state`.

Pour créer la colonne `joined`, accédez à la table à laquelle le champ sera déplacé dans le Gestionnaire de Data Warehouse. Dans cet exemple, il s’agit de la table `customer_address`.

1. Cliquez sur **[!UICONTROL Create a Column]**.
1. Sélectionnez `Joined Column` dans la liste déroulante `Definition`.
1. Donnez à la colonne un nom qui la différencie de la colonne `state` de votre base de données. Nommez la colonne `billing state (mapped)` afin que vous puissiez déterminer la colonne à utiliser lors de la segmentation dans le créateur de rapports.
1. Le chemin dont vous avez besoin pour connecter les tables n’existe pas. Vous devez donc en créer une. Cliquez sur **[!UICONTROL Create new path]** dans la liste déroulante `Select a table and column`.

   Si vous ne savez pas quelle est la relation de la table ou comment définir correctement les clés principale et étrangère, consultez [le tutoriel](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) pour obtenir de l&#39;aide.

   * Du côté `Many`, sélectionnez la table vers laquelle vous déplacez le champ (là encore, pour nous il s&#39;agit de `customer_address`) et la colonne `Foreign Key`, ou `state`, dans l&#39;exemple.
   * Sur le côté `One`, sélectionnez la table `mapping` et la colonne `Primary key`. Dans ce cas, vous sélectionnerez la colonne `state_input` de la table `mapping_state`.
   * Voici à quoi ressemble le chemin :

     ![](../../assets/State_Mapping_Path.png)

1. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save]** pour créer le chemin.
1. Le chemin ne peut pas être renseigné immédiatement après l’enregistrement. Si cela se produit, cliquez sur la zone `Path` et sélectionnez le chemin que vous avez créé.
1. Cliquez sur **[!UICONTROL Save]** pour créer la colonne.

## Que dois-je faire maintenant ? {#wrapup}

Une fois le cycle de mise à jour terminé, vous pourrez utiliser la nouvelle colonne jointe pour segmenter correctement vos données au lieu de la colonne désordonnée de votre base de données. Examinez maintenant vos options de regroupement - ce n’est plus un problème de stress :

![](../../assets/Clean_State_Segments.png)

Les tableaux de mappage sont pratiques pour tout moment où vous souhaitez nettoyer certaines données potentiellement dangereuses dans votre Data Warehouse. Cependant, les tables de mappage peuvent également être utilisées pour d’autres cas d’utilisation cool, comme [la réplication de votre  [!DNL Google Analytics channels] dans [!DNL Commerce Intelligence]](../data-warehouse-mgr/rep-google-analytics-channels.md).

### Associé

* [Comprendre et évaluer les relations entre les tables](../data-warehouse-mgr/table-relationships.md)
* [Création/suppression de chemins pour les colonnes calculées](../data-warehouse-mgr/create-paths-calc-columns.md)
