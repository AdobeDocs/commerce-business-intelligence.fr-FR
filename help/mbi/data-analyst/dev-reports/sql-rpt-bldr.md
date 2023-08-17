---
title: Utilisation du Report Builder SQL
description: Découvrez les avantages et inconvénients de l’utilisation du Report Builder SQL.
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---

# Utilisation [!DNL SQL Report Builder]

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../administrator/user-management/user-management.md) pour créer et modifier des graphiques SQL. `Standard` les utilisateurs peuvent réorganiser ces graphiques dans les tableaux de bord ; et `Read-only` les utilisateurs ont la même expérience qu’avec les graphiques traditionnels. En outre, `Read-only` les utilisateurs n&#39;ont pas accès au texte de la requête.

Voir [vidéo de formation](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html) pour en savoir plus.

[!DNL SQL], ou langage de requête structuré, est un langage de programmation utilisé pour communiquer avec des bases de données. Dans [!DNL Commerce Intelligence], [!DNL SQL] est utilisé pour interroger ou récupérer des données de votre Data Warehouse. Consultez les rapports de votre tableau de bord : en coulisses, chacun est alimenté par une [!DNL SQL] requête.

Vous pouvez utiliser la variable [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) pour interroger directement votre Data Warehouse, affichez les résultats, puis transformez-les en graphique. Vous pouvez commencer à créer un rapport à l’aide de l’événement [!DNL SQL Report Builder] en cliquant **[!UICONTROL Report Builder** > **[!DNL SQL Report Builder]]**.

Voir [vidéo de formation](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html) pour en savoir plus.

La variable [!DNL SQL Report Builder] vous permet d’interroger directement votre Data Warehouse, d’afficher les résultats et de les transformer rapidement en graphique. La meilleure partie concernant l’utilisation de [!DNL SQL] pour créer des rapports, il n’est pas nécessaire d’attendre les cycles de mise à jour pour effectuer une itération sur les colonnes que vous créez. Si les résultats ne semblent pas bons, vous pouvez rapidement modifier et réexécuter la requête jusqu’à ce que les éléments correspondent à vos attentes.

Cette rubrique vous guide tout au long de l’utilisation de la variable [!DNL SQL Report Builder]. Une fois que vous avez pris connaissance de votre parcours, consultez la [!DNL SQL] pour le tutoriel sur les visualisations ou essayez d’optimiser certaines des requêtes que vous avez écrites.

Couvert dans cet article :

