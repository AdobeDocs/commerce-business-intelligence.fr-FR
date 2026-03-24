---
title: Analyse de l’activité du site web et des taux de conversion des clients
description: Découvrez comment configurer un tableau de bord qui suivra l’activité de votre site web, notamment les pages vues, les sessions et les utilisateurs, ainsi que votre taux de conversion client au fil du temps.
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
role: Admin, User
feature: Reports, Data Integration
TQID: https://experienceleague.adobe.com/HcoHrBbXXjQGsd80DA06Dwq2dDmhUiuRbRLj-QONlw4
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 756
ht-degree: 0%

---

# Analyse de l’activité du site web

[!DNL Adobe Commerce Intelligence] vous permet d’intégrer facilement vos données de coûts publicitaires au reste de vos données. Cela vous permet non seulement de comprendre l’activité de votre site web, mais également d’obtenir le pourcentage de visiteurs et visiteuses sur votre site web qui deviennent un utilisateur ou une utilisatrice enregistré(e) ou effectuent un achat.

Cette rubrique explique comment configurer un tableau de bord qui suivra l’activité de votre site web, notamment les pages vues, les sessions et les utilisateurs, ainsi que votre taux de conversion client au fil du temps.

## Conditions préalables

**Importer vos données de coût publicitaire** - Connecter [[!DNL [Google AdWords]]](../importing-data/integrations/google-adwords.md) à [!DNL Adobe Commerce Intelligence] - synchronise automatiquement vos dépenses [!DNL AdWords] dans Commerce Intelligence.

**Suivre les données du canal d’acquisition d’utilisateurs** - Pour lier vos données [!DNL Google AdWords] à des commandes spécifiques dans votre base de données, vous devez [suivre l’acquisition d’utilisateurs](../analysis/google-track-user-acq.md) via [!DNL Google Analytics E-commerce]. Vous pouvez ainsi connecter chaque commande à une source et un support utm.

## Campagnes d’acquisition d’utilisateurs

Cette collection de rapports est créée à l’aide des éléments suivants :

* Mesures générées automatiquement lorsque vous connectez vos données [!DNL Google AdWords]
* Mesures de base qui doivent déjà être disponibles sur votre compte, telles que `Number of orders` et `New users`
* Dimensions créées lors de la jonction de vos données [!DNL Google Analytics Ecommerce] à votre base de données, telles que la source utm de la commande et le support utm de la commande. Contactez l’équipe d’assistance si ces champs ne sont pas actuellement disponibles dans votre compte

## Création de rapports

**Commencez par créer un rapport qui indique le nombre de pages vues, de sessions et d’utilisateurs au fil du temps :**

1. Créez un rapport.
1. Cliquez sur **[!UICONTROL Add Metric]**, puis placez le pointeur de la souris sur la section [!DNL Google Analytics] au bas de la liste déroulante et sélectionnez `Page Views`.
1. Ajoutez une autre mesure en pointant à nouveau la souris sur la section [!DNL Google Analytics], cette fois en sélectionnant `Sessions`.
1. Ajoutez une troisième mesure, en pointant à nouveau la souris sur la section [!DNL Google Analytics], cette fois en sélectionnant `Users`.
1. Maintenant, définissez la période sur une plage mobile, comprise entre 31 jours et 1 jour auparavant, puis définissez l’intervalle sur `by day`.
1. Attribuez un nom à votre rapport (par exemple, `Page views, sessions and users by day`), puis cliquez sur **[!UICONTROL Save]**.

**Le deuxième rapport examine le nombre de pages vues au cours de l’année écoulée :**

1. Créez un rapport.
1. Cliquez sur **[!UICONTROL Add Metric]**, placez le pointeur de la souris sur la section [!DNL Google Analytics] en bas de la liste déroulante, puis sélectionnez _Pages vues_.
1. Définissez la période sur une plage mobile, comprise entre 13 mois et 1 mois auparavant, puis définissez l’intervalle sur `by month`.
1. Donnez un nom à votre rapport, par exemple `Page views by month,` et Cliquez sur **[!UICONTROL Save]**.

**Le troisième graphique examine le taux de rebond au cours de l’année écoulée :**

