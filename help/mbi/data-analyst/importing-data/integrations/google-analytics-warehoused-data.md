---
title: Données Google Analytics stockées attendues
description: Découvrez comment interagir avec vos données stockées Google Analytics.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# Données [!DNL Google Analytics Warehoused] attendues

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>Certaines informations ont été utilisées avec la permission de vos amis à [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

L&#39;intégration [!DNL Google Analytics Warehoused] dans [!DNL Commerce Intelligence] utilise l&#39; [!DNL Google Analytics] [API Core Reporting](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>Pour éviter des résultats inattendus ou absurdes, vérifiez que toutes les dimensions que vous utilisez sont [compatibles avec une ou plusieurs mesures](https://ga-dev-tools.google/dimensions-metrics-explorer/) que vous utilisez dans `Report Builder`.

Une seule table, appelée `report`, est créée dans votre Data Warehouse.

Le schéma de cette table est composé des mesures et Dimensions que vous avez sélectionnées lors du processus de configuration et de deux autres colonnes : `start-date` et `end-date`.

Si, par exemple, vous avez sélectionné les mesures et Dimensions suivantes lors de la configuration :

* `Metrics` : `ga:users`
* `Dimensions` : `ga:month`

Le tableau ressemble à l’exemple ci-dessous.

| **Nom de colonne** | **Description** |
|-----|-----|
| `\_id` | Cette colonne est le `primary key`. |
| `\_rjm\_record\_hash` | [!DNL Commerce Intelligence] identifiant unique. Cette colonne est créée par [!DNL Commerce Intelligence]. |
| `\_updated\_at` | Cette colonne contient la dernière mise à jour de la ligne de données. Cette colonne est créée par [!DNL Commerce Intelligence]. |
| `start-date` | Identification du jour de la ligne. |
| `end-date` | Identification du jour de la ligne. |
| `month` | Dimension sélectionnée : mois de la session, entier à deux chiffres compris entre 01 et 12. |
| `users` | Mesure sélectionnée : nombre total d’utilisateurs pour la période demandée. |

{style="table-layout:auto"}

## Quelle est la différence entre [!DNL Google Analytics Warehoused] et [!DNL Live Integration] ?

Le principal différenciateur est qu’une intégration est stockée ([!DNL Google Analytics Warehoused]) et l’autre non ([!DNL Google Analytics Live]). Dans les cas de [!DNL Google Analytics Warehoused], cela permet la manipulation de vos données [!DNL Google Analytics] et vous permet de combiner [!DNL Google Analytics] et d’autres sources de données pour créer des rapports pertinents.

Examinez [!DNL Google Analytics] campagnes publicitaires pour obtenir un exemple de ce qui peut être fait du point de vue de la manipulation. Supposons que vous ayez plusieurs campagnes publicitaires portant des noms différents pour le quatrième trimestre. Les campagnes sont le résultat d’une initiative marketing spécifique. Avec les données stockées, vous pouvez créer une colonne qui recherche les noms des campagnes en question et renvoie le nom de l&#39;initiative du quatrième trimestre `Operation Dumbo`.

L’aspect de combinaison permet de joindre [!DNL Google Analytics] données à d’autres données afin d’effectuer des analyses. Par exemple, prenez les données `Total Time On Site By Ad Campaign` de [!DNL Google Analytics] et rejoignez-les par rapport aux données `Total Spent Per Campaign` de [!DNL Facebook Ads] pour obtenir une vue d&#39;ensemble de l&#39;engagement qui vous coûte.

Avec l&#39;intégration [!DNL Google Analytics Live] en revanche, chaque graphique [!DNL Google Analytics] est comme un petit silo qui n&#39;est pas stocké dans votre Data Warehouse [!DNL Commerce Intelligence].

## En rapport :

* [Connexion [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
