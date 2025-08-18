---
title: Données Spree attendues
description: Explorez les principaux tableaux de données que vous pouvez importer de Spree dans votre compte  [!DNL Commerce Intelligence] .
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Données de [!DNL Spree] attendues

Après avoir [connecté votre [!DNL Spree] boutique](../../../data-analyst/importing-data/integrations/spree.md), vous pouvez utiliser [Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md) pour effectuer facilement le suivi des champs de données pertinents de votre plateforme [!DNL Spree] à des fins d’analyse.

Cette rubrique explore les principaux tableaux de données que vous pouvez importer depuis [!DNL Spree] dans votre compte [!DNL Commerce Intelligence], y compris des liens vers [ documentation supplémentaire ](https://guides.spreecommerce.org/developer/addresses.html#address) sur les données [!DNL Spree].

| **Nom de la table** | **Description** |
|-----|-----|
| `Users` | Le tableau `users` inclut les détails du compte pour les clients enregistrés, y compris l’adresse e-mail, le nom et la date d’enregistrement de la personne. Vous pouvez ainsi analyser différents segments de clients et leurs comportements d’achat. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | Le tableau `orders` sert de base à toutes les mesures au niveau des commandes. Vous trouverez ici tous les détails de la commande d’achats effectués dans votre boutique [!DNL Spree], y compris `completed\_at` (horodatage de la commande) `user\_id` (ID de l’utilisateur enregistré qui a passé la commande). Si la commande a été passée par un utilisateur enregistré, le `user\_id` renvoie au tableau `users` pour permettre une analyse du comportement d’achat de l’utilisateur. |
| `Line items` | La table `line\_items` est un enfant de la table `orders` ou de la `subscriptions`. Il enregistre les détails d’une ligne de commande ou d’abonnement. Pour les commandes comportant plusieurs produits, chaque produit possède sa propre ligne de données dans ce tableau, y compris une `product\_id` qui vous permet de le lier au tableau `Products`. |
| `Products` | Le tableau `products` enregistre tous les détails d&#39;un article vendable dans votre catalogue Spree. Vous pouvez ainsi segmenter vos mesures au niveau de l’élément de ligne par attributs de produit. |
| `Subscriptions` | Si vous disposez d’une extension d’abonnements [!DNL Spree], la table `subscriptions` contient les informations de chaque abonnement individuel, y compris les `created\_at` (date de début), `cancelled\_at` (date d’annulation d’un abonnement) et la `interval` de l’abonnement. |

{style="table-layout:auto"}

## Connexe :

* [Connexion  [!DNL Spree]](../integrations/spree.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=fr)
