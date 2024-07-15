---
title: Construire[!DNL Google ECommerce] dimensions
description: Découvrez comment créer des dimensions qui relient vos données eCommerce à vos commandes et données client.
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# Créer [!DNL Google ECommerce] Dimensions

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../administrator/user-management/user-management.md).

Maintenant que vous avez fini de [connecter votre compte[!DNL Google ECommerce]](../../data-analyst/importing-data/integrations/google-ecommerce.md), que pouvez-vous faire avec ces données dans [!DNL Commerce Intelligence] ? Cette rubrique vous guide tout au long de la création de dimensions qui relient vos données eCommerce à vos commandes et données client.

Les dimensions traitées vous permettent de créer des analyses qui [ répondent à des questions essentielles sur vos canaux et campagnes marketing ](../../data-analyst/analysis/most-value-source-channel.md). Quel pourcentage des recettes provient de chaque source ? Comment la valeur de durée de vie de [!DNL Facebook] clients acquis se compare-t-elle à celle de [!DNL Google] ?

## Prérequis et présentation

Pour créer les dimensions dans cette rubrique, vous avez besoin d’une table [!DNL Google ECommerce], d’une table `orders` et d’une table `customers`. Ces tables doivent être [synchronisées avec votre Data Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) pour que les dimensions puissent être créées. Les tableaux synchronisés s’affichent dans la section `Synced Tables` de `Data Warehouse Manager`.

Voici un aperçu rapide de la synchronisation des tableaux et des colonnes si vous avez besoin d’une actualisation :

![](../../assets/Syncing_New_Columns.gif)

Après avoir créé une jointure entre la table `orders` et la table [!DNL Google eCommerce], vous créez les trois premières dimensions dans la liste ci-dessous. Ensuite, vous utilisez ces dimensions pour créer trois dimensions utilisateur/client dans le tableau `customers`. Pour terminer, vous pouvez joindre ces colonnes à la table `orders`.

Voici les dimensions couvertes :

* **Table des commandes**

* Source [!DNL Google Analytics] de la commande
* Support [!DNL Google Analytics] de la commande
* Campagne [!DNL Google Analytics]d&#39;une commande
* Source [!DNL Google Analytics] de la première commande du client
* [!DNL Google Analytics] support de première commande du client
* Campagne [!DNL Google Analytics] de première commande du client

* **Table des clients**

* Source [!DNL Google Analytics] de la première commande du client
* [!DNL Google Analytics] support de première commande du client
* Campagne [!DNL Google Analytics] de première commande du client

## Construire les dimensions

Pour créer des dimensions, ouvrez le [Gestionnaire de Data Warehouse](../data-warehouse-mgr/tour-dwm.md) en cliquant sur **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### Table des commandes, round 1

Cet exemple crée la dimension **Source [!DNL Google Analytics] de commande**.

1. Dans la liste des tables du Data Warehouse, cliquez sur la table (ici, `orders`) contenant les informations de commande.
1. Cliquez sur **[!UICONTROL Create a Column]**.
1. Attribuez un nom à la colonne.
1. Sélectionnez `Joined Column` dans la liste déroulante [définition](../data-warehouse-mgr/calc-column-types.md). Cet exemple fonctionne avec une [relation un-à-un](../data-warehouse-mgr/table-relationships.md), faisant correspondre la colonne `eCommerce.transactionID` à exactement une ligne de la table `orders`.
1. Vous devez ensuite définir le chemin ou la manière dont le tableau et la colonne utilisés sont connectés. Cliquez sur la liste déroulante `Select a table and column` .
1. Le chemin dont vous avez besoin n’est pas disponible. Vous devez donc en créer un nouveau. Cliquez sur **[!UICONTROL Create new Path]**.
1. Dans la fenêtre qui s’affiche, définissez le côté `Many` sur `orders.order\_id` ou la colonne dans la table `orders` qui contient l’identifiant de commande.
1. Sur le côté `One`, recherchez la table `Google ECommerce`, puis définissez la colonne sur `transactionID`.

   ![](../../assets/google-ecommerce-table.png)

1. Cliquez sur **[!UICONTROL Save]** pour créer le chemin.
1. Une fois le chemin ajouté, cliquez de nouveau sur la liste déroulante **[!UICONTROL Select table and column]** .
1. Recherchez la table `ECommerce`, puis cliquez sur la colonne `Source`. Cela lie les commandes aux informations source.
1. Une fois que vous êtes revenu dans le schéma de table, cliquez de nouveau sur **[!UICONTROL Save]** pour créer la dimension.

Voici un aperçu de l’ensemble du processus :

![](../../assets/help_center.gif)

Essayez ensuite de créer **Order&#39;s [!DNL Google Analytics] medium** et `campaign`. Peu de changements pour ces dimensions, essayez-le. Mais si vous êtes bloqué, vous pouvez extraire [la fin de cet article](#stuck) pour voir ce qui est différent.

### Table des clients {#customers}

Cet exemple crée la dimension [!DNL Google Analytics] source **de la** première commande du client.

