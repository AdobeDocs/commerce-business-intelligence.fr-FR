---
title: Création de visualisations à partir de requêtes SQL
description: Apprenez à vous familiariser avec la terminologie utilisée dans le Report Builder SQL et à vous donner une base solide pour créer des visualisations SQL.
exl-id: 9b9bc205-5b64-4e64-8d23-057072e5dd72
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# Création de visualisations à partir de requêtes SQL

L’objectif de ce tutoriel est de vous familiariser avec la terminologie utilisée dans la section `SQL Report Builder` et vous donner des bases solides pour la création `SQL visualizations`.

Le [`SQL Report Builder`](../data-analyst/dev-reports/sql-rpt-bldr.md) est un créateur de rapports avec des options : vous pouvez exécuter une requête dans le seul but de récupérer un tableau de données ou transformer ces résultats en rapport. Ce tutoriel explique comment créer une visualisation à partir d’une requête SQL.

## Terminologie

Avant de commencer ce tutoriel, reportez-vous à la terminologie suivante utilisée dans la section `SQL Report Builder`.

- `Series`: La colonne que vous souhaitez mesurer est appelée Série dans le Report Builder SQL. Les exemples courants sont les suivants : `revenue`, `items sold`, et `marketing spend`. Au moins une colonne doit être définie comme `Series` pour créer une visualisation.

- `Category`: La colonne que vous souhaitez utiliser pour segmenter vos données est appelée une `Category` C’est comme si la variable `Group By` de la fonction [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md). Par exemple, si vous souhaitez segmenter les recettes sur la durée de vie de vos clients selon leur source d’acquisition, la colonne contenant la source d’acquisition est spécifiée comme `Category`. Plusieurs colonnes peuvent être définies sous la forme d’une `Category`.

>[!NOTE]
>
>Les dates et les horodatages peuvent également être utilisés comme `Categories`. Il ne s’agit que d’une autre colonne de données de votre requête et il doit être formaté et ordonné selon vos besoins dans la requête elle-même.

- `Labels`: Ils sont appliqués en tant qu’étiquettes sur l’axe X. Lors de l’analyse des tendances des données au fil du temps, les colonnes &quot;année&quot; et &quot;mois&quot; sont généralement spécifiées sous forme de libellés. Plusieurs colonnes peuvent être définies comme libellé.

## Étape 1 : Écrire la requête

Gardez à l’esprit les points suivants :

- Le `SQL Report Builder` uses [`Redshift SQL`](https://docs.aws.amazon.com/redshift/latest/dg/c_redshift-and-postgres-sql.html).

- Si vous créez un rapport avec une série temporelle, veillez à `ORDER BY` la ou les colonnes d’horodatage. Cela permet de s’assurer que les horodatages sont mappés dans le bon ordre sur le rapport.

- Le `EXTRACT` est très utile pour analyser le jour, la semaine, le mois ou l’année de l’horodatage. Cela s’avère utile lorsque la variable `time interval` que vous souhaitez utiliser sur le rapport est `daily`, `weekly`, `monthly`ou `yearly`.

Pour commencer, ouvrez le `SQL Report Builder` en cliquant **[!UICONTROL Report Builder** > **SQL Report Builder]**.

À titre d’exemple, considérez cette requête qui renvoie le nombre total mensuel d’articles vendus pour chaque produit :

```sql
    SELECT SUM("qty") AS "Items Sold", "products's name" AS "product name",
    EXTRACT(year from "Order date") AS "year",
    EXTRACT(month from "Order date") AS "month"
    FROM "items"
    WHERE "products's name" LIKE '%Jeans'
    GROUP BY  "products's name", "year","month"
    ORDER BY "year" ASC,"month" ASC
    LIMIT 3500
```

Cette requête renvoie cette table de résultats :

![](../assets/SQL_results_table.png)

## Étape 2 : Création de la visualisation

Avec ces résultats, *comment créer la visualisation ?* Pour commencer, cliquez sur le bouton **[!UICONTROL Chart]** dans le `Results` volet. Cela affichera la variable `Chart settings` .

Lors de la première exécution d’une requête, le rapport peut sembler impénétrable, car toutes les colonnes de la requête sont tracées sous la forme d’une série :

![](../assets/SQL_initial_report_results.png)

Pour cet exemple, nous voulons qu’il s’agisse d’un graphique en courbes qui évolue au fil du temps. Pour le créer, utilisez les paramètres suivants :

- `Series`: Sélectionnez la `Items sold` en tant que `Series` car nous voulons le mesurer. Après avoir défini une `Series` une seule ligne est tracée dans le rapport.

- `Category`: Pour cet exemple, nous voulons afficher chaque produit sous la forme d’une ligne différente dans le rapport. Pour ce faire, nous définissons `Product name` comme la propriété `Category`.

- `Labels`: Utiliser les colonnes `year` et `month` comme libellés sur l’axe X pour pouvoir afficher `Items Sold` comme tendance au fil du temps.

>[!NOTE]
>
>La requête doit contenir un `ORDER BY` clause sur les étiquettes si elles sont `date`/`time` colonnes.

Voici un aperçu rapide de la manière dont nous avons créé cette visualisation, depuis l’exécution de la requête jusqu’à la configuration du rapport :

![](../assets/SQL_report_settings.gif)

## Étape 3 : Sélectionnez une `Chart Type`

Cet exemple utilise la méthode `Line` type de graphique. Pour utiliser un `chart type`, cliquez sur les icônes situées au-dessus de la section options du graphique pour le modifier :

![](../assets/Chart_types.png)

## Étape 4 : Enregistrement de la visualisation

Si vous souhaitez réutiliser ce rapport, attribuez-lui un nom, puis cliquez sur **[!UICONTROL Save]** dans le coin supérieur droit.

Dans la liste déroulante, sélectionnez `Chart` comme la propriété `Type` puis un tableau de bord dans lequel enregistrer le rapport.

## Félicitations ! Tu as fini.

Vous voulez aller plus loin ? Consultez la section [bonnes pratiques relatives à l’optimisation des requêtes](../best-practices/optimizing-your-sql-queries.md).
