---
title: Opérateurs de filtres spéciaux
description: Découvrez quelques opérateurs spéciaux utilisés dans les filtres lors de la création d’un rapport ou d’une mesure.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# Options de filtre

Dans cet article, nous allons explorer quelques sujets spécifiques `operators` utilisé dans `filters` when [création d&#39;un rapport](../../tutorials/using-visual-report-builder.md){ : target=&quot;_blank&quot;} ou [création d’une mesure](../../data-user/reports/ess-manage-data-metrics.md){ : target=&quot;_blank&quot;}.

## `Filter Operators`

* `LIKE` pour la correspondance de modèle. Il doit être utilisé conjointement avec les caractères génériques % (pour un caractère générique avec un nombre variable de lettres) ou _ (pour un caractère générique à une seule lettre).  Par exemple, la restriction `LIKE \_ake%` renvoie true pour `Jake Stein`, `Jake Smith`ou `Fake Smith`.  La valeur renvoyée est false pour `Drake Smith`.

* `NOT LIKE` est similaire à la correspondance de modèles ci-dessus, mais vérifie quels modèles ne correspondent pas.

* `IS` vérifie si la colonne est `NULL`ou vide.

* `IS NOT` est similaire au `IS` , mais vérifie les colonnes non NULL.

* `IN` recherche la présence d’une valeur dans une liste séparée par des virgules. (par exemple, &quot;Couleur&quot; `IN` rouge, orange&quot; est l’équivalent de couleur `equal to` rouge OU couleur `equal to` orange).

* `NOT IN` est similaire à `IN` ci-dessus, mais vérifie l’absence d’une valeur.
