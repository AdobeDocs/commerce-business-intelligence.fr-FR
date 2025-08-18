---
title: Données Facebook Ads attendues
description: Découvrez un bref aperçu des tableaux qu’il est recommandé de synchroniser avec votre Data Warehouse
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Données de [!DNL Facebook Ads] attendues

Après avoir [connecté votre [!DNL Facebook Ads] compte](../integrations/facebook-ads.md), vous pouvez utiliser [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) pour effectuer facilement le suivi des champs de données pertinents à analyser.

Cette rubrique donne un bref aperçu des tableaux qu’Adobe vous recommande de synchroniser avec votre Data Warehouse. Cela ne fait que mettre en évidence les tableaux principaux, car il existe un certain nombre de sous-tableaux.

## Tables de campagnes publicitaires principales

Ces tableaux contiennent des données sur les composants principaux des campagnes publicitaires.

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

Cette table est la table principale des campagnes d’un compte [!DNL Facebook Ads]. Les colonnes comprennent `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

Cet enregistrement de table est la table principale des ensembles de [!DNL Facebook Ads] dans un compte [!DNL Facebook Ads]. Les colonnes incluent le `Campaign id/name` de l’annonce auquel appartient le jeu d’annonces, l’établissement du budget, le type d’enchère, la planification et les informations de ciblage de l’audience.

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

Ce tableau enregistre toutes les publicités dans un compte [!DNL Facebook Ads]. Les colonnes incluent les informations sur l’annonce, y compris le jeu d’annonces et la campagne publicitaire auxquels elle appartient, les enchères et le ciblage de l’annonce, ainsi qu’une référence à des contenus publicitaires spécifiques (image/texte) que l’annonce utilise.

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

Ce tableau enregistre les contenus publicitaires utilisés dans [!DNL Facebook Ads]. Les contenus publicitaires comprennent le nom, la description et les URL d’image appropriées du contenu publicitaire.

## Tables de campagne segmentées

Les tableaux suivants contiennent une entrée pour chaque combinaison campagne/ensemble/publicité pour chaque jour, segmentée par dimensions telles que l’âge, le sexe et le pays.

### `facebook _ads insights_ (account-id)`

Ce tableau comprend une entrée pour chaque combinaison campagne/ensemble/publicité pour chaque jour, ainsi que des statistiques comprenant les impressions, les clics, le coût, cpc, cpm, cpp, ctr, la portée, la portée sociale et les dépenses.

### `facebook _ads insights_ (account-id)_~\_actions`

Il s&#39;agit d&#39;un sous-tableau de la table `facebook_ads_insights_{account_id}`. Il inclut des données de conversion pour les actions qui se produisent en fonction de différentes campagnes.

### `facebook _ads insights country_ (account-id)`

Ce tableau contient les mêmes informations que le tableau `facebook_ads_insights_{account_id}` et les segmente par pays.

### `facebook ads insights age and gender (account-id)`

Ce tableau contient les mêmes informations que le tableau `facebook_ads_insights_{account_id}` et les segmente par âge et par sexe.

## Connexe

* [Connexion  [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=fr)
