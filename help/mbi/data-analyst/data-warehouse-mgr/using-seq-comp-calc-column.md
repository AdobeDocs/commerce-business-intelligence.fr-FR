---
title: Colonne calculée de comparaison séquentielle
description: Découvrez l’objectif et les utilisations de la colonne calculée Comparaison séquentielle .
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 2433a614e9858684842804a0ae29fb67f0d41ead
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Colonne calculée de comparaison séquentielle

Cette rubrique décrit l’objectif et les utilisations de la colonne calculée `Sequential Comparison` disponible dans la page **[!DNL Manage Data > Data Warehouse]**. Vous trouverez ci-dessous une explication de ce qu&#39;il fait, suivie d&#39;un exemple et des mécanismes de sa création.

**Explication**

Le type de colonne `Sequential Comparison` : trouve la différence entre les événements consécutifs. Le type de colonne `Sequential Comparison` le plus courant est la colonne `Seconds since previous order`. Trois entrées sont nécessaires pour cette colonne :

1. `Event Owner` : cette entrée détermine l’entité pour laquelle les lignes sont regroupées. Par exemple, dans la colonne `Seconds since previous order`, le propriétaire de l’événement est le client, car vous souhaitez trouver le nombre de secondes depuis la commande précédente du même client.
1. `Event Date` : cette entrée applique la séquence d’événements. Dans les cas de `Seconds since previous order`, la colonne contenant l’horodatage de la commande doit être la `Event Date`. Cette entrée est toujours un horodatage.
1. `Value to Compare` : cette entrée est la valeur réelle à comparer. Elle soustrait la valeur de la ligne précédente de la valeur de la ligne actuelle. Par conséquent, une colonne recherchant la différence de temps entre les commandes successives d’un client est appelée `Seconds since previous order`. Cette entrée ne doit pas nécessairement être un horodatage. Un exemple non horodaté consiste à trouver la différence de valeur de commande entre les commandes successives d’un client.

**Exemple**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 2015-01-01 00:00:00 | NULL |
| **`2`** | B | 2015-01-01 00:30:00 | NULL |
| **`3`** | A | 2015-01-01 02:00:00 | 7200 |
| **`4`** | A | 2015-01-02 13:00:00 | 126000 |
| **`5`** | B | 2015-01-03 13:00:00 | 217800 |

Dans l’exemple ci-dessus, `Seconds since owner's previous event` est la colonne calculée `Sequential Comparison`. Pour le `owner_id = A`, il identifie d’abord une séquence basée sur la colonne `timestamp`, puis soustrait le `timestamp` de l’événement précédent de l’horodatage de l’événement actuel. Dans la troisième ligne du tableau (la deuxième ligne pour `owner_id A`), la valeur de `Seconds since owner's previous event` est le nombre de secondes entre &#39;2015-01-01 02:00&#39; et &#39;2015-01-01 00:00:00&#39;. Cette différence est égale à deux heures = 7 200 secondes.

Pour ce type de colonne calculé, la ligne correspondant au premier événement du propriétaire a une valeur `NULL`.

**Mécanique**

Pour créer une colonne **Event Number** :

1. Accédez à la page **[!DNL Manage Data > Data Warehouse]**.

1. Accédez au tableau sur lequel vous souhaitez créer cette colonne.

1. Cliquez sur **[!UICONTROL Create New Column]** dans le coin supérieur droit.

1. Sélectionnez `Same Table` comme `Definition Type` (si les colonnes que vous souhaitez comparer ne se trouvent pas sur la même table, vous devrez peut-être les déplacer).

1. Sélectionnez `SEQUENTIAL_COMPARISON` comme `Column Definition Equation`.

1. Choisissez les entrées, comme expliqué ci-dessus :
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`

1. Vous pouvez également ajouter des filtres pour exclure les lignes de la prise en compte. Les lignes exclues ont une valeur `NULL` pour cette colonne.

1. Attribuez un nom à la colonne en haut de la page et cliquez sur **[!UICONTROL Save]**.

1. La colonne peut utiliser *immédiatement*.

![SEC](../../assets/SEC_new.png)
