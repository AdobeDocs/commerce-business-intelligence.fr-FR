---
title: Données Zendesk attendues
description: Découvrez les principaux tableaux de données que vous pouvez importer de Zendesk dans Commerce Intelligence, y compris des liens vers de la documentation supplémentaire sur les données Zendesk.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Données de [!DNL Zendesk] attendues

Une fois [vous avez connecté votre [!DNL Zendesk] compte](../integrations/zendesk.md), vous pouvez utiliser le [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) pour effectuer facilement le suivi des champs de données pertinents à analyser.

Cette rubrique explore les principaux tableaux de données que vous pouvez importer depuis [!DNL Zendesk] vers [!DNL Adobe Commerce Intelligence], y compris des liens vers de la documentation supplémentaire sur les données [!DNL Zendesk].

| Nom de la table | Description |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | La table `Audits` enregistre l’activité associée à un ticket, y compris les modifications de statut et les réponses du client et de l’agent. Ce tableau comprend un identifiant de ticket qui renvoie au tableau `Tickets`, ce qui vous permet d’analyser le temps jusqu’à la première réponse et le temps jusqu’à la résolution pour chaque ticket. |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | La table `audit_~\_events` est l’enfant de la table `audits` et enregistre les détails supplémentaires d’un événement de ticket. |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | Le tableau `Organizations` enregistre les informations de la société sur vos utilisateurs finaux, telles que le nom, l’identifiant, les noms de domaine associés, les balises et tout champ personnalisé. |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | La table `Tickets` enregistre tous les détails du ticket, y compris l’horodatage `created_at` et les `requester\_id` et `assignee\_id`, ce qui vous permet de lier un ticket à un utilisateur final et à un agent dans la table `Users`, respectivement. |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | Le tableau `ticket fields` contient des informations sur les champs de texte de base et les champs de ticket personnalisés dans votre compte . Les attributs de ce tableau incluent les informations spécifiques aux champs `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`, aux agents et aux utilisateurs finaux, ainsi que les informations de création et de mise à jour. |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | Le tableau `Users` comprend tous les détails sur les utilisateurs finaux et les agents, y compris le nom et l’adresse e-mail de la personne. Vous pouvez ainsi analyser à la fois l’engagement des utilisateurs finaux et les performances de vos agents. |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | Les groupes sont la manière dont les agents sont organisés sur votre compte Zendesk. Le tableau `Groups` enregistre des informations telles que les informations de `group ID`, de `URL`, de `name`, de création et de mise à jour. |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | Les macros sont des actions que vous définissez et qui modifient les valeurs des champs d’un ticket. Ce tableau contient des attributs tels que le titre, l&#39;ID, les actions, les restrictions, ainsi que des informations sur la création et la mise à jour de la macro. |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | Le tableau `Tags` contient la liste de toutes les balises de votre compte. |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | Cette table contient des données sur les mesures de ticket. Les champs incluent le `ticket ID`, le `URL` et le nombre de groupes, de personnes désignées, de réouvertures, de réponses, d’heures de réponse (en minutes), d’heures de résolution complète et d’informations sur la dernière mise à jour (par exemple, le statut, la personne désignée ou le demandeur). |

{style="table-layout:auto"}

## Connexe

* [Connexion à Zendesk](../integrations/zendesk.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=fr)
