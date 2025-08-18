---
title: Google Analytics et attribution UTM
description: En savoir plus sur le processus d’attribution de la source Google Analytics.
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
role: Admin, Data Architect, Data Engineer, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# Attribution [!DNL Google Analytics] et UTM

Il est essentiel de [suivre la source d’acquisition des utilisateurs](../../data-analyst/analysis/google-track-user-acq.md) pour [identifier les campagnes publicitaires les plus performantes](../../data-analyst/analysis/most-value-source-channel.md). Cette rubrique explore le processus d’attribution de source [!DNL Google Analytics]. En d’autres termes, quel élément d’information est enregistré quand.

## Qu’est-ce que l’attribution ?

`Attribution` s’agit de spécifier une source de référence pour une activité particulière. Ces activités sont généralement des macro-conversions ou des micro-conversions, les macro étant des choses comme **achats**, les micro étant des choses comme **enregistrement, inscription par e-mail, commentaire de blog** et ainsi de suite.

Idéalement, chaque fois qu’un événement de conversion se produit, une source de référence est enregistrée. Mais comment la source est-elle déterminée ?

La réalité est que les utilisateurs proviennent souvent de nombreuses sources avant d&#39;atteindre/de valider une micro ou macro conversion. Par exemple, ils peuvent se rendre sur le site via l&#39;organique, puis en sortir, puis venir via le référencement payant, puis en sortir, puis en revenir directement sur le site lui-même. Ces informations de suivi de la source sont souvent fournies au site via les paramètres UTM, mais il existe également des systèmes plus sophistiqués. Pour vos besoins, concentrez-vous sur [UTM](https://support.google.com/analytics/answer/1033867?hl=en&ref_topic=1032998).

## Comment attribue-t-[!DNL Google Analytics] des sources de référence via des paramètres UTM ?

Lorsque les paramètres UTM sont spécifiés sur l’URL, ils sont analysés et placés dans un [!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie). Si un site web n’a pas de [!DNL Google Analytics], il est inutile d’avoir des UTM. [!DNL Google Analytics] comporte des règles relatives à la manière dont il traite un utilisateur qui accède à plusieurs URL avec des UTM au cours de sa vie (plus d’informations à ce sujet ultérieurement). En supposant que le site web soit configuré pour capturer les paramètres UTM dans une base de données externe, lorsqu’une micro ou macro conversion se produit, tout ce qui se trouve dans le cookie [!DNL Google Analytics] au moment de la conversion est répliqué dans la base de données.

## Premier clic ou dernier clic

### Attribution du dernier clic

L’attribution Dernier clic est le modèle d’attribution le plus couramment utilisé par [!DNL Google Analytics]. Dans ce cas, le cookie [!DNL Google Analytics] représente les paramètres UTM de la source la plus récente avant l’événement de conversion. Il est [ enregistré dans la base de données](../../data-analyst/analysis/google-track-user-acq.md). Le cookie [!DNL Google Analytics] ne remplace les paramètres UTM précédents que si l’utilisateur clique sur une nouvelle URL contenant un nouveau jeu de paramètres UTM.

Prenons l’exemple d’un utilisateur qui visite d’abord un site web via [!DNL Google Analytics] *référencement payant*, puis le renvoie via *recherche organique* et revient finalement au site web *directement* ou via un lien *e-mail* **sans paramètres UTM** avant l’événement de conversion. Dans cet exemple, le cookie [!DNL Google Analytics] indique que la source de l’utilisateur est organique (organique), puisqu’il s’agit de la dernière source avant la conversion. Le *chemin* de l’utilisateur avant que cet événement de conversion final ne soit ignoré. Si, au lieu de cela, l’utilisateur a visité le site web à partir d’un lien e-mail avec UTM, le cookie [!DNL Google Analytics] dira que la source est « e-mail ». Par conséquent, si des paramètres UTM existent dans le cookie et que l’utilisateur accède à via direct, le cookie [!DNL Google Analytics] affiche les paramètres UTM plutôt que « direct ».

>[!NOTE]
>
>Les paramètres des cookies [!DNL Google Analytics] d’un utilisateur spécifique sont effacés à l’expiration du cookie [ou ](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)’un utilisateur efface ses cookies dans le navigateur.*

### Attribution du premier clic

Certains outils d’attribution payants vous permettent de capturer la « pile de galettes » de sources dans le chemin d’accès d’un utilisateur. Dans ce cas, dans l’exemple ci-dessus, le premier clic sur l’attribution indique le référencement payant. Certains sites web implémentent également leurs propres cookies pour capturer une pile de crêpes et stocker la première source dans leur base de données.

## Comment analyser l’attribution ?

[!DNL Google Analytics] dispose d’une fonctionnalité robuste dans son interface web qui vous permet d’exécuter quatre modèles d’attribution différents :

1. premier clic
1. dernier clic
1. linéaire (diviser le chiffre d’affaires de manière égale entre toutes les sources du chemin d’accès)
1. pondéré (attribution personnalisée)

Maintenant que vous comprenez quel est le modèle d’attribution pour chaque micro ou macro-conversion, la question devient « Que faites-vous de la totalité des conversions d’un utilisateur ? ».  Par exemple, examinez les UTM enregistrés en fonction de la logique de dernier clic de la version générale :

* Les utilisateurs s’enregistrent sous organique
* Premier achat de l&#39;utilisateur sous référencement payant 5,00 $
* Deuxième achat de l&#39;utilisateur sous e-mail 50,00 $
* Troisième achat de l&#39;utilisateur en dessous du bio 10,00 $

Voici où vous demandez : « Combien de revenus ai-je tirés du référencement payant ? À partir de l’e-mail ?  Du bio ? ». Vous pouvez dire que les réponses sont 5, 50 et 10 (quelle que soit la dernière source), ou vous pouvez également dire que vous attribuez tous les revenus à la première source (les 65 vont à l&#39;agriculture biologique). Vous pouvez également effectuer une analyse pondérée ou appliquer le modèle linéaire (c’est-à-dire environ 22 modèles chacun).

## Documentation connexe

* [Suivre la source de référence des commandes via [!DNL Google Analytics] E-Commerce](../importing-data/integrations/google-ecommerce.md)
* [Suivre la source de référence des utilisateurs dans votre base de données](../analysis/google-track-user-acq.md)
* [Effectuez le suivi des données relatives aux appareils, aux navigateurs et aux systèmes d’exploitation dans votre base de données](../analysis/google-track-user-acq.md)
* [Découvrez vos sources et canaux d’acquisition les plus précieux.](../analysis/most-value-source-channel.md)
* [Connecter votre  [!DNL Google Adwords] ](../importing-data/integrations/google-adwords.md)
* [Augmenter le retour sur investissement de vos campagnes publicitaires](../analysis/roi-ad-camp.md)
* [Cinq bonnes pratiques pour le balisage UTM dans  [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
