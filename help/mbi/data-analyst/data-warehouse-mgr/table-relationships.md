---
title: Compréhension et évaluation des relations entre les tables
description: Découvrez comment comprendre combien d’occurrences possibles dans une table peuvent appartenir à une entité dans une autre.
exl-id: e7256f46-879a-41da-9919-b700f2691013
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 0%

---

# Compréhension et évaluation des relations entre les tables

Lors de l&#39;évaluation de la relation entre deux tables données, vous devez comprendre combien d&#39;occurrences possibles dans une table peuvent appartenir à une entité dans une autre, et vice versa. Par exemple, utilisez un tableau `users` et un tableau `orders`. Dans ce cas, vous souhaitez connaître le nombre de **commandes** qu’un **utilisateur** donné a passées et le nombre d’**utilisateurs** possibles auxquels une **commande** peut appartenir.

La compréhension des relations est essentielle au maintien de l’intégrité des données, car elle a une incidence sur la précision de vos [colonnes calculées](../data-warehouse-mgr/creating-calculated-columns.md) et [dimensions](../data-warehouse-mgr/manage-data-dimensions-metrics.md). Pour en savoir plus, voir [types de relation](#types) et [comment évaluer les tables dans votre Data Warehouse.](#eval)

## Types de relation {#types}

Il existe trois types de relations entre deux tables :

1. [`un-à-un`](#onetoone)
1. [« un à plusieurs »](#onetomany)
1. [« plusieurs à plusieurs »](#manytomany)

### `One-to-One` {#onetoone}

Dans une relation `one-to-one`, un enregistrement de la table `B` n&#39;appartient qu&#39;à un seul enregistrement de la table `A`. Et un enregistrement du tableau `A` n&#39;appartient qu&#39;à un seul enregistrement du tableau `B`.

Par exemple, dans la relation entre les personnes et les numéros de permis de conduire, une personne ne peut avoir qu&#39;un seul numéro de permis de conduire, et un numéro de permis de conduire appartient à une seule personne.

![](../../assets/one-to-one.png)

### `One-to-Many` {#onetomany}

Dans une relation `one-to-many`, un enregistrement dans la table `A` peut potentiellement appartenir à plusieurs enregistrements dans la table `B`. Pensez à la relation entre `orders` et `items` : une commande peut contenir de nombreux éléments, mais un élément appartient à une seule commande. Dans ce cas, la table `orders` est le côté un et la table `items` est le côté plusieurs.

![](../../assets/one-to-many_001.png)

### `Many-to-Many` {#manytomany}

Dans une relation `many-to-many`, un enregistrement dans la table `B` peut potentiellement appartenir à plusieurs enregistrements dans la table `A`. Et inversement, un enregistrement dans la table `A` peut potentiellement appartenir à plusieurs enregistrements dans la table `B`.

Pensez à la relation entre **produits** et **catégories** : un produit peut appartenir à de nombreuses catégories, et une catégorie peut contenir de nombreux produits.

![](../../assets/many-to-many.png)

## Évaluation de vos tableaux {#eval}

Étant donné les types de relations qui existent entre les tables, vous pouvez apprendre à évaluer les tables dans votre Data Warehouse. Comme ces relations déterminent la définition des colonnes calculées multi-tables, il est important de comprendre comment identifier les relations entre les tables et à quel côté, `one` ou `many`, la table appartient.

Vous pouvez utiliser deux méthodes pour évaluer les relations d’une paire de tables donnée dans votre Data Warehouse. La première méthode utilise un [cadre conceptuel](#concept) qui considère la manière dont les entités de la table interagissent les unes avec les autres. La deuxième méthode utilise le schéma de la [table](#schema).

### Utilisation du cadre conceptuel {#concept}

Cette méthode utilise un framework conceptuel pour décrire comment les entités dans les deux tableaux peuvent interagir entre elles. Il est important de comprendre que ce cadre évalue ce qui est possible, compte tenu de la relation.

Par exemple, lorsque vous pensez aux utilisateurs et aux commandes, prenez en compte tout ce qui est possible dans la relation. Un utilisateur enregistré ne peut passer aucune commande, une seule commande ou plusieurs commandes au cours de sa vie. Si vous avez lancé votre entreprise et qu&#39;aucune commande n&#39;a été passée, il est possible qu&#39;un utilisateur donné puisse passer de nombreuses commandes au cours de sa vie. Les tables sont construites pour cela.

Pour utiliser cette méthode :

1. Identifiez l’entité décrite dans chaque tableau. **Conseil : il s’agit généralement d’un substantif**. Par exemple, les tableaux `user` et `orders` décrivent explicitement les utilisateurs et les commandes.

1. Identifiez un ou plusieurs verbes qui décrivent l’interaction de ces entités. Par exemple, lorsque vous comparez des utilisateurs à des commandes, les utilisateurs passent des commandes. Dans l’autre sens, les commandes « appartiennent » aux utilisateurs.

Ce type de structure peut être appliqué à n’importe quel appariement de tables dans votre Data Warehouse. Vous pouvez ainsi identifier facilement le type de relation, ainsi que la table à un côté et la table à plusieurs côtés.

Une fois que vous avez identifié la terminologie qui décrit l’interaction entre les deux tables, définissez l’interaction dans les deux directions en tenant compte de la manière dont une instance donnée de la première entité est liée à la seconde. Voici quelques exemples de chaque relation :

### `One-to-One`

Une personne donnée ne peut avoir qu&#39;un seul numéro de permis de conduire. Un numéro de permis de conduire donné appartient à une seule personne.

Il s’agit d’une relation `one-to-one` où chaque table est un côté.

![](../../assets/one-to-one3.png)

### `One-to-Many`

Une commande donnée peut contenir de nombreux éléments. Un article donné appartient à une seule commande.

Il s&#39;agit d&#39;une relation `one-to-many` où la table des commandes est le côté un et la table des éléments est le côté plusieurs.

![](../../assets/one-to-many3.png)

### `Many-to-Many`

Un produit donné peut éventuellement appartenir à de nombreuses catégories. Une catégorie donnée peut éventuellement contenir de nombreux produits.

Il s’agit d’une relation `many-to-many` où chaque table a plusieurs côtés.

![](../../assets/many-to-many3.png)

### Utilisation du schéma de la table {#schema}

La deuxième méthode utilise le schéma de la table. Le schéma définit les colonnes qui sont les clés [`Primary`](https://en.wikipedia.org/wiki/Unique_key) et [`Foreign`](https://en.wikipedia.org/wiki/Foreign_key). Vous pouvez utiliser ces clés pour lier des tables et aider à déterminer les types de relation.

Une fois que vous avez identifié les colonnes qui relient deux tables, utilisez les types de colonnes pour évaluer la relation entre les tables. Voici quelques exemples :

### `One-to-one`

Si les tables sont liées à l&#39;`primary key` des deux tables, la même entité unique est décrite dans chaque table et la relation est `one-to-one`.

Par exemple, une table `users` peut capturer la plupart des attributs utilisateur (tels que le nom), tandis qu’une table `user_source` supplémentaire capture les sources d’enregistrement des utilisateurs. Dans chaque tableau, une ligne représente un utilisateur.

![](../../assets/one-to-one1.png)

### `One-to-many`

>[!NOTE]
>
>Acceptez-vous les commandes de clients ? Consultez [Commandes des invités](../data-warehouse-mgr/guest-orders.md) pour découvrir comment les commandes des invités peuvent avoir un impact sur vos relations entre les tables.

Lorsque des tables sont liées à l’aide d’un `Foreign key` pointant vers une `primary key`, cette configuration décrit une relation `one-to-many`. D’un côté, le tableau contenant les `primary key` ; de l’autre, le tableau contenant les `foreign key`.

![](../../assets/one-to-many1.png)

### `Many-to-many`

Si l’une des conditions suivantes est vraie, la relation est `many-to-many` :

* `Non-primary key` colonnes sont utilisées pour lier deux tableaux
  ![](../../assets/many-to-many1.png)
* Partie d&#39;un `primary key` composite permettant de lier deux tables

![](../../assets/many-to-mnay2.png)

## Étapes suivantes

Il est essentiel d’évaluer correctement les relations entre les tables pour modéliser précisément vos données. Maintenant que vous comprenez comment les tables sont liées les unes aux autres, reportez-vous à la section [Utilisation du gestionnaire Data Warehouse](../data-warehouse-mgr/tour-dwm.md).
