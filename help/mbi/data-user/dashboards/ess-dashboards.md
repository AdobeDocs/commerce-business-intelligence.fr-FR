---
title: Tableaux de bord
description: Découvrez comment créer et utiliser un tableau de bord.
exl-id: a872344b-ac66-41eb-a471-5a69f8802527
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# Tableaux de bord

[!DNL Adobe Commerce Intelligence] Tableaux de bord vous donnent un aperçu rapide de la performance et de l&#39;activité de vente de votre magasin en un coup d&#39;œil. Les tableaux de bord individuels peuvent être partagés avec d’autres utilisateurs et organisés en groupes logiques. Vous pouvez également définir différents niveaux d’autorisation pour d’autres utilisateurs.

Il est facile de créer un rapport, de l’ajouter à un tableau de bord et d’exporter les données vers Excel. Les graphiques et les rapports peuvent être redimensionnés et déplacés dans le tableau de bord.

![Tableau de bord](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## Création de tableaux de bord {#createdash}

Les tableaux de bord sont des compartiments thématiques partageables pour les analyses que vous créez dans les Report Builders. C’est ainsi que vous pouvez encourager votre équipe à collaborer et à maintenir une source unique de vérité à l’échelle de votre organisation.

*Si vous êtes un administrateur ou un utilisateur standard* vous pouvez créer un tableau de bord en cliquant sur le menu déroulant `Dashboard Options` et en choisissant `Create New dashboard`.

L’aspect des tableaux de bord que vous créez dépend entièrement de vous. Vous pouvez organiser et redimensionner les éléments du tableau de bord en fonction de vos besoins et de votre workflow.

![organiser l’élément du tableau de bord de redimensionnement](../../assets/arrange_resize_dashboard_element.gif)

### Création d’un tableau de bord

1. Dans le menu, cliquez sur **[!UICONTROL Dashboards]**.

1. Le nom du tableau de bord par défaut s’affiche dans le coin supérieur gauche de l’en-tête du tableau de bord. Cliquez sur la flèche vers le bas (![](../../assets/magento-bi-btn-down.png)) pour afficher les options disponibles.

   ![Créer un tableau de bord](../../assets/magento-bi-dashboard-create.png)

1. Cliquez sur **[!UICONTROL Create Dashboard]**. Procédez ensuite comme suit :

   * Saisissez un `Name` pour votre tableau de bord.

   * Pour créer un `Group` pour le tableau de bord, saisissez le nom du groupe.

     Par exemple, si votre installation Commerce comporte plusieurs vues de magasin, vous pouvez créer un groupe pour chaque vue de magasin.

   * Cliquez sur **[!UICONTROL Create]**.

   ![ nom du tableau de bord ](../../assets/magento-bi-dashboard-create-name.png)

   * Le nom de votre nouveau tableau de bord s’affiche dans le coin supérieur gauche. Cliquez sur la flèche vers le bas (![](../../assets/magento-bi-btn-down.png)) pour afficher les options. Si vous avez créé un groupe, le nouveau tableau de bord s’affiche sous le groupe dans la liste.

### Ajout d’un rapport

1. Pour ajouter un rapport, effectuez l’une des opérations suivantes :

   * Cliquez sur l’invite de **[!UICONTROL Add a report]** sur la page.

   * Dans l’en-tête du tableau de bord, cliquez sur **[!UICONTROL Add Report]**.

     ![Ajouter rapport](../../assets/magento-bi-dashboard-create-add-report.png)

1. Cliquez sur **[!UICONTROL Create Report]** pour afficher la **[!UICONTROL Report Builder Options]**.

   ![Options Report Builder](../../assets/magento-bi-report-builder.png)

## Organiser les éléments sur un tableau de bord

* Pour redimensionner un graphique ou un rapport, faites glisser le coin inférieur droit vers la nouvelle taille.

* Pour déplacer un graphique ou un rapport, passez la souris sur le titre ou l’en-tête jusqu’à ce que le curseur se transforme en croix. Puis, faites-le glisser jusqu’à ce qu’il soit en position.

## Gestion des tableaux de bord {#managedash}

Dans **[!DNL Manage Data** > **Dashboards]**, vous pouvez gérer les autorisations d’utilisateur pour les tableaux de bord que vous possédez, supprimer les tableaux de bord dont vous n’avez plus besoin et définir un tableau de bord par défaut.

### Partage de tableaux de bord {#sharingdash}

Pour adapter véritablement les [!DNL Commerce Intelligence] à l’échelle de votre entreprise et fournir des informations précieuses, Adobe vous encourage à partager les tableaux de bord que vous créez avec d’autres membres de l’équipe. *Vous pouvez partager les tableaux de bord que vous possédez* en cliquant sur l’option `Share Dashboard` en haut de la page.

Lorsque vous partagez un tableau de bord, vous pouvez attribuer des autorisations à l’échelle de votre organisation OU sur une base individuelle, ce qui signifie que vous pouvez décider qui peut afficher et modifier vos rapports.

>[!NOTE]
>
>Les utilisateurs `Read-Only` n’ont accès qu’aux tableaux de bord qui sont directement partagés avec eux. Ils ne peuvent pas rechercher et ajouter des tableaux de bord eux-mêmes. N&#39;oubliez pas de les tenir au courant !

### Accès aux tableaux de bord partagés {#accessshared}

*Si vous êtes un utilisateur administrateur ou standard* et que vous souhaitez ajouter un tableau de bord partagé à votre compte, vous pouvez le faire en cliquant sur **[!UICONTROL Dashboard Options]** puis sur **[!UICONTROL Find]** dans la liste déroulante.

![rechercher tableau de bord](../../assets/find_dashboard.png)<!--{: width="1000" height="535"}-->

### Gérer les paramètres du tableau de bord

1. Dans le menu, cliquez sur **[!DNL Manage Data** > **Dashboards]**.

1. Le cas échéant, saisissez une nouvelle `Dashboard Name`.

1. Pour affecter le tableau de bord à un `Dashboard Group` spécifique, faites votre choix dans la liste des groupes.

   **`Permissions`**

   Pour donner à tous les utilisateurs le même niveau d’accès au tableau de bord, procédez comme suit :

   1. Sous **`Shared with`**, choisissez l’une des options suivantes :

      * `View`
      * `Edit`
      * `None`

   1. Lorsque vous êtes invité à confirmer, cliquez sur **[!UICONTROL OK]** pour mettre à jour le niveau des autorisations pour chaque utilisateur.

   1. Pour modifier le niveau d’autorisation d’une personne, recherchez l’utilisateur dans la liste et modifiez le niveau d’autorisation. La modification est automatiquement enregistrée.

   **`Default`**

   1. Pour que ce tableau de bord soit le tableau de bord par défaut de votre compte [!DNL Commerce Intelligence], cliquez sur **[!UICONTROL Make Default]**.

   **`Remove`**

   1. Pour supprimer le tableau de bord, cliquez sur **[!UICONTROL Delete Dashboard]**.
