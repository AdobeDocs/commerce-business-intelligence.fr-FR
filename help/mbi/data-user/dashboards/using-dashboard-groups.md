---
title: Utilisation des groupes de tableaux de bord
description: Découvrez comment permettre une meilleure organisation des tableaux de bord.
exl-id: e48b7345-62d0-4898-997e-3c3c02040ad3
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Utilisation des groupes de tableaux de bord

Les groupes de tableaux de bord permettent une meilleure organisation des tableaux de bord. Le cas d’utilisation le plus courant consiste à regrouper des tableaux de bord similaires sous le même &quot;groupe&quot;. Par exemple, tous les tableaux de bord liés au marketing peuvent être regroupés sous un groupe de tableau de bord &quot;Marketing&quot;.

Dans la liste déroulante de sélection des tableaux de bord, les groupes de tableaux de bord s’affichent par ordre alphabétique, tous les tableaux de bord situés sous &quot;Aucun groupe&quot; s’affichant en dernier. Les tableaux de bord situés sous le même groupe s’affichent ensemble et par ordre alphabétique dans chaque groupe.

## Partage de groupes de tableaux de bord

Les groupes de tableaux de bord ne peuvent pas être partagés directement entre les utilisateurs. Lorsqu’un tableau de bord est partagé avec des utilisateurs, le groupe sous lequel il se trouve est automatiquement créé pour ces utilisateurs s’il n’existe pas. Si le groupe de tableaux de bord existe, il est ajouté à la liste.

Lorsqu’un groupe de tableau de bord est modifié par son propriétaire, la modification est répercutée automatiquement sur tous les utilisateurs avec lesquels le tableau de bord a été partagé. Les utilisateurs ne peuvent pas modifier le groupe de tableaux de bord des tableaux de bord qu’ils ne possèdent pas.

## Création de groupes de tableaux de bord

Les groupes de tableaux de bord peuvent être créés de deux façons :

1. Lors de la création d’un tableau de bord :

   ![créer un groupe de tableau de bord](../../assets/create-dashboard-groups-new-dashboard.png)

1. Lors de la modification du groupe d’un tableau de bord existant, sur la page `Manage Data > Dashboards` :

   1. Cliquez sur le tableau de bord pour lequel vous souhaitez créer le groupe.

   1. Sous `Dashboard Group (optional)`, le groupe de tableau de bord actuel s’affiche.

   1. Pour créer un groupe, saisissez le nom du nouveau groupe, puis cliquez en dehors de la zone.

      ![créer un groupe de tableau de bord](../../assets/create-dashboard-groups-existing-dashboard.png)

## Ajout de tableaux de bord existants à des groupes existants

1. Sur la page `Manage Data > Dashboards`, sélectionnez le tableau de bord pour lequel modifier le groupe.

1. Le texte sous `Dashboard Group (optional)` affiche le groupe de tableau de bord actuel du tableau de bord.

1. Pour modifier le groupe du tableau de bord, choisissez un autre groupe dans la liste, ici `PS`, `Campaigns`.

   ![ Modifier le tableau de bord du groupe ](../../assets/add-existing-dashboard-existing-group.png)

## Suppression de groupes de tableaux de bord

Lorsqu’un groupe de tableau de bord ne comporte aucun tableau de bord, il est automatiquement supprimé.
