---
title: Données Facebook Ads attendues
description: Découvrez un bref aperçu des tables dont la synchronisation avec votre Data Warehouse est recommandée.
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Valeur attendue [!DNL Facebook Ads] data

Après avoir [connecté à [!DNL Facebook Ads] account](../integrations/facebook-ads.md), vous pouvez utiliser la variable [Gestionnaire de Data Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) pour effectuer facilement le suivi des champs de données pertinents à des fins d’analyse.

Cette rubrique présente un bref aperçu des tables que Adobe vous recommande de synchroniser avec votre Data Warehouse. Cela ne fait que mettre en surbrillance les tables principales, car il existe plusieurs sous-tables.

## Tables de campagnes publicitaires principales

Ces tableaux contiennent des données sur les composants de campagne publicitaire principaux.

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

Ce tableau est le tableau principal des campagnes d’une [!DNL Facebook Ads] compte . Les colonnes incluent `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

Cet enregistrement de tableau est le tableau principal de [!DNL Facebook Ads] Définit dans un [!DNL Facebook Ads] compte . Les colonnes comprennent la publicité `Campaign id/name` le jeu d’annonces auquel appartient, le budget, le type d’offre, la planification et les informations de ciblage d’audience.

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

Ce tableau enregistre toutes les publicités d’une [!DNL Facebook Ads] compte . Les colonnes comprennent les informations sur la publicité, notamment la visionneuse de publicités et la campagne publicitaire auxquelles elle appartient, l’offre publicitaire, le ciblage publicitaire et la référence à un élément créatif spécifique (image/texte) utilisé par la publicité.

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

Ce tableau enregistre les créations utilisées dans [!DNL Facebook Ads]. Les créatifs incluent le nom, la description et les URL d’image pertinentes, le cas échéant.

## Tableaux d’opération segmentés

Les tableaux suivants contiennent une entrée pour chaque combinaison campagne/jeu/publicité pour chaque jour, segmentée par des dimensions telles que l’âge, le sexe et le pays.

### `facebook _ads insights_ (account-id)`

Ce tableau comprend une entrée pour chaque combinaison campagne/jeu/publicité pour chaque jour, ainsi que des statistiques incluant les impressions, les clics, le coût, le CPC, le cpm, le ctr, la portée, la portée sociale et les dépenses.

### `facebook _ads insights_ (account-id)_~\_actions`

Il s’agit d’un sous-tableau de la variable `facebook_ads_insights_{account_id}` table. Elle inclut des données de conversion pour les actions qui se produisent en fonction de différentes campagnes.

### `facebook _ads insights country_ (account-id)`

Ce tableau contient les mêmes informations que la variable `facebook_ads_insights_{account_id}` et les segmente par pays.

### `facebook ads insights age and gender (account-id)`

Ce tableau contient les mêmes informations que la variable `facebook_ads_insights_{account_id}` et les segmente par âge et par sexe.

## Associé

* [Connexion [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
