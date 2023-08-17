---
title: Création et utilisation d’une colonne calculée SQL
description: Découvrez comment créer des colonnes avancées sous la forme de colonnes de calcul SQL sur la nouvelle architecture Adobe Commerce Intelligence.
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, SQL Report Builder, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 0%

---

# Création d’une colonne calculée SQL

Cette rubrique décrit l’objectif et les utilisations de la fonction `Calculation` type de colonne, qui peut être ajouté aux tableaux à l’aide de la variable [Gestionnaire de Data Warehouse](../data-warehouse-mgr/tour-dwm.md). Vous trouverez ci-dessous des explications sur les calculs SQL, les raisons de leur utilisation, le processus de création d’un calcul SQL, ainsi que deux exemples.

**Explication**

Dans le passé, colonnes considérées `advanced` ne peut être effectué que par un analyste de l’équipe du succès client à l’adresse [!DNL Adobe Commerce Intelligence]. Désormais, toute la puissance est entre les mains de l’utilisateur final, et des colonnes avancées peuvent être créées sous la forme de `SQL Calculation` sur la nouvelle [!DNL Commerce Intelligence] l’architecture.

La variable `Calculation` Le type de colonne, désormais disponible en tant qu’option dans Data Warehouse Manager, est une même opération de table qui permet de transformer les colonnes d’un tableau à l’aide de la logique PostgreSQL. Documentation sur les fonctions et opérateurs pouvant être utilisés dans le `Calculation` Le type de colonne est disponible sur le site web PostgreSQL [here](https://www.postgresql.org/docs/9.6/functions.html).

Les différentes colonnes qui peuvent être créées avec l’objet `Calculation` sont pratiquement illimitées, mais la plupart des colonnes peuvent être créées à l’aide d’instructions IF-THEN et d’une arithmétique de base, qui est utilisée dans les exemples ci-dessous.

**Exemple 1 : la dernière commande du client est-elle ?**

La plupart des comptes comportent une colonne appelée `Is customer's last order?` sur leur `orders` pour effectuer des analyses sur les taux d’achat répétés et les clients connectés. Si votre compte repose sur la nouvelle architecture, cette colonne est créée à l’aide d’une `Calculation` et sont visibles dans la capture d’écran ci-dessous :

![](../../assets/Is_customer_s_last_order.png)

La variable `Is customer's last order?` La colonne utilise les entrées `Customer's lifetime number of orders` et `Customer's order number` alias `A` et `B` respectivement.

Ligne par ligne, la signification du PostgreSQL est :

* case : cela commence une série d’instructions If - Then
* when `A` est nul ou `B` est nul puis nul : si l’entrée est vide, la sortie doit également être vide. Cela permet d’éviter les erreurs SQL.
* when `A=B` then `Yes`: Si `Customer's lifetime number of orders` est égal à `Customer's order number` pour cette ligne, puis renvoyer `Yes`. Ainsi, si un client a passé quatre commandes, la ligne correspondant à sa quatrième commande est renvoyée `Yes` pour `Is customer's last order?`
* else `No`: si aucune des autres conditions n’est remplie, renvoie `No`
* end : cela met fin aux instructions if - Then

Les valeurs possibles qui peuvent être renvoyées par cette colonne (`NULL`, `Yes`, `No`) contiennent des caractères non numériques, donc le type de données ici est Chaîne.

**Exemple 2 : valeur totale de l’élément de commande (quantité * prix)**

De nombreux clients aiment analyser les recettes au niveau de l’élément, en les divisant par des champs comme `product name` ou `category`. La plupart des bases de données ne donnent pas réellement les recettes d’un produit dans une commande ; elles indiquent plutôt la quantité vendue dans la commande et le prix de l’article.

Pour activer l’analyse des recettes de produits, la plupart des comptes comportent une colonne intitulée `Order item total value (quantity * price)` sur leur `Orders Items` table. Si votre compte repose sur la nouvelle architecture, cette colonne est également créée à l’aide d’une `Calculation` et sont visibles dans la capture d’écran ci-dessous :

![](../../assets/Order_item_total_value.png)

Dans le schéma Commerce, la variable `Order item total value (quantity * price)` La colonne utilise les entrées `qty ordered` et `base price` alias `A` et `B` respectivement.

Les valeurs renvoyées par cette nouvelle colonne sont en euros et en centimes, le type de données correct est donc : `Decimal(10,2)`.

**Mécanique**

Une nouvelle `Calculation` peut être ajoutée à un tableau en accédant à **[!DNL Manage Data > Data Warehouse]** comme illustré ci-dessous :

![](../../assets/blobid2.png)

Vous pouvez créer un `Calculation` en suivant les étapes ci-dessous :

1. Sélectionnez le tableau sur lequel vous souhaitez ajouter le `Calculation` colonne .
1. Dans le tableau approprié, cliquez sur **[!UICONTROL Create New Column]** en haut à droite de l’écran.
1. Dans la `Select a definition` menu déroulant, sélectionnez `Same Table`.
1. Sélectionner `Calculation` comme la propriété `column definition equation`.
1. Saisissez le nom de la colonne.
1. Choisissez la `input` colonnes du tableau utilisées dans la logique pour votre nouvelle colonne. Chaque colonne que vous ajoutez reçoit un alias de lettre, donc la première colonne est `A`, la seconde est `B` etc.
1. Dans la fenêtre, saisissez la logique PostgreSQL pour votre nouvelle colonne à l’aide des alias de lettre de vos entrées. Le calcul SQL doit être limité à une seule définition de colonne, incluant toute la logique entre les instructions SELECT et FROM d’une requête SQL. Les mots-clés SQL utilisant l’une des lettres d’entrée doivent être en minuscules. Par exemple, lors de l’utilisation de la variable `CASE` , il doit être écrit en minuscules - `case`. Le système suppose qu’il s’agit d’une majuscule `A` fait référence à l’une des entrées.
1. Choisissez le type de données approprié.
   * `Integer` - Nombre entier
   * `Decimal(10,2)` : nombre décimal contenant 10 chiffres au total, dont 2 situés à droite du point décimal
   * `String` - Tout type de texte ou série de caractères qui n’utilisent pas de nombres
   * `Datetime` - aaaa-MM-jj hh:mm:format ss

1. Cliquez sur **[!UICONTROL test column]**. Cela génère une liste de cinq valeurs de test pour chacune de vos entrées et affiche le résultat de la logique de l’étape 6 pour chaque ensemble de valeurs de test. Si une partie du code SQL génère une erreur, le message d’erreur approprié est renvoyé. Les exemples de résultats ne peuvent être générés que si toutes les colonnes d’entrée sont des champs natifs. Si l’une des colonnes d’entrée est des colonnes calculées, vous devez valider les résultats en ajoutant la colonne à une mesure et en la visualisant dans le Report Builder Visuel.

1. Lorsque vous êtes satisfait des résultats, cliquez sur **[!UICONTROL Save]**. La colonne est utilisable.
