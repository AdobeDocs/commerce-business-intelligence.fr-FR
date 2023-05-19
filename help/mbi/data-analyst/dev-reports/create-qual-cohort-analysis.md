---
title: Créer une analyse qualitative des cohortes
description: Découvrez ce qu’est une cohorte qualitative, pourquoi vous pourriez être intéressé par la création de cette analyse et comment la créer dans Commerce Intelligence.
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# Créez un `Qualitative Cohort Analysis`

Sais-tu comment ta [!DNL Google Adwords]Les segments de clients acquis développent leur LTV par rapport aux clients acquis par le référencement organique ? Avez-vous déjà pensé à exécuter une `cohort` analyse côte à côte sur différents segments de clients dans le même rapport ? Si tel est le cas, une `qualitative cohort analysis` vous aide à répondre à ces questions.

Cette rubrique aborde ce qu’est une cohorte qualitative, pourquoi vous pourriez être intéressé par la création de cette analyse et comment la créer dans [!DNL Commerce Intelligence].

## Quels éléments ? `qualitative cohorts`De toute façon ? {#whatare}

`Cohort` L’analyse en général peut être définie de manière générale comme l’analyse de groupes d’utilisateurs partageant des caractéristiques similaires au cours de leur cycle de vie. Il vous permet d’identifier les tendances comportementales entre différents groupes d’utilisateurs.

Voir [analyse des cohortes](https://www.cohortanalysis.com/).

Le plus `cohort` analyses dans [!DNL Commerce Intelligence] regrouper les utilisateurs par une date commune (par exemple, l’ensemble de tous les clients qui ont effectué leur premier achat au cours d’un mois donné). A `qualitative cohort` est légèrement différent : il s’agit d’un groupe d’utilisateurs défini par une caractéristique qui n’est pas temporelle. Par exemple :

* Ensemble de tous les utilisateurs acquis à partir d’une campagne publicitaire
* Ensemble de tous les utilisateurs dont le premier achat comprenait un bon (ou ne l’avait pas fait)
* Ensemble de tous les utilisateurs d’un certain âge

## En quoi cela diffère-t-il de la normale `cohort` builder ? {#different}

Le [`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) est optimisée pour les cohortes de regroupement utilisant une caractéristique temporelle. Cela s’avère particulièrement utile pour les analyses portant sur un segment spécifique d’utilisateurs (par exemple, tous les utilisateurs acquis au moyen d’une campagne de recherche payante). Dans le `Cohort Analysis Builder`, vous pouvez (1) vous concentrer sur ce groupe d’utilisateurs spécifique, et (2) `cohort` à une date (comme leur date de première commande).

Cependant, si vous souhaitez analyser le comportement des cohortes de plusieurs segments d’utilisateurs dans le même rapport de cohorte (`paid` recherche et `organic` Rechercher par rapport au trafic direct, par exemple ?), cette analyse plus avancée peut être créée dans la variable `Report Builder`.

## Quelles informations dois-je envoyer pour configurer mon analyse ? {#support}

Création d’un `qualitative cohort` dans le rapport `Report Builder` implique la création d’une équipe d’analystes d’Adobe. [colonnes calculées avancées](../data-warehouse-mgr/creating-calculated-columns.md) sur les tables nécessaires.

Pour les créer, envoyez une [ticket de support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) (et reportez-vous à cet article !). Voici ce que vous devez savoir :

* Le `metric` vous souhaitez exécuter l’analyse des cohortes avec et avec le tableau qu’elle utilise (par exemple : `Revenue`, reposant sur la variable `orders` ).

* Le `user segments` vous souhaitez définir et où ces informations se trouvent dans votre base de données (par exemple : différentes valeurs de `User's referral source`, natif de la fonction `users` et déplacé vers le `orders`).

* Le `cohort date` vous souhaitez que votre analyse utilise (par exemple : la valeur `User's first order date` horodatage). Cet exemple nous permet de consulter chaque segment et de demander : `How does a user's revenue grow in the months following their first order date?`.

* Le `time interval` sur lequel vous souhaitez afficher l’analyse (par exemple : `weeks`, `months`ou `quarters` après la `User's first order date`).

Une fois que l’équipe d’analystes d’Adobe a répondu à ce qui précède, vous disposez de deux nouvelles colonnes calculées avancées pour élaborer votre rapport. Vous pouvez ensuite suivre les instructions ci-dessous pour le faire.

## Créer une analyse qualitative des cohortes {#create}

Tout d’abord, vous souhaitez ajouter la mesure qui vous intéresse dans les cohortes, une fois pour chaque `cohort` vous analysez. Dans cet exemple, vous souhaitez afficher les `Revenue` effectuées dans les mois suivant la première commande d’un client, segmentées par la variable `User's referral source`. Cela signifie que, pour chaque segment, vous en ajoutez un. `Revenue` et filtrer pour le segment spécifique :

![](../../assets/qualcohort1.gif)

Deuxièmement, vous devez apporter deux modifications aux options temporelles du rapport :

1. Définissez la variable `time interval` to `None`. Cela est dû au fait que vous finissez par regrouper par intervalle de temps en tant que dimension au lieu d’utiliser les options d’heure habituelles.

1. Définissez la variable `time range` dans la fenêtre de temps que vous souhaitez que le rapport couvre.

Dans cet exemple, vous pouvez consulter un `all time` vue `Revenue`. Ensuite, vous devez obtenir une série de points :

![](../../assets/qualcohort2.gif)

Troisièmement, vous ajustez pour configurer la variable `cohorts`. Selon la variable `cohort date` et `time interval` que vous avez spécifié à l’équipe d’analystes d’Adobe, votre compte contient une dimension qui exécute la variable `cohort` dater. Dans cet exemple, cette dimension personnalisée est appelée `Months between this order and customer's first order date`. En utilisant cette dimension, vous devez :

* `Group by` la dimension avec la variable `group by` option

* Sélectionnez toutes les valeurs de la variable `dimension` dans laquelle vous êtes intéressé

* Avec le `Show top/bottom option`, sélectionnez les X premiers mois qui vous intéressent et triez selon le `Months between this order and customer's first order date` dimension

Vous pouvez maintenant voir une ligne pour chaque `cohort` que vous avez spécifié. Consultez l’exemple maintenant — vous voyez le `Revenue` fournies par les utilisateurs de chaque source de référence, `grouped by` le nombre de mois entre leur première commande et toute commande ultérieure. L’exemple a également ajouté une `Cumulative perspective` pour afficher la variable `cohorts'` croissance agrégée : consultez le tableau des résultats pour plus de granularité.

Qu&#39;est-ce que ça nous dit ? Ici, la source de référence spécifique `Paid search` est utile pendant le premier mois de la durée de vie d’achat d’un client, mais ne parvient pas à conserver sa base de clients avec des recettes répétées. while `Direct Traffic` Les recettes des mois suivants commencent à s’accumuler à un rythme semblable.

Peu importe comment vous le découpez, `cohort` l’analyse est un outil puissant dans votre boîte à outils d’analyse. Ce type d’analyse peut donner des informations intéressantes sur votre entreprise, que les `time-based cohorts` peut ne pas être le cas, ce qui vous permet de prendre de meilleures décisions basées sur les données.
