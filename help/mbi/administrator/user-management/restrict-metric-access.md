---
title: Limitation de l’accès aux mesures
description: Découvrez comment utiliser l’accès aux mesures et les restrictions.
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Gestion des utilisateurs des mesures

Outre la définition des niveaux d’autorisation utilisateur, vous pouvez également restreindre l’accès aux mesures utilisateur par utilisateur. Par exemple, si vous souhaitez que votre service de comptabilité ait accès aux mesures liées aux recettes, mais pas aux mesures d’acquisition d’utilisateurs, vous pouvez restreindre l’accès à ces mesures.

Dans de tels cas, Adobe recommande de définir le compte de cet utilisateur sur **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** les autorisations doivent être accordées aux utilisateurs qui n’ont pas besoin de créer ou modifier des mesures, des colonnes calculées, des intégrations ou des utilisateurs, mais qui n’ont pas besoin d’accéder aux données du Data Warehouse. Si vous souhaitez restreindre entièrement l’accès aux données, utilisez la variable **[!UICONTROL Read Only]** autorisations à la place.

Après avoir défini le niveau d’autorisation, vous pouvez sélectionner les mesures sous la forme **[!UICONTROL Standard]** L’utilisateur peut y accéder en procédant comme suit :

1. Accédez à **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. Sélectionnez le compte d’utilisateur de votre choix.
1. Le **[!UICONTROL Metrics]** affiche une liste des mesures disponibles. Vérifiez les mesures auxquelles vous souhaitez que l’utilisateur ait accès. désélectionnez celles auxquelles l’utilisateur ne doit pas avoir accès.
1. [!DNL MBI] enregistre automatiquement les modifications. Si la modification est réussie, [!DNL MBI] affiche **[!UICONTROL Saved!]** en haut de la page.

>[!NOTE]
>
>Tous les utilisateurs avec **[!UICONTROL Standard]** Les autorisations peuvent accéder à toutes les données du Data Warehouse par l’intermédiaire de l’exportation de données en plus de toutes les mesures issues de [!DNL Google Analytics].

Vous pouvez également restreindre l’accès à une mesure en la modifiant et en **[!UICONTROL Standard]** en sélectionnant des utilisateurs dans le **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** .

>[!NOTE]
>
>Si vous dupliquez une mesure, [!DNL MBI] copie les autorisations utilisateur définies dans la mesure d’origine.
