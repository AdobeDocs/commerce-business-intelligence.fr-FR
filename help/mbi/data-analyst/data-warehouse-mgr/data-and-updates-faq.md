---
title: Informations sur les données et les mises à jour
description: Découvrez comment vérifier le statut de votre cycle de mise à jour.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '417'
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

Les valeurs du graphique peuvent changer tout au long de la journée en raison de la synchronisation de nouvelles données avec votre Data Warehouse. En outre, les valeurs des colonnes de données existantes peuvent changer en raison de [révérifications](../data-warehouse-mgr/cfg-data-rechecks.md). Un nouveau contrôle est un processus qui recherche les valeurs modifiées dans les colonnes de données, par exemple, un état de commande qui passe de `open` to `shipped`.

Il existe plusieurs manières différentes [pour vérifier le statut de votre cycle de mise à jour](../../best-practices/check-update-cycle.md), selon le type d’autorisations utilisateur dont vous disposez.

## Quelle est la différence entre une mise à jour régulière et forcée ? {#regularforcedupdates}

Les mises à jour régulières **scheduled** processus pendant que les mises à jour forcées sont **processus manuels initiés par vous**. Si vous avez des heures d’interruption, ou une période où [!DNL MBI] ne doit pas mettre à jour vos données : forcer une mise à jour déclenche un cycle qui ne respecte pas les limitations de la période de blackout.

## Pourquoi le cycle de mise à jour prend-il beaucoup de temps ? {#updatecycletime}

De nombreux facteurs peuvent ajouter à un temps de mise à jour déjà long. Certain [méthodes de réplication](../data-warehouse-mgr/cfg-replication-methods.md), [fréquences de recontrôle supérieures](../data-warehouse-mgr/cfg-data-rechecks.md), et le nombre de tableaux de bord et de graphiques ne représente que quelques contributeurs. Adobe recommande [reconfiguration de certains de vos paramètres](../../best-practices/reduce-update-cycle-time.md) et [optimisation de la base de données pour les analyses](../../best-practices/opt-db-analysis.md) pour réduire les temps de mise à jour.

## Puis-je être informé de la fin d’un cycle de mise à jour ? {#notifyupdate}

Si une mise à jour est en cours, un lien se trouve sur la variable `Connections` page que vous pouvez utiliser pour demander une notification par courrier électronique une fois le cycle terminé.

## Pourquoi[!DNL Google ECommerce]données différentes de ma base de données ? {#ecommdatabase}

Incohérences entre les [!DNL Google Analytics] et votre base de données peut survenir pour diverses raisons. Le suivi n’étant pas correctement activé, les utilisateurs qui visitent incognito et les événements de clic ne fonctionnent pas correctement sont quelques exemples. Si vos recettes et commandes ne semblent pas appropriées, [utiliser cet article ;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=en) pour diagnostiquer le problème.

## Comment résoudre un problème d’incohérence des données ? {#datadiscrepancy}

Adobe sait que voir des données incohérentes peut être une expérience frustrante. Essayez d’utiliser la variable [Liste de contrôle des écarts de données](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html?lang=en) ou [Tutoriel sur les exportations de données](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=en) pour diagnostiquer le problème. Si vous êtes toujours en panne, [support technique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
