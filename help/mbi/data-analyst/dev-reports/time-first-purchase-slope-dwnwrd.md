---
title: Rapport Délai moyen avant le premier achat
description: Découvrez comment utiliser le rapport Délai moyen avant le premier achat.
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 330832e2668024b00edb2b7c49b92bb042bd004a
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Rapport Délai moyen avant le premier achat

De nombreux clients Adobe disposent d’une mesure et d’un graphique nommés `Average time to first purchase`, qui indique le temps moyen entre la date d’enregistrement d’un groupe d’utilisateurs et la date de premier achat. Les données descendent presque invariablement à mesure que le temps se rapproche du présent.

![délai moyen de première commande](../../assets/average-time-to-first-order.png)

En effet, ces nouveaux clients n’ont pas encore eu la possibilité de générer des achats effectués plus d’un mois après leur date d’adhésion. Comme les utilisateurs qui n’ont jamais effectué d’achat ne sont pas du tout inclus (jusqu’à ce qu’ils effectuent un achat), cela biaise la moyenne à la baisse pour les nouveaux groupes de clients.

Il existe plusieurs autres façons potentielles d’examiner cette mesure qui introduisent moins de biais. Explorez un exemple.

## Exemple : réalisation d&#39;une analyse `cohort` des premières commandes

Il se peut que votre tableau de bord `Users` contienne un graphique intitulé `Time to first order cohort`. Ce rapport utilise la mesure `Distinct buyers`, regroupe les utilisateurs par `cohort` semaines ou mois d’enregistrement et affiche le ratio (entre `0` et `1`) des utilisateurs qui ont effectué un premier achat au cours des semaines ou mois suivants après l’enregistrement.

Le graphique peut indiquer que pour les utilisateurs qui se sont inscrits en décembre 2014, `0.56` (ou `56%`) a passé une première commande au mois 2 (par exemple, en janvier 2015).

Cette analyse des cohortes est un bon indicateur du taux d’activation des utilisateurs au fil du temps. Si ce graphique commence à s’aplatir ou à se stabiliser et que vous n’êtes toujours pas près de la conversion à 100 % pour les acheteurs, il est peut-être temps d’activer les utilisateurs restants par le biais de campagnes par e-mail.
