---
title: Données commerciales attendues
description: Explorer les principaux tableaux de données que les utilisateurs de Commerce importent dans l’IMS
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Données commerciales attendues

Après avoir [connecté à votre boutique Commerce](../../../data-analyst/importing-data/integrations/magento.md), vous pouvez utiliser Data Warehouse Manager pour effectuer facilement le suivi des champs de données pertinents de votre base de données Commerce à des fins d’analyse.

Dans cet article, nous explorons les principaux tableaux de données dans lesquels les utilisateurs de Commerce importent [!DNL MBI].

| **Nom de la table** | **Description** |
|-----|-----|
| `Customers` | Le `customer\_entity` Les tableaux connexes et décrivent les informations associées à chaque *client enregistré* dans votre base de données, comme leur adresse électronique et leur date d’enregistrement. Grâce à ces informations, vous pouvez commencer à segmenter par attributs et cohortes au niveau du client. |
| `Orders` | Le `sales\_flat\_order` enregistre toutes les commandes, y compris la variable `created\_at` date et heure auxquelles la commande a été passée et `base\_grand\_total` qui additionne les recettes. Ces champs seront la base de vos mesures au niveau de la commande. Si la commande a été effectuée par une *client enregistré*, la variable `customer\_id` renvoie au champ  `customer\_entity` tableau permettant d’analyser le comportement d’achat des clients. |
| `Order items` | Le `sales\_flat\_order\_item` enregistre chaque élément appartenant à une commande. Cela inclut la variable `price` et `qty\_ordered` , ainsi que la variable `order\_id` qui se connecte au champ `sales\_flat\_order` table. Ce tableau constitue la base des mesures telles que `Item sold`et vous permet de segmenter par `product` et `product type`. |
| `Products` | Le `catalog\_product\_entity` Le tableau stocke des informations sur les attributs au niveau du produit, tels que la catégorie, la taille et la couleur. |
| `Categories` | Vos produits appartiennent à un ou plusieurs `product categories`, selon la configuration de votre version de Commerce. Le `catalog\_category\_entity` Le tableau stocke la hiérarchie de ces catégories (par exemple, Propriétés > T-Shirts) et la variable `catalog\_category\_product` Le tableau consigne les connexions entre vos produits et ces catégories. |

{style=&quot;table-layout:auto&quot;}

## Associé

* [Connexion [!DNL Magento]](../integrations/magento.md)
* [Réauthentification des intégrations](https://support.magento.com/hc/en-us/articles/360016733151)
