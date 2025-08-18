---
title: Validation des données dans Mixpanel
description: Découvrez comment vérifier que vous avez synchronisé toutes les données qui sont disponibles directement dans Mixpanel.
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# Validation des données dans [!DNL Mixpanel]

Lorsque [!DNL Adobe Commerce Intelligence] se connecte pour la première fois à vos données [!DNL Mixpanel], votre gestionnaire de compte ou votre analyste peut vous demander de fournir des exportations de données à partir de [!DNL Mixpanel] à des fins de validation. Vous pouvez ainsi confirmer que vous avez synchronisé toutes les données qui sont disponibles pour vous directement dans [!DNL Mixpanel].

## Processus d’exportation des données : `Events`

1. Consultez votre section `Segmentation` et affichez les `Your Top Events`.

   ![](../../../assets/your-top-events.png)

1. Sélectionnez `Past 96 Hours` pour la période

   ![](../../../assets/past-96-hours.png)

1. Faites défiler jusqu’à la partie inférieure droite du rapport et exportez un fichier `.csv` :

   ![](../../../assets/export-csv-mixpanel.png)

1. Envoyez le fichier `.csv` au gestionnaire de compte ou à l’analyste avec lequel vous travaillez sur ce processus de validation.
