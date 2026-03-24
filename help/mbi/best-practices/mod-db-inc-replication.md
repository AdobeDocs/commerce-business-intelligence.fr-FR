---
title: Modification de la base de données pour prendre en charge la réplication incrémentielle
description: Découvrez comment modifier votre base de données pour prendre en charge la réplication incrémentielle.
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
role: Admin, Developer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
TQID: https://experienceleague.adobe.com/VH5mhfRJteAxiQAmh14TzhnAqym65X6SFRMGuSuEvwM
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 334
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
