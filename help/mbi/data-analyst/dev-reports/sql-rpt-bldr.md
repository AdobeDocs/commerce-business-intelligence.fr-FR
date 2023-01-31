---
title: Utilisation du Report Builder SQL
description: Découvrez les avantages et inconvénients de l’utilisation du Report Builder SQL.
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
source-git-commit: 09b6983c3e06a1f18035542dfa3b9de9ac3ceb38
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 0%

---

# Utilisation `SQL Report Builder`

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../administrator/user-management/user-management.md) pour créer et modifier des graphiques SQL. `Standard` les utilisateurs peuvent réorganiser ces graphiques dans les tableaux de bord ; et `Read-only` les utilisateurs auront la même expérience qu’avec les graphiques traditionnels. En outre, `Read-only` les utilisateurs n&#39;ont pas accès au texte de la requête.

Voir notre [vidéo de formation](https://support.magento.com/hc/en-us/articles/360016730131) pour en savoir plus.

`SQL`, ou langage de requête structuré, est un langage de programmation utilisé pour communiquer avec des bases de données. Dans [!DNL MBI], SQL est utilisé pour interroger ou récupérer des données de votre entrepôt de données. Consultez les rapports de votre tableau de bord : en coulisses, chacun est alimenté par une requête SQL.

Vous pouvez utiliser la variable [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) pour interroger directement votre entrepôt de données, affichez les résultats et transformez-les en graphique. Vous pouvez commencer à créer un rapport à l’aide de l’événement `SQL Report Builder` en accédant à **[!UICONTROL Report Builder** > **SQL Report Builder]**.

Voir notre [vidéo de formation](https://support.magento.com/hc/en-us/articles/360016730131-Training-Video-SQL-Report-Builder) pour en savoir plus.

Le `SQL Report Builder` vous permet d’interroger directement votre entrepôt de données, d’afficher les résultats et de les transformer rapidement en graphique. Le meilleur aspect de l’utilisation de SQL pour créer des rapports est le suivant : [il n’est pas nécessaire d’attendre les cycles de mise à jour pour itérer sur les colonnes](https://support.magento.com/hc/en-us/articles/360016506212) vous créez. Si les résultats n’ont pas l’air tout à fait corrects, vous pouvez rapidement modifier et relancer la requête jusqu’à ce que les éléments correspondent à vos attentes.

Dans cet article, nous vous guidons tout au long de l’utilisation du `SQL Report Builder`. Une fois que vous avez pris connaissance de votre cheminement, consultez notre tutoriel sur SQL pour les visualisations ou essayez d’optimiser certaines des requêtes que vous avez écrites.

Voici un aperçu de ce que nous abordons dans cet article :

1. [Ecriture d&#39;une requête](#writing)

1. [Exécution de la requête et affichage des résultats](#runquery)

1. [Création d’une visualisation](#createviz)

1. [Enregistrer le rapport](#save)

## Intégrations de Reports Builder SQL

Dans l&#39;état actuel du monde, [[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) est la seule intégration indisponible à utiliser avec la variable [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md). Nous travaillons à inclure cette fonctionnalité dans une version ultérieure.

Pour commencer à créer un rapport SQL, cliquez sur **[!UICONTROL Report Builder]** ou **[!UICONTROL Add Report]** en haut de n’importe quel tableau de bord. Dans le `Report Picker` écran, cliquez sur **[!UICONTROL SQL Report Builder]** pour ouvrir l’éditeur SQL.

## Prise en main

Pour modifier un rapport, cliquez sur l’engrenage (![](../../assets/gear-icon.png)) dans le coin supérieur droit d’un graphique SQL, puis cliquez sur **[!UICONTROL Edit]**.

## Ecriture d&#39;une requête {#writing}

>[!NOTE]
>
>`SQL Report Builder` les requêtes sont sensibles à la casse. Assurez-vous d’utiliser la bonne casse lors de l’écriture de requêtes ou vous risquez de générer des résultats ou des erreurs inattendus.

En procédant comme suit : [directives relatives à l’optimisation des requêtes](../../best-practices/optimizing-your-sql-queries.md), écrivez une requête dans l’éditeur SQL.

>[!IMPORTANT]
>
>**Mesures dans les rapports SQL** - Lorsque vous insérez une mesure dans un rapport SQL, la variable `current definition` de la mesure sera utilisée.

Si la mesure est mise à jour ultérieurement, le rapport SQL *ne sera pas* reflètent les modifications. Vous devrez modifier manuellement le rapport pour que les modifications soient prises en compte.

Les boutons situés en haut de la barre latérale vous permettent de basculer entre les listes de tableaux et de mesures disponibles dans la variable `SQL Report Builder`. Si vous ne voyez pas ce que vous recherchez dans la liste, essayez de le rechercher à l’aide de la barre de recherche située en haut de la barre latérale.

Vous pouvez également utiliser la barre latérale dans l’éditeur SQL pour insérer des mesures, des tableaux et des colonnes directement dans vos requêtes en pointant dessus et en cliquant sur **[!UICONTROL Insert]**:

![Insertion d&#39;un tableau dans l&#39;éditeur SQL.](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>Quelconque [Fonction SELECT](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST), ou toute fonction qui ne mute pas de données, prise en charge par PostgreSQL est prise en charge dans le Report Builder SQL. Cela inclut, sans s’y limiter, les mesures AVG, COUNT, COUNT DISTINCT, MIN/MAX et SUM.

En outre, tout type JOIN est pris en charge, mais nous vous recommandons de n’utiliser que le type INNER JOIN , car il est le moins cher des types JOIN.

## Exécution de la requête et affichage des résultats {#runquery}

Lorsque vous avez terminé d’écrire votre requête, cliquez sur **[!UICONTROL Run Query]**. Les résultats s’affichent dans un tableau sous l’éditeur SQL :

![Exécution de la requête et affichage des résultats.](../../assets/SQL_Run_Query.gif)

Si les résultats semblent ternes, vous pouvez modifier la requête et la relancer jusqu’à ce que vous soyez satisfait.

Parfois, vous verrez [messages sous l’éditeur contenant EXPLAIN](../../best-practices/optimizing-your-sql-queries.md). Si vous voyez l’un d’eux, cela signifie que votre requête n’a pas été exécutée et nécessite un ajustement.

Une fois la requête modifiée, vous pouvez passer à la création d’une visualisation ou à l’enregistrement de votre travail dans un tableau de bord.

## Création d’une visualisation {#createviz}

Pour créer une visualisation avec les résultats de la requête, cliquez sur le bouton **[!UICONTROL Chart]** dans le `Results` volet. Dans cet onglet, vous allez sélectionner :

* Le `Series`ou la colonne à mesurer, telle que **Articles vendus**.
* Le `Category`ou la colonne que vous souhaitez utiliser pour segmenter vos données, par exemple **source d&#39;acquisition**.
* Le `Labels`ou les valeurs de l’axe X.

Voici un aperçu rapide du processus de visualisation :

![](../../assets/SQL_RB_viz_overview.gif)

Pour une présentation détaillée de la création d’une visualisation, reportez-vous à notre [Tutoriel sur la création de visualisations à partir de requêtes SQL](../../tutorials/create-visuals-from-sql.md){ : target=&quot;_blank&quot;}.

## Enregistrer le rapport {#save}

Avant de pouvoir enregistrer votre travail, vous devez donner un nom au rapport. N’oubliez pas de suivre le [bonnes pratiques relatives à l’attribution de noms](../../best-practices/naming-elements.md){ : target=&quot;_blank&quot;} et choisissez quelque chose qui véhicule clairement ce qu’est le rapport !

Cliquez sur **[!UICONTROL Save]** dans le coin supérieur droit de l’éditeur SQL et sélectionnez le rapport. `Type` (`Chart` ou `Table`). Pour terminer, sélectionnez le tableau de bord dans lequel enregistrer le rapport et cliquez sur **[!UICONTROL Save to Dashboard]**.

![](../../assets/SQL_Save_Report.gif)

### Analyse de vos données

#### `SQL Report Builder`

[`The SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) vous permet d’interroger directement votre entrepôt de données, d’afficher les résultats et de les transformer rapidement en rapport. L’utilisation de SQL vous permet également de [pour utiliser des fonctions SQL non disponibles](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) dans le `Visual` ou `Cohort` Reports Builder, ce qui vous permet de mieux contrôler vos données.

Nous souhaitons mentionner que les colonnes calculées créées à l’aide de SQL ne dépendent pas des cycles de mise à jour, ce qui signifie que vous pouvez les itérer comme vous le souhaitez et voir immédiatement les résultats.

>[!NOTE]
>
>Cela s&#39;applique uniquement à la structure de la colonne, et non à l&#39;actualisation des données. Les nouvelles données dépendent toujours des cycles de mise à jour terminés avec succès.

| **C&#39;est parfait pour...** | **Ce n&#39;est pas si bien pour...** |
|---|---|
| Analystes intermédiaires/avancés | Débutants : vous devez connaître SQL. |
| L’apprentissage SQL | Analyses simples : l’écriture d’une requête peut être plus efficace que l’utilisation du Report Builder Visuel. |
| Création de colonnes calculées à usage unique | Partage avec d&#39;autres personnes - prenez en compte votre audience : comprennent-ils SQL ? Dans le cas contraire, ils peuvent être perturbés par la manière dont le rapport est créé. |
| Données avec `one-to-many` relations |  |
| Test d&#39;une nouvelle colonne ou analyse |  |

#### Résultats de la base de données et de l’éditeur SQL

La plupart du temps, les différences de résultats peuvent être attribuées aux cycles de mise à jour. If [!DNL MBI] est en train de répliquer les données de votre base de données vers votre Data Warehouse ; il se peut que vous obteniez des résultats différents même lors de l’utilisation de la même requête.

Les problèmes de connexion peuvent également entraîner des incohérences. Accédez au `Connections` en cliquant sur **[!DNL Manage Data** > **Connections]**) pour l’extraire. Y a-t-il une erreur pour l’intégration de la base de données en question ? Si tel est le cas, vous devrez peut-être [réauthentifier l’intégration](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations) pour que les choses recommencent.

Si toutes vos intégrations sont connectées avec succès et que vous n’êtes pas au milieu d’un cycle de mise à jour, il peut y avoir autre chose à faire. Essayez d’utiliser la variable [guides de dépannage des incohérences de données](https://support.magento.com/hc/en-us/sections/360003074492) sur notre site d’assistance pour identifier le problème.

#### La suppression d&#39;un rapport SQL supprime-t-elle également les colonnes sous-jacentes de mon Data Warehouse ?

Non, vous ne perdrez aucune colonne de votre Data Warehouse, quelle que soit la manière dont vous les avez créées.

Colonnes créées à l’aide du `Data Warehouse Manager` ne sera pas affecté si vous supprimez un rapport ou une requête qui les utilise.

Colonnes créées à l’aide du `SQL Report Builder` ne sont pas enregistrés dans votre Data Warehouse.


#### `Report Builder` versus `SQL Report Builder`

Le `SQL Report Builder` vous offre davantage de flexibilité lors de la création et de la structuration de vos graphiques. Vous pouvez, par exemple, sélectionner les valeurs à afficher sur le `X` et `Y` axes. Pour plus d’informations sur la création de graphiques dans le `SQL Report Builder`, consultez notre [Création de visualisations à partir de requêtes SQL](../../tutorials/create-visuals-from-sql.md) tutoriel .

#### `Cohort Report Builder` {#cohortrb}

Contrairement au `Visual Report Builder`, la variable [`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) est destiné à un seul objectif : analyser et identifier les tendances comportementales de groupes d’utilisateurs similaires au fil du temps. L’utilisation du Report Builder de cohortes ne nécessite aucune connaissance SQL. Vous pouvez donc vous y plonger sans hésitation si vous commencez.

| **C&#39;est parfait pour...** | **Ce n&#39;est pas si bien pour...** |
|---|---|
| Analystes intermédiaires/avancés | Débutants : vous avez besoin d’une formation définissant les cohortes. |
| Identification des tendances comportementales au fil du temps | L&#39;analyse qualitative, ça peut être [done](../dev-reports/create-qual-cohort-analysis.md), mais nécessite notre aide. |

## Reconstruire les requêtes après le cycle de mise à jour

Vous n’avez pas à recréer vos requêtes. Rapports créés à l’aide de la variable [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) sont sauvés comme ceux créés dans les `Report Builder`. Le processus de mise à jour des graphiques SQL est exactement le même : une fois vos données mises à jour, les valeurs de vos graphiques seront recalculées et réaffichées.

>[!NOTE]
>
>Lors de la suppression d&#39;un rapport/requête SQL, elle ne supprime pas les colonnes sous-jacentes de votre Data Warehouse. Vous ne perdrez aucune colonne, quelle que soit la manière dont vous les avez créées.

* Les colonnes créées à l’aide du Gestionnaire de Data Warehouse ne seront pas affectées si vous supprimez un rapport ou une requête qui les utilise.

* Les colonnes créées à l’aide du Report Builder SQL ne sont pas enregistrées dans votre Data Warehouse.

## Remplissage {#wrapup}

Si vous souhaitez essayer quelque chose d’un peu plus difficile, pourquoi ne pas essayer d’écrire une requête optimisée pour la visualisation ? Consultez notre [Tutoriel sur la création de visualisations à partir de requêtes SQL](../../tutorials/create-visuals-from-sql.md){ : target=&quot;_blank&quot;} pour commencer.
