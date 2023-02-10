---
title: Réplication des canaux Google Analytics à l’aide de sources d’acquisition
description: Découvrez comment répliquer des canaux Google Analytics à l’aide de sources d’acquisition.
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# Google Analytics utilisant des sources d’acquisition

## Que sont les canaux ? {#channels}

Création de segments personnalisés pour observer les performances de différents trafic et observer les tendances (pour le meilleur ou pour le pire). est l’une des utilisations les plus puissantes pour  [!DNL Google Analytics ]. Une classe de segments qui existe par défaut dans [!DNL Google Analytics ] are `Channels`. Les canaux sont un ensemble de méthodes courantes par lesquelles les visiteurs se rendent sur votre site.  [!DNL Google Analytics ] trie automatiquement les nombreuses façons dont vous acquérez un utilisateur (qu’il s’agisse de liens de médias sociaux, de paiement par clic, d’e-mail ou de référence) et les regroupe dans un compartiment ou un canal.

## Pourquoi je ne vois pas mon `channels` dans l&#39;IMS ? {#nochannels}

`Channels` sont des regroupements de données simples et agrégés. Pour classer vos acquisitions en compartiments de canal, Google définit des règles et des définitions distinctes à l’aide de paramètres spécifiques : une combinaison d&#39;acquisition [Source](https://support.google.com/analytics/answer/1033173?hl=en) (l’origine de votre trafic) et l’acquisition [Volume moyen](https://support.google.com/analytics/answer/6099206?hl=en) (catégorie générale de la source).

Bien que ces compartiments puissent vous aider à comprendre d’où provient votre trafic, ces données ne sont pas réellement balisées par canal, mais par une combinaison de source et de support. Comme Google envoie des informations sur les canaux en tant que deux points de données distincts, les regroupements de canaux ne s’affichent pas automatiquement dans [!DNL MBI].

## Quels sont les groupements de canaux par défaut ? Comment sont-ils créés ?

Par défaut, Google vous configure avec 8 canaux différents. Examinons les règles qui déterminent leur mode de création :

| Canal | Qu&#39;est-ce que c&#39;est ? | Comment est-il créé ? |
|---|---|---|
| Direct | Toute personne qui accède directement à votre site. | Source = `Direct`<br>ET Moyen = `(not set); OR Medium = (none)` |
| Recherche organique | Trafic classé de manière organique dans les moteurs de recherche non rémunérés. | Moyen = `organic` |
| Référent | Trafic provenant d’un lien externe qui n’est pas une recherche organique ou de sites web qui ne sont pas des réseaux sociaux. | Moyen = `referral` |
| Recherche payante | Trafic qui comporte un code de suivi UTM dans lequel le support est &quot;cpc&quot;, &quot;ppc&quot; ou &quot;paidsearch&quot; ET est un réseau de distribution d’annonces qui ne correspond pas à &quot;Content&quot;. | Moyen = `^(cpc|ppc|paidsearch)$`<br>ET ≠ réseau de distribution de publicités `Content` |
| Social | Trafic référent provenant d’une partie ou d’une partie approximativement [400 réseaux sociaux](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/) et ne sont pas balisés en tant que publicités. | Référence de la source sociale = `Yes`<br>OU Moyen = `^(social|social-network|social-media|sm|social network|social media)$` |
| Email | Trafic des sessions balisées avec un support de &quot;courrier électronique&quot;. | Code de suivi UTM de Medium = `email` |
| Affichage | Trafic qui comporte un code de suivi UTM où le support est affiché ou cpm. Inclut également les interactions AdWords où le réseau de distribution d’annonces correspond à &quot;Contenu&quot; | Moyen = `^(display|cpm|banner)$`<br>OU Réseau de distribution d’annonces = `Content`<br>ET Format de publicité ≠ `Text` |
| Autre | Sessions provenant d’autres canaux publicitaires, à l’exclusion de la recherche payante, qui sont balisées avec un support de &quot;cpc&quot;, &quot;ppc&quot;, &quot;cpm&quot;, &quot;cpv&quot;, &quot;cpa&quot;, &quot;cpp&quot;, &quot;affilié&quot;. | Moyen = `^(cpv|cpa|cpp|content-text)$` |

{style=&quot;table-layout:auto&quot;}

## Comment puis-je recréer ces groupements de canaux dans mon Data Warehouse ? {#recreate}

Maintenant que vous savez que les canaux ne sont que des combinaisons de sources et de supports, il est facile de recréer ces regroupements en 3 étapes dans votre Data Warehouse.

1. **Activez vos[!DNL Google ECommerce]integration**

   [Une fois activée](../importing-data/integrations/google-ecommerce.md), veillez à [synchronisation](../{{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#syncing) la variable **medium** et **source** dans votre Data Warehouse. Une fois cette étape terminée, les données d’acquisition de sources et moyennes seront introduites dans votre Data Warehouse.

1. **Chargement d’un mappage des regroupements de canaux Google**

   Pour gagner du temps, Commerce a déjà créé un tableau avec les regroupements par défaut mappés en tant que fichier que vous pouvez [télécharger](../../assets/ga-channel-mapping.csv).

   Si vous êtes un professionnel Google Analytics et que vous avez créé vos propres canaux, vous souhaiterez ajouter vos règles spécifiques à la table de mappage avant de charger le fichier dans [!DNL MBI].

   Apportez-le dans votre Data Warehouse en tant que [Téléchargement du fichier](../importing-data/connecting-data/using-file-uploader.md).

   ![](../../assets/Setting_Primary_Keys.png)

1. **Établir une relation entre[!DNL Google ECommerce]et téléchargement du fichier de mappage**

   Pour établir une relation entre la variable[!DNL Google ECommerce]et la table de mapping, [envoyer une demande d’assistance ;](../../guide-overview.md) à notre équipe d’analystes de données et reportez-vous à cet article. L’analyste crée une nouvelle colonne calculée appelée **Canal** dans la table Commerce. **Après un cycle de mise à jour complet**, cette colonne sera prête à être utilisée dans un filtre ou un groupe par .

Félicitations ! Vous disposez maintenant de groupements de canaux Google Analytics dans votre Data Warehouse, ce qui signifie que vous pouvez analyser vos données d’un point de vue nouveau :

![Segmentation de la mesure Nombre de commandes par canal](../../assets/GA_Channel_Gif.gif)

Dans cet exemple, nous avons commencé simplement en segmentant la variable **Nombre de commandes** mesure par **Canal**. C’est maintenant votre tour. Testez votre nouvelle colonne et découvrez les tendances que vous pouvez identifier dans vos données de canal Google Analytics !

## Documentation connexe

* [Utilisation du Report Builder](../../tutorials/using-visual-report-builder.md)
* [Valeur attendue[!DNL Google ECommerce]data](../importing-data/integrations/google-ecommerce-data.md)
* [Création[!DNL Google ECommerce]dimensions avec les données de commande et de client ;](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Quelles sont vos sources et canaux d’acquisition les plus précieux ?](../analysis/most-value-source-channel.md)
