---
title: Différences entre SQL et Data Warehouse Manager
description: Découvrez les différences entre SQL et Data Warehouse Manager.
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
TQID: 'https://experienceleague.adobe.com/aWLLAi9e-A6Di7AGujRNd79W7GqSRo5yIgmQRZAHOEQ'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: c38ccf61-5a4f-5140-ad2b-c3434e82ed6d
    internal-label: SQL Report Builder
  - id: f842eedf-96a8-52c7-891d-4e56f7441a7e
    internal-label: Reports
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%
---
# Différences entre [!DNL SQL] et [!DNL Data Warehouse Manager]

Il existe deux différences majeures entre les colonnes créées dans le [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) et celles créées à l’aide du [[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md) . L’un est la dépendance aux cycles de mise à jour, l’autre est la manière dont les colonnes sont enregistrées dans votre compte.

## Colonnes de la [!DNL SQL Report Builder]

Les colonnes ne dépendent pas des cycles de mise à jour. Il n’est donc plus nécessaire d’attendre qu’une colonne soit terminée avant de pouvoir effectuer une itération sur votre colonne. Si vous faites une erreur, il suffit de quelques touches pour la corriger - plus besoin d&#39;attendre que deux mises à jour se terminent avant de pouvoir reprendre le travail.

>[!IMPORTANT]
>
>Les colonnes créées à l’aide de l’éditeur de [!DNL SQL] ne sont pas enregistrées dans votre Data Warehouse. Vous avez toujours accès à la requête contenant la colonne, mais si vous souhaitez utiliser la colonne dans plusieurs rapports, vous devez la recréer dans la requête pour chaque rapport. Cela signifie que les colonnes créées à l’aide de l’éditeur de [!DNL SQL] ne peuvent pas être utilisées dans le [!DNL Report Builder] traditionnel.

## Colonnes du gestionnaire Data Warehouse

Les colonnes dépendent des cycles de mise à jour. Par conséquent, un cycle complet doit être terminé avant de pouvoir être modifiées. Ces colonnes sont enregistrées dans le gestionnaire Data Warehouse et peuvent être utilisées dans le [!DNL Report Builder] ou le [!DNL SQL Report Builder] traditionnel.
