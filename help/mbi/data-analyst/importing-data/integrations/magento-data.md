---
title: Données commerciales attendues
description: Explorez les principaux tableaux de données que les utilisateurs de Commerce importent dans Commerce Intelligence.
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Valeur attendue [!DNL Adobe Commerce] Données

Après avoir [connecté à [!DNL Adobe Commerce] store](../../../data-analyst/importing-data/integrations/magento.md), vous pouvez utiliser Data Warehouse Manager pour effectuer facilement le suivi des champs de données pertinents de votre base de données Commerce à des fins d’analyse.

Cette rubrique explore les principaux tableaux de données que les utilisateurs de Commerce importent dans . [!DNL Commerce Intelligence].

| **Nom de la table** | **Description** |
|-----|-----|
| `Customers` | Le `customer\_entity` Les tableaux connexes et décrivent les informations associées à chaque *client enregistré* dans votre base de données, comme leur adresse électronique et leur date d’enregistrement. Grâce à ces informations, vous pouvez commencer à segmenter par attributs et cohortes au niveau du client. |
| `Orders` | Le `sales\_flat\_order` enregistre toutes les commandes, y compris la variable `created\_at` date et heure auxquelles la commande a été passée et `base\_grand\_total` qui additionne les recettes. Ces champs sont la base de vos mesures au niveau de la commande. Si la commande a été effectuée par une *client enregistré*, la variable `customer\_id` renvoie au champ  `customer\_entity` tableau permettant d’analyser le comportement d’achat des clients. |
| `Order items` | Le `sales\_flat\_order\_item` enregistre chaque élément appartenant à une commande. Cela inclut la variable `price` et `qty\_ordered` et la variable `order\_id` qui se connecte au champ `sales\_flat\_order` table. Ce tableau constitue la base des mesures telles que `Item sold`et vous permet de segmenter par `product` et `product type`. |
| `Products` | Le `catalog\_product\_entity` Le tableau stocke des informations sur les attributs au niveau du produit, tels que la catégorie, la taille et la couleur. |
| `Categories` | Vos produits appartiennent à un ou plusieurs `product categories`, selon la configuration de votre version de Commerce. Le `catalog\_category\_entity` Le tableau stocke la hiérarchie de ces catégories (Vêtements > Principaux > T-shirts, par exemple) et la variable `catalog\_category\_product` Le tableau consigne les connexions entre vos produits et ces catégories. |

{style="table-layout:auto"}

## Associé

* [Connexion [!DNL Adobe Commerce]](../integrations/magento.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