1. [Ecriture d&#39;une requête](#writing)

1. [Exécution de la requête et affichage des résultats](#runquery)

1. [Création d’une visualisation](#createviz)

1. [Enregistrer le rapport](#save)

## [!DNL SQL Report Builder] Intégrations

[[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) est la seule intégration indisponible à utiliser avec la variable [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md). Cette fonctionnalité est en cours de développement.

Pour commencer à créer un [!DNL SQL] rapport, cliquez sur **[!UICONTROL Report Builder]** ou **[!UICONTROL Add Report]** en haut de n’importe quel tableau de bord. Dans le [!DNL Report Picker] écran, cliquez sur **[!UICONTROL SQL Report Builder]** pour ouvrir le [!DNL SQL] éditeur.

## Prise en main

Pour modifier un rapport, cliquez sur l’engrenage (![](../../assets/gear-icon.png)) dans le coin supérieur droit d’un [!DNL SQL]Graphique basé sur les balises et clic **[!UICONTROL Edit]**.

## Ecriture d&#39;une requête {#writing}

>[!NOTE]
>
>[!DNL SQL Report Builder] les requêtes sont sensibles à la casse. Assurez-vous d’utiliser la bonne casse lors de l’écriture de requêtes ou vous risquez de générer des résultats ou des erreurs inattendus.

En procédant comme suit : [directives relatives à l’optimisation des requêtes](../../best-practices/optimizing-your-sql-queries.md), écrivez une requête dans le [!DNL SQL] éditeur.

>[!IMPORTANT]
>
>**Mesures dans [!DNL SQL] rapports** - Lorsque vous insérez une mesure dans un rapport SQL, la variable `current definition` de la mesure est utilisée.

Si la mesure est mise à jour ultérieurement, le rapport SQL *ne fait pas* reflètent les modifications. Vous devez modifier manuellement le rapport pour que les modifications soient prises en compte.

À l’aide des boutons situés en haut de la barre latérale, vous pouvez permuter entre les listes de tableaux et les mesures disponibles dans la variable [!DNL SQL Report Builder]. Si vous ne voyez pas ce que vous recherchez dans la liste, essayez de le rechercher à l’aide de la barre de recherche située en haut de la barre latérale.

Vous pouvez également utiliser la barre latérale dans la variable [!DNL SQL] pour insérer des mesures, des tableaux et des colonnes directement dans vos requêtes en pointant dessus et en cliquant sur **[!UICONTROL Insert]**:

![Insérer un tableau dans le [!DNL SQL] éditeur.](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>Quelconque [Fonction SELECT](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST), ou toute fonction qui ne mute pas de données, prise en charge par PostgreSQL est prise en charge dans le Report Builder SQL. Cela inclut, sans s’y limiter, les mesures AVG, COUNT, COUNT DISTINCT, MIN/MAX et SUM.

Aussi, n’importe quel `JOIN` Le type est pris en charge, mais Adobe recommande uniquement d’utiliser INNER JOIN, car il est le moins cher de la variable `JOIN` types.

## Exécution de la requête et affichage des résultats {#runquery}

Lorsque vous avez terminé d’écrire votre requête, cliquez sur **[!UICONTROL Run Query]**. Les résultats s’affichent dans un tableau sous l’éditeur SQL :

![Exécution de la requête et affichage des résultats.](../../assets/SQL_Run_Query.gif)

Si les résultats semblent ternes, vous pouvez modifier la requête et la réexécuter jusqu’à ce que vous soyez satisfait.

Parfois, vous verrez [messages sous l’éditeur contenant EXPLAIN](../../best-practices/optimizing-your-sql-queries.md). Si vous voyez l’un d’eux, cela signifie que votre requête n’a pas été exécutée et nécessite un ajustement.

Une fois la requête modifiée, vous pouvez passer à la création d’une visualisation ou à l’enregistrement de votre travail dans un tableau de bord.

## Création d’une visualisation {#createviz}

Pour créer une visualisation avec les résultats de la requête, cliquez sur le bouton **[!UICONTROL Chart]** dans le `Results` volet. Dans cet onglet, vous sélectionnez :

* La variable `Series`ou la colonne à mesurer, telle que **Articles vendus**.
* La variable `Category`ou la colonne que vous souhaitez utiliser pour segmenter vos données, par exemple **source d&#39;acquisition**.
* La variable `Labels`ou les valeurs de l’axe X.

Voici un aperçu rapide du processus de visualisation :

![](../../assets/SQL_RB_viz_overview.gif)

Pour une présentation détaillée de la création d’une visualisation, reportez-vous à la section [Tutoriel sur la création de visualisations à partir de requêtes SQL](../../tutorials/create-visuals-from-sql.md){ : target=&quot;_blank&quot;}.

## Enregistrer le rapport {#save}

Avant de pouvoir enregistrer votre travail, vous devez donner un nom au rapport. N’oubliez pas de suivre le [bonnes pratiques relatives à l’attribution de noms](../../best-practices/naming-elements.md){: target=&quot;_blank&quot;} et choisissez quelque chose qui véhicule clairement ce qu’est le rapport !

Cliquez sur **[!UICONTROL Save]** dans le coin supérieur droit du [!DNL SQL] et sélectionnez le rapport `Type` (`Chart` ou `Table`). Pour terminer, sélectionnez le tableau de bord dans lequel enregistrer le rapport et cliquez sur **[!UICONTROL Save to Dashboard]**.

![](../../assets/SQL_Save_Report.gif)

### Analyse de vos données

#### [!DNL SQL Report Builder]

[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) vous donne la possibilité d’interroger directement votre Data Warehouse, d’afficher les résultats et de les transformer rapidement en rapport. Utilisation [!DNL SQL] vous permet également de [pour utiliser [!DNL SQL] fonctions non disponibles](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) dans le `Visual` ou `Cohort` Reports Builder, ce qui vous permet de mieux contrôler vos données.

Colonnes calculées créées à l’aide de [!DNL SQL] ne dépendent pas des cycles de mise à jour, ce qui signifie que vous pouvez les itérer comme vous le souhaitez et voir immédiatement les résultats.

>[!NOTE]
>
>Cela ne s&#39;applique qu&#39;à la structure de la colonne, et non à l&#39;actualisation des données. Les nouvelles données dépendent toujours des cycles de mise à jour terminés avec succès.

| **C&#39;est parfait pour...** | **Ce n&#39;est pas si bien pour...** |
|---|---|
| Analystes intermédiaires/avancés | Débutants - vous devez savoir [!DNL SQL]. |
| La variable [!DNL SQL] savvy | Analyses simples : l’écriture d’une requête peut s’avérer plus efficace que l’utilisation de la fonction [!UICONTROL Visual Report Builder]. |
| Création de colonnes calculées à usage unique | Partage avec d&#39;autres - considérez votre audience : comprennent-ils [!DNL SQL]? Dans le cas contraire, ils peuvent être perturbés par la manière dont le rapport est créé. |
| Données avec `one-to-many` relations |  |
| Test d&#39;une nouvelle colonne ou analyse |  |

#### Résultats de la base de données et de l’éditeur SQL

La plupart du temps, les différences de résultats peuvent être attribuées aux cycles de mise à jour. If [!DNL Commerce Intelligence] est en train de répliquer les données de votre base de données vers votre Data Warehouse ; il se peut que vous obteniez des résultats différents même lors de l’utilisation de la même requête.

Les problèmes de connexion peuvent également entraîner des incohérences. Accédez au `Connections` en cliquant sur **[!DNL Manage Data** > **Connections]** pour l’extraire : y a-t-il une erreur pour l’intégration de la base de données en question ? Si tel est le cas, vous devrez peut-être [réauthentifier l’intégration](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html) pour que les choses recommencent.

Si toutes vos intégrations sont connectées avec succès et que vous n’êtes pas au milieu d’un cycle de mise à jour, il peut y avoir autre chose à faire.

#### La suppression d’une [!DNL SQL] supprimer également les colonnes sous-jacentes de mon Data Warehouse ?

Non, vous ne perdez aucune colonne de votre Data Warehouse, quelle que soit la manière dont vous les avez créées.

Colonnes créées à l’aide du `Data Warehouse Manager` ne sont pas affectés si vous supprimez un rapport ou une requête qui les utilise.

Colonnes créées à l’aide du [!DNL SQL Report Builder] ne sont pas enregistrés dans votre Data Warehouse.


#### `Report Builder` versus `SQL Report Builder`

La variable [!DNL SQL Report Builder] vous offre davantage de flexibilité lors de la création et de la structuration de vos graphiques. Vous pouvez, par exemple, sélectionner les valeurs à afficher sur le `X` et `Y` axes. Pour plus d’informations sur la création de graphiques dans le [!DNL SQL Report Builder], extrayez le [Création de visualisations à partir de [!DNL SQL] requêtes](../../tutorials/create-visuals-from-sql.md) tutoriel .

#### `Cohort Report Builder` {#cohortrb}

Contrairement à la variable [!DNL Visual Report Builder], la variable [[!DNL Cohort Report Builder]](../dev-reports/cohort-rpt-bldr.md) est destiné à un seul objectif : analyser et identifier les tendances comportementales de groupes d’utilisateurs similaires au fil du temps. En utilisant la variable [!DNL Cohort Report Builder] ne nécessite pas [!DNL SQL] savourer, pour pouvoir plonger sans hésiter si vous commencez.

| **C&#39;est parfait pour...** | **Ce n&#39;est pas si bien pour...** |
|---|---|
| Analystes intermédiaires/avancés | Débutants : vous avez besoin de cohortes définissant les pratiques. |
| Identification des tendances comportementales au fil du temps | L&#39;analyse qualitative, ça peut être [done](../dev-reports/create-qual-cohort-analysis.md), mais nécessite une assistance Adobe. |

## Reconstruire les requêtes après le cycle de mise à jour

Vous n’avez pas à recréer vos requêtes. Rapports créés à l’aide de la variable [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) sont sauvés comme ceux créés dans les `Report Builder`. Le processus de mise à jour pour [!DNL SQL] les graphiques sont les mêmes : une fois vos données mises à jour, les valeurs de vos graphiques seront recalculées et affichées à nouveau.

>[!NOTE]
>
>Lors de la suppression d’une [!DNL SQL] report/requête, il ne supprime pas les colonnes sous-jacentes de votre Data Warehouse. Vous ne perdez aucune colonne, quelle que soit la manière dont vous les avez créées.

* Les colonnes créées à l’aide du Gestionnaire de Data Warehouse ne sont pas affectées si vous supprimez un rapport ou une requête qui les utilise.

* Les colonnes créées à l’aide du Report Builder SQL ne sont pas enregistrées dans votre Data Warehouse.

## Remplissage {#wrapup}

Si vous souhaitez essayer quelque chose d’un peu plus difficile, pourquoi ne pas essayer d’écrire une requête optimisée pour la visualisation ? Consultez la section [Création de visualisations à partir de [!DNL SQL] tutoriel sur les requêtes](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;} pour commencer.
