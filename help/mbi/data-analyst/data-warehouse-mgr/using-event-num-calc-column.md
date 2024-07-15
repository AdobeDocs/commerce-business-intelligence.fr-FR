---
title: Colonne calculée Nombre d’événements
description: Découvrez l’objectif et les utilisations de la colonne calculée Numéro d’événement .
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# Colonne calculée Nombre d’événements

Cette rubrique décrit l’objectif et les utilisations de la colonne calculée `Event Number` disponible dans la page **[!DNL Manage Data > Data Warehouse]**. Vous trouverez ci-dessous une explication de ce qu&#39;il fait, suivie d&#39;un exemple, et des mécanismes de sa création.

**Explication**

Le type de colonne `Event Number` identifie la séquence dans laquelle les événements se sont produits pour un **propriétaire d’événement** particulier, comme un `customer` ou un `user`. Si vous connaissez SQL, ce type de colonne est identique à la fonction `RANK`. Il peut être utilisé pour observer des différences de comportement entre les premiers événements, les événements de répétition ou les énièmes événements dans vos données.

En cas d’égalité, cette colonne contient le même **rang** pour les événements liés et ignore les nombres suivants. Par exemple, s’il classait les nombres 5,8,10,10,12, les grades seraient de 1,2,3,3,5.

Le cas d’utilisation le plus courant de cette colonne consiste à analyser les acheteurs qui se lancent pour la première fois et les acheteurs réguliers. Les premiers acheteurs sont identifiés en ajoutant un filtre (à une mesure ou un rapport) sur `Customer's order number` = 1. `Customer's order number` est une colonne de type `Event Number`.

**Exemple**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

Dans l’exemple ci-dessus, la colonne `Owner's event number` est une colonne `Event Number`. Il classe les événements du propriétaire dans l’ordre dans lequel ils se sont produits (en fonction de la colonne `timestamp`).

Par exemple, prenez en compte toutes les lignes où `owner_id = A`. La première ligne du tableau correspond à l’horodatage le plus ancien pour ce propriétaire, suivie de la troisième ligne du tableau, suivie de la quatrième ligne du tableau.

**Mécanique**

Voici quelques instructions pour créer une colonne `Event Number` :

1. Accédez à la page **[!UICONTROL Manage Data > Data Warehouse]**.

1. Accédez au tableau sur lequel vous souhaitez créer cette colonne.

1. Cliquez sur **[!UICONTROL Create a Column]** et sélectionnez le type de colonne `EVENT_NUMBER (…)` sous la section `Same Table` .

1. La première liste déroulante `Event Owner` spécifie l’entité pour laquelle le rang doit être déterminé. Dans le cas où un `Customer's order number`, un identifiant de client tel que `customer_id` ou `customer_email` serait le `Event Owner`.

1. La seconde liste déroulante `Event Rank` spécifie la colonne qui applique la séquence qui détermine le rang de la ligne. Dans le cas où un `Customer's order number`, l’horodatage `created_at` serait le `Event Rank`.

1. Dans la liste déroulante `Options`, vous pouvez ajouter des filtres pour exclure les lignes de la prise en compte. Les lignes exclues ont une valeur `NULL` pour cette colonne.

1. Attribuez un nom à la colonne et cliquez sur **[!UICONTROL Save]**.

1. La colonne peut utiliser _immédiatement._
