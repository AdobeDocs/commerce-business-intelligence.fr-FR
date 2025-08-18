---
title: Analyse des cohortes de chiffre d’affaires au cours de la vie
description: Explorez la puissance de l’analyse des cohortes Commerce Intelligence.
exl-id: f2b55745-d364-4ba6-9857-ce9cee05c3ae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 0%

---

# Analyse [!DNL Lifetime Revenue Cohort]

Il existe de nombreuses façons d’examiner vos données dans [!DNL Adobe Commerce Intelligence], et vous savez que l’interprétation et la compréhension sont aussi importantes que le calcul et la visualisation. Cette rubrique explore la puissance de l’analyse [!DNL Commerce Intelligence] `cohort`.

## Que signifie `lifetime revenue cohort` analyse ?

Le graphique ci-dessous montre les dépenses cumulées par utilisateur pendant une période après leur acquisition. `Cohorts` utilisateurs sont répartis par mois d&#39;acquisition.

Par exemple, la ligne orange ci-dessus indique la moyenne des utilisateurs acquis en novembre 2011. Le premier point de données signifie qu’au cours de leur premier mois, les utilisateurs qui ont été acquis en novembre ont dépensé en moyenne environ `$200`. Le deuxième point de données signifie qu’à la fin de leur deuxième mois, ces utilisateurs avaient passé en moyenne environ `$240`. Leurs dépenses moyennes au cours du deuxième mois étaient d&#39;environ `$40 (240 - 200)`. Les différentes lignes représentent différentes cohortes d’utilisateurs et d’utilisatrices. La ligne verte représente les utilisateurs qui ont été acquis en décembre, et la bleue représente les utilisateurs qui ont été acquis en octobre.

## Pourquoi est-ce important ?

Ce type d’analyse `cohort` peut être utile à plusieurs fins différentes, mais l’avantage le plus immédiat est souvent de meilleures décisions d’acquisition de clients. De nombreuses entreprises limitent leurs dépenses de marketing aux canaux qui génèrent de la rentabilité lors du premier achat d&#39;un client. Ces entreprises paient pour acquérir des clients par l&#39;intermédiaire d&#39;un canal donné tant que leur premier achat moyen donne des rendements plus `gross margin` que ce qu&#39;il en coûte pour les acquérir.

Le problème avec cette approche est qu&#39;elle entraîne souvent un sous-investissement dans la croissance. Si vos concurrents font du marketing en se fondant sur une meilleure compréhension du comportement d&#39;achat, ils vous surpassent. L’analyse des `lifetime revenue cohort` vous aide à comprendre les conséquences de l’augmentation de vos dépenses d’acquisition de clients et elle offre un moyen facile de les transmettre au reste de votre équipe. Si les futurs clients se comportent comme les clients existants, l’acquisition de clients pour un CPA plus élevé entraîne une période de récupération prévisible. Selon la situation de trésorerie de l&#39;entreprise, vous pouvez définir la période de récupération qui vous convient, trouver l&#39;emplacement approprié sur le graphique et dépenser en conséquence.

En outre, vous pouvez utiliser cette analyse pour voir si vous vous améliorez en matière d’intégration, d’engagement et de génération de revenus à partir des utilisateurs acquis. Par exemple, cette analyse des `cohort` est un excellent moyen de déterminer si une promotion de livraison gratuite pour les nouveaux utilisateurs a donné lieu à des acheteurs récurrents ou à des acheteurs uniques qui ne reviennent jamais.

## En quoi cela varie-t-il selon les modèles d’entreprise ?

Pour la plupart des entreprises, le graphique d&#39;analyse `lifetime revenue cohort` indiquera un montant important de dépenses au cours de la période initiale, puis augmentera plus lentement au fil du temps. Ce pic initial est dû au fait que les clients sont plus susceptibles d’effectuer leur premier achat peu de temps après leur acquisition qu’à tout autre moment. Dans les cas où l’événement d’acquisition lui-même est un achat, 100 % des clients effectuent un achat au cours de leur première période. Dans les cas où l&#39;enregistrement peut avoir lieu avant les achats, cet effet est moins drastique.

Par exemple, [!DNL Groupon] aurait probablement un saut initial beaucoup plus faible que [!DNL Amazon], parce que beaucoup de gens qui s&#39;inscrivent à [!DNL Groupon] ne font pas d&#39;achat immédiatement. À moins qu&#39;il n&#39;y ait un nombre élevé de remboursements, ce graphique s&#39;inclinera vers la droite après le saut initial. Le taux de croissance a tendance à diminuer au fil du temps, car les clients sont plus actifs lorsqu’ils s’inscrivent pour la première fois. Cela entraîne une baisse de la moyenne, car le nombre de personnes dans la cohorte reste constant, quel que soit le nombre de personnes qui reviennent acheter plus. Dans les entreprises qui offrent des abonnements, la pente se réduira de façon moins marquée que dans les entreprises où les gens font des achats ponctuels.

Parfois, une entreprise d&#39;abonnement aura en fait une pente qui augmentera au fil du temps. C&#39;est rare de voir cela, mais c&#39;est un excellent signal pour l&#39;entreprise lorsque cela se produit. Cela ne signifie pas qu’il n’y a aucun client récurrent, mais plutôt que les mises à niveau pour les clients qui restent compensent largement les clients qui quittent l’entreprise.

## Comment cela est-il calculé ?

Il existe deux entrées simples dans ce calcul : le nombre de membres dans la `cohort` (qui ne change jamais) et le montant des revenus générés par ces membres au cours de la période donnée. Pour déterminer les membres de la `cohort`, vous comptez le nombre d’utilisateurs acquis au cours de la période en question. Une acquisition peut être un premier achat, la création d’un compte, une inscription à une newsletter ou un autre événement. Le calcul `revenue` est un peu plus compliqué. Vous souhaitez additionner le chiffre d&#39;affaires des commandes passées par des membres de ce `cohort` et qui ont eu lieu dans un délai fixe à compter de leur date d&#39;acquisition (par exemple, les trois premiers mois). Enfin, vous divisez le chiffre d’affaires par le nombre de membres dans le `cohort` pour chaque période du graphique et ajoutez cette valeur de manière cumulative au fil du temps.

## Quelles sont les variations de ce graphique ?

Il existe de nombreux types d’analyses `cohort` utiles. La variation la plus courante est le [filtrage par source d’acquisition des utilisateurs](../analysis/most-value-source-channel.md). Par exemple, vous pouvez examiner ce graphique pour les clients qui proviennent d’`organic` recherche, d’une recherche `paid` ou d’un programme d’affiliation. Cela vous permet de comprendre si les clients d’une source d’acquisition sont plus fidèles ou plus précieux qu’une autre. Vous pouvez également filtrer selon les données démographiques ou d’autres attributs utilisateur.

Une autre façon d’examiner les données est d’adopter une perspective de données incrémentielles plutôt que cumulatives. Cela indique le montant incrémentiel qu’un utilisateur moyen dépense chaque mois après leur acquisition. Cela s’avère utile pour prévoir le nombre d’achats répétés que vous obtenez des utilisateurs existants. Vous pouvez examiner cette question avec d&#39;autres choses que les recettes également. Par exemple, les marges et les mesures non financières telles que les invitations, les votes ou les messages.
