---
title: Données Google Adwords attendues
description: Découvrez comment utiliser Data Warehouse Manager pour effectuer facilement le suivi des champs de données pertinents à des fins d’analyse.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# Valeur attendue [!DNL Google Adwords] data

Après [vous avez connecté votre [!DNL Google Adwords] account](../integrations/google-adwords.md), vous pouvez utiliser la variable [Gestionnaire de Data Warehouse](../../data-warehouse-mgr/tour-dwm.md) pour effectuer facilement le suivi des champs de données pertinents à des fins d’analyse.

Deux tables sont alors disponibles pour la réplication dans votre Data Warehouse :

* `campaigns[account-id]`
* `adwords[account-id]`

La variable `campaigns` table *doit être utilisé par défaut.*, afin que vous puissiez commencer par synchroniser tous les champs pertinents de ce tableau.

La variable `adwords` Le tableau contient quatre colonnes qui ne se trouvent pas dans la variable `campaigns` table :

1. `keyword`
1. `adContent`
1. `adDestinationUrl`
1. `adGroup`

Lorsque vous souhaitez réaliser une analyse qui prend en compte ces attributs, vous devez utiliser la variable `adwords` table.

>[!IMPORTANT]
>
>Ce tableau exclut les lignes où les quatre colonnes sont `null`.

Vous trouverez ci-dessous un aperçu du schéma attendu pour les deux tableaux.

## [!DNL Campaigns] table

La variable `campaigns` Le tableau contient les colonnes suivantes :

| **Colonne** | **Description** |
|-----|-----|
| `\_id` | Clé primaire de la table |
| `accountId` | ID du compte |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Nombre total de clics pour la journée |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Coût total de la campagne pour la journée |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] Identifiant de campagne |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Nom de la campagne (par exemple, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | Date d’exécution de la campagne |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Nombre d’impressions pour la journée |
| `profileId` | Identifiant du profil |
| `profileName` | Nom du profil |
| `\_updated\_at` | Date et heure de la dernière mise à jour de cette ligne |

{style="table-layout:auto"}

## [!DNL AdWords] table

La variable `adwords` Le tableau contient les colonnes suivantes :

| **Colonne** | **Description** |
|-----|-----|
| `\_id` | Clé primaire de la table |
| `accountId` | ID du compte |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Nombre total de clics pour la journée |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Coût total de la campagne pour la journée |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] Identifiant de campagne |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Nom de la campagne (par exemple, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | Date d’exécution de la campagne |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Nombre d’impressions pour la journée |
| `profileId` | Identifiant du profil |
| `profileName` | Nom du profil |
| `\_updated\_at` | Date et heure de la dernière mise à jour de cette ligne |
| `keyword` | Mot-clé de la campagne |
| `adContent` | Première ligne du texte de la campagne en ligne |
| `adDestinationUrl` | L’URL à laquelle la variable [!DNL Adwords] trafic référencé des publicités |
| `adGroup` | Nom de la variable [!DNL Adwords] groupe publicitaire |

{style="table-layout:auto"}

A partir de ces données, vous pouvez commencer à créer [mesures](../../../data-user/reports/ess-manage-data-metrics.md) et [rapports](../../../tutorials/using-visual-report-builder.md) en fonction des dépenses et [l’épouser aux recettes de votre vie pour calculer le retour sur investissement](../../analysis/roi-ad-camp.md).

## Tables consolidées

[!DNL Adobe] recommande de créer une `consolidated ad spend` pour combiner les données de toutes vos sources publicitaires multiples en un seul tableau. Vous pouvez ainsi utiliser un seul ensemble de mesures pour l’analyse des publicités.

Si vous ne disposez pas d’une table consolidée et que vous créez un beau tableau de bord sur la page `adwords` tableau, vous devez répliquer le rapport ou créer des mesures en double pour comparer ces données à votre [!DNL Facebook Ads] data. L’utilisation d’un tableau consolidé vous permet d’incorporer facilement des [!DNL Facebook Ads] avec vos données existantes [!DNL Adwords] rapports. Vous pouvez également segmenter par plateforme publicitaire.

Si vous avez déjà synchronisé les champs ci-dessus, [contactez-nous](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) pour consolider vos dépenses publicitaires.
