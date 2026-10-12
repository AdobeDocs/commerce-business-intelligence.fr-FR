---
title: Modification du tableau opérationnel d’une mesure
description: Découvrez comment modifier le tableau de données qu’une mesure utilise pour effectuer son opération.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: 'https://experienceleague.adobe.com/9yJ1Zc2NLDvXYO16UvDkeWE0hD1jx0-Ne3AyFFHX5ns'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '244'
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

1. Si la nouvelle table ne contient pas de colonne correspondante, vous pouvez la **créer dans votre table de données** ou [contacter l’assistance](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies) s’il s’agit d’une colonne de calcul ou d’une dimension créée par [!DNL Commerce Intelligence]. Vous pouvez également **supprimer la dimension de la mesure**. Pour supprimer une dimension dont vous n’avez plus besoin, revenez simplement à l’éditeur de la mesure et sélectionnez les dimensions à supprimer sous `Dimensions`.

   ![&#x200B; Menu déroulant de sélection de colonne opérationnelle &#x200B;](../../assets/change-metrics-3.png)
