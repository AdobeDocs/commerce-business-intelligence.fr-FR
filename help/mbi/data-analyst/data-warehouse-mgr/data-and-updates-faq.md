---
title: Informations sur les données et les mises à jour
description: Découvrez comment vérifier le statut de votre cycle de mise à jour.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
source-git-commit: 09b6983c3e06a1f18035542dfa3b9de9ac3ceb38
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# Informations sur les données et les mises à jour

* [Pourquoi mes données ont-elles changé ?](#datachange)
* [Quelle est la différence entre une mise à jour régulière et forcée ?](#regularforcedupdates)
* [Pourquoi le cycle de mise à jour prend-il beaucoup de temps ?](#updatecycletime)
* [Puis-je être informé de la fin d’un cycle de mise à jour ?](#notifyupdate)
* [Pourquoi [!DNL Google ECommerce] données différentes de ma base de données ?](#ecommdatabase)
* [Comment résoudre un problème d’incohérence des données ?](#datadiscrepancy)

## Pourquoi mes données ont-elles changé ? {#datachange}

Les valeurs du graphique peuvent changer tout au long de la journée en raison de la synchronisation de nouvelles données dans votre entrepôt de données. De plus, les valeurs des colonnes de données existantes peuvent changer en raison de la variable [révérifications](../data-warehouse-mgr/cfg-data-rechecks.md). Un nouveau contrôle est un processus qui recherche les valeurs modifiées dans les colonnes de données, par exemple, un état de commande qui passe de `open` to `shipped`.

Il existe plusieurs manières différentes [pour vérifier le statut de votre cycle de mise à jour](../../best-practices/check-update-cycle.md), selon le type d’autorisations utilisateur dont vous disposez.

## Quelle est la différence entre une mise à jour régulière et forcée ? {#regularforcedupdates}

Les mises à jour régulières **scheduled** processus pendant que les mises à jour forcées sont **processus manuels initiés par vous**. Si vous avez des heures d’interruption, ou une période où [!DNL MBI] ne doit pas mettre à jour vos données : forcer une mise à jour déclenche un cycle qui ne respecte pas les limitations de la période de blackout.

## Pourquoi le cycle de mise à jour prend-il beaucoup de temps ? {#updatecycletime}

De nombreux facteurs peuvent s’ajouter à un temps de mise à jour déjà long. Certain [méthodes de réplication](../data-warehouse-mgr/cfg-replication-methods.md), [fréquences de recontrôle supérieures](../data-warehouse-mgr/cfg-data-rechecks.md), et le nombre de tableaux de bord et de graphiques ne représente que quelques contributeurs. Nous vous recommandons [reconfiguration de certains de vos paramètres](../../best-practices/reduce-update-cycle-time.md) et [optimisation de la base de données pour les analyses](../../best-practices/opt-db-analysis.md) pour réduire les temps de mise à jour.

## Puis-je être informé de la fin d’un cycle de mise à jour ? {#notifyupdate}

Absolument ! Si une mise à jour est en cours, un lien apparaît sur la variable `Connections` page que vous pouvez utiliser pour demander une notification par courrier électronique une fois le cycle terminé.

## Pourquoi[!DNL Google ECommerce]données différentes de ma base de données ? {#ecommdatabase}

Incohérences entre les [!DNL Google Analytics] et votre base de données peut apparaître pour plusieurs raisons. Le suivi n’étant pas correctement activé, les utilisateurs qui visitent incognito et les événements de clic ne fonctionnent pas correctement sont quelques exemples. Si vos recettes et commandes ne semblent pas exactes, [utiliser cet article ;](https://support.magento.com/hc/en-us/articles/360016505232) pour diagnostiquer le problème.

## Comment résoudre un problème d’incohérence des données ? {#datadiscrepancy}

Nous savons que voir des données incohérentes peut être une expérience frustrante. Essayez d’utiliser notre [Liste de contrôle des écarts de données](https://support.magento.com/hc/en-us/articles/360016731271) ou [Tutoriel sur les exportations de données](https://support.magento.com/hc/en-us/articles/360016730631) pour diagnostiquer le problème. Si vous êtes toujours en panne, [support technique](../../guide-overview.md).
