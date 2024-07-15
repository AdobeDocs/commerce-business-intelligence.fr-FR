---
title: Données Commerce attendues
description: Explorer les principaux tableaux de données que les utilisateurs de Commerce importent dans Commerce Intelligence
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Données [!DNL Adobe Commerce] attendues

Une fois que vous avez [connecté à votre  [!DNL Adobe Commerce] boutique](../../../data-analyst/importing-data/integrations/magento.md), vous pouvez utiliser le Gestionnaire de Data Warehouse pour effectuer facilement le suivi des champs de données pertinents de votre base de données Commerce en vue de l’analyse.

Cette rubrique explore les principaux tableaux de données que les utilisateurs de Commerce importent dans [!DNL Commerce Intelligence].

| **Nom de la table** | **Description** |
|-----|-----|
| `Customers` | Les `customer\_entity` et les tableaux connexes décrivent les informations associées à chaque *client enregistré* dans votre base de données, comme son adresse électronique et sa date d’enregistrement. Grâce à ces informations, vous pouvez commencer à segmenter par attributs et cohortes au niveau du client. |
| `Orders` | La table `sales\_flat\_order` enregistre toutes les commandes, y compris l’horodatage `created\_at` où la commande a été passée et le champ `base\_grand\_total` qui additionne les recettes. Ces champs sont la base de vos mesures au niveau de la commande. Si la commande a été effectuée par un *client enregistré*, le champ `customer\_id` renvoie à la table `customer\_entity` pour permettre l’analyse du comportement d’achat des clients. |
| `Order items` | La table `sales\_flat\_order\_item` enregistre chaque élément appartenant à une commande. Cela inclut les champs `price` et `qty\_ordered`, ainsi que le champ `order\_id` qui se connecte à la table `sales\_flat\_order`. Ce tableau est la base de mesures telles que `Item sold` et vous permet de segmenter par `product` et `product type`. |
| `Products` | La table `catalog\_product\_entity` stocke des informations sur les attributs au niveau du produit, tels que la catégorie, la taille et la couleur. |
| `Categories` | Vos produits appartiennent à un ou plusieurs `product categories` différents, en fonction de la configuration de votre version Commerce. La table `catalog\_category\_entity` stocke la hiérarchie de ces catégories (Vêtements > Trops > T-Shirts, par exemple), et la table `catalog\_category\_product` consigne les connexions entre vos produits et ces catégories. |

{style="table-layout:auto"}

## Associé

* [Connexion [!DNL Adobe Commerce]](../integrations/magento.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
