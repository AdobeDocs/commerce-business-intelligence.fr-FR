---
title: Colonne calculée Nombre d’événements
description: Découvrez l’objectif et les utilisations de la colonne calculée Numéro d’événement .
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 3%

---

# Colonne calculée Nombre d’événements

Cette rubrique décrit l’objectif et les utilisations de la fonction `Event Number` colonne calculée disponible dans la **[!DNL Manage Data > Data Warehouse]** page. Vous trouverez ci-dessous une explication de ce qu&#39;il fait, suivie d&#39;un exemple, et des mécanismes de sa création.

**Explication**

Le `Event Number` type de colonne : identifie la séquence dans laquelle des événements se sont produits pour un **propriétaire d’événement**, comme un `customer` ou `user`. Si vous maîtrisez SQL, ce type de colonne est identique au `RANK` fonction . Il peut être utilisé pour observer des différences de comportement entre les premiers événements, les événements de répétition ou les énièmes événements dans vos données.

En cas d&#39;égalité, cette colonne contient la même **rank** pour les événements liés et ignore les nombres suivants. Par exemple, s’il classait les nombres 5,8,10,10,12, les grades seraient de 1,2,3,3,5.

Le cas d’utilisation le plus courant de cette colonne consiste à analyser les acheteurs qui se lancent pour la première fois et les acheteurs réguliers. Les premiers acheteurs sont identifiés en ajoutant un filtre (à une mesure ou à un rapport) sur `Customer's order number` = 1. `Customer's order number` est une colonne de type `Event Number`.

**Exemple**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

Dans l’exemple ci-dessus, la colonne `Owner's event number` est un `Event Number` colonne . Il classe les événements du propriétaire dans l’ordre dans lequel ils se sont produits (en fonction de la variable `timestamp` ).

Par exemple, prenez en compte toutes les lignes où `owner_id = A`. La première ligne du tableau correspond à l’horodatage le plus ancien pour ce propriétaire, suivie de la troisième ligne du tableau, suivie de la quatrième ligne du tableau.

**Mécanique**

Voici quelques instructions sur la création d’un `Event Number` column :

1. Accédez au **[!UICONTROL Manage Data > Data Warehouse]** page.
1. Accédez au tableau sur lequel vous souhaitez créer cette colonne.
1. Cliquez sur **[!UICONTROL Create a Column]** et sélectionnez la variable `EVENT_NUMBER (…)` type de colonne : sous le `Same Table` .
1. Première liste déroulante `Event Owner` spécifie l’entité pour laquelle le rang doit être déterminé. Dans le cas où une `Customer's order number`, un identifiant de client tel que `customer_id` ou `customer_email` serait `Event Owner`.
1. Deuxième liste déroulante `Event Rank` spécifie la colonne qui applique la séquence qui détermine le rang de la ligne. Dans le cas où une `Customer's order number`, la variable `created_at` l’horodatage correspondrait à `Event Rank`.
1. Sous , `Options` , vous pouvez ajouter des filtres pour exclure les lignes de la prise en compte. Les lignes exclues ont une `NULL` pour cette colonne.
1. Attribuez un nom à la colonne et cliquez sur **[!UICONTROL Save]**.
1. La colonne peut être utilisée _immédiatement._
