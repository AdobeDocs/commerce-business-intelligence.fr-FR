---
title: Report Builder de cohortes pour les cohortes non basées sur des dates
description: Découvrez comment regrouper des utilisateurs par une activité ou un attribut similaire.
exl-id: c7b85ce9-113c-4ffc-855f-3d53fe2347d8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 76c5329c3f55570fa4e46601e902dc5a09e319e7
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# [!DNL Cohort Report Builder] pour les cohortes non basées sur des dates

[`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) est un excellent outil pour aider les marchands à étudier le comportement des différents sous-ensembles d’utilisateurs au fil du temps. Dans le passé, le `Cohort Report Builder` a été optimisé pour regrouper les utilisateurs par un `cohort date` commun (par exemple, l’ensemble de tous les clients qui ont effectué leur premier achat au cours d’un mois donné). La fonction `Non-Date Based Cohort` vous donne désormais la possibilité de regrouper les utilisateurs selon une activité ou un attribut similaire. Examinez quelques cas d’utilisation de cette fonctionnalité.

## Cas d’utilisation

Cette liste n’est pas exhaustive, mais voici quelques analyses potentielles qui peuvent être réalisées avec cette fonctionnalité.

* Examiner les recettes des clients acquis de [!DNL Google] par rapport à [!DNL Facebook]
* Analyser les clients dont le premier achat a été effectué aux États-Unis par rapport au Canada
* Examiner le comportement des clients acquis à partir de diverses campagnes publicitaires

## Comment créer votre analyse

1. Cliquez sur **[!UICONTROL Report Builder]** dans l’onglet de gauche ou sur **[!UICONTROL Add Report** > **Create Report]** dans n’importe quel tableau de bord.

1. Dans l’écran `Report Builder Selection`, cliquez sur **[!UICONTROL Create Report]** en regard de l’option `Visual Report Builder` .

### Ajout d’une mesure

Maintenant que vous vous trouvez dans le `Report Builder`, vous ajoutez la mesure sur laquelle vous souhaitez effectuer l’analyse (par exemple : `Revenue` ou `Orders`).

>[!NOTE]
>
>Les mesures [!DNL Google Analytics] natives ne sont pas compatibles avec les `Cohort Report Builder`. L’objectif de cet exemple est d’examiner les recettes au fil du temps pour les clients de premier ordre qui ont été acquis par différentes sources [!DNL Google Analytics].

### Basculer `Metric View` vers `Cohort`

![1-bascule de la mesure vers la cohorte](../../assets/1-toggle-metric-view-to-cohort.png)

Une nouvelle fenêtre s’ouvre, dans laquelle vous pouvez configurer les détails du rapport de cohorte.

Cinq spécifications sont nécessaires pour créer un rapport de cohorte :

1. Comment regrouper les cohortes
1. Sélection de cohortes
1. Horodatage de l’action
1. Période de la première action de la cohorte
1. Période après occurrence de cohorte

![cohort-groups](../../assets/2-cohort-groups.png)<!--{: width="200" height="224"}-->



#### 1. Regroupement `cohorts`

`Cohorts` sont regroupés par une caractéristique de comportement, dans cet exemple `Customer's first order GA source`. Les options disponibles ici sont les colonnes qui sont déjà désignées comme `groupable` pour la mesure.

#### 2. Sélection des cohortes

Vous pouvez afficher tous les résultats de la caractéristique donnée. Comme cela peut entraîner un grand nombre de `cohorts`, vous pouvez sélectionner le `cohorts` spécifique (qui correspond aux différentes valeurs disponibles pour `Customer's first order GA source`) dont vous avez besoin.

![cohort-groups](../../assets/4-cohort-groups.png)<!--{: width="300" height="338"}-->

#### 3. `Action timestamp`

Vous pouvez ainsi choisir une colonne basée sur la date autre que la colonne sur laquelle la mesure est créée. Vous trouverez ci-dessous la sélection de la période qui s’applique au `action timestamp` donné.

#### 4. `Cohort first action time range`

C’est ici que vous sélectionnez la période contenant le `cohorts action timestamp` (c’est pourquoi les clients qui ont passé la première commande de novembre 2017 à octobre 2018). Il peut s’agir d’une période glissante ou d’une période fixe.

#### 5. `Time range after cohort occurrence`

Voulez-vous voir le `cohorts` au fil du temps par mois, semaine ou année ? C&#39;est ici que vous faites ces sélections. Sous cette section, vous allez sélectionner le `time range` une fois que le `cohort action timestamp` a eu lieu. Par exemple, cela vous montre 12 mois de données pour les clients qui ont passé la première commande pendant la période d’action.

![cohort-first-action-time-range](../../assets/5-cohort-first-action-time-range.png)<!--{: width="400" height="557"}-->

>[!NOTE]
>
>[!UICONTROL Filters] appliqué à vos mesures reste intact lorsque vous basculez entre les vues `Standard` et `Cohort`.

### Associé

Voir [`Perspectives`](../../data-analyst/dev-reports/cohort-rpt-bldr.md).
