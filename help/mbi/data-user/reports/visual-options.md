---
title: Options de visualisation dans le Report Builder visuel
description: Découvrez comment utiliser les options Visualisation dans le Report Builder Visuel.
exl-id: e42a004e-28e3-4484-bb5a-b58c810b23e0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 0%

---

# Options de visualisation

La sélection de la bonne visualisation pour un jeu de données donné est un élément essentiel du processus d’analyse. Chaque ensemble de données a une histoire à raconter, mais l&#39;effet de cette histoire est souligné par son impact visuel et sa lisibilité.

[!DNL Commerce Intelligence] [!DNL Visual Report Builder] offre 12 options de visualisation distinctes, chacune ayant ses propres avantages et cas d’utilisation. Cette rubrique aborde les différentes options de visualisation dans [!DNL Commerce Intelligence], y compris les configurations de rapport requises le cas échéant, ainsi qu’un exemple de cas d’utilisation. Les visualisations suivantes sont disponibles dans [!DNL Commerce Intelligence] :

* `Scalar`
* `Table`
* `Line`
* `Bar`
* `Stacked Bar`
* `Column`
* `Stacked Column`
* `Pie`
* `Area`
* `Funnel`
* `Scatter plot`
* `Bubble`
* `Heatmap`

## `Scalar`

Les rapports `Scalar` s’affichent sous la forme d’une seule valeur numérique. Il est le plus souvent utilisé pour afficher la valeur &quot;tout le temps&quot; d’une mesure clé telle que les recettes ou les commandes, ou pour comparer les recettes à ce jour par rapport au budget avec deux rapports scalaires distincts. Dans l’exemple ci-dessous, ceci indique simplement le nombre total de commandes pour l’intervalle de création de rapports donné :

![](../../assets/blobid0.png)

Pour enregistrer un rapport en tant que rapport évolutif, configurez vos filtres et paramètres temporels, puis cliquez sur **[!UICONTROL Save]** ou **[!UICONTROL Update]** dans la section supérieure droite du rapport. Dans la liste déroulante `Type` , choisissez le nom Nombre : mesure pour enregistrer le rapport en tant que valeur affichée sur la barre de gauche.

![](../../assets/blobid1.png)

**Exigences** :

* `Time interval` : `None`
* `Group by` : `None`
* Une mesure uniquement

## `Table`

Comme son nom l’indique, les rapports `table` sont idéaux pour afficher les détails tabulaires. Lorsqu’un même rapport doit afficher de nombreux groupes par valeurs ou par mesures, un tableau est souvent le meilleur moyen d’y parvenir. À titre d’exemple, vous trouverez ci-dessous un tableau &quot;Détails du client&quot;, présentant les commandes et les recettes regroupées par email client :

![](../../assets/blobid2.png)

Comme pour les rapports scalaires, vous pouvez enregistrer un rapport en tant que tableau en cliquant sur **[!UICONTROL Save]** ou **[!UICONTROL Update]** dans le créateur de rapports, puis en sélectionnant l’option Tableau dans la liste déroulante `Type`.

![](../../assets/blobid3.png)

**Conditions requises :**

* Bien qu’il n’y ait aucune configuration de rapport requise, il est important de noter que les tableaux sont limités à 3 500 lignes. Si votre jeu de données contient plus de 3 500 lignes, vous devez soit filtrer les résultats pour réduire la portée, soit exporter les résultats vers `.csv` ou `Excel` pour afficher l’ensemble de données.

## `Line`

`Line` Les graphiques constituent le choix idéal pour comparer les performances de cohortes de mesures similaires. Par exemple, en analysant les recettes de deux régions sur la même période ou en comparant la croissance d’une année à l’autre des commandes réalisées, comme illustré ci-dessous :

![](../../assets/blobid0.png)

Chaque mesure et formule ajoutée au rapport est représentée par sa propre ligne. Lors de la comparaison de mesures avec des unités et des échelles similaires, n’oubliez pas de décocher la case pour `Multiple Y-Axes` afin d’afficher toutes les mesures sur la même échelle.

Pour enregistrer un rapport sous forme de graphique en courbes, ajustez le rapport `Type` sur `Chart`, puis sélectionnez la visualisation appropriée dans le créateur de rapports, comme illustré ci-dessous :

![](../../assets/blobid1.png)

**Conditions requises :**

* Aucun

## `Bar`

`Bar` Les graphiques affichent vos données sous la forme d’une série de barres horizontales. Ils sont idéaux pour afficher les performances globales d’un nombre limité de mesures ou de groupes par valeurs. Par exemple, un graphique à barres peut être utilisé pour comparer les recettes par magasin :

![](../../assets/blobid2.png)

Chaque combinaison de mesure, de groupe par et d’intervalle de temps distincte s’affiche dans sa propre barre. Si vous avez deux mesures avec une `group by`, contenant trois valeurs `group by` distinctes, votre rapport affiche six barres distinctes.

