---
title: Données Commerce attendues
description: Explorez les principaux tableaux de données que les utilisateurs de Commerce importent dans Commerce Intelligence
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Données de [!DNL Adobe Commerce] attendues

Après avoir [connecté votre [!DNL Adobe Commerce] boutique](../../../data-analyst/importing-data/integrations/magento.md), vous pouvez utiliser Data Warehouse Manager pour effectuer facilement le suivi des champs de données pertinents de votre base de données Commerce à des fins d’analyse.

Cette rubrique explore les principaux tableaux de données que les utilisateurs de Commerce importent dans [!DNL Commerce Intelligence].

| **Nom de la table** | **Description** |
|-----|-----|
| `Customers` | Le `customer\_entity` et les tableaux associés décrivent les informations associées à chaque *client enregistré* dans votre base de données, comme son adresse e-mail et sa date d’enregistrement. Avec ces informations, vous pouvez commencer à segmenter par attributs et cohortes au niveau du client. |
| `Orders` | La table `sales\_flat\_order` enregistre toutes les commandes, y compris la date et l’heure `created\_at` auxquelles la commande a été passée et le champ `base\_grand\_total` qui additionne le chiffre d’affaires. Ces champs constituent la base des mesures au niveau des commandes. Si la commande a été passée par un *client enregistré*, le champ `customer\_id` renvoie vers la table `customer\_entity` pour permettre une analyse du comportement d’achat du client. |
| `Order items` | La table `sales\_flat\_order\_item` enregistre chaque article appartenant à une commande. Cela inclut les champs `price` et `qty\_ordered`, ainsi que le champ `order\_id` qui se connecte à la table `sales\_flat\_order`. Ce tableau est la base des mesures telles que `Item sold` et vous permet de segmenter par `product` et `product type`. |
| `Products` | Le tableau `catalog\_product\_entity` stocke des informations sur les attributs au niveau du produit, tels que la catégorie, la taille et la couleur. |
| `Categories` | Vos produits appartiennent à un ou plusieurs `product categories` différents, selon la configuration de votre version de Commerce. La table `catalog\_category\_entity` stocke la hiérarchie de ces catégories (Vêtements > Tops > T-shirts, par exemple) et la table `catalog\_category\_product` enregistre les connexions entre vos produits et ces catégories. |

{style="table-layout:auto"}

## Connexe

* [Connexion  [!DNL Adobe Commerce]](../integrations/magento.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
