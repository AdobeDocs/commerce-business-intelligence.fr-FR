---
title: Colonne Calculée Du Numéro D’Événement
description: Découvrez l’objectif et les utilisations de la colonne calculée Numéro d’événement .
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# Colonne Calculée Du Numéro D’Événement

Cette rubrique décrit l’objectif et les utilisations de la colonne calculée `Event Number` disponible dans la page **[!DNL Manage Data > Data Warehouse]**. Vous trouverez ci-dessous une explication de son fonctionnement, suivie d’un exemple et des mécanismes de sa création.

**Explication**

Le type de colonne `Event Number` identifie la séquence dans laquelle les événements se sont produits pour un **propriétaire d’événement** spécifique, comme un `customer` ou un `user`. Si vous connaissez SQL, ce type de colonne est identique à la fonction `RANK`. Il peut être utilisé pour observer les différences de comportement entre les premiers événements, les événements répétés ou les énièmes événements dans vos données.

En cas d’égalité, cette colonne contient le même **rang** pour les événements liés et ignore les nombres suivants. Par exemple, s&#39;il classait les nombres 5,8,10,10,12, les rangs seraient 1,2,3,3,5.

Le cas d’utilisation le plus courant de cette colonne consiste à analyser les nouveaux acheteurs et les acheteurs réguliers. Les nouveaux acheteurs sont identifiés en ajoutant un filtre (à une mesure ou à un rapport) sur `Customer's order number` = 1. `Customer's order number` est une colonne de type `Event Number`.

**Exemple**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| 1 ** | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| 3 ** | A | 2015-01-01 02:00:00 | 2 |
| 4 ** | A | 2015-01-02 13:00:00 | 3 |
| 5 ** | B | 2015-01-03 13:00:00 | 2 |

Dans l’exemple ci-dessus, la colonne `Owner's event number` est une colonne `Event Number`. Il classe les événements du propriétaire dans l&#39;ordre dans lequel ils se sont produits (en fonction de la colonne `timestamp`).

Prenons l’exemple de toutes les lignes contenant des `owner_id = A`. La première ligne du tableau est la première date et heure de ce propriétaire, suivie de la troisième ligne du tableau, suivie de la quatrième.

**mécanique**

Voici quelques instructions pour créer une colonne `Event Number` :

1. Accédez à la page **[!UICONTROL Manage Data > Data Warehouse]**.

1. Accédez à la table sur laquelle vous souhaitez créer cette colonne.

1. Cliquez sur **[!UICONTROL Create a Column]** et choisissez le type de colonne `EVENT_NUMBER (…)` : sous la section `Same Table` .

1. Le premier `Event Owner` déroulant spécifie l&#39;entité pour laquelle le classement doit être déterminé. Dans le cas d’un `Customer's order number`, un identifiant de client tel que `customer_id` ou `customer_email` serait le `Event Owner`.

1. Le deuxième `Event Rank` déroulant spécifie la colonne qui applique la séquence qui détermine le classement de la ligne. Dans le cas d’une `Customer's order number`, la date et l’heure `created_at` sont les `Event Rank`.

1. Dans la liste déroulante `Options` , vous pouvez ajouter des filtres pour exclure des lignes de la prise en compte. Les lignes exclues ont une valeur `NULL` pour cette colonne.

1. Attribuez un nom à la colonne, puis cliquez sur **[!UICONTROL Save]**.

1. La colonne peut être utilisée _immédiatement._
