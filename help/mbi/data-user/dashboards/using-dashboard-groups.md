---
title: Utilisation des groupes de tableaux de bord
description: Découvrez comment optimiser l’organisation des tableaux de bord.
exl-id: e48b7345-62d0-4898-997e-3c3c02040ad3
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Utilisation des groupes de tableaux de bord

Les groupes de tableaux de bord permettent une meilleure organisation des tableaux de bord. Le cas d’utilisation le plus courant consiste à regrouper des tableaux de bord similaires sous le même « groupe ». Par exemple, tous les tableaux de bord liés au marketing peuvent être regroupés sous un groupe de tableaux de bord « Marketing ».

Dans le menu déroulant de sélection du tableau de bord, les groupes de tableaux de bord s’affichent par ordre alphabétique, tous les tableaux de bord situés sous « Aucun groupe » s’affichant en dernier. Les tableaux de bord appartenant au même groupe sont affichés ensemble et par ordre alphabétique dans chaque groupe.

## Partage de groupes de tableaux de bord

Les groupes de tableaux de bord ne peuvent pas être directement partagés entre les utilisateurs. Lorsqu’un tableau de bord est partagé avec des utilisateurs, le groupe de tableaux de bord sous lequel il se trouve est automatiquement créé pour ces utilisateurs s’il n’existe pas. Si le groupe de tableaux de bord existe déjà, le tableau de bord est ajouté à la liste.

Lorsque le groupe d’un tableau de bord est modifié par son propriétaire, la modification est répercutée automatiquement pour tous les utilisateurs avec lesquels le tableau de bord a été partagé. Les utilisateurs ne peuvent pas modifier le groupe de tableaux de bord pour les tableaux de bord qui ne leur appartiennent pas.

## Créer des groupes de tableaux de bord

Les groupes de tableaux de bord peuvent être créés de deux manières :

1. Lors de la création d’un tableau de bord :

   ![créer un groupe de tableaux de bord](../../assets/create-dashboard-groups-new-dashboard.png)

1. Lors de la modification du groupe d’un tableau de bord existant, à partir de la page `Manage Data > Dashboards` :

   1. Cliquez sur le tableau de bord pour lequel vous souhaitez créer le groupe.

   1. Sous `Dashboard Group (optional)`, le groupe de tableaux de bord actuel s’affiche.

   1. Pour créer un groupe, saisissez son nom, puis cliquez en dehors de la zone.

      ![créer un groupe de tableaux de bord](../../assets/create-dashboard-groups-existing-dashboard.png)

## Ajouter des tableaux de bord existants à des groupes existants

1. Sur la page `Manage Data > Dashboards`, sélectionnez le tableau de bord pour lequel le groupe doit être modifié.

1. Le texte situé sous `Dashboard Group (optional)` affiche le groupe de tableaux de bord actuel du tableau de bord.

1. Pour modifier le groupe du tableau de bord, choisissez un autre groupe dans la liste : dans ce cas, `PS`, `Campaigns`.

   ![tableau de bord de modification de groupe](../../assets/add-existing-dashboard-existing-group.png)

## Supprimer des groupes de tableaux de bord

Lorsqu’un groupe de tableaux de bord ne comporte aucun tableau de bord, il est automatiquement supprimé.
