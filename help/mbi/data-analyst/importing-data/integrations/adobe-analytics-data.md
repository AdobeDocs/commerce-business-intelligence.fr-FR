---
title: Données  [!DNL Adobe Analytics] attendues
description: Découvrez les étapes de connexion de votre instance RDS.
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Données [!DNL Adobe Analytics] attendues

L’intégration [!DNL Adobe Analytics] pour [!DNL Adobe Commerce Intelligence] utilise l’ [API de création de rapports Analytics 2.0](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>Pour vous assurer d’obtenir les données attendues, vous pouvez d’abord créer un rapport dans le Workspace [!DNL Adobe Analytics] avec les mesures et dimensions souhaitées. Vous pouvez ainsi vérifier la compatibilité et la disponibilité des données.

Une table par suite de rapports connectée appelée `report-suite-<ID>` (où `<ID>` est un identifiant unique généré par [!DNL Commerce Intelligence]) est créé dans votre Data Warehouse.

Le schéma de ce tableau est composé des mesures et des dimensions que vous avez sélectionnées dans le processus de configuration de l’intégration. Plusieurs colonnes supplémentaires sont également générées par [!DNL Commerce Intelligence], à des fins d’identification.

Par exemple, si vous avez sélectionné la mesure et la dimension suivantes lors de la configuration :
- `Metric` : `Page views`
- `Dimension` : `Page`

Le tableau contiendra les colonnes suivantes :

| Nom de la colonne | Description |
| --- | --- |
| `_id` | Cette colonne est la clé primaire. |
| `_item_hash` | [!DNL Commerce Intelligence] identifiant unique. Cette colonne est créée par [!DNL Commerce Intelligence]. |
| `_updated_at` | Cette colonne contient la dernière mise à jour de la ligne de données. Il est créé par [!DNL Commerce Intelligence]. |
| `start_date` | Date de début des données incluses pour la ligne. `start_date` est toujours 00:00 du même jour sur une ligne. |
| `end_date` | Date de fin des données incluses pour la ligne. `end_date` est toujours 23:59 du même jour sur une ligne. |
| `page_views` | Mesure sélectionnée : nombre total de pages vues pour la période identifiée. |
| `page` | Dimension sélectionnée : noms de page individuels avec vues suivies. |

Contrôlez quelles mesures et dimensions sélectionnées disposent de données dans votre table [!DNL Commerce Intelligence] en utilisant les options *sync* ou *unsync* de la page `Data Warehouse`. Les colonnes non synchronisées apparaissent en gris. Si vous arrêtez de synchroniser une colonne, vous pouvez recommencer la synchronisation ultérieurement.

## Limites actuelles

Cette section décrit les limites de l’intégration [!DNL Adobe Analytics] pour [!DNL Commerce Intelligence].

| Limitation | Description |
| --- | --- |
| `Historical data period` | Comme pour les autres intégrations tierces, l’intégration [!DNL Adobe Analytics] extrait une quantité limitée de données historiques, puis continue à conserver les données à jour. La période historique est configurée sur 2 semaines. |
| `Empty component combinations` | Certaines combinaisons de mesures et de dimensions ne contiennent aucune donnée. Si une telle combinaison est sélectionnée pour la réplication, [!DNL Commerce Intelligence] exclut la colonne de la table répliquée. Pour éviter de sélectionner une telle combinaison, vous pouvez d’abord créer un rapport dans le [[!DNL Adobe Analytics] Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html?lang=fr) afin de vérifier que vous obtenez les données attendues. |
| `Re-authorization cadence` | La réautorisation de l’intégration [!DNL Adobe Analytics] est requise toutes les deux semaines. Pour réautoriser, accédez à la page Modifier pour l’intégration et cliquez sur **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] fournit des données de mesure pour une dimension à la fois. Si vous sélectionnez plusieurs dimensions lors de la configuration, chaque ligne de votre tableau [!DNL Commerce Intelligence] contient une valeur de dimension unique et des valeurs nulles pour chacune des dimensions. |
