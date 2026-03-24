---
title: Modification du tableau opérationnel d’une mesure
description: Découvrez comment modifier le tableau de données qu’une mesure utilise pour effectuer son opération.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/9yJ1Zc2NLDvXYO16UvDkeWE0hD1jx0-Ne3AyFFHX5ns
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 231
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

   ![ Menu déroulant de sélection de colonne opérationnelle ](../../assets/change-metrics-3.png)
