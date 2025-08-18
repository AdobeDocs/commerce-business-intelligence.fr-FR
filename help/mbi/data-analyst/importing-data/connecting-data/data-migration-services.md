---
title: Services de migration des données
description: Découvrez tout ce dont vous avez besoin pour soumettre une demande et commencer la migration.
exl-id: 105cd003-98ef-4358-80b9-b3190c2c57b7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# Migration des données

La migration vers un nouveau schéma de base de données, un nouveau serveur ou une nouvelle base de données de rapports ne doit pas nécessairement être stressante. L’[[!DNL Adobe] équipe Services](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) offre une assistance en matière de migration.

Pour garantir une transition aussi fluide que possible, veillez à fournir les informations les plus détaillées possible lors de l’envoi de votre demande de migration. Cette rubrique contient tout ce dont vous avez besoin pour envoyer une demande et commencer la migration. En nous fournissant une image complète de vos besoins, nous vous garantissons que votre projet est correctement défini et que l&#39;estimation est exacte.

## Prise en main {#started}

Avant de commencer, vous devez connaître les réponses à ces questions :

* **La nouvelle base de données est-elle sur un nouveau serveur ?** Avant d’envoyer une requête, mettez à jour les paramètres de votre connexion de données sous **[!UICONTROL Manage Data** > **Connections]**. Si vous avez besoin d’un rappel sur la façon de procéder, accédez à la section [`Integrations`](../integrations/integrations.md) et recherchez les instructions relatives au type de base de données que vous utilisez.

* **Toutes vos données historiques existent-elles dans la nouvelle base de données ou doivent-elles être migrées ?** Vous pouvez consolider les données historiques et nouvelles pendant le processus de migration. Même si vous n&#39;avez pas besoin d&#39;une consolidation, faites-le nous savoir dans votre demande.

Une fois que vous disposez des réponses à la question précédente, vous devez connaître le type de migration. La nouvelle base de données aura-t-elle le schéma [`same`](#sameschema) ou aura-t-elle un schéma [`different`](#newschema) ? Vous trouverez ci-dessous des instructions détaillées pour chaque type de migration.

## Migration vers une nouvelle base de données avec le même schéma {#sameschema}

Lors de l’envoi de la requête, signalons que le schéma de base de données ne change pas et que la connexion est déjà configurée dans [!DNL Adobe Commerce Intelligence].

Si la base de données porte un nouveau nom, incluez-le dans la requête afin que vos tableaux de bord puissent être correctement migrés.

Si le nom de la base de données ne change pas, la migration est terminée. Les tableaux de bord et les rapports seront actualisés une fois la prochaine mise à jour complète terminée.

## Migration vers une nouvelle base de données avec un schéma différent {#newschema}

>[!IMPORTANT]
>
>Si certaines colonnes de données n’ont pas de colonnes équivalentes dans la nouvelle base de données, il est possible que certaines analyses soient perdues dans le processus.

Pour réussir ce type de migration, les colonnes de données existantes doivent être mises en correspondance avec leurs équivalents dans la nouvelle base de données. Cela n’est pas obligatoire, mais l’exécution de la correspondance pour nous permet d’accélérer le délai d’exécution de votre demande et de réduire le prix de la migration.

Si vous vous sentez à l’aise pour faire la correspondance vous-même, suivez ces instructions et joignez la feuille de calcul terminée à votre demande :

1. Passez en revue tous les tableaux et colonnes en cours de synchronisation avec votre Data Warehouse (**[!UICONTROL Manage Data** > **Data Warehouse]**).

1. Dans une feuille de calcul, créez un onglet pour chaque table à migrer vers la nouvelle base de données.

1. Dans chaque onglet, créez une colonne pour toutes les colonnes existantes qui doivent être migrées. Adobe recommande de lui donner un nom du type `Existing column name`.

1. Vous devez également créer une autre colonne pour les équivalents de colonne dans la nouvelle base de données dans chaque onglet de la feuille de calcul. Adobe recommande d’attribuer un nom de type `New column name` à la colonne.

1. Renseignez les colonnes existantes et leurs équivalents. Si une colonne existante n’a pas de nouvel équivalent, saisissez `N/A`.

   En outre, s&#39;il existe une nouvelle façon de calculer les mêmes informations dans la nouvelle base de données, saisissez-les dans la colonne [`New column name`].

Voici un aperçu d’un exemple :

![](../../../assets/Migration_Spreadsheet.png)

>[!NOTE]
>
>Si certaines colonnes de données n’ont pas de colonnes équivalentes dans la nouvelle base de données, il est possible que certaines analyses soient perdues dans le processus.

## Comment soumettre une demande ? {#submitreq}

Vous pouvez nous contacter en [soumettant une demande d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

Si vous avez suivi les étapes de la section précédente pour créer la feuille de calcul correspondant aux colonnes, n’oubliez pas de la joindre.

## Quelle est la prochaine étape ? {#wrapup}

Pour déterminer la portée du projet, vous devez collaborer avec l’analyste de l’équipe des services Commerce chargée de la migration. La complexité des modifications et la réactivité de vous et de l’analyste ont une incidence directe sur le temps nécessaire à la migration. Une fois que vous aurez établi les détails, un calendrier sera établi et vous sera envoyé avec un énoncé de travail.
