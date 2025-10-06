---
title: Utilisation de SQL Report Builder
description: Découvrez les tenants et aboutissants de l’utilisation de SQL Report Builder.
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 0%

---

# Utilisation de [!DNL SQL Report Builder]

>[!NOTE]
>
>Nécessite des [autorisations d’administrateur](../../administrator/user-management/user-management.md) pour créer et modifier des graphiques SQL. `Standard` utilisateurs peuvent réorganiser ces graphiques sur les tableaux de bord et `Read-only` les utilisateurs bénéficient de la même expérience que les graphiques traditionnels. En outre, les utilisateurs `Read-only` n’ont pas accès au texte de la requête.

Voir la [vidéo de formation](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=fr) pour en savoir plus.

[!DNL SQL], ou langage de requête structuré, est un langage de programmation utilisé pour communiquer avec des bases de données. Dans [!DNL Commerce Intelligence], [!DNL SQL] est utilisé pour interroger ou récupérer des données à partir de votre Data Warehouse. Examinez les rapports de votre tableau de bord : en coulisses, chacun est alimenté par une requête [!DNL SQL].

Vous pouvez utiliser l’[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) pour interroger directement votre Data Warehouse, afficher les résultats et les transformer en graphique. Vous pouvez commencer à créer un rapport avec le [!DNL SQL Report Builder] en cliquant sur **[!UICONTROL Report Builder** > **[!DNL SQL Report Builder]]**.

Voir la [vidéo de formation](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=fr) pour en savoir plus.

Le [!DNL SQL Report Builder] vous permet d’interroger directement votre Data Warehouse, d’afficher les résultats et de les transformer rapidement en graphique. Le meilleur aspect de l’utilisation de [!DNL SQL] pour créer des rapports est que vous n’avez pas besoin d’attendre les cycles de mise à jour pour effectuer une itération sur les colonnes que vous créez. Si les résultats ne s’affichent pas correctement, vous pouvez rapidement modifier et réexécuter la requête jusqu’à ce que les éléments correspondent à vos attentes.

Cette rubrique vous guide tout au long de l’utilisation de l’[!DNL SQL Report Builder] . Une fois que vous connaissez la méthode, consultez le tutoriel [!DNL SQL] pour les visualisations ou essayez d’optimiser certaines des requêtes que vous avez écrites.

Couvert dans cet article :

