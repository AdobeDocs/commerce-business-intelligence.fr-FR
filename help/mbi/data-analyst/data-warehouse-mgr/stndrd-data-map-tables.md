---
title: Normalisation des données avec les tableaux de mappage
description: Découvrez comment utiliser les tables de mappage.
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# Normalisation des données avec les tableaux de mappage

Image : vous êtes dans la variable `Report Builder`, création d’une `Revenue by State` rapport. Vous êtes dans la zone. Tout va nager jusqu&#39;à ce que vous alliez ajouter une `billing state` regroupement à votre rapport et vous voyez ceci :

![](../../assets/Messy_State_Segments.png)

## Comment cela pourrait-il se produire ?

Malheureusement, un manque de normalisation peut parfois entraîner des problèmes de données et de têtes lors de la création de rapports. Dans notre exemple, il se peut qu’il n’y ait pas eu de menu déroulant ni de méthode normalisée permettant à nos clients de saisir les informations d’état de facturation. Cela entraîne une grande variété de valeurs. `pa`, `PA`, `penna`, `pennsylvania`, et `Pennsylvania` - tous pour le même état, ce qui va certainement conduire à des résultats étranges dans la `Report Builder`.

Il est possible qu’il existe une ressource technologique qui peut vous aider à nettoyer les données ou à insérer les colonnes dont vous avez besoin directement dans votre base de données, mais dans le cas contraire, nous disposons d’une autre solution : **la table de mappage**. Un tableau de mappage vous permet de nettoyer et de normaliser rapidement et facilement les données désordonnées en mappant les données à une seule sortie.

>[!NOTE]
>
>Vous ne pouvez pas créer de tableau de mappage pour les tables consolidées sans l’aide de notre équipe d’assistance. Contactez-nous pour plus d&#39;informations.

## Comment puis-je le créer ? {#how}

**Actualisation de la mise en forme des données :**

* Assurez-vous que votre feuille de calcul comporte une rangée d’en-tête.
* Évitez d’utiliser des virgules ! Cela entraîne des problèmes lors du téléchargement du fichier.
* Utiliser le format de date standard `(YYYY-MM-DD HH:MM:SS)` pour les dates.
* Les pourcentages doivent être renseignés en tant que décimales.
* Assurez-vous que tous les zéros de début ou de fin sont correctement conservés.

Avant de plonger, nous vous recommandons de [export des données du tableau brut](../../tutorials/export-raw-data.md). En examinant d’abord les données brutes, vous pouvez explorer toutes les combinaisons possibles pour les données à nettoyer, ce qui garantit que le tableau de mappage couvre tout.

Pour créer un tableau de mappage, vous devez créer une feuille de calcul de deux colonnes qui suit le [règles de formatage pour les téléchargements de fichiers](../../data-analyst/importing-data/connecting-data/using-file-uploader.md).

Dans la première colonne, saisissez les valeurs stockées dans votre base avec **une seule valeur par ligne**. Par exemple : `pa` et `PA` ne peut pas se trouver sur la même ligne ; chaque entrée doit avoir sa propre ligne. Voir ci-dessous pour obtenir un exemple.

Dans la seconde colonne, saisissez les valeurs correspondantes. **should**. Poursuite de notre exemple d’état de facturation, si nous le voulons `pa`, `PA`, `Pennsylvania`, et `pennsylvania` être simplement `PA`, nous allons entrer `PA` dans cette colonne pour chaque valeur d’entrée.

![](../../assets/Mapping_table_examples.jpg)

## Que dois-je faire dans [!DNL MBI] pour l’utiliser ? {#use}

Une fois la création de la table de mappage terminée, vous devrez [télécharger le fichier](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) into [!DNL MBI] et [création d’une colonne jointe](../../data-analyst/data-warehouse-mgr/calc-column-types.md) qui relocalise le nouveau champ dans la table souhaitée. Vous pouvez effectuer cette opération une fois le fichier synchronisé dans votre entrepôt de données.

Dans notre exemple, nous allons déplacer la colonne que nous avons créée sur l’ `mapping_state` tableau (`state_input`) au `customer_address` à l’aide d’une colonne jointe. Cela nous permettra de regrouper en fonction du nettoyage `state_input` au lieu de la colonne `state` colonne .

Pour créer la variable `joined` , accédez au tableau vers lequel le champ sera déplacé dans le Gestionnaire de Data Warehouse. Dans notre exemple, il s’agit de la variable `customer_address` table.

1. Cliquez sur **[!UICONTROL Create a Column]**.
1. Sélectionner `Joined Column` de la `Definition` menu déroulant.
1. Attribuez à la colonne un nom qui la différencie du `state` dans votre base de données. Nous irons avec `billing state (mapped)` nous pouvons donc déterminer la colonne à utiliser lors de la segmentation dans le créateur de rapports.
1. Le chemin dont nous avons besoin pour connecter les tables n’existe pas, nous devons donc en créer une nouvelle. Cliquez sur **[!UICONTROL Create new path]**  dans le `Select a table and column` menu déroulant.

   Si vous ne savez pas quelle est la relation de la table ou comment définir correctement les clés Principale et étrangère, extrayez-vous. [notre tutoriel](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) pour de l&#39;aide.

   * Sur le `Many` côté, sélectionnez la table vers laquelle vous déplacez le champ (encore une fois, pour nous, il s&#39;agit de `customer_address`) et la variable `Foreign Key` ou `state` , dans notre exemple.
   * Sur le `One` côté , sélectionnez la variable `mapping` et le `Primary key` colonne . Dans ce cas, nous allons sélectionner la variable `state_input` de la colonne `mapping_state` table.
   * Voici à quoi ressemble notre chemin :

      ![](../../assets/State_Mapping_Path.png)

1. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save]** pour créer le chemin.
1. Le chemin ne peut pas être renseigné immédiatement après l’enregistrement. Si cela se produit, cliquez sur la variable `Path` et sélectionnez le chemin que vous venez de créer.
1. Cliquez sur **[!UICONTROL Save]** pour créer la colonne.

C&#39;est tout !

## Que dois-je faire maintenant ? {#wrapup}

Une fois le cycle de mise à jour terminé, vous pourrez utiliser la nouvelle colonne jointe pour segmenter correctement vos données au lieu de la colonne désordonnée de votre base de données. Jetez un coup d’oeil à nos options de regroupement maintenant - plus de stress pénible :

![](../../assets/Clean_State_Segments.png)

Les tableaux de mappage sont pratiques pour le nettoyage de certaines données potentiellement dangereuses dans votre entrepôt de données. Cependant, les tableaux de mappage peuvent également être utilisés pour d’autres cas pratiques, comme [réplication de vos canaux Google Analytics dans MBI](../data-warehouse-mgr/rep-google-analytics-channels.md).

### Associé

* [Comprendre et évaluer les relations entre les tables](../data-warehouse-mgr/table-relationships.md)
* [Création/suppression de chemins pour les colonnes calculées](../data-warehouse-mgr/create-paths-calc-columns.md)
