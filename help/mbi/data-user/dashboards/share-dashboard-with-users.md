---
title: Partage des tableaux de bord avec d’autres utilisateurs
description: Découvrez comment partager des tableaux de bord avec d’autres utilisateurs.
exl-id: 6279b049-d1b2-4d40-b30b-ee8772e990f4
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Partage des tableaux de bord avec d’autres utilisateurs

Le partage de tableaux de bord est un excellent moyen de maintenir votre équipe au courant et d’encourager la discussion collaborative. En créant et en partageant un tableau de bord central, vous pouvez fournir à votre équipe les informations dont elle a besoin tout en conservant le contrôle. [[!DNL Adobe] recommande](../../best-practices/share-dashboard-best-practice.md){: target=&quot;_blank&quot;} que vous accordez `Edit` droits d’accès à quelques-uns pour minimiser les modifications accidentelles.

>[!NOTE]
>
>Si le tableau de bord que vous partagez contient des rapports créés avec des mesures auxquelles un utilisateur spécifique n’a pas accès, les rapports affichent une `Error Loading Data` message. Si vous souhaitez que les données s’affichent pour l’utilisateur spécifique, une [utilisateur admin](../../administrator/user-management/user-management.md) doit accorder l’accès à toutes les mesures utilisées dans ces rapports.

## Partage d’un tableau de bord

1. Cliquez sur **[!UICONTROL Share Dashboard]** en haut de l’écran.

   Liste de tous les utilisateurs de votre [!DNL Commerce Intelligence] s’affiche.

1. Pour sélectionner un utilisateur avec lequel partager le tableau de bord, cochez la case située à gauche de son nom.

   Pour sélectionner/désélectionner tous les utilisateurs, cliquez sur **[!UICONTROL Select]** et sélectionnez `Everyone` ou `None`, respectivement.

1. Les autorisations peuvent être définies utilisateur par utilisateur ou en masse.

   *Pour définir des autorisations individuelles*, cliquez sur **[!UICONTROL None]** à droite du nom de l’utilisateur. Dans cette liste déroulante, sélectionnez le type d’autorisations que l’utilisateur doit posséder.

   *Pour définir les autorisations en masse*, cliquez sur **[!UICONTROL Set Permissions]**. Dans cette liste déroulante, sélectionnez le type d’autorisations que les utilisateurs sélectionnés doivent posséder.

   >[!NOTE]
   >
   >Vous pouvez également utiliser cette fonction pour mettre à jour les autorisations précédemment définies. Par exemple, si vous souhaitez arrêter de partager le tableau de bord avec quelqu’un, définissez ses autorisations sur `None`.

1. Pour partager le tableau de bord, cliquez sur **[!UICONTROL Save Changes]**. Le ou les utilisateurs sélectionnés recevront un e-mail les invitant à afficher le tableau de bord.

Exemple :

![tableau de bord du partage](../../assets/Share_Dashboards.gif)
