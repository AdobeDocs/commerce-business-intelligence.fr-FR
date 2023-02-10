---
title: Google Analytics - Aperçu des données de source d’acquisition d’utilisateurs
description: Découvrez comment segmenter vos données par source d’acquisition d’utilisateurs.
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 1%

---

# Segmentation par source d’acquisition d’utilisateurs

>[!NOTE]
>
>Le processus ci-dessous ne prend pas en charge [!DNL GoogleUniversal Analytics].

La possibilité de segmenter vos données par source d’acquisition d’utilisateurs est essentielle pour gérer efficacement votre plan marketing. Connaître la source d’acquisition des nouveaux utilisateurs indique les canaux qui génèrent les meilleurs retours et permet à votre équipe d’allouer les dollars marketing en toute confiance.

Si vous n’effectuez pas déjà le suivi des sources d’acquisition d’utilisateurs dans votre base de données, [!DNL MBI] peut vous aider à démarrer :

## Suivi de la source d’acquisition des utilisateurs

Nous vous recommandons de suivre deux méthodes pour suivre les données de source de référence en fonction de votre configuration :

### (Option 1) Suivi des données de source de référence de commande via [!DNL Google Analytics E-Commerce] (y compris [!DNL Shopify] Magasins)

Si vous utilisez [!DNL Google Analytics E-Commerce] pour suivre vos données de commande et de vente, vous pouvez tirer parti de notre [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) pour synchroniser les données de source de référence de chaque commande. Vous pourrez ainsi segmenter les recettes et les commandes par source de référence (par exemple, `utm_source` ou `utm_medium`) et également obtenir une idée des sources d’acquisition des clients via [!DNL MBI] dimensions personnalisées, telles que `User's first order source`.

