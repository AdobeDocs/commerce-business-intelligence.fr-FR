---
title: Données de diffusion prévues
description: Explorez les tables de données principales que vous pouvez importer à partir de Spree dans votre compte  [!DNL Commerce Intelligence] .
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Données [!DNL Spree] attendues

Une fois que vous avez [connecté à votre  [!DNL Spree] boutique](../../../data-analyst/importing-data/integrations/spree.md), vous pouvez utiliser le [Gestionnaire de Data Warehouse](../../data-warehouse-mgr/tour-dwm.md) pour facilement suivre les champs de données pertinents de votre plateforme [!DNL Spree] à des fins d’analyse.

Cette rubrique explore les tables de données principales que vous pouvez importer de [!DNL Spree] dans votre compte [!DNL Commerce Intelligence], y compris les liens vers la [documentation supplémentaire](https://guides.spreecommerce.org/developer/addresses.html#address) sur les données [!DNL Spree].

| **Nom de la table** | **Description** |
|-----|-----|
| `Users` | La table `users` contient les détails du compte des clients enregistrés, y compris l’adresse électronique, le nom et la date d’enregistrement de la personne. Vous pouvez ainsi analyser différents segments de clients et leurs comportements d’achat. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | La table `orders` sert de base à toutes vos mesures au niveau de la commande. Vous trouverez ici tous les détails de commande des achats de votre boutique [!DNL Spree], y compris `completed\_at` (horodatage de la commande), `user\_id` (ID de l’utilisateur enregistré qui a passé la commande). Si la commande a été effectuée par un utilisateur enregistré, `user\_id` revient à la table `users` pour permettre l’analyse du comportement d’achat des utilisateurs. |
| `Line items` | La table `line\_items` est un enfant de la table `orders` ou `subscriptions`. Elle enregistre les détails d’élément de ligne d’une commande ou d’un abonnement. Pour les commandes comportant plusieurs produits, chaque produit possède sa propre ligne de données dans ce tableau, y compris un `product\_id` qui vous permet de l’associer à la table `Products`. |
| `Products` | La table `products` enregistre tous les détails d’un article vendable dans votre catalogue Spree. Vous pouvez ainsi segmenter les mesures au niveau de l’élément de ligne par attributs de produit. |
| `Subscriptions` | Si vous disposez d’une extension [!DNL Spree] abonnements, la table `subscriptions` contient les informations de chaque abonnement individuel, y compris `created\_at` (date de début), `cancelled\_at` (date d’annulation d’un abonnement) et `interval` de l’abonnement. |

{style="table-layout:auto"}

## En rapport :

* [Connexion [!DNL Spree]](../integrations/spree.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
