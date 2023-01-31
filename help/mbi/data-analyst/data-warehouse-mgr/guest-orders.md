---
title: Commandes des invités
description: Découvrez l’impact des commandes d’invités sur vos données et les options que vous devez correctement tenir compte des commandes d’invités dans vos [!DNL MBI] entrepôt de données.
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# Commandes d’invités

Lors de la révision de vos commandes, si vous constatez que plusieurs `customer\_id` Les valeurs sont nulles ou n’ont pas de valeur à associer à `customers` , cela indique généralement que votre boutique autorise les commandes d’invités. Cela signifie que votre `customers` La table n’est probablement pas incluse pour tous vos clients.

Dans cette rubrique, nous discutons de l’impact des commandes d’invités sur vos données et des options que vous devez correctement tenir compte des commandes d’invités dans vos [!DNL MBI] entrepôt de données.

## Impact des commandes d’invités sur les données

Dans la base de données commerciale standard, il existe une `orders` table qui se joint à un `customers` table. Chaque ligne du `orders` comporte une `customer\_id` qui est propre à une ligne sur la colonne `customers` table.

* **Si tous les clients sont enregistrés** et les commandes d’invités ne sont pas autorisées, ce qui signifie que chaque enregistrement dans la variable `orders` contient une valeur dans la variable `customer\_id` colonne . Par conséquent, chaque commande revient au `customers` table. Vous pouvez le voir sur l’image ci-dessous.

   ![](../../assets/guest-orders-4.png)

* **Si les commandes d’invités sont autorisées**, cela signifie que certaines commandes n’ont pas de valeur dans la variable `customer\_id` colonne . Seuls les clients enregistrés reçoivent une valeur pour la variable `customer\_id` sur la `orders` table. Les clients qui ne sont pas enregistrés recevront un `NULL` (ou vide) pour cette colonne. Par conséquent, les enregistrements de commande ne contiendront pas tous les enregistrements correspondants dans la variable `customers` table.

   >[!NOTE]
   >
   >Pour identifier l’individu unique qui a passé la commande, un autre attribut utilisateur unique doit se trouver en regard de . `customer\_id` joint à une commande. En règle générale, l’adresse électronique du client est utilisée.

## Comment tenir compte des commandes d’invités dans la configuration de l’entrepôt de données

En règle générale, l’ingénieur du service commercial qui met en oeuvre votre compte prendra en compte les commandes des invités lors de la création de la base de votre entrepôt de données.

La méthode la plus optimale pour comptabiliser les commandes d’invités consiste à baser toutes les mesures au niveau du client sur la variable `orders` table. Cette configuration utilise un ID de client unique que tous les clients possèdent, y compris les invités (normalement, l’e-mail du client est utilisé). Cela ignore les données d’enregistrement de la variable `customers` table. Avec cette option, seuls les clients qui ont effectué au moins un achat seront inclus dans les rapports au niveau du client. Les utilisateurs enregistrés qui n’ont pas encore effectué un achat ne seront pas inclus. Avec cette option, votre `New customer` est basée sur la date de première commande du client dans la variable `orders` table.

Vous pouvez remarquer que la variable `Customers we count` le filtre défini dans ce type de configuration comporte un filtre pour `Customer's order number = 1`. Réfléchissons à pourquoi ceci est.

![](../../assets/guest-orders-filter-set.png)

En l’absence de commandes d’invités, chaque client existe comme une ligne unique dans la table des clients (voir Image 1). Une mesure telle que `New customers` peut simplement compter l’identifiant de ce tableau en fonction de `created\_at` date pour comprendre Nouveaux clients en fonction de la date d’enregistrement.

Dans une configuration de commandes d’invité où toutes les mesures de client sont basées sur la variable `orders` pour tenir compte des commandes d’invités, vous devez vous assurer que vous êtes `not counting customers twice`. Si vous comptez l&#39;identifiant de la table des commandes, vous comptez chaque commande. Si vous comptabilisez plutôt l’identifiant sur la variable `orders` et utiliser un filtre, `Customer's order number = 1`, vous allez ensuite compter chaque client unique. `only one time`. Cela s’applique à toutes les mesures au niveau du client, telles que `Customer's lifetime revenue` ou `Customer's lifetime number of orders`.

Dans l’image 2 ci-dessus, vous pouvez voir qu’il existe une valeur nulle `customer\_ids` dans le `orders` table. Si nous utilisons la variable `customer\_email` pour identifier des clients uniques, vous pouvez constater que `erin@test.com` a passé trois (3) commandes. Par conséquent, nous pouvons créer une `New customers` sur votre `orders` table basée sur les conditions suivantes :

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
