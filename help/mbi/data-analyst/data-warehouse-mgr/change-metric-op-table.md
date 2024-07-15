---
title: Modification du tableau opérationnel d’une mesure
description: Découvrez comment modifier le tableau de données utilisé par une mesure pour effectuer son fonctionnement.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# Modification du tableau opérationnel d’une mesure

Dans certains cas, vous pouvez décider de modifier le tableau de données utilisé par une mesure pour effectuer son opération. Par exemple, si vous disposez d’une nouvelle table d’utilisateurs, vous souhaitez migrer les mesures liées aux utilisateurs de la table `Users\_Old` pour utiliser la table `Users\_New` à la place.

1. Accédez à **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. Cliquez sur **[!UICONTROL Edit]** en regard de la mesure pour laquelle vous souhaitez changer de table `operational`.
1. Dans l’éditeur, cliquez sur **[!UICONTROL Change]**.

   ![](../../assets/change-metrics-1.png)
1. Sélectionnez le nouveau tableau sur lequel vous souhaitez baser cette mesure.
1. Faire correspondre les dimensions de données existantes à celles correspondantes dans le nouveau tableau. Par exemple, si vous aviez une colonne appelée `User's registration date`, sélectionnez simplement la colonne de la nouvelle table qui enregistre les mêmes données de date. (Voir l’étape suivante si le nouveau tableau ne contient pas de colonnes correspondantes)

   ![](../../assets/change-metrics-2.png)

1. Si la nouvelle table ne contient pas de colonne correspondante, vous pouvez **la créer dans votre table de données** ou [contacter l&#39;assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) s&#39;il s&#39;agit d&#39;une colonne de calcul ou d&#39;une dimension effectuée par [!DNL Commerce Intelligence]. Vous pouvez également **supprimer la dimension de la mesure**. Pour supprimer une dimension dont vous n’avez plus besoin, revenez simplement à l’éditeur de mesures et sélectionnez les dimensions à supprimer sous `Dimensions`.

   ![](../../assets/change-metrics-3.png)
