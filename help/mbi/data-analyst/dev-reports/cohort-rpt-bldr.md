---
title: Report Builder de cohorte
description: Découvrez l’analyse des groupes d’utilisateurs qui partagent des caractéristiques similaires tout au long de leurs cycles de vie.
exl-id: d80c5389-7256-40e0-86e0-49903113f93d
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 736dbdc3ea6bc8b7c852f06110705765f040c31f
workflow-type: tm+mt
source-wordcount: '1597'
ht-degree: 0%

---

# Report Builder de cohorte

Avez-vous déjà voulu étudier le comportement des différents sous-ensembles de vos utilisateurs au fil du temps ? Par exemple, vous êtes-vous déjà demandé si les utilisateurs qui s’inscrivent pendant une période de promotion ont un chiffre d’affaires moyen sur toute leur vie plus élevé que ceux qui ne s’inscrivent pas ? Si la réponse est `Yes`, alors le `Cohort Report Builder` est l&#39;outil parfait pour vous. [!DNL Adobe Commerce Intelligence] est optimisé pour effectuer cette analyse et la rendre pertinente pour votre entreprise.

## Qu’est-ce que l’analyse des cohortes ? {#what}

L’analyse des `Cohort` peut être définie de manière large comme l’analyse de groupes d’utilisateurs qui partagent des caractéristiques similaires tout au long de leur cycle de vie. Il vous permet d’identifier les tendances comportementales parmi différents groupes d’utilisateurs.

Dans votre tableau de bord [!DNL Commerce Intelligence], il est facile de créer des `cohorts` utilisateur en fonction d’une date de `cohort` et d’une mesure dans votre compte.

## Pourquoi l’analyse des cohortes est-elle importante ? {#important}

Comme mentionné ci-dessus, l’analyse des `cohort` vous permet d’identifier les tendances comportementales parmi différents groupes d’utilisateurs. Grâce à une solide compréhension du comportement de certains groupes, vous pouvez adapter vos décisions et vos dépenses afin de maximiser vos ventes. Prenons l&#39;exemple d&#39;une analyse des `cohort` de revenus à vie. Bien que ce type d&#39;analyse soit bénéfique pour de nombreuses raisons, la plus immédiate est celle qui permet de prendre de meilleures décisions d&#39;acquisition de clients.

## Comment créer ma propre analyse de `cohort` ?

### Nouvelle architecture

Voici les instructions d’utilisation du `Cohort Report Builder` sur la [nouvelle architecture](../../administrator/account-management/new-architecture.md).

1. Cliquez sur **[!UICONTROL Report Builder]** dans l’onglet de gauche ou **[!UICONTROL Add Report** > **Create Report]** dans n’importe quel tableau de bord.

1. Dans l’écran de sélection des `Report Builder`, cliquez sur **[!UICONTROL Create Report]** en regard de l’option `Visual Report Builder` .

**Ajouter une mesure**

Maintenant que vous êtes dans la `Report Builder`, ajoutez la mesure sur laquelle vous souhaitez effectuer l’analyse (par exemple : `Revenue` ou `Orders`).

>[!NOTE]
>
>Les mesures de [!DNL Google Analytics] natives ne sont pas compatibles avec le `Cohort Report Builder`.

**Activer/désactiver la vue de mesure pour`Cohort`**

![Visual Report Builder affiche l’option de basculement de l’analyse des cohortes](../../assets/visual-report-builder-cohort-toggle.png)

Une nouvelle fenêtre s’ouvre alors pour configurer les détails du rapport `Cohort`.

### Cinq spécifications sont nécessaires pour créer un rapport `Cohort` :

1. Comment regrouper les `cohorts`
1. La période de `cohort`
1. Nombre de `cohorts` à afficher
1. La quantité minimale de données que chaque `cohort` doit contenir
1. Période après `cohort` occurrence

#### &#x200B;1. `cohorts` de regroupement

Les `Cohorts` sont regroupées par horodatage, comme **date d’enregistrement** ou **date de première commande**.

