---
title: Validation des données dans Mixpanel
description: Découvrez comment vérifier que vous avez synchronisé toutes les données qui sont disponibles directement dans Mixpanel.
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/D6qvHVgPX0WEbKZSYel4siWMLTu9BloFBQMTxXxnbY0
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 134
ht-degree: 0%

---

# Validation des données dans [!DNL Mixpanel]

Lorsque [!DNL Adobe Commerce Intelligence] se connecte pour la première fois à vos données [!DNL Mixpanel], votre gestionnaire de compte ou votre analyste peut vous demander de fournir des exportations de données à partir de [!DNL Mixpanel] à des fins de validation. Vous pouvez ainsi confirmer que vous avez synchronisé toutes les données qui sont disponibles pour vous directement dans [!DNL Mixpanel].

## Processus d’exportation des données : `Events`

1. Consultez votre section `Segmentation` et affichez les `Your Top Events`.

   ![Tableau de bord Mixpanel présentant vos principaux événements](../../../assets/your-top-events.png)

1. Sélectionnez `Past 96 Hours` pour la période

   ![Sélecteur de période Mixpanel affichant l’option des 96 dernières heures](../../../assets/past-96-hours.png)

1. Faites défiler jusqu’à la partie inférieure droite du rapport et exportez un fichier `.csv` :

   ![Option Exporter un panneau mixte au format CSV dans le menu](../../../assets/export-csv-mixpanel.png)

1. Envoyez le fichier `.csv` au gestionnaire de compte ou à l’analyste avec lequel vous travaillez sur ce processus de validation.

