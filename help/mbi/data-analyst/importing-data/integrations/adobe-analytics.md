---
title: Connecter Adobe Analytics
description: Apprenez à rassembler l’accent mis sur le parcours client de bout en bout  [!DNL Adobe Analytics]  et l’accent mis sur l’e-commerce sur lequel vous vous appuyez [!DNL Commerce Intelligence].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/KkiKySM2q8ewqhQ1kdUjLuTM4iOpzrZb5Ok-UvBBpJE
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 312
ht-degree: 0%

---

# Connexion [!DNL Adobe Analytics]

>[!NOTE]
>
>Nécessite des [autorisations d’administrateur](../../../administrator/user-management/user-management.md).

Logo ![](../../../assets/adobe-analytic-slogo.png)

L’intégration [!DNL Adobe Analytics] d’[!DNL Adobe Commerce Intelligence] vous permet de rassembler l’objectif de parcours client de bout en bout de [!DNL Adobe Analytics] et l’objectif eCommerce sur lequel vous vous appuyez à partir d’[!DNL Commerce Intelligence]. Vous obtenez ainsi une vue d&#39;ensemble de la performance globale de votre magasin.

Plus précisément, l’intégration [!DNL Adobe Analytics] pour [!DNL Commerce Intelligence] permet aux commerçants de commencer à combiner leurs jeux de données [!DNL Adobe Commerce] et [!DNL Adobe Analytics].

- Créez une connexion à partir de votre compte [!DNL Adobe Analytics] existant dans [!DNL Commerce Intelligence].

- Sélectionnez jusqu’à 25 mesures et dimensions dans une suite de rapports à répliquer dans votre Data Warehouse.

- Utilisez toutes les fonctionnalités [!DNL Commerce Intelligence] standard pour transformer, joindre et générer des rapports sur les données [!DNL Adobe Analytics] répliquées.

## Conditions préalables à la connexion

Les informations de connexion suivantes sont nécessaires :

- [!DNL Adobe Analytics] les informations de connexion

- `Name` et/ou `ID` de [!DNL Adobe Analytics] suite de rapports à partir de laquelle répliquer les données

- Liste des mesures et dimensions à répliquer dans [!DNL Commerce Intelligence]

## Connexion de l’intégration [!DNL Adobe Analytics] pour [!DNL Commerce Intelligence]

1. Accédez à la page `Integrations` sous **[!DNL Manage Data** > **Integrations]**.

1. Cliquez sur **[!UICONTROL Add an Integration]**.

1. Cliquez sur l’icône **[!UICONTROL Adobe Analytics]** pour accéder à la page qui vous permet d’autoriser la connexion à votre compte [!DNL Adobe Analytics].

1. Cliquez sur **[!UICONTROL Authorize with Adobe Analytics]**.

1. Saisissez vos informations d’identification [!DNL Adobe Analytics]. Une fois l’autorisation réussie, vous êtes redirigé vers [!DNL Commerce Intelligence].

1. Une liste des suites de rapports disponibles s’affiche. Sélectionnez la suite de rapports à partir de laquelle vous souhaitez importer les données, puis cliquez sur **[!UICONTROL Continue]**.

1. L’écran de sélection des mesures et des dimensions s’affiche. Sélectionnez au moins une mesure et au moins une dimension, jusqu’à un total combiné de 25 mesures et dimensions. Recherchez par nom ou faites défiler l’écran pour trouver vos composants, puis cochez les cases à cocher pour les sélectionner. Cliquez sur **[!UICONTROL Continue]**.

1. La suite de rapports sélectionnée s’affiche dans un tableau. Cliquez sur **[!UICONTROL Save]** pour confirmer votre sélection.

1. Informez l’[!DNL Commerce Intelligence] [équipe d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) que votre intégration est autorisée et qu’elle exécute le processus de connexion initial pour vous.

Une fois le processus de connexion initial exécuté, votre tableau est disponible dans la page Data Warehouse, sous l’onglet `All Tables` . Sélectionnez les colonnes que vous souhaitez répliquer pour que les données apparaissent après la prochaine mise à jour complète.
