---
title: Création et utilisation d’une colonne calculée SQL
description: Découvrez comment créer des colonnes avancées sous la forme de colonnes de calcul SQL sur la nouvelle architecture MBI.
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# Création d’une colonne calculée SQL

Cette rubrique décrit l’objectif et les utilisations de la fonction `Calculation` type de colonne : qui peuvent être ajoutés aux tableaux à l’aide de la variable [Gestionnaire de Data Warehouse](../data-warehouse-mgr/tour-dwm.md). Vous trouverez ci-dessous une explication des calculs SQL, des raisons de leur utilisation, du processus de création d’un calcul SQL, ainsi que deux exemples.

**Explication**

Dans le passé, colonnes considérées `advanced` ne peut être effectué que par un analyste de l’équipe du succès client à l’adresse [!DNL MBI]. Désormais, toute la puissance est entre les mains de l’utilisateur final, et des colonnes avancées peuvent être créées sous la forme de `SQL Calculation` sur la nouvelle [!DNL MBI] l’architecture.

Le `Calculation` Le type de colonne, désormais disponible en tant qu’option dans Data Warehouse Manager, est une même opération de table qui permet de transformer les colonnes d’un tableau à l’aide de la logique PostgreSQL. Documentation sur les fonctions et opérateurs pouvant être utilisés dans le `Calculatio`Un type de colonne est disponible sur le site Web de PostgreSQL. [here](https://www.postgresql.org/docs/9.6/static/functions.html).

Les différentes colonnes qui peuvent être créées avec l’objet `Calculation` sont pratiquement illimitées, mais la plupart des colonnes peuvent être créées à l’aide d’instructions IF-THEN et d’une arithmétique de base, qui seront utilisées dans les exemples ci-dessous.

**Exemple 1 : La dernière commande du client ?**

La plupart des comptes comportent une colonne appelée `Is customer's last order?` sur leur `orders` pour effectuer des analyses sur les taux d’achat répétés et les clients connectés. Si votre compte repose sur la nouvelle architecture, cette colonne est créée à l’aide d’une `Calculation` et sont visibles dans la capture d’écran ci-dessous :

![](../../assets/Is_customer_s_last_order.png)

Le `Is customer's last order?` La colonne utilise les entrées `Customer's lifetime number of orders` et `Customer's order number` alias `A` et `B` respectivement.

Ligne par ligne, la signification du PostgreSQL est :

* Cas : Cela commence une série d’instructions If - Then
* when `A` est nul ou `B` est nul puis nul : Si l’une des entrées est vide, la sortie doit également être vide. Cela permet d’éviter les erreurs SQL.
* when `A=B` then `Yes`: If `Customer's lifetime number of orders` est égal à `Customer's order number` pour cette ligne, puis renvoyer `Yes`. Ainsi, si un client a passé 4 commandes, la ligne correspondant à sa quatrième commande est renvoyée. `Yes` pour `Is customer's last order?`
* else `No`: Si aucune des autres conditions lorsque des instructions sont satisfaites, renvoie `No`
* end : Cela met fin aux instructions If - Then

Les valeurs possibles qui peuvent être renvoyées par cette colonne (`NULL`, `Yes`, `No`) ne contient pas de caractères numériques. Par conséquent, le type de données ici est String.

**Exemple 2 : Valeur totale de l’élément de commande (quantité * prix)**

La plupart de nos clients aiment analyser les recettes au niveau de l’élément, en les divisant par des champs comme `product name` ou `category`. La plupart des bases de données ne donnent pas réellement les recettes d’un produit dans une commande ; au lieu de cela, ils indiquent la quantité vendue dans la commande et le prix de l’article.

Pour activer l’analyse des recettes de produits, la plupart des comptes comportent une colonne intitulée `Order item total value (quantity * price)` sur leur `Orders Items` table. Si votre compte repose sur la nouvelle architecture, cette colonne est également créée à l’aide d’une `Calculation` et sont visibles dans la capture d’écran ci-dessous :

![](../../assets/Order_item_total_value.png)

Dans le schéma Commerce, la variable `Order item total value (quantity * price)` La colonne utilise les entrées `qty ordered` et `base price` alias `A` et `B` respectivement.

Les valeurs qui seront renvoyées par cette nouvelle colonne seront de l’ordre de 30 centimes, de sorte que le type de données correct est `Decimal(10,2)`.

**Mécanique**

Une nouvelle `Calculation` peut être ajoutée à un tableau en accédant à **[!DNL Manage Data > Data Warehouse]** comme illustré ci-dessous :

![](../../assets/blobid2.png)

Vous pouvez créer un `Calculation` en suivant les étapes ci-dessous :

1. Sélectionnez le tableau sur lequel vous souhaitez ajouter le `Calculation` colonne .
1. Dans le tableau approprié, cliquez sur **[!UICONTROL Create New Column]** en haut à droite de l’écran.
1. Dans la `Select a definition` menu déroulant, sélectionnez `Same Table`.
1. Sélectionner `Calculation` comme la propriété `column definition equation`.
1. Saisissez le nom de la colonne.
1. Choisissez la `input` des colonnes du tableau qui seront utilisées dans la logique de votre nouvelle colonne. Chaque colonne que vous ajoutez reçoit un alias de lettre, donc la première colonne est `A`, le second sera `B` etc.
1. Dans la fenêtre, saisissez la logique PostgreSQL pour votre nouvelle colonne à l’aide des alias de lettre de vos entrées. Le calcul SQL doit être limité à une seule définition de colonne, incluant toute la logique entre les instructions SELECT et FROM d’une requête SQL. Notez que les mots-clés SQL utilisant l’une des lettres d’entrée doivent être en minuscules. Par exemple, lors de l’utilisation de la variable `CASE` , il doit être écrit en minuscules - `case`. Le système suppose qu’il s’agit d’une majuscule `A` fait référence à l’une des entrées.
1. Choisissez le type de données approprié.
   * `Integer` - Nombre entier
   * `Decimal(10,2)` : nombre décimal contenant 10 chiffres totaux, dont 2 situés à droite du point décimal
   * `String` - Tout type de texte ou série de caractères qui utilise des caractères non numériques
   * `Datetime` - aaaa-MM-jj hh:mm:format ss

1. Cliquez sur **[!UICONTROL test column]**. Cela génère une liste de 5 valeurs de test pour chacune de vos entrées et affiche le résultat de la logique de l’étape 6 pour chaque ensemble de valeurs de test. Si une partie du code SQL génère une erreur, le message d’erreur approprié est renvoyé. Notez que les exemples de résultats ne peuvent être générés que si toutes les colonnes d’entrée sont des champs natifs. Si l’une des colonnes d’entrée est des colonnes calculées, vous devez valider les résultats en ajoutant la colonne à une mesure et en la visualisant dans le Report Builder Visuel.
1. Lorsque les résultats vous conviennent, cliquez sur **[!UICONTROL Save]**, et votre colonne sera disponible.
