---
title: Partager des tableaux de bord avec d’autres utilisateurs
description: Découvrez comment partager des tableaux de bord avec d’autres utilisateurs.
exl-id: 6279b049-d1b2-4d40-b30b-ee8772e990f4
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Partager des tableaux de bord avec d’autres utilisateurs

Le partage de tableaux de bord est un excellent moyen de tenir votre équipe informée et d’encourager la discussion collaborative. En créant et en partageant un tableau de bord central, vous pouvez fournir à votre équipe les informations dont elle a besoin tout en gardant le contrôle. [[!DNL Adobe] recommande](../../best-practices/share-dashboard-best-practice.md){: target="_blank"} d’accorder des droits de `Edit` à un nombre restreint de personnes afin de minimiser les modifications accidentelles.

>[!NOTE]
>
>Si le tableau de bord que vous partagez contient des rapports créés avec des mesures auxquelles un utilisateur spécifique n’a pas accès, les rapports affichent un message de `Error Loading Data`. Si vous souhaitez que les données s’affichent pour un utilisateur spécifique, un [utilisateur administrateur](../../administrator/user-management/user-management.md) doit accorder l’accès à toutes les mesures utilisées dans ces rapports.

## Partage d’un tableau de bord

1. Cliquez sur **[!UICONTROL Share Dashboard]** dans la partie supérieure de l’écran.

   Une liste de tous les utilisateurs de votre compte [!DNL Commerce Intelligence] s’affiche.

1. Pour sélectionner un utilisateur ou une utilisatrice avec lequel/laquelle partager le tableau de bord, cochez la case à gauche de son nom.

   Pour sélectionner/désélectionner tous les utilisateurs, cliquez sur **[!UICONTROL Select]** et sélectionnez `Everyone` ou `None`, respectivement.

1. Les autorisations peuvent être définies utilisateur par utilisateur ou en masse.

   *Pour définir des autorisations individuelles* cliquez sur **[!UICONTROL None]** à droite du nom de l’utilisateur. Dans cette liste déroulante, sélectionnez le type d’autorisations dont l’utilisateur doit disposer.

   *Pour définir des autorisations en masse*, cliquez sur **[!UICONTROL Set Permissions]**. Dans cette liste déroulante, sélectionnez le type d’autorisations dont les utilisateurs sélectionnés doivent disposer.

   >[!NOTE]
   >
   >Vous pouvez également utiliser cette fonctionnalité pour mettre à jour les autorisations définies précédemment. Par exemple, si vous souhaitez arrêter de partager le tableau de bord avec quelqu’un, définissez ses autorisations sur `None`.

1. Pour partager le tableau de bord, cliquez sur **[!UICONTROL Save Changes]**. Les utilisateurs sélectionnés recevront un e-mail les invitant à consulter le tableau de bord.

Exemple :

![partager le tableau de bord](../../assets/Share_Dashboards.gif)
