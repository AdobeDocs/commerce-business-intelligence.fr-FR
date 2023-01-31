---
title: Identification de vos sources marketing et canaux les plus utiles
description: Découvrez certains rapports que vous pouvez utiliser pour découvrir vos canaux marketing les plus précieux.
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 0%

---

# Identification des sources marketing réussies

Vous avez fait des recherches sur votre audience, créé votre campagne, investi dans quelques canaux marketing. Maintenant que le temps est écoulé, comment ces canaux fonctionnent-ils ? Quel canal a attiré les nouveaux utilisateurs ? Quelle source a le plus contribué à vos recettes totales ?

Avec [!DNL MBI], vous pouvez facilement segmenter les recettes et les utilisateurs par source de référence, qu’ils correspondent ou non à [!DNL [Google Analytics' UTM fields]](https://support.google.com/analytics/answer/1191184?hl=en) ou des champs de données personnalisés. Cette segmentation vous permettra de trouver les canaux les plus performants et d’investir davantage votre budget marketing.

Dans cet article, nous allons explorer certains rapports que vous pouvez utiliser pour découvrir vos canaux marketing les plus précieux :

* [Nouveaux utilisateurs par sources](#newusersbysource)
* [Chiffre d’affaires moyen de la durée de vie par source d’utilisateur](#avglifetimerev)
* [Valeur de commande moyenne par source d’utilisateur](#avgorderval)
* [Recettes par date d’enregistrement des utilisateurs et par sources](#revbyregdateandsource)
* [Répétition des commandes par source d’utilisateur](#repeatordersbysource)

## Conditions préalables {#prereqs}

Pour créer les analyses de cet article, vous devez accéder aux données de source d’acquisition/de référence marketing. Si vous ne le suivez pas déjà, vous devrez apporter [données source de référence de commande provenant de [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md) into [!DNL MBI] avant de pouvoir continuer. En outre, l’ajout d’informations sur les appareils utilisateur à vos analyses vous permet de voir la technologie que vos référents utilisent.

## Nouveaux utilisateurs par source {#newusersbysource}

L’évaluation du rendement des sources d’orientation est essentielle pour déterminer vos canaux les plus précieux. Ce rapport présente le nombre d’utilisateurs nouvellement enregistrés, par source d’acquisition, au fil du temps, ce qui vous permet de suivre les performances des sources de référence dans l’acquisition de nouveaux utilisateurs enregistrés.

Pour créer ce rapport dans le [Report Builder](../../tutorials/using-visual-report-builder.md), ajoutez le **Nouveaux utilisateurs** mesure (ou mesure équivalente qui comptabilise le nombre de nouveaux utilisateurs au fil du temps) du rapport. Procédez ensuite comme suit :

1. Définissez la variable [!UICONTROL Time Period] à la période d&#39;enregistrement que vous souhaitez analyser.
1. Définissez la variable [!UICONTROL Interval] au mois.
1. Définir [!UICONTROL Group By] à la source d’acquisition (ou de référence) et sélectionnez les sources à inclure.
1. Dans cet exemple, nous avons utilisé la méthode `stacked columns` [!UICONTROL chart type].

Voici une présentation visuelle :

![Création d’un rapport Nouveaux utilisateurs par source .](../../assets/New_Users_by_source.gif)

## Chiffre d’affaires moyen de la durée de vie par source d’utilisateur {#avglifetimerev}

Il est important de trouver les canaux qui attirent de nouveaux utilisateurs, mais quelle est la valeur globale de ces renvois ? Ce rapport présente les recettes de durée de vie moyenne des utilisateurs provenant de sources d’acquisition spécifiques au fil du temps. En d’autres termes, cela vous permet de voir si les utilisateurs acquis par une source particulière dépensent plus avec vous au cours de leur vie qu’un groupe d’utilisateurs acquis par une autre source.

Pour créer ce rapport dans le Report Builder, ajoutez le **Chiffre d’affaires moyen** au rapport. Procédez ensuite comme suit :

1. Définissez la variable [!UICONTROL Time Period] à la période que vous souhaitez analyser.
1. Définissez la variable [!UICONTROL Interval] au mois.
   [!UICONTROL Group By] à la source d’acquisition (ou de référence) et sélectionnez les sources à inclure.
1. Dans cet exemple, nous avons utilisé la méthode `line chart` type.

Voici une présentation visuelle :

![Création de recettes de durée de vie moyenne par source d’utilisateur](../../assets/Lifetime_revenue_by_user_source.gif).

Cet exemple ne tient compte que des recettes sur la durée de vie, mais vous pouvez également répliquer cette analyse pour examiner la variable [!UICONTROL Number of orders] ou [!UICONTROL Distinct buyers] par la source de référence.

## Valeur de commande moyenne par source d’utilisateur {#avgorderval}

Pour mieux comprendre le montant d’argent dépensé par les utilisateurs d’une source d’acquisition spécifique, vous pouvez créer un rapport qui examine la valeur de leur commande moyenne. Vous pourrez ainsi déterminer si les utilisateurs acquis à partir d’une source spécifique dépensent plus par commande que les utilisateurs provenant d’une autre source.

Pour créer ce rapport dans le Report Builder, ajoutez le **Valeur de commande moyenne** puis procédez comme suit :

1. Définissez la variable [!UICONTROL Time Period] à la période d&#39;enregistrement que vous souhaitez analyser.
1. Définissez la variable [!UICONTROL Time Interval] au mois.
1. Définir [!UICONTROL Group By] à la source d’acquisition (ou de référence) et sélectionnez les sources à inclure.
1. Dans cet exemple, nous avons utilisé la méthode **colonnes empilées** type de graphique.

Voici une présentation visuelle :

![Création d’un rapport Valeur de commande moyenne par source d’utilisateur.](../../assets/Average_order_value_by_source.gif)

## Chiffre d’affaires total par date d’enregistrement de l’utilisateur et source {#revbyregdateandsource}

L’analyse des recettes sur la durée de vie que nous avons effectuée plus tôt vous permet de consulter les recettes moyennes sur la durée de vie des utilisateurs provenant de sources différentes, mais qu’en est-il des recettes totales sur la durée de vie ? Ce rapport vous permet d’identifier le montant global des recettes générées par les utilisateurs enregistrés au cours d’une période spécifique et à partir d’une source spécifique.

Pour créer ce rapport dans le Report Builder, ajoutez le `Revenue by user registration date` mesure. Si vous n’avez pas [créé cette mesure](../../data-user/reports/ess-manage-data-metrics.md) vous pouvez déjà le faire en répliquant la variable `Revenue` et de modifier la variable `time stamp` à l’utilisateur `creation date`. Après avoir ajouté la mesure, procédez comme suit :

1. Définissez la variable [!UICONTROL Time Period] à la période d&#39;enregistrement que vous souhaitez analyser.
1. Définissez la variable [!UICONTROL Time Interval] au mois.
1. Définir [!UICONTROL Group By] à la source d’acquisition (ou de référence) et sélectionnez les sources à inclure.
1. Dans cet exemple, nous avons utilisé la méthode `stacked columns` type de graphique.

Voici une présentation visuelle :

![Création d’un rapport Total des recettes par date d’enregistrement de l’utilisateur et source.](../../assets/Revenue_by_user_registration_date_and_source.gif)

## Répétition des commandes par source d’utilisateur {#repeatordersbysource}

Le rapport Valeur de commande moyenne vous indique, en moyenne, le montant que les utilisateurs acquis d’une source spécifique dépensent lors du placement d’une commande. Ce rapport, en revanche, ne vous indique pas si ces mêmes utilisateurs sont des clients réguliers. Mais avec les commandes répétées par les sources des utilisateurs, vous pouvez voir si les utilisateurs d’une source particulière effectuent plus ou moins des achats répétés.

Pour créer ce rapport dans le [Report Builder](../../tutorials/using-visual-report-builder.md), ajoutez le **Nombre de commandes** puis procédez comme suit :

1. Définissez la variable [!UICONTROL Time Period] à la période d&#39;enregistrement que vous souhaitez analyser.
1. Définissez la variable [!UICONTROL Time Interval] au mois.
1. Ajouter un [!UICONTROL filter] afin que seuls les utilisateurs avec des commandes répétées soient inclus :

   Numéro de commande de l’utilisateur supérieur à 1

1. Définir [!UICONTROL Group By] à la source d’acquisition (ou de référence) et sélectionnez les sources à inclure.
1. Dans cet exemple, nous avons utilisé la méthode `stacked columns` type de graphique.

Voici une présentation visuelle :

![Création d’un rapport Commandes répétées par source d’utilisateur .](../../assets/Repeat_orders_by_user_source.gif)


## Remplissage {#wrapup}

Dans cet article, nous n&#39;avons abordé que quelques analyses que vous pouvez utiliser pour analyser la valeur de vos canaux d&#39;acquisition et marketing, mais ce n&#39;est que la partie visible de l&#39;iceberg. Si vous avez créé une analyse puissante que nous n&#39;avons pas décrite ici, laissez-nous vous expliquer ce que vous faites dans les commentaires.

## Associé {#related}

* [Suivi de la source de référence des commandes via [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)
* [Connectez-vous à [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Création [!DNL Google ECommerce] dimensions avec commandes et données client](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Bonnes pratiques relatives au balisage UTM dans [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
