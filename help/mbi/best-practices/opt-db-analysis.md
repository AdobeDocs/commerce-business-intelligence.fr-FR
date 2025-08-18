---
title: Optimisation de votre base de données pour l'analyse
description: Découvrez comment optimiser votre base de données pour l’analyse.
exl-id: e73e1a1e-c933-476d-97bc-bd8f52bb2fa1
role: Admin, Data Architect, Data Engineer, User
feature: Business Performance, Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# Optimisation de votre base de données

L&#39;avantage principal de l&#39;utilisation d&#39;une base de données opérationnelle pour [!DNL Adobe Commerce Intelligence] est que rien n&#39;a besoin d&#39;être construit ou modifié pour collecter des données. Des informations précieuses sont déjà là : il vous suffit de les déverrouiller.

Cette rubrique contient quelques recommandations pour vous aider à optimiser votre base de données pour l’analyse et à tirer des informations exploitables des données brutes.

## Ne Pas Supprimer Les Données

>[!TIP]
>
>Les lois locales et internationales qui affectent votre entreprise (et vos propres conditions d’utilisation) peuvent avoir une incidence sur les types de données que vous pouvez conserver et la durée de conservation de ces données. Le respect de ces lois devrait être votre première priorité.

Lorsqu’une commande est annulée, qu’un utilisateur désactive son compte ou qu’un produit est arrêté, il est tentant de supprimer les informations associées dans la base de données. Les tableaux s’allongent et l’élimination de l’encombrement semble une idée prudente. Toutefois, la suppression de lignes signifie que ces informations sont perdues à jamais ou que vous devez parcourir d’anciennes sauvegardes pour les trouver.

Au lieu de cela, vous pouvez ajouter une colonne de statut au tableau, qui indique le moment où la ligne n’est plus active ou pertinente. Il est également recommandé d’ajouter une colonne qui stocke la date à laquelle la modification a été apportée ou de créer un journal pour les modifications historiques. Si les tableaux deviennent suffisamment volumineux pour que les performances commencent à en pâtir, envisagez d’archiver les anciennes données dans un tableau utilisé à des fins d’analyse.

## Rarement Remplacer les données

Le remplacement des données doit être effectué avec parcimonie et précaution.

En prenant comme exemple les dates de connexion, de nombreuses entreprises stockent la dernière date de connexion plutôt qu’un tableau des connexions historiques. Bien que vous n’ayez besoin de la dernière date de connexion que pour des raisons fonctionnelles, ces données écrasées représentent une énorme perte du point de vue analytique. Le fait de ne pas tenir de journal complet de ces actions élimine la possibilité de voir combien d’utilisateurs sont restés en dehors du service pendant de longues périodes, puis ont été réactivés. Il est également impossible de créer des éléments tels que des analyses de cohortes d’engagement des utilisateurs basées sur les connexions.

En règle générale, si vous mettez à jour un enregistrement en raison d’une action de l’utilisateur, ne remplacez pas les informations relatives à une action de l’utilisateur précédente ou distincte.

## Inclure `Updated_at` colonnes pour les données mises à jour au fil du temps

Si les valeurs des lignes d&#39;une table changent au fil du temps, par exemple, **order\_status** passe de`processing` à `complete`, incluez une colonne **updated\_at** pour enregistrer la date de la dernière modification. Vérifiez qu’une valeur **updated\_at** est disponible lors de la première insertion de la nouvelle ligne de données, lorsque la date **updated\_at** correspond à la date **created\_at**.

En plus d’optimiser l’analyse, les colonnes **updated\_at** vous permettent d’utiliser des [méthodes de réplication incrémentale](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md), ce qui peut réduire la durée de vos cycles de mise à jour.

## Stocker le Source d’acquisition d’utilisateurs

L&#39;une des erreurs les plus courantes est le [source d&#39;acquisition utilisateur](../data-analyst/analysis/google-track-user-acq.md) (UAS) qui n&#39;est pas stocké dans la base de données opérationnelle. Dans la plupart des cas, lorsqu’il s’agit d’un problème, l’UAS n’est suivi que par le biais de [!DNL Google Analytics] ou d’un autre outil d’analyse web. Bien que ces outils puissent s’avérer utiles, le stockage exclusif des UAS présente certains inconvénients. Par exemple, vous ne pouvez pas extraire de données au niveau de l’utilisateur de ces outils. Lorsque cela est possible, il s’agit généralement d’un processus difficile. Il doit être facile d’obtenir ces informations et de les associer à des données provenant d’autres sources, telles que les informations comportementales et transactionnelles également stockées dans votre base de données.

Stocker l’UAS dans votre propre base de données est souvent la plus grande amélioration qu’une entreprise en ligne peut apporter à ses capacités analytiques. Cela permet d’analyser les ventes, l’engagement des utilisateurs, les périodes de récupération, la valeur de durée de vie du client, l’attrition et d’autres mesures critiques par UAS. [Ces données sont essentielles pour décider où investir les ressources marketing](../data-analyst/analysis/most-value-source-channel.md).

Trop d’entreprises se concentrent uniquement sur la recherche de canaux qui proposent de nouveaux utilisateurs au coût le plus bas. Si vous ne suivez pas la qualité des utilisateurs acquis de chaque canal, vous courez le risque d&#39;attirer des utilisateurs qui ne génèrent pas de valeur commerciale.

## Configuration de la table de données

### Définir une clé de Principal

Une [clé primaire](https://en.wikipedia.org/wiki/Unique_key) est une colonne (ou un ensemble de colonnes) immuable qui produit des valeurs uniques dans un tableau. Les clés de Principal sont extrêmement importantes, car elles permettent de s’assurer que vos tables sont correctement répliquées dans [!DNL Commerce Intelligence].

Lors de la création de clés primaires, utilisez un type de données entier pour la colonne qui augmente automatiquement. Adobe recommande d’éviter autant que possible d’utiliser plusieurs clés primaires de colonne.

Si votre table est une vue SQL, ajoutez une colonne qui peut agir comme une clé primaire. [!DNL Commerce Intelligence] peut identifier automatiquement cette colonne en tant que clé primaire.

### Attribuer un type de données à votre colonne de données

Si aucun [type de données](https://en.wikipedia.org/wiki/Data_type) n’est affecté à une colonne de données, [!DNL Commerce Intelligence] devine le type de données à utiliser. Si le système ne procède pas correctement aux estimations, vous ne pourrez peut-être pas effectuer les analyses appropriées tant que l’équipe d’assistance d’Adobe n’aura pas adapté la colonne au type de données approprié. Par exemple, si une colonne de date est estimée comme un type de données numériques, vous pouvez suivre la tendance dans le temps à l’aide de cette dimension de date.

### Ajouter des préfixes à vos tables de données si vous disposez de plusieurs bases de données

Si plusieurs bases de données sont connectées à [!DNL Commerce Intelligence], Adobe vous recommande d&#39;ajouter des préfixes à vos tables afin d&#39;éviter toute confusion. Les préfixes vous permettent de mémoriser l’origine des mesures ou des dimensions de données.