Pour enregistrer un rapport sous forme de graphique à barres, ajustez le rapport `Type` sur `Chart` et sélectionnez l’option `Bar` comme illustré ci-dessous :

![](../../assets/blobid3.png)

**Conditions requises :**

* Aucun

## `Stacked Bar`

`Stacked bar` graphiques sont similaires à leurs frères graphiques à barres, avec la possibilité supplémentaire d’afficher la ventilation proportionnelle de chaque barre. La plupart du temps, les graphiques à barres empilés sont configurés avec plusieurs mesures et un seul groupe par, de sorte que chaque barre représente un groupe unique par valeur, divisé entre ses composantes de mesure.

Par exemple, le rapport ci-dessous comporte deux mesures de recettes identiques : l’une filtrée pour les premières commandes et l’autre filtrée pour les commandes répétées. Une fois le regroupement par magasin effectué, vous pouvez afficher à la fois la contribution totale aux recettes pour chaque magasin (représentée par la largeur totale de la barre) et la première fois par rapport à la ventilation des recettes répétée pour chaque magasin.

![](../../assets/blobid4.png)

Assurez-vous que la case `Multiple Y-Axes` n’est pas cochée lors de la configuration d’un rapport comme ci-dessus.

Pour enregistrer un rapport sous forme de graphique à barres empilées, ajustez le rapport `Type` sur `Chart` et sélectionnez l’option de barre empilée dans le créateur de rapports :

![](../../assets/blobid5.png)

**Conditions requises :**

* Aucun

## `Column`

`Column` Les graphiques représentent chaque point de données sous la forme d’une colonne verticale. Ils sont plus efficaces pour afficher les données de tendance de temps que la visualisation de graphique à barres horizontales. Chaque mesure et groupe unique par combinaison est représenté dans sa propre série de barres. Un rapport Colonne est préférable pour les rapports comportant trois mesures ou moins ou une mesure ayant un seul groupe en contenant 1 à 3 groupes par valeurs.

Dans l’exemple ci-dessous, vous voyez deux mesures de recettes : l’une filtrée pour les recettes pour la première fois et l’autre pour les recettes répétées, avec des tendances au fil du temps par mois :

![](../../assets/blobid6.png)

Les rapports Colonnes peuvent être enregistrés en remplaçant le rapport `Type` par `Chart` et en sélectionnant l’option de visualisation de colonnes :

![](../../assets/blobid7.png)

**Conditions requises :**

* Aucun

## `Stacked Column`

Les rapports `Stacked column` sont presque identiques aux graphiques en colonnes, sauf que des colonnes similaires sont empilées les unes au-dessus des autres, de sorte que la hauteur totale représente la somme des valeurs. Les colonnes empilées sont à nouveau mieux visualisées avec un nombre limité de mesures ou de classes.

En utilisant la même configuration de rapport que celle décrite dans la section `Column` ci-dessus, un rapport avec deux mesures de recettes (filtrées pour la première fois et répétées) ressemblerait à ce qui suit avec une visualisation en colonne empilée :

![](../../assets/blobid8.png)

Encore une fois, il est important que la case à cocher `Multiple Y-Axes` soit décochée lors de l’affichage de plusieurs mesures avec la visualisation en colonnes empilée.

Pour enregistrer un rapport en tant que colonne empilée, définissez le rapport `Type` sur `Chart` et sélectionnez l’option `stacked column` :

![](../../assets/blobid9.png)

**Conditions requises :**

* Aucun

## `Pie`

`Pie` Les graphiques sont idéaux pour afficher une seule mesure avec une ou plusieurs classes de groupe ou plusieurs mesures sans classes de groupe. Dans les deux cas, l’intervalle doit être défini sur &quot;aucun&quot; pour afficher les données dans un graphique circulaire. Dans l’exemple ci-dessous, une mesure de commandes unique est regroupée par nom de magasin pour afficher la ventilation des commandes par magasin :

![](../../assets/blobid10.png)

Pour enregistrer un rapport sous forme de graphique circulaire, définissez le rapport `Type` sur `Chart` et sélectionnez l’option `pie` comme illustré ci-dessous :

![](../../assets/blobid11.png)

**Conditions requises :**

* `Time interval` : `None`
* L’une des options suivantes :
   * `Single metric with one or more group bys`
   * `Multiple metrics with no group bys`

## `Area`

`Area` Les graphiques sont presque identiques aux graphiques en colonnes empilés, sauf que les colonnes s’affichent en continu. Tout comme les colonnes empilées, les diagrammes de surface sont mieux visualisés avec un nombre limité de groupes ou de mesures.

En reprenant le même exemple de la section `stacked column` , le rapport ci-dessous présente la première fois par rapport aux recettes répétées avec la visualisation des graphiques à aires :

![](../../assets/blobid12.png)

