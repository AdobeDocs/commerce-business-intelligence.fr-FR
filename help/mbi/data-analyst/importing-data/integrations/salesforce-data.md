---
title: Données Salesforce attendues
description: Découvrez les objets pris et non pris en charge dans les données Salesforce.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/eBX3Y0luu60A8PSAF43H6O3fsYjJnSWzyIybSOcSELE
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
source-wordcount: 117
ht-degree: 0%

---

# Données de [!DNL Salesforce] attendues

Une fois la [[!DNL Salesforce] configuration](../integrations/salesforce.md) terminée, une table pour chaque [objet](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm) interrogeable, nommée `sf_/\{sobject-name}`, est créée dans votre Data Warehouse.

>[!NOTE]
>
>La structure (colonnes) de chaque tableau dépend des champs contenus dans l’objet .

Pour obtenir la liste des objets disponibles pour votre organisation, reportez-vous à la documentation [!DNL Salesforce] [Obtenir une liste d’objets](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). Une fois que vous disposez d’une liste d’objets, consultez la section [Diagramme de relation d’entité (ERD)](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) de [!DNL Salesforce] documentation pour voir comment les entités sont liées les unes aux autres.

## Objets non pris en charge

Actuellement, [!DNL Salesforce] n’expose pas les objets suivants dans leur API :

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [Qu&#39;est-ce qu&#39;un objet externe ?](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_external_objects.htm)
* `CollaborationGroupRecord`
* `ContentDocument`
* `ContentDocumentLink`
* `FeedItem`
* `FieldDefinition`
* `IdeaComment`
* `ListViewChartInstance`
* `Order`
* `PlatformAction`

* `KnowledgeArticleVersion`
* `NewsFeed`
* `RecentlyViewed`
* `TopicAssignment`
* `UserRecordAccess`
* `UserProfileFeed`
* `Vote`

## Connexe :

* [Connexion  [!DNL Salesforce]](../integrations/salesforce.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
