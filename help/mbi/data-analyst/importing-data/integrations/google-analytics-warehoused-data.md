---
title: Données Google Analytics Warehouse attendues
description: Apprenez à interagir avec vos données stockées dans Google Analytics.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# Données de [!DNL Google Analytics Warehoused] attendues

>[!NOTE]
>
>Nécessite des [autorisations d’administrateur](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>Certaines informations ont été utilisées avec la permission de vos amis de [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] intégration dans [!DNL Commerce Intelligence] utilise l’[!DNL Google Analytics] [API Core Reporting](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>Pour éviter des résultats inattendus ou absurdes, vérifiez que toutes les dimensions que vous utilisez sont [compatibles avec une ou plusieurs mesures](https://ga-dev-tools.google/dimensions-metrics-explorer/) que vous utilisez dans le `Report Builder`.

Un seul tableau, appelé `report`, est créé dans votre Data Warehouse.

Le schéma de ce tableau est composé des mesures et des dimensions que vous avez sélectionnées lors du processus de configuration et de deux autres colonnes : `start-date` et `end-date`.

Si, par exemple, vous avez sélectionné les mesures et dimensions suivantes lors de la configuration :

* `Metrics` : `ga:users`
* `Dimensions` : `ga:month`

Le tableau ressemble à l’exemple ci-dessous.

| **Nom de la colonne** | **Description** |
|-----|-----|
| `\_id` | Cette colonne est la `primary key`. |
| `\_rjm\_record\_hash` | Identifiant unique [!DNL Commerce Intelligence]. Cette colonne est créée par [!DNL Commerce Intelligence]. |
| `\_updated\_at` | Cette colonne contient la dernière mise à jour de la ligne de données. Cette colonne est créée par [!DNL Commerce Intelligence]. |
| `start-date` | Identification du jour auquel la ligne est destinée. |
| `end-date` | Identification du jour auquel la ligne est destinée. |
| `month` | Dimension sélectionnée : mois de la session, entier à deux chiffres compris entre 01 et 12. |
| `users` | Mesure sélectionnée : nombre total d’utilisateurs pour la période demandée. |

{style="table-layout:auto"}

## Quelle est la différence entre [!DNL Google Analytics Warehoused] et [!DNL Live Integration] ?

Le principal différenciateur est qu’une intégration est stockée ([!DNL Google Analytics Warehoused]) et que l’autre ne l’est pas ([!DNL Google Analytics Live]). En cas de [!DNL Google Analytics Warehoused], cela permet de manipuler vos données [!DNL Google Analytics] et vous donne la possibilité de combiner des [!DNL Google Analytics] et d’autres sources de données pour créer des rapports pertinents.

Regardez [!DNL Google Analytics] campagnes publicitaires pour un exemple de ce qui peut être fait du point de vue de la manipulation. Supposons que vous ayez plusieurs campagnes publicitaires pour le 4e trimestre avec des noms différents. Les campagnes sont le résultat d’une initiative marketing spécifique. Avec les données entreposées, vous pouvez créer une colonne qui recherche les noms de campagne en question et renvoie le nom de l’initiative T4 de `Operation Dumbo`.

L&#39;aspect de combinaison permet de joindre des données [!DNL Google Analytics] à d&#39;autres données afin de réaliser des analyses. Par exemple, prenez `Total Time On Site By Ad Campaign` données de [!DNL Google Analytics] et associez-les aux données `Total Spent Per Campaign` de [!DNL Facebook Ads] pour obtenir une vue d’ensemble du coût de l’engagement.

Avec l’intégration [!DNL Google Analytics Live], en revanche, chaque graphique [!DNL Google Analytics] ressemble à un petit silo qui n’est pas stocké dans votre Data Warehouse [!DNL Commerce Intelligence].

## Connexe :

* [Connexion  [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
