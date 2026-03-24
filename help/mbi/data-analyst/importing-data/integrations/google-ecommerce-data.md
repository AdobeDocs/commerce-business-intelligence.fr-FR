---
title: Données [!DNL Google ECommerce]
description: Découvrez quels types de données sont partagés avec Google ECommerce.
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/tGcSyz6DHcusK-RomMkRZoyY7acXb0dmXlHcc5pW7cg
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 158
ht-degree: 0%

---

# Données de [!DNL Google ECommerce] attendues

Une fois que votre compte [!DNL Google ECommerce] est connecté à [!DNL Commerce Intelligence], le système commence à importer les données dans une table intitulée `ecommerce`. Ce tableau enregistre une ligne de données pour chaque transaction. Cela inclut les colonnes de données au niveau de l’ordre suivantes :

| Nom de la colonne | Description |
|-----|-----|
| `\_id` | Cette colonne est la clé primaire. |
| `accountId` | Cette colonne contient l’identifiant de compte associé à votre compte eCommerce [!DNL Google Analytics]. |
| `profileName` | Cette colonne contient le nom de votre profil [!DNL Google Analytics]. |
| `profileId` | Cette colonne contient votre identifiant de profil [!DNL Google Analytics]. |
| `socialNetwork` | Cette colonne contient le nom du réseau social (par exemple, [!DNL Facebook] ou [!DNL YouTube]) |
| `campaign` | Cette colonne contient le nom de la campagne (par exemple, [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en)). |
| `medium` | Cette colonne contient le nom du média (par exemple, [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `source` | Cette colonne contient le nom de la source. (par exemple, [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | Cette colonne contient la description du mot-clé (par exemple, [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)). |
| `transactionId` | Cette colonne contient l’ID de commande. Il est utilisé pour relier les données de référence aux données de vos commandes. |
| `updated\_at` | Cette colonne contient la dernière mise à jour de la ligne de données. |

{style="table-layout:auto"}
