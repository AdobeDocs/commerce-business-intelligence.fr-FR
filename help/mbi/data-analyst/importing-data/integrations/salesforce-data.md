---
title: Données Salesforce attendues
description: Découvrez les objets pris en charge et non pris en charge dans les données Salesforce.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Valeur attendue [!DNL Salesforce] data

[Après la [!DNL Salesforce] la configuration est terminée](../integrations/salesforce.md), un tableau pour chaque table de requête [objet](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_concepts.htm) - named `sf_/\{sobject-name}` - sera créé dans votre entrepôt de données.

>[!NOTE]
>
>La structure (colonnes) de chaque tableau dépend des champs contenus dans l’objet.

Pour obtenir une liste des objets mis à la disposition de votre entreprise, reportez-vous à la section [!DNL Salesforce] [Obtention d’une documentation de liste d’objets](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). Une fois que vous disposez d’une liste d’objets, extrayez le [Diagramme de relation d’entité (ERD)](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) de [!DNL Salesforce] documentation pour découvrir comment les entités se connectent entre elles.

## Objets non pris en charge

À l’heure actuelle, [!DNL Salesforce] n’expose actuellement pas les objets suivants dans leur API :

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [Qu’est-ce qu’un objet externe ?](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_external_objects.htm)
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

## En rapport :

* [Connexion [!DNL Salesforce]](../integrations/salesforce.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
