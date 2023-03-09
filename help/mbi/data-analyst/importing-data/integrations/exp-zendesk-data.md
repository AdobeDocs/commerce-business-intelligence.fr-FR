---
title: Données Zendesk attendues
description: Découvrez les principaux tableaux de données que vous pouvez importer depuis Zendesk dans MBI, y compris des liens vers une documentation supplémentaire sur les données Zendesk.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# Données Zendesk attendues

Après [vous avez connecté votre [!DNL Zendesk] account](../integrations/zendesk.md), vous pouvez utiliser la variable [Gestionnaire de Data Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) pour effectuer facilement le suivi des champs de données pertinents à des fins d’analyse.

Cet article explore les principaux tableaux de données à partir desquels vous pouvez importer des [!DNL Zendesk] into [!DNL MBI], y compris des liens vers une documentation supplémentaire sur [!DNL Zendesk] data.

| Nom de la table | Description |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | Le `Audits` table des enregistrements activité associée à un ticket, y compris les modifications d’état et les réponses des clients et des agents. Ce tableau comprend un ID de ticket qui renvoie à la variable `Tickets` qui vous permet d’analyser le temps de première réponse et le temps de résolution pour chaque ticket. |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | Le `audit_~\_events` est l’enfant de la fonction `audits` et enregistre les détails supplémentaires d’un événement de ticket. |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | Le `Organizations` le tableau enregistre les informations de la société sur vos utilisateurs finaux telles que le nom, l’identifiant, les noms de domaine associés, les balises et les champs personnalisés. |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | Le `Tickets` le tableau enregistre tous les détails du ticket, y compris le `created_at` l’horodatage et la variable `requester\_id` et `assignee\_id`, qui vous permet de lier un ticket à un utilisateur final et à un agent dans la variable `Users` tableau, respectivement. |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | Le `ticket fields` contient des informations sur les champs de texte de base et les champs de ticket personnalisés de votre compte. Les attributs de ce tableau incluent le champ `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`, des informations spécifiques à l’agent et à l’utilisateur final, ainsi que des informations de création et de mise à jour. |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | Le `Users` le tableau contient tous les détails sur les utilisateurs finaux et les agents, y compris le nom et l’email de l’individu. Cela vous permet d’analyser à la fois l’engagement de vos utilisateurs finaux et les performances de vos agents. |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | Les groupes sont la manière dont les agents sont organisés dans votre compte Zendesk. Le `Groups` des informations d’enregistrement de tableau, telles que `group ID`, `URL`, `name`, ainsi que les informations de création et de mise à jour. |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | Les macros sont des actions définies par vous qui modifient les valeurs des champs d’un ticket. Ce tableau contient des attributs tels que le titre, l’identifiant, les actions, les restrictions et les informations de création et de mise à jour de la macro. |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | Le `Tags` contient une liste de toutes les balises de votre compte. |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | Ce tableau contient des données sur les mesures des tickets. Les champs incluent la variable `ticket ID`, `URL`, ainsi que le nombre de groupes, de personnes désignées, de réouvertures, de réponses, d’heures de réponse (en minutes), d’heures de résolution complètes et d’informations sur la dernière mise à jour (par exemple, état, personne désignée ou demandeur). |

{style="table-layout:auto"}

## Associé

* [Connexion à Zendesk](../integrations/zendesk.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
