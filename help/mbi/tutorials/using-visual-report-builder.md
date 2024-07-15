---
title: Utilisation du Report Builder visuel
description: Découvrez comment analyser les données de votre rapport pour une période spécifique.
exl-id: da97b63d-63f0-4fd6-87e3-4cac49a42acc
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# Utilisez le [!DNL Visual Report Builder]

L’ [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md) vous permet d’explorer visuellement vos données afin d’obtenir des informations et d’orienter les décisions professionnelles. Ce tutoriel vous guide tout au long du processus de création d’un rapport de base.

>[!NOTE]
>
>Pour ajouter un rapport à un tableau de bord, vous avez besoin de `Standard` [autorisations utilisateur](../administrator/user-management/user-management.md) et de `Edit` accès au tableau de bord.

## Etape 1 : création d&#39;un rapport

Pour commencer à créer un rapport, cliquez sur **[!UICONTROL Report Builder]** dans la barre latérale ou sur **[!UICONTROL Add Report]** en haut de n’importe quel tableau de bord. Lorsque la page `Report Builder` s’affiche, cliquez sur l’option **[!UICONTROL Visual Report Builder]** .

Pour modifier un rapport créé dans le [!DNL Visual Report Builder], cliquez sur l’icône d’engrenage (Options) dans le coin supérieur droit d’un graphique, puis cliquez sur **[!UICONTROL Edit]**.

## Étape 2 : ajout de mesures

La première étape de la création d’une analyse consiste à sélectionner [la mesure](../data-user/reports/ess-manage-data-metrics.md) à analyser. Bien que les mesures soient répertoriées par défaut par ordre alphabétique, vous pouvez également les regrouper en fonction du tableau qui alimente la mesure.

Vous pouvez ajouter d’autres mesures une fois la mesure initiale sélectionnée et superposer toutes les mesures sur un seul rapport ou effectuer des calculs multimesures en ajoutant des formules.

## Étape 3 : Ajout de `Formulas`

`Formulas` sont ajoutés aux rapports en cliquant sur **[!UICONTROL Add Formula]**, situé juste au-dessus de la liste des mesures du rapport. Dans l’ [éditeur de formule](../data-analyst/dev-reports/formulas-in-rpt-bldr.md), toutes les mesures incluses dans le rapport peuvent être utilisées comme entrées. Les opérateurs mathématiques de base sont utilisés pour manipuler les différentes mesures.

Supposons que vous souhaitiez créer un rapport qui montre les recettes moyennes par commande. Dans ce cas, vous diviserez la mesure `Revenue` par la mesure `Number of orders`.

![](../assets/ave-rev-per-order.png)

## Étape 4 : définition des `Time Period` et `Interval of Analysis` {#time}

Pour vous concentrer sur une période spécifique, vous pouvez définir la période de l’analyse. Vous pouvez également choisir des intervalles de temps pour segmenter les données (par exemple, par année, par trimestre ou par mois). Utilisez les menus dans le coin supérieur droit du graphique pour définir la période et l’intervalle.

![](../assets/Time_Options_Report_Builder.png)

Lorsque vous définissez une période spécifique pour cette période, assurez-vous que la date de début se trouve au début de l’intervalle et que la date de fin se trouve à la fin de l’intervalle.

Par exemple, la définition d’une période entre `January 1st` et `March 1st` et le choix d’un intervalle `monthly` présente `March` comme point de données, mais ignore chaque jour dans `March` à l’exception de `March 1`. Dans ce cas, vous devez effectuer votre `Time Period` à partir de `January 1 to March 31`.

## Étape 5 : `Group by` / `Segmenting the Analysis` {#groupby}

[Pour segmenter vos mesures selon une dimension de données](../best-practices/segment-filter.md), cliquez sur le menu **[!UICONTROL Group by]** en haut à gauche du graphique. Cela révèle une liste déroulante comprenant toutes les dimensions disponibles de la première mesure incluse dans la liste.

Vous pouvez choisir `None` pour empêcher la segmentation d’une mesure. Par exemple, vous souhaitez peut-être une mesure qui renvoie les recettes totales sans être segmentée, tout en ayant une autre mesure de recettes segmentée par région.

Revenez à l’exemple de chiffre d’affaires moyen par commande et définissez le Group by sur code promotion. Vous affichez ainsi les recettes moyennes par commande pour les commandes avec et sans code promotion.

![](../assets/Group_By_Report_Builder.png)

Si les mesures incluses dans l’analyse sont créées sur différents tableaux de données, une fenêtre contextuelle vous permet de sélectionner la dimension de données correspondante dans chaque tableau. L’objectif ici est de trouver des dimensions qui partagent des types de valeurs pour la segmentation :

![](../assets/Dimension_Editor.png)

## Étape 6 : définition de `Metric Filters`, `Perspective` et `Time Interval` {#metric-specific}

Pour chaque mesure ajoutée à l’analyse, vous pouvez ajouter des filtres, sélectionner la perspective de données appropriée et définir les options `time interval`. Pour accéder à ces fonctionnalités, cliquez sur les icônes d’entonnoir (`Filter`), d’oeil (`Perspective`) et d’horloge (`Time`) situées en regard des mesures incluses dans le rapport.

![](../assets/Filters_Perspective_Interval_Report_builder.png)

### `Filters`

`Filters` limite le jeu de données inclus dans l’analyse. Les filtres sont utiles, par exemple, lors de l’évaluation de canaux d’acquisition individuels et de la suppression de valeurs aberrantes.