>[!NOTE]
>
>Pour les utilisateurs Shopify** : Activer [!DNL [Google Analytics E-Commerce] tracking in Shopify](http://docs.shopify.com/manual/settings/general/google-analytics#ecommerce-tracking) avant de connecter votre [!DNL Google Analytics E-Commerce] compte à [!DNL MBI].

### (Option 2) Enregistrement [!DNL Google Analytics]Données source d’acquisition dans votre base de données

Dans cet article, nous expliquerons comment économiser [!DNL Google Analytics] les informations du canal d’acquisition dans votre propre base de données, à savoir : `source`, `medium`, `term`, `content`, `campaign`, et `gclid` qui étaient présents lors de la première visite d’un utilisateur sur votre site web. Pour une explication de ces paramètres, consultez la section [!DNL [Google Analytics] documentation](http://support.google.com/analytics/bin/answer.py?hl=en&amp;answer=1191184). Nous allons ensuite explorer certaines des puissantes analyses marketing qui peuvent être effectuées à l’aide de ces informations dans [!DNL MBI].

#### Pourquoi ?

Si vous vous contentez de consulter la valeur par défaut [!DNL Google Analytics] mesures de conversion et d’acquisition, vous n’obtenez pas l’ensemble de l’image. Bien qu’il soit intéressant de voir le nombre de conversions du référencement organique par rapport au référencement payant, que pouvez-vous faire avec ces informations ? Devriez-vous dépenser plus d&#39;argent pour le référencement payant ? Cela dépend de la valeur des clients provenant de ce canal, ce qui n’est pas ce que les Google Analytics fournissent.

>[!NOTE]
>
>[!DNL [Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) résout ce problème en stockant les données de transaction dans [!DNL Google Analytics], mais cette solution ne fonctionne pas pour les sites autres que eCommerce, et certains outils tels que l’analyse des cohortes ne sont pas faciles à utiliser dans la variable [!DNL Google Analytics] .

Que se passe-t-il si vous souhaitez envoyer par courrier électronique une offre de relance à tous les clients acquis à partir d’une certaine campagne par courrier électronique ? Ou intégrer les données d’acquisition à votre système CRM ? Cela est impossible dans [!DNL Google Analytics] - en fait, il est contraire aux Conditions d’utilisation de [!DNL Google Analytics] pour stocker toutes les données qui identifient un individu.  Mais cela ne signifie pas que vous ne pouvez pas stocker ces données vous-même.

#### Méthode

[!DNL Google Analytics] stocke les informations de référence du visiteur dans un cookie appelé `__utmz`. Une fois ce cookie défini (par la variable [!DNL Google Analytics] code de suivi), son contenu sera envoyé à votre domaine avec chaque demande ultérieure de cet utilisateur. Ainsi, en PHP, par exemple, vous pouvez vérifier le contenu de `$_COOKIE['__utmz']` et vous verriez une chaîne qui ressemble à ceci :

> `100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

Il existe clairement des données source d’acquisition codées dans la chaîne. Nous avons vérifié qu’il s’agit de la dernière source d’acquisition du visiteur et des données de campagne associées. Maintenant nous avons juste besoin de savoir comment extraire les données. Heureusement, Justin Cutroni a déjà décrit le fonctionnement de cet encodage, et a partagé du code JavaScript pour extraire les éléments clés d&#39;information.

Nous avons pris ce code et l&#39;avons traduit en une [Bibliothèque PHP hébergée sur github](https://github.com/RJMetrics/referral-grabber-php).   Pour utiliser la bibliothèque, `include` une référence à `ReferralGrabber.php` puis appelez

> `$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

La valeur renvoyée `$data` Un tableau sera une carte des clés. `source`, `medium`, `term`, `content`, `campaign`, `gclid` et leurs valeurs respectives.

Nous vous recommandons d’ajouter une nouvelle table à votre base de données appelée, par exemple : `user_referral`, avec les colonnes comme : `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. Chaque fois qu’un utilisateur s’inscrit, prenez les informations de référence et stockez-les dans ce tableau.

#### Utilisation de ces données

Maintenant que nous enregistrons la source d’acquisition d’utilisateurs, comment pouvons-nous l’utiliser ?

Supposons que nous utilisions une base de données SQL et que nous ayons une `users` avec la structure suivante :

| ID | EMAIL | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | organique |
| 2 | jim@abc.com | 2012-01-24 | google | cpc |
| 3 | joe@def.com | 2012-01-25 | direct | - |
| 4 | jess@ghi.com | 2012-01-26 | référence | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | other | organique |
| ... | ... | ... | ... | ... |

Pour commencer, nous pouvons compter le nombre d&#39;utilisateurs provenant de chaque canal de référence en exécutant la requête suivante sur votre base de données :

> `SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

Le résultat ressemblera à ceci :

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| direct | 156 |
| référence | 55 |
| other | 16 |

C&#39;est intéressant, mais d&#39;usage limité. Ce que nous aimerions vraiment savoir, c&#39;est le taux de croissance de ces nombres au fil du temps, le montant des recettes générées par chaque source d&#39;acquisition, une [analyse des cohortes](http://cohortanalysis.com/) des utilisateurs provenant de chaque source et de la probabilité qu’un utilisateur de l’un de ces canaux revienne en tant que client à l’avenir. Les requêtes nécessaires à ces analyses sont complexes, c&#39;est pourquoi nous avons créé [!DNL MBI]. Grâce à ces informations, nous pouvons déterminer nos canaux d’acquisition les plus rentables et concentrer notre temps et notre argent marketing en conséquence.

### Associé

* **[Découvrez vos sources et canaux d’acquisition les plus précieux](../analysis/most-value-source-channel.md)**
* **[Connectez-vous à [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)**
* **[Augmentation du retour sur investissement de vos campagnes publicitaires](../analysis/roi-ad-camp.md)**
* **[Comment [!DNL Google Analytics] Fonctionnement de l’attribution UTM ?](../analysis/utm-attributes.md)**
