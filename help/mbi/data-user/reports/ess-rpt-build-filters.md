---
title: Filtres
description: Découvrez comment utiliser les filtres.
exl-id: eb683dfe-9a90-400a-a0c0-3dc00d1f28b5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 0854d644cb72b3fc8b8b31a0bf7e8dca4cc99724
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# Filtres

Un ou plusieurs filtres peuvent être ajoutés pour limiter les données utilisées pour produire un rapport. Chaque filtre est une expression qui comprend une colonne du tableau associé, un opérateur et une valeur. Par exemple, pour inclure uniquement les clients réguliers, vous pouvez créer un filtre qui inclut uniquement les clients qui ont passé plusieurs commandes. Plusieurs filtres peuvent être utilisés avec des opérateurs logiques `AND/OR` pour ajouter une logique au rapport.

>[!TIP]
>
>Un rapport peut contenir un maximum de 3 500 points de données. Pour réduire le nombre de points de données, utilisez un filtre afin de réduire la quantité de données utilisées pour générer le rapport.

[!DNL Adobe Commerce Intelligence] comprend une sélection de filtres que vous pouvez utiliser prêts à l’emploi ou modifier en fonction de vos besoins. Le nombre de filtres que vous pouvez créer n’est pas limité.

## Pour ajouter un filtre :

1. Dans le graphique, passez la souris sur chaque point de données.

   Dans ce rapport, chaque point de données affiche le nombre total de clients pour le mois.

1. Dans le panneau de gauche, cliquez sur l’icône Filtres (![](../../assets/magento-bi-btn-filter.png)) .

   ![Ajouter filtre](../../assets/magento-bi-report-builder-filter-add.png)

1. Cliquez sur **[!UICONTROL Add Filter]**.

   Les filtres sont numérotés par ordre alphabétique et le premier est `[A]`. Les deux premières parties du filtre sont des options de liste déroulante, et la troisième partie est une valeur.

   ![](../../assets/magento-bi-report-builder-filter-add-a.png)

   * Cliquez sur la première partie du filtre et choisissez la colonne que vous souhaitez utiliser comme objet de l&#39;expression.

     ![Choisir la première partie du filtre](../../assets/magento-bi-report-builder-filter-part1.png)

   * Cliquez sur la deuxième partie du filtre et choisissez l&#39;opérateur .

     ![Choisir l’opérateur](../../assets/magento-bi-report-builder-filter-part2.png)

   * Dans la troisième partie du filtre, saisissez la valeur nécessaire pour terminer l’expression.

     ![Saisissez la valeur](../../assets/magento-bi-report-builder-filter-part3.png)

   * Une fois le filtre terminé, cliquez sur **[!UICONTROL Apply]**.

     Le rapport inclut désormais uniquement les clients et clientes réguliers, et le nombre d’enregistrements de clients récupérés pour le rapport a été réduit de 33 000 à 12 600.

     ![ Rapport filtré ](../../assets/magento-bi-report-builder-filter-report.png)<!--{: .zoom}-->

1. Dans la barre latérale, cliquez sur l’icône de perspective (![icône de perspective](../../assets/magento-bi-btn-perspective.png)).

   ![Perspective](../../assets/magento-bi-report-builder-filter-perspective.png)<!--{: .zoom}-->

1. Dans la liste des paramètres, choisissez `Cumulative`. Cliquez ensuite sur **[!UICONTROL Apply]**.

   ![Perspective Cumulée](../../assets/magento-bi-report-builder-filter-perspective-cumulative.png)

   La perspective `Cumulative` répartit le changement au fil du temps, plutôt que d’afficher les variations à la hausse et à la baisse pour chaque mois.

1. Saisissez un `Title` pour le rapport et cliquez dessus **[!UICONTROL Save]** tant que `Chart` de votre tableau de bord.

   ![Enregistrer dans le tableau de bord](../../assets/magento-bi-report-builder-filter-perspective-cumulative-save.png)
