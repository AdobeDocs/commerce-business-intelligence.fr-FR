---
title: Utilisation du Report Builder SQL
description: Découvrez les avantages et inconvénients de l’utilisation du Report Builder SQL.
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 0%

---

# Utilisation de [!DNL SQL Report Builder]

>[!NOTE]
>
>Nécessite [des autorisations d’administrateur](../../administrator/user-management/user-management.md) pour créer et modifier des graphiques SQL. Les utilisateurs de `Standard` peuvent réorganiser ces graphiques dans les tableaux de bord et les utilisateurs de `Read-only` ont la même expérience que les graphiques traditionnels. En outre, les utilisateurs de `Read-only` n’ont pas accès au texte de la requête.

Pour en savoir plus, consultez la [vidéo de formation](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=fr) .

[!DNL SQL], ou langage de requête structuré, est un langage de programmation utilisé pour communiquer avec des bases de données. Dans [!DNL Commerce Intelligence], [!DNL SQL] est utilisé pour interroger ou récupérer des données de votre Data Warehouse. Examinez les rapports de votre tableau de bord : en arrière-plan, chacun d’eux est alimenté par une requête [!DNL SQL].

Vous pouvez utiliser le [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) pour interroger directement votre Data Warehouse, afficher les résultats et les transformer en graphique. Vous pouvez commencer à créer un rapport avec le [!DNL SQL Report Builder] en cliquant sur **[!UICONTROL Report Builder** > **[!DNL SQL Report Builder]]**.

Pour en savoir plus, consultez la [vidéo de formation](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=fr) .

Le [!DNL SQL Report Builder] vous permet d’interroger directement votre Data Warehouse, d’afficher les résultats et de les transformer rapidement en graphique. L’utilisation de [!DNL SQL] pour créer des rapports présente le meilleur aspect : il n’est pas nécessaire d’attendre les cycles de mise à jour pour itérer sur les colonnes que vous créez. Si les résultats ne semblent pas bons, vous pouvez rapidement modifier et réexécuter la requête jusqu’à ce que les éléments correspondent à vos attentes.

Cette rubrique vous guide tout au long de l’utilisation de [!DNL SQL Report Builder]. Une fois que vous avez pris connaissance de votre parcours, consultez le tutoriel [!DNL SQL] pour les visualisations ou essayez d’optimiser certaines des requêtes que vous avez écrites.

Couvert dans cet article :

