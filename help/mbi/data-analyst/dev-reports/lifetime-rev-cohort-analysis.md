---
title: Analyse des cohortes de recettes sur la durée de vie
description: Explorez la puissance de l’analyse des cohortes de Commerce Intelligence.
exl-id: f2b55745-d364-4ba6-9857-ce9cee05c3ae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---

# [!DNL Lifetime Revenue Cohort] Analyse

Il existe de nombreuses façons d’examiner vos données dans [!DNL Adobe Commerce Intelligence]et vous savez que l&#39;interprétation et la compréhension sont aussi importantes que le calcul et la visualisation. Cette rubrique explore la puissance de [!DNL Commerce Intelligence] `cohort` analyse.

## Que faire ? `lifetime revenue cohort` l&#39;analyse signifie ?

Le graphique ci-dessous montre les dépenses cumulées par utilisateur pendant une période après leur acquisition. `Cohorts` des utilisateurs sont répartis par mois d’acquisition.

Par exemple, la ligne orange ci-dessus indique la moyenne des utilisateurs acquis en novembre 2011. Le premier point de données signifie qu’au cours de leur premier mois, les utilisateurs achetés en novembre ont dépensé en moyenne environ `$200`. Le deuxième point de données signifie qu’à la fin de leur deuxième mois, ces utilisateurs avaient passé en moyenne environ `$240`. Leur dépense moyenne pour le mois deux était approximativement `$40 (240 - 200)`. Les différentes lignes représentent différentes cohortes d’utilisateurs. La ligne verte représente les utilisateurs acquis en décembre, et la bleue les utilisateurs acquis en octobre.

## Pourquoi est-ce important ?

Ce genre de `cohort` l’analyse peut s’avérer utile à plusieurs fins, mais l’avantage le plus immédiat est souvent de prendre de meilleures décisions en matière d’acquisition client. De nombreuses entreprises limitent leurs dépenses marketing aux canaux qui génèrent de la rentabilité lors du premier achat d’un client. Ces entreprises paient pour acquérir des clients par le biais d’un canal donné tant que leur premier achat moyen produit plus de `gross margin` qu&#39;il en coûte de les acquérir.

Le problème avec cette approche est qu&#39;elle entraîne souvent un sous-investissement dans la croissance. Si vos concurrents font du marketing en se basant sur une meilleure compréhension du comportement d’achat, ils vous surpassent. Le `lifetime revenue cohort` l’analyse vous aide à comprendre les conséquences de l’augmentation de vos dépenses d’acquisition client. elle vous permet de transmettre facilement cette information au reste de votre équipe. Si les futurs clients se comportent comme les clients existants, l’acquisition de clients pour un CPA plus élevé entraîne une période de retour anticipé. En fonction de la position de trésorerie de l’entreprise, vous pouvez définir la période de retour arrière que vous maîtrisez, trouver l’emplacement approprié sur le graphique et dépenser en conséquence.

Vous pouvez également utiliser cette analyse pour déterminer si vous vous améliorez en termes d’intégration, d’engagement et de génération de recettes à partir des utilisateurs que vous acquérez. Par exemple, ceci : `cohort` l’analyse est un excellent moyen de déterminer si une promotion de livraison gratuite pour les nouveaux utilisateurs a pour résultat des acheteurs réguliers ou des acheteurs ponctuels qui ne reviennent jamais.

## En quoi cela variera-t-il selon les différents modèles d’entreprise ?

Pour la plupart des entreprises, la variable `lifetime revenue cohort` le graphique d&#39;analyse montre une dépense importante au cours de la période initiale, puis augmente plus lentement au fil du temps. Ce pic initial est dû au fait que les clients sont plus susceptibles d’effectuer leur premier achat peu après leur acquisition qu’à tout autre moment. Dans les cas où l’événement d’acquisition lui-même est un achat, 100 % des clients effectuent un achat au cours de leur première période. Dans les cas où l’enregistrement peut avoir lieu avant les achats, cet effet est moins radical.

Par exemple : [!DNL Groupon] aurait probablement un saut initial beaucoup plus faible que [!DNL Amazon], car beaucoup de gens s&#39;inscrivent [!DNL Groupon] ne faites pas d’achat immédiatement. À moins d’un nombre élevé de remboursements, ce graphique s’inclinera vers la droite après le saut initial. Le taux de croissance tend à diminuer au fil du temps, car les clients sont les plus principaux lorsqu’ils s’inscrivent pour la première fois. Cela entraîne une baisse de la moyenne, car le nombre de personnes dans la cohorte reste constant, quel que soit le nombre de personnes qui reviennent acheter plus. Dans les sociétés d’abonnement, la pente se réduira de manière moins agressive que dans les entreprises où les clients effectuent des achats ponctuels.

Parfois, une entreprise d’abonnement aura une pente qui augmente au fil du temps. C&#39;est rare de voir cela, mais c&#39;est un excellent signal pour l&#39;entreprise quand il se produit. Cela ne signifie pas qu’il n’y ait aucun client régulier, mais plutôt que les mises à niveau pour les clients qui restent plus que compenser les clients qui partent.

## Comment est-ce calculé ?

Ce calcul comporte deux entrées simples : combien de membres se trouvent dans la variable `cohort` (qui ne change jamais) et le montant des recettes générées par ces membres au cours de la période donnée. Pour déterminer les membres dans la variable `cohort`, vous comptabilisez le nombre d’utilisateurs acquis au cours de la période en question. Une acquisition peut être un premier achat, la création de compte, l’inscription à un bulletin d’information ou un autre événement. Le `revenue` le calcul est un peu plus compliqué. Vous souhaitez additionner les recettes des commandes passées par des membres de ce groupe. `cohort` et ont eu lieu dans un délai fixe à compter de leur date d’acquisition (par exemple, les trois premiers mois). Enfin, vous divisez les recettes par le nombre de membres dans la variable `cohort` pour chaque période du graphique et ajoutez cette valeur de manière cumulative au fil du temps.

## Quelles sont les variations de ce graphique ?

Il existe de nombreuses sortes d&#39;utiles `cohort` des analyses. La variation la plus courante est la suivante : [filtrage par source d’acquisition d’utilisateurs](../analysis/most-value-source-channel.md). Par exemple, vous pouvez consulter ce graphique pour les clients provenant de `organic` recherche, `paid` rechercher ou un programme affilié. Vous pouvez ainsi déterminer si les clients d’une source d’acquisition sont plus fidèles ou plus précieux qu’un autre. Vous pouvez également filtrer par données démographiques ou d’autres attributs utilisateur.

Une autre façon d’examiner les données consiste à avoir une perspective incrémentielle plutôt qu’cumulée des données. Cela indique le montant incrémentiel dépensé par un utilisateur moyen chaque mois après son acquisition. Cela s’avère utile pour prévoir le nombre d’achats répétés que vous obtenez des utilisateurs existants. Vous pouvez également y regarder d’autres choses en plus des recettes. Il peut s’agir, par exemple, de mesures de marge et non financières telles que les invitations, les votes ou les messages.
