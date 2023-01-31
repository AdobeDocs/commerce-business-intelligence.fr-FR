---
title: Utiliser les options d’heure dans le Report Builder visuel
description: Découvrez comment analyser les données de votre rapport pour une période spécifique.
exl-id: a1bb4838-f882-44b1-a29f-84b985032ceb
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 0%

---

# Utilisation `Time` Options dans `Visual Report Builder`

L’une des fonctionnalités des `Visual Report Builder` est la variable globale `Time Range` et `Interval` paramètres. Ces paramètres vous permettent d’analyser les données de votre rapport pendant une période spécifique.

Cependant, pour certaines analyses, vous devrez peut-être tenir compte de périodes ou d’intervalles dans le même rapport. C&#39;est là que nous en sommes `Time` Les options entrent. Pour vous donner une meilleure idée de la manière d’utiliser `Time` Dans vos rapports, ce tutoriel abordera les cas d’utilisation suivants :

* [Analyse des mesures sans horodatage](#notimestamp)
* [Octroi à une mesure d’un intervalle de temps indépendant](#independenttimeinterval)
* [Comparaison de la même mesure sur différentes périodes](#difftimerange)

Si vous souhaitez suivre certains des exemples de rapports abordés dans cette rubrique, ouvrez le [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md) avant de continuer.

## Analyse des mesures sans horodatage {#notimestamp}

Certaines mesures ne peuvent pas simplement suivre la tendance au fil du temps, car les données ne sont pas collectées ni stockées avec un horodatage associé. Par exemple, un tableau d’inventaire ne contient souvent qu’une seule ligne pour chaque SKU. Dans ce cas, vous devez [création de la mesure](../data-user/reports/ess-manage-data-metrics.md) sans spécifier d’horodatage.

Lors de l’utilisation d’une telle mesure dans vos rapports, vous remarquerez que l’ajout de cette mesure à un rapport définit automatiquement une `Time Interval` de `None` et `Time Range` de `Global`:

![](../assets/Metrics_without_timestamps.gif)

## Octroi à une mesure d’un intervalle de temps indépendant {#independenttimeinterval}

`Time` Les options vous permettent de créer des graphiques à 100 % basés sur le temps afin d’identifier le jour, la semaine, le mois ou l’année qui ont le plus contribué à une période donnée. Dans cette section, nous créons un graphique qui présente le pourcentage des recettes générées au cours de chaque mois calendaire de l&#39;année.

Ce type de rapport peut s’avérer utile si vous souhaitez comparer les recettes générées d’une année à l’autre. Par exemple, si un graphique pour 2015 révèle que janvier a contribué à hauteur de 18 % des recettes pour l&#39;année et qu&#39;un graphique pour 2016 n&#39;a montré que 8 %, vous pouvez commencer à chercher ce qui aurait pu se produire.

1. Ajoutez vos `Revenue` au rapport.
1. Cliquez sur **[!UICONTROL Duplicate]** pour effectuer une copie de la mesure.
1. Cliquez sur la variable globale **[!UICONTROL Time Range]** , puis **[!UICONTROL Moving Time Range]**. Définissez cette variable sur `Last Year`.
1. Cliquez sur la variable globale **[!UICONTROL Time Interval]** et définissez-la sur `Monthly`.
1. Report Builder ajoute automatiquement un second axe Y pour une seconde mesure. Désélectionnez l’option `Multiple Y-Axes` de la boîte.
1. Ensuite, nous appliquons une `Time Interval` à la première mesure. Cliquez sur **[!UICONTROL Time Options]** (icône d’horloge) à droite de la `first Revenue metric`.
1. Cliquez sur **[!UICONTROL Time Options]** dans la fenêtre développée qui s’affiche au-dessus du rapport.
1. Dans la liste déroulante, définissez les options suivantes :

   * `Time Interval`: Définissez cette variable sur `None`.

   * `Time Range`: Définissez cette variable sur `Last Year` par le premier clic **[!UICONTROL Custom]**, puis **[!UICONTROL Moving Range]**, puis enfin, en sélectionnant le `Last Year` .

   * Cliquez sur **[!UICONTROL Apply]** pour enregistrer les paramètres d’intervalle et de plage. Cela crée une mesure qui calcule le total des recettes de l’année précédente. Ensuite, nous utilisons cette mesure comme dénominateur dans une formule.

   * Pour afficher le pourcentage des recettes pour chaque mois, nous devons ajouter une formule au rapport. Cliquez sur **[!UICONTROL Add Formula]**.

   * Entrée `B/A` dans le champ de formule et sélectionnez `% Percent` dans la liste déroulante en regard du champ de texte. Cette formule divise le montant des recettes d’un mois spécifique l’année dernière par le montant total des recettes de l’année dernière.

   * Cliquez sur **[!UICONTROL Apply Changes]**.

   * Masquez les deux mesures d’entrée et renommez la formule.

Maintenant, nous pouvons voir à quel point chaque mois a eu un impact l&#39;année dernière :

![](../assets/Independent_Time_Int.png)

## Comparaison de la même mesure sur différentes périodes {#difftimerange}

Cet exemple utilise une dimension personnalisée appelée `Day number of the month`. Si vous souhaitez créer ce rapport et que vous ne disposez pas déjà de cette dimension dans votre Data Warehouse, [support technique](../guide-overview.md) pour obtenir de l’aide.

Les deux exemples les plus courants dans cette catégorie sont (1) la comparaison des mesures de croissance (recettes d’une année à l’autre ou d’un mois à l’autre) et (2) une meilleure compréhension des tendances récentes de ventes d’inventaire ou d’article.

Pour illustrer ce cas d’utilisation, nous examinons les recettes quotidiennes du mois précédent par rapport au même mois de l’année précédente. Imaginons que nous souhaitions examiner les recettes pour chaque jour de janvier 2016, puis les comparer à janvier 2015, janvier 2014, et ainsi de suite - ce rapport nous le montrerait.

1. Ajoutez vos `Revenue` au rapport.
1. Cliquez sur **[!UICONTROL Duplicate]** pour effectuer une copie de la mesure.
1. Renommez la première mesure en `Items sold last 7 days` et la deuxième mesure à `Items sold last 28 days`.
1. Cliquez sur **[!UICONTROL Time Range]**, puis **[!UICONTROL Moving Time Range]**. Définissez cette variable sur `Last Month`.
1. Cliquez sur **[!UICONTROL Time Interval]** et définissez-le sur `None`.
1. Cliquez sur **[!UICONTROL Time Options]** (icône d’horloge) en regard de la seconde `Revenue` mesure.
1. Cliquez sur **[!UICONTROL Time Options]** dans la fenêtre développée qui s’affiche au-dessus du rapport.
1. Dans la liste déroulante, définissez les options suivantes :

   * `Time Interval`: Définissez cette variable sur `None`.

   * `Time Range`: Définissez cette variable sur `From 14 Months Ago To 13 Months Ago` par le premier clic **[!UICONTROL Custom]** then **[!UICONTROL Moving Range]**. Pour définir la plage, utilisez les champs et les listes déroulantes dans la partie supérieure du menu. Ce paramètre nous permet d’afficher les recettes du mois précédent, mais de l’année précédente.
   Ne vous inquiétez pas si la mesure disparaît du rapport. La définition d’une option de temps indépendante masque automatiquement la mesure du rapport. Pour le réafficher, cliquez sur **[!UICONTROL Show]** en regard de la mesure.

   ![](../assets/Different_Time_Ranges.gif)

   * Cliquez sur **[!UICONTROL Apply]** pour enregistrer les paramètres d’intervalle et de plage.

   * Ensuite, nous ajoutons notre personnalisé `Day number of the month` dimension en cliquant sur **[!UICONTROL Group By]** et en sélectionnant la dimension. Cela renverra le numéro du jour du mois d’une commande ; par exemple, une commande passée le 2 mars renverra `2`.

   * Dans le `Group By` menu déroulant, sélectionnez `Show All` et cliquez sur **[!UICONTROL Apply]**. Les valeurs de l’axe X du rapport seront ainsi créées :

   ![](../assets/TO4.png)

   * Renommez les mesures. Dans notre exemple, la première mesure est `Revenue - 2015` et le second est `Revenue - 2014`.



Autre utilisation courante de la personnalisation `Time Options` est de déterminer les semaines d’approvisionnement. En particulier pendant la période des fêtes ou une période promotionnelle spéciale, vous pouvez considérer les articles vendus au cours de la dernière semaine, du mois et de la période promotionnelle précédente pour prendre des décisions d’achat éclairées.

N’oubliez pas de définir vous-même les plages de temps à ce dont vous avez besoin lors de la création de ce rapport.

1. Ajoutez vos `Items Sold` au rapport.
1. Cliquez sur **[!UICONTROL Duplicate]** pour effectuer une copie de la mesure.
1. Renommez les mesures. Vous pouvez utiliser les mêmes noms que nous, ou utiliser quelque chose de similaire :
   1. Renommez la première mesure en `Items sold last 7 days`.
   1. Renommez la seconde mesure en `Items sold last 28 days`.
1. Sur le `Items sold last 7 days` , cliquez sur la mesure globale **[!UICONTROL Time Range]** option alors **[!UICONTROL Moving Time Range]**. Pour cet exemple, nous l’avons défini sur `Last 7 Days`.
1. Cliquez sur **[!UICONTROL Time Interval]** et définissez-le sur `None`.
1. Ensuite, nous définissons la variable `Time Options` pour le `Items sold last 28 days` mesure. Cliquez sur **[!UICONTROL Time Options]** (icône d’horloge) à droite de la `second Items sold` mesure.
1. Cliquez sur **[!UICONTROL Time Options]** dans la fenêtre développée qui s’affiche au-dessus du rapport.
1. Dans la liste déroulante, définissez les options suivantes :

   * `Time Interval`: Définissez cette variable sur `None`.
   * `Time Range`: Définissez cette variable sur `From 29 days to 1 day ago` par le premier clic **[!UICONTROL Custom]**, puis **[!UICONTROL Moving Range]**. Pour définir la plage, utilisez les champs et les listes déroulantes dans la partie supérieure du menu.
   * Cliquez sur **[!UICONTROL Apply]** pour enregistrer les paramètres d’intervalle et de plage.
   * Dupliquez la variable `Items sold last 28 days` et ouvrez la nouvelle mesure `Time Options`. Définissez les options suivantes :

      * `Time Interval`: laissez ceci comme `None`.
      * `Time Range`: modifiez la date selon la période qui s’aligne sur la promotion qui vous intéresse en cliquant sur **[!UICONTROL Specific Date Range]** puis saisissez les dates appropriées.
      * Renommer la mesure `Items sold during last promotion` ou quelque chose de similaire.
      * Ajoutez vos `Units on hand` mesure.
      * Nous devons ensuite ajouter les calculs qui montrent les semaines en cours, en tenant compte des tendances de vente, pour les périodes (`last 7 days`, `last 28 days`, et `last promo` (point) que nous incluons dans le rapport. Vous devez effectuer cette opération une fois pour chaque période.

Pour créer les formules, cliquez sur **[!UICONTROL Add Formula]**. Saisissez la formule ci-dessous et cliquez sur **[!UICONTROL Apply Changes]** lorsque vous avez terminé. Répétez cette opération pour chacune des trois périodes :

* Pour le `last 7 days time period`, saisissez `D / A` dans le `Formula` champ .
* Pour le `last 28 days time period`, saisissez `D / (B/4)` dans le `Formula` champ .

   >[!NOTE]
   >
   >Il est important de normaliser ici les périodes sélectionnées. Dans cet exemple, 28 jours doivent être divisés en quatre semaines. Vous devrez peut-être appliquer une logique différente à la formule.

* Pour le `last promo period`, saisissez `D / C` dans le `Formula` champ .

   ![](../assets/Different_Time_Ranges_2.png)

* Enfin, personnalisez le rapport en masquant les mesures et en ajoutant une `SKU` ou une dimension similaire au rapport en tant que `Group By`.

Cet exemple montre que les niveaux d’inventaire actuels étaient bien positionnés pour une vente de 14 jours à l’échelle du produit. Cependant, l&#39;ajout d&#39;une période promotionnelle comparable suggère que l&#39;entreprise doit apporter des changements, soit en commandant plus d&#39;inventaire, soit en faisant uniquement la promotion des articles ayant suffisamment d&#39;unités en stock.

Étant donné que vos clients se comportent différemment au fil du temps, vous pouvez vous attendre à voir les écarts de données lors d’analyses. La définition d’options de temps personnalisées vous permet de créer rapidement des analyses complexes, ce qui vous permet de prendre des décisions basées sur les données qui tiennent compte des tendances historiques.

Voir notre [vidéo de formation](https://support.magento.com/hc/en-us/articles/360016730071-Training-Video-Time-Options-in-the-Visual-Report-Builder) pour en savoir plus.