Outre les menus déroulants et la zone de texte, vous pouvez également utiliser des opérateurs de filtres spéciaux tels que `LIKE` ou `IN` pour créer des filtres.

L’utilisation de caractères génériques (`%` ou `_`) avec des instructions `LIKE` est prise en charge. Le caractère générique `%` correspond à plusieurs caractères, tandis que `_` ne correspond qu’à un seul caractère. Par exemple :

- `affiliate's name Like B%` autorise uniquement les données des clients dont le nom commence par `B`.

- `affiliate's name Like _ake` autorise uniquement les données provenant de clients dont les noms sont de type `Jake`, `Rake` ou `Bake`, mais pas `Drake` ni `Blake`.

L’ajout de plusieurs filtres permet un contrôle strict des données du graphique. Par défaut, toutes les conditions de filtrage doivent être vraies pour qu’un élément de données soit inclus, mais vous pouvez créer des relations OU en modifiant la zone de texte Règles de filtrage .

![](../assets/edit-filter-rules.png)

### `Perspectives`

`Perspectives` Permet de basculer facilement entre les différentes vues de vos données. Examinez les éléments disponibles :

- `Standard perspective` : la perspective standard vous montre le résultat de la date correspondante sur l’axe X (par exemple, les recettes de janvier). C’est la perspective que vous utilisez dans votre exemple de revenu moyen par commande.

![](../assets/Standard.png)

- Perspective `Amount` OU `Percent Change` par rapport à `Previous Period` : cette perspective indique la quantité ou le pourcentage de changement d’un intervalle à l’autre et est utile pour mesurer le taux de changement dans les mesures à évolution rapide. Il existe également une perspective permettant de comparer l’intervalle à la même période l’année dernière pour afficher la croissance d’une année à l’autre.

![](../assets/Amt_or_Percent_Change.png)

- `Cumulative perspective` : `cumulative perspective` affiche la somme en cours ou cumulée de la mesure sur la période. Il est souvent utilisé pour analyser le nombre total de clients et planifier une capacité future.

![](../assets/Cumulative_Perspective.png)

- `Percent of First Value perspective` : cette perspective affiche les données sous la forme d’un pourcentage de l’intervalle de première heure inclus dans l’analyse. Cela s’avère utile pour mesurer l’efficacité d’actions spécifiques par rapport aux performances de la première période.

![](../assets/Percent_of_First_Value.png)

- `Rolling averages window perspective` : la perspective de la fenêtre des moyennes roulantes indique la valeur moyenne glissante d’une mesure sur la période spécifiée. L’intervalle doit être le même que l’intervalle défini au niveau du rapport. Si, par exemple, le rapport affiche le dernier trimestre complet des recettes par semaine, vous pouvez définir la période de fenêtre variable moyenne sur quatre semaines. Cela signifie que les trois premières valeurs sont nulles et que la quatrième valeur représente la moyenne des quatre premières semaines des recettes. Pour plus de clarté, veillez à désactiver la case à cocher `Multiple Y-Axes` si vous affichez la même mesure avec une moyenne variable, comme dans l’exemple ci-dessous.

![](../assets/rolling_avg_window.png)

### Options d’heure spécifiques aux mesures

Il existe deux options pour les mesures utilisées dans les rapports : elles peuvent afficher la tendance au fil du temps en fonction des options temporelles globales, ou non, ce qui les affichera comme un nombre scalaire.

La modification d’un intervalle de temps de mesure à `None` renvoie un nombre `scalar`, ce qui est utile lors de la création de formules qui impliquent la division d’une mesure de tendance de temps par un nombre `scalar`. En outre, vous pouvez modifier la période de la mesure `scalar` en une période indépendante de celle du rapport.

Par exemple, vous vouliez voir les recettes mensuelles 2019 exprimées en pourcentage du chiffre d’affaires global de 2019. Vous pouvez ajouter deux mesures `Revenue` à un rapport avec une période globale du 1er janvier 2019 au 31 décembre 2019, segmentée par intervalle mensuel.

>[!NOTE]
>
>Si vous ajoutez des dimensions `group by`, sélectionnez une nouvelle visualisation ou ajustez l’intervalle de temps, puis enregistrez uniquement le nombre (`scalar`). Ces ajustements ne sont pas conservés la prochaine fois que vous ouvrez ce rapport à partir d’un tableau de bord ; seule la période est conservée.

Pour en savoir plus sur l’utilisation des options temporelles dans vos rapports, consultez ce [tutoriel](../tutorials/time-options-visual-rpt-bldr.md).

## Étape 7 : enregistrer le rapport

Lorsque vous créez un graphique, vous pouvez l’enregistrer en cliquant sur **[!UICONTROL Save]** dans le coin supérieur droit de `Visual Report Builder`.

Vous pouvez choisir d&#39;enregistrer un graphique, un tableau ou un nombre (`scalar`) à l&#39;aide de la liste déroulante `Type` et du tableau de bord sur lequel le rapport doit être enregistré à l&#39;aide de la liste déroulante `Location`.

Vous pouvez ensuite enregistrer le rapport en cliquant sur **[!UICONTROL Save to Dashboard]**.

![](../assets/save-to-dashboard.png)

## Sorties de rapport

Pour vous aider à choisir la sortie du rapport, reportez-vous aux sections suivantes :

### Graphique

![](../assets/RB_Chart.png)

### Tableau

![](../assets/RB_Table.png)

### Nombre (`scalar`)

![](../assets/RB_Scalar.png)

Félicitations ! Tu as fini.
