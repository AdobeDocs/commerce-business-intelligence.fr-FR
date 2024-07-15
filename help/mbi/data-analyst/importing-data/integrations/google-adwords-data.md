---
title: Données Google Adwords attendues
description: Découvrez comment utiliser Data Warehouse Manager pour effectuer facilement le suivi des champs de données pertinents à des fins d’analyse.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# Données [!DNL Google Adwords] attendues

Une fois [que vous avez connecté votre  [!DNL Google Adwords] compte](../integrations/google-adwords.md), vous pouvez utiliser le [Gestionnaire de Data Warehouse](../../data-warehouse-mgr/tour-dwm.md) pour facilement suivre les champs de données pertinents à des fins d’analyse.

Deux tables sont alors disponibles pour la réplication dans votre Data Warehouse :

* `campaigns[account-id]`
* `adwords[account-id]`

La `campaigns` table *doit être utilisée par défaut*. Vous pouvez donc commencer par synchroniser tous les champs pertinents de cette table.

La table `adwords` contient quatre colonnes qui ne se trouvent pas dans la table `campaigns` :

1. `keyword`
1. `adContent`
1. `adDestinationUrl`
1. `adGroup`

Lorsque vous souhaitez réaliser une analyse qui prend en compte ces attributs, vous devez utiliser la table `adwords`.

>[!IMPORTANT]
>
>Cette table exclut les lignes où les quatre colonnes sont toutes `null`.

Vous trouverez ci-dessous un aperçu du schéma attendu pour les deux tableaux.

## [!DNL Campaigns] table

La table `campaigns` contient les colonnes suivantes :

| **Colonne** | **Description** |
|-----|-----|
| `\_id` | Clé primaire de la table |
| `accountId` | ID du compte |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Nombre total de clics pour la journée |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Coût total de la campagne pour la journée |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] ID de campagne |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Nom de la campagne (par exemple, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | Date d’exécution de la campagne |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Nombre d’impressions pour la journée |
| `profileId` | Identifiant du profil |
| `profileName` | Nom du profil |
| `\_updated\_at` | Date et heure de la dernière mise à jour de cette ligne |

{style="table-layout:auto"}

## [!DNL AdWords] table

La table `adwords` contient les colonnes suivantes :

| **Colonne** | **Description** |
|-----|-----|
| `\_id` | Clé primaire de la table |
| `accountId` | ID du compte |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Nombre total de clics pour la journée |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Coût total de la campagne pour la journée |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] ID de campagne |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Nom de la campagne (par exemple, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | Date d’exécution de la campagne |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Nombre d’impressions pour la journée |
| `profileId` | Identifiant du profil |
| `profileName` | Nom du profil |
| `\_updated\_at` | Date et heure de la dernière mise à jour de cette ligne |
| `keyword` | Mot-clé de la campagne |
| `adContent` | Première ligne du texte de la campagne en ligne |
| `adDestinationUrl` | L’URL à laquelle les publicités [!DNL Adwords] ont référencé le trafic |
| `adGroup` | Nom du groupe publicitaire [!DNL Adwords] |

{style="table-layout:auto"}

Grâce à ces données, vous pouvez commencer à créer des [mesures](../../../data-user/reports/ess-manage-data-metrics.md) et des [rapports](../../../tutorials/using-visual-report-builder.md) basés sur les données de dépenses et [les associer aux recettes de votre durée de vie pour calculer le retour sur investissement](../../analysis/roi-ad-camp.md).

## Tables consolidées

[!DNL Adobe] recommande de créer une table `consolidated ad spend` pour combiner les données de toutes vos sources publicitaires multiples en une seule table. Vous pouvez ainsi utiliser un seul ensemble de mesures pour l’analyse des publicités.

Si vous ne disposez pas d’une table consolidée et que vous créez un beau tableau de bord sur la table `adwords`, vous devez répliquer la création de rapports ou créer des mesures en double pour comparer ces données à vos données [!DNL Facebook Ads]. L&#39;utilisation d&#39;une table consolidée vous permet d&#39;incorporer aisément des données [!DNL Facebook Ads] à vos rapports [!DNL Adwords] existants. Vous pouvez également segmenter par plateforme publicitaire.

Si vous avez déjà synchronisé les champs ci-dessus, [contactez-nous](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) pour consolider vos dépenses publicitaires.
