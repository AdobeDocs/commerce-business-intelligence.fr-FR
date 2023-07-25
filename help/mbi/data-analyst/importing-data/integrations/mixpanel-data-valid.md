---
title: Validation des données dans Mixpanel
description: Découvrez comment vérifier que vous avez synchronisé toutes les mêmes données disponibles directement dans Mixpanel.
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# Validation des données dans [!DNL Mixpanel]

When [!DNL Adobe Commerce Intelligence] se connecte d’abord à votre [!DNL Mixpanel] , votre gestionnaire de compte ou votre analyste peut vous demander de fournir des exportations de données depuis [!DNL Mixpanel] à des fins de validation. Cela vous permet de confirmer que vous avez synchronisé toutes les mêmes données disponibles directement dans [!DNL Mixpanel].

## Processus d’exportation des données : `Events`

1. Visitez votre `Segmentation` section et affichage `Your Top Events`.

   ![](../../../assets/your-top-events.png)

1. Sélectionner `Past 96 Hours` pour la période

   ![](../../../assets/past-96-hours.png)

1. Accédez à la partie inférieure droite du rapport et exportez un `.csv` fichier :

   ![](../../../assets/export-csv-mixpanel.png)

1. Envoyez la variable `.csv` au gestionnaire de compte ou à l’analyste avec lequel vous travaillez sur ce processus de validation.
