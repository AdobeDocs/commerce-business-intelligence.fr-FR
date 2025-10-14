---
title: Opérateurs de filtres spéciaux
description: Découvrez quelques opérateurs spéciaux utilisés dans les filtres lors de la création d’un rapport ou d’une mesure.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Options de filtre

Cette rubrique explore quelques `operators` spéciales utilisées dans `filters` lors de la [création d’un rapport](../../tutorials/using-visual-report-builder.md){: target="_blank"} ou de la [&#x200B; d’une mesure](../../data-user/reports/ess-manage-data-metrics.md){: target="_blank"}.

## `Filter Operators`

* `LIKE` pour la correspondance de modèles. Utilisez-le avec les caractères génériques % (pour un caractère générique avec un nombre variable de lettres) ou _ (pour une lettre simple avec un caractère générique).  Par exemple, la `LIKE \_ake%` de restriction renvoie true pour `Jake Stein`, `Jake Smith` ou `Fake Smith`.  Elle renverrait false pour `Drake Smith`.

* `NOT LIKE` est similaire à la correspondance de modèles ci-dessus, mais vérifie les modèles qui ne correspondent pas.

* `IS` vérifie si la colonne est `NULL` ou vide.

* `IS NOT` est similaire à l’opérateur `IS` ci-dessus, mais vérifie les colonnes non NULL.

* `IN` vérifie la présence d’une valeur dans une liste séparée par des virgules. (par exemple, « Couleur `IN` rouge, orange » équivaut à la couleur `equal to` rouge OU couleur `equal to` orange).

* `NOT IN` est similaire à `IN` ci-dessus, mais vérifie l’absence d’une valeur.