>[!NOTE]
>
>Vous ne pouvez pas utiliser le même horodatage que celui sur lequel la mesure est basée pour la date `cohort`. Pour une analyse qui le requiert, vous pouvez utiliser l’`Standard report builder` à la place.

#### &#x200B;2. Période de `Cohort`

Choisissez la période par laquelle regrouper les `cohorts`. En d’autres termes, quelle partie de l’horodatage que vous avez sélectionné ci-dessus est la plus importante : le `week`, le `month`, le `quarter` ou le `year` ? Votre rapport affiche les données dans l’intervalle que vous sélectionnez ici

#### &#x200B;3. et 4. Définissez le nombre de `cohorts` à afficher et la quantité de données dont chaque `cohort` doit disposer

Ces paramètres vous aident à n’afficher que les `cohorts` qui vous intéressent. En outre, la zone de `Preview` pratique située au bas de la fenêtre indique exactement les cohortes affichées dans votre rapport.

Par défaut, la `cohort` actuelle n’est pas incluse, sauf si vous modifiez la quantité minimale de données requise pour chaque `cohort` à `0`. Dans ce cas, les `cohort` de la période en cours ne contiennent que des données partielles.

#### &#x200B;5. Période Après `Cohort` Occurrence

Cette fonctionnalité vous permet de définir la période des données que vous affichez pour la `cohorts` sélectionnée. Par exemple, si vous souhaitez afficher 24 `cohorts` mensuelles basées sur `customer's first order date`, mais que vous ne vous intéressez qu’aux 3 premiers mois de données pour chaque `cohort`, vous pouvez définir la `number of cohorts to view` sur `24` et la `time range after cohort occurrence` sur `3`.

L’intervalle pour cette valeur change en fonction de ce que vous avez sélectionné dans le `cohort time period` et la valeur est définie sur `12` par défaut ; la valeur ne change pas, sauf si vous cliquez sur l’icône de calendrier pour la modifier.

![Sélecteur de période de cohorte affichant les options de date](../../assets/cohort-time-range.png)

#### Autres notes

* [!UICONTROL Filters] : les mesures appliquées à restent intactes lorsque vous basculez entre les vues `Standard` et `Cohort`.