1. Dans la liste des tables du Data Warehouse, cliquez sur la table (ici, `customers`) contenant les informations sur votre client.
1. Cliquez sur **[!UICONTROL Create a Column]**.
1. Attribuez un nom à la colonne.
1. Pour cet exemple, sélectionnez la définition `is MAX` dans la liste déroulante [définition](../../data-analyst/data-warehouse-mgr/calc-column-types.md). La définition `is MIN` peut également fonctionner si elle est appliquée à une colonne de texte avec une seule valeur possible. L’important est de s’assurer que les filtres appropriés sont définis, ce que vous faites plus tard.
1. Cliquez sur la liste déroulante **[!UICONTROL Select a table and column]** et sélectionnez la table `orders`, puis la colonne `Order's [!DNL Google Analytics] source`.
1. Cliquez sur **[!UICONTROL Save]**.
1. Une fois que vous êtes revenu dans le schéma de la table, cliquez sur la liste déroulante `Options`, puis `Filters`.
1. Cliquez sur **[!UICONTROL Add Filter Set]**, puis sélectionnez l’ensemble `Orders we count`. Vous souhaitez que seules les commandes incluses dans les commandes que vous comptabilisez soient incluses. Il est donc important que cet ensemble de filtres soit sélectionné.
1. Cliquez sur **[!UICONTROL Add Filter]**. Vous souhaitez trouver la source [!DNL Google Analytics] de la première commande du client. Vous devez donc ajouter un filtre :

   _orders.Numéro de commande du client = 1

   _
1. Cliquez sur **[!UICONTROL Save]** pour créer la dimension.

Essayez ensuite de créer **le [!DNL Google Analytics] support** et `campaign` de la première commande du client. Peu de changements pour ces dimensions, essayez-le. Mais si vous êtes bloqué, vous pouvez extraire [la fin de cet article](#stuck) pour voir ce qui est différent.

### Bonus : table des commandes, 2e tour

Vous pouvez vous arrêter ici si vous le souhaitez, mais cette section permet une analyse plus approfondie en apportant les **dimensions [!DNL Google Analytics] de première commande du client** que vous avez créées dans la [dernière section](#customers) dans la table `orders`. La création de dimensions dans cette section vous permet d’analyser toutes les mesures créées sur votre table `orders` - `Revenue`, `Number of orders`, `Distinct buyers`, etc. - à l’aide des attributs [!DNL Google Analytics] de la première commande d’un client.

Cet exemple joint la dimension `Customer's first order's [!DNL Google Analytics] source` à la table `orders`.

1. Dans la liste des tables du Data Warehouse, cliquez sur la table (ici, `orders`) contenant les informations de commande.
1. Cliquez sur **[!UICONTROL Create a Column]**.
1. Attribuez un nom à la colonne.
1. Sélectionnez `Joined Column` dans la liste déroulante de définitions. Cette opération associe les dimensions client que vous avez créées dans la section précédente au tableau `orders`.
1. Cliquez sur la liste déroulante **[!UICONTROL Select a table and column]** , puis sélectionnez la table `customers` et la colonne `Customer's first order's [!DNL Google Analytics] source` .
1. Si un chemin n’est pas automatiquement renseigné, sélectionnez le chemin qui connecte le mieux les clients et les tables de commandes.
1. Cliquez sur **[!UICONTROL Save]** pour créer la dimension.

Voici un aperçu de l’ensemble du processus :

![](../../assets/help_center2.gif)

Terminez en joignant les dimensions `Customer's first order's` moyenne et `campaign` à la table `orders`. Rejoignez les dimensions et en cas de problème, puis extrayez [la fin de l’article](#stuck) si vous avez besoin d’aide.

### Remplissage

Vous avez fini de créer les dimensions, ce qui signifie que vous pouvez désormais créer des analyses puissantes qui effectuent le suivi des performances de vos différents canaux et campagnes. N’oubliez pas que les **nouvelles colonnes ne seront pas disponibles tant que la prochaine mise à jour n’aura pas été terminée**.

Certaines des dimensions les plus populaires sont abordées dans ce sujet, mais le ciel est la limite - essayez de créer la vôtre ou n’hésitez pas à nous envoyer un ping si vous voulez de l’aide pour explorer d’autres options. 

### Remarques supplémentaires

**`Orders`table #1** : lors de la création des dimensions `Order's [!DNL Google Analytics]` moyennes et `campaign`, la différence est les colonnes sélectionnées à l’étape 12. Dans cet exemple, la colonne était `Source`.

**`Customers`table** : lors de la création des dimensions `Customer's first order's [!DNL Google Analytics]` moyennes et `campaign`, la différence est les colonnes sélectionnées à l’étape 5. Dans cet exemple, la colonne était la source `Order's [!DNL Google Analytics]`.

**`Orders`table #2** : lors de l’association des colonnes `Customer's first order's [!DNL Google Analytics]` medium et `campaign` à la table `orders`, la différence est les colonnes sélectionnées à l’étape 5. Dans cet exemple, la colonne était la source `Customer's first order's [!DNL Google Analytics]`.
