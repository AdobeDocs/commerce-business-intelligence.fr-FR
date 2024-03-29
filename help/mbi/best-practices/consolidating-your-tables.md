---
title: Consolidation de vos tableaux
description: Découvrez comment consolider vos tables et bases de données.
exl-id: 6065bed3-fb84-4147-a223-92dc3e1b15a5
role: Admin, User
feature: Commerce Tables, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Consolidation de vos tableaux

Si vous utilisez plusieurs fronts de magasins ou sur plusieurs marchés, vous pouvez avoir des bases de données similaires stockées séparément. Dans [!DNL Adobe Commerce Intelligence], il est facile de consolider des tables similaires à partir de différentes bases de données.

Par exemple, vous pouvez avoir une `orders` table pour `Market A`, et un `orders` table pour `Market B`. [!DNL Commerce Intelligence] peut consolider les deux tableaux et vous permettre de consulter les données de l’ordre des agrégats des deux `Market A` et `B`, en plus de la segmenter selon un marché spécifique.

Pour que la consolidation des tables fonctionne, les tables d’entrée doivent être **structurée de manière similaire**. En d’autres termes, tous les tableaux d’entrée doivent contenir les colonnes de données requises dans le tableau consolidé.

Cette rubrique décrit certains des cas d’utilisation les plus courants pour les tableaux consolidés et les étapes suivantes nécessaires à la création des vôtres.

## Recommendations pour savoir quand utiliser les tables consolidées

L’exemple suivant indique à quel moment il peut être approprié d’utiliser des tableaux consolidés dans votre système.

### Intégration de données à partir de plusieurs sites web

Si vous vendez vos produits sous différentes marques et différents sites web, il est probable que les tableaux de chaque marque ou site web soient structurés de la même manière.

Par exemple, vous pouvez avoir une `orders` tableau pour le site web `A` et un autre, mais similaire, `orders` tableau pour le site web `B`. Dans ce cas, il peut s’avérer utile de consolider le `orders` tableaux du site web `A` et `B`. Vous pouvez ainsi consulter les recettes consolidées et le nombre de commandes provenant du site web. `A` et `B`, en plus de pouvoir segmenter les mesures en fonction de ces deux sites web.

### Intégration de données héritées

De nombreuses entreprises ont restructuré leurs bases de données à un moment ou un autre, et les données de l&#39;ancienne base de données ne sont pas toujours converties vers le nouveau système. Vous pouvez utiliser des tableaux consolidés pour joindre les colonnes clés des tableaux hérités à celles du système actif. Cela vous permet d’effectuer une analyse unifiée de vos données tout au long de l’histoire.

### Combinaison d’événements pour les analyses utilisateur actives

Imaginez un site web sur lequel les utilisateurs peuvent faire plusieurs choses : répondre à un questionnaire, jouer à un jeu, faire un achat, contacter un ami, etc. En règle générale, chacun de ces événements est stocké dans sa propre table. Il est donc difficile d’analyser le nombre d’utilisateurs distincts qui ont effectué au moins une action, quelle qu’elle soit, au cours d’une période donnée.

Vous pouvez utiliser des tableaux consolidés pour créer une liste unifiée de tous les utilisateurs et le moment où l’un de ces événements s’est produit. Vous pouvez ensuite exécuter des requêtes sur la table consolidée pour réaliser facilement une telle analyse.

Comme pour tous les autres tableaux de votre Data Warehouse, vous pouvez ajouter des colonnes supplémentaires pour alimenter différents types de graphiques et d’analyses.

## Création, affichage ou mise à jour d’une table consolidée

Si vous souhaitez ajouter une table consolidée à votre Data Warehouse, contactez [!DNL Commerce Intelligence] [support](../guide-overview.md#Submitting-a-Support-Ticket).

>[!NOTE]
>
>Parce que les tableaux consolidés ne sont pas visibles dans la variable `Data Warehouse Manager`, l’affichage et la mise à jour de ces tableaux ne peuvent être effectués que par [!DNL Commerce Intelligence] la prise en charge.
