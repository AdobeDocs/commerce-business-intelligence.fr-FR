---
title: Rapport Temps moyen jusqu’au premier achat
description: Découvrez comment utiliser le rapport Temps moyen jusqu’au premier achat .
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 330832e2668024b00edb2b7c49b92bb042bd004a
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Rapport Temps moyen jusqu’au premier achat

De nombreux clients Adobe ont une mesure et un graphique nommés `Average time to first purchase`, qui indique la durée moyenne entre la date d’enregistrement d’un groupe d’utilisateurs et la date du premier achat. Les données sont presque invariablement descendantes au fur et à mesure que le temps se rapproche du présent.

![durée moyenne de la première commande](../../assets/average-time-to-first-order.png)

En effet, ces nouveaux clients n’ont pas encore eu la possibilité de générer des achats qui ont été effectués plus d’un mois à compter de leur date de jointure. Puisque les utilisateurs qui n’ont jamais effectué d’achat ne sont pas du tout inclus (tant qu’ils n’ont pas effectué d’achat), cela influe sur la moyenne vers le bas pour les groupes de clients plus récents.

Il existe d’autres façons potentielles d’examiner cette mesure qui introduisent moins de biais. Examinez un exemple.

## Exemple : effectuer une `cohort` analyse des premières commandes

Vous pouvez avoir un graphique sur votre `Users` tableau de bord nommé `Time to first order cohort`. Ce rapport utilise la variable `Distinct buyers` mesure, groupe les utilisateurs par `cohort` semaines ou mois d’inscription et affiche le rapport (entre `0` et `1`) des utilisateurs qui ont effectué un premier achat au cours des semaines ou des mois suivants après l’enregistrement.

Le graphique peut indiquer que pour les utilisateurs qui se sont inscrits en décembre 2014, `0.56` (ou `56%`) a effectué une première commande au mois 2 (par exemple, janvier 2015).

Cette analyse des cohortes est un bon indicateur du taux d’activation des utilisateurs au fil du temps. Si ce graphique commence à s’aplatir ou à se calmer et que vous ne parvenez toujours pas à effectuer une conversion à 100 % vers les acheteurs, il peut être temps d’activer les utilisateurs restants par le biais de campagnes par e-mail.