1. Créez un rapport.
1. Cliquez sur **[!UICONTROL Add Metric]**, placez le pointeur de la souris sur la section [!DNL Google Analytics] en bas de la liste déroulante, puis sélectionnez _Taux de rebond_.
1. Définissez la période sur une plage mobile, comprise entre 13 mois et 1 mois auparavant, puis définissez l’intervalle sur `by month`.
1. Donnez un nom à votre rapport, comme `Bounce rate by month`, puis cliquez sur **[!UICONTROL Save]**.

**Maintenant, regardez la durée de session moyenne des nouveaux visiteurs par rapport aux visiteurs récurrents :**

1. Créez un rapport.
1. Cliquez sur **UICONTROL Ajouter une mesure**, placez le pointeur de la souris sur la section [!DNL Google Analytics] au bas de la liste déroulante, puis sélectionnez `Average Session Length`.
1. Remplacez votre période par une période mobile, comprise entre 13 mois et 1 mois auparavant, puis définissez l’intervalle sur `by month` ?
1. Ajoutez un `Group by` et sélectionnez `New or returning visitor`.  Cochez la case `Show All`, puis cliquez sur **[!UICONTROL Apply]**.
1. Donnez un nom à votre rapport, comme `Average session length`, puis cliquez sur **[!UICONTROL Save]**.

**Ensuite, examinez vos principaux domaines référents au cours des 30 derniers jours :**

1. Créez un rapport.
1. Cliquez sur **[!UICONTROL Add Metric]**, placez le pointeur de la souris sur la section [!DNL Google Analytics] au bas de la liste déroulante, puis sélectionnez `Sessions`.
1. Définissez la période sur une plage mobile, comprise entre 31 jours et 1 jour auparavant, puis définissez l’intervalle sur `none`.
1. Ajoutez un `Group by` et sélectionnez `ga:source`.  Cochez la case _Tout afficher_, puis cliquez sur **[!UICONTROL Apply]**.
1. Ajoutez un autre `group by` et sélectionnez `ga:medium`. Cochez à nouveau la case `Show All`, puis cliquez sur **[!UICONTROL Apply]**.
1. Attribuez un nom à votre rapport, comme `Top 20 Referring Domains, 30 Days`, puis cliquez sur **[!UICONTROL Save]**.

**Enfin, regardez la conversion :**

1. Créez un rapport.
1. Ajoutez les mesures suivantes :

* `New users`
   * Cliquez sur **[!UICONTROL Hide]** sous le nom de la mesure

* `Number of orders`
   * Ajoutez un filtre pour `Customer's order number` = 1 et cliquez sur **[!UICONTROL Apply]**
   * Renommez la mesure en cliquant sur son nom, en l’appelant `Number of first orders`, puis en cliquant sur **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** la mesure

* `Users`
   * **[!UICONTROL Hide]** la mesure
   * Remplacez la période par `24 months ago to now` et l’intervalle par `by month`.
   * Ajoutez les formules suivantes en cliquant sur **[!UICONTROL Formula]**.
   * A/D puis cliquez sur **[!UICONTROL Apply]**
   * Renommer le `Registration conversion` de formule
   * B/D puis cliquez sur **[!UICONTROL Apply]**
   * Renommer le `First order conversion` de formule
   * C/D, puis cliquez sur **[!UICONTROL Apply]**
   * Renommer le `Any order conversion` de formule

* Attribuez maintenant un nom à votre rapport, comme `Conversion by month`, puis cliquez sur **[!UICONTROL Save]**.

## Étapes suivantes

Maintenant que vous avez accès aux données sur votre trafic web et vos taux de conversion, vous pouvez commencer à les exploiter pour prendre des décisions commerciales, telles que Quels sites sont les mieux à même de générer du trafic vers votre site ? ou laquelle de vos campagnes est la plus efficace pour acquérir des clients avec une valeur de durée de vie élevée ?

À mesure que vous ajustez les dépenses publicitaires et la stratégie marketing, vous pouvez continuer à suivre les résultats dans [!DNL Commerce Intelligence], en effectuant une itération sur ce tableau de bord pour répondre aux priorités changeantes de votre entreprise.
