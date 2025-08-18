---
title: Données Mixpanel attendues
description: Explorez les principaux tableaux de données que vous pouvez importer depuis Mixpanel dans votre compte  [!DNL Commerce Intelligence] .
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Données de [!DNL Mixpanel] attendues

Une fois [vous avez connecté votre [!DNL Mixpanel] compte](../integrations/mixpanel.md), vous pouvez utiliser le [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) pour effectuer facilement le suivi des champs de données pertinents à analyser.

Cette rubrique explore les principaux tableaux de données que vous pouvez importer à partir de [!DNL Mixpanel] dans votre compte [!DNL Commerce Intelligence]. Les tableaux suivants seront créés dans votre Data Warehouse après la connexion [!DNL Mixpanel]. Pour visualiser tous les champs disponibles pour le tracking, cliquez sur les liens dans la colonne du nom de la table.

>[!NOTE]
>
>En raison des limitations de l’API [!DNL Mixpanel], les données historiques (données datant de plus de sept (7) jours à compter de la date de connexion à [!DNL Commerce Intelligence]) ne sont pas répliquées.

| **Nom de la table** | **Description** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | Ce tableau contient les données brutes de l’événement, y compris l’événement, les dates de l’événement et l’intervalle de la plateforme. |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | Ce tableau contient des données sur vos entonnoirs, y compris l’identifiant de l’entonnoir, sa durée (nombre de jours dont dispose l’utilisateur pour terminer l’entonnoir), ainsi que les dates de début et de fin de l’entonnoir. |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | Contient des données provenant de People Analytics, notamment les ID de session, des informations sur la page et l’utilisateur, ainsi que la date et l’heure de la dernière consultation de l’utilisateur. |

{style="table-layout:auto"}

## Documentation connexe

* [Connexion  [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
