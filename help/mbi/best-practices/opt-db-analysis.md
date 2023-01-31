---
title: Optimisation de la base de données pour l’analyse
description: Découvrez comment optimiser votre base de données pour l’analyse.
exl-id: e73e1a1e-c933-476d-97bc-bd8f52bb2fa1
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 0%

---

# Optimiser votre base de données

Le Principal avantage de l&#39;utilisation d&#39;une base de données opérationnelle pour les renseignements commerciaux est que rien n&#39;a besoin d&#39;être construit ou modifié pour collecter des données. De précieuses informations existent déjà; tout ce que tu as à faire est de le déverrouiller.

Cette rubrique contient quelques recommandations destinées à vous aider à optimiser votre base de données pour l’analyse et à obtenir des informations exploitables à partir de données brutes.

## Ne pas supprimer de données

>[!TIP]
>
>Les lois locales et internationales qui affectent votre entreprise (et vos propres conditions d’utilisation) peuvent affecter les types de données que vous pouvez conserver et la durée pendant laquelle vous pouvez les conserver. Le respect de ces lois devrait être votre première priorité.

Lorsqu’une commande est annulée, qu’un utilisateur désactive son compte ou qu’un produit est arrêté, il est tentant de supprimer les informations associées dans la base de données. Les tables poussent et éliminent l&#39;encombrement semble être une idée prudente. Cependant, la suppression de lignes signifie que ces informations sont perdues pour toujours ou que vous devrez effectuer d’anciennes sauvegardes pour les retrouver.

Vous pouvez plutôt ajouter une colonne d’état au tableau qui indique quand la ligne n’est plus principale ou pertinente. Il est également recommandé d’ajouter une colonne qui stocke la date de la modification ou de créer un journal pour les modifications historiques. Si les tableaux deviennent suffisamment volumineux pour que les performances commencent à diminuer, pensez à archiver les anciennes données dans un tableau utilisé pour les analyses.

## Remplacer rarement les données

Le remplacement des données doit être effectué avec modération et avec précaution.

En prenant l’exemple des dates de connexion, de nombreuses entreprises stockent la date de dernière connexion plutôt qu’une table des connexions historiques. Bien que vous puissiez avoir uniquement besoin de la date de dernière connexion à des fins fonctionnelles, ces données remplacées représentent une perte énorme du point de vue des analyses. Si vous ne conservez pas un journal complet de ces actions, vous ne pourrez plus voir combien d’utilisateurs sont restés à l’écart pendant de longues périodes, puis ont été réactivés. Cela rend également impossible la création d’éléments tels que des analyses des cohortes d’engagement des utilisateurs basées sur les connexions.

En règle générale, si vous mettez à jour un enregistrement en raison d’une action de l’utilisateur, ne remplacez pas les informations relatives à une action précédente ou d’un utilisateur distinct.

## Inclure `Updated_at` Colonnes de données mises à jour au fil du temps

Si les valeurs des lignes d’un tableau changent au fil du temps, par exemple : **order\_status** change depuis`processing` to `complete`, incluez une **updated\_at** pour enregistrer le moment où la dernière modification se produit. Assurez-vous que la variable **updated\_at** est disponible lors de la première insertion de la nouvelle ligne de données, à ce moment la variable **updated\_at** date correspond au **created\_at** date.

En plus de l&#39;optimisation pour les analyses, **updated\_at** Les colonnes vous permettent également d’utiliser [Méthodes de réplication incrémentielle](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md), ce qui peut vous aider à raccourcir la durée de vos cycles de mise à jour.

## Store User Acquisition Source

L’une des erreurs les plus courantes est la suivante : [source d’acquisition d’utilisateurs](../data-analyst/analysis/google-track-user-acq.md) (UAS) non stocké dans la base de données opérationnelle. Dans la plupart des cas où il s’agit d’un problème, le suivi de l’UAS se fait uniquement par le biais de [!DNL Google Analytics] ou un autre outil web analytics. Bien que ces outils puissent être extrêmement utiles, le stockage exclusif de l&#39;UAS présente certains inconvénients; par exemple, vous ne pouvez pas extraire de données au niveau de l’utilisateur à partir de ces outils. Quand c&#39;est possible, c&#39;est généralement un processus difficile. Il devrait être facile d’obtenir ces informations et de les associer à des données provenant d’autres sources, telles que les informations comportementales et transactionnelles également stockées dans votre base de données.

Le stockage de l’UAS dans votre propre base de données est souvent la plus grande amélioration que les entreprises en ligne peuvent apporter à leurs capacités d’analyse. Cela permet d’analyser les ventes, l’engagement des utilisateurs, les périodes de retour sur investissement, la valeur de durée de vie des clients, l’attrition et d’autres mesures critiques par l’interface utilisateur (UAS). [Ces données sont essentielles pour décider où investir les ressources marketing](../data-analyst/analysis/most-value-source-channel.md).

Trop d’entreprises se concentrent uniquement sur la recherche de canaux qui fournissent les nouveaux utilisateurs au moindre coût. Cependant, si vous ne suivez pas la qualité des utilisateurs acquis de chaque canal, vous courez le risque d’attirer des utilisateurs qui ne génèrent pas de valeur commerciale.

## Configuration du tableau de données

### Définition d’une clé Principal

A [Clé Principale](http://en.wikipedia.org/wiki/Unique_key) est une colonne (ou un ensemble de colonnes) inchangée qui produit des valeurs uniques dans un tableau. Les clés Principal sont extrêmement importantes, car elles garantissent que vos tableaux sont correctement répliqués dans [!DNL MBI].

Lors de la création de Principales clés, utilisez un type de données entier pour la colonne qui augmente automatiquement. Dans la mesure du possible, nous vous recommandons également de ne pas utiliser de clés Principales à plusieurs colonnes.

Si votre table est une vue SQL, ajoutez une colonne pouvant agir comme une clé Principale. [!DNL MBI] pourra identifier automatiquement cette colonne en tant que clé Principale.

### Affectation d’un type de données à votre colonne de données

Si une colonne de données n’est pas affectée [type de données](http://en.wikipedia.org/wiki/Data_type), [!DNL MBI] devine le type de données à utiliser. Si le système ne devine pas correctement, vous ne pourrez peut-être pas effectuer les analyses appropriées tant que notre équipe de support n’aura pas adapté la colonne au type de données approprié. Par exemple, si une colonne de date est considérée comme un type de données numérique, vous pouvez suivre la tendance au fil du temps à l’aide de cette dimension de date.

### Ajouter des préfixes à vos tableaux de données si vous disposez de plusieurs bases de données

Si plusieurs bases de données sont connectées à [!DNL MBI], nous vous recommandons d’ajouter des préfixes à vos tableaux pour éviter toute confusion. Les préfixes vous aideront à vous rappeler d’où proviennent les mesures ou les dimensions de données.
