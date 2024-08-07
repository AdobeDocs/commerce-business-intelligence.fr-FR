---
title: Limitation de l’accès aux mesures
description: Découvrez comment utiliser l’accès aux mesures et les restrictions.
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Gestion des utilisateurs des mesures

Outre la définition des niveaux d’autorisation utilisateur, vous pouvez également restreindre l’accès aux mesures utilisateur par utilisateur. Par exemple, si vous souhaitez que votre service de comptabilité ait accès aux mesures liées aux recettes, mais pas aux mesures d’acquisition d’utilisateurs, vous pouvez restreindre l’accès à ces mesures.

Dans de tels cas, Adobe recommande de définir le compte de cet utilisateur sur **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** des autorisations doivent être accordées aux utilisateurs qui n’ont pas besoin de créer ou modifier des mesures, des colonnes calculées, des intégrations ou des utilisateurs, mais qui n’ont pas besoin d’accéder aux données dans le Data Warehouse. Si vous souhaitez restreindre entièrement l’accès aux données, utilisez plutôt les autorisations **[!UICONTROL Read Only]** .

Après avoir défini le niveau d’autorisation, vous pouvez sélectionner les mesures auxquelles un utilisateur **[!UICONTROL Standard]** peut accéder en procédant comme suit :

1. Accédez à **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. Sélectionnez le compte d’utilisateur de votre choix.
1. L’onglet **[!UICONTROL Metrics]** affiche une liste des mesures disponibles. Vérifiez les mesures auxquelles l’utilisateur doit avoir accès et désélectionnez celles auxquelles il ne doit pas avoir accès.
1. [!DNL Adobe Commerce Intelligence] enregistre automatiquement les modifications. Si la modification est réussie, [!DNL Commerce Intelligence] affiche **[!UICONTROL Saved!]** en haut de la page.

>[!NOTE]
>
>Tous les utilisateurs disposant d’autorisations **[!UICONTROL Standard]** peuvent accéder à toutes les données du Data Warehouse via l’exportation de données en plus de toutes les mesures de [!DNL Google Analytics].

Vous pouvez également restreindre l&#39;accès à une mesure en la modifiant et en **[!UICONTROL Standard]** en sélectionnant des utilisateurs dans la section **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)**.

>[!NOTE]
>
>Si vous dupliquez une mesure, [!DNL Commerce Intelligence] copie les autorisations utilisateur définies dans la mesure d’origine.
