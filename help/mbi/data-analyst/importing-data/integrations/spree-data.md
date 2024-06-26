---
title: Données de diffusion prévues
description: Explorez les principaux tableaux de données que vous pouvez importer à partir de Spree dans votre [!DNL Commerce Intelligence] compte .
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Valeur attendue [!DNL Spree] data

Après avoir [connecté à [!DNL Spree] store](../../../data-analyst/importing-data/integrations/spree.md), vous pouvez utiliser la variable [Gestionnaire de Data Warehouse](../../data-warehouse-mgr/tour-dwm.md) pour effectuer facilement le suivi des champs de données pertinents à partir de vos [!DNL Spree] plateforme d’analyse.

Cette rubrique explore les principaux tableaux de données à partir desquels vous pouvez importer des [!DNL Spree] dans votre [!DNL Commerce Intelligence] compte, y compris les liens vers [documentation supplémentaire](https://guides.spreecommerce.org/developer/addresses.html#address) about [!DNL Spree] data.

| **Nom de la table** | **Description** |
|-----|-----|
| `Users` | La variable `users` le tableau comprend les détails du compte des clients enregistrés, y compris l’adresse électronique, le nom et la date d’enregistrement de la personne. Vous pouvez ainsi analyser différents segments de clients et leurs comportements d’achat. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | La variable `orders` sert de base à toutes vos mesures au niveau de la commande. Vous trouverez ici tous les détails de commande des achats de votre [!DNL Spree] magasin, y compris `completed\_at` (horodatage de la commande), `user\_id` (ID de l’utilisateur enregistré qui a passé la commande). Si la commande a été effectuée par un utilisateur enregistré, la variable `user\_id` renvoie au `users` pour permettre l’analyse du comportement d’achat des utilisateurs. |
| `Line items` | La variable `line\_items` est un enfant de l’une des fonctions `orders` table ou `subscriptions`. Elle enregistre les détails d’élément de ligne d’une commande ou d’un abonnement. Pour les commandes comportant plusieurs produits, chaque produit possède sa propre ligne de données dans ce tableau, y compris une `product\_id` qui vous permet de l’associer à la variable `Products` table. |
| `Products` | La variable `products` Le tableau enregistre tous les détails du produit pour un article vendable dans votre catalogue Spree. Vous pouvez ainsi segmenter les mesures au niveau de l’élément de ligne par attributs de produit. |
| `Subscriptions` | Si vous avez une [!DNL Spree] extension abonnements, l’extension `subscriptions` contient les informations de chaque abonnement individuel, y compris `created\_at` (la date de début), `cancelled\_at` (date d’annulation d’un abonnement), et la variable `interval` de l’abonnement. |

{style="table-layout:auto"}

## En rapport :

* [Connexion [!DNL Spree]](../integrations/spree.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
