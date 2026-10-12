---
title: Limiter l’accès aux mesures
description: Découvrez comment utiliser l’accès aux mesures et les restrictions.
role: Admin, User
feature: User Management
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b6935462-7263-4ced-a703-60de6a5aeb2d
    internal-label: Administration
subfeature_v2:
  - id: a763c1a2-1d0a-40d7-9617-8139636fd12e
    internal-label: Access management
  - id: d971c7be-3e54-4af9-807c-8d1f9f7b22df
    internal-label: User management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%
---

# Gérer les utilisateurs des mesures

Outre la définition de niveaux d’autorisation utilisateur, vous pouvez également restreindre l’accès aux mesures utilisateur par utilisateur. Par exemple, si vous souhaitez que votre service comptable ait accès aux mesures liées aux recettes, mais pas aux mesures d’acquisition d’utilisateurs, vous pouvez restreindre l’accès à ces mesures.

Dans de tels cas, Adobe recommande de définir le compte de cet utilisateur sur **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** autorisations doivent être accordées aux utilisateurs qui n’ont pas besoin de créer ou de modifier des mesures, des colonnes calculées, des intégrations ou des utilisateurs, mais qui ont besoin d’accéder aux données dans Data Warehouse. Si vous souhaitez restreindre entièrement l’accès aux données, utilisez plutôt les autorisations **[!UICONTROL Read Only]** .

Une fois le niveau d’autorisation défini, vous pouvez sélectionner les mesures auxquelles un utilisateur **[!UICONTROL Standard]** peut accéder en procédant comme suit :

1. Accédez à **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. Sélectionnez le compte utilisateur de votre choix.
1. L’onglet **[!UICONTROL Metrics]** affiche une liste des mesures disponibles. Cochez les mesures auxquelles vous souhaitez que l’utilisateur ait accès et désélectionnez celles auxquelles il ne devrait pas avoir accès.
1. [!DNL Adobe Commerce Intelligence] enregistre automatiquement les modifications. Si la modification est réussie, [!DNL Commerce Intelligence] affiche **[!UICONTROL Saved!]** en haut de la page.

>[!NOTE]
>
>Tous les utilisateurs disposant d’autorisations **[!UICONTROL Standard]** peuvent accéder à toutes les données dans Data Warehouse via l’exportation de données, en plus de toutes les mesures issues de [!DNL Google Analytics].

Vous pouvez également restreindre l’accès à une mesure en la modifiant et en sélectionnant **[!UICONTROL Standard]** utilisateurs dans la section **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** .

>[!NOTE]
>
>Si vous dupliquez une mesure, [!DNL Commerce Intelligence] copie les autorisations utilisateur définies dans la mesure d’origine.
