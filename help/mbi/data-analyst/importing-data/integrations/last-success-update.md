---
title: Présentation des résultats entre la base de données et SQL Editor
description: Découvrez comment comprendre les résultats entre la base de données et l’éditeur SQL.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# Résultats de la base de données `SQL Editor` Résultats

Vous êtes peut-être curieux de ce que la variable `Last successful update began` se trouve à l’intérieur de votre `Integrations` page :

![Last_success_update.png](../../../assets/Last_successful_update.png)

## Comprendre le `timestamp` field

Il affiche le début `timestamp` (dans le fuseau horaire défini sur votre compte) de la variable _dernier cycle de mise à jour réussi_ sur votre compte.

- Si l’une des tables synchronisées a rencontré un problème lors du dernier cycle de mise à jour, cet horodatage est *non mis à jour*.
- Par conséquent, il peut arriver que des rapports aient été mis à jour avec des données récentes, mais la variable *La dernière mise à jour réussie a commencé* est encore à la traîne.

## Identifier le dernier point de données &quot;réel&quot;

Le dernier point de données pour une intégration particulière est déterminé par la variable `Last Data Point Received` `timestamp` situé à droite de chaque intégration. Cet horodatage fait référence au dernier point où votre entrepôt de données a bien reçu des points de données de cette source, qu’il s’agisse d’une base de données, d’une API ou d’une intégration tierce.

Pour vérifier l’actualisation des données de *tables spécifiques*, nous vous recommandons de créer rapidement une [Rapport SQL](../../dev-reports/sql-rpt-bldr.md) qui effectue une `MAX(timestamp)` sur la table la plus importante de votre compte. Comparaison de cet horodatage au `Last Data Point` indique si le problème a affecté l’intégralité du compte ou un sous-ensemble des tables. Nous vous recommandons de le faire pour trois à quatre tables importantes, généralement utilisées.

- Si la variable `MAX(timestamp)` sont plus récentes que `Last Data Point Received`, cela signifie qu’un sous-ensemble des tables a été affecté, mais que le cycle de mise à jour global du compte est stable.
- Si la variable `MAX(timestamp)` est égale ou antérieure à `Last Data Point Received`, cela signifie que le cycle de mise à jour du compte a été affecté. Dans ce cas, [envoi d’un ticket d’assistance](../../../guide-overview.md).
