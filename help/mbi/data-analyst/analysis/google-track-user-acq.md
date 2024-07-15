---
title: Google Analytics - Présentation des données Source d’acquisition d’utilisateurs
description: Découvrez comment segmenter vos données par source d’acquisition d’utilisateurs.
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 3098909fdccb726108c24f2424e4ba4c1db9d1c2
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 1%

---

# Segmentation par source d’acquisition d’utilisateurs

>[!NOTE]
>
>Le processus ci-dessous ne prend pas en charge [!DNL Google Universal Analytics].

La possibilité de segmenter vos données par source d’acquisition d’utilisateurs est essentielle pour gérer efficacement votre plan marketing. Connaître la source d’acquisition des nouveaux utilisateurs indique les canaux qui génèrent les meilleurs retours et permet à votre équipe d’allouer les dollars marketing en toute confiance.

Si vous ne suivez pas déjà les sources d&#39;acquisition d&#39;utilisateurs dans votre base de données, [!DNL Adobe Commerce Intelligence] peut vous aider à démarrer :

## Suivi de la source d’acquisition des utilisateurs

[!DNL Adobe] recommande deux méthodes pour suivre les données de source de référence en fonction de votre configuration :

### (Option 1) Suivi des données source de référence de commande via [!DNL Google Analytics E-Commerce]

Si vous utilisez [!DNL Google Analytics E-Commerce] pour suivre les données de commande et de vente, vous pouvez utiliser le [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) pour synchroniser les données de source de référence de chaque commande. Vous pouvez ainsi segmenter les recettes et les commandes par source de référence (par exemple, `utm_source` ou `utm_medium`). Vous obtenez également une idée des sources d’acquisition de clients via [!DNL Commerce Intelligence] dimensions personnalisées telles que `User's first order source`.

### (Option 2) Enregistrement des données source d’acquisition [!DNL Google Analytics] dans votre base de données

Cette rubrique explique comment enregistrer les informations du canal d’acquisition [!DNL Google Analytics] dans votre propre base de données, à savoir les paramètres `source`, `medium`, `term`, `content`, `campaign` et `gclid` présents lors de la première visite d’un utilisateur sur votre site web. Pour une explication de ces paramètres, consultez la [[!DNL Google Analytics] documentation](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article). Ensuite, vous explorez certaines des puissantes analyses marketing qui peuvent être effectuées avec ces informations dans [!DNL Commerce Intelligence].

#### Pourquoi ?

Si vous vous contentez d’examiner les mesures de conversion et d’acquisition par défaut [!DNL Google Analytics], vous n’obtenez pas l’image complète. Bien qu’il soit intéressant de voir le nombre de conversions du référencement organique par rapport au référencement payant, que pouvez-vous faire avec ces informations ? Devriez-vous dépenser plus d&#39;argent en recherche payante ? Cela dépend de la valeur des clients provenant de ce canal, ce qui n’est pas ce que les Google Analytics fournissent.

>[!NOTE]
>
>[[!DNL Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) résout ce problème en stockant les données de transaction dans [!DNL Google Analytics], mais cette solution ne fonctionne pas pour les sites autres que eCommerce. En outre, certains outils tels que l’analyse des cohortes ne sont pas faciles à utiliser dans l’interface [!DNL Google Analytics].

Que se passe-t-il si vous souhaitez envoyer par courrier électronique une offre de relance à tous les clients acquis à partir d’une certaine campagne par courrier électronique ? Ou intégrer les données d’acquisition à votre système CRM ? Cela est impossible dans [!DNL Google Analytics] - en fait, il est contraire aux Conditions d’utilisation de [!DNL Google Analytics] de stocker toutes les données qui identifient un individu. Mais vous pouvez stocker ces données vous-même.

#### Méthode

[!DNL Google Analytics] stocke les informations de référence des visiteurs dans un cookie appelé `__utmz`. Une fois ce cookie défini (par le code de suivi [!DNL Google Analytics]), son contenu sera envoyé à chaque demande ultérieure de cet utilisateur vers votre domaine. Ainsi, en PHP, par exemple, vous pouvez extraire le contenu de `$_COOKIE['__utmz']` et vous verrez une chaîne qui ressemble à ceci :

`100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

Il existe clairement des données source d’acquisition codées dans la chaîne. Ceci est testé afin de confirmer qu’il s’agit de la dernière source d’acquisition du visiteur et des données de campagne associées. Vous devez maintenant savoir comment extraire les données.

Ce code a été traduit en une [bibliothèque PHP hébergée sur github](https://github.com/RJMetrics/referral-grabber-php). Pour utiliser la bibliothèque, `include` une référence à `ReferralGrabber.php`, puis appelez

`$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

Le tableau `$data` renvoyé est une carte des clés `source`, `medium`, `term`, `content`, `campaign`, `gclid` et leurs valeurs respectives.

Adobe recommande d&#39;ajouter à votre base de données un tableau appelé, par exemple, `user_referral`, avec des colonnes du type : `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. Chaque fois qu’un utilisateur s’inscrit, prenez les informations de référence et stockez-les dans ce tableau.

#### Utilisation de ces données

Maintenant que vous enregistrez la source d’acquisition utilisateur, comment pouvez-vous l’utiliser ?

Supposons que vous utilisez une base de données SQL et que vous ayez une table `users` avec la structure suivante :

| ID | EMAIL | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | organique |
| 2 | jim@abc.com | 2012-01-24 | google | cpc |
| 3 | joe@def.com | 2012-01-25 | direct | - |
| 4 | jess@ghi.com | 2012-01-26 | référence | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | other | organique |
| .. | .. | .. | .. | .. |

Pour commencer, vous pouvez comptabiliser le nombre d&#39;utilisateurs provenant de chaque canal de référence en exécutant la requête suivante sur votre base de données :

`SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

Le résultat ressemble à ceci :

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| direct | 156 |
| référence | 55 |
| other | 16 |

C&#39;est intéressant, mais d&#39;usage limité. Ce que vous souhaitez vraiment savoir est :

* Le taux de croissance de ces nombres au fil du temps
* Montant des recettes générées par chaque source d’acquisition
* Une [analyse des cohortes](https://en.wikipedia.org/wiki/Cohort_analysis) d’utilisateurs provenant de chaque source
* La probabilité qu’un utilisateur de l’un de ces canaux revienne comme client à l’avenir

Les requêtes nécessaires à ces analyses sont complexes. Grâce à ces informations, vous pouvez déterminer vos canaux d’acquisition les plus rentables et concentrer le temps et l’argent marketing en conséquence.

### Associé

* **[Découvrez vos sources et canaux d’acquisition les plus précieux](../analysis/most-value-source-channel.md)**
* **[Connectez votre  [!DNL Google Adwords] compte](../importing-data/integrations/google-adwords.md)**
* **[Augmentez le retour sur investissement de vos campagnes publicitaires](../analysis/roi-ad-camp.md)**
* **[Comment fonctionne l’attribution UTM  [!DNL Google Analytics] UTM ?](../analysis/utm-attributes.md)**
