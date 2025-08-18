---
title: Données Google Adwords attendues
description: Découvrez comment utiliser Data Warehouse Manager pour effectuer facilement le suivi des champs de données pertinents à analyser.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# Données de [!DNL Google Adwords] attendues

Une fois [vous avez connecté votre [!DNL Google Adwords] compte](../integrations/google-adwords.md), vous pouvez utiliser le [Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md) pour effectuer facilement le suivi des champs de données pertinents à analyser.

Vous remarquerez que deux tables sont disponibles pour la réplication dans votre Data Warehouse :

* `campaigns[account-id]`
* `adwords[account-id]`

Le tableau `campaigns` *doit être utilisé par défaut* afin que vous puissiez commencer par synchroniser tous les champs pertinents de ce tableau.

Le tableau `adwords` contient quatre colonnes qui ne figurent pas dans le tableau `campaigns` :

1. `keyword`
1. `adContent`
1. `adDestinationUrl`
1. `adGroup`

Lorsque vous souhaitez effectuer une analyse qui prend en compte ces attributs, vous devez utiliser le tableau `adwords`.

>[!IMPORTANT]
>
>Ce tableau exclut les lignes où les quatre colonnes sont `null`.

Vous trouverez ci-dessous un aperçu du schéma attendu pour les deux tables.

## [!DNL Campaigns] table

Le tableau `campaigns` contient les colonnes suivantes :

| **Colonne** | **Description** |
|-----|-----|
| `\_id` | Clé primaire de la table |
| `accountId` | L’identifiant de compte |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adclicks) | Nombre total de clics sur la journée |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adcost) | Coût total de la campagne pour la journée |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adwordscampaignid) | ID de campagne [!DNL Adwords] |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=traffic_sources&jump=ga_campaign) | Nom de la campagne (par exemple, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=time&jump=ga_date) | Date d’exécution de la campagne |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_impressions) | Nombre d’impressions par jour |
| `profileId` | L’identifiant de profil |
| `profileName` | Nom du profil |
| `\_updated\_at` | Date et heure de la dernière mise à jour pour cette ligne |

{style="table-layout:auto"}

## [!DNL AdWords] table

Le tableau `adwords` contient les colonnes suivantes :

| **Colonne** | **Description** |
|-----|-----|
| `\_id` | Clé primaire de la table |
| `accountId` | L’identifiant de compte |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adclicks) | Nombre total de clics sur la journée |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adcost) | Coût total de la campagne pour la journée |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adwordscampaignid) | ID de campagne [!DNL Adwords] |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=traffic_sources&jump=ga_campaign) | Nom de la campagne (par exemple, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=time&jump=ga_date) | Date d’exécution de la campagne |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_impressions) | Nombre d’impressions par jour |
| `profileId` | L’identifiant de profil |
| `profileName` | Nom du profil |
| `\_updated\_at` | Date et heure de la dernière mise à jour pour cette ligne |
| `keyword` | Le mot clé de la campagne |
| `adContent` | Première ligne du texte de la campagne en ligne |
| `adDestinationUrl` | URL à laquelle les publicités [!DNL Adwords] ont fait référence pour le trafic |
| `adGroup` | Nom du groupe publicitaire [!DNL Adwords] |

{style="table-layout:auto"}

Grâce à ces données, vous pouvez commencer à créer des [mesures](../../../data-user/reports/ess-manage-data-metrics.md) et des [rapports](../../../tutorials/using-visual-report-builder.md) basés sur les données de dépenses et les [associer au chiffre d’affaires de votre durée de vie pour calculer le retour sur investissement](../../analysis/roi-ad-camp.md).

## Tables consolidées

[!DNL Adobe] recommande de créer un tableau `consolidated ad spend` pour combiner les données de toutes vos sources publicitaires multiples en un seul tableau. Vous pouvez ainsi utiliser un seul ensemble de mesures pour l’analyse de la publicité.

Si vous ne disposez pas d’une table consolidée et que vous créez un beau tableau de bord sur la table `adwords`, vous devez répliquer les rapports ou créer des mesures en double pour comparer ces données à vos données [!DNL Facebook Ads]. L’utilisation d’un tableau consolidé vous permet d’incorporer facilement des données [!DNL Facebook Ads] à vos rapports [!DNL Adwords] existants. Vous pouvez également segmenter par plateforme publicitaire.

Si vous avez déjà synchronisé les champs ci-dessus, [contactez-nous](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) pour consolider vos dépenses publicitaires.
