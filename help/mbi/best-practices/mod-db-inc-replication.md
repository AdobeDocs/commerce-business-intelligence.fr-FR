---
title: Modification de la base de données pour la prise en charge de la réplication incrémentielle
description: Découvrez comment modifier votre base de données pour prendre en charge la réplication incrémentielle.
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Prise en charge de la réplication incrémentielle

Si vos tableaux ne permettent actuellement pas la réplication incrémentielle, reportez-vous aux recommandations suivantes pour les solutions possibles.

## Modifications pour modification à l’adresse

Le `Modified At` , qui est la méthode de réplication la plus adaptée, utilise une `datetime` pour détecter les données nouvelles et/ou mises à jour. N’oubliez pas que la variable `datetime` dans les tables utilisant cette méthode doit être indexée et ne peut pas contenir de valeurs nulles à tout moment.

Si votre tableau ne comporte pas de `datetime` colonne, vous pouvez ajouter un index `modified at` colonne . Les valeurs nulles ne sont pas autorisées dans un `modified at` colonne . Vérifiez que la colonne est renseignée pour chaque ligne.

Pour garantir la variable `Modified At` fonctionne comme prévu, vous ne pouvez pas supprimer de lignes du tableau. Vous devez plutôt marquer la ligne comme non valide en ajoutant une `deleted` au tableau. Cette colonne renverra une `1` si la ligne n’est pas valide et `0` dans le cas contraire. Vous pouvez ensuite utiliser cette colonne pour filtrer les lignes non valides lors de la création de mesures et de rapports.

## Modifications pour une clé Principal d’incrémentation automatique unique

Si la variable `Modified At` ne peut pas être activée, alors la clé Principal d’incrémentation automatique unique est la meilleure option suivante. De nouvelles données sont découvertes dans les tableaux à l’aide de cette méthode en recherchant des valeurs de clé Principales supérieures à la valeur la plus élevée actuelle dans le Data Warehouse.

N’oubliez pas que les tableaux utilisant cette méthode sont des colonnes simples avec des entiers incrémentant automatiquement les Principales clés. Pour utiliser cette méthode dans votre base de données, apportez les modifications suivantes :

* Si la clé Principale est soit une clé composite, soit un nombre non entier, remplacez la clé Principale par un nombre entier d’incrémentation automatique.
* Si la clé Principale est une seule colonne entière, mais que des clés peuvent être affectées de manière non séquentielle, modifiez la clé Principale pour qu’elle s’incrémente automatiquement.

## Remplissage

En apportant des modifications mineures à vos tableaux, vous pouvez tirer parti des méthodes de réplication incrémentielle plus rapides et plus efficaces. toutefois, si cela n’est toujours pas possible, vous pouvez tout de même prendre d’autres mesures pour [réduire le temps de mise à jour](../best-practices/reduce-update-cycle-time.md) et [optimiser votre base de données](../best-practices/opt-db-analysis.md).
