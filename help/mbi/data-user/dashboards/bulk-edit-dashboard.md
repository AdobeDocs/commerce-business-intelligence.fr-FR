---
title: Modification en masse de graphiques dans des tableaux de bord
description: Découvrez comment utiliser la fonction de modification en masse dans  [!DNL Commerce Intelligence].
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '260'
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
