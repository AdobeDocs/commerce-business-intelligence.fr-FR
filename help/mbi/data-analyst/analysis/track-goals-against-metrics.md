---
title: Suivi des objectifs par rapport aux mesures
description: Découvrez comment configurer un tableau de bord qui vous aidera à suivre les objectifs de votre entreprise par rapport à vos données réelles, y compris le chiffre d’affaires, les nouveaux utilisateurs enregistrés et les commandes au fil du temps.
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Suivi des objectifs par rapport aux mesures de performances

La plupart des clients aimeraient suivre leurs **objectifs commerciaux**, mais ne réalisent pas que c&#39;est possible en [!DNL Adobe Commerce Intelligence]. Cette rubrique explique comment configurer un tableau de bord qui vous aidera à comparer vos objectifs commerciaux et vos données réelles, notamment le chiffre d’affaires, les nouveaux utilisateurs enregistrés et les commandes, au fil du temps. Vous apprendrez également à comparer les performances d’une année sur l’autre, le tout dans un tableau de bord comme celui-ci :

![](../../assets/Goals-_dashboard_2.png)

Avant de commencer, vous devez consulter le [téléchargeur de fichiers](../importing-data/connecting-data/using-file-uploader.md) et vous assurer d’avoir défini les objectifs de votre entreprise pour une période donnée.

## Prise en main

Vous devez d&#39;abord télécharger un fichier contenant des cibles quotidiennes, mensuelles ou trimestrielles précises pour votre entreprise.

Vous pouvez utiliser le [téléchargeur de fichier](../importing-data/connecting-data/using-file-uploader.md) et l’image ci-dessous pour formater votre fichier. Les cibles les plus courantes suivies par les clients dans [!DNL Commerce Intelligence] comprennent les commandes, le chiffre d’affaires et les nouveaux comptes enregistrés.

![](../../assets/Goals-_Excel.png)

## Mesures

Créez une mesure pour chaque cible. Par exemple, si vous chargez des cibles mensuelles de revenus et de commandes, vous devez créer deux nouvelles mesures :

* **Cible mensuelle des revenus**
* Dans le tableau **`Monthly goals`**
* Cette mesure effectue une **Somme**
* Dans la colonne **`Revenue target`**
* Classé par l’horodatage **`Month`**

* **Cible des commandes mensuelles**
* Dans le tableau **`Monthly goals`**
* Cette mesure effectue une **Somme**
* Dans la colonne **`Orders target`**
* Classé par l’horodatage **`Month`**

* **Cible mensuelle des nouveaux comptes enregistrés**
* Dans le tableau **`Monthly goals`**
* Cette mesure effectue une **Somme**
* Dans la colonne **`New registered accounts target`**
* Classé par l’horodatage **`Month`**

## Rapports

Il est utile de combiner des valeurs statiques et des graphiques visuels lors de l’analyse de vos cibles. Vous trouverez ci-dessous trois exemples de rapports pour commencer à suivre les performances de votre chiffre d’affaires.

* **Chiffre d’affaires restant pour atteindre la cible**
* `A` de mesure : `Revenue`
* &#x200B;
  [!UICONTROL Metric]: `Revenue`

* `B` de mesure : `Target Revenue`
* [!UICONTROL Metric] : `Monthly Revenue Target`

* [!UICONTROL Formula] : `Revenue left to achieve target`
* &#x200B;
  [!UICONTROL Formule]: `(B-A)`
* &#x200B;
  [!UICONTROL Format]: `Number`

* [!UICONTROL Time period] : (quelle que soit la période pertinente que vous souhaitez)
* &#x200B;
  [!UICONTROL Interval]: `Month`
* &#x200B;
  [!UICONTROL Type de graphique]: `Scalar`

* **Cibles de chiffre d’affaires**
* `A` de mesure : `Revenue`
* &#x200B;
  [!UICONTROL Metric]: `Revenue`

* `B` de mesure : `Target Revenue`
* [!UICONTROL Metric] : `Monthly Revenue Target`

* `C` de mesure : `Revenue (amount change since previous year)` (masquer)
* &#x200B;
  [!UICONTROL Metric]: `Revenue`
* [!UICONTROL Perspective] : `Amount change vs. Previous year`

* [!UICONTROL Formula] : (ce mois-ci l&#39;année dernière)
* &#x200B;
  [!UICONTROL Formule]: `(A-C)`
* &#x200B;
  [!UICONTROL Format]: `Currency`

* Désactiver `Multiple Y-Axes`
* [!UICONTROL Time period] : (quelle que soit la période pertinente que vous souhaitez)*
* &#x200B;
  [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type] : `Line Chart`

Une fois que vous avez terminé les états ci-dessus pour les objectifs de chiffre d&#39;affaires, vous pouvez créer des états identiques pour les objectifs relatifs aux commandes, aux comptes enregistrés ou à toute autre valeur que vous avez incluse dans le téléchargement du fichier d&#39;objectifs.

Après avoir compilé tous les rapports, vous pouvez les organiser selon vos besoins dans le tableau de bord. Le résultat peut ressembler à l’image en haut de cette page.
