---
title: Commandes des invités
description: Découvrez l’impact des commandes d’invités sur vos données et les options que vous devez correctement tenir compte des commandes d’invités dans votre  [!DNL Commerce Intelligence] Data Warehouse.
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# Commandes d’invités

Lors de la révision de vos commandes, si vous constatez que de nombreuses valeurs `customer\_id` sont nulles ou n’ont pas de valeur à associer à la table `customers`, cela indique que votre boutique autorise les commandes d’invités. Cela signifie que votre table `customers` ne comprend probablement pas tous vos clients.

Cette rubrique décrit l’impact des commandes d’invités sur vos données et les options que vous devez correctement tenir compte des commandes d’invités dans votre Data Warehouse [!DNL Commerce Intelligence].

## Impact des commandes d’invités sur les données

Dans la base de données commerciale classique, il existe une table `orders` qui rejoint une table `customers`. Chaque ligne de la table `orders` comporte une colonne `customer\_id` propre à une ligne de la table `customers`.

* **Si tous les clients sont enregistrés** et que les commandes d’invités ne sont pas autorisées, cela signifie que chaque enregistrement de la table `orders` a une valeur dans la colonne `customer\_id`. Par conséquent, chaque commande revient à la table `customers`.

  ![](../../assets/guest-orders-4.png)

* **Si les commandes d’invités sont autorisées**, cela signifie que certaines commandes n’ont pas de valeur dans la colonne `customer\_id`. Seuls les clients enregistrés reçoivent une valeur pour la colonne `customer\_id` de la table `orders`. Les clients qui ne sont pas enregistrés reçoivent une valeur `NULL` (ou vide) pour cette colonne. Par conséquent, tous les enregistrements de commande n’ont pas les enregistrements correspondants dans la table `customers`.

  >[!NOTE]
  >
  >Pour identifier l’individu unique qui a effectué la commande, un autre attribut utilisateur unique doit être associé à une commande en regard de `customer\_id`. En règle générale, l’adresse électronique du client est utilisée.

## Comment tenir compte des commandes d’invités dans la configuration du Data Warehouse

En règle générale, l’ingénieur commercial qui met en oeuvre votre compte prend en compte les commandes des invités lors de la création de la base de votre Data Warehouse.

La manière la plus optimale de comptabiliser les commandes d’invités est de baser toutes les mesures au niveau du client sur la table `orders`. Cette configuration utilise un ID de client unique que tous les clients possèdent, y compris les invités (normalement, l’e-mail du client est utilisé). Cela ignore les données d&#39;enregistrement de la table `customers`. Avec cette option, seuls les clients qui ont effectué au moins un achat sont inclus dans les rapports au niveau du client. Les utilisateurs enregistrés qui n’ont pas encore effectué un achat ne sont pas inclus. Avec cette option, votre mesure `New customer` est basée sur la date de première commande du client dans la table `orders`.

Vous pouvez remarquer que le filtre `Customers we count` défini dans ce type de configuration comporte un filtre pour `Customer's order number = 1`.

![](../../assets/guest-orders-filter-set.png)

En l’absence de commandes d’invités, chaque client existe comme une ligne unique dans la table des clients (voir Image 1). Une mesure telle que `New customers` peut simplement comptabiliser l’identifiant de cette table en fonction de la date `created\_at` pour comprendre les nouveaux clients en fonction de la date d’enregistrement.

Dans une configuration de commandes d’invités où toutes les mesures de clients sont basées sur la table `orders` pour tenir compte des commandes d’invités, vous devez vous assurer que vous êtes `not counting customers twice`. Si vous comptez l’identifiant de la table des commandes, vous comptez chaque commande. Si vous comptabilisez plutôt l&#39;identifiant sur la table `orders` et utilisez un filtre, `Customer's order number = 1`, alors vous allez compter chaque client unique `only one time`. Cela s’applique à toutes les mesures au niveau des clients, telles que `Customer's lifetime revenue` ou `Customer's lifetime number of orders`.

Vous pouvez voir ci-dessus qu’il existe une valeur nulle `customer\_ids` dans la table `orders`. Si vous utilisez `customer\_email` pour identifier des clients uniques, vous pouvez constater que `erin@test.com` a passé trois (3) commandes. Par conséquent, vous pouvez créer une mesure `New customers` sur votre table `orders` en fonction des conditions suivantes :

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
