---
title: Données Commerce attendues
description: Explorez les principaux tableaux de données que les utilisateurs de Commerce importent dans Commerce Intelligence
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/D-GNfk1-kMscgF1xBKM5xG7wRV4IkIDh9wEBCMGb630
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 253
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
