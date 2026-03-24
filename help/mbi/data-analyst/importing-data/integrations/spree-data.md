---
title: Données Spree attendues
description: Explorez les principaux tableaux de données que vous pouvez importer de Spree dans votre compte  [!DNL Commerce Intelligence] .
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/DhJhNDqTEki-evyidC-9d08qq-XSDPRu1jJqG1lOijI
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
source-wordcount: 263
ht-degree: 0%

---

# Données de [!DNL Spree] attendues

Après avoir [connecté votre [!DNL Spree] boutique](../../../data-analyst/importing-data/integrations/spree.md), vous pouvez utiliser [Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md) pour effectuer facilement le suivi des champs de données pertinents de votre plateforme [!DNL Spree] à des fins d’analyse.

Cette rubrique explore les principaux tableaux de données que vous pouvez importer depuis [!DNL Spree] dans votre compte [!DNL Commerce Intelligence], y compris des liens vers [&#x200B; documentation supplémentaire &#x200B;](https://guides.spreecommerce.org/developer/addresses.html#address) sur les données [!DNL Spree].

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
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
