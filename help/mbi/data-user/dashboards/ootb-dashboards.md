---
title: Tableaux de bord inclus
description: Découvrez comment vérifier l’intégrité des mesures essentielles telles que les recettes de durée de vie des utilisateurs, le nombre d’achats répétés, etc., ce qui crée des bases solides pour l’exploration future.
exl-id: f50fc417-e5d4-401c-9baa-cda1468196a2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# Tableaux de bord inclus

[!DNL Adobe] offres `eCommerce` et `SaaS` Modules de démarrage. Ces modules, créés par les analystes Adobe, contiennent un ensemble personnalisé de tableaux de bord et de rapports pour votre jeu de données. Les analyses contenues dans ces packages vous permettent de vérifier l’intégrité des mesures essentielles telles que les recettes de durée de vie des utilisateurs, le nombre d’achats répétés, etc., ce qui crée une base solide pour une exploration future.

>[!NOTE]
>
>La disponibilité de certains tableaux de bord dépend de votre jeu de données.

Si vous avez des questions ou si vous souhaitez ajouter un module à votre compte, envoyez une [ticket de support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) pour obtenir de l’aide.

## Présentation exécutive

La variable `executive overview` Le tableau de bord est créé à partir de graphiques qui existent sur d’autres tableaux de bord. Ce tableau de bord offre un aperçu général de vos données et contient des graphiques qui seraient examinés quotidiennement, tandis que d’autres tableaux de bord contiennent des informations plus détaillées. Au départ, il est défini comme tableau de bord par défaut dans chaque compte.

Un ensemble général de graphiques est inclus pour vous. Adobe vous recommande d’adapter ce tableau de bord à vos besoins en ajoutant d’autres graphiques que vous utilisez le plus souvent.

## Analyse des cohortes

