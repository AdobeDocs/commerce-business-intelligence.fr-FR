---
title: Présentation des résultats entre la base de données et SQL Editor
description: Découvrez comment comprendre les résultats entre la base de données et l’éditeur SQL.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# Résultats de la base de données et [!DNL SQL Editor] résultats

Vous êtes peut-être curieux de savoir quel champ `Last successful update began` se trouve dans votre page `Integrations` :

![Last_success_update.png](../../../assets/Last_successful_update.png)

## Comprendre le champ `timestamp`

Il affiche le début `timestamp` (dans le fuseau horaire défini sur votre compte) du _dernier cycle de mise à jour réussi_ de votre compte.

- Si l’une des tables synchronisées a rencontré un problème au cours du dernier cycle de mise à jour, cet horodatage est *non mis à jour*.
- Par conséquent, il peut arriver que des rapports aient été mis à jour avec de nouvelles données, mais la *dernière mise à jour réussie commencée* est toujours en retard.

## Identifier le dernier point de données &quot;réel&quot;

Le dernier point de données pour une intégration particulière est déterminé par l’horodatage `Last Data Point Received` situé à droite de chaque intégration. Cet horodatage fait référence au dernier point où votre Data Warehouse a bien reçu des points de données de cette source, qu’il s’agisse d’une base de données, d’une API ou d’une intégration tierce.

Pour vérifier l&#39;actualisation des données provenant de *tables spécifiques*, Adobe recommande de créer un [[!DNL SQL] rapport](../../dev-reports/sql-rpt-bldr.md) rapide qui exécute un `MAX(timestamp)` sur la table la plus importante de votre compte. La comparaison de cet horodatage à `Last Data Point` indique si le problème a affecté l’ensemble du compte ou un sous-ensemble des tables. Adobe recommande de le faire pour trois à quatre tables importantes, couramment utilisées.

- Si les valeurs `MAX(timestamp)` sont plus récentes que `Last Data Point Received`, cela signifie qu’un sous-ensemble des tables a été affecté, mais que le cycle de mise à jour global du compte est stable.
- Si les valeurs `MAX(timestamp)` sont égales ou antérieures à `Last Data Point Received`, cela signifie que le cycle de mise à jour du compte a été affecté. Dans ce cas, [soumettez un ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
