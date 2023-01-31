---
title: Données Facebook Ads attendues
description: Découvrez un bref aperçu des tables que nous vous recommandons de synchroniser avec votre entrepôt de données
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# Valeur attendue [!DNL Facebook Ads] data

![](../../../assets/Facebook_Logo.png)

Après avoir [connecté à [!DNL Facebook Ads] account](../integrations/facebook-ads.md), vous pouvez utiliser la variable [Gestionnaire de Data Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) pour effectuer facilement le suivi des champs de données pertinents à des fins d’analyse.

Dans cet article, nous vous donnons un bref aperçu des tables que nous vous recommandons de synchroniser avec votre entrepôt de données. Il ne s’agit pas d’une liste complète, car il existe plusieurs sous-tables. Nous ne faisons que mettre en surbrillance les tableaux principaux.

## Tables de campagnes publicitaires principales

Ces tableaux contiennent des données sur les composants de campagne publicitaire principaux.

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adcampaign/)

Ce tableau est le tableau principal des campagnes d’une [!DNL Facebook Ads] compte . Les colonnes incluent `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

Cet enregistrement de table est la table principale de [!DNL Facebook Ads] Définit dans un [!DNL Facebook Ads] compte . Les colonnes comprennent la publicité `Campaign id/name` le jeu d’annonces auquel appartient, les informations de budget, de type d’offre, de planification et de ciblage des audiences.

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adgroup/)

Ce tableau enregistre toutes les publicités d’une [!DNL Facebook Ads] compte . Les colonnes comprennent les informations sur la publicité, y compris la visionneuse de publicités et la campagne publicitaire à laquelle elle appartient, l’enchère publicitaire, le ciblage publicitaire et la référence à un élément créatif spécifique (image/texte) utilisé par la publicité.

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adcreative/)

Ce tableau enregistre tous les éléments créatifs utilisés dans [!DNL Facebook Ads]. Cela inclut le nom créatif, la description et les URL d’image appropriées, le cas échéant.

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
* [Réauthentification des intégrations](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)
