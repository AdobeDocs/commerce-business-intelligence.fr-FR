---
title: Tableaux de bord inclus
description: Découvrez comment vérifier l’intégrité des mesures essentielles, telles que le chiffre d’affaires de durée de vie de l’utilisateur, le nombre d’achats répétés, etc., afin de créer une base solide pour l’exploration future.
exl-id: f50fc417-e5d4-401c-9baa-cda1468196a2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---

# Tableaux de bord inclus

[!DNL Adobe] propose des packages de démarrage `eCommerce` et `SaaS`. Ces packages, créés par les analystes d’Adobe, contiennent un ensemble personnalisé de tableaux de bord et de rapports pour votre jeu de données. Les analyses contenues dans ces packages vous permettent de vérifier l’intégrité des mesures essentielles, telles que le chiffre d’affaires de durée de vie de l’utilisateur, le nombre d’achats répétés, etc., créant ainsi une base solide pour l’exploration future.

>[!NOTE]
>
>La disponibilité de certains tableaux de bord dépend de votre jeu de données.

Si vous avez des questions ou si vous souhaitez ajouter un package à votre compte, envoyez un [ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) pour obtenir de l’aide.

## Présentation opérationnelle

Le tableau de bord `executive overview` est créé à partir de graphiques qui existent sur d’autres tableaux de bord. Ce tableau de bord donne un aperçu général de vos données et contient des graphiques qui seraient examinés quotidiennement, tandis que d’autres tableaux de bord contenaient des informations plus détaillées. Au départ, il est défini comme tableau de bord par défaut dans chaque compte.

Un ensemble général de graphiques est inclus. Adobe vous recommande d’adapter ce tableau de bord à vos besoins en ajoutant les graphiques que vous utilisez le plus souvent.

## Analyse de cohortes

Le tableau de bord `cohort analysis` comprend un ensemble de graphiques qui montrent la croissance moyenne du chiffre d’affaires de l’utilisateur sur toute la durée de vie et la croissance du chiffre d’affaires incrémentiel, regroupées par cohortes d’enregistrement. Cela permet de savoir si la valeur à vie du client (VVC), c&#39;est-à-dire la valeur d&#39;un client pour une entreprise, augmente au fil du temps, et de cerner les tendances entourant la croissance de la VVC. Par défaut, *tous les utilisateurs enregistrés (acheteurs et non-acheteurs) sont pris en compte* dans le calcul de la VVC moyenne, voir la rubrique [analyse des cohortes](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Ce tableau de bord peut également inclure des graphiques de cohortes qui analysent le chiffre d’affaires total des utilisateurs d’une source d’acquisition, d’un canal ou d’une population spécifique (par exemple, New York ou la Californie). L&#39;objectif est de montrer comment vous pouvez analyser le LTV pour des segments spécifiques de votre base d&#39;utilisateurs et voir si un groupe ou un autre produit un LTV plus élevé au fil du temps.

