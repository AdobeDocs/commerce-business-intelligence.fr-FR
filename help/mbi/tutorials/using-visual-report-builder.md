---
title: Utilisation de Visual Report Builder
description: Découvrez comment analyser les données de votre rapport pour une période spécifique.
exl-id: da97b63d-63f0-4fd6-87e3-4cac49a42acc
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# Utiliser le [!DNL Visual Report Builder]

Le [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md) vous permet d’explorer visuellement vos données afin d’obtenir des informations et d’aider à la prise de décisions commerciales. Ce tutoriel vous guide tout au long du processus de création d’un rapport de base.

>[!NOTE]
>
>Pour ajouter un rapport à un tableau de bord, vous devez disposer d’`Standard` [autorisations utilisateur](../administrator/user-management/user-management.md) et d’un accès `Edit` au tableau de bord.

## Etape 1 : création d&#39;un rapport

Pour commencer à créer un rapport, cliquez sur **[!UICONTROL Report Builder]** dans la barre latérale ou **[!UICONTROL Add Report]** en haut d’un tableau de bord. Lorsque la page `Report Builder` s’affiche, cliquez sur l’option **[!UICONTROL Visual Report Builder]** .

Pour modifier un rapport créé dans le [!DNL Visual Report Builder], cliquez sur l’icône en forme d’engrenage (Options) dans le coin supérieur droit d’un graphique, puis cliquez sur **[!UICONTROL Edit]**.

## Étape 2 : Ajouter des mesures

La première étape de la création d’une analyse consiste à sélectionner [la mesure](../data-user/reports/ess-manage-data-metrics.md) à analyser. Bien que les mesures soient répertoriées par ordre alphabétique par défaut, vous pouvez également les regrouper selon le tableau qui alimente la mesure.

Vous pouvez ajouter des mesures supplémentaires une fois la mesure initiale sélectionnée et superposer toutes les mesures sur un seul rapport ou effectuer des calculs multimesures en ajoutant des formules.

## Etape 3 : Ajouter des `Formulas`

`Formulas` sont ajoutées aux rapports en cliquant sur **[!UICONTROL Add Formula]**, juste au-dessus de la liste des mesures dans le rapport. Dans l’[éditeur de formules](../data-analyst/dev-reports/formulas-in-rpt-bldr.md), toutes les mesures incluses dans le rapport peuvent être utilisées comme entrées. Des opérateurs mathématiques de base sont utilisés pour manipuler les différentes mesures.

Supposons que vous souhaitiez créer un rapport qui nous indique le chiffre d’affaires moyen par commande. Dans ce cas, vous divisez la mesure `Revenue` par la mesure `Number of orders`.

![](../assets/ave-rev-per-order.png)

## Étape 4 : définition des `Time Period` et des `Interval of Analysis` {#time}

Pour vous concentrer sur une période particulière, vous pouvez définir la période de l’analyse. Vous pouvez également choisir des intervalles de temps pour segmenter les données (par exemple, par année, par trimestre ou par mois). Utilisez les menus situés dans le coin supérieur droit du graphique pour définir la période et l’intervalle.

![](../assets/Time_Options_Report_Builder.png)

Lors de la définition d’une période spécifique, assurez-vous que la date de début se trouve au début de l’intervalle et la date de fin à la fin.

Par exemple, la définition d’une période de `January 1st` à `March 1st` et le choix d’un intervalle de `monthly` affichent `March` comme point de données, mais ignorent tous les jours dans `March`, à l’exception de `March 1`. Dans ce cas, vous devez effectuer votre `Time Period` à partir de `January 1 to March 31`.

## Étape 5 : `Group by` / `Segmenting the Analysis` {#groupby}

[Pour segmenter vos mesures en fonction d’une dimension de données](../best-practices/segment-filter.md) cliquez sur le menu **[!UICONTROL Group by]** en haut à gauche du graphique. Une liste déroulante comprenant toutes les dimensions disponibles de la première mesure incluse dans la liste s’affiche.

Vous pouvez choisir `None` pour empêcher la segmentation d’une mesure. Par exemple, vous pouvez avoir besoin d’une mesure qui renvoie le chiffre d’affaires total sans être segmentée, tout en ayant une autre mesure de chiffre d’affaires segmentée par région.

Revenez à votre exemple de chiffre d’affaires moyen par commande et définissez le Regrouper par sur le code promotion. Vous voyez ici le chiffre d&#39;affaires moyen par commande pour les commandes avec et sans code promotion.

![](../assets/Group_By_Report_Builder.png)

Si les mesures incluses dans l’analyse sont basées sur différents tableaux de données, un pop-up vous permet de sélectionner la dimension de données correspondante dans chaque tableau. L’objectif ici est de trouver des dimensions qui partagent le type de valeurs pour la segmentation :

![](../assets/Dimension_Editor.png)

## Étape 6 : définition des `Metric Filters`, `Perspective` et `Time Interval` {#metric-specific}

Pour chaque mesure ajoutée à l’analyse, vous pouvez ajouter des filtres, sélectionner la perspective de données appropriée et définir des options de `time interval`. Pour accéder à ces fonctionnalités, cliquez sur les icônes d’entonnoir (`Filter`), d’œil (`Perspective`) et d’horloge (`Time`) situées à côté des mesures incluses dans le rapport.

![](../assets/Filters_Perspective_Interval_Report_builder.png)

### `Filters`

`Filters` limiter le jeu de données inclus dans l’analyse. Les filtres sont utiles, par exemple, pour évaluer des canaux d’acquisition individuels et supprimer des valeurs aberrantes.

