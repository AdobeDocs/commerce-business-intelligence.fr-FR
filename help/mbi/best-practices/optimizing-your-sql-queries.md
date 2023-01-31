---
title: Optimisation de vos requêtes SQL
description: Découvrez comment optimiser vos requêtes SQL.
exl-id: 2782c707-6a02-4e5d-bfbb-eff20659fbb2
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# Optimisation des requêtes SQL

Le Report Builder SQL vous permet de lancer des requêtes et d’effectuer une itération sur ces requêtes à un moment donné. Cela s’avère utile lorsque vous devez modifier une requête sans avoir à attendre la fin d’un cycle de mise à jour avant de réaliser une colonne ou un rapport que vous avez créé qui doit être mis à jour.

Avant l&#39;exécution d&#39;une requête, [[!DNL MBI] estime son coût](https://support.magento.com/hc/en-us/articles/360016730391). Le coût prend en compte le temps et le nombre de ressources nécessaires pour exécuter une requête. Si ce coût est jugé trop élevé ou si le nombre de lignes retournées dépasse les limites, la requête ne s’exécutera pas. Nous avons dressé une liste des recommandations pour interroger votre entrepôt de données, afin de vous assurer que vous écrivez les requêtes les plus simples possible.

## Utilisation de l’option SELECT (Sélectionner) ou Sélectionner toutes les colonnes

La sélection de toutes les colonnes ne permet pas d’effectuer une requête opportune et facilement exécutée. Requêtes utilisant `SELECT *` L’exécution peut prendre un certain temps, en particulier si votre tableau comporte un grand nombre de colonnes.

C’est pourquoi nous vous recommandons d’éviter d’utiliser `SELECT *` dans la mesure du possible et n’incluez que les colonnes dont vous avez besoin :

| **Au lieu de ça...** | **Essayez ceci !** |
|-----|-----|
| ![](../../mbi/assets/Select_all_1.png) | ![](../../mbi/assets/Select_all_2.png) |

{style=&quot;table-layout:auto&quot;}

## Utilisation de jointures externes complètes

Les jointures externes sélectionnent l&#39;intégralité des deux tables jointes, ce qui augmentera le coût de calcul de la requête. Cela signifie que l’exécution de votre requête prendra plus de temps et qu’elle risque plus d’échouer, car le délai d’exécution peut être plus long que la limite d’exécution pour renvoyer les résultats.

Au lieu d’utiliser ce type de jointure, pensez à utiliser une jointure interne ou de gauche. Les jointures internes renvoient des résultats uniquement lorsqu’il existe une correspondance de colonnes entre les tableaux (par exemple, `order_id` existe dans les deux `customers` et `orders` table); les jointures à gauche renverront tous les résultats du tableau de gauche (premier) avec les résultats correspondants dans le tableau de droite (deuxième).

Découvrez comment réécrire une requête PLEIN OUTER JOIN :

| **Au lieu de ça...** | **Essayez ceci !** |
|-----|-----|
| ![](../../mbi/assets/Full_Outer_Join_1.png) | ![](../../mbi/assets/Full_Outer_Join_2.png) |

{style=&quot;table-layout:auto&quot;}

Comme vous pouvez le voir, ces requêtes sont identiques dans tous les sens, à l’exception du type JOIN qu’elles utilisent.

## Utilisation de plusieurs jointures

Bien que vous puissiez inclure plusieurs jointures dans votre requête, n’oubliez pas que cela peut entraîner la hausse des coûts de la requête. Pour éviter d’atteindre le seuil de coût, nous vous recommandons d’éviter, si possible, plusieurs jointures.

## Utilisation des filtres

Utilisez des filtres chaque fois que possible. `WHERE` et `HAVING` les clauses filtreront vos résultats et ne vous donneront que les données que vous souhaitez.

## Utilisation de filtres dans les clauses JOIN

Si vous utilisez un filtre lors de l&#39;exécution d&#39;une jointure, veillez à l&#39;appliquer aux deux tableaux de la jointure. Même s’il est redondant, cela réduit le coût de calcul de la requête et accélère le temps d’exécution.

| **Au lieu de ça...** | **Essayez ceci !** |
|-----|-----|
| ![](../../mbi/assets/Join_filters_1.png) | ![](../../mbi/assets/Join_filters_2.png) |

{style=&quot;table-layout:auto&quot;}

## Utilisation d’opérateurs

Lorsque vous écrivez des requêtes, pensez à utiliser les opérateurs &quot;moins chers&quot; possibles. Chaque requête a un coût de calcul, qui est déterminé par les fonctions, opérateurs et filtres qui composent la requête. Certains opérateurs nécessitent moins d&#39;effort de calcul, ce qui les rend moins coûteux que d&#39;autres.

Les opérateurs de comparaison (>, &lt;, =, etc.) sont les moins chers, suivis par [C&#39;EST COMME. Opérateurs SIMILAIRES À et POSIX](https://www.postgresql.org/docs/9.5/functions-matching.html) qui sont les opérateurs les plus chers.

## Utilisation d’EXISTS contre IN

Utilisation `EXISTS` versus `IN` dépend du type de résultats que vous essayez de renvoyer. Si une seule valeur vous intéresse, utilisez la variable `EXISTS` au lieu de `IN`. `IN` est utilisé conjointement avec les listes de valeurs séparées par des virgules, ce qui augmentera le coût de calcul de la requête.

When `IN` les requêtes sont exécutées, le système doit d’abord traiter la sous-requête (la variable `IN` ), puis la requête entière en fonction de la relation spécifiée dans la variable `IN` . `EXISTS` est beaucoup plus efficace, car la requête n’a pas à être exécutée plusieurs fois : une valeur true/false est renvoyée lors de la vérification de la relation spécifiée dans la requête.

Pour le dire simplement : le système n’a pas à traiter autant lors de l’utilisation de `EXISTS`.

| **Au lieu de ça...** | **Essayez ceci !** |
|-----|-----|
| ![](../../mbi/assets/Exists_1.png) | ![](../../mbi/assets/Exists_2.png) |

{style=&quot;table-layout:auto&quot;}

## Utilisation de ORDER BY

`ORDER BY` est une fonction coûteuse en SQL et peut augmenter considérablement le coût d’une requête. Si vous recevez un message d’erreur indiquant que le coût EXPLAIN de votre requête est trop élevé, essayez d’éliminer tout `ORDER BY`est de votre requête, sauf si cela est absolument nécessaire.

Cela ne veut pas dire que `ORDER BY` ne peuvent pas être utilisées, mais uniquement lorsqu’elles le sont.

## Utilisation de GROUP BY et ORDER BY

Bien que cette approche ne soit pas conforme à ce que vous essayez de faire dans certains cas, la règle générale est que si vous utilisez une `GROUP BY` et `ORDER BY`, vous devez placer les colonnes des deux clauses dans le même ordre. Par exemple :

| **Au lieu de ça...** | **Essayez ceci !** |
|-----|-----|
| ![](../../mbi/assets/Group_by_2.png) | ![](../../mbi/assets/Group_by_1.png) |

{style=&quot;table-layout:auto&quot;}

## Remplissage

La meilleure façon d&#39;apprendre à écrire du SQL - et de le faire efficacement - est par tâtonnements successifs. Pour trouver ce qui vous convient le mieux, essayez de recréer quelques rapports en utilisant uniquement l&#39;éditeur SQL.
