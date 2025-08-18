---
title: Modification de la base de données pour prendre en charge la réplication incrémentielle
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

Si vos tables ne permettent pas actuellement la réplication incrémentielle, reportez-vous aux recommandations suivantes pour obtenir des solutions possibles.

## Modifications pour Modified At

La méthode `Modified At`, qui est la méthode de réplication la plus idéale, utilise une colonne `datetime` pour détecter les données nouvelles et/ou mises à jour. N&#39;oubliez pas que la colonne `datetime` dans les tables utilisant cette méthode doit être indexée et ne peut contenir à aucun moment des valeurs nulles.

Si votre tableau ne comporte pas de colonne `datetime`, vous pouvez ajouter une colonne de `modified at` d’index. Les valeurs nulles ne sont pas autorisées dans une colonne `modified at`. Vérifiez que la colonne est renseignée pour chaque ligne.

Pour que la méthode `Modified At` fonctionne comme prévu, vous ne pouvez pas supprimer de lignes du tableau. Vous devez plutôt marquer la ligne comme non valide en ajoutant une colonne `deleted` au tableau. Cette colonne renvoie une `1` si la ligne n’est pas valide et `0` dans le cas contraire. Vous pouvez ensuite utiliser cette colonne pour filtrer les lignes non valides lorsque vous créez des mesures et des rapports.

## Modifications pour une seule clé de Principal d’incrémentation automatique

Si la méthode `Modified At` ne peut pas être activée, la clé de Principal à incrémentation automatique unique est la meilleure option suivante. Les nouvelles données sont découvertes dans les tableaux à l’aide de cette méthode en recherchant des valeurs de clé primaire qui sont supérieures à la valeur la plus élevée actuelle dans le Data Warehouse.

N’oubliez pas que les tableaux utilisant cette méthode sont à une seule colonne avec des clés primaires d’incrémentation automatique de nombres entiers. Pour utiliser cette méthode dans votre base de données, effectuez les modifications suivantes :

* Si la clé primaire est une clé composite ou non entière, remplacez-la par un entier à incrémentation automatique
* Si la clé primaire est une colonne entière unique mais que les clés peuvent être affectées de manière non séquentielle, modifiez la clé primaire en incrémentant automatiquement

## Conclusion

En apportant des modifications mineures à vos tableaux, vous pouvez tirer parti des méthodes de réplication incrémentielle plus rapides et plus efficaces. Cependant, si cela s’avère impossible, vous pouvez prendre d’autres mesures pour [réduire le temps de mise à jour](../best-practices/reduce-update-cycle-time.md) et [optimiser votre base de données](../best-practices/opt-db-analysis.md).
