---
title: Comprendre les résultats entre la base de données et l'éditeur SQL
description: Découvrez comment comprendre les résultats entre la base de données et l’éditeur SQL.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# Résultats de la base de données par rapport aux résultats [!DNL SQL Editor]

Vous êtes peut-être curieux de savoir quel est le champ `Last successful update began` dans votre page `Integrations` :

![Last_successful_update.png](../../../assets/Last_successful_update.png)

## Comprendre le champ `timestamp`

Elle affiche la `timestamp` de début (dans le fuseau horaire défini sur votre compte) du _dernier cycle de mise à jour réussi_ sur votre compte.

- Si l&#39;une des tables synchronisées rencontre un problème lors du dernier cycle de mise à jour, cet horodatage n&#39;est *pas mis à jour*.
- Par conséquent, il peut y avoir des cas où les rapports ont été mis à jour avec des données récentes, mais où la *Dernière mise à jour réussie a commencé* est toujours en retard.

## Identifier le dernier point de données « réel »

Le dernier point de données d’une intégration spécifique est déterminé par l’horodatage `Last Data Point Received` situé à droite de chaque intégration. Cet horodatage fait référence au dernier point auquel votre Data Warehouse a reçu avec succès des points de données de cette source, qu’il s’agisse d’une base de données, d’une API ou d’une intégration tierce.

Pour vérifier l’actualisation des données de *tableaux spécifiques*, Adobe recommande de créer un rapport [[!DNL SQL]  rapide](../../dev-reports/sql-rpt-bldr.md) qui effectue une `MAX(timestamp)` sur le tableau le plus important de votre compte. La comparaison de cet horodatage avec le `Last Data Point` indique si le problème a affecté l’ensemble du compte ou un sous-ensemble des tables. Adobe recommande de le faire pour trois à quatre tableaux importants couramment utilisés.

- Si les valeurs `MAX(timestamp)` sont plus récentes que `Last Data Point Received`, cela signifie qu’un sous-ensemble des tables a été affecté, mais que le cycle de mise à jour du compte global est stable.
- Si les valeurs `MAX(timestamp)` sont égales ou antérieures à `Last Data Point Received`, cela signifie que le cycle de mise à jour du compte a été affecté. Dans ce cas, [soumettez un ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