Pour enregistrer un rapport sous forme d&#39;diagramme de surface, ajustez le `Type` sur `Chart` et sélectionnez l&#39;option Zone :

![](../../assets/blobid13.png)

**Conditions requises :**

* Aucun

## `Funnel`

`Funnel` Les graphiques sont parfaits pour visualiser la conversion sur une séquence d’événements attendue. Vous pouvez, par exemple, analyser le chiffre d’affaires potentiel de votre entonnoir de vente du prospect à l’accord conclu, ou mesurer la baisse du nombre de clients entre leur première et leur deuxième commandes, leurs deuxième et troisième commandes, etc. Vous trouverez ci-dessous un exemple de ce dernier :

![](../../assets/blobid4.png)

Dans un rapport Entonnoir, la valeur relative d’une étape donnée de l’entonnoir est reflétée par la hauteur de l’étape. La configuration du rapport détermine l’ordre dans lequel les étapes sont affichées. Il existe deux façons de configurer un rapport Entonnoir :

* `Single metric with one group by` : - Ordre des étapes déterminé par le paramètre &quot;Afficher le haut/bas&quot; du groupe par. Par défaut, les étapes de l’entonnoir s’affichent dans l’ordre de la valeur la plus grande à la plus petite, mais vous pouvez également les trier par ordre alphabétique selon le groupe par nom.

* `Multiple metrics with no group by` : - Ordre des étapes déterminé par l’ordre dans lequel les mesures sont ajoutées au rapport.

Pour enregistrer un rapport sous forme de graphique entonnoir, ajustez le rapport `Type` sur `Chart` et sélectionnez la visualisation appropriée dans le créateur de rapports.

![](../../assets/blobid5.png)

**Conditions requises :**

* `Time interval` : `None`
* L’une des options suivantes :
   * `Single metric with one group by`
   * `Multiple metrics with no group by`

## `Scatter plot`

Un `scatter plot` est utilisé pour examiner la relation d’une mesure avec deux variables différentes afin que vous puissiez facilement identifier les corrélations et les valeurs aberrantes. Ce type de visualisation est préférable uniquement avec les dimensions numériques. Essayez-le avec la mesure Commandes et les dimensions `Customer's lifetime number of coupons` et `Customer's lifetime revenue` pour voir comment l’utilisation des coupons est liée aux recettes. Vous pouvez choisir entre un graphique de dispersion avec et sans courbe de tendance :

![](../../assets/scatter-plot-1.png)

![ sans tendance](../../assets/scatter-plot-2.png)

![](../../assets/scatter-plot-3.png)

![Avec trendline](../../assets/scatter-plot-4.png)

**Conditions requises :**

Option 1 :

* Deux `metrics`
* Un `group by`
* `Time interval` : `None`

Option 2 :

* Deux `metrics`
* No `group by`
* Set `time interval`

## Graphique `Bubble`

Un graphique `bubble` peut afficher jusqu’à quatre dimensions de données pour lesquelles les axes `X` et `Y` spécifient l’emplacement des bulles. L’axe `Z` correspond à la taille des bulles. En incluant deux groupes, vous pouvez ajouter de la couleur aux bulles. Ce type de visualisation est préférable lorsque vous souhaitez tracer plusieurs dimensions de données dans un seul graphique.

Par exemple, le graphique suivant montre le nombre de clients (taille de la bulle) regroupés selon une source d’acquisition spécifique (couleur de la bulle) et un état (différentes bulles d’une couleur spécifique), par rapport au total des recettes et aux commandes de durée de vie moyenne.

![](../../assets/bubble-1.png)

Le graphique suivant montre le nombre de clients (taille de la bulle) regroupés par source d’acquisition (couleur de la bulle) et par état (différentes bulles dans une couleur spécifique), par rapport à la valeur de durée de vie moyenne et aux recettes totales.

![](../../assets/bubble-2.png)

**Conditions requises pour un graphique à bulles à série unique :**

Option 1

* Trois `metrics`
* Un `group by`
* `Time interval` : `None`

Option 2

* Trois `metrics`
* No `group by`
* Set `time interval`

**Conditions requises pour le graphique à bulles multisérie :**

* Trois `metrics`
* Deux `group by`
* `Time interval` : `None`

## `Heatmap`

Utilisez `heatmaps` pour visualiser les zones réactives dans vos données. Par exemple, une carte thermique peut indiquer l’endroit où vous obtenez habituellement un volume plus élevé. La visualisation de ces données peut vous aider à ajuster vos niveaux d’inventaire pour vous assurer de répondre à la demande pendant ces fenêtres de pointe.

La carte thermique suivante montre les commandes par jour de la semaine, en heure de la journée, sur plusieurs semaines.

![](../../assets/heat-map.png)<!--{: width="650"}-->

**Conditions requises :**

Option 1

* Un `metric`
* Deux `group by`
* `Time interval` : `None`

Option 2

* Un `metric`
* Un `group by`
* Set `time interval`
