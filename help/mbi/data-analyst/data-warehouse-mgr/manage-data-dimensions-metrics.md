---
title: Gestion des dimensions de données
description: Découvrez ce qu’est une dimension et qu’elle peut être utilisée pour filtrer ou segmenter les graphiques en fonction d’une mesure.
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# Gestion des dimensions de données

>[!NOTE]
>
>Nécessite des [autorisations d’administrateur](../../administrator/user-management/user-management.md).

Une dimension est un champ dans le même tableau qu’une mesure qui peut être utilisé pour filtrer ou segmenter les graphiques en fonction de cette mesure. Par exemple, une mesure de chiffre d’affaires peut contenir la ville, l’État, le pays, le statut de la commande, le code coupon et d’autres types de dimensions.

## Ajout de dimensions à plusieurs mesures

Pour ajouter une ou plusieurs dimensions à plusieurs mesures à la fois :

1. Accédez à **[!UICONTROL Manage Data > Metrics]**.

1. Cliquez sur **[!UICONTROL Add Dimensions To Metric(s)]**.

1. Choisissez la table qui contient les dimensions.

1. Dans la colonne `Choose Metric(s) to Add Dimensions` , sélectionnez les mesures auxquelles vous souhaitez ajouter des dimensions. Une fois sélectionnée, la colonne `Choose Dimensions to Add` s’affiche à droite. Cochez les dimensions à ajouter à la mesure sélectionnée.

   ![Boîte de dialogue Ajouter des dimensions affichant les options de dimension disponibles](../../assets/Add_Dimensions.png)

1. Si vous souhaitez segmenter ou regrouper selon l’une des dimensions de données dans les rapports, veillez à indiquer qu’elles sont _Regroupables_.

1. Cliquez sur **[!UICONTROL Add]**.

## Supprimer des dimensions de plusieurs mesures

Pour supprimer une ou plusieurs dimensions de plusieurs mesures :

1. Accédez à **[!UICONTROL Data > Metrics]**.

1. Cliquez sur **[!UICONTROL Remove Dimensions From Metric(s)]**.

1. Choisissez la table qui contient les dimensions.

1. Sélectionnez les mesures dont vous souhaitez supprimer les dimensions à gauche, ainsi que les dimensions que vous souhaitez supprimer à droite.

1. Cliquez sur **[!UICONTROL Remove]**.

1. Si les dimensions sont utilisées dans les rapports, un avertissement s’affiche avec la liste des graphiques qui utilisent les dimensions. Cliquez sur **[!UICONTROL Delete]** pour supprimer les dimensions cochées et toutes leurs dépendances, y compris les rapports.

## Gestion des dimensions dans les mesures

**Pour ajouter une ou plusieurs dimensions dans une mesure :**

1. Accédez à **[!UICONTROL Data > Metrics]**.

1. Cliquez sur **[!UICONTROL Edit]** sur la mesure pour laquelle vous souhaitez une nouvelle dimension.

1. Dans la section `Dimensions` , utilisez la liste déroulante `Add a dimension` pour sélectionner une dimension à ajouter.

>[!NOTE]
>
>Toute dimension que vous souhaitez filtrer ou regrouper doit déjà faire l’objet d’un suivi dans [!DNL Commerce Intelligence]. Si vous ne trouvez pas la dimension souhaitée, vous devrez peut-être commencer à suivre une nouvelle colonne de données dans votre base de données via la page [Data Warehouse](../data-warehouse-mgr/tour-dwm.md).


**Pour supprimer une ou plusieurs dimensions d’une mesure :**

1. Accédez à **[!UICONTROL Manage Data > Metrics]**.

1. Cliquez sur **[!UICONTROL Edit]** sur la mesure pour laquelle vous souhaitez une nouvelle dimension.

1. Dans la section `Dimensions` , cochez la case de la colonne Supprimer en regard de la ou des dimensions à supprimer.

>[!NOTE]
>
>Même après la suppression d’une dimension, elle existe toujours en tant que colonne dans votre tableau dans votre Data Warehouse. Vous pouvez l’ajouter à nouveau à n’importe quelle mesure et créer de nouvelles mesures à l’aide de ces dimensions. Pour supprimer la colonne de données à laquelle une dimension correspond de [!DNL Commerce Intelligence], annulez simplement le suivi de la colonne de données via la page [Data Warehouse](../data-warehouse-mgr/tour-dwm.md).

## Documentation connexe

* [Bonnes pratiques relatives à la segmentation et au filtrage](../../best-practices/segment-filter.md)
