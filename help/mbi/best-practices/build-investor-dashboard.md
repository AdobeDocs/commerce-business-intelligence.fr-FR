---
title: Créer un tableau de bord pour les investisseurs
description: Découvrez comment créer un tableau de bord pour les investisseurs.
exl-id: 917e7628-3498-4413-a7e1-61799989a7dd
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# Créer un tableau de bord d’investisseur

De nombreux clients travaillent avec des investisseurs et doivent partager des informations à partir de la plateforme, mais les tableaux de bord que vous créez pour prendre des décisions commerciales quotidiennes peuvent ne pas correspondre à ce qu&#39;un investisseur recherche. Vous trouverez ci-dessous quelques bonnes pratiques pour créer un tableau de bord complet mais simple, idéal pour partager avec des investisseurs actifs et potentiels.

Voici ce dont vous avez besoin pour créer des rapports pour votre tableau de bord d’investisseur :

## Rapports Scalaires

* **[!UICONTROL All-time revenue]**
* **[!UICONTROL Distinct buyers]**
* **[!UICONTROL All-time number of orders]**
* **[!UICONTROL AOV]**
* **[!UICONTROL Items sold]**

## Rapports visuels

* **[!UICONTROL Revenue by quarter]**
   * Mesure - Chiffre d’affaires
* **[!UICONTROL Revenue from 1st time orders vs repeat orders]**
   * Mesure - Chiffre d’affaires de première commande
      * Filtre - Le numéro de commande de l’utilisateur est égal à 1
   * Mesure 2 - Chiffre d’affaires de commandes répétées
      * Filtre : le numéro de commande de l’utilisateur est supérieur à 1.
   * Décochez la case Plusieurs axes Y
   * Transformer en graphique à colonnes empilées
* **[!UICONTROL AOV by quarter]**
   * Mesure 1 - Chiffre d’affaires
      * Masquer cette mesure
   * Mesure 2 - Nombre de commandes
      * Masquer cette mesure
   * Formule - AOV
      * A/B
* **[!UICONTROL All-time revenue by source]**
   * Mesure - Chiffre d’affaires
   * Regrouper par `utm_source` du client
* **[!UICONTROL Revenue from top 10 products]**
   * Mesure - Chiffre d’affaires du produit
      * Masquer le graphique
      * Regroupez par nom de produit. Sélectionnez tous les produits.
      * Définir la période sur Tous les temps
      * Définissez l’intervalle sur Aucun
      * Dans « Afficher en haut/en bas », afficher uniquement les 10 premiers par bénéfice produit
* **[!UICONTROL Cumulative distinct buyers by quarter]**
   * Mesure - Acheteurs distincts
      * Perspective - Cumulée
* **[!UICONTROL Site visits - New vs. repeat by month]**
* Sessions

Avec une intégration [!DNL Google Analytics], vous pouvez inclure des rapports sur :

* Visites de site
* Taux de conversion

Avec les [services d’enrichissement des données de Commerce](https://business.adobe.com/products/magento/magento-commerce.html), vous pouvez inclure des rapports sur :

* Clients uniques par état/région, âge, sexe.

## Autres conseils

* Utilisez une convention d’affectation des noms claire et concise [convention de nommage](../best-practices/naming-elements.md)
* Partager le tableau de bord avec les utilisateurs investisseurs
* Ou envoyez-le via **[!UICONTROL Automated email summary]**(../data-user/export-data/email-summaries.md)
* Créez un seul tableau de bord. Cela facilite la gestion du contenu et vous savez exactement ce que vos investisseurs recherchent.

Organisez vos rapports avec soin et faites attention aux détails. Une fois terminé, le tableau de bord ressemble à ce qui suit :

![Créer un tableau de bord d’investisseur](../../mbi/assets/investor-dboard-example.png)
