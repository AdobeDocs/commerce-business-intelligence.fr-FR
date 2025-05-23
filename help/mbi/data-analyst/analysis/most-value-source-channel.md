---
title: Identification de vos sources marketing et canaux les plus utiles
description: Découvrez certains rapports que vous pouvez utiliser pour découvrir vos canaux marketing les plus précieux.
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 0%

---

# Identification des sources marketing réussies

Vous avez fait des recherches sur votre audience, créé votre campagne, investi dans quelques canaux marketing. Maintenant que le temps est écoulé, comment ces canaux fonctionnent-ils ? Quel canal a attiré les nouveaux utilisateurs ? Quelle source a le plus contribué à vos recettes totales ?

Avec [!DNL Adobe Commerce Intelligence], vous pouvez facilement segmenter vos recettes et vos utilisateurs par source de référence, qu’ils correspondent à [[!DNL [Google Analytics' UTM fields]]](https://support.google.com/analytics/answer/1191184?hl=en) ou à des champs de données personnalisés. Cette segmentation vous permet de trouver les canaux les plus performants et d’investir davantage votre budget marketing.

Cette rubrique explore certains rapports que vous pouvez utiliser pour découvrir vos canaux marketing les plus précieux :

* [Nouveaux utilisateurs par sources](#newusersbysource)
* [Chiffre d’affaires moyen de la durée de vie par source d’utilisateur](#avglifetimerev)
* [Valeur de commande moyenne par source d’utilisateur](#avgorderval)
* [Recettes par date d’enregistrement des utilisateurs et par sources](#revbyregdateandsource)
* [Répétition des commandes par source d’utilisateur](#repeatordersbysource)

## Conditions préalables {#prereqs}

Pour générer les analyses dans cette rubrique, vous devez accéder aux données de source d’acquisition/de référence marketing. Si vous ne le suivez pas déjà, vous devez importer [les données de source de référence de commande de [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md) vers [!DNL Adobe Commerce Intelligence] avant de pouvoir continuer. En outre, l’ajout d’informations sur les appareils utilisateur à vos analyses vous permet de voir la technologie que vos référents utilisent.

## Nouveaux utilisateurs par source {#newusersbysource}

L’évaluation du rendement des sources d’orientation est essentielle pour déterminer vos canaux les plus précieux. Ce rapport présente le nombre d’utilisateurs nouvellement enregistrés, par source d’acquisition, au fil du temps, ce qui vous permet de suivre les performances des sources de référence dans l’acquisition de nouveaux utilisateurs enregistrés.

Pour créer ce rapport dans le [Report Builder](../../tutorials/using-visual-report-builder.md), ajoutez la mesure **Nouveaux utilisateurs** (ou une mesure équivalente qui comptabilise le nombre de nouveaux utilisateurs au fil du temps) au rapport. Procédez ensuite comme suit :

1. Définissez le [!UICONTROL Time Period] sur la période d’enregistrement que vous souhaitez analyser.
1. Définissez le [!UICONTROL Interval] sur mensuel.
1. Définissez [!UICONTROL Group By] sur la source d’acquisition (ou de référence) et sélectionnez les sources que vous souhaitez inclure.
1. Cet exemple utilise le `stacked columns` [!UICONTROL chart type].

Voici une présentation visuelle :

![Création d&#39;un nouvel utilisateur par rapport source.](../../assets/New_Users_by_source.gif)

## Chiffre d’affaires moyen de la durée de vie par source d’utilisateur {#avglifetimerev}

Il est important de trouver les canaux qui attirent de nouveaux utilisateurs, mais quelle est la valeur globale de ces renvois ? Ce rapport présente les recettes de durée de vie moyenne des utilisateurs provenant de sources d’acquisition spécifiques au fil du temps. En d’autres termes, cela vous permet de voir si les utilisateurs acquis par une source particulière dépensent plus avec vous au cours de leur vie qu’un groupe d’utilisateurs acquis par une autre source.

Pour créer ce rapport dans le Report Builder, ajoutez la mesure **Chiffre d’affaires moyen de la durée de vie** au rapport. Procédez ensuite comme suit :

1. Définissez le [!UICONTROL Time Period] sur la période que vous souhaitez analyser.
1. Définissez le [!UICONTROL Interval] sur mensuel.
   [!UICONTROL Group By] à la source d’acquisition (ou de référence) et sélectionnez les sources à inclure.
1. Cet exemple utilise le type `line chart` .

Voici une présentation visuelle :

![Création d’une durée de vie moyenne par source d’utilisateur](../../assets/Lifetime_revenue_by_user_source.gif).

Cet exemple ne tient compte que des recettes sur la durée de vie, mais vous pouvez également répliquer cette analyse pour examiner les [!UICONTROL Number of orders] ou [!UICONTROL Distinct buyers] par source de référence.

## Valeur de commande moyenne par source d’utilisateur {#avgorderval}

Pour mieux comprendre le montant d’argent dépensé par les utilisateurs d’une source d’acquisition spécifique, vous pouvez créer un rapport qui examine la valeur de leur commande moyenne. Cela vous permet de déterminer si les utilisateurs acquis à partir d’une source particulière dépensent plus par commande que les utilisateurs provenant d’une autre source.

Pour créer ce rapport dans le Report Builder, ajoutez la mesure **Valeur de commande moyenne** , puis procédez comme suit :

1. Définissez le [!UICONTROL Time Period] sur la période d’enregistrement que vous souhaitez analyser.
1. Définissez le [!UICONTROL Time Interval] sur mensuel.
1. Définissez [!UICONTROL Group By] sur la source d’acquisition (ou de référence) et sélectionnez les sources que vous souhaitez inclure.
1. Cet exemple utilise le type de graphique **colonnes empilées** .

Voici une présentation visuelle :

![Création d’une valeur de commande moyenne par rapport à la source de l’utilisateur.](../../assets/Average_order_value_by_source.gif)

## Chiffre d’affaires total par date d’enregistrement de l’utilisateur et source {#revbyregdateandsource}

L’analyse des recettes sur la durée de vie qui a été traitée précédemment vous permet de consulter les recettes sur la durée de vie moyenne des utilisateurs provenant de sources différentes, mais qu’en est-il des recettes totales sur la durée de vie ? Ce rapport vous permet d’identifier le montant global des recettes générées par les utilisateurs enregistrés au cours d’une période et d’une source spécifiques.

Pour créer ce rapport dans le Report Builder, ajoutez la mesure `Revenue by user registration date`. Si vous n’avez pas [déjà créé cette mesure](../../data-user/reports/ess-manage-data-metrics.md), vous pouvez le faire en répliquant la mesure `Revenue` et en modifiant la `time stamp` en `creation date` de l’utilisateur. Après avoir ajouté la mesure, procédez comme suit :

1. Définissez le [!UICONTROL Time Period] sur la période d’enregistrement que vous souhaitez analyser.
1. Définissez le [!UICONTROL Time Interval] sur mensuel.
1. Définissez [!UICONTROL Group By] sur la source d’acquisition (ou de référence) et sélectionnez les sources que vous souhaitez inclure.
1. Cet exemple utilise le type de graphique `stacked columns`.

Voici une présentation visuelle :

![Création d’un total des recettes par rapport à la date d’enregistrement de l’utilisateur et au rapport source.](../../assets/Revenue_by_user_registration_date_and_source.gif)

## Répétition des commandes par source d’utilisateur {#repeatordersbysource}

Le rapport Valeur de commande moyenne vous indique, en moyenne, le nombre d’utilisateurs acquis d’une source spécifique qui dépensent lors du placement d’une commande. Ce rapport, en revanche, ne vous indique pas si ces mêmes utilisateurs sont des clients réguliers. Mais avec les commandes répétées par les sources des utilisateurs, vous pouvez voir si les utilisateurs d’une source particulière effectuent plus ou moins des achats répétés.

Pour créer ce rapport dans le [Report Builder](../../tutorials/using-visual-report-builder.md), ajoutez la mesure **Nombre de commandes**, puis procédez comme suit :

1. Définissez le [!UICONTROL Time Period] sur la période d’enregistrement que vous souhaitez analyser.
1. Définissez le [!UICONTROL Time Interval] sur mensuel.
1. Ajoutez un [!UICONTROL filter] afin que seuls les utilisateurs avec des commandes répétées soient inclus :

   Numéro de commande de l’utilisateur supérieur à 1

1. Définissez [!UICONTROL Group By] sur la source d’acquisition (ou de référence) et sélectionnez les sources que vous souhaitez inclure.
1. Cet exemple utilise le type de graphique `stacked columns`.

Voici une présentation visuelle :

![Création d’un rapport Commandes répétées par source d’utilisateur.](../../assets/Repeat_orders_by_user_source.gif)


## Remplissage {#wrapup}

Cette rubrique n’a abordé que quelques analyses que vous pouvez utiliser pour analyser la valeur de vos canaux d’acquisition et marketing, mais ce n’est que la partie visible de l’iceberg.

## Associé {#related}

* [Suivi de la source de référence de l’ordre via [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)
* [Connexion à votre compte  [!DNL Google Adwords] ](../importing-data/integrations/google-adwords.md)
* [Construire des dimensions avec des commandes et des données client [!DNL Google ECommerce] ](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Bonnes pratiques relatives au balisage UTM dans [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
