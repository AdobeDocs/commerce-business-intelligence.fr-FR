---
title: Modification du tableau opérationnel d’une mesure
description: Découvrez comment modifier le tableau de données qu’une mesure utilise pour effectuer son opération.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Modification du tableau opérationnel d’une mesure

Dans certains cas, vous pouvez décider de modifier le tableau de données qu’une mesure utilise pour effectuer son opération. Par exemple, si vous disposez d’une nouvelle table d’utilisateurs, vous souhaitez migrer les mesures liées aux utilisateurs depuis la table `Users\_Old` pour utiliser la table `Users\_New` à la place.

1. Accédez à **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. Cliquez sur **[!UICONTROL Edit]** en regard de la mesure pour laquelle vous souhaitez changer de tableau de `operational`.
1. Dans l’éditeur, cliquez sur **[!UICONTROL Change]**.

   ![Page de définition de la mesure affichant le paramètre du tableau opérationnel](../../assets/change-metrics-1.png)
1. Sélectionnez la nouvelle table sur laquelle vous souhaitez baser cette mesure.
1. Faire correspondre les dimensions de données existantes aux dimensions correspondantes dans le nouveau tableau. Par exemple, si vous aviez une colonne intitulée `User's registration date`, il vous suffit de sélectionner la colonne qui, dans la nouvelle table, enregistre les mêmes données de date. (Voir l’étape suivante si le nouveau tableau ne comporte pas de colonnes correspondantes)

   ![Liste déroulante de sélection de tableau présentant les tableaux disponibles](../../assets/change-metrics-2.png)

1. Si la nouvelle table ne contient pas de colonne correspondante, vous pouvez la **créer dans votre table de données** ou [contacter l’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) s’il s’agit d’une colonne de calcul ou d’une dimension créée par [!DNL Commerce Intelligence]. Vous pouvez également **supprimer la dimension de la mesure**. Pour supprimer une dimension dont vous n’avez plus besoin, revenez simplement à l’éditeur de la mesure et sélectionnez les dimensions à supprimer sous `Dimensions`.

   ![&#x200B; Menu déroulant de sélection de colonne opérationnelle &#x200B;](../../assets/change-metrics-3.png)
