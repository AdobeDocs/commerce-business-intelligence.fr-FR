---
title: Analyse de l’activité du site web et des taux de conversion des clients
description: Découvrez comment configurer un tableau de bord qui effectuera le suivi de l’activité de votre site web (notamment des pages vues, des sessions et des utilisateurs) et de votre taux de conversion client au fil du temps.
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
role: Admin, User
feature: Reports, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---

# Analyse de l’activité du site web

[!DNL Adobe Commerce Intelligence] vous permet d’intégrer facilement vos données de coûts publicitaires au reste de vos données. Cela vous permet non seulement de comprendre l’activité de votre site web, mais également d’obtenir le pourcentage de visiteurs de votre site web qui deviennent un utilisateur enregistré ou effectuent un achat.

Cette rubrique explique comment configurer un tableau de bord qui effectuera le suivi de l’activité de votre site web (y compris les pages vues, les sessions et les utilisateurs) et du taux de conversion de vos clients au fil du temps.

## Conditions préalables

**Importation de vos données de coûts publicitaires** - Connexion [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md) to [!DNL Adobe Commerce Intelligence] - cela synchronise automatiquement votre [!DNL AdWords] dépensez dans Commerce Intelligence.

**Suivi des données du canal d’acquisition des utilisateurs** - Pour lier votre [!DNL Google AdWords] données à des commandes spécifiques dans votre base de données, vous devez [suivi de l’acquisition des utilisateurs](../analysis/google-track-user-acq.md) via [!DNL Google Analytics E-commerce]. Vous pouvez ainsi connecter chaque commande à une source et un support utm.

## Campagnes d’acquisition d’utilisateurs

Cette collection de rapports est créée à l’aide des éléments suivants :

* Mesures générées automatiquement lors de la connexion à la variable [!DNL Google AdWords] data
* Mesures de base qui doivent déjà être disponibles sur votre compte, comme `Number of orders` et `New users`
* Dimensions créées lors de la jointure de [!DNL Google Analytics Ecommerce] les données de votre base de données, comme la source utm de commande et le support utm de commande. Contactez l’équipe d’assistance si ces champs ne sont pas actuellement disponibles dans votre compte.

## Création de rapports

**Commencez par créer un rapport indiquant le nombre de pages vues, de sessions et d’utilisateurs au fil du temps :**

1. Créez un rapport.
1. Cliquez sur **[!UICONTROL Add Metric]**, puis placez le pointeur de la souris sur l’objet [!DNL Google Analytics] au bas de la liste déroulante, puis sélectionnez `Page Views`.
1. Ajoutez une autre mesure, en pointant à nouveau sur la fonction [!DNL Google Analytics] , cette fois en sélectionnant `Sessions`.
1. Ajoutez une troisième mesure, en pointant à nouveau sur la fonction [!DNL Google Analytics] , cette fois en sélectionnant `Users`.
1. Maintenant, remplacez votre période par une période glissante, d’il y a 31 jours à il y a 1 jour, et ajustez l’intervalle sur `by day`.
1. Attribuez un nom à votre rapport (par exemple, `Page views, sessions and users by day`), puis cliquez sur **[!UICONTROL Save]**.

**Le deuxième rapport examine le nombre de pages vues au cours de l’année écoulée :**

1. Créez un rapport.
1. Cliquez sur **[!UICONTROL Add Metric]**, placez le pointeur de la souris sur l’objet [!DNL Google Analytics] au bas de la liste déroulante, puis sélectionnez _Pages vues_.
1. Remplacez votre période par une plage mobile, d’il y a 13 mois à il y a 1 mois, puis ajustez l’intervalle sur `by month`.
1. Attribuez un nom à votre rapport, par exemple `Page views by month,` et cliquez sur **[!UICONTROL Save]**.

**Le troisième graphique présente le taux de rebond au cours de l’année écoulée :**

