---
title: Connexion à Adobe Analytics
description: Découvrez comment rassembler la mise au point de parcours client de bout en bout de [!DNL Adobe Analytics] et la mise au point de commerce électronique sur laquelle vous vous fiez à partir de [!DNL Commerce Intelligence].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Connexion [!DNL Adobe Analytics]

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

L&#39;intégration [!DNL Adobe Analytics] pour [!DNL Adobe Commerce Intelligence] vous permet de rassembler la concentration de parcours client de bout en bout de [!DNL Adobe Analytics] et la concentration eCommerce sur laquelle vous vous fiez à partir de [!DNL Commerce Intelligence]. Vous obtenez ainsi une vue d’ensemble complète des performances générales de votre magasin.

Plus précisément, l’intégration [!DNL Adobe Analytics] pour [!DNL Commerce Intelligence] permet aux commerçants de commencer à combiner leurs jeux de données [!DNL Adobe Commerce] et [!DNL Adobe Analytics].

- Créez une connexion à partir de votre compte [!DNL Adobe Analytics] existant vers [!DNL Commerce Intelligence].

- Sélectionnez jusqu’à 25 mesures et dimensions dans une suite de rapports pour effectuer une réplication dans votre Data Warehouse.

- Utilisez toutes les fonctionnalités [!DNL Commerce Intelligence] standard pour transformer, rejoindre et générer des rapports sur les données [!DNL Adobe Analytics] répliquées.

## Conditions préalables à la connexion

Les informations suivantes sont nécessaires pour se connecter :

- [!DNL Adobe Analytics] identifiants de connexion

- `Name` et/ou `ID` de la suite de rapports [!DNL Adobe Analytics] pour répliquer les données de

- Liste des mesures et des dimensions à répliquer dans [!DNL Commerce Intelligence]

## Connexion de l’intégration [!DNL Adobe Analytics] pour [!DNL Commerce Intelligence]

1. Accédez à la page `Integrations` sous **[!DNL Manage Data** > **Integrations]**.

1. Cliquez sur **[!UICONTROL Add an Integration]**.

1. Cliquez sur l&#39;icône **[!UICONTROL Adobe Analytics]** pour accéder à la page qui vous permet d&#39;autoriser la connexion à votre compte [!DNL Adobe Analytics].

1. Cliquez sur **[!UICONTROL Authorize with Adobe Analytics]**.

1. Saisissez vos informations d’identification [!DNL Adobe Analytics]. Après une autorisation réussie, vous êtes redirigé vers [!DNL Commerce Intelligence].

1. Une liste des suites de rapports disponibles s’affiche. Sélectionnez la suite de rapports à partir de laquelle vous souhaitez importer les données, puis cliquez sur **[!UICONTROL Continue]**.

1. L’écran de sélection des mesures et des dimensions s’affiche. Sélectionnez au moins une mesure et au moins une dimension, pour un total combiné de 25 mesures et dimensions. Recherchez par nom ou faites défiler l’écran pour trouver vos composants, puis cochez les cases à cocher à sélectionner. Cliquez sur **[!UICONTROL Continue]**.

1. La suite de rapports sélectionnée s’affiche dans un tableau. Cliquez sur **[!UICONTROL Save]** pour confirmer votre sélection.

1. Informez l&#39; [!DNL Commerce Intelligence] [équipe d&#39;assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) que votre intégration est autorisée et qu&#39;ils exécutent le processus de connexion initial pour vous.

Une fois le processus de connexion initial exécuté, votre table sera disponible dans la page du Data Warehouse, sous l’onglet `All Tables`. Sélectionnez les colonnes que vous souhaitez répliquer et les données apparaîtront après la prochaine mise à jour complète.