La variable `cohort analysis` Le tableau de bord comprend un ensemble de graphiques qui présentent la croissance moyenne des recettes sur la durée de vie des utilisateurs et la croissance incrémentielle des recettes, regroupées par cohortes d’enregistrement. Cela révèle si la valeur de durée de vie (LTV) d’un client, la valeur d’un client pour une entreprise, augmente au fil du temps et identifie également les tendances relatives à la croissance LTV. Par défaut, *tous les utilisateurs enregistrés (acheteurs et non-acheteurs) sont comptabilisés* dans le calcul LTV moyen - voir la section [rubrique sur l’analyse des cohortes](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Ce tableau de bord peut également inclure des graphiques de cohortes qui analysent les recettes sur toute la durée de vie des utilisateurs provenant d’une source d’acquisition, d’un canal ou d’une population spécifique (par exemple, New York ou la Californie). Cela vous permet de démontrer comment analyser LTV pour des segments spécifiques de votre base d’utilisateurs et voir si un groupe ou un autre produit plus de LTV au fil du temps.

Pour plus d’informations sur les cohortes, voir [Exécution de l’analyse des cohortes](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Si vous n’effectuez actuellement pas de suivi sur la source d’acquisition d’utilisateurs, reportez-vous à la section [Présentation du suivi des données de source d’acquisition d’utilisateurs](../../data-analyst/analysis/google-track-user-acq.md).

## Email summary

La variable `Email Summary` Le tableau de bord comprend un exemple de jeu de graphiques qui peuvent être utilisés dans un résumé quotidien automatisé des emails. Voir [création de résumés d’emails automatisés](../../data-user/export-data/email-summaries.md) pour plus d’informations sur la configuration des résumés d’emails.  

## Intégrité de rétention

La variable `Retention health` le tableau de bord révèle le comportement d’achat répété de votre base d’utilisateurs.

La variable `Time between orders` Le graphique présente la durée moyenne et/ou la durée moyenne écoulée entre le premier et le deuxième ordre d’un utilisateur, le deuxième et le troisième ordre, etc. Vous pouvez [envisagez d’utiliser ces données pour configurer vos campagnes de marketing par e-mail](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/).

La variable `Users by lifetime number of orders` Le graphique répertorie le nombre total d’utilisateurs pour chaque nombre de commandes au cours de la durée de vie afin de fournir un aperçu général du comportement d’achat répété.  

La variable `Repeat order probability` Le graphique indique la probabilité qu’un utilisateur disposant d’un certain numéro de commande effectue un achat répété. Pour connaître la probabilité des clients qui ont effectué `x` commandes à effectuer `(x+1)` les commandes, divisez simplement le nombre de personnes qui ont fait au moins `(x+1)` achats par le nombre de personnes qui ont effectué au moins `x` achats.

### Exemple

Nombre de clients qui ont effectué un achat au cours de leur vie : `90`

Nombre de clients qui ont effectué deux achats au cours de leur vie : `30`

Nombre de clients qui ont effectué trois achats au cours de leur vie : `10`

Dans cet exemple, la probabilité que les clients qui ont effectué un achat au cours de leur vie effectuent un second achat est la suivante : `(30 + 10) / (30+10+90) = 30.77%`.

## Croissance de la télévision client

La variable `Customer LTV growth` Le tableau de bord comprend un ensemble de graphiques qui répertorie les recettes moyennes par utilisateur. Les graphiques sont segmentés en fonction des recettes moyennes générées au cours des 30, 60, 90 ou 365 premiers jours suivant l’enregistrement.  

La ligne inférieure des graphiques montre que ces moyennes segmentées par sources d’acquisition ou par données démographiques indiquent les groupes d’utilisateurs qui génèrent le plus de recettes au fil du temps.

## Performances du produit

La variable `Product Performance` Le tableau de bord comprend des graphiques qui indiquent les performances générales du produit en affichant le nombre d’articles vendus et les recettes par article et en identifiant les produits les plus performants.

## Activité récente

La variable `Recent Activity` Le tableau de bord affiche les données de performances pour les 30 derniers jours.

## Santé transactionnelle

La variable `Transaction Health` le tableau de bord comprend des graphiques d’aperçu des recettes, des commandes et de la valeur de commande moyenne. Ces graphiques peuvent être segmentés par canaux marketing, par données démographiques ou par codes de bons spéciaux.

## Utilisateurs à cibler

La variable `Users to target` Le tableau de bord comprend des graphiques de type tableau qui répertorient les utilisateurs ayant des comportements d’achat spécifiques en commun. Voici quelques exemples :

* Liste des acheteurs ponctuels qui effectuent un achat `X` il y a des mois (que vous souhaitez peut-être réactiver).

* Liste des principaux débiteurs (que vous souhaitez peut-être garder heureux)

* Liste des principaux débiteurs actifs dans le passé `X` jours (à qui vous souhaitez peut-être récompenser)

L’utilisation de vos outils d’exportation de données facilite l’utilisation de [créer des listes email d’utilisateurs ayant un comportement d’achat similaire pour le marketing cible ;](http://blog.rjmetrics.com/creating-contact-lists-for-top-customers/).

## Activité de l’utilisateur

La variable `User activity` Le tableau de bord comprend des graphiques qui segmentent les utilisateurs selon diverses données, notamment la source d’acquisition, les données démographiques et la première commande moyenne. Elle comprend également l’analyse des cohortes d’utilisateurs, y compris la moyenne globale des recettes de la durée de vie par mois d’enregistrement des utilisateurs.

La variable `% of cohort members who have purchased` est utile, car il indique le taux de conversion (de 0 à 1) des utilisateurs en fonction du moment où ils s’inscrivent (chaque ligne représente une cohorte d’utilisateurs). Il indique également le moment où ils effectuent leur premier achat (par exemple, durant les mois 1, 2, 3... après inscription). Cela peut vous indiquer que 10 % des utilisateurs ont été activés au mois 1, alors que ce nombre augmente aux mois 2, 3, 4... et peut se calmer plus tard.

En règle générale, les lignes de ce graphique deviennent horizontales après un certain temps. Cela indique que peu de membres de cohortes supplémentaires effectuent une conversion organique après ce point. La plupart des utilisateurs qui vont effectuer un achat l’ont déjà fait. A ce stade, il est très peu probable que ces membres se convertissent en acheteurs sans intervention. [Atteindre ces derniers avec des promotions personnalisées ou des emails ciblés est un moyen peu risqué de lancer la conversion de cette population.](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/)
