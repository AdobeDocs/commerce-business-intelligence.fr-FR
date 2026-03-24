---
title: Données Mixpanel attendues
description: Explorez les principaux tableaux de données que vous pouvez importer depuis Mixpanel dans votre compte  [!DNL Commerce Intelligence] .
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/iM6GzisImrjed7uCZf6lf6HIze9MwWdhq2gEP-IrIXA
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 187
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
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | Ce tableau contient des données sur vos entonnoirs, notamment l’identifiant funnel, la durée du funnel (nombre de jours dont l’utilisateur dispose pour terminer le funnel), ainsi que les dates de début et de fin du funnel. |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | Contient des données provenant de People Analytics, notamment les ID de session, des informations sur la page et l’utilisateur, ainsi que la date et l’heure de la dernière consultation de l’utilisateur. |

{style="table-layout:auto"}

## Documentation connexe

* [Connexion  [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
