---
title: Opérateurs de filtres spéciaux
description: Découvrez quelques opérateurs spéciaux utilisés dans les filtres lors de la création d’un rapport ou d’une mesure.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/xUfPCWqheQFIG9faVsA5PEWiyn6hLO-Rrm8jPzmaWiw
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 143
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
