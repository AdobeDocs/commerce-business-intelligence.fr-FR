---
title: Utilisation des options de temps dans Visual Report Builder
description: Découvrez comment analyser les données de votre rapport pour une période spécifique.
exl-id: a1bb4838-f882-44b1-a29f-84b985032ceb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 0%

---

# Utilisation des options de [!DNL Time] dans [!DNL Visual Report Builder]

L’une des fonctionnalités de la [!DNL Visual Report Builder] est la `Time Range` globale et les paramètres de `Interval`. Ces paramètres vous permettent d’analyser les données de votre rapport pendant une période spécifique.

Cependant, pour certaines analyses, vous devrez peut-être tenir compte de différentes périodes ou intervalles de temps dans le même rapport. C&#39;est là que `Time` options entrent en jeu. Pour vous donner une meilleure idée de l’utilisation des options de `Time` dans vos rapports, ce tutoriel couvre les cas d’utilisation suivants :

* [Analyse des mesures sans horodatage](#notimestamp)
* [Assignation d’un intervalle de temps indépendant à une mesure](#independenttimeinterval)
* [Comparaison d’une même mesure sur différentes périodes](#difftimerange)

Si vous souhaitez suivre certains des exemples de rapports abordés dans cette rubrique, ouvrez le [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md) avant de continuer.

## Analyse des mesures sans horodatage {#notimestamp}

Certaines mesures ne peuvent simplement pas suivre la tendance au fil du temps, car les données ne sont pas collectées ou stockées avec un horodatage associé. Par exemple, une table d’inventaire ne contient souvent qu’une seule ligne pour chaque SKU. Dans ce cas, vous devez [créer la mesure](../data-user/reports/ess-manage-data-metrics.md) sans spécifier d’horodatage.

Lors de l’utilisation d’une telle mesure dans vos rapports, vous remarquerez que l’ajout de cette mesure à un rapport définit automatiquement un `Time Interval` indépendant de `None` et de `Time Range` de `Global` :

![Rapport affichant la mesure avec l’intervalle de temps défini sur Aucun et la période définie sur Global](../assets/Metrics_without_timestamps.gif)

## Assignation d’un intervalle de temps indépendant à une mesure {#independenttimeinterval}

`Time` options vous permettent de créer des graphiques à 100 % temporels afin d’identifier le jour, la semaine, le mois ou l’année ayant apporté le plus de valeur au cours d’une période spécifique. Dans cette section, créez un graphique qui indique le pourcentage du chiffre d’affaires généré pour chaque mois civil d’une année.

Ce type de rapport peut s&#39;avérer utile si vous souhaitez comparer les revenus générés d&#39;une année sur l&#39;autre. Par exemple, vous avez un graphique pour 2015 qui révèle que janvier a contribué à 18 % des revenus de l&#39;année et un graphique pour 2016 qui montre seulement 8 %. Vous pourriez commencer à chercher ce qui a pu se passer.

1. Ajoutez votre mesure `Revenue` au rapport.
1. Cliquez sur **[!UICONTROL Duplicate]** pour effectuer une copie de la mesure.
1. Cliquez sur l’option **[!UICONTROL Time Range]** globale , puis sur **[!UICONTROL Moving Time Range]**. Définissez ce paramètre sur `Last Year`.
1. Cliquez sur l’option **[!UICONTROL Time Interval]** globale et définissez-la sur `Monthly`.
1. Report Builder ajoute automatiquement un second axe Y pour une seconde mesure. Désélectionnez la case `Multiple Y-Axes`.
1. Ensuite, vous appliquez une `Time Interval` indépendante à la première mesure. Cliquez sur **[!UICONTROL Time Options]** (icône d’horloge) à droite de la `first Revenue metric`.
1. Cliquez sur **[!UICONTROL Time Options]** dans la fenêtre développée qui s’affiche au-dessus du rapport.
1. Dans la liste déroulante, définissez les éléments suivants :

   * `Time Interval` : définissez ce paramètre sur `None`.

   * `Time Range` : définissez ce paramètre sur `Last Year` en cliquant d’abord sur **[!UICONTROL Custom]**, puis sur **[!UICONTROL Moving Range]** et en sélectionnant l’option `Last Year`.

   * Cliquez sur **[!UICONTROL Apply]** pour enregistrer les paramètres d’intervalle et de plage. Cette opération crée une mesure qui calcule le chiffre d’affaires total de l’année précédente. Ensuite, vous utilisez cette mesure comme dénominateur dans une formule.

   * Pour afficher le pourcentage du chiffre d’affaires de chaque mois, vous devez ajouter une formule au rapport. Cliquez sur **[!UICONTROL Add Formula]**.

   * Saisissez `B/A` dans le champ de formule et sélectionnez `% Percent` dans la liste déroulante en regard du champ de texte. Cette formule divise le montant des revenus d&#39;un mois spécifique de l&#39;année dernière par le montant total des revenus de l&#39;année dernière.

   * Cliquez sur **[!UICONTROL Apply Changes]**.

   * Masquez les deux mesures d’entrée et renommez la formule.

Maintenant, vous pouvez voir à quel point chaque mois a été impactant l’année dernière :

![Graphique montrant le pourcentage du chiffre d’affaires par mois pour l’année précédente](../assets/Independent_Time_Int.png)

## Comparaison d’une même mesure sur différentes périodes {#difftimerange}

Cet exemple utilise une dimension personnalisée appelée `Day number of the month`. Si vous souhaitez créer ce rapport et que cette dimension ne figure pas déjà dans votre Data Warehouse, [contactez l’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) pour obtenir de l’aide.

Les deux exemples les plus courants dans cette catégorie sont (1) la comparaison des mesures de croissance (revenus d&#39;une année à l&#39;autre ou d&#39;un mois à l&#39;autre) et (2) une meilleure compréhension des tendances récentes des stocks ou des ventes d&#39;articles.

Pour démontrer ce cas d’utilisation, regardez le chiffre d’affaires quotidien du mois précédent par rapport au même mois de l’année précédente. Supposons que vous souhaitiez examiner le chiffre d’affaires de chaque jour de janvier 2016, puis le comparer à janvier 2015, janvier 2014, etc., ce rapport nous le montrerait.

1. Ajoutez votre mesure `Revenue` au rapport.
1. Cliquez sur **[!UICONTROL Duplicate]** pour effectuer une copie de la mesure.
1. Renommez la première mesure en `Items sold last 7 days` et la seconde en `Items sold last 28 days`.
1. Cliquez sur **[!UICONTROL Time Range]**, puis sur **[!UICONTROL Moving Time Range]**. Définissez ce paramètre sur `Last Month`.
1. Cliquez sur **[!UICONTROL Time Interval]** et définissez-le sur `None`.
1. Cliquez sur **[!UICONTROL Time Options]** (icône d’horloge) en regard de la deuxième mesure de `Revenue`.
1. Cliquez sur **[!UICONTROL Time Options]** dans la fenêtre développée qui s’affiche au-dessus du rapport.
1. Dans la liste déroulante, définissez les éléments suivants :

   * `Time Interval` : définissez ce paramètre sur `None`.

   * `Time Range` : définissez ce paramètre sur `From 14 Months Ago To 13 Months Ago` en cliquant d’abord sur **[!UICONTROL Custom]** puis sur **[!UICONTROL Moving Range]**. Utilisez les champs et les listes déroulantes en haut du menu pour définir la plage. Ce paramètre nous permet de voir le chiffre d’affaires du mois précédent, mais de l’année précédente.

   Ne vous inquiétez pas si la mesure disparaît du rapport : la définition d’une option de temps indépendante masque automatiquement la mesure du rapport. Pour le réafficher, cliquez sur **[!UICONTROL Show]** en regard de la mesure.

   ![Démonstration de la définition de différentes périodes pour les mesures dans un rapport](../assets/Different_Time_Ranges.gif)

   * Cliquez sur **[!UICONTROL Apply]** pour enregistrer les paramètres d’intervalle et de plage.

   * Ajoutez ensuite votre dimension `Day number of the month` personnalisée en cliquant sur **[!UICONTROL Group By]** et en sélectionnant la dimension. Cette option renvoie le numéro de jour du mois d’une commande ; par exemple, une commande passée le 2 mars renvoie `2`.

   * Dans la liste déroulante `Group By`, sélectionnez `Show All` et cliquez sur **[!UICONTROL Apply]**. Cela crée les valeurs de l’axe X pour le rapport :

   ![Rapport présentant la comparaison des revenus, regroupés par jour et par numéro de mois](../assets/TO4.png)

   * Renommez les mesures. Dans cet exemple, la première mesure est `Revenue - 2015` et la seconde est `Revenue - 2014`.

Une autre utilisation courante des `Time Options` personnalisés consiste à déterminer les semaines d’approvisionnement. En particulier pendant la période des fêtes ou une période promotionnelle spéciale, vous pouvez tenir compte des articles vendus au cours de la semaine, du mois et de la période promotionnelle précédente pour prendre des décisions d’achat éclairées.

N&#39;oubliez pas de définir les périodes en fonction de vos besoins lors de la création de ce rapport.

1. Ajoutez votre mesure `Items Sold` au rapport.
1. Cliquez sur **[!UICONTROL Duplicate]** pour effectuer une copie de la mesure.
1. Renommez les mesures. Vous pouvez utiliser les mêmes noms ou utiliser une expression similaire :
   1. Renommez la première mesure en `Items sold last 7 days`.
   1. Renommez la deuxième mesure en `Items sold last 28 days`.
1. Sur la mesure `Items sold last 7 days`, cliquez sur l’option **[!UICONTROL Time Range]** globale , puis **[!UICONTROL Moving Time Range]**. Pour cet exemple, définissez-le sur `Last 7 Days`.
1. Cliquez sur **[!UICONTROL Time Interval]** et définissez-le sur `None`.
1. Définissez ensuite la `Time Options` de la mesure `Items sold last 28 days`. Cliquez sur **[!UICONTROL Time Options]** (icône d’horloge) à droite de la mesure `second Items sold`.
1. Cliquez sur **[!UICONTROL Time Options]** dans la fenêtre développée qui s’affiche au-dessus du rapport.
1. Dans la liste déroulante, définissez les éléments suivants :

   * `Time Interval` : définissez ce paramètre sur `None`.
   * `Time Range` : définissez ce paramètre sur `From 29 days to 1 day ago` en cliquant d’abord sur **[!UICONTROL Custom]**, puis sur **[!UICONTROL Moving Range]**. Utilisez les champs et les listes déroulantes en haut du menu pour définir la plage.
   * Cliquez sur **[!UICONTROL Apply]** pour enregistrer les paramètres d’intervalle et de plage.
   * Dupliquez la mesure `Items sold last 28 days` et ouvrez le `Time Options` de la nouvelle mesure. Définissez les options sur ce qui suit :

      * `Time Interval` : laissez ceci comme `None`.
      * `Time Range` : remplacez cette valeur par la période correspondant à la promotion qui vous intéresse. Pour ce faire, cliquez sur **[!UICONTROL Specific Date Range]**, puis saisissez les dates appropriées.
      * Renommez la mesure `Items sold during last promotion` ou une opération similaire.
      * Ajoutez votre mesure `Units on hand`.
      * Ensuite, vous devez ajouter les calculs qui nous indiquent les semaines en cours, en tenant compte des tendances des ventes, pour les périodes (`last 7 days`, `last 28 days` et période `last promo`) que vous incluez dans le rapport. Vous devez effectuer cette opération une fois pour chaque période.

Pour créer les formules, cliquez sur **[!UICONTROL Add Formula]**. Saisissez les formules ci-dessous et cliquez sur **[!UICONTROL Apply Changes]** lorsque vous avez terminé. Répétez cette opération pour chacune des trois périodes :

* Pour le `last 7 days time period` , saisissez `D / A` dans le champ `Formula` .
* Pour le `last 28 days time period` , saisissez `D / (B/4)` dans le champ `Formula` .

  >[!NOTE]
  >
  >Il est important de normaliser les périodes sélectionnées ici. Dans cet exemple, divisez 28 jours en quatre semaines. Vous devrez peut-être appliquer une logique différente à la formule.

* Pour le `last promo period` , saisissez `D / C` dans le champ `Formula` .

  ![Rapport affichant les calculs d&#39;approvisionnement pour différentes périodes](../assets/Different_Time_Ranges_2.png)

* Enfin, personnalisez le rapport en masquant les mesures et en ajoutant une `SKU` ou une dimension similaire au rapport sous forme de `Group By`.

Cet exemple montre que les niveaux actuels des stocks étaient bien situés pour une vente de 14 jours à l&#39;échelle du produit. Cependant, l&#39;ajout d&#39;une période promotionnelle comparable suggère que l&#39;entreprise doit apporter certains changements, soit en commandant plus d&#39;inventaire, soit en faisant la promotion des articles avec suffisamment d&#39;unités en stock.

Étant donné que vos clients se comportent différemment au fil du temps, vous pouvez vous attendre à voir des variations dans les données lors des analyses. La définition d’options de temps personnalisées vous permet de créer rapidement des analyses complexes, ce qui permet de prendre des décisions pilotées par les données qui tiennent compte des tendances historiques.