1. [Écrire une requête](#writing)

1. [Exécution de la requête et affichage des résultats](#runquery)

1. [Création d’une visualisation](#createviz)

1. [Enregistrer le rapport](#save)

## Intégrations [!DNL SQL Report Builder]

[[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) est la seule intégration qui ne peut pas être utilisée avec le [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md). Cette fonctionnalité est en cours de développement.

Pour commencer à créer un rapport [!DNL SQL], cliquez sur **[!UICONTROL Report Builder]** ou **[!UICONTROL Add Report]** en haut de n’importe quel tableau de bord. Dans l’écran [!DNL Report Picker], cliquez sur **[!UICONTROL SQL Report Builder]** pour ouvrir l’éditeur de [!DNL SQL].

## Prise en main

Pour modifier un rapport, cliquez sur l’icône d’engrenage (![icône d’engrenage](../../assets/gear-icon.png)) dans le coin supérieur droit d’un graphique basé sur des [!DNL SQL], puis cliquez sur **[!UICONTROL Edit]**.

## Écrire une requête {#writing}

>[!NOTE]
>
>[!DNL SQL Report Builder] requêtes sont sensibles à la casse. Assurez-vous d’utiliser la casse appropriée lorsque vous écrivez des requêtes, sans quoi vous pourriez rencontrer des résultats inattendus ou des erreurs.

En suivant les [instructions pour l’optimisation des requêtes](../../best-practices/optimizing-your-sql-queries.md), écrivez une requête dans l’éditeur de [!DNL SQL].

>[!IMPORTANT]
>
>**Mesures dans [!DNL SQL] rapports** - Lorsque vous insérez une mesure dans un rapport SQL, la `current definition` de la mesure est utilisée.

Si la mesure est mise à jour ultérieurement, le rapport SQL *ne reflète pas* les modifications. Vous devez modifier manuellement le rapport pour que les modifications soient prises en compte.

À l’aide des boutons situés en haut de la barre latérale, vous pouvez basculer entre les listes de tableaux et de mesures disponibles dans le [!DNL SQL Report Builder]. Si vous ne voyez pas ce que vous recherchez dans la liste, essayez de le rechercher à l’aide de la barre de recherche située en haut de la barre latérale.

Vous pouvez également utiliser la barre latérale dans l’éditeur de [!DNL SQL] pour insérer des mesures, des tableaux et des colonnes directement dans vos requêtes en pointant dessus et en cliquant sur **[!UICONTROL Insert]** :

![Insertion d’un tableau dans l’éditeur de [!DNL SQL].](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>Toute fonction [SELECT](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST), ou toute fonction qui ne mute pas les données, prise en charge par PostgreSQL, est prise en charge dans SQL Report Builder. Cela inclut, sans s’y limiter, AVG, COUNT, COUNT DISTINCT, MIN/MAX et SUM.

En outre, tout type de `JOIN` est pris en charge, mais Adobe recommande de n&#39;utiliser que la JOINTURE INTERNE, car il s&#39;agit du type de `JOIN` le moins coûteux.

## Exécution de la requête et affichage des résultats {#runquery}

Une fois la requête rédigée, cliquez sur **[!UICONTROL Run Query]**. Les résultats s&#39;affichent dans un tableau sous l&#39;éditeur SQL :

![Exécution de la requête et affichage des résultats.](../../assets/SQL_Run_Query.gif)

Si les résultats laissent à désirer, vous pouvez modifier la requête et l’exécuter à nouveau jusqu’à ce que vous soyez satisfait.

Il se peut que des [messages s’affichent sous l’éditeur, avec la mention EXPLAIN](../../best-practices/optimizing-your-sql-queries.md). Si vous voyez l’un de ces éléments, cela signifie que votre requête n’a pas été exécutée et qu’elle nécessite quelques ajustements.

Une fois la modification de la requête terminée, vous pouvez passer à la création d’une visualisation ou à l’enregistrement de votre travail dans un tableau de bord.

## Création d’une visualisation {#createviz}

Pour créer une visualisation avec les résultats de votre requête, cliquez sur l’onglet **[!UICONTROL Chart]** dans le volet `Results`. Dans cet onglet, vous sélectionnez :

* Le `Series` ou la colonne que vous souhaitez mesurer, par exemple **Articles vendus**.
* Le `Category` ou la colonne que vous souhaitez utiliser pour segmenter vos données, comme **source d’acquisition**.
* Les valeurs de l’axe `Labels` ou X.

Voici un aperçu rapide de ce à quoi ressemble le processus de visualisation :

![Démonstration animée de la visualisation SQL Report Builder](../../assets/SQL_RB_viz_overview.gif)

Pour une présentation détaillée de la création d’une visualisation, reportez-vous au tutoriel [Création de visualisations à partir de requêtes SQL](../../tutorials/create-visuals-from-sql.md){: target="_blank"}.

## Enregistrer le rapport {#save}

Avant de pouvoir enregistrer votre travail, vous devez donner un nom au rapport. N’oubliez pas de suivre les [directives relatives aux bonnes pratiques pour l’attribution de noms](../../best-practices/naming-elements.md){: target="_blank"} et de choisir quelque chose qui véhicule clairement le contenu du rapport.

Cliquez sur **[!UICONTROL Save]** dans le coin supérieur droit de l’éditeur de [!DNL SQL] et sélectionnez le `Type` de rapport (`Chart` ou `Table`). Pour conclure, sélectionnez le tableau de bord dans lequel enregistrer le rapport et cliquez sur **[!UICONTROL Save to Dashboard]**.

![Démonstration animée de l&#39;enregistrement d&#39;un rapport SQL dans un tableau de bord](../../assets/SQL_Save_Report.gif)

### Analyse des données

#### [!DNL SQL Report Builder]

[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) vous permet d’interroger directement vos Data Warehouse, d’afficher les résultats et de les transformer rapidement en rapport. L’utilisation de [!DNL SQL] vous permet également [d’utiliser  [!DNL SQL]  fonctions qui ne sont pas disponibles](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) dans le `Visual` ou `Cohort` Report Builder, ce qui vous permet de mieux contrôler vos données.

Les colonnes calculées créées à l’aide de [!DNL SQL] ne dépendent pas des cycles de mise à jour. Vous pouvez donc effectuer une itération sur ces colonnes comme bon vous semble et consulter immédiatement les résultats.

>[!NOTE]
>
>Cela s’applique uniquement à la structure de la colonne, et non à l’actualisation des données. Les nouvelles données dépendent toujours des cycles de mise à jour terminés avec succès.

| **C&#39;est parfait pour...** | **Ce n&#39;est pas si génial pour...** |
|---|---|
| Analystes intermédiaires/avancés | Débutants - vous devez savoir [!DNL SQL]. |
| Le savoir-faire [!DNL SQL] | Des analyses simples : l’écriture d’une requête peut être plus complexe que la simple utilisation de l’[!UICONTROL Visual Report Builder]. |
| Création de colonnes calculées à usage unique | Partage avec d’autres personnes - considérez votre audience : comprend-elle [!DNL SQL] ? Dans le cas contraire, ils risquent d’être déconcertés par la manière dont le rapport est créé. |
| Données avec relations `one-to-many` |  |
| Tester une nouvelle colonne ou analyse |  |

#### Résultats de la comparaison entre la base de données et l’éditeur SQL

La plupart du temps, les différences de résultats peuvent être attribuées aux cycles de mise à jour. Si [!DNL Commerce Intelligence] est en train de répliquer les données de votre base de données vers votre Data Warehouse, il se peut que vous obteniez des résultats différents même si vous utilisez la même requête.

Les problèmes de connexion peuvent également entraîner des incohérences. Accédez à la page `Connections` en cliquant sur **[!DNL Manage Data** > **Connections]** pour l’extraire. L’intégration de base de données en question génère-t-elle une erreur ? Si tel est le cas, vous devrez peut-être [réauthentifier l’intégration](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=fr) pour que les choses fonctionnent à nouveau.

Si toutes vos intégrations sont connectées avec succès et que vous n’êtes pas au milieu d’un cycle de mise à jour, une autre erreur peut se produire.

#### La suppression d’un rapport [!DNL SQL] supprime-t-elle également les colonnes sous-jacentes de mon Data Warehouse ?

Non, vous ne perdez aucune colonne de votre Data Warehouse, quelle que soit la manière dont vous les avez créées.

Les colonnes créées à l’aide du `Data Warehouse Manager` ne sont pas affectées si vous supprimez un rapport ou une requête qui les utilise.

Les colonnes créées à l’aide du [!DNL SQL Report Builder] ne sont pas enregistrées dans votre Data Warehouse.


#### `Report Builder` contre `SQL Report Builder`

Le [!DNL SQL Report Builder] vous offre davantage de flexibilité lors de la création et de la structuration de vos graphiques. Vous pouvez, par exemple, sélectionner les valeurs à afficher sur les axes `X` et `Y`. Pour plus d’informations sur la création de graphiques dans le [!DNL SQL Report Builder], consultez le tutoriel [Création de visualisations à partir  [!DNL SQL]  requêtes](../../tutorials/create-visuals-from-sql.md).

#### `Cohort Report Builder` {#cohortrb}

Contrairement à la [!DNL Visual Report Builder], la [[!DNL Cohort Report Builder]](../dev-reports/cohort-rpt-bldr.md) a un seul objectif : analyser et identifier les tendances comportementales de groupes d’utilisateurs similaires au fil du temps. L&#39;utilisation de la [!DNL Cohort Report Builder] ne nécessite pas de savoir-faire [!DNL SQL], vous pouvez donc plonger sans hésitation si vous débutez.

| **C&#39;est parfait pour...** | **Ce n&#39;est pas si génial pour...** |
|---|---|
| Analystes intermédiaires/avancés | Débutants - vous avez besoin de cohortes qui définissent la pratique. |
| Identifier les tendances comportementales au fil du temps | Analyse qualitative : elle peut être [réalisée](../dev-reports/create-qual-cohort-analysis.md), mais nécessite une assistance Adobe. |

## Reconstruction des requêtes après le cycle de mise à jour

Vous n’avez pas à recréer vos requêtes. Les rapports créés à l’aide du [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) sont enregistrés comme ceux créés dans le `Report Builder` traditionnel. Le processus de mise à jour des graphiques [!DNL SQL] est le même : une fois vos données mises à jour, les valeurs de vos graphiques sont recalculées et réaffichées.

>[!NOTE]
>
>La suppression d’un rapport/d’une requête [!DNL SQL] ne supprime pas les colonnes sous-jacentes de votre Data Warehouse. Vous ne perdez aucune colonne, quelle que soit la manière dont vous les avez créées.

* Les colonnes créées à l’aide du gestionnaire Data Warehouse ne sont pas affectées si vous supprimez un rapport ou une requête qui les utilise.

* Les colonnes créées à l’aide de SQL Report Builder ne sont pas enregistrées dans votre Data Warehouse.

## Conclusion {#wrapup}

Si vous souhaitez essayer quelque chose d’un peu plus difficile, pourquoi ne pas essayer d’écrire une requête optimisée pour la visualisation ? Consultez le tutoriel [Création de visualisations à partir  [!DNL SQL]  requêtes](../../tutorials/create-visuals-from-sql.md){: target="_blank"} pour commencer.
