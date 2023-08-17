---
title: Création d’un tableau de bord pour les investisseurs
description: Découvrez comment créer un tableau de bord pour les investisseurs.
exl-id: 917e7628-3498-4413-a7e1-61799989a7dd
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# Créer le tableau de bord des investisseurs

De nombreux clients travaillent avec des investisseurs et doivent partager des informations à partir de la plateforme, mais les tableaux de bord que vous créez pour prendre des décisions commerciales quotidiennes ne sont peut-être pas ce qu’un investisseur recherche. Vous trouverez ci-dessous quelques bonnes pratiques pour créer un tableau de bord complet mais simple, idéal pour le partage avec des investisseurs actifs et potentiels.

Voici ce que vous devez créer pour le tableau de bord de votre investisseur :

## Rapports scalaires

* **[!UICONTROL All-time revenue]**
* **[!UICONTROL Distinct buyers]**
* **[!UICONTROL All-time number of orders]**
* **[!UICONTROL AOV]**
* **[!UICONTROL Items sold]**

## Rapports Visuels

* **[!UICONTROL Revenue by quarter]**
   * Mesure - Recettes
* **[!UICONTROL Revenue from 1st time orders vs repeat orders]**
   * Mesure : recettes de la première commande
   * Filtre : le numéro de commande de l’utilisateur est égal à 1
   * Mesure 2 - Recettes des commandes répétées
      * Filtre : le numéro de commande de l’utilisateur est supérieur à 1
   * Décochez la case pour plusieurs axes Y
   * Passer à un graphique à colonnes empilées
* **[!UICONTROL AOV by quarter]**
   * Mesure 1 - Recettes
      * Masquer cette mesure
   * Mesure 2 - Nombre de commandes
      * Masquer cette mesure
   * Formule - AOV
      * A/B
* **[!UICONTROL All-time revenue by source]**
   * Mesure - Recettes
   * Groupe par client `utm_source`
* **[!UICONTROL Revenue from top 10 products]**
   * Mesure - Chiffre d’affaires des produits
      * Masquer le graphique
      * Regrouper par nom de produit. Sélectionnez tous les produits.
      * Définissez la période sur Toutes les heures.
      * Définissez l’intervalle sur Aucun .
      * Dans &quot;Afficher le haut/le bas&quot;, affichez uniquement les 10 premiers triés par produit rentable
* **[!UICONTROL Cumulative distinct buyers by quarter]**
   * Mesure - acheteurs distincts
      * Perspective - Cumulative
* **[!UICONTROL Site visits - New vs. repeat by month]**
* Sessions

Avec [!DNL Google Analytics] intégration, vous pouvez inclure des rapports sur les éléments suivants :

* Visites du site
* Taux de conversion

Avec la variable [Services d’enrichissement des données de commerce](https://business.adobe.com/products/magento/magento-commerce.html), vous pouvez inclure des rapports sur les éléments suivants :

* Clients uniques par état/région, âge, genre.

## Autres conseils

* Utiliser une ligne claire et concise [convention de dénomination](../best-practices/naming-elements.md)
* Partage du tableau de bord avec les utilisateurs investisseurs
* Ou l’envoyer via **[!UICONTROL Automated email summary]**(../data-user/export-data/email-summaries.md)
* Créez un seul tableau de bord. Cela facilite la maintenance du contenu, et vous savez exactement ce que voient vos investisseurs.

Organisez vos rapports avec soin et prêtez attention aux détails. Une fois l’opération terminée, le tableau de bord se présente comme suit :

![](../../mbi/assets/investor-dboard-example.png)
