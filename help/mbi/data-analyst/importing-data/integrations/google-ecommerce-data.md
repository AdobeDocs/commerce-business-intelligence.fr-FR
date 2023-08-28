---
title: Valeur attendue[!DNL Google ECommerce]data
description: Découvrez les types de données qui sont partagés avec Google Commerce.
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 3f16484f189f6b4a8b072d2e3514d2f170993d60
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Valeur attendue [!DNL Google ECommerce] data

Après votre [!DNL Google ECommerce] le compte est connecté à [!DNL Commerce Intelligence], le système commence à importer des données dans un tableau intitulé `ecommerce`. Ce tableau enregistre une ligne de données pour chaque transaction. Cela inclut les colonnes de données au niveau de l’ordre suivantes :

| Nom de la colonne | Description |
|-----|-----|
| `\_id` | Cette colonne est la clé primaire. |
| `accountId` | Cette colonne contient l’identifiant de compte associé à votre [!DNL Google Analytics] Compte eCommerce. |
| `profileName` | Cette colonne contient les [!DNL Google Analytics] nom du profil. |
| `profileId` | Cette colonne contient les [!DNL Google Analytics] identifiant de profil. |
| `socialNetwork` | Cette colonne contient le nom du réseau social (par exemple : [!DNL Facebook], ou [!DNL YouTube]) |
| `campaign` | Cette colonne contient le nom de la campagne (par exemple : [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en)). |
| `medium` | Cette colonne contient le nom du support (par exemple : [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `source` | Cette colonne contient le nom source. (par exemple, [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | Cette colonne contient la description du mot-clé (par exemple : [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `transactionId` | Cette colonne contient l’identifiant de la commande. Il est utilisé pour associer les données de référence à vos données de commande. |
| `updated\_at` | Cette colonne contient la dernière mise à jour de la ligne de données. |

{style="table-layout:auto"}
