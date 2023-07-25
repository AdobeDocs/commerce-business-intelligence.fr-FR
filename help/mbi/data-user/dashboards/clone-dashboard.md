---
title: Clonage des tableaux de bord
description: Découvrez comment cloner des tableaux de bord.
exl-id: f0bfa786-ab01-4c55-9d8a-ed002c2321b6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Clonage d’un tableau de bord

Le clonage d’un tableau de bord permet de copier tous les rapports d’un tableau de bord dans un nouveau tableau de bord.

Cela s’avère utile si vous souhaitez recréer un ensemble de graphiques existant, mais changer la perspective (par exemple, une vue de données différente, un autre marché, un autre site web ou un autre magasin). Après avoir dupliqué le tableau de bord, vous pouvez modifier chacun des nouveaux graphiques pour modifier sa mesure, sa vue de données, son filtre ou son groupe par groupe.

1. Pour cloner un tableau de bord, cliquez sur **[!UICONTROL Options]** en haut de l’écran.

1. Dans la liste déroulante , cliquez sur **[!UICONTROL Save As]**.

1. Lorsque vous y êtes invité, saisissez la variable `New Dashboard Name`. Adobe recommande les noms qui vous indiquent, en un coup d’oeil, les informations contenues dans le tableau de bord.

   Par exemple, vous clonez un tableau de bord nommé `Customer Activity`. Ce tableau de bord contenait des informations sur l’activité des clients pour votre emplacement Philadelphie, mais vous souhaitez maintenant créer un tableau de bord pour votre nouvel emplacement à New York. Ce tableau de bord peut être nommé `New York City - Customer Activity`.

1. Utilisez la variable `Chart Title Find` et `Chart Title Replace` champs pour trouver tous les graphiques avec `Philadelphia` dans le titre et remplacez-le par `New York City`.

   Si vous ne saisissez aucune valeur dans ces champs, une `(2)` ajoute automatiquement à la fin de tous les titres de graphique dans le nouveau tableau de bord.

1. Cliquez sur **[!UICONTROL Save]** pour cloner le tableau de bord.

Exemple :

![tableau de bord des clones](../../assets/datgif.gif)
