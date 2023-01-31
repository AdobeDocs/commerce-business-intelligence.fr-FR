---
title: Données Google Analytics stockées attendues
description: Découvrez comment interagir avec vos données stockées Google Analytics.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# Valeur attendue [!DNL Google Analytics] Données stockées

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>Certaines informations ont été utilisées avec la permission de nos amis sur [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] intégration dans [!DNL MBI] utilise la variable [!DNL Google Analytics] [API Core Reporting](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>Pour éviter des résultats inattendus ou absurdes, vérifiez que toutes les dimensions utilisées sont [compatible avec la ou les mesures](https://developers.google.com/analytics/devguides/reporting/core/dimsmets) vous utilisez dans la variable `Report Builder`.

Une seule table, appelée `report` - sera créé dans votre Data Warehouse.

Le schéma de ce tableau sera composé des mesures et Dimensions que vous avez sélectionnées lors du processus de configuration et de deux autres colonnes : `start-date` et `end-date`.

Si, par exemple, vous avez sélectionné les mesures et Dimensions suivantes lors de la configuration :

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

Le tableau ressemble à l’exemple ci-dessous.

| **Nom de la colonne** | **Description** |
|-----|-----|
| `\_id` | Cette colonne correspond au `primary key`. |
| `\_rjm\_record\_hash` | [!DNL MBI] identifiant unique. Cette colonne est créée par [!DNL MBI]. |
| `\_updated\_at` | Cette colonne contient la dernière fois que la ligne de données a été mise à jour. Cette colonne est créée par [!DNL MBI]. |
| `start-date` | Identification du jour de la ligne. |
| `end-date` | Identification du jour de la ligne. |
| `month` | Dimension sélectionnée : Mois de la session, entier à deux chiffres compris entre 01 et 12. |
| `users` | Mesure sélectionnée : Nombre total d’utilisateurs pour la période demandée. |

{style=&quot;table-layout:auto&quot;}

## Rappel : Différence entre l’intégration de l’entrepôt de Google Analytics et l’intégration en direct

Le principal différenciateur est qu’une intégration est stockée ([!DNL Google Analytics Warehoused]), et l’autre n’est pas ([!DNL Google Analytics Live]). Dans le cas de [!DNL Google Analytics Warehoused], cela permet de manipuler votre [!DNL Google Analytics] et vous donne la possibilité de combiner des [!DNL Google Analytics] et d’autres sources de données pour créer des rapports pertinents.

Regardons de plus près [!DNL Google Analytics] campagnes publicitaires pour un exemple de ce qui peut être fait du point de vue de la manipulation. Supposons que vous ayez plusieurs campagnes publicitaires portant des noms différents pour le quatrième trimestre. Les campagnes sont le résultat d’une initiative marketing spécifique. Avec les données stockées, nous pouvons créer une nouvelle colonne qui recherche les noms des campagnes en question et renvoie le nom de l&#39;initiative du quatrième trimestre de `Operation Dumbo`.

L’aspect de combinaison permet [!DNL Google Analytics] données à associer à d&#39;autres données afin de mener des analyses. Par exemple, prenez `Total Time On Site By Ad Campaign` des données provenant de [!DNL Google Analytics] et rejoignez-le contre `Total Spent Per Campaign` des données provenant de [!DNL Facebook Ads] pour obtenir une vue d’ensemble de l’engagement qui vous coûte.

Avec le [!DNL Google Analytics Live] d’autre part, chaque [!DNL Google Analytics] Le graphique est comme un petit silo qui n’est pas stocké dans votre [!DNL MBI] entrepôt de données.

## En rapport :

* [Connexion [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