1. [Ecriture d&#39;une requête](#writing)

1. [Exécution de la requête et affichage des résultats](#runquery)

1. [Création d’une visualisation](#createviz)

1. [Enregistrer le rapport](#save)

## [!DNL SQL Report Builder] Intégrations

[[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) est la seule intégration indisponible à utiliser avec [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md). Cette fonctionnalité est en cours de développement.

Pour commencer à créer un rapport [!DNL SQL], cliquez sur **[!UICONTROL Report Builder]** ou **[!UICONTROL Add Report]** en haut de n’importe quel tableau de bord. Dans l’écran [!DNL Report Picker], cliquez sur **[!UICONTROL SQL Report Builder]** pour ouvrir l’éditeur [!DNL SQL].

## Prise en main

Pour modifier un rapport, cliquez sur l’icône d’engrenage (![](../../assets/gear-icon.png)) dans le coin supérieur droit d’un graphique basé sur [!DNL SQL] et cliquez sur **[!UICONTROL Edit]**.

## Ecriture d&#39;une requête {#writing}

>[!NOTE]
>
>Les requêtes [!DNL SQL Report Builder] sont sensibles à la casse. Assurez-vous d’utiliser la bonne casse lors de l’écriture de requêtes ou vous risquez de générer des résultats ou des erreurs inattendus.

En suivant les [instructions pour l’optimisation des requêtes](../../best-practices/optimizing-your-sql-queries.md), écrivez une requête dans l’éditeur [!DNL SQL].

>[!IMPORTANT]
>
>**Mesures dans les [!DNL SQL] rapports** - Lorsque vous insérez une mesure dans un rapport SQL, le `current definition` de la mesure est utilisé.

Si la mesure est mise à jour ultérieurement, le rapport SQL *ne reflète pas les modifications.* Vous devez modifier manuellement le rapport pour que les modifications soient prises en compte.

En utilisant les boutons situés en haut de la barre latérale, vous pouvez basculer entre les listes de tableaux et de mesures disponibles pour une utilisation dans le [!DNL SQL Report Builder]. Si vous ne voyez pas ce que vous recherchez dans la liste, essayez de le rechercher à l’aide de la barre de recherche située en haut de la barre latérale.

Vous pouvez également utiliser la barre latérale dans l’éditeur [!DNL SQL] pour insérer des mesures, des tableaux et des colonnes directement dans vos requêtes en pointant dessus et en cliquant sur **[!UICONTROL Insert]** :

![Insertion d&#39;une table dans l&#39;éditeur [!DNL SQL].](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>Toute [fonction SELECT](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST), ou toute fonction qui ne mute pas de données, prise en charge par PostgreSQL est prise en charge dans le Report Builder SQL. Cela inclut, sans s’y limiter, les mesures AVG, COUNT, COUNT DISTINCT, MIN/MAX et SUM.

En outre, tout type `JOIN` est pris en charge, mais Adobe recommande uniquement d’utiliser INNER JOIN, car il est le moins cher des types `JOIN`.

## Exécution de la requête et affichage des résultats {#runquery}

Lorsque vous avez terminé d’écrire votre requête, cliquez sur **[!UICONTROL Run Query]**. Les résultats s’affichent dans un tableau sous l’éditeur SQL :

![Exécution de la requête et affichage des résultats.](../../assets/SQL_Run_Query.gif)

Si les résultats semblent ternes, vous pouvez modifier la requête et la réexécuter jusqu’à ce que vous soyez satisfait.

Vous pouvez parfois voir [messages sous l’éditeur avec EXPLAIN en eux](../../best-practices/optimizing-your-sql-queries.md). Si vous voyez l’un d’eux, cela signifie que votre requête n’a pas été exécutée et nécessite un ajustement.

Une fois la requête modifiée, vous pouvez passer à la création d’une visualisation ou à l’enregistrement de votre travail dans un tableau de bord.

## Création d’une visualisation {#createviz}

Pour créer une visualisation avec vos résultats de requête, cliquez sur l’onglet **[!UICONTROL Chart]** dans le volet `Results`. Dans cet onglet, vous sélectionnez :

* `Series` ou la colonne que vous souhaitez mesurer, par exemple **Éléments vendus**.
* `Category` ou la colonne que vous souhaitez utiliser pour segmenter vos données, par exemple **source d’acquisition**.
* Les valeurs `Labels` ou de l’axe X.

Voici un aperçu rapide du processus de visualisation :

![](../../assets/SQL_RB_viz_overview.gif)

Pour une présentation détaillée de la création d’une visualisation, reportez-vous au [tutoriel Création de visualisations à partir de requêtes SQL](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;}.

## Enregistrer le rapport {#save}

Avant de pouvoir enregistrer votre travail, vous devez donner un nom au rapport. N’oubliez pas de suivre les [bonnes pratiques pour nommer](../../best-practices/naming-elements.md){: target=&quot;_blank&quot;} et de choisir quelque chose qui véhicule clairement ce qu’est le rapport !

Cliquez sur **[!UICONTROL Save]** dans le coin supérieur droit de l’éditeur [!DNL SQL] et sélectionnez le rapport `Type` (`Chart` ou `Table`). Pour terminer, sélectionnez le tableau de bord dans lequel enregistrer le rapport et cliquez sur **[!UICONTROL Save to Dashboard]**.

![](../../assets/SQL_Save_Report.gif)

### Analyse de vos données

#### [!DNL SQL Report Builder]

[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) vous donne la possibilité d’interroger directement votre Data Warehouse, d’afficher les résultats et de les transformer rapidement en rapport. L&#39;utilisation de [!DNL SQL] vous permet également [ d&#39;utiliser des  [!DNL SQL]  fonctions qui ne sont pas disponibles ](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) dans les Reports Builder `Visual` ou `Cohort`, ce qui vous permet de mieux contrôler vos données.

Les colonnes calculées créées à l’aide de [!DNL SQL] ne dépendent pas des cycles de mise à jour, ce qui signifie que vous pouvez les itérer à votre convenance et voir immédiatement les résultats.

>[!NOTE]
>
>Cela ne s&#39;applique qu&#39;à la structure de la colonne, et non à l&#39;actualisation des données. Les nouvelles données dépendent toujours des cycles de mise à jour terminés avec succès.

| **C&#39;est parfait pour...** | **Ce n&#39;est pas très bien pour...** |
|---|---|
| Analystes intermédiaires/avancés | Débutants : vous devez connaître [!DNL SQL]. |
| Le [!DNL SQL] expert | Analyses simples : l’écriture d’une requête peut être plus efficace que l’utilisation de [!UICONTROL Visual Report Builder]. |
| Création de colonnes calculées à usage unique | Partage avec d&#39;autres - considérez votre audience : comprennent-ils [!DNL SQL] ? Dans le cas contraire, ils peuvent être perturbés par la manière dont le rapport est créé. |
| Données avec des relations `one-to-many` |  |
| Test d&#39;une nouvelle colonne ou analyse |  |

#### Résultats de la base de données et de l’éditeur SQL

La plupart du temps, les différences de résultats peuvent être attribuées aux cycles de mise à jour. Si [!DNL Commerce Intelligence] est en train de répliquer les données de votre base de données vers votre Data Warehouse, vous pouvez voir des résultats différents même lors de l’utilisation de la même requête.

Les problèmes de connexion peuvent également entraîner des incohérences. Accédez à la page `Connections` en cliquant sur **[!DNL Manage Data** > **Connections]** pour l’extraire. Y a-t-il une erreur pour l’intégration de la base de données en question ? Si c&#39;est le cas, vous devrez peut-être [réauthentifier l&#39;intégration](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=fr) pour que les tâches s&#39;exécutent à nouveau.

Si toutes vos intégrations sont connectées avec succès et que vous n’êtes pas au milieu d’un cycle de mise à jour, il peut y avoir autre chose à faire.

#### La suppression d&#39;un rapport [!DNL SQL] supprime-t-elle également les colonnes sous-jacentes de mon Data Warehouse ?

Non, vous ne perdez aucune colonne de votre Data Warehouse, quelle que soit la manière dont vous les avez créées.

Les colonnes créées à l’aide de `Data Warehouse Manager` ne sont pas affectées si vous supprimez un rapport ou une requête qui les utilise.

Les colonnes créées à l’aide de [!DNL SQL Report Builder] ne sont pas enregistrées dans votre Data Warehouse.


#### `Report Builder` contre `SQL Report Builder`

[!DNL SQL Report Builder] offre davantage de flexibilité lors de la création et de la structuration de vos graphiques. Vous pouvez, par exemple, sélectionner les valeurs à afficher sur les axes `X` et `Y`. Pour plus d’informations sur la création de graphiques dans [!DNL SQL Report Builder], consultez le tutoriel [Création de visualisations à partir de [!DNL SQL] requêtes](../../tutorials/create-visuals-from-sql.md) .

#### `Cohort Report Builder` {#cohortrb}

Contrairement à [!DNL Visual Report Builder], le [[!DNL Cohort Report Builder]](../dev-reports/cohort-rpt-bldr.md) est destiné à un seul objectif : analyser et identifier les tendances comportementales de groupes d’utilisateurs similaires au fil du temps. L&#39;utilisation de [!DNL Cohort Report Builder] ne nécessite pas de connaissances [!DNL SQL], vous pouvez donc vous plonger directement sans hésitation si vous commencez.

| **C&#39;est parfait pour...** | **Ce n&#39;est pas très bien pour...** |
|---|---|
| Analystes intermédiaires/avancés | Débutants : vous avez besoin de cohortes définissant les pratiques. |
| Identification des tendances comportementales au fil du temps | Analyse qualitative : elle peut être [terminée](../dev-reports/create-qual-cohort-analysis.md), mais nécessite une assistance Adobe. |

## Reconstruire les requêtes après le cycle de mise à jour

Vous n’avez pas à recréer vos requêtes. Les rapports créés à l’aide de [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) sont enregistrés comme ceux créés dans le `Report Builder` traditionnel. Le processus de mise à jour des graphiques [!DNL SQL] est le même : une fois vos données mises à jour, les valeurs de vos graphiques seront recalculées et réaffichées.

>[!NOTE]
>
>Lors de la suppression d’un rapport/d’une requête [!DNL SQL], elle ne supprime pas les colonnes sous-jacentes de votre Data Warehouse. Vous ne perdez aucune colonne, quelle que soit la manière dont vous les avez créées.

* Les colonnes créées à l’aide du Gestionnaire de Data Warehouse ne sont pas affectées si vous supprimez un rapport ou une requête qui les utilise.

* Les colonnes créées à l’aide du Report Builder SQL ne sont pas enregistrées dans votre Data Warehouse.

## Remplissage {#wrapup}

Si vous souhaitez essayer quelque chose d’un peu plus difficile, pourquoi ne pas essayer d’écrire une requête optimisée pour la visualisation ? Consultez le [tutoriel Création de visualisations à partir de [!DNL SQL] requêtes](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;} pour commencer.
