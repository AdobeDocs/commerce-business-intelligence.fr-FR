---
title: Données Zendesk attendues
description: Découvrez les principaux tableaux de données que vous pouvez importer de Zendesk dans Commerce Intelligence, y compris des liens vers une documentation supplémentaire sur les données Zendesk.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Données [!DNL Zendesk] attendues

Une fois [que vous avez connecté votre  [!DNL Zendesk] compte](../integrations/zendesk.md), vous pouvez utiliser le [Gestionnaire de Data Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) pour facilement suivre les champs de données pertinents à des fins d’analyse.

Cette rubrique explore les tables de données principales que vous pouvez importer de [!DNL Zendesk] dans [!DNL Adobe Commerce Intelligence], y compris les liens vers une documentation supplémentaire sur les données [!DNL Zendesk].

| Nom de la table | Description |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | La table `Audits` enregistre l’activité associée à un ticket, y compris les modifications d’état et les réponses du client et de l’agent. Cette table comprend un ID de ticket qui renvoie à la table `Tickets`, ce qui vous permet d’analyser le temps de première réponse et l’heure de résolution de chaque ticket. |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | La table `audit_~\_events` est l’enfant de la table `audits` et enregistre des détails supplémentaires sur un événement de ticket. |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | La table `Organizations` enregistre les informations de la société sur vos utilisateurs finaux telles que le nom, l’identifiant, les noms de domaine associés, les balises et tous les champs personnalisés. |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | La table `Tickets` enregistre tous les détails du ticket, y compris l’horodatage `created_at` et les `requester\_id` et `assignee\_id`, ce qui vous permet de lier un ticket à un utilisateur final et un agent dans la table `Users` respectivement. |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | La table `ticket fields` contient des informations sur les champs de texte de base et les champs de ticket personnalisés de votre compte. Les attributs de cette table incluent le champ `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`, les informations spécifiques à l’agent et à l’utilisateur final, ainsi que les informations de création et de mise à jour. |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | La table `Users` contient tous les détails sur les utilisateurs finaux et les agents, y compris le nom et l’email de l’individu. Cela vous permet d’analyser à la fois l’engagement de vos utilisateurs finaux et les performances de vos agents. |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | Les groupes sont la manière dont les agents sont organisés dans votre compte Zendesk. La table `Groups` enregistre des informations telles que `group ID`, `URL`, `name`, ainsi que des informations de création et de mise à jour. |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | Les macros sont des actions définies par vous qui modifient les valeurs des champs d’un ticket. Ce tableau contient des attributs tels que le titre, l’identifiant, les actions, les restrictions et les informations de création et de mise à jour de la macro. |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | La table `Tags` contient une liste de toutes les balises de votre compte. |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | Ce tableau contient des données sur les mesures des tickets. Les champs incluent les `ticket ID`, `URL` et le nombre de groupes, de personnes désignées, de réouvertures, de réponses, de temps de réponse (en minutes), de temps de résolution complet et de dernières mises à jour (par exemple, statut, personne désignée ou demandeur). |

{style="table-layout:auto"}

## Associé

* [Connexion à Zendesk](../integrations/zendesk.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
