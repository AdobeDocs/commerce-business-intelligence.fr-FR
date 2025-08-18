---
title: Gérer les tableaux de bord
description: Découvrez comment gérer les autorisations d’utilisateur pour les tableaux de bord que vous possédez, supprimer les tableaux de bord dont vous n’avez plus besoin et définir un tableau de bord par défaut.
exl-id: 32c21093-2a7d-4d8e-afc0-19bd702f9b36
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Gestion d’un tableau de bord

>[!NOTE]
>
>Nécessite des [autorisations d’administrateur](../../administrator/user-management/user-management.md).

Dans **[!DNL Manage Data** > **Dashboards]**, vous pouvez gérer les autorisations d’utilisateur pour les tableaux de bord que vous possédez, supprimer les tableaux de bord dont vous n’avez plus besoin et définir un tableau de bord par défaut. Cette rubrique aborde les sujets suivants :

1. [Renommer des tableaux de bord](#rename)

1. [Gestion des autorisations relatives aux tableaux de bord](#userperm)

1. [Modification du tableau de bord par défaut](#default)

1. [Suppression de tableaux de bord](#delete)

## Renommer un tableau de bord {#rename}

Pour renommer un tableau de bord :

1. Cliquez sur le nom du tableau de bord à modifier.

2. Saisissez le nouveau nom dans le champ `Dashboard Name` .

## Gérer les autorisations utilisateur {#userperm}

Il existe trois niveaux d’accès dans [!DNL Commerce Intelligence] pour les tableaux de bord : `View`, `Edit` et `None`.

* `View` permet aux utilisateurs sélectionnés d’afficher le tableau de bord, mais pas de le modifier. Les utilisateurs peuvent également redimensionner les graphiques, exporter des données et copier les graphiques sur leurs propres tableaux de bord à l’aide de la fonction Enregistrer sous s’ils disposent des autorisations standard ou d’administration.

* `Edit` permet aux utilisateurs sélectionnés de modifier et d’enregistrer des graphiques dans ce tableau de bord s’ils disposent des autorisations Standard ou Administrateur. En outre, les utilisateurs disposant d’autorisations de modification peuvent également partager des tableaux de bord avec d’autres utilisateurs.

* `None` signifie que les utilisateurs sélectionnés ne peuvent pas afficher ni modifier ce tableau de bord.

Les autorisations utilisateur peuvent être modifiées de deux manières : pour tous les utilisateurs ou pour un utilisateur individuel.

1. *Pour modifier les autorisations de tous les utilisateurs* utilisez le menu déroulant en regard du libellé `Set all users' permissions to…`.

1. *Pour modifier les autorisations d’un utilisateur individuel* utilisez le menu déroulant en regard du nom de l’utilisateur pour définir le niveau d’accès souhaité.

## Modifier le tableau de bord par défaut {#default}

Pour modifier le tableau de bord par défaut du compte :

1. Cliquez sur le nom du tableau de bord que vous souhaitez utiliser par défaut.

1. Cliquez sur **[!UICONTROL Make Default]**.

## Supprimer tableaux de bord {#delete}

Pour supprimer un tableau de bord :

1. Cliquez sur le nom du tableau de bord à supprimer.

1. Cliquez sur **[!UICONTROL Delete Dashboard]**.
