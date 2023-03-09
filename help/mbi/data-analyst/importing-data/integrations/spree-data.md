---
title: Données de diffusion prévues
description: Explorez les principaux tableaux de données que vous pouvez importer à partir de Spree dans votre [!DNL MBI] compte .
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Valeur attendue [!DNL Spree] data

Après avoir [connecté à [!DNL Spree] store](../../../data-analyst/importing-data/integrations/spree.md), vous pouvez utiliser la variable [Gestionnaire de Data Warehouse](../../data-warehouse-mgr/tour-dwm.md) pour effectuer facilement le suivi des champs de données pertinents à partir de vos [!DNL Spree] plateforme d’analyse.

Cet article explore les principaux tableaux de données à partir desquels vous pouvez importer des [!DNL Spree] dans [!DNL MBI] compte, y compris les liens vers [documentation supplémentaire](https://guides.spreecommerce.org/developer/addresses.html#address) about [!DNL Spree] data.

| **Nom de la table** | **Description** |
|-----|-----|
| `Users` | Le `users` le tableau comprend les détails du compte des clients enregistrés, y compris l’adresse électronique, le nom et la date d’enregistrement de la personne. Vous pouvez ainsi analyser différents segments de clients et leurs comportements d’achat. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | Le `orders` sert de base à toutes vos mesures au niveau de la commande. Vous trouverez ici tous les détails de commande des achats de votre [!DNL Spree] magasin, y compris `completed\_at` (horodatage de la commande), `user\_id` (ID de l’utilisateur enregistré qui a passé la commande). Si la commande a été effectuée par un utilisateur enregistré, la variable `user\_id` renvoie au `users` pour permettre l’analyse du comportement d’achat des utilisateurs. |
| `Line items` | Le `line\_items` est un enfant de l’un des `orders` table ou `subscriptions`. Elle enregistre les détails d’élément de ligne d’une commande ou d’un abonnement. Pour les commandes comportant plusieurs produits, chaque produit possède sa propre ligne de données dans ce tableau, y compris une `product\_id` qui vous permet de l’associer à la variable `Products` table. |
| `Products` | Le `products` Le tableau enregistre tous les détails du produit pour un article vendable dans votre catalogue Spree. Vous pouvez ainsi segmenter les mesures au niveau de l’élément de ligne par attributs de produit. |
| `Subscriptions` | Si vous avez une [!DNL Spree] extension abonnements, l’extension `subscriptions` contient les informations de chaque abonnement individuel, y compris `created\_at` (la date de début), `cancelled\_at` (date d’annulation d’un abonnement), et la variable `interval` de l’abonnement. |

{style="table-layout:auto"}

## En rapport :

* [Connexion [!DNL Spree]](../integrations/spree.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
