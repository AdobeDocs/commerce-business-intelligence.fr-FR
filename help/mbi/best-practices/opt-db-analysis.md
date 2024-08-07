---
title: Optimisation de la base de données pour l’analyse
description: Découvrez comment optimiser votre base de données pour l’analyse.
exl-id: e73e1a1e-c933-476d-97bc-bd8f52bb2fa1
role: Admin, Data Architect, Data Engineer, User
feature: Business Performance, Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# Optimiser votre base de données

L&#39;avantage principal de l&#39;utilisation d&#39;une base de données opérationnelle pour [!DNL Adobe Commerce Intelligence] est que rien n&#39;a besoin d&#39;être construit ou modifié pour collecter des données. Il y a déjà des informations précieuses, il suffit de les déverrouiller.

Cette rubrique contient quelques recommandations destinées à vous aider à optimiser votre base de données pour l’analyse et à obtenir des informations exploitables à partir de données brutes.

## Ne pas supprimer de données

>[!TIP]
>
>Les lois locales et internationales qui affectent votre entreprise (et vos propres conditions d’utilisation) peuvent affecter les types de données que vous pouvez conserver et la durée pendant laquelle vous pouvez les conserver. Le respect de ces lois devrait être votre première priorité.

Lorsqu’une commande est annulée, qu’un utilisateur désactive son compte ou qu’un produit est arrêté, il est tentant de supprimer les informations associées dans la base de données. Les tables poussent et éliminent l&#39;encombrement semble être une idée prudente. Cependant, la suppression de lignes signifie que ces informations sont perdues pour toujours ou que vous devez effectuer d’anciennes sauvegardes pour les retrouver.

Vous pouvez ajouter une colonne d’état au tableau qui indique quand la ligne n’est plus active ou pertinente. Il est également recommandé d’ajouter une colonne qui stocke la date de la modification ou de créer un journal pour les modifications historiques. Si les tableaux deviennent suffisamment volumineux pour que les performances commencent à diminuer, pensez à archiver les anciennes données dans un tableau utilisé pour les analyses.

## Écraser rarement des données

Le remplacement des données doit être effectué avec modération et avec précaution.

En prenant l’exemple des dates de connexion, de nombreuses entreprises stockent la date de dernière connexion plutôt qu’une table des connexions historiques. Bien que vous puissiez avoir uniquement besoin de la date de dernière connexion à des fins fonctionnelles, ces données remplacées représentent une perte énorme du point de vue des analyses. Si vous ne conservez pas un journal complet de ces actions, vous ne pourrez plus voir combien d’utilisateurs sont restés à l’écart pendant de longues périodes, puis ont été réactivés. Cela rend également impossible la création d’éléments tels que des analyses des cohortes d’engagement des utilisateurs basées sur les connexions.

En règle générale, si vous mettez à jour un enregistrement en raison d’une action de l’utilisateur, ne remplacez pas les informations relatives à une action précédente ou d’un utilisateur distinct.

## Inclure `Updated_at` colonnes pour les données mises à jour au fil du temps

Si les valeurs des lignes d’une table changent au fil du temps, par exemple si **order\_status** passe de`processing` à `complete`, incluez une colonne **updated\_at** afin d’enregistrer le moment où la dernière modification se produit. Assurez-vous qu’une valeur **updated\_at** est disponible lors de la première insertion de la nouvelle ligne de données, lorsque la date **updated\_at** correspond à la date **created\_at**.

Outre l’optimisation pour les analyses, les colonnes **updated\_at** vous permettent également d’utiliser les [méthodes de réplication incrémentielle](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md), qui peuvent aider à raccourcir la durée de vos cycles de mise à jour.

## Store User Acquisition Source

L’une des erreurs les plus courantes est la [source d’acquisition d’utilisateurs](../data-analyst/analysis/google-track-user-acq.md) (UAS) qui n’est pas stockée dans la base de données opérationnelle. Dans la plupart des cas, lorsqu’il s’agit d’un problème, l’UAS est uniquement suivi via [!DNL Google Analytics] ou un autre outil d’analyse web. Bien que ces outils puissent s’avérer utiles, le stockage exclusif de l’UAS présente certains inconvénients. Par exemple, vous ne pouvez pas extraire des données au niveau de l’utilisateur à partir de ces outils. Quand c&#39;est possible, c&#39;est généralement un processus difficile. Il devrait être facile d’obtenir ces informations et de les associer à des données provenant d’autres sources, telles que les informations comportementales et transactionnelles également stockées dans votre base de données.

Le stockage de l’UAS dans votre propre base de données est souvent la plus grande amélioration qu’une entreprise en ligne puisse apporter à ses capacités d’analyse. Cela permet d’analyser les ventes, l’engagement des utilisateurs, les périodes de retour sur investissement, la valeur de durée de vie des clients, l’attrition et d’autres mesures critiques par l’interface utilisateur (UAS). [Ces données sont essentielles pour décider où investir des ressources marketing](../data-analyst/analysis/most-value-source-channel.md).

Trop d’entreprises se concentrent uniquement sur la recherche de canaux qui fournissent de nouveaux utilisateurs au moindre coût. Si vous ne suivez pas la qualité des utilisateurs acquis de chaque canal, vous courez le risque d’attirer des utilisateurs qui ne génèrent pas de valeur ajoutée.

## Configuration du tableau de données

### Définition d’une clé de Principal

Une [clé primaire](https://en.wikipedia.org/wiki/Unique_key) est une colonne (ou un ensemble de colonnes) qui produit des valeurs uniques dans un tableau. Les clés de Principal sont incroyablement importantes, car elles garantissent que vos tables sont correctement répliquées dans [!DNL Commerce Intelligence].

Lors de la création de clés primaires, utilisez un type de données entier pour la colonne qui augmente automatiquement. Adobe vous recommande d’éviter, dans la mesure du possible, d’utiliser plusieurs clés primaires à colonnes.

Si votre table est une vue SQL, ajoutez une colonne pouvant agir comme clé primaire. [!DNL Commerce Intelligence] peut identifier automatiquement cette colonne comme clé primaire.

### Affectation d’un type de données à votre colonne de données

Si une colonne de données n’a pas de [type de données](https://en.wikipedia.org/wiki/Data_type) affecté, [!DNL Commerce Intelligence] détermine le type de données à utiliser. Si le système ne devine pas correctement, vous ne pourrez peut-être pas effectuer les analyses appropriées tant que l’équipe d’assistance à l’Adobe n’aura pas adapté la colonne au type de données approprié. Par exemple, si une colonne de date est considérée comme un type de données numérique, vous pouvez suivre la tendance au fil du temps à l’aide de cette dimension de date.

### Ajouter des préfixes à vos tableaux de données si vous disposez de plusieurs bases de données

Si plusieurs bases de données sont connectées à [!DNL Commerce Intelligence], Adobe vous recommande d’ajouter des préfixes à vos tables afin d’éviter toute confusion. Les préfixes vous aident à mémoriser d’où proviennent les mesures ou les dimensions de données.
