---
title: Filtres
description: Découvrez comment utiliser les filtres.
exl-id: eb683dfe-9a90-400a-a0c0-3dc00d1f28b5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Filtres

Un ou plusieurs filtres peuvent être ajoutés pour limiter les données utilisées pour générer un rapport. Chaque filtre est une expression qui inclut une colonne de la table associée, un opérateur et une valeur. Par exemple, pour inclure uniquement les clients réguliers, vous pouvez créer un filtre qui inclut uniquement les clients qui ont passé plusieurs commandes. Plusieurs filtres peuvent être utilisés avec des `AND/OR` pour ajouter une logique au rapport.

>[!TIP]
>
>Un rapport peut contenir, au maximum, 3 500 points de données. Pour réduire le nombre de points de données, utilisez un filtre afin de réduire la quantité de données utilisées pour générer le rapport.

[!DNL Adobe Commerce Intelligence] comprend une sélection de filtres que vous pouvez utiliser &quot;prêts à l’emploi&quot; ou modifier en fonction de vos besoins. Le nombre de filtres que vous pouvez créer n’est pas limité.

## Pour ajouter un filtre :

1. Dans le graphique, passez la souris sur chaque point de données.

   Dans ce rapport, chaque point de données indique le nombre total de clients pour le mois.

1. Dans le panneau de gauche, cliquez sur Filtres (![](../../assets/magento-bi-btn-filter.png)).

   ![Ajouter un filtre](../../assets/magento-bi-report-builder-filter-add.png)

1. Cliquez sur **[!UICONTROL Add Filter]**.

   Les filtres sont numérotés par ordre alphabétique, et le premier est `[A]`. Les deux premières parties du filtre sont des options de menu déroulant et la troisième est une valeur.

   ![](../../assets/magento-bi-report-builder-filter-add-a.png)

   * Cliquez sur la première partie du filtre et choisissez la colonne que vous souhaitez utiliser comme objet de l&#39;expression.

     ![Sélection de la première partie du filtre](../../assets/magento-bi-report-builder-filter-part1.png)

   * Cliquez sur la seconde partie du filtre et choisissez l&#39;opérateur.

     ![Choisissez l&#39;opérateur](../../assets/magento-bi-report-builder-filter-part2.png)

   * Dans la troisième partie du filtre, saisissez la valeur nécessaire pour terminer l’expression.

     ![Saisissez la valeur](../../assets/magento-bi-report-builder-filter-part3.png)

   * Une fois le filtre terminé, cliquez sur **[!UICONTROL Apply]**.

     Le rapport comprend désormais uniquement les clients réguliers, et le nombre d’enregistrements de clients récupérés pour le rapport a été réduit de 33 000 à 12 600.

     ![Rapport filtré](../../assets/magento-bi-report-builder-filter-report.png)<!--{: .zoom}-->

1. Dans la barre latérale, cliquez sur la perspective ( ![](../../assets/magento-bi-btn-perspective.png)).

   ![Perspective](../../assets/magento-bi-report-builder-filter-perspective.png)<!--{: .zoom}-->

1. Dans la liste des paramètres, choisissez `Cumulative`. Cliquez ensuite sur **[!UICONTROL Apply]**.

   ![Perspective cumulée](../../assets/magento-bi-report-builder-filter-perspective-cumulative.png)

   Le `Cumulative` La perspective répartit le changement au fil du temps, plutôt que d’afficher les décalages vers le haut et vers le bas pour chaque mois.

1. Saisissez un `Title` pour le rapport et cliquez sur **[!UICONTROL Save]** it as a `Chart` à votre tableau de bord.

   ![Enregistrer dans le tableau de bord](../../assets/magento-bi-report-builder-filter-perspective-cumulative-save.png)
