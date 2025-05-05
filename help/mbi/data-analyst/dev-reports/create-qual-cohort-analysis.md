---
title: Créer une analyse qualitative des cohortes
description: Découvrez ce qu’est une cohorte qualitative, pourquoi vous pourriez être intéressé par la création de cette analyse et comment la créer dans Commerce Intelligence.
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# Créer un `Qualitative Cohort Analysis`

Savez-vous comment vos segments de clients [!DNL Google Adwords] acquis développent leur LTV par rapport aux clients acquis par le référencement organique ? Avez-vous déjà pensé à exécuter une analyse `cohort` sur différents segments de clients côte à côte dans le même rapport ? Si tel est le cas, un `qualitative cohort analysis` vous aide à répondre à ces questions.

Cette rubrique aborde ce qu’est une cohorte qualitative, pourquoi vous pourriez être intéressé par la création de cette analyse et comment la créer dans [!DNL Commerce Intelligence].

## Que sont `qualitative cohorts`, de toute façon ? {#whatare}

L’analyse de `Cohort` en général peut être définie globalement comme l’analyse de groupes d’utilisateurs partageant des caractéristiques similaires au cours de leur cycle de vie. Il vous permet d’identifier les tendances comportementales entre différents groupes d’utilisateurs.

Voir [analyse des cohortes](https://www.cohortanalysis.com/).

La plupart des `cohort` analysent ensemble les utilisateurs du groupe [!DNL Commerce Intelligence] à une date commune (par exemple, l’ensemble de tous les clients qui ont effectué leur premier achat au cours d’un mois donné). Un `qualitative cohort` est un peu différent : il s’agit d’un groupe d’utilisateurs défini par une caractéristique qui n’est pas basée sur le temps. Par exemple :

* Ensemble de tous les utilisateurs acquis à partir d’une campagne publicitaire
* Ensemble de tous les utilisateurs dont le premier achat comprenait un bon (ou ne l’avait pas fait)
* Ensemble de tous les utilisateurs d’un certain âge

## En quoi cela diffère-t-il du créateur `cohort` normal ? {#different}

[`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) est optimisé pour les cohortes de regroupement utilisant une caractéristique basée sur le temps. Cela s’avère particulièrement utile pour les analyses portant sur un segment spécifique d’utilisateurs (par exemple, tous les utilisateurs acquis au moyen d’une campagne de recherche payante). Dans `Cohort Analysis Builder`, vous pouvez (1) vous concentrer sur ce groupe d’utilisateurs spécifique et (2) `cohort` sur une date (comme leur date de première commande).

Cependant, si vous souhaitez analyser le comportement des cohortes de plusieurs segments d’utilisateurs dans le même rapport de cohortes (`paid` par rapport à `organic` recherches par rapport au trafic direct, par exemple ?), cette analyse plus avancée peut être créée dans `Report Builder`.

## Quelles informations dois-je envoyer pour configurer mon analyse ? {#support}

La création d&#39;un rapport `qualitative cohort` dans le `Report Builder` implique que l&#39;équipe d&#39;analystes d&#39;Adobe crée quelques [ colonnes calculées avancées ](../data-warehouse-mgr/creating-calculated-columns.md) sur les tables nécessaires.

Pour les créer, envoyez un [ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) (et reportez-vous à cet article !). Voici ce que vous devez savoir :

* `metric` avec lequel vous souhaitez analyser les cohortes et avec quel tableau il utilise (par exemple : `Revenue`, basé sur la table `orders`).

* `user segments` que vous souhaitez définir et où ces informations se trouvent dans votre base de données (par exemple : différentes valeurs de `User's referral source`, natives de la table `users` et déplacées vers `orders`).

* L’ `cohort date` que vous souhaitez que votre analyse utilise (par exemple : l’horodatage `User's first order date`). Cet exemple nous permet de regarder chaque segment et de demander `How does a user's revenue grow in the months following their first order date?`.

* `time interval` sur lequel vous souhaitez afficher l’analyse (par exemple : `weeks`, `months` ou `quarters` après le `User's first order date`).

Une fois que l’équipe d’analystes d’Adobe a répondu à ce qui précède, vous disposez de deux nouvelles colonnes calculées avancées pour élaborer votre rapport. Vous pouvez ensuite suivre les instructions ci-dessous pour le faire.

## Créer une analyse qualitative des cohortes {#create}

Tout d’abord, vous souhaitez ajouter la mesure qui vous intéresse dans les cohortes, une fois pour chaque `cohort` que vous analysez. Dans cet exemple, vous souhaitez voir le cumul `Revenue` effectué dans les mois suivant la première commande d’un client, segmenté par le `User's referral source`. Cela signifie que, pour chaque segment, vous ajoutez une mesure `Revenue` et filtrez pour le segment spécifique :

![](../../assets/qualcohort1.gif)

Deuxièmement, vous devez apporter deux modifications aux options temporelles du rapport :

1. Définissez le `time interval` sur `None`. Cela est dû au fait que vous finissez par regrouper par intervalle de temps en tant que dimension au lieu d’utiliser les options d’heure habituelles.

1. Définissez le `time range` sur la fenêtre temporelle que vous souhaitez que le rapport couvre.

Dans cet exemple, vous observez une vue `all time` de `Revenue`. Ensuite, vous devez obtenir une série de points :

![](../../assets/qualcohort2.gif)

Troisièmement, vous ajustez pour configurer le `cohorts`. En fonction des `cohort date` et `time interval` que vous avez spécifiés à l’équipe d’Adobe analyste, votre compte comporte une dimension qui effectue la date `cohort`. Dans cet exemple, cette dimension personnalisée est appelée `Months between this order and customer's first order date`. En utilisant cette dimension, vous devez :

* `Group by` la dimension avec l’option `group by`

* Sélectionnez toutes les valeurs de `dimension` qui vous intéressent

* Avec `Show top/bottom option`, sélectionnez les X premiers mois qui vous intéressent et triez selon la dimension `Months between this order and customer's first order date`

Vous pouvez maintenant voir une ligne pour chaque `cohort` que vous avez spécifié. Consultez l’exemple maintenant : vous voyez le `Revenue` fourni par les utilisateurs de chaque source de référence, `grouped by` le nombre de mois entre leur première commande et toute commande ultérieure. L’exemple a également ajouté un `Cumulative perspective` pour afficher la croissance agrégée `cohorts'` : consultez le tableau de résultats pour plus de granularité.

Qu&#39;est-ce que ça nous dit ? Ici, la source de référence spécifique `Paid search` est utile le premier mois de la durée de vie d’achat d’un client, mais ne parvient pas à conserver sa base de clients avec des recettes répétées. Alors que `Direct Traffic` commence à un montant inférieur, les recettes des mois suivants s’accumulent effectivement à un rythme similaire.

Quelle que soit la manière dont vous le découpez, l’analyse `cohort` est un outil puissant dans votre boîte à outils d’analyse. Ce type d’analyse peut donner des insights intéressants sur votre entreprise, qui ne sont pas toujours `time-based cohorts`, ce qui vous permet de prendre de meilleures décisions basées sur les données.
