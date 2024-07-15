---
title: Création et utilisation d’une colonne calculée SQL
description: Découvrez comment créer des colonnes avancées sous la forme de colonnes de calcul SQL sur la nouvelle architecture Adobe Commerce Intelligence.
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, SQL Report Builder, Commerce Tables
source-git-commit: 8090c2e0f17f0e8d3bdec668ce546206bf024691
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# Création d’une colonne calculée SQL

Cette rubrique décrit l’objectif et les utilisations du type de colonne `Calculation`, qui peut être ajouté aux tableaux à l’aide du [Gestionnaire de Data Warehouse](../data-warehouse-mgr/tour-dwm.md). Vous trouverez ci-dessous des explications sur les calculs SQL, les raisons de leur utilisation, le processus de création d’un calcul SQL, ainsi que deux exemples.

**Explication**

Dans le passé, les colonnes considérées `advanced` ne pouvaient être effectuées que par un analyste de l’équipe du succès client ici à l’adresse [!DNL Adobe Commerce Intelligence]. Désormais, toute la puissance est entre les mains de l’utilisateur final et des colonnes avancées peuvent être créées sous la forme de `SQL Calculation` colonnes sur la nouvelle architecture [!DNL Commerce Intelligence].

Le type de colonne `Calculation`, désormais disponible en tant qu’option dans Data Warehouse Manager, est une même opération de table qui permet de transformer les colonnes d’une table à l’aide de la logique PostgreSQL. Vous trouverez de la documentation sur les fonctions et opérateurs pouvant être utilisés dans le type de colonne `Calculation` sur le site Web PostgreSQL [ici](https://www.postgresql.org/docs/9.6/functions.html).

Les différentes colonnes qui peuvent être créées avec la colonne `Calculation` sont presque illimitées, mais la plupart des colonnes peuvent être créées à l’aide d’instructions IF-THEN et d’une arithmétique de base, qui est utilisée dans les exemples ci-dessous.

**Exemple 1 : La dernière commande du client ?**

La plupart des comptes ont une colonne appelée `Is customer's last order?` sur leur table `orders` pour effectuer des analyses sur les taux d’achat répétés et les clients connectés. Si votre compte repose sur la nouvelle architecture, cette colonne est créée à l’aide d’une colonne `Calculation` et vous pouvez la voir dans la capture d’écran ci-dessous :

![](../../assets/Is_customer_s_last_order.png)

La colonne `Is customer's last order?` utilise les entrées `Customer's lifetime number of orders` et `Customer's order number` en alias `A` et `B` respectivement.

Ligne par ligne, la signification du PostgreSQL est :

* case : cela commence une série d’instructions If - Then
* lorsque `A` est nul ou `B` est nul, puis nul : si l’entrée est vide, la sortie doit également être vide. Cela permet d’éviter les erreurs SQL.
* lorsque `A=B` puis `Yes` : si `Customer's lifetime number of orders` est égal à `Customer's order number` pour cette ligne, alors renvoie `Yes`. Ainsi, si un client a passé quatre commandes, la ligne correspondant à sa quatrième commande renverra `Yes` pour `Is customer's last order?`
* else `No` : si aucune des autres conditions n’est remplie, return `No`
* end : cela met fin aux instructions if - Then

Les valeurs possibles qui peuvent être renvoyées par cette colonne (`NULL`, `Yes`, `No`) contiennent des caractères non numériques. Par conséquent, le type de données ici est String.

**Exemple 2 : valeur totale de l’élément de commande (quantité * prix)**

De nombreux clients aiment analyser les recettes au niveau de l’élément en les divisant par des champs comme `product name` ou `category`. La plupart des bases de données ne donnent pas réellement les recettes d’un produit dans une commande ; elles indiquent plutôt la quantité vendue dans la commande et le prix de l’article.

Pour activer l’analyse des recettes de produits, la plupart des comptes ont une colonne appelée `Order item total value (quantity * price)` sur leur table `Orders Items`. Si votre compte repose sur la nouvelle architecture, cette colonne est également créée à l’aide d’une colonne `Calculation` et vous pouvez la voir dans la capture d’écran ci-dessous :

![](../../assets/Order_item_total_value.png)

Dans le schéma Commerce, la colonne `Order item total value (quantity * price)` utilise les entrées `qty ordered` et `base price` en alias respectivement `A` et `B`.

Les valeurs renvoyées par cette nouvelle colonne sont en euros et en centimes, le type de données correct est donc `Decimal(10,2)`.

**Mécanique**

Une nouvelle colonne `Calculation` peut être ajoutée à un tableau en accédant à **[!DNL Manage Data > Data Warehouse]** comme illustré ci-dessous :

![](../../assets/blobid2.png)

À partir de là, vous pouvez créer une colonne `Calculation` en suivant les étapes ci-dessous :

1. Sélectionnez la table sur laquelle vous souhaitez ajouter la colonne `Calculation`.
1. Sur la bonne table, cliquez sur **[!UICONTROL Create New Column]** en haut à droite de l’écran.
1. Dans la liste déroulante `Select a definition`, sélectionnez `Same Table`.
1. Sélectionnez `Calculation` comme `column definition equation`.
1. Saisissez le nom de la colonne.
1. Sélectionnez les colonnes `input` de la table utilisées dans la logique pour votre nouvelle colonne. Chaque colonne que vous ajoutez reçoit un alias de lettre, donc la première colonne est `A`, la seconde est `B`, etc.
1. Dans la fenêtre, saisissez la logique PostgreSQL pour votre nouvelle colonne à l’aide des alias de lettre de vos entrées. Le calcul SQL doit être limité à une seule définition de colonne, incluant toute la logique entre les instructions SELECT et FROM d’une requête SQL. Les mots-clés SQL utilisant l’une des lettres d’entrée doivent être en minuscules. Par exemple, lors de l’utilisation de l’instruction `CASE`, elle doit être écrite en minuscules - `case`. Le système suppose qu’un `A` majuscule fait référence à l’une des entrées.
1. Choisissez le type de données approprié.
   * `Integer` - Nombre entier
   * `Decimal(10,2)` : nombre décimal contenant 10 chiffres au total, dont 2 situés à droite du point décimal
   * `String` - Tout type de texte ou série de caractères qui n’utilisent pas de nombres
   * `Datetime` - `yyyy-MM-dd hh:mm:ss` format

1. Cliquez sur **[!UICONTROL test column]**. Cela génère une liste de cinq valeurs de test pour chacune de vos entrées et affiche le résultat de la logique de l’étape 6 pour chaque ensemble de valeurs de test. Si une partie du code SQL génère une erreur, le message d’erreur approprié est renvoyé. Les exemples de résultats ne peuvent être générés que si toutes les colonnes d’entrée sont des champs natifs. Si l’une des colonnes d’entrée est des colonnes calculées, vous devez valider les résultats en ajoutant la colonne à une mesure et en la visualisant dans le Report Builder Visuel.

1. Lorsque les résultats vous conviennent, cliquez sur **[!UICONTROL Save]**. La colonne est utilisable.
