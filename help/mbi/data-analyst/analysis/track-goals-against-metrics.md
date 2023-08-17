---
title: Objectifs de suivi par rapport aux mesures
description: Découvrez comment configurer un tableau de bord qui vous aidera à effectuer le suivi des objectifs de votre entreprise par rapport à vos données réelles, notamment les recettes, les nouveaux utilisateurs enregistrés et les commandes au fil du temps.
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Objectifs de suivi par rapport aux mesures de performances

La plupart des clients souhaitent effectuer le suivi de leurs **objectifs commerciaux**, mais ne réalisez pas que cela est possible dans [!DNL Adobe Commerce Intelligence]. Cette rubrique explique comment configurer un tableau de bord qui vous aidera à effectuer le suivi des objectifs de votre entreprise par rapport à vos données réelles, notamment les recettes, les nouveaux utilisateurs enregistrés et les commandes au fil du temps. Vous apprenez également à comparer les performances d’une année à l’autre, le tout dans un tableau de bord comme celui-ci :

![](../../assets/Goals-_dashboard_2.png)

Avant de commencer, consultez la section [téléchargement de fichier](../importing-data/connecting-data/using-file-uploader.md) et assurez-vous d’avoir défini vos objectifs commerciaux pour une période donnée.

## Prise en main

Vous devez d’abord charger un fichier contenant des cibles quotidiennes/mensuelles/trimestrielles spécifiques pour votre entreprise.

Vous pouvez utiliser la variable [téléchargement de fichier](../importing-data/connecting-data/using-file-uploader.md) et l’image ci-dessous pour formater votre fichier. Les cibles les plus courantes dont les clients effectuent le suivi [!DNL Commerce Intelligence] comprennent les commandes, les recettes et les nouveaux comptes enregistrés.

![](../../assets/Goals-_Excel.png)

## Mesures

Créez une mesure pour chaque cible. Par exemple, si vous transférez des cibles de recettes mensuelles et de commandes, vous devez créer deux nouvelles mesures :

* **Objectif de recettes mensuel**
* Dans le **`Monthly goals`** table
* Cette mesure effectue une **Somme**
* Sur le **`Revenue target`** column
* Commandé par le **`Month`** timestamp

* **Cible des commandes mensuelles**
* Dans le **`Monthly goals`** table
* Cette mesure effectue une **Somme**
* Sur le **`Orders target`** column
* Commandé par le **`Month`** timestamp

* **Ciblage mensuel des nouveaux comptes enregistrés**
* Dans le **`Monthly goals`** table
* Cette mesure effectue une **Somme**
* Sur le **`New registered accounts target`** column
* Commandé par le **`Month`** timestamp

## Rapports

Il est utile de disposer d’un mélange de valeurs statiques et de graphiques visuels lors de l’analyse de vos cibles. Vous trouverez ci-dessous trois exemples de rapports pour vous aider à commencer à suivre les performances de vos recettes.

* **Recettes restantes pour atteindre la cible**
* Mesure `A`: `Revenue`
* 
  [!UICONTROL Mesure]: `Revenue`

* Mesure `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* [!UICONTROL Formula]: `Revenue left to achieve target`
* 
  [!UICONTROL Formule]: `(B-A)`
* 
  [!UICONTROL Format]: `Number`

* [!UICONTROL Time period]: (quelle que soit la période appropriée que vous souhaitez)
* 
  [!UICONTROL Interval]: `Month`
* 
  [!UICONTROL Type de graphique]: `Scalar`

* **Cibles de recettes**
* Mesure `A`: `Revenue`
* 
  [!UICONTROL Mesure]: `Revenue`

* Mesure `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* Mesure `C`: `Revenue (amount change since previous year)` (masquer)
* 
  [!UICONTROL Mesure]: `Revenue`
* [!UICONTROL Perspective]: `Amount change vs. Previous year`

* [!UICONTROL Formula]: (ce mois l’an dernier)
* 
  [!UICONTROL Formule]: `(A-C)`
* 
  [!UICONTROL Format]: `Currency`

* Désactiver `Multiple Y-Axes`
* [!UICONTROL Time period]: (quelle que soit la période appropriée que vous souhaitez)*
* 
  [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

Une fois que vous avez terminé les rapports ci-dessus pour les cibles de recettes, vous pouvez créer des rapports identiques pour les objectifs relatifs aux commandes, aux comptes enregistrés ou à toute autre valeur incluse dans le téléchargement du fichier d’objectifs.

Après avoir compilé tous les rapports, vous pouvez les organiser dans le tableau de bord suivant vos besoins. Le résultat peut ressembler à l’image en haut de cette page.
