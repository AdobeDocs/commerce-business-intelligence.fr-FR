---
title: Modification de la base de données pour la prise en charge de la réplication incrémentielle
description: Découvrez comment modifier votre base de données pour prendre en charge la réplication incrémentielle.
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# Prise en charge de la réplication incrémentielle

Si vos tableaux ne permettent actuellement pas la réplication incrémentielle, reportez-vous aux recommandations suivantes pour les solutions possibles.

## Modifications pour modification à l’adresse

La méthode `Modified At`, qui est la méthode de réplication la plus idéale, utilise une colonne `datetime` pour détecter de nouvelles données et/ou des données mises à jour. N’oubliez pas que la colonne `datetime` des tables utilisant cette méthode doit être indexée et ne peut pas contenir de valeurs nulles à tout moment.

Si votre table ne contient pas de colonne `datetime`, vous pouvez ajouter une colonne d&#39;index `modified at`. Les valeurs nulles ne sont pas autorisées dans une colonne `modified at`. Vérifiez que la colonne est renseignée pour chaque ligne.

Pour vous assurer que la méthode `Modified At` fonctionne comme prévu, vous ne pouvez pas supprimer de lignes de la table. Vous devez plutôt marquer la ligne comme non valide en ajoutant une colonne `deleted` au tableau. Cette colonne renvoie un `1` si la ligne n’est pas valide et `0` dans le cas contraire. Vous pouvez ensuite utiliser cette colonne pour filtrer les lignes non valides lors de la création de mesures et de rapports.

## Modifications pour une clé de Principal à incrémentation automatique unique

Si la méthode `Modified At` ne peut pas être activée, la clé de Principal d’incrémentation automatique unique est la meilleure option suivante. De nouvelles données sont découvertes dans les tableaux à l’aide de cette méthode en recherchant des valeurs de clé primaire supérieures à la valeur la plus élevée actuelle dans le Data Warehouse.

N’oubliez pas que les tableaux utilisant cette méthode sont des colonnes simples avec des entiers incrémentant automatiquement les clés primaires. Pour utiliser cette méthode dans votre base de données, apportez les modifications suivantes :

* Si la clé primaire est soit une clé composite, soit un nombre non entier, remplacez la clé primaire par un nombre entier d’incrémentation automatique.
* Si la clé primaire est une seule colonne entière, mais que des clés peuvent être affectées de manière non séquentielle, modifiez la clé primaire pour qu’elle soit incrémentée automatiquement.

## Remplissage

En apportant des modifications mineures à vos tableaux, vous pouvez tirer parti des méthodes de réplication incrémentielle plus rapides et plus efficaces. Cependant, si cela n&#39;est pas possible, vous pouvez tout de même prendre d&#39;autres mesures pour [réduire le temps de mise à jour](../best-practices/reduce-update-cycle-time.md) et [optimiser votre base de données](../best-practices/opt-db-analysis.md).
