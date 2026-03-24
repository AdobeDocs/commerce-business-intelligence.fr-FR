---
title: Modification en masse de graphiques dans des tableaux de bord
description: Découvrez comment utiliser la fonction de modification en masse dans  [!DNL Commerce Intelligence].
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
TQID: https://experienceleague.adobe.com/FcFTKq9TvldFwo7nl-bGRyup1uxscjrnOutJcA-h-5c
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 260
ht-degree: 1%

---

# Modification en masse de graphiques dans les tableaux de bord

La fonctionnalité de modification en masse facilite la modification des noms de graphique et des dates dans vos tableaux de bord. Par exemple, vous souhaitez que tous les graphiques d’un tableau de bord spécifique fassent référence à un seul magasin et génèrent des rapports sur une base mensuelle plutôt que trimestrielle. Plutôt que de tout modifier manuellement, laissez la fonction `bulk-editing` faire le travail. Dans cette rubrique, vous apprendrez à utiliser :

* [La  [!DNL Find/Replace] ](#findreplace)

* [La  [!DNL Prepend Name] ](#prepend)

* [La  [!DNL Change Dates] ](#dates)

Cela dit, considérez ceci : *Ces changements doivent-ils être permanents ?* Dans le cas contraire, envisagez de cloner le tableau de bord, puis de modifier les dates dans le nouveau tableau de bord. Vous pouvez ainsi conserver votre tableau de bord d’origine tout en apportant les modifications dont vous avez besoin.

>[!NOTE]
>
>Si vous modifiez de nombreux rapports, le processus de mise à jour peut prendre un certain temps.

## Utilisation de [!DNL Find/Replace] {#findreplace}

1. Cliquez sur l’icône d’engrenage (![icône d’engrenage](../../assets/gear-icon.png)) en regard du nom de votre tableau de bord, puis sur la fenêtre de [!UICONTROL Bulk Edit Reports].

1. Cliquez sur **[!UICONTROL Chart Title Find and Replace]** dans la fenêtre contextuelle.

1. Dans le champ `Chart Title Find` , saisissez les mots ou les caractères à rechercher.

1. Dans le champ `Replace With` , saisissez les mots ou les caractères qui doivent remplacer le contenu du champ `Find` .

1. Cliquez sur **[!UICONTROL Update Reports]**.

Exemple :

![modification en bloc](../../assets/bulk_edit.gif)

## `Chart Names` en attente {#prepend}

1. Cliquez sur l’icône d’engrenage (![icône d’engrenage](../../assets/gear-icon.png)) en regard du nom de votre tableau de bord, puis sur la fenêtre de [!UICONTROL Bulk Edit Reports].

1. Cliquez sur **[!UICONTROL Prepend Report Names]** dans la fenêtre contextuelle.

1. Saisissez les mots ou les caractères avec lesquels vous souhaitez ajouter le préfixe à vos graphiques.

1. Cliquez sur **[!UICONTROL Update Reports]**.

Exemple :

![ajouter](../../assets/prepend.gif)

## Modification des `Dates` {#dates}

1. Cliquez sur l’icône d’engrenage (![icône d’engrenage](../../assets/gear-icon.png)) en regard du nom de votre tableau de bord, puis sélectionnez la fenêtre de [!UICONTROL Bulk Edit Reports].

1. Cliquez sur **[!UICONTROL Change Dates]** dans la fenêtre pop-up.

1. Définissez les nouveaux `Start/End Date` et `Time Interval`. Vous pouvez également laisser ces champs inchangés.

1. Cliquez sur **[!UICONTROL Update Reports]**.

Exemple :

![modification des dates](../../assets/dates.gif)
