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

[!DNL Adobe Commerce Intelligence] Les tableaux de bord vous donnent un aperçu rapide des performances et de l’activité de vente de votre boutique en un coup d’oeil. Les tableaux de bord individuels peuvent être partagés avec d’autres utilisateurs et organisés en groupes logiques. Vous pouvez également définir différents niveaux d’autorisation pour d’autres utilisateurs.

Il est facile de créer un rapport, de l’ajouter à un tableau de bord et d’exporter les données vers Excel. Les tableaux et les rapports peuvent être redimensionnés et déplacés dans leur position sur le tableau de bord.

![Tableau de bord](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## Création de tableaux de bord {#createdash}

Les tableaux de bord sont des compartiments à thème partageables pour les analyses que vous créez dans les Reports Builder. C’est ainsi que vous pouvez encourager votre équipe à collaborer et à maintenir une source unique de vérité dans l’ensemble de votre organisation.

*Si vous êtes administrateur ou utilisateur standard*, vous pouvez créer un tableau de bord en cliquant sur le bouton `Dashboard Options` menu déroulant et choix `Create New dashboard`.

Ce à quoi ressemblent les tableaux de bord que vous créez dépend entièrement de vous. Vous pouvez organiser et redimensionner les éléments du tableau de bord de la manière qui vous convient le mieux à vos besoins et à votre workflow.

![organiser le redimensionnement de l’élément de tableau de bord](../../assets/arrange_resize_dashboard_element.gif)

### Création d’un tableau de bord

1. Dans le menu, cliquez sur **[!UICONTROL Dashboards]**.

1. Le nom du tableau de bord par défaut s’affiche dans le coin supérieur gauche de l’en-tête du tableau de bord. Cliquez sur la flèche vers le bas (![](../../assets/magento-bi-btn-down.png)) pour afficher les options disponibles.

   ![Créer un tableau de bord](../../assets/magento-bi-dashboard-create.png)

1. Cliquez sur **[!UICONTROL Create Dashboard]**. Ensuite, procédez comme suit :

   * Saisissez un `Name` pour votre tableau de bord.

   * Pour créer une `Group` pour le tableau de bord, saisissez le nom du groupe.

     Par exemple, si votre installation Commerce présente plusieurs vues de magasin, vous pouvez créer un Groupe pour chaque vue de magasin.

   * Cliquez sur **[!UICONTROL Create]**.

   ![nom du tableau de bord](../../assets/magento-bi-dashboard-create-name.png)

   * Le nom de votre nouveau tableau de bord s’affiche dans le coin supérieur gauche. Cliquez sur la flèche vers le bas (![](../../assets/magento-bi-btn-down.png)) pour afficher les options. Si vous avez créé un groupe, le nouveau tableau de bord s’affiche sous le groupe dans la liste.

### Ajouter un rapport

1. Pour ajouter un rapport, effectuez l’une des opérations suivantes :

   * Cliquez sur le bouton **[!UICONTROL Add a report]** sur la page.

   * Dans l’en-tête du tableau de bord, cliquez sur **[!UICONTROL Add Report]**.

     ![Ajouter un rapport](../../assets/magento-bi-dashboard-create-add-report.png)

1. Cliquez sur **[!UICONTROL Create Report]** pour afficher la variable **[!UICONTROL Report Builder Options]**.

   ![Options de Report Builder](../../assets/magento-bi-report-builder.png)

## Réorganiser les éléments sur un tableau de bord

* Pour redimensionner un graphique ou un rapport, faites glisser le coin inférieur droit vers la nouvelle taille.

* Pour déplacer un graphique ou un rapport, passez la souris sur le titre ou l’en-tête jusqu’à ce que le curseur se transforme en croix. Ensuite, faites-le glisser jusqu’à sa position.

## Gestion des tableaux de bord {#managedash}

Dans **[!DNL Manage Data** > **Dashboards]**, vous pouvez gérer les autorisations utilisateur des tableaux de bord que vous détenez, supprimer les tableaux de bord dont vous n’avez plus besoin et définir un tableau de bord par défaut.

### Partage de vos tableaux de bord {#sharingdash}

Pour une réelle échelle [!DNL Commerce Intelligence] dans l’ensemble de votre organisation et fournissez des informations précieuses, Adobe vous encourage à partager les tableaux de bord que vous créez avec d’autres membres de l’équipe. *Vous pouvez partager les tableaux de bord vous-même.* en cliquant sur le bouton `Share Dashboard` en haut de la page.

Lorsque vous partagez un tableau de bord, vous pouvez attribuer des autorisations à l’échelle de votre organisation OU sur une base individuelle, ce qui signifie que vous pouvez choisir qui peut afficher et modifier vos rapports.

>[!NOTE]
>
>`Read-Only` Les utilisateurs n’ont accès qu’aux tableaux de bord qui sont directement partagés avec eux ; ils ne peuvent pas rechercher ni ajouter de tableaux de bord par eux-mêmes. N&#39;oubliez pas de les garder en boucle !

### Accès aux tableaux de bord partagés {#accessshared}

*Si vous êtes un administrateur ou un utilisateur standard* et que vous souhaitez ajouter un tableau de bord partagé à votre compte, vous pouvez le faire en cliquant sur **[!UICONTROL Dashboard Options]** puis cliquez sur **[!UICONTROL Find]** dans la liste déroulante.

![trouver le tableau de bord](../../assets/find_dashboard.png)<!--{: width="1000" height="535"}-->

### Gestion des paramètres du tableau de bord

1. Dans le menu, cliquez sur **[!DNL Manage Data** > **Dashboards]**.

1. Le cas échéant, saisissez une nouvelle `Dashboard Name`.

1. Pour affecter le tableau de bord à un `Dashboard Group`, effectuez un choix dans la liste des groupes.

   **`Permissions`**

   Pour donner à tous les utilisateurs le même niveau d&#39;accès au tableau de bord, procédez comme suit :

   1. Sous **`Shared with`**, sélectionnez l’une des options suivantes :

      * `View`
      * `Edit`
      * `None`

   1. Lorsque vous êtes invité à confirmer, cliquez sur **[!UICONTROL OK]** pour mettre à jour le niveau d’autorisation de chaque utilisateur.

   1. Pour modifier le niveau d’autorisation d’une personne, recherchez l’utilisateur dans la liste et modifiez le niveau d’autorisation. La modification est enregistrée automatiquement.

   **`Default`**

   1. Pour que ce tableau de bord devienne la valeur par défaut de votre [!DNL Commerce Intelligence] compte, cliquez sur **[!UICONTROL Make Default]**.

   **`Remove`**

   1. Pour supprimer le tableau de bord, cliquez sur **[!UICONTROL Delete Dashboard]**.