Pour plus d’informations sur les cohortes, voir [ Exécution d’une analyse des cohortes ](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Si vous ne suivez actuellement pas la source d’acquisition des utilisateurs, reportez-vous à la section [Présentation des données Source de suivi d’acquisition des utilisateurs](../../data-analyst/analysis/google-track-user-acq.md).

## Résumé des e-mails

Le tableau de bord `Email Summary` comprend un exemple d’ensemble de graphiques qui peuvent être utilisés dans un résumé automatisé d’e-mail quotidien. Pour plus d’informations sur la configuration des résumés d’e-mails[ voir ](../../data-user/export-data/email-summaries.md)création de résumés d’e-mail automatisés.  

## Intégrité de la rétention

Le tableau de bord `Retention health` révèle le comportement d’achat répété de votre base d’utilisateurs.

Le graphique `Time between orders` indique le temps écoulé moyen et/ou médian entre le premier et le deuxième ordre, le deuxième et le troisième ordre d’un utilisateur, etc. Vous pouvez [utiliser ces données pour configurer vos campagnes marketing par e-mail](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/).

Le graphique `Users by lifetime number of orders` répertorie le nombre total d’utilisateurs pour chaque nombre de commandes au cours de la durée de vie afin de fournir une vue d’ensemble du comportement d’achat répété.  

Le graphique `Repeat order probability` indique la probabilité qu’un utilisateur disposant d’un certain numéro de commande effectue un nouvel achat. Pour voir la probabilité que les clients qui ont passé des commandes `x` passent des commandes `(x+1)`, divisez simplement le nombre de personnes qui ont effectué au moins `(x+1)` achats par le nombre de personnes qui ont effectué au moins `x` achats.

### Exemple

Nombre de clients qui ont effectué un achat au cours de leur durée de vie : `90`

Nombre de clients qui ont effectué deux achats au cours de leur durée de vie : `30`

Nombre de clients ayant effectué trois achats au cours de leur durée de vie : `10`

Dans cet exemple, la probabilité de commande répétée des clients qui ont effectué un achat au cours de leur durée de vie pour effectuer un deuxième achat est : `(30 + 10) / (30+10+90) = 30.77%`.

## Croissance du LTV client

Le tableau de bord `Customer LTV growth` comprend un ensemble de graphiques qui déterminent le chiffre d’affaires moyen par utilisateur. Les graphiques sont segmentés en fonction du chiffre d’affaires moyen généré dans les 30, 60, 90 ou 365 premiers jours suivant l’enregistrement.  

La ligne inférieure des graphiques montre que ces moyennes sont segmentées par sources d’acquisition ou données démographiques afin de révéler quels groupes d’utilisateurs génèrent le plus de revenus au fil du temps.

## Performances du produit

Le tableau de bord `Product Performance` comprend des graphiques qui révèlent les performances générales des produits en affichant le nombre d’articles vendus et les recettes par article, et en identifiant les produits les plus performants.

## Activité récente

Le tableau de bord `Recent Activity` affiche les données de performances des 30 derniers jours.

## Santé transactionnelle

Le tableau de bord `Transaction Health` comprend des graphiques de présentation du chiffre d’affaires, des commandes et de la valeur moyenne des commandes. Ces graphiques peuvent être segmentés par canaux marketing, données démographiques ou par codes de coupon spéciaux.

## Utilisateurs à cibler

Le tableau de bord `Users to target` comprend des graphiques sous forme de tableau qui répertorient les utilisateurs ayant des comportements d’achat spécifiques en commun. Voici quelques exemples :

* Liste des acheteurs occasionnels ayant effectué un achat il y a `X` mois (que vous souhaiterez peut-être réactiver)

* Liste des principaux dépensiers (que vous souhaiterez peut-être garder heureux)

* Liste des principaux dépensiers qui ont été actifs au cours des `X` derniers jours (que vous pourriez vouloir récompenser)

À l’aide de vos outils d’exportation de données, il est facile de [créer des listes d’e-mails d’utilisateurs ayant un comportement d’achat similaire pour le marketing cible](http://blog.rjmetrics.com/creating-contact-lists-for-top-customers/).

## Activité utilisateur

Le tableau de bord `User activity` comprend des graphiques qui segmentent les utilisateurs en fonction de diverses données, notamment la source d’acquisition, les données démographiques et le délai moyen de première commande. Il comprend également une analyse des cohortes d’utilisateurs, y compris le chiffre d’affaires moyen global sur toute la durée de vie par mois d’enregistrement des utilisateurs.

Le graphique `% of cohort members who have purchased` est utile, car il indique le taux de conversion (de 0 à 1) des utilisateurs en fonction du moment où ils s’enregistrent (chaque ligne représente une cohorte d’utilisateurs). Il indique également quand ils effectuent leur premier achat (par exemple, au mois 1, 2, 3... après l’enregistrement). Cela peut vous montrer que 10 % des utilisateurs ont été activés au mois 1, tandis que ce nombre augmente au mois 2, 3, 4... et peut se stabiliser ultérieurement.

En règle générale, les lignes de ce graphique deviennent horizontales au bout d’un certain temps. Cela indique que peu de membres de la cohorte supplémentaires effectuent une conversion organique après ce moment - la plupart des utilisateurs qui vont effectuer un achat l’ont déjà fait. À ce stade, il est très peu probable que ces membres convertissent leurs actions en acheteurs sans intervention. [Les contacter avec des promotions personnalisées ou des e-mails ciblés est un moyen à faible risque de démarrer la conversion de cette population.](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/)
