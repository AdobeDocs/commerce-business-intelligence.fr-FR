---
title: Utiliser les options d’heure dans le Report Builder visuel
description: Découvrez comment analyser les données de votre rapport pour une période spécifique.
exl-id: a1bb4838-f882-44b1-a29f-84b985032ceb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 0%

---

# Utiliser les options [!DNL Time] dans [!DNL Visual Report Builder]

L’une des fonctionnalités de [!DNL Visual Report Builder] est les paramètres globaux `Time Range` et `Interval`. Ces paramètres vous permettent d’analyser les données de votre rapport pendant une période spécifique.

Cependant, pour certaines analyses, vous devrez peut-être tenir compte de périodes ou d’intervalles dans le même rapport. C’est là que les options `Time` entrent en jeu. Pour vous donner une meilleure idée de l’utilisation des options `Time` dans vos rapports, ce tutoriel couvre les cas d’utilisation suivants :

* [Analyse des mesures sans horodatage](#notimestamp)
* [Octroi à une mesure d’un intervalle de temps indépendant](#independenttimeinterval)
* [Comparaison de la même mesure sur différentes périodes](#difftimerange)

Si vous souhaitez suivre certains des exemples de rapports abordés dans cette rubrique, ouvrez le [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md) avant de continuer.

## Analyse des mesures sans horodatage {#notimestamp}

Certaines mesures ne peuvent pas simplement suivre la tendance au fil du temps, car les données ne sont pas collectées ni stockées avec un horodatage associé. Par exemple, un tableau d’inventaire ne contient souvent qu’une seule ligne pour chaque SKU. Dans ce cas, [créez la mesure](../data-user/reports/ess-manage-data-metrics.md) sans spécifier d’horodatage.

Lors de l’utilisation d’une telle mesure dans vos rapports, vous remarquerez que l’ajout de cette mesure à un rapport définit automatiquement un `Time Interval` indépendant de `None` et un `Time Range` de `Global` :

![](../assets/Metrics_without_timestamps.gif)

## Octroi à une mesure d’un intervalle de temps indépendant {#independenttimeinterval}

`Time` Les options vous permettent de créer des graphiques à 100 % basés sur le temps afin d’identifier le jour, la semaine, le mois ou l’année qui ont apporté la plus grande valeur au cours d’une période spécifique. Dans cette section, vous créez un graphique qui présente le pourcentage des recettes générées au cours de chaque mois calendaire de l&#39;année.

Ce type de rapport peut s’avérer utile si vous souhaitez comparer les recettes générées d’une année à l’autre. Par exemple, vous avez un graphique pour 2015 qui révèle que janvier a contribué à 18 % des recettes de l’année et un graphique pour 2016 n’a montré que 8 %. Vous pourriez commencer à faire des recherches sur ce qui aurait pu arriver.

1. Ajoutez la mesure `Revenue` au rapport.
1. Cliquez sur **[!UICONTROL Duplicate]** pour effectuer une copie de la mesure.
1. Cliquez sur l’option globale **[!UICONTROL Time Range]**, puis **[!UICONTROL Moving Time Range]**. Définissez-le sur `Last Year`.
1. Cliquez sur l’option globale **[!UICONTROL Time Interval]** et définissez-la sur `Monthly`.
1. Report Builder ajoute automatiquement un second axe Y pour une seconde mesure. Désélectionnez la zone `Multiple Y-Axes`.
1. Ensuite, vous appliquez un `Time Interval` indépendant à la première mesure. Cliquez sur **[!UICONTROL Time Options]** (icône de l’horloge) à droite de `first Revenue metric`.
1. Cliquez sur **[!UICONTROL Time Options]** dans la fenêtre étendue qui s’affiche au-dessus du rapport.
1. Dans la liste déroulante, définissez les options suivantes :

   * `Time Interval` : définissez cette variable sur `None`.

   * `Time Range` : définissez cette variable sur `Last Year` en cliquant d’abord sur **[!UICONTROL Custom]**, puis sur **[!UICONTROL Moving Range]**, et en sélectionnant enfin l’option `Last Year`.

   * Cliquez sur **[!UICONTROL Apply]** pour enregistrer les paramètres d’intervalle et de plage. Cela crée une mesure qui calcule le total des recettes de l’année précédente. Ensuite, vous utilisez cette mesure comme dénominateur dans une formule.

   * Pour afficher le pourcentage des recettes pour chaque mois, vous devez ajouter une formule au rapport. Cliquez sur **[!UICONTROL Add Formula]**.

   * Saisissez `B/A` dans le champ de formule et sélectionnez `% Percent` dans la liste déroulante en regard du champ de texte. Cette formule divise le montant des recettes d’un mois spécifique l’année dernière par le montant total des recettes de l’année dernière.

   * Cliquez sur **[!UICONTROL Apply Changes]**.

   * Masquez les deux mesures d’entrée et renommez la formule.

Vous pouvez voir à quel point chaque mois a eu un impact l&#39;année dernière :

![](../assets/Independent_Time_Int.png)

## Comparaison de la même mesure sur différentes périodes {#difftimerange}

Cet exemple utilise une dimension personnalisée appelée `Day number of the month`. Si vous souhaitez créer ce rapport et que vous ne disposez pas déjà de cette dimension dans votre Data Warehouse, [contactez l&#39;assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) pour obtenir de l&#39;aide.

Les deux exemples les plus courants dans cette catégorie sont (1) la comparaison des mesures de croissance (recettes d’une année à l’autre ou d’un mois à l’autre) et (2) une meilleure compréhension des tendances récentes de ventes d’inventaire ou d’article.

Pour illustrer ce cas d’utilisation, comparez les recettes quotidiennes du mois précédent au même mois de l’année précédente. Supposons que vous souhaitiez consulter les recettes pour chaque jour de janvier 2016, puis les comparer à janvier 2015, janvier 2014, etc. - ce rapport nous le montrerait.

1. Ajoutez la mesure `Revenue` au rapport.
1. Cliquez sur **[!UICONTROL Duplicate]** pour effectuer une copie de la mesure.
1. Renommez la première mesure en `Items sold last 7 days` et la seconde en `Items sold last 28 days`.
1. Cliquez sur **[!UICONTROL Time Range]**, puis sur **[!UICONTROL Moving Time Range]**. Définissez-le sur `Last Month`.
1. Cliquez sur **[!UICONTROL Time Interval]** et définissez-le sur `None`.
1. Cliquez sur **[!UICONTROL Time Options]** (icône représentant une horloge) en regard de la seconde mesure `Revenue`.
1. Cliquez sur **[!UICONTROL Time Options]** dans la fenêtre étendue qui s’affiche au-dessus du rapport.
1. Dans la liste déroulante, définissez les options suivantes :

   * `Time Interval` : définissez cette variable sur `None`.

   * `Time Range` : définissez cette variable sur `From 14 Months Ago To 13 Months Ago` en cliquant d’abord sur **[!UICONTROL Custom]**, puis sur **[!UICONTROL Moving Range]**. Pour définir la plage, utilisez les champs et les listes déroulantes dans la partie supérieure du menu. Ce paramètre nous permet d’afficher les recettes du mois précédent, mais de l’année précédente.

   Ne vous inquiétez pas si la mesure disparaît du rapport. La définition d’une option d’heure indépendante masque automatiquement la mesure du rapport. Pour le réafficher, cliquez sur **[!UICONTROL Show]** en regard de la mesure.

   ![](../assets/Different_Time_Ranges.gif)

   * Cliquez sur **[!UICONTROL Apply]** pour enregistrer les paramètres d’intervalle et de plage.

   * Ensuite, vous ajoutez votre dimension `Day number of the month` personnalisée en cliquant sur **[!UICONTROL Group By]** et en sélectionnant la dimension. Cela renverra le numéro du jour du mois d’une commande ; par exemple, une commande passée le 2 mars renverra `2`.

   * Dans la liste déroulante `Group By`, sélectionnez `Show All` et cliquez sur **[!UICONTROL Apply]**. Les valeurs de l’axe X sont ainsi créées pour le rapport :

   ![](../assets/TO4.png)

   * Renommez les mesures. Dans l’exemple, la première mesure est `Revenue - 2015` et la seconde est `Revenue - 2014`.

Une autre utilisation courante de `Time Options` personnalisé consiste à déterminer les semaines d&#39;approvisionnement. En particulier pendant la période des fêtes ou une période promotionnelle spéciale, vous pouvez considérer les articles vendus au cours de la dernière semaine, du mois et de la période promotionnelle précédente pour prendre des décisions d’achat éclairées.

N’oubliez pas de définir vous-même les plages de temps à ce dont vous avez besoin lors de la création de ce rapport.

1. Ajoutez la mesure `Items Sold` au rapport.
1. Cliquez sur **[!UICONTROL Duplicate]** pour effectuer une copie de la mesure.
1. Renommez les mesures. Vous pouvez utiliser les mêmes noms ou un élément similaire :
   1. Renommez la première mesure en `Items sold last 7 days`.
   1. Renommez la seconde mesure en `Items sold last 28 days`.
1. Sur la mesure `Items sold last 7 days`, cliquez sur l’option globale **[!UICONTROL Time Range]** , puis sur **[!UICONTROL Moving Time Range]**. Pour cet exemple, définissez-le sur `Last 7 Days`.
1. Cliquez sur **[!UICONTROL Time Interval]** et définissez-le sur `None`.
1. Ensuite, vous définissez le `Time Options` pour la mesure `Items sold last 28 days`. Cliquez sur **[!UICONTROL Time Options]** (icône représentant une horloge) à droite de la mesure `second Items sold`.
1. Cliquez sur **[!UICONTROL Time Options]** dans la fenêtre étendue qui s’affiche au-dessus du rapport.
1. Dans la liste déroulante, définissez les options suivantes :

   * `Time Interval` : définissez cette variable sur `None`.
   * `Time Range` : définissez cette variable sur `From 29 days to 1 day ago` en cliquant d’abord sur **[!UICONTROL Custom]**, puis sur **[!UICONTROL Moving Range]**. Pour définir la plage, utilisez les champs et les listes déroulantes dans la partie supérieure du menu.
   * Cliquez sur **[!UICONTROL Apply]** pour enregistrer les paramètres d’intervalle et de plage.
   * Dupliquez la mesure `Items sold last 28 days` et ouvrez la nouvelle mesure `Time Options`. Définissez les options suivantes :

      * `Time Interval` : conservez cette valeur `None`.
      * `Time Range` : remplacez cette valeur par la période qui s’aligne sur la promotion qui vous intéresse en cliquant sur **[!UICONTROL Specific Date Range]**, puis en saisissant les dates appropriées.
      * Renommez la mesure `Items sold during last promotion` ou un nom similaire.
      * Ajoutez la mesure `Units on hand`.
      * Ensuite, vous devez ajouter les calculs qui nous montrent les semaines en cours, en tenant compte des tendances de vente, pour les périodes (`last 7 days`, `last 28 days` et `last promo`) que vous incluez dans le rapport. Vous devez le faire une seule fois pour chaque période.

Pour créer les formules, cliquez sur **[!UICONTROL Add Formula]**. Saisissez la formule ci-dessous et cliquez sur **[!UICONTROL Apply Changes]** lorsque vous avez terminé. Répétez cette opération pour chacune des trois périodes :

* Pour le `last 7 days time period`, saisissez `D / A` dans le champ `Formula` .
* Pour le `last 28 days time period`, saisissez `D / (B/4)` dans le champ `Formula` .

  >[!NOTE]
  >
  >Il est important de normaliser ici les périodes sélectionnées. Ventilez 28 jours en quatre semaines dans cet exemple. Vous devrez peut-être appliquer une logique différente à la formule.

* Pour le `last promo period`, saisissez `D / C` dans le champ `Formula` .

  ![](../assets/Different_Time_Ranges_2.png)

* Enfin, personnalisez le rapport en masquant les mesures et en ajoutant `SKU` ou une dimension similaire au rapport sous la forme `Group By`.

Cet exemple montre que les niveaux d’inventaire actuels étaient bien positionnés pour une vente de 14 jours à l’échelle du produit. Cependant, l&#39;ajout d&#39;une période promotionnelle comparable suggère que l&#39;entreprise doit apporter des changements, soit en commandant plus d&#39;inventaire, soit en faisant uniquement la promotion des articles ayant suffisamment d&#39;unités en stock.

Étant donné que vos clients se comportent différemment au fil du temps, vous pouvez vous attendre à voir les écarts de données lors d’analyses. La définition d’options de temps personnalisées vous permet de créer rapidement des analyses complexes, ce qui vous permet de prendre des décisions basées sur les données qui tiennent compte des tendances historiques.

