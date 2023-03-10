---
title: Valeur attendue[!DNL Google ECommerce]data
description: Découvrez les types de données qui sont partagés avec Google ECommerce.
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Valeur attendue[!DNL Google ECommerce] data

Après votre [!DNL Google ECommerce] le compte est connecté à [!DNL MBI], le système commence à importer des données dans un tableau intitulé `ecommerce`. Ce tableau enregistre une ligne de données pour chaque transaction. Cela inclut les colonnes de données au niveau de l’ordre suivantes :

| Nom de la colonne | Description |
|-----|-----|
| `\_id` | Cette colonne est la Principale clé. |
| `accountId` | Cette colonne contient l’identifiant de compte associé à votre [!DNL Google Analytics] Compte eCommerce. |
| `profileName` | Cette colonne contient les [!DNL Google Analytics] nom du profil. |
| `profileId` | Cette colonne contient les [!DNL Google Analytics] identifiant de profil. |
| `socialNetwork` | Cette colonne contient le nom du réseau social (par exemple : [!DNL Facebook]ou [!DNL YouTube]) |
| `campaign` | Cette colonne contient le nom de la campagne (par exemple : [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en)). |
| `medium` | Cette colonne contient le nom du support (par exemple : [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `source` | Cette colonne contient le nom source. (par exemple, [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | Cette colonne contient la description du mot-clé (par exemple : [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `transactionId` | Cette colonne contient l’identifiant de la commande. Il est utilisé pour associer les données de référence à vos données de commande. |
| `updated\_at` | Cette colonne contient la dernière fois que la ligne de données a été mise à jour. |

{style="table-layout:auto"}
