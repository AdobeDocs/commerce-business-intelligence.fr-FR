---
title: Report Builder de cohorte
description: Découvrez l’analyse des groupes d’utilisateurs qui partagent des caractéristiques similaires au cours de leur cycle de vie.
exl-id: d80c5389-7256-40e0-86e0-49903113f93d
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 0%

---

# Report Builder de cohorte

Avez-vous déjà voulu étudier le comportement des différents sous-ensembles de vos utilisateurs au fil du temps ? Par exemple, vous êtes-vous déjà demandé si les utilisateurs qui s’inscrivent lors d’une période de promotion ont des recettes de durée de vie moyenne plus élevées que ceux qui ne s’y inscrivent pas ? Si la réponse est `Yes`, alors `Cohort Report Builder` est l’outil idéal pour vous. [!DNL Adobe Commerce Intelligence] est optimisé pour effectuer cette analyse et la rendre pertinente pour votre entreprise.

## Qu’est-ce que l’analyse des cohortes ? {#what}

L’analyse de `Cohort` peut être définie globalement comme l’analyse de groupes d’utilisateurs partageant des caractéristiques similaires au cours de leur cycle de vie. Il vous permet d’identifier les tendances comportementales entre différents groupes d’utilisateurs.

Pour une introduction détaillée sur l&#39;analyse `cohort`, consultez [cette page](https://www.cohortanalysis.com/).

Dans votre tableau de bord [!DNL Commerce Intelligence], il est facile de créer l’utilisateur `cohorts` en fonction d’une date `cohort` et d’une mesure dans votre compte.

## Pourquoi l’analyse des cohortes est-elle importante ? {#important}

Comme mentionné ci-dessus, l’analyse `cohort` vous permet d’identifier les tendances comportementales entre différents groupes d’utilisateurs. Grâce à une solide compréhension du comportement de certains groupes, vous pouvez personnaliser vos décisions et vos dépenses afin d’optimiser vos ventes. Par exemple, prenez une analyse de recettes `cohort` sur toute une vie. Bien que ce type d’analyse soit bénéfique pour de nombreuses raisons, l’analyse immédiate est de meilleures décisions d’acquisition client.

## Comment créer ma propre analyse `cohort` ?

### Nouvelle architecture

Voici les instructions d’utilisation de `Cohort Report Builder` sur la [Nouvelle architecture](../../administrator/account-management/new-architecture.md).

1. Cliquez sur **[!UICONTROL Report Builder]** dans l’onglet de gauche ou sur **[!UICONTROL Add Report** > **Create Report]** dans n’importe quel tableau de bord.

1. Dans l&#39;écran de sélection `Report Builder`, cliquez sur **[!UICONTROL Create Report]** en regard de l&#39;option `Visual Report Builder` .

**Ajout d’une mesure**

Maintenant que vous vous trouvez dans le `Report Builder`, ajoutez la mesure sur laquelle vous souhaitez effectuer l’analyse (par exemple : `Revenue` ou `Orders`).

>[!NOTE]
>
>Les mesures [!DNL Google Analytics] natives ne sont pas compatibles avec les `Cohort Report Builder`.

**Basculer la vue de mesure vers`Cohort`**

![](../../assets/visual-report-builder-cohort-toggle.png)

Une nouvelle fenêtre s’ouvre alors pour configurer les détails du rapport `Cohort`.

### Cinq spécifications sont nécessaires pour créer un rapport `Cohort` :

1. Comment regrouper les `cohorts`
1. Période `cohort`
1. Nombre de `cohorts` à afficher
1. La quantité minimale de données que chaque `cohort` doit contenir
1. Période après l’occurrence `cohort`

#### 1. Regroupement `cohorts`

`Cohorts` sont regroupés par horodatage, comme **date d&#39;enregistrement** ou **date de première commande**.

>[!NOTE]
>
>Vous ne pouvez pas utiliser le même horodatage que celui utilisé par la mesure pour la date `cohort`. Pour une analyse qui requiert cela, vous pouvez utiliser `Standard report builder` à la place.

#### 2. `Cohort` sur une période

Choisissez la période par laquelle regrouper `cohorts`. En d’autres termes, quelle partie de l’horodatage que vous avez sélectionnée ci-dessus est la plus importante : `week`, `month`, `quarter` ou `year` ? Votre rapport affiche les données dans l’intervalle que vous sélectionnez ici

#### 3. et 4. Définissez le nombre de `cohorts` à afficher et la quantité de données que chaque `cohort` doit avoir.

Ces paramètres vous aident à afficher uniquement le `cohorts` qui vous intéresse et la zone pratique `Preview` située en bas de la fenêtre vous indique exactement les cohortes affichées dans votre rapport.

Par défaut, le `cohort` actif n&#39;est pas inclus, sauf si vous modifiez la quantité minimale de données requise pour chaque `cohort` en `0`. Dans ce cas, le `cohort` de la période actuelle ne comprend que des données partielles.

#### 5. Période après `Cohort` occurrence

