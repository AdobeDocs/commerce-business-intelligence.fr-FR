---
title: Modification en masse de graphiques dans les tableaux de bord
description: Découvrez comment utiliser la fonction de modification en masse dans  [!DNL Commerce Intelligence].
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Modification en masse de graphiques dans les tableaux de bord

La fonction de modification en masse facilite la modification des noms et dates des graphiques dans vos tableaux de bord. Par exemple, vous souhaitez que tous les graphiques d’un tableau de bord spécifique fassent référence à une seule boutique et à un rapport sur une base mensuelle plutôt qu’trimestrielle. Au lieu de tout modifier manuellement, laissez la fonction `bulk-editing` effectuer le travail. Dans cette rubrique, vous apprendrez à utiliser :

* [La fonction  [!DNL Find/Replace] ](#findreplace)

* [La fonction  [!DNL Prepend Name] ](#prepend)

* [La fonction  [!DNL Change Dates] ](#dates)

Cela dit, considérez ceci - *Ces modifications doivent-elles être permanentes ?* Si ce n’est pas le cas, pensez à cloner le tableau de bord, puis à modifier les dates dans le nouveau tableau de bord. Cela vous permet de conserver votre tableau de bord d’origine tout en apportant les modifications dont vous avez besoin.

>[!NOTE]
>
>Si vous modifiez de nombreux rapports, le processus de mise à jour peut prendre un certain temps.

## Utilisation de [!DNL Find/Replace] {#findreplace}

1. Cliquez sur l’icône d’engrenage (![](../../assets/gear-icon.png)) en regard du nom de votre tableau de bord, puis sur la fenêtre [!UICONTROL Bulk Edit Reports].

1. Cliquez sur **[!UICONTROL Chart Title Find and Replace]** dans la fenêtre contextuelle.

1. Dans le champ `Chart Title Find`, saisissez les mots ou les caractères que vous souhaitez trouver.

1. Dans le champ `Replace With` , saisissez les mots ou les caractères qui doivent remplacer ce qui se trouve dans le champ `Find`.

1. Cliquez sur **[!UICONTROL Update Reports]**.

Exemple :

![modification en masse](../../assets/bulk_edit.gif)

## Préparation de `Chart Names` {#prepend}

1. Cliquez sur l’icône d’engrenage (![](../../assets/gear-icon.png)) en regard du nom de votre tableau de bord, puis sur la fenêtre [!UICONTROL Bulk Edit Reports].

1. Cliquez sur **[!UICONTROL Prepend Report Names]** dans la fenêtre contextuelle.

1. Saisissez les mots ou caractères que vous souhaitez ajouter en préfixe à vos graphiques.

1. Cliquez sur **[!UICONTROL Update Reports]**.

Exemple :

![prepend](../../assets/prepend.gif)

## Modification de `Dates` {#dates}

1. Cliquez sur l’icône d’engrenage (![](../../assets/gear-icon.png)) en regard du nom de votre tableau de bord, puis sélectionnez la fenêtre [!UICONTROL Bulk Edit Reports].

1. Cliquez sur **[!UICONTROL Change Dates]** dans la fenêtre contextuelle.

1. Définissez les nouveaux `Start/End Date` et `Time Interval`. Vous pouvez également laisser ces champs inchangés.

1. Cliquez sur **[!UICONTROL Update Reports]**.

Exemple :

![modification de dates](../../assets/dates.gif)
