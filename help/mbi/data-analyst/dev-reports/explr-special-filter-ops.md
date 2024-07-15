---
title: Opérateurs de filtres spéciaux
description: Découvrez quelques opérateurs spéciaux utilisés dans les filtres lors de la création d’un rapport ou d’une mesure.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Options de filtre

Cette rubrique explore quelques `operators` spéciaux utilisés dans `filters` lors de la [création d’un rapport](../../tutorials/using-visual-report-builder.md){: target=&quot;_blank&quot;} ou de la [création d’une mesure](../../data-user/reports/ess-manage-data-metrics.md){: target=&quot;_blank&quot;}.

## `Filter Operators`

* `LIKE` pour la correspondance de motifs. Il doit être utilisé avec les caractères génériques % (pour un caractère générique avec un nombre de lettres variable) ou _ (pour un caractère générique à une seule lettre).  Par exemple, la restriction `LIKE \_ake%` renvoie true pour `Jake Stein`, `Jake Smith` ou `Fake Smith`.  Elle renvoie false pour `Drake Smith`.

* `NOT LIKE` est similaire à la correspondance de modèles ci-dessus, mais vérifie quels modèles ne correspondent pas.

* `IS` vérifie si la colonne est `NULL` ou vide.

* `IS NOT` est similaire à l’opérateur `IS` ci-dessus, mais recherche des colonnes non NULL.

* `IN` recherche la présence d’une valeur dans une liste séparée par des virgules. (par exemple, &quot;Couleur `IN` rouge,orange&quot; est l’équivalent de la couleur `equal to` rouge OU couleur `equal to` orange).

* `NOT IN` est similaire à `IN` ci-dessus, mais vérifie l’absence d’une valeur.
