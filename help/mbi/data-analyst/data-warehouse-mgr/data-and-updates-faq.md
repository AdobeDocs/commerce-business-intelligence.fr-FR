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
* [Pourquoi le cycle de mise à jour est-il long ?](#updatecycletime)
* [Puis-je être averti à la fin d’un cycle de mise à jour ?](#notifyupdate)
* [Pourquoi les données sont [!DNL Google ECommerce] elles différentes de ma base de données ?](#ecommdatabase)
* [Comment résoudre un problème lié à une incohérence des données ?](#datadiscrepancy)

## Pourquoi mes données ont-elles changé ? {#datachange}

Les valeurs du graphique peuvent changer tout au long de la journée en raison de la synchronisation de nouvelles données avec votre Data Warehouse. En outre, les valeurs des colonnes de données existantes peuvent changer en raison de [nouvelles vérifications](../data-warehouse-mgr/cfg-data-rechecks.md). Une revérification est un processus qui recherche les valeurs modifiées dans les colonnes de données, comme un statut de commande passant de `open` à `shipped`.

Il existe plusieurs façons différentes [pour vérifier le statut de votre cycle de mise à jour](../../best-practices/check-update-cycle.md), en fonction des paramètres d’autorisations de l’utilisateur ou de l’utilisatrice.

## Quelle est la différence entre une mise à jour régulière et forcée ? {#regularforcedupdates}

Les mises à jour régulières sont des processus **planifiés** tandis que les mises à jour forcées sont **des processus manuels que vous lancez**. Si vous avez des heures d&#39;interruption (ou une période pendant laquelle [!DNL Commerce Intelligence] ne devez pas mettre à jour vos données), forcer une mise à jour lance un cycle qui ne respecte pas les limites de la période d&#39;interruption.

## Pourquoi le cycle de mise à jour est-il long ? {#updatecycletime}

De nombreux facteurs peuvent s’ajouter à une durée de mise à jour déjà longue. Certaines [méthodes de réplication](../data-warehouse-mgr/cfg-replication-methods.md), [fréquence de vérification plus élevée](../data-warehouse-mgr/cfg-data-rechecks.md) et le nombre de tableaux de bord et de graphiques ne sont que quelques-unes des contributions. Adobe recommande de [reconfigurer certains de vos paramètres](../../best-practices/reduce-update-cycle-time.md) et [optimiser votre base de données pour analyse](../../best-practices/opt-db-analysis.md) afin de réduire le temps de mise à jour.

## Puis-je être averti à la fin d’un cycle de mise à jour ? {#notifyupdate}

Si une mise à jour est en cours, la page `Connections` contient un lien que vous pouvez utiliser pour demander une notification par e-mail une fois le cycle terminé.

## Pourquoi les données sont[!DNL Google ECommerce]elles différentes de ma base de données ? {#ecommdatabase}

Des incohérences entre [!DNL Google Analytics] et votre base de données peuvent survenir pour diverses raisons. Le suivi n’étant pas correctement activé, les utilisateurs qui visitent en navigation privée et les événements de clics ne fonctionnent pas correctement ne sont que quelques exemples. Si votre chiffre d’affaires et vos commandes ne vous semblent pas corrects, [consultez cette rubrique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) pour diagnostiquer un problème.

## Comment résoudre un problème lié à une incohérence des données ? {#datadiscrepancy}

Adobe sait que voir des données incohérentes peut être une expérience frustrante. Essayez d’utiliser la [Liste de contrôle des incohérences de données](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html) ou le tutoriel [Exportations de données](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html) pour diagnostiquer le problème. Si vous êtes toujours bloqué, [contactez l’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
