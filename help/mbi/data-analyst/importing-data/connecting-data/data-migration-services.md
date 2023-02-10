---
title: Services de migration de données
description: Découvrez tout ce dont vous avez besoin pour envoyer une requête et commencer la migration.
exl-id: 105cd003-98ef-4358-80b9-b3190c2c57b7
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# Migration des données

La migration vers une nouvelle base de données, un nouveau serveur ou une nouvelle base de données de rapports n’a pas à être stressante. Notre **[!DNL Adobe Commerce Services - Analytics]** l’équipe d’ offre de l’aide en matière de migration - nous faisons tout le travail nécessaire pour que vous n’ayez pas à le faire.

Pour garantir une transition aussi fluide que possible, nous vous demandons d’être aussi détaillé que possible lors de l’envoi de votre demande de migration. Dans cet article, vous trouverez tout ce dont vous avez besoin pour envoyer une demande et commencer la migration. Nous fournir une image complète de vos besoins vous garantira que votre projet est correctement ciblé et que l’estimation est exacte.

## Prise en main {#started}

Avant de plonger, vous devez connaître les réponses à ces questions :

* **La nouvelle base de données est-elle sur un nouveau serveur ?** Avant d’envoyer une requête, mettez à jour les paramètres de votre connexion aux données sous **[!UICONTROL Manage Data** > **Connections]**. Si vous avez besoin d’une actualisation sur la manière de procéder, accédez à la [`Integrations`](../integrations/integrations.md) et recherchez les instructions relatives au type de base de données que vous utilisez.
* **Toutes vos données historiques existent-elles dans la nouvelle base de données ou doivent-elles être migrées ?** Nous pouvons consolider les données historiques et nouvelles pendant le processus de migration. Même si vous n&#39;avez pas besoin d&#39;une consolidation, nous vous invitons à nous le faire savoir dans votre demande.

Une fois que vous aurez reçu les réponses ci-dessus, nous devrons connaître le type de migration : la nouvelle base de données contiendra-t-elle la variable [`same`](#sameschema) ou aura-t-il un [`different`](#newschema) schéma ? Les sections ci-dessous contiennent des instructions détaillées sur chaque type de migration.

## Migration vers une nouvelle base de données avec le même schéma {#sameschema}

Lors de l’envoi de la demande, informez-nous que le schéma de la base de données n’a pas changé et que la connexion est déjà configurée dans [!DNL MBI].

Si la base de données porte un nouveau nom, incluez-le dans la requête afin que vos tableaux de bord puissent être migrés correctement.

Si le nom de la base de données n’est pas modifié, la migration est terminée. Les tableaux de bord et les rapports s’actualisent une fois la prochaine mise à jour complète terminée. Nous vous demandons de toujours nous contacter afin que nous puissions anticiper tous les problèmes qui pourraient résulter de la migration.

## Migration vers une nouvelle base de données avec un schéma différent {#newschema}

>[!IMPORTANT]
>
>Si certaines colonnes de données ne comportent pas de colonnes équivalentes dans la nouvelle base de données, il est possible que certaines analyses soient perdues dans le processus.

Pour réussir ce type de migration, les colonnes de données existantes doivent correspondre avec leurs équivalents dans la nouvelle base de données. Cela n’est pas obligatoire pour vous, mais l’exécution de la correspondance pour nous permettra d’accélérer le temps de traitement de votre demande et de réduire le prix de la migration.

Si vous vous sentez à l’aise d’effectuer la correspondance, suivez ces instructions et joignez la feuille de calcul finalisée à votre demande :

1. Examinez tous les tableaux et colonnes actuellement synchronisés avec votre Data Warehouse (**[!UICONTROL Manage Data** > **Data Warehouse]**).
1. Dans une feuille de calcul, créez un onglet pour chaque tableau à migrer vers la nouvelle base de données.
1. Dans chaque onglet, créez une colonne pour toutes les colonnes existantes qui doivent être migrées. Nous vous recommandons de lui donner un nom du type `Existing column name`.
1. Vous devez également créer une autre colonne pour les équivalents de colonne dans la nouvelle base de données dans chaque onglet de la feuille de calcul. Nous vous recommandons de nommer la colonne de la manière suivante : `New column name`.
1. Renseignez les colonnes existantes et leurs équivalents. Si une colonne existante n’a pas de nouvel équivalent, il vous suffit de saisir `N/A`.

   De plus, s’il existe une nouvelle façon de calculer les mêmes informations dans la nouvelle base de données, saisissez-les dans la variable [`New column name`] colonne .

Voici un exemple :

![](../../../assets/Migration_Spreadsheet.png)

>[!NOTE]
>
>Si certaines colonnes de données ne comportent pas de colonnes équivalentes dans la nouvelle base de données, il est possible que certaines analyses soient perdues dans le processus.

## Comment envoyer une demande ? {#submitreq}

Vous pouvez nous contacter par vous-même [envoi d’une demande d’assistance ;](../../../guide-overview.md).

Si vous avez suivi les étapes de la section précédente pour créer la feuille de calcul correspondant aux colonnes, n’oubliez pas de la joindre.

## Quelle sera la suite ? {#wrapup}

Pour déterminer la portée du projet, vous devez collaborer avec l’analyste de l’équipe Commerce Services qui effectue la migration. La complexité des modifications et la réactivité de vous-même et de l’analyste influent directement sur le temps nécessaire à la migration. Une fois que nous aurons dévoilé les détails, une chronologie sera établie et vous sera envoyée avec une déclaration de travail.