Cette fonctionnalité vous permet de définir la période des données que vous affichez pour le `cohorts` sélectionné. Par exemple, si vous souhaitez afficher 24 `cohorts` mensuels sur la base de `customer's first order date`, mais que vous n’êtes intéressé que par les 3 premiers mois de données pour chaque `cohort`, vous pouvez définir `number of cohorts to view` sur `24` et `time range after cohort occurrence` sur `3`.

L’intervalle de cette valeur change avec ce que vous avez sélectionné dans `cohort time period` et la valeur est définie sur `12` par défaut ; la valeur ne change pas, sauf si vous cliquez sur l’icône de calendrier pour la modifier.

![](../../assets/cohort-time-range.png)

#### Autres notes

* [!UICONTROL Filters] : les mesures appliquées restent intactes lorsque vous permutez entre les vues `Standard` et `Cohort`.

* Voir [`Perspectives`](#perspectives).

#### Exemple

Voici un exemple pour tout rassembler. Dans cet exemple, je veux vérifier le comportement de la commande après le premier achat de `cohort` pour voir si cette cohorte revient pour effectuer des achats répétés dans les six prochains mois.

![Cohorte des commandes](../../assets/crb_example.gif)

### Architecture héritée

#### Architecture héritée {#personalinfo}

Vous trouverez ci-dessous des instructions spécifiques à la version héritée de `Cohort Report Builder`. Si vous souhaitez utiliser la nouvelle version, consultez la section [Nouvelle architecture](../../administrator/account-management/new-architecture.md) pour plus d’informations sur la migration vers un compte [!DNL Commerce Intelligence] Nouvelle architecture.

#### Comment créer ma propre analyse `cohort` ? {#create}

![](../../assets/create-cohort-analysis.png)

`Cohort` analyse en action ! Vous pouvez constater ici que les recettes augmentent au fil du temps de manière cumulée et par utilisateur.

Cette section vous guide tout au long de la création de votre propre analyse `cohort`. Pour obtenir des exemples (et des GIFs animés présentant le processus), consultez la [section Exemples](#examples) de cette rubrique.

1. Cliquez sur **[!UICONTROL Report Builder]** dans l’onglet de gauche ou sur **[!UICONTROL Add Report** > **Create Report]** dans n’importe quel tableau de bord.

1. Dans l’écran `Report Builder Selection`, cliquez sur **[!UICONTROL Create Report]** en regard de l’option `Cohort Analysis` .

#### Ajout d’une mesure

Maintenant que vous vous trouvez dans le `Cohort Report Builder`, ajoutez la mesure (exemple : `Revenue` ou `Number of orders`) sur laquelle vous souhaitez effectuer l’analyse.

>[!NOTE]
>
>Les mesures [!DNL Google Analytics] natives ne sont pas compatibles avec les `Cohort Report Builder`.

#### Sélection de la date de cohorte {#date}

L’étape suivante consiste à spécifier le `cohort date`. Il s’agit de la date à laquelle vos utilisateurs sont regroupés. Par exemple, il peut s’agir de `User's first order date` ou `User's registration date`.

>[!NOTE]
>
>Vous ne pouvez pas utiliser la même date que celle sur laquelle la mesure est créée (par exemple : `created at`) que la `cohort date`.

#### Définition de l’intervalle et de la période

Définissez ensuite les `Interval` et `Time Period`.

`Interval`
L’option `Interval` vous permet de définir le `length` de votre `cohorts`. Si, par exemple, cette valeur est définie sur `Month`, votre rapport est mesuré en mois.

Vous pouvez modifier l’affichage de ces intervalles sur l’axe X à l’aide du menu **Durée** .

`Time Period`
Utilisez le menu `Time Period` pour choisir l’utilisateur spécifique `cohorts` à analyser. Vous pouvez afficher chaque `cohort`, effectuer une sélection dans une liste, définir une période ou définir une plage de temps variable `cohorts` à inclure. Par exemple, si vous avez utilisé l’option `Specific Cohorts`, vous pouvez sélectionner des mois spécifiques à inclure dans l’analyse :

![Utilisation du menu `Time Period` pour ajouter le `Cohorts`](../../assets/Cohort_Time_Period.gif) spécifique

Si vous vous groupez `cohorts` par date d’enregistrement, puis sélectionnez avril, mai et juin dans la liste `Specific Cohorts`, tous les utilisateurs enregistrés dans ces mois seront inclus.

#### Définir l&#39;axe des X

Sous `duration`, vous pouvez définir les paramètres de l’axe X du graphique. C’est-à-dire le nombre de périodes représentées par chaque point de données et le nombre de points de données à inclure dans l’analyse.

#### Sélectionner la table `counting members`

Si vous avez choisi de regrouper des utilisateurs par un `cohort date` qui a été joint à une autre table, vous pouvez voir une option `counting members in the … table` .

![](../../assets/Cohort_Counting_Members_option.png)

Consultez un exemple pour comprendre ce paramètre. Supposons que vous ayez créé une cohorte de rapports pour une mesure `Revenue` par `Customer's registration date`. Vous vouliez également utiliser la perspective `Average value per cohort member` pour visualiser les recettes par acheteur au fil du temps. Pour trouver la valeur moyenne par acheteur, vous devez décider du nombre d&#39;acheteurs à diviser. S&#39;agit-il du nombre de clients enregistrés dans votre table `customers` ou du nombre d&#39;acheteurs distincts dans votre `orders table` pour la même période ?

Ce paramètre répond à cette question. Le décompte des membres dans la table `customers` inclut tous les clients (qu&#39;ils aient effectué un achat ou non) en moyenne. Le décompte des membres dans la table `orders` inclut uniquement les clients qui ont effectué un achat.

#### Sélectionner une perspective {#perspective}

Après avoir défini la mesure et la manière dont vous souhaitez l’analyser, vous pouvez sélectionner le `perspective` à utiliser.

Juste au-dessus de la visualisation du rapport se trouve une liste déroulante de paramètres `perspective`.

Voir [Perspectives](#perspectives).

![](../../assets/Cohort_Perspective_Menu.png)

## Exemples d’analyse des cohortes {#examples}

Maintenant que vous avez compris comment créer une analyse `cohort`, consultez quelques exemples.

### Je veux savoir comment mon utilisateur `cohorts` se développe au fil du temps.

![L&#39;utilisateur `cohorts` grandit au fil du temps](../../assets/cohort1.gif)

Dans cet exemple, vous avez analysé la mesure `Revenue`, regroupé vos cohortes par `customer's first order date` et sélectionné les 8 plus récents `cohorts` (définis dans le menu `Time Period`) à inclure dans l’analyse. Pour voir comment les cohortes se sont développées au fil du temps, vous avez utilisé le `Cumulative Average Value per Cohort Member` `perspective`.

### Je veux savoir, en moyenne, combien de commandes un utilisateur effectue à différents moments de sa vie.

(../../assets/cohort2.gif

Pour cet exemple, vous avez analysé la mesure `Number of orders`, regroupé vos cohortes par `customer's first order date` et inclus les huit cohortes les plus récentes (définies dans le menu `Time Period`) dans l’analyse. Pour afficher le nombre moyen de commandes pour chaque cohorte, vous avez remplacé `perspective` par `Average Value per Cohort Member`.

### Je veux comparer l’activité d’achat future d’un utilisateur à l’activité de son premier mois avec celle de l’entreprise.

![Comparaison de l’activité d’achat future d’un utilisateur avec son premier mois d’activité](../../assets/cohort3.gif)

## `Perspectives` {#perspectives}

`Standard`
Cela indique la contribution incrémentielle d’un groupe de cohortes donné à un moment donné de leur cycle de vie. (exemple : le point &quot;Semaine 6&quot; affiche tous les points de données effectués par les utilisateurs au cours de leur sixième semaine.)

`Average Value per Cohort Member`
Cela divise l’analyse `Standard cohort` dans (1) par le nombre d’utilisateurs dans chaque groupe `cohort`. Cela peut s’avérer utile pour comparer les performances des cohortes d’après les pommes, car tous les groupes de cohortes ne peuvent pas inclure le même nombre d’utilisateurs. Par exemple, le chiffre d’affaires moyen pour la semaine 6 par utilisateur d’un certain `cohort`.

`Cumulative`
Ce `perspective` affiche l’analyse `cohort` traditionnelle sur une base `cumulative`. En d’autres termes, il montre la contribution totale d’une cohorte donnée à ce jour à un moment donné de son cycle de vie. Par exemple, les recettes cumulées après six semaines d’utilisateurs provenant d’une certaine cohorte.

`Cumulative Average Value per Cohort Member`
Cela divise l’analyse `Cumulative` dans (3) par le nombre d’utilisateurs dans chaque groupe `cohort`. Il indique la contribution de durée de vie moyenne (souvent les recettes de durée de vie moyenne) par membre `cohort` à chaque période de la vie `cohort's`. Par exemple, les recettes de durée de vie moyenne après six mois d’utilisateurs ayant rejoint le site en juin.

`Percent of First Value (show first value)`
Cela analyse la contribution agrégée `cohort` à un moment spécifique dans un cycle de vie `cohort's` en tant que pourcentage de leur contribution dans la première période. Par exemple, les recettes du mois 6 divisées par les recettes du mois 1 des utilisateurs qui ont rejoint le mois de juin.

`Percent of First Value (hide first value)`
Il s’agit de la même valeur que le `perspective` ci-dessus, sauf que la première valeur de période de 100 % est masquée.

## Remplissage {#finish}

`Cohort Report Builder` est optimisé pour regrouper les utilisateurs par un `cohort date` commun. Il peut être intéressant de regrouper les utilisateurs selon une activité ou un attribut similaire. Adobe recommande de consulter [ce tutoriel sur les cohortes qualitatives](../dev-reports/create-qual-cohort-analysis.md) pour commencer.
