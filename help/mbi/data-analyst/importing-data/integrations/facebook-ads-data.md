---
title: Données Facebook Ads attendues
description: Découvrez un bref aperçu des tableaux qu’il est recommandé de synchroniser avec votre Data Warehouse
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/LBpqIMm4nGx-Vu-zxw-iPLgNg1yfDsYi0yDyFHCyxvA
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
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 303
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
