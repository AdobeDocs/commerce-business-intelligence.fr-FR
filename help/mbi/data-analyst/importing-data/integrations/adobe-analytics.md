---
title: Connexion à Adobe Analytics
description: Découvrez comment rassembler le point de mire du parcours client de bout en bout de la [!DNL Adobe Analytics] et l’accent eCommerce sur lequel vous vous fiez [!DNL MBI].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Connexion [!DNL Adobe Analytics]

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

Le [!DNL Adobe Analytics] intégration pour [!DNL MBI] vous permet de rassembler le point de mire du parcours client de bout en bout de la [!DNL Adobe Analytics] et l’accent eCommerce sur lequel vous vous fiez [!DNL MBI], pour obtenir une vue d’ensemble plus complète des performances générales de votre boutique.

Plus précisément, la [!DNL Adobe Analytics] intégration pour [!DNL MBI] fournit des fonctionnalités permettant aux commerçants de commencer à combiner leurs jeux de données Commerce et Analytics.
- Créer une connexion à partir de votre [!DNL Adobe Analytics] compte dans [!DNL MBI].
- Sélectionnez jusqu’à 25 mesures et dimensions d’une suite de rapports à répliquer dans votre [!DNL MBI] entrepôt de données.
- Utiliser toutes les normes [!DNL MBI] fonctionnalité permettant de transformer, de rejoindre et de créer des rapports sur les produits répliqués. [!DNL Adobe Analytics] data.

## Conditions préalables à la connexion

Les informations suivantes sont nécessaires pour se connecter :
- [!DNL Adobe Analytics] informations de connexion
- `Name` et/ou `ID` de [!DNL Adobe Analytics] suite de rapports à partir de laquelle répliquer les données
- Liste des mesures et des dimensions à répliquer dans [!DNL MBI]

## Connexion de la variable [!DNL Adobe Analytics] Intégration pour MBI

1. Accédez au `Integrations` page sous **[!DNL Manage Data** > **Integrations]**.
1. Cliquez sur **[!UICONTROL Add an Integration]**, situé sur le côté droit de l’écran.
1. Cliquez sur le bouton **[!UICONTROL Adobe Analytics]** pour accéder à la page qui vous permet d’autoriser votre [!DNL Adobe Analytics] connexion au compte.
1. Cliquez sur **[!UICONTROL Authorize with Adobe Analytics]**.
1. Saisissez votre [!DNL Adobe Analytics] informations d’identification. Après une autorisation réussie, vous êtes redirigé vers [!DNL MBI].
1. Une liste des suites de rapports disponibles s’affiche. Sélectionnez la suite de rapports à partir de laquelle vous souhaitez importer les données, puis cliquez sur **[!UICONTROL Continue]**.
1. L’écran de sélection des mesures et des dimensions s’affiche. Sélectionnez au moins une mesure et au moins une dimension, pour un total combiné de 25 mesures et dimensions. Recherchez par nom ou faites défiler l’écran pour trouver vos composants, puis cochez les cases à cocher à sélectionner. Cliquez sur **[!UICONTROL Continue]**.
1. La suite de rapports sélectionnée s’affiche dans un tableau. Cliquez sur **[!UICONTROL Save]** pour confirmer votre sélection.
1. Informer le [!DNL MBI] L’équipe d’assistance doit avoir l’autorisation de votre intégration et elle doit exécuter le processus de connexion initial pour vous.

Une fois le processus de connexion initial exécuté, votre tableau sera disponible dans la page du Data Warehouse, sous la `All Tables` . Sélectionnez les colonnes que vous souhaitez répliquer et les données apparaîtront après la prochaine mise à jour complète.
