---
title: Réplication de canaux Google Analytics à l'aide de sources d'acquisition
description: Découvrez comment répliquer des canaux Google Analytics à l’aide de sources d’acquisition.
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# [!DNL Google Analytics] à l’aide des sources d’acquisition

## Que sont les canaux ? {#channels}

La création de segments personnalisés pour voir les performances des différents trafics et observer les tendances est l’une des utilisations les plus puissantes de [!DNL Google Analytics]. Une classe de segments qui existe par défaut dans [!DNL Google Analytics] est `Channels`. Les canaux sont un groupe de méthodes courantes que les personnes utilisent pour se rendre sur votre site.  [!DNL Google Analytics] trie automatiquement les nombreuses façons dont vous acquérez un utilisateur (qu’il s’agisse de réseaux sociaux, de paiement par clic, d’e-mails ou de liens de référence) et les regroupe dans un compartiment ou un canal.

## Pourquoi ne puis-je pas voir mes `channels` dans Commerce Intelligence ? {#nochannels}

`Channels` sont des ensembles de données simples et agrégés. Pour trier vos acquisitions en intervalles de canaux, [!DNL Google] définit des règles et des définitions distinctes à l’aide de paramètres spécifiques : une combinaison d’acquisition [Source](https://support.google.com/analytics/answer/1033173?hl=en) (l’origine de votre trafic) et d’acquisition [Medium](https://support.google.com/analytics/answer/6099206?hl=en) (la catégorie générale de la source).

Bien que ces compartiments puissent vous aider à comprendre la provenance de votre trafic, ces données ne sont pas balisées par canal, mais par une combinaison de Source et de Medium. Étant donné que [!DNL Google] envoie les informations de canal sous la forme de deux points de données distincts, les regroupements de canaux ne s’affichent pas automatiquement dans [!DNL Commerce Intelligence].

## Quels sont les regroupements de canaux par défaut ? Comment sont-ils créés ?

Par défaut, [!DNL Google] configure huit canaux différents. Les règles qui déterminent le mode de création des canaux sont les suivantes.

| **Canal** | **Qu&#39;est-ce que c&#39;est ?** | **Comment est-il créé ?** |
|---|---|---|
| Direct | Toute personne qui accède directement à votre site. | SOURCE = `Direct`<br> ET MEDIUM = `(not set); OR Medium = (none)` |
| Recherche organique | Trafic classé de manière organique dans les moteurs de recherche non payants. | MEDIUM = `organic` |
| Référence | Trafic provenant d’un lien externe qui n’est pas une recherche organique ou de sites web qui ne sont pas des réseaux sociaux. | MEDIUM = `referral` |
| Référencement Payant | Trafic dont le code de suivi UTM indique que le média est « cpc », « ppc » ou « paidsearch » ET qui est un réseau de distribution publicitaire qui ne correspond pas à « Content ». | Medium = `^(cpc|ppc|paidsearch)$`<br>AND Ad Distribution Network ≠ `Content` |
| Social | Trafic de référence provenant de l’un des quelque 400 réseaux sociaux [&#128279;](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/) et qui n’est pas balisé en tant que publicité. | Référencement vers Social Source = `Yes`<br>OU Medium = `^(social|social-network|social-media|sm|social network|social media)$` |
| E-mail | Trafic des sessions balisées avec le support « e-mail ». | Code de suivi UTM de Medium = `email` |
| Affichage | Trafic comportant un code de suivi UTM sur lequel le support est display ou cpm. Inclut également les interactions AdWords où le réseau de distribution publicitaire correspond au « Contenu » | Medium = `^(display|cpm|banner)$`<br>OU réseau de distribution publicitaire = `Content`<br>ET format publicitaire ≠ `Text` |
| Autres frais | Sessions d’autres canaux publicitaires (sans inclure le référencement payant) balisés avec un support de type « cpc », « ppc », « cpm », « cpv », « cpa », « cpp », « affiliate ». | MEDIUM = `^(cpv|cpa|cpp|content-text)$` |

{style="table-layout:auto"}

## Comment recréer ces regroupements de canaux dans mon Data Warehouse ? {#recreate}

Maintenant que vous savez que les canaux ne sont que des combinaisons de sources et de supports, il est facile en 3 étapes de recréer ces regroupements dans votre Data Warehouse.

1. **Activer votre[!DNL Google ECommerce]intégration**

   [Une fois activé](../importing-data/integrations/google-ecommerce.md), veillez à [synchroniser]&#x200B;(../{{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#syncing) les champs **medium** et **source** dans votre Data Warehouse. Une fois cette opération terminée, les données d’acquisition moyennes et sources sont importées dans votre Data Warehouse.

1. **Charger un mappage des regroupements de canaux Google**

   Adobe Commerce crée une table avec les regroupements par défaut mappés sous la forme d’un fichier que vous pouvez [télécharger](../../assets/ga-channel-mapping.csv).

   Si vous êtes un [!DNL Google Analytics] professionnel et que vous avez créé vos propres canaux, vous souhaitez ajouter vos règles spécifiques à la table de mappage avant de charger le fichier dans [!DNL Commerce Intelligence].

   Ajoutez-le à votre Data Warehouse en tant que [Chargement de fichier](../importing-data/connecting-data/using-file-uploader.md).

   ![](../../assets/Setting_Primary_Keys.png)

1. **Établir une relation entre[!DNL Google ECommerce]et le chargement de fichier de mappages**

   Pour établir une relation entre le et la table de mappage[!DNL Google ECommerce] [envoyez une demande d’assistance](../../guide-overview.md#Submitting-a-Support-Ticket) à votre équipe d’analystes de données et référencez cette rubrique. L’analyste crée une colonne calculée appelée **Canal** dans le tableau ECommerce. **Après un cycle de mise à jour complet** cette colonne est prête à être utilisée dans un `Filter` ou une `Group by`.

Vous disposez désormais de regroupements [!DNL Google Analytics Channel] dans votre Data Warehouse, ce qui signifie que vous pouvez analyser vos données selon une nouvelle perspective :

![Segmentation de la mesure Nombre de commandes par canal](../../assets/GA_Channel_Gif.gif)

Dans cet exemple, vous avez commencé simplement par segmenter la mesure **Nombre de commandes** par **Canal**. Testez votre nouvelle colonne et découvrez les tendances que vous pouvez identifier dans vos données [!DNL Google Analytics Channel].

## Documentation connexe

* [Utilisation du Report Builder](../../tutorials/using-visual-report-builder.md)
* [Données [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce-data.md)
* [Création[!DNL Google ECommerce]dimensions avec des données de commande et de client](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Quelles sont vos sources et vos canaux d’acquisition les plus précieux ?](../analysis/most-value-source-channel.md)
