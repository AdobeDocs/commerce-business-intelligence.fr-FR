---
title: Données de panneau mixte attendues
description: Explorez les principaux tableaux de données que vous pouvez importer à partir de Mixpanel dans votre [!DNL MBI] compte .
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Valeur attendue [!DNL Mixpanel] data

Après [vous avez connecté votre [!DNL Mixpanel] account](../integrations/mixpanel.md), vous pouvez utiliser la variable [Gestionnaire de Data Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) pour effectuer facilement le suivi des champs de données pertinents à des fins d’analyse.

Dans cet article, nous explorons les principaux tableaux de données à partir desquels vous pouvez importer des [!DNL Mixpanel] dans [!DNL MBI] compte . Les tableaux suivants seront créés dans votre entrepôt de données après la connexion de Mixpanel. Pour visualiser tous les champs disponibles pour le tracking, cliquez sur les liens de la colonne du nom du tableau.

>[!NOTE]
>
>En raison des limites de la variable [!DNL Mixpanel] API, données historiques : données datant de plus de sept (7) jours à compter de la date de connexion à [!DNL MBI] - ne sera pas répliqué.

| **Nom de la table** | **Description** |
|-----|-----|
| [`mixpanel\_export`](https://mixpanel.com/docs/api-documentation/exporting-raw-data-you-inserted-into-mixpanel#datafeed) | Ce tableau contient des données d’événement brutes, notamment l’événement, les dates d’événement et le compartiment de la plateforme. |
| [`mixpanel\_funnels`](https://mixpanel.com/docs/api-documentation/data-export-api#funnels-default) | Ce tableau contient des données sur vos entonnoirs, notamment l’identifiant de l’entonnoir, la durée de l’entonnoir (nombre de jours pendant lesquels l’utilisateur doit terminer l’entonnoir) et les dates de début et de fin de l’entonnoir. |
| [`mixpanel\_engage`](https://mixpanel.com/docs/api-documentation/data-export-api#engage-default) | Il contient les données de People Analytics, notamment les ID de session, les informations sur la page et l’utilisateur, ainsi que la date et l’heure de la dernière consultation de l’utilisateur. |

{style=&quot;table-layout:auto&quot;}

## Documentation connexe

* [Connexion [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
