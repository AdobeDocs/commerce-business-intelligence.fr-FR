---
title: Données Facebook Ads attendues
description: Découvrez un bref aperçu des tables dont la synchronisation avec votre Data Warehouse est recommandée.
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Données [!DNL Facebook Ads] attendues

Une fois que vous avez [connecté à votre  [!DNL Facebook Ads] compte](../integrations/facebook-ads.md), vous pouvez utiliser le [Gestionnaire de Data Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) pour facilement suivre les champs de données pertinents à des fins d’analyse.

Cette rubrique présente un bref aperçu des tables que Adobe vous recommande de synchroniser avec votre Data Warehouse. Cela ne fait que mettre en surbrillance les tables principales, car il existe plusieurs sous-tables.

## Tables de campagnes publicitaires principales

Ces tableaux contiennent des données sur les composants de campagne publicitaire principaux.

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

Cette table est la table principale des campagnes dans un compte [!DNL Facebook Ads]. Les colonnes comprennent `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

Cet enregistrement de table est la table principale des [!DNL Facebook Ads] Visionneuses dans un compte [!DNL Facebook Ads]. Les colonnes comprennent la publicité `Campaign id/name` à laquelle appartient la visionneuse d’annonces, le budget, le type d’offre, la planification et les informations de ciblage d’audience.

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

Cette table enregistre toutes les publicités dans un compte [!DNL Facebook Ads]. Les colonnes comprennent les informations sur la publicité, notamment la visionneuse de publicités et la campagne publicitaire auxquelles elle appartient, l’offre publicitaire, le ciblage publicitaire et la référence à un élément créatif spécifique (image/texte) utilisé par la publicité.

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

Cette table enregistre les créations utilisées dans [!DNL Facebook Ads]. Les créatifs incluent le nom, la description et les URL d’image pertinentes, le cas échéant.

## Tableaux d’opération segmentés

Les tableaux suivants contiennent une entrée pour chaque combinaison campagne/jeu/publicité pour chaque jour, segmentée par des dimensions telles que l’âge, le sexe et le pays.

### `facebook _ads insights_ (account-id)`

Ce tableau comprend une entrée pour chaque combinaison campagne/jeu/publicité pour chaque jour, ainsi que des statistiques incluant les impressions, les clics, le coût, le CPC, le cpm, le ctr, la portée, la portée sociale et les dépenses.

### `facebook _ads insights_ (account-id)_~\_actions`

Il s’agit d’une sous-table de la table `facebook_ads_insights_{account_id}`. Elle inclut des données de conversion pour les actions qui se produisent en fonction de différentes campagnes.

### `facebook _ads insights country_ (account-id)`

Ce tableau contient les mêmes informations que la table `facebook_ads_insights_{account_id}` et les segmente par pays.

### `facebook ads insights age and gender (account-id)`

Ce tableau contient les mêmes informations que la table `facebook_ads_insights_{account_id}` et les segmente par âge et par sexe.

## Associé

* [Connexion [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=fr)