* Voir [`Perspectives`](#perspectives).

#### Exemple

Voici un exemple pour assembler l’ensemble. Dans cet exemple, je souhaite vérifier le comportement de la commande après le premier achat d’un `cohort` pour voir si cette cohorte revient pour effectuer des achats répétés au cours des six prochains mois.

![cohorte Commandes](../../assets/crb_example.gif)

### Architecture héritée

#### Architecture héritée {#personalinfo}

Vous trouverez ci-dessous des instructions spécifiques à l’ancienne version du `Cohort Report Builder`. Si vous souhaitez utiliser la nouvelle version, consultez [Nouvelle architecture](../../administrator/account-management/new-architecture.md) pour plus d’informations sur la migration vers un compte [!DNL Commerce Intelligence] Nouvelle architecture.

#### Comment créer ma propre analyse de `cohort` ? {#create}

![Boîte de dialogue Créer une analyse des cohortes avec les options de configuration](../../assets/create-cohort-analysis.png)

`Cohort` l’analyse en action ! Ici, vous pouvez voir le chiffre d’affaires augmenter au fil du temps sur une base cumulative et par utilisateur.

Cette section vous guide tout au long de la création de votre propre analyse `cohort`. Pour obtenir des exemples (et des GIF animés présentant le processus), consultez la [section Exemples](#examples) de cette rubrique.

1. Cliquez sur **[!UICONTROL Report Builder]** dans l’onglet de gauche ou **[!UICONTROL Add Report** > **Create Report]** dans n’importe quel tableau de bord.

1. Dans l’écran `Report Builder Selection`, cliquez sur **[!UICONTROL Create Report]** en regard de l’option `Cohort Analysis` .

#### Ajout d’une mesure

Maintenant que vous êtes dans le `Cohort Report Builder`, ajoutez la mesure (par exemple : `Revenue` ou `Number of orders`) sur laquelle vous souhaitez effectuer l’analyse.

>[!NOTE]
>
>Les mesures de [!DNL Google Analytics] natives ne sont pas compatibles avec le `Cohort Report Builder`.

#### Sélectionner la date de cohorte {#date}

L’étape suivante consiste à spécifier le `cohort date` . Il s’agit de la date à laquelle vos utilisateurs sont regroupés. Par exemple, il peut s’agir de `User's first order date` ou `User's registration date`.

>[!NOTE]
>
>Vous ne pouvez pas utiliser la même date sur laquelle la mesure est créée (exemple : `created at`) que la `cohort date`.

#### Définition de l’intervalle et de la période

Ensuite, définissez les `Interval` et `Time Period`.

`Interval`
L’option `Interval` vous permet de définir la `length` de votre `cohorts`. Par exemple, si cette valeur est définie sur `Month`, votre rapport est mesuré en mois.

Vous pouvez modifier l’affichage de ces intervalles sur l’axe X à l’aide du menu **Durée**.

`Time Period`
Utilisez le menu `Time Period` pour choisir l’`cohorts` utilisateur spécifique à analyser. Vous pouvez afficher chaque `cohort`, effectuer un choix dans une liste, spécifier une période ou définir une période variable de `cohorts` à inclure. Par exemple, si vous avez utilisé l’option `Specific Cohorts` , vous pouvez sélectionner des mois spécifiques à inclure dans l’analyse :

![Utilisation du menu `Time Period` pour ajouter des `Cohorts`](../../assets/Cohort_Time_Period.gif) spécifiques

Si vous effectuez un regroupement `cohorts` par date d’enregistrement, puis que vous sélectionnez les mois d’avril, de mai et de juin dans la liste des `Specific Cohorts`, tous les utilisateurs enregistrés au cours de ces mois sont inclus.

#### Définir l’axe X

Sous `duration`, vous pouvez définir les paramètres de l’axe X du graphique. C’est-à-dire le nombre de périodes représentées par chaque point de données et le nombre de points de données à inclure dans l’analyse.

#### Choisir la table des `counting members`

Si vous avez choisi de regrouper les utilisateurs en fonction d&#39;une `cohort date` qui a été jointe à partir d&#39;une autre table, une option `counting members in the … table` peut s&#39;afficher.

![Option Membres du comptage de cohortes affichant les modes indépendants ou cumulés](../../assets/Cohort_Counting_Members_option.png)

Examinez un exemple pour comprendre ce paramètre. Supposons que vous ayez créé un rapport qui cohorte une mesure `Revenue` par `Customer's registration date`. Vous vouliez également utiliser le `Average value per cohort member` de perspective pour voir le chiffre d’affaires par acheteur au fil du temps. Pour trouver la valeur moyenne par acheteur, vous devez décider du nombre d&#39;acheteurs à diviser. S&#39;agit-il du nombre de clients inscrits dans votre tableau de `customers` ou du nombre d&#39;acheteurs distincts dans votre `orders table` pour la même période?

Ce paramètre répond à cette question. Le comptage des membres dans le tableau `customers` inclut tous les clients (qu’ils aient effectué ou non un achat) dans la moyenne. Le comptage des membres dans le tableau `orders` comprend uniquement les clients qui ont effectué un achat.

#### Sélectionner une perspective {#perspective}

Après avoir défini la mesure et la manière dont vous souhaitez l’analyser, vous pouvez sélectionner la `perspective` à utiliser.

Juste au-dessus de la visualisation du rapport se trouve une liste déroulante des paramètres de `perspective`.

Voir [&#x200B; Perspectives &#x200B;](#perspectives).

![Menu Cohorte en perspective présentant différentes options d’affichage](../../assets/Cohort_Perspective_Menu.png)

## Exemples d’analyse des cohortes {#examples}

Maintenant que vous avez passé en revue la création d’une analyse de `cohort`, regardez quelques exemples.

### Je veux savoir comment mes `cohorts` d’utilisateurs évoluent au fil du temps.

![L’`cohorts` utilisateur augmente au fil du temps](../../assets/cohort1.gif)

Dans cet exemple, vous avez analysé la mesure `Revenue`, regroupé vos cohortes par `customer's first order date` et sélectionné les 8 `cohorts` les plus récentes (définies dans le menu `Time Period`) à inclure dans l’analyse. Pour voir comment les cohortes ont augmenté au fil du temps, vous avez utilisé la `Cumulative Average Value per Cohort Member` `perspective`.

### Je veux savoir, en moyenne, combien de commandes un utilisateur passe à différents moments de sa vie.

(../../assets/cohort2.gif

Pour cet exemple, vous avez analysé la mesure `Number of orders`, regroupé vos cohortes par `customer's first order date` et inclus les huit cohortes les plus récentes (définies dans le menu `Time Period`) dans l’analyse. Pour afficher le nombre moyen de commandes pour chaque cohorte, vous avez modifié la `perspective` en `Average Value per Cohort Member`.

### Je veux comprendre comment l&#39;activité d&#39;achat future d&#39;un utilisateur se compare à son activité du premier mois avec l&#39;entreprise.

![Comparaison de l’activité d’achat future d’un utilisateur à son premier mois d’activité](../../assets/cohort3.gif)

## `Perspectives` {#perspectives}

`Standard`
Cela montre la contribution incrémentielle d’un groupe de cohortes donné à un moment donné de son cycle de vie. (exemple : le point « Semaine 6 » affiche tous les points de données créés par les utilisateurs au cours de leur sixième semaine.)

`Average Value per Cohort Member`
Cette opération divise l’analyse de `Standard cohort` dans (1) par le nombre d’utilisateurs dans chaque groupe de `cohort`. Cela peut s’avérer utile pour comparer les performances des cohortes de pommes à pommes, car tous les groupes de cohortes peuvent ne pas inclure le même nombre d’utilisateurs. Par exemple, le chiffre d’affaires moyen de la semaine 6 par utilisateur d’une certaine `cohort`.

`Cumulative`
Cette `perspective` présente l’analyse `cohort` traditionnelle sur une base `cumulative`. En d’autres termes, il indique la contribution totale d’une cohorte donnée à ce jour à un moment donné de son cycle de vie. Par exemple, le chiffre d’affaires cumulé après six semaines d’utilisateurs d’une certaine cohorte.

`Cumulative Average Value per Cohort Member`
Cette opération divise l’analyse de `Cumulative` en (3) par le nombre d’utilisateurs dans chaque groupe de `cohort`. Il indique la contribution moyenne sur toute la durée de vie (souvent le revenu moyen sur toute la durée de vie) par membre `cohort` à chaque période de la vie `cohort's`. Par exemple, le chiffre d’affaires moyen à vie après six mois d’utilisateurs ayant rejoint l’équipe en juin.

`Percent of First Value (show first value)`
Cette méthode analyse la contribution `cohort` agrégée à un moment spécifique d&#39;un cycle de vie `cohort's` en pourcentage de leur contribution au cours de la première période. Par exemple, le chiffre d’affaires du mois 6 divisé par le chiffre d’affaires du mois 1 des utilisateurs qui se sont inscrits en juin.

`Percent of First Value (hide first value)`
Il s’agit du même élément que la `perspective` ci-dessus, sauf que la valeur de la première période de 100 % est masquée.

## Conclusion {#finish}

Le `Cohort Report Builder` est optimisé pour regrouper les utilisateurs selon un `cohort date` commun. Il se peut que vous souhaitiez regrouper les utilisateurs par activité ou attribut similaire. Adobe recommande de consulter [ce tutoriel sur les cohortes qualitatives](../dev-reports/create-qual-cohort-analysis.md) pour commencer.
