---
title: Google Analytics - Présentation des données Source de suivi d’acquisition d’utilisateurs
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

La possibilité de segmenter vos données par source d’acquisition d’utilisateurs est essentielle pour gérer efficacement votre plan marketing. Connaître la source d’acquisition des nouveaux utilisateurs montre quels canaux génèrent les meilleurs rendements et permet à votre équipe d’allouer les fonds marketing en toute confiance.

Si vous n’effectuez pas déjà le suivi des sources d’acquisition d’utilisateurs dans votre base de données, [!DNL Adobe Commerce Intelligence] pouvez commencer par :

## Suivi de la source d’acquisition des utilisateurs

[!DNL Adobe] recommande deux méthodes pour effectuer le suivi des données de la source de référence en fonction de votre configuration :

### (Option 1) Suivre les données de la source de référence des commandes via [!DNL Google Analytics E-Commerce]

Si vous utilisez [!DNL Google Analytics E-Commerce] pour suivre les données de commande et de vente, vous pouvez utiliser le [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) pour synchroniser les données de la source de référence de chaque commande. Vous pouvez ainsi segmenter le chiffre d’affaires et les commandes par source de référence (par exemple, `utm_source` ou `utm_medium`). Vous pouvez également vous faire une idée des sources d’acquisition de clients grâce à [!DNL Commerce Intelligence] dimensions personnalisées telles que `User's first order source`.

### (Option 2) Enregistrement des données sources d&#39;acquisition des [!DNL Google Analytics] dans votre base de données

Cette rubrique explique comment enregistrer [!DNL Google Analytics] informations sur le canal d’acquisition dans votre propre base de données, à savoir les paramètres `source`, `medium`, `term`, `content`, `campaign` et `gclid` qui étaient présents lors de la première visite d’un utilisateur ou d’une utilisatrice sur votre site web. Pour une explication de ces paramètres, consultez la [[!DNL Google Analytics] documentation](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article). Ensuite, vous explorez certaines des puissantes analyses marketing qui peuvent être effectuées avec ces informations dans [!DNL Commerce Intelligence].

#### Pourquoi ?

Si vous regardez simplement les mesures de conversion et d’acquisition [!DNL Google Analytics] par défaut, vous n’obtenez pas une vue d’ensemble. Bien que le nombre de conversions d’un référencement organique par rapport à un référencement payant soit intéressant, que pouvez-vous faire avec cette information ? Devriez-vous dépenser plus d&#39;argent sur le référencement payant ? Cela dépend de la valeur des clients provenant de ce canal, ce qui n’est pas quelque chose que Google Analytics fournit.

>[!NOTE]
>
>[[!DNL Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) atténue ce problème en stockant les données de transaction dans [!DNL Google Analytics], mais cette solution ne fonctionne pas pour les sites hors eCommerce. En outre, certains outils tels que l’analyse des cohortes ne sont pas faciles à utiliser dans l’interface [!DNL Google Analytics].

Que se passe-t-il si vous souhaitez envoyer par e-mail une offre de relance à tous les clients acquis à partir d’une certaine campagne par e-mail ? Ou intégrer des données d&#39;acquisition à votre système CRM ? Ceci est impossible en [!DNL Google Analytics] - en fait, il est contraire aux Conditions d&#39;utilisation pour [!DNL Google Analytics] de stocker toute donnée qui identifie un individu. Mais vous pouvez stocker ces données vous-même.

#### La Méthode

[!DNL Google Analytics] stocke les informations de référence des visiteurs dans un cookie appelé `__utmz`. Une fois ce cookie défini (par le code de suivi [!DNL Google Analytics]), son contenu est envoyé avec chaque requête ultérieure à votre domaine de cet utilisateur. Donc en PHP, par exemple, vous pouvez vérifier le contenu de `$_COOKIE['__utmz']` et vous verrez une chaîne qui ressemble à quelque chose comme ceci :

`100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

Il existe clairement des données source d’acquisition codées dans la chaîne. Il est testé pour confirmer qu’il s’agit de la dernière source d’acquisition du visiteur et des données de campagne associées. Vous devez maintenant savoir comment extraire les données.

Ce code a été traduit en [bibliothèque PHP hébergée sur github](https://github.com/RJMetrics/referral-grabber-php). Pour utiliser la bibliothèque, `include` une référence à `ReferralGrabber.php`, puis appelez

`$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

Le tableau de `$data` renvoyé est un mappage des clés `source`, `medium`, `term`, `content`, `campaign`, `gclid` et de leurs valeurs respectives.

Adobe recommande d’ajouter à votre base de données une table appelée par exemple `user_referral`, avec des colonnes telles que : `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. Chaque fois qu’un utilisateur s’inscrit, saisissez les informations de référence et enregistrez-les dans cette table.

#### Utilisation de ces données

Maintenant que vous enregistrez la source d’acquisition d’utilisateurs, comment pouvez-vous l’utiliser ?

Supposons que vous utilisiez une base de données SQL et que vous ayez une table `users` avec la structure suivante :

| ID | E-MAIL | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 24/01/2012 | google | organique |
| 2 | jim@abc.com | 24/01/2012 | google | cpc |
| 3 | joe@def.com | 25/01/2012 | direct | - |
| 4 | jess@ghi.com | 26/01/2012 | recommandation | techcrunch.com |
| 5 | jen@ghi.net | 30/01/2012 | autres frais | organique |
| ... | ... | ... | ... | ... |

Pour commencer, vous pouvez compter le nombre d’utilisateurs provenant de chaque canal de référence en exécutant la requête suivante sur votre base de données :

`SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

Le résultat ressemble à ceci :

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| direct | 156 |
| recommandation | 55 |
| autres frais | 16 |

C&#39;est intéressant, mais d&#39;une utilité limitée. Ce que vous souhaitez savoir, c&#39;est :

* Le taux de croissance de ces chiffres au fil du temps
* Le montant des revenus générés par chaque source d&#39;acquisition
* Une [ analyse des cohortes ](https://en.wikipedia.org/wiki/Cohort_analysis) utilisateurs provenant de chaque source
* Probabilité qu’un utilisateur de l’un de ces canaux revienne en tant que client à l’avenir

Les requêtes nécessaires à ces analyses sont complexes. Avec ces informations, vous pouvez déterminer vos canaux d’acquisition les plus rentables et concentrer le temps et l’argent marketing en conséquence.

### Connexe

* **[Découvrez vos sources et canaux d’acquisition les plus précieux](../analysis/most-value-source-channel.md)**
* **[Connecter votre [!DNL Google Adwords] compte](../importing-data/integrations/google-adwords.md)**
* **[Augmentez le retour sur investissement de vos campagnes publicitaires](../analysis/roi-ad-camp.md)**
* **[Comment l’attribution UTM fonctionne [!DNL Google Analytics] elle ?](../analysis/utm-attributes.md)**
