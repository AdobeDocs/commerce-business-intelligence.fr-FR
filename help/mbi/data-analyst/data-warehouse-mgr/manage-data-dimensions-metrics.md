---
title: Gestion des dimensions de données
description: Découvrez ce qu’est une dimension et l’utiliser pour filtrer ou segmenter les graphiques en fonction d’une mesure.
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# Gestion des dimensions de données

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../administrator/user-management/user-management.md).

Une dimension est un champ du même tableau qu’une mesure qui peut être utilisée pour filtrer ou segmenter les graphiques en fonction de cette mesure. Par exemple, une mesure de recettes peut contenir la ville, l’état, le pays, l’état de la commande, le code de bon et d’autres types de dimensions.

## Ajout de dimensions à plusieurs mesures

Pour ajouter une ou plusieurs dimensions à plusieurs mesures à la fois :

1. Accédez à **[!UICONTROL Manage Data > Metrics]**.

1. Cliquez sur **[!UICONTROL Add Dimensions To Metric(s)]**.

1. Sélectionnez la table contenant les dimensions.

1. Dans le `Choose Metric(s) to Add Dimensions` , sélectionnez les mesures auxquelles vous souhaitez ajouter des dimensions. Une fois la sélection effectuée, la fonction `Choose Dimensions to Add` s’affiche à droite. Cochez les dimensions que vous souhaitez ajouter à la mesure sélectionnée.

   ![](../../assets/Add_Dimensions.png)

1. Si vous souhaitez segmenter ou regrouper en fonction de l’une des dimensions de données des rapports, veillez à indiquer qu’elles sont _Groupable_.

1. Cliquez sur **[!UICONTROL Add]**.

## Suppression de dimensions de plusieurs mesures

Pour supprimer une ou plusieurs dimensions de plusieurs mesures :

1. Accédez à **[!UICONTROL Data > Metrics]**.

1. Cliquez sur **[!UICONTROL Remove Dimensions From Metric(s)]**.

1. Sélectionnez la table contenant les dimensions.

1. Sélectionnez les mesures dont vous souhaitez supprimer les dimensions à gauche, ainsi que les dimensions que vous souhaitez supprimer à droite.

1. Cliquez sur **[!UICONTROL Remove]**.

1. Si les dimensions sont utilisées dans les rapports, un avertissement s’affiche avec la liste des graphiques qui utilisent les dimensions. Cliquez sur **[!UICONTROL Delete]** pour supprimer les dimensions vérifiées et toutes leurs dépendances, y compris les rapports.

## Gestion des dimensions dans les mesures

**Pour ajouter une ou plusieurs dimensions à une mesure :**

1. Accédez à **[!UICONTROL Data > Metrics]**.

1. Cliquez sur **[!UICONTROL Edit]** sur la mesure, vous souhaitez une nouvelle dimension.

1. Dans le `Dimensions` , utilisez la fonction `Add a dimension` pour sélectionner une dimension à ajouter.

>[!NOTE]
>
>Toute dimension dont vous souhaitez filtrer ou regrouper les éléments doit déjà faire l’objet d’un suivi dans [!DNL Commerce Intelligence]. Si vous ne trouvez pas la dimension souhaitée, vous devrez peut-être commencer le suivi d’une nouvelle colonne de données dans votre base de données via la variable [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) page.


**Pour supprimer une ou plusieurs dimensions d’une mesure :**

1. Accédez à **[!UICONTROL Manage Data > Metrics]**.

1. Cliquez sur **[!UICONTROL Edit]** sur la mesure, vous souhaitez une nouvelle dimension.

1. Sous , `Dimensions` , cochez la case dans la colonne de suppression en regard de la ou des dimensions que vous souhaitez supprimer.

>[!NOTE]
>
>Même après la suppression d’une dimension, elle existe toujours sous la forme d’une colonne sur votre table dans votre Data Warehouse. Vous pouvez la réajouter à n’importe quelle mesure et créer de nouvelles mesures à l’aide de ces dimensions. Pour supprimer la colonne de données à partir de laquelle correspond une dimension [!DNL Commerce Intelligence], il vous suffit d’annuler le suivi de la colonne de données via l’événement [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) page.

## Documentation connexe

* [Bonnes pratiques relatives à la segmentation et au filtrage](../../best-practices/segment-filter.md)
