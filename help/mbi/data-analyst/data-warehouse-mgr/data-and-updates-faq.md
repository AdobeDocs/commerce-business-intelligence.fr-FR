---
title: Informations sur les données et les mises à jour
description: Découvrez comment vérifier le statut de votre cycle de mise à jour.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Informations sur les données et les mises à jour

* [Pourquoi mes données ont-elles changé ?](#datachange)
* [Quelle est la différence entre une mise à jour régulière et forcée ?](#regularforcedupdates)
* [Pourquoi le cycle de mise à jour prend-il beaucoup de temps ?](#updatecycletime)
* [Puis-je être informé de la fin d’un cycle de mise à jour ?](#notifyupdate)
* [Pourquoi  [!DNL Google ECommerce] données est-il différent de ma base de données ?](#ecommdatabase)
* [Comment résoudre un problème d’incohérence des données ?](#datadiscrepancy)

## Pourquoi mes données ont-elles changé ? {#datachange}

Les valeurs du graphique peuvent changer tout au long de la journée en raison de la synchronisation de nouvelles données avec votre Data Warehouse. En outre, les valeurs des colonnes de données existantes peuvent changer en raison de [rechecks](../data-warehouse-mgr/cfg-data-rechecks.md). Un nouveau contrôle est un processus qui recherche les valeurs modifiées dans les colonnes de données, comme un état de commande passant de `open` à `shipped`.

Il existe plusieurs manières de [ vérifier l’état de votre cycle de mise à jour ](../../best-practices/check-update-cycle.md), en fonction des paramètres d’autorisation de l’utilisateur.

## Quelle est la différence entre une mise à jour régulière et forcée ? {#regularforcedupdates}

Les mises à jour régulières sont des processus **planifiés** tandis que les mises à jour forcées sont des **processus manuels initiés par vous**. Si vous avez des heures d’interruption (ou une période pendant laquelle [!DNL Commerce Intelligence] ne doit pas mettre à jour vos données), forcer une mise à jour lance un cycle qui ne respecte pas les limites de la période d’interruption.

## Pourquoi le cycle de mise à jour prend-il beaucoup de temps ? {#updatecycletime}

De nombreux facteurs peuvent ajouter à un temps de mise à jour déjà long. Certaines [méthodes de réplication](../data-warehouse-mgr/cfg-replication-methods.md), [fréquences de contrôle supérieures](../data-warehouse-mgr/cfg-data-rechecks.md) et le nombre de tableaux de bord et de graphiques ne sont que quelques contributeurs. Adobe recommande de [reconfigurer certains de vos paramètres](../../best-practices/reduce-update-cycle-time.md) et [optimiser votre base de données pour l’analyse](../../best-practices/opt-db-analysis.md) afin de réduire les temps de mise à jour.

## Puis-je être informé de la fin d’un cycle de mise à jour ? {#notifyupdate}

Si une mise à jour est en cours, il existe un lien sur la page `Connections` que vous pouvez utiliser pour demander une notification par courrier électronique une fois le cycle terminé.

## Pourquoi [!DNL Google ECommerce]données est-il différent de ma base de données ? {#ecommdatabase}

Les disparités entre [!DNL Google Analytics] et votre base de données peuvent survenir pour diverses raisons. Le suivi n’étant pas correctement activé, les utilisateurs qui visitent incognito et les événements de clic ne fonctionnent pas correctement sont quelques exemples. Si vos recettes et commandes ne semblent pas correctes, [consultez cette rubrique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=fr) pour diagnostiquer un problème.

## Comment résoudre un problème d’incohérence des données ? {#datadiscrepancy}

Adobe sait que voir des données incohérentes peut être une expérience frustrante. Essayez d’utiliser le [tutoriel sur l’écart des données](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html?lang=fr) ou le [tutoriel sur les exportations de données](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=fr) pour diagnostiquer le problème. Si vous êtes toujours en panne, [contactez l&#39;assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr).
