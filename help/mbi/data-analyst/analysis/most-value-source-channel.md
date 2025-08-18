---
title: Identification des sources et des canaux marketing les plus précieux
description: Découvrez certains rapports que vous pouvez utiliser pour découvrir vos canaux marketing les plus précieux.
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 0%

---

# Identification Des Sources Marketing Réussies

Vous avez fait des recherches sur votre audience, vous avez créé votre campagne, vous avez investi dans quelques canaux marketing. Maintenant qu’un certain temps s’est écoulé, quelles sont les performances de ces canaux ? Quel canal a attiré le plus de nouveaux utilisateurs ? Quelle est la source qui a le plus contribué à votre chiffre d&#39;affaires total ?

Avec [!DNL Adobe Commerce Intelligence], vous pouvez facilement segmenter votre chiffre d’affaires et vos utilisateurs et utilisatrices par source de référence, qu’il s’agisse de champs de données [[!DNL [Google Analytics' UTM fields]]](https://support.google.com/analytics/answer/1191184?hl=en) ou personnalisés. Cette segmentation vous permet de trouver les canaux les plus performants et de mieux investir votre budget marketing.

Cette rubrique explore certains rapports que vous pouvez utiliser pour découvrir vos canaux marketing les plus précieux :

* [Nouveaux utilisateurs par sources](#newusersbysource)
* [Chiffre d’affaires moyen au cours de la durée de vie par source d’utilisateur](#avglifetimerev)
* [Valeur de commande moyenne par source d&#39;utilisateur](#avgorderval)
* [Chiffre d’affaires par date et source d’enregistrement de l’utilisateur](#revbyregdateandsource)
* [Répéter les commandes par source d&#39;utilisateur](#repeatordersbysource)

## Conditions préalables {#prereqs}

Pour créer les analyses de cette rubrique, vous devez accéder aux données sources d’acquisition/de référence marketing. Si vous ne le suivez pas déjà, vous devez importer les données de la source de référence [order referral depuis [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md) dans [!DNL Adobe Commerce Intelligence] avant de pouvoir continuer. En outre, l’ajout d’informations sur les appareils utilisateur à vos analyses vous permet de voir la technologie utilisée par vos recommandations.

## Nouveaux utilisateurs par source {#newusersbysource}

L’évaluation des performances des sources de recommandation est essentielle pour déterminer vos canaux les plus précieux. Ce rapport montre le nombre d’utilisateurs nouvellement inscrits, par source d’acquisition, au fil du temps, ce qui vous permet de suivre les performances des sources de référence dans l’acquisition de nouveaux utilisateurs inscrits.

Pour créer ce rapport dans le [Report Builder](../../tutorials/using-visual-report-builder.md), ajoutez la mesure **Nouveaux utilisateurs** (ou une mesure équivalente qui comptabilise le nombre de nouveaux utilisateurs au fil du temps) au rapport. Procédez ensuite comme suit :

1. Définissez la [!UICONTROL Time Period] sur la période d&#39;enregistrement à analyser.
1. Définissez la [!UICONTROL Interval] sur mensuelle.
1. Définissez l’[!UICONTROL Group By] sur la source d’acquisition (ou de référence) et sélectionnez les sources à inclure.
1. Cet exemple utilise le `stacked columns` [!UICONTROL chart type].

Voici une présentation visuelle :

![Création d’un rapport Nouveaux utilisateurs par source.](../../assets/New_Users_by_source.gif)

## Chiffre d’affaires moyen au cours de la durée de vie par source d’utilisateur {#avglifetimerev}

Il est important de trouver les canaux qui attirent de nouveaux utilisateurs, mais dans quelle mesure ces recommandations sont-elles utiles dans l’ensemble ? Ce rapport présente le chiffre d’affaires moyen des utilisateurs sur une durée de vie, provenant de sources d’acquisition spécifiques. En d’autres termes, cela vous permet de voir si les utilisateurs acquis d’une source particulière passent plus d’argent avec vous au cours de leur durée de vie qu’un groupe d’utilisateurs acquis d’une autre source.

Pour créer ce rapport dans Report Builder, ajoutez la mesure **Chiffre d’affaires moyen sur la durée de vie** au rapport. Procédez ensuite comme suit :

1. Définissez la [!UICONTROL Time Period] sur la période que vous souhaitez analyser.
1. Définissez la [!UICONTROL Interval] sur mensuelle.
   [!UICONTROL Group By] à la source d’acquisition (ou de référence) et sélectionnez les sources à inclure.
1. Cet exemple utilise le type `line chart` .

Voici une présentation visuelle :

![Création d’un revenu moyen sur la durée de vie par source utilisateur](../../assets/Lifetime_revenue_by_user_source.gif).

Cet exemple ne s’intéresse qu’au chiffre d’affaires cumulé, mais vous pouvez également répliquer cette analyse pour examiner le [!UICONTROL Number of orders] ou le [!UICONTROL Distinct buyers] par source de référence.

## Valeur de commande moyenne par source d&#39;utilisateur {#avgorderval}

Pour avoir une meilleure idée de l’argent dépensé par les utilisateurs d’une source d’acquisition spécifique, vous pouvez créer un rapport qui examine leur valeur moyenne de commande. Vous pouvez ainsi déterminer si les utilisateurs acquis auprès d’une source particulière dépensent plus par commande que les utilisateurs d’une autre source.

Pour créer ce rapport dans le Report Builder, ajoutez la mesure **Valeur de commande moyenne** puis procédez comme suit :

1. Définissez la [!UICONTROL Time Period] sur la période d&#39;enregistrement à analyser.
1. Définissez la [!UICONTROL Time Interval] sur mensuelle.
1. Définissez l’[!UICONTROL Group By] sur la source d’acquisition (ou de référence) et sélectionnez les sources à inclure.
1. Cet exemple utilise le type de graphique **colonnes empilées**.

Voici une présentation visuelle :

![Création d&#39;un rapport Valeur de commande moyenne par source utilisateur.](../../assets/Average_order_value_by_source.gif)

## Chiffre d’affaires total par date et source d’enregistrement des utilisateurs {#revbyregdateandsource}

L’analyse des revenus sur la durée de vie qui a été abordée précédemment vous permet d’examiner les revenus sur la durée de vie moyenne des utilisateurs acquis de différentes sources, mais qu’en est-il des revenus totaux sur la durée de vie ? Ce rapport vous permet d’identifier le montant total des revenus générés par les utilisateurs enregistrés au cours d’une période spécifique et à partir d’une source spécifique.

Pour créer ce rapport dans le Report Builder, ajoutez la mesure `Revenue by user registration date` . Si vous n’avez pas encore [créé cette mesure](../../data-user/reports/ess-manage-data-metrics.md), vous pouvez le faire en répliquant la mesure `Revenue` et en modifiant la `time stamp` sur la `creation date` de l’utilisateur. Après avoir ajouté la mesure, procédez comme suit :

1. Définissez la [!UICONTROL Time Period] sur la période d&#39;enregistrement à analyser.
1. Définissez la [!UICONTROL Time Interval] sur mensuelle.
1. Définissez l’[!UICONTROL Group By] sur la source d’acquisition (ou de référence) et sélectionnez les sources à inclure.
1. Cet exemple utilise le type de graphique `stacked columns`.

Voici une présentation visuelle :

![Création d’un rapport Chiffre d’affaires total par date d’enregistrement et source des utilisateurs.](../../assets/Revenue_by_user_registration_date_and_source.gif)

## Répéter les commandes par source d&#39;utilisateur {#repeatordersbysource}

L’état Valeur moyenne de la commande vous indique, en moyenne, combien d’utilisateurs acquis auprès d’une source particulière dépensent lors de la commande. Ce rapport ne vous indique toutefois pas si ces mêmes utilisateurs sont des clients réguliers. Mais avec les sources Commandes répétées par les utilisateurs, vous pouvez voir si les utilisateurs d&#39;une source particulière font plus ou moins d&#39;achats répétés.

Pour créer ce rapport dans le [Report Builder](../../tutorials/using-visual-report-builder.md), ajoutez la mesure **Nombre de commandes** puis procédez comme suit :

1. Définissez la [!UICONTROL Time Period] sur la période d&#39;enregistrement à analyser.
1. Définissez la [!UICONTROL Time Interval] sur mensuelle.
1. Ajoutez une [!UICONTROL filter] afin que seuls les utilisateurs avec des ordres répétés soient inclus :

   Numéro de commande de l&#39;utilisateur supérieur à 1

1. Définissez l’[!UICONTROL Group By] sur la source d’acquisition (ou de référence) et sélectionnez les sources à inclure.
1. Cet exemple utilise le type de graphique `stacked columns`.

Voici une présentation visuelle :

![Création d&#39;un rapport Répétition des ordres par origine utilisateur.](../../assets/Repeat_orders_by_user_source.gif)


## Conclusion {#wrapup}

Ce sujet n’a abordé que quelques analyses que vous pouvez utiliser pour analyser la valeur de vos canaux d’acquisition et de marketing, mais ce n’est que la partie visible de l’iceberg.

## Connexe {#related}

* [Suivi de la source de référence d’ordre via  [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)
* [Connexion  [!DNL Google Adwords]  compte](../importing-data/integrations/google-adwords.md)
* [Création [!DNL Google ECommerce] dimensions avec des commandes et des données client](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Bonnes pratiques relatives au balisage UTM dans  [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