1. Créez un rapport.
1. Cliquez sur **[!UICONTROL Add Metric]**, placez le pointeur de la souris sur l’objet [!DNL Google Analytics] au bas de la liste déroulante, puis sélectionnez _Taux de rebond_.
1. Remplacez votre période par une plage mobile, d’il y a 13 mois à il y a 1 mois, puis ajustez l’intervalle sur `by month`.
1. Attribuez un nom à votre rapport, par exemple `Bounce rate by month`, puis cliquez sur **[!UICONTROL Save]**.

**Maintenant, comparez la durée de session moyenne des nouveaux visiteurs à celle des visiteurs récurrents :**

1. Créez un rapport.
1. Cliquez sur **UICONTROL Add Metric**, placez le pointeur de la souris sur l’objet [!DNL Google Analytics] au bas de la liste déroulante, puis sélectionnez `Average Session Length`.
1. Remplacez votre période par une plage mobile, d’il y a 13 mois à il y a 1 mois, puis ajustez l’intervalle sur `by month`?
1. Ajouter un `Group by` et sélectionnez `New or returning visitor`.  Vérifiez les `Show All` , puis cliquez sur **[!UICONTROL Apply]**.
1. Attribuez un nom à votre rapport, par exemple `Average session length`, puis cliquez sur **[!UICONTROL Save]**.

**Examinez ensuite les principaux domaines référents au cours des 30 derniers jours :**

1. Créez un rapport.
1. Cliquez sur **[!UICONTROL Add Metric]**, placez le pointeur de la souris sur l’objet [!DNL Google Analytics] au bas de la liste déroulante, puis sélectionnez `Sessions`.
1. Remplacez votre période par une période glissante, d’il y a 31 jours à 1 jour, puis ajustez l’intervalle sur `none`.
1. Ajouter un `Group by` et sélectionnez `ga:source`.  Vérifiez les _Tout afficher_ , puis cliquez sur **[!UICONTROL Apply]**.
1. Ajouter un autre `group by` et sélectionnez `ga:medium`. Vérifiez à nouveau le `Show All` , puis cliquez sur **[!UICONTROL Apply]**.
1. Attribuez un nom à votre rapport, par exemple `Top 20 Referring Domains, 30 Days`, puis cliquez sur **[!UICONTROL Save]**.

**Enfin, examinez la conversion :**

1. Créez un rapport.
1. Ajoutez les mesures suivantes :

* `New users`
   * Cliquez sur **[!UICONTROL Hide]** sous le nom de la mesure

* `Number of orders`
   * Ajouter un filtre pour `Customer's order number` = 1 et cliquez sur **[!UICONTROL Apply]**
   * Renommez la mesure en cliquant sur le nom de la mesure, en l’appelant. `Number of first orders`, puis cliquez sur **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** la mesure

* `Users`
   * **[!UICONTROL Hide]** la mesure
   * Remplacer la période par `24 months ago to now`, puis définissez l’intervalle sur `by month`.
   * Ajoutez les formules suivantes en cliquant sur **[!UICONTROL Formula]**.
   * A/D, puis cliquez sur **[!UICONTROL Apply]**
   * Renommer la formule `Registration conversion`
   * B/D, puis cliquez sur **[!UICONTROL Apply]**
   * Renommer la formule `First order conversion`
   * C/D puis cliquez sur **[!UICONTROL Apply]**
   * Renommer la formule `Any order conversion`

* Attribuez maintenant un nom à votre rapport, par exemple `Conversion by month`, puis cliquez sur **[!UICONTROL Save]**.

## Étapes suivantes

Maintenant que vous avez accès aux données relatives au trafic web et aux taux de conversion, vous pouvez commencer à les exploiter pour prendre des décisions professionnelles, telles que Quels sites sont les mieux placés pour diriger le trafic vers votre site ? ou laquelle de vos campagnes est la plus efficace pour acquérir des clients avec une valeur de durée de vie élevée ?

Au fur et à mesure que vous ajustez les dépenses publicitaires et la stratégie marketing, vous pouvez continuer à suivre les résultats dans [!DNL Commerce Intelligence], en itérant sur ce tableau de bord pour répondre aux priorités évolutives de votre entreprise.
