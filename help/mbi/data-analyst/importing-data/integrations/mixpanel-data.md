---
title: Données de panneau mixte attendues
description: Explorez les tables de données principales que vous pouvez importer depuis Mixpanel dans votre compte  [!DNL Commerce Intelligence] .
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Données [!DNL Mixpanel] attendues

Une fois [que vous avez connecté votre  [!DNL Mixpanel] compte](../integrations/mixpanel.md), vous pouvez utiliser le [Gestionnaire de Data Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) pour facilement suivre les champs de données pertinents à des fins d’analyse.

Cette rubrique explore les tables de données principales que vous pouvez importer de [!DNL Mixpanel] dans votre compte [!DNL Commerce Intelligence]. Les tables suivantes seront créées dans votre Data Warehouse après la connexion à [!DNL Mixpanel]. Pour visualiser tous les champs disponibles pour le tracking, cliquez sur les liens de la colonne du nom du tableau.

>[!NOTE]
>
>En raison des limites de l’API [!DNL Mixpanel], les données historiques - données datant de plus de sept (7) jours à compter de la date de connexion à [!DNL Commerce Intelligence] - ne sont pas répliquées.

| **Nom de la table** | **Description** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | Ce tableau contient des données d’événement brutes, notamment l’événement, les dates d’événement et le compartiment de la plateforme. |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | Ce tableau contient des données sur vos entonnoirs, notamment l’identifiant de l’entonnoir, la durée de l’entonnoir (nombre de jours pendant lesquels l’utilisateur doit terminer l’entonnoir) et les dates de début et de fin de l’entonnoir. |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | Il contient les données de People Analytics, notamment les ID de session, les informations sur la page et l’utilisateur, ainsi que la date et l’heure de la dernière consultation de l’utilisateur. |

{style="table-layout:auto"}

## Documentation connexe

* [Connexion [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