Outre les menus déroulants et la zone de texte, vous pouvez également utiliser des opérateurs de filtre spéciaux, tels que `LIKE` ou `IN`, pour créer des filtres.

L’utilisation de caractères génériques (`%` ou `_`) avec des instructions `LIKE` est prise en charge. Le caractère générique `%` correspond à plusieurs caractères, tandis que `_` ne correspond qu’à un seul caractère. Par exemple :

- `affiliate's name Like B%` autorise uniquement les données des clients dont le nom commence par `B`.

- `affiliate's name Like _ake` autorise uniquement les données des clients dont le nom se présente sous la forme `Jake`, `Rake` ou `Bake`, mais pas `Drake` ou `Blake`.

L’ajout de plusieurs filtres permet un contrôle étroit des données du graphique. Par défaut, toutes les conditions de filtrage doivent être vraies pour qu’un élément de données soit inclus, mais vous pouvez créer des relations OU en modifiant la zone de texte Règles de filtrage .

![](../assets/edit-filter-rules.png)

### `Perspectives`

`Perspectives` Permet de basculer facilement entre les différentes vues de vos données. Examinez ce qui est disponible :

- `Standard perspective` : la perspective standard affiche le résultat pour la date correspondante sur l’axe X (par exemple, le chiffre d’affaires de janvier). Il s’agit de la perspective que vous utilisez dans votre exemple de chiffre d’affaires moyen par commande.

![](../assets/Standard.png)

- `Amount` OU `Percent Change` par rapport à `Previous Period` perspective : cette perspective affiche le montant ou le pourcentage de changement d’un intervalle à l’autre et est utile pour mesurer le taux de changement des mesures en rapide évolution. Il est également possible de comparer l’intervalle à la même période l’année dernière pour montrer la croissance d’une année sur l’autre.

![](../assets/Amt_or_Percent_Change.png)

- `Cumulative perspective` : la `cumulative perspective` affiche le montant cumulé ou en cours de la mesure sur la période. Il est souvent utilisé pour analyser le nombre total de clients et planifier la capacité future.

![](../assets/Cumulative_Perspective.png)

- `Percent of First Value perspective` : cette perspective affiche les données sous la forme d’un pourcentage du premier intervalle inclus dans l’analyse. Cela s’avère utile pour mesurer l’efficacité d’actions spécifiques par rapport à la performance de la première période.

![](../assets/Percent_of_First_Value.png)

- `Rolling averages window perspective` : la fenêtre des moyennes flottantes en perspective affiche la valeur de moyenne flottante d’une mesure sur la période spécifiée. L’intervalle doit être identique à celui défini au niveau du rapport. Par exemple, si l&#39;état affiche le dernier trimestre complet de revenus par semaine, vous pouvez définir la période de fenêtre moyenne glissante sur quatre semaines. Ainsi, les trois premières valeurs sont nulles et la quatrième valeur représente la moyenne des quatre premières semaines de revenus. Pour plus de clarté, veillez à désactiver la case à cocher `Multiple Y-Axes` si vous affichez la même mesure avec une moyenne glissante, comme dans l’exemple ci-dessous.

![](../assets/rolling_avg_window.png)

### Options de temps spécifiques aux mesures

Il existe deux options pour les mesures utilisées dans les rapports : elles peuvent suivre une tendance dans le temps en fonction des options de temps global, ou non, qui les afficheront sous forme de nombre scalaire.

La modification d’un intervalle de temps de mesure en `None` renvoie un nombre `scalar`, ce qui s’avère utile lors de la création de formules qui impliquent la division d’une mesure de tendance temporelle par un nombre `scalar`. Vous pouvez également modifier la période de la mesure `scalar` en une période indépendante de celle du rapport.

Supposons, par exemple, que vous souhaitiez que les revenus mensuels de 2019 soient exprimés en pourcentage des revenus globaux de 2019. Vous pouvez ajouter deux mesures `Revenue` à un rapport avec une période globale comprise entre le 1er janvier 2019 et le 31 décembre 2019, segmentée par intervalle mensuel.

>[!NOTE]
>
>Si vous ajoutez des dimensions `group by`, choisissez une nouvelle visualisation ou ajustez l’intervalle de temps, puis enregistrez uniquement le nombre (`scalar`). Ces ajustements ne sont pas conservés la prochaine fois que vous ouvrez ce rapport depuis un tableau de bord. Seule la période sera conservée.

Pour en savoir plus sur l’utilisation des options de temps dans vos rapports, consultez ce [tutoriel](../tutorials/time-options-visual-rpt-bldr.md).

## Etape 7 : enregistrer le rapport

Lorsque vous créez un graphique, vous pouvez l’enregistrer en cliquant sur **[!UICONTROL Save]** dans le coin supérieur droit du `Visual Report Builder`.

Vous pouvez choisir d’enregistrer un graphique, un tableau ou un nombre (`scalar`) à l’aide de la liste déroulante `Type` et du tableau de bord dans lequel le rapport doit être enregistré à l’aide de la liste déroulante `Location`.

Vous pouvez ensuite enregistrer le rapport en cliquant sur **[!UICONTROL Save to Dashboard]**.

![](../assets/save-to-dashboard.png)

## Sorties de rapport

Pour vous aider à choisir la sortie de rapport à sélectionner, reportez-vous aux sections suivantes :

### Graphique

![](../assets/RB_Chart.png)

### Tableau

![](../assets/RB_Table.png)

### Nombre (`scalar`)

![](../assets/RB_Scalar.png)

Félicitations ! Vous avez terminé.
