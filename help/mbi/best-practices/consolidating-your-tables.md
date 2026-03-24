---
title: Consolidation des tables
description: Découvrez comment consolider vos tables et bases de données.
exl-id: 6065bed3-fb84-4147-a223-92dc3e1b15a5
role: Admin, User
feature: Commerce Tables, Data Integration
TQID: https://experienceleague.adobe.com/HC5REx483htdfFigZPxcrZeD5byyJKk-beQqnEARt1E
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 469
ht-degree: 0%

---

# Consolidation des tables

Si vous exploitez plusieurs boutiques ou sur plusieurs marchés, vous pouvez avoir des bases de données similaires stockées séparément. En [!DNL Adobe Commerce Intelligence], il est facile de consolider des tables similaires à partir de différentes bases de données.

Par exemple, vous pouvez avoir une table de `orders` pour `Market A` et une table de `orders` similaire pour `Market B`. [!DNL Commerce Intelligence] pouvez consolider les deux tableaux et vous permettre d’examiner les données de commande agrégées de `Market A` et `B`, en plus de les segmenter par marché spécifique.

Pour que la consolidation des tableaux fonctionne, les tableaux d’entrée doivent être **structurés de manière similaire**. En d’autres termes, toutes les tables d’entrée doivent contenir les colonnes de données requises dans la table consolidée.

Cette rubrique présente certains des cas d&#39;utilisation les plus courants pour les tables consolidées et les étapes suivantes requises pour créer les vôtres.

## Recommandations sur l&#39;utilisation des tables consolidées

Vous trouverez ci-dessous des informations sur les cas dans lesquels il peut être approprié d&#39;utiliser des tables consolidées dans votre système.

### Intégration de données provenant de plusieurs sites web

Si vous vendez vos produits sous différentes marques et sites web, il est probable que les tableaux de chaque marque ou site web soient structurés de manière similaire.

Par exemple, vous pouvez disposer d’une table de `orders` pour les `A` du site web et d’une table de `orders` distincte, mais similaire, pour les `B` du site web. Dans ce cas, il peut s’avérer utile de consolider les tableaux `orders` à partir des `A` et des `B` du site web. Vous pouvez ainsi consulter le chiffre d’affaires consolidé et le nombre de commandes provenant des `A` et `B` de sites web, en plus de pouvoir segmenter les mesures en fonction de ces deux sites web.

### Intégration des données héritées

De nombreuses entreprises ont restructuré leurs bases de données à un moment ou à un autre, et les données de l&#39;ancienne base de données ne sont pas toujours converties dans le nouveau système. Vous pouvez utiliser des tables consolidées pour joindre les colonnes clés des tables héritées à celles du système actif. Vous pouvez ainsi effectuer une analyse unifiée de vos données à travers l’historique.

### Combinaison d’événements pour l’analyse des utilisateurs et utilisatrices actifs

Imaginez un site web où les utilisateurs peuvent faire plusieurs choses : répondre à un questionnaire, jouer à un jeu, effectuer un achat, recommander un ami, etc. En règle générale, chacun de ces événements est stocké dans sa propre table. Il est donc difficile d’analyser le nombre d’utilisateurs distincts ayant effectué au moins une action de quelque type que ce soit au cours d’une période donnée.

Vous pouvez utiliser des tables consolidées pour créer une liste unifiée de tous les utilisateurs et le moment où l’un de ces événements a eu lieu. Vous pouvez ensuite exécuter des requêtes sur la table consolidée pour mener facilement une telle analyse.

Comme pour tous les autres tableaux de votre Data Warehouse, vous pouvez ajouter des colonnes supplémentaires pour alimenter différents types de graphiques et d’analyses.

## Création, affichage ou mise à jour d&#39;une table consolidée

Si vous souhaitez ajouter une table consolidée à votre Data Warehouse, contactez [!DNL Commerce Intelligence] [assistance technique](../guide-overview.md#Submitting-a-Support-Ticket).

>[!NOTE]
>
>Étant donné que les tables consolidées ne sont pas visibles dans le `Data Warehouse Manager`, l’affichage et la mise à jour de ces tables ne peuvent être effectués que par le biais d’une prise en charge [!DNL Commerce Intelligence].
