---
title: Build[!DNL Google ECommerce]dimensions
description: Découvrez comment créer des dimensions qui relient vos données eCommerce à vos commandes et données client.
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 0%

---

# Build [!DNL Google ECommerce] Dimensions

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../administrator/user-management/user-management.md).

Maintenant que vous avez terminé [connexion[!DNL Google ECommerce]account](../../data-analyst/importing-data/integrations/google-ecommerce.md), que pouvez-vous faire avec ces données dans [!DNL MBI]? Cet article vous guide tout au long de la création de dimensions qui relient vos données eCommerce à vos commandes et données client.

Les dimensions abordées vous permettent de créer des analyses qui [répondre à des questions essentielles sur vos canaux marketing et campagnes ;](../../data-analyst/analysis/most-value-source-channel.md). Quel pourcentage des recettes provient de chaque source ? Comparaison de la valeur de durée de vie des clients acquis par Facebook par rapport à celle de [!DNL Google]?

## Prérequis et présentation

Pour créer des dimensions dans cet article, vous devez disposer d’un [!DNL Google ECommerce] , une `orders` et un `customers` table. Ces tables doivent être [synchronisé à votre Data Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) avant que les dimensions ne puissent être créées. Les tableaux synchronisés s’affichent dans la variable `Synced Tables` de la section `Data Warehouse Manager`.

Voici un aperçu rapide de la synchronisation des tableaux et des colonnes si vous avez besoin d’une actualisation :

![](../../assets/Syncing_New_Columns.gif)

Après avoir créé une jointure à partir de la fonction `orders` au [!DNL Google eCommerce] vous créez les trois premières dimensions dans la liste ci-dessous. Ensuite, vous utilisez ces dimensions pour créer trois dimensions utilisateur/client dans la variable `customers` table. Pour terminer, vous pouvez joindre ces colonnes au `orders` table.

Voici les dimensions couvertes :

* **Table des commandes**

* Commande [!DNL Google Analytics] source
* Commande [!DNL Google Analytics] medium
* Commande [!DNL Google Analytics]Une campagne
* Première commande du client [!DNL Google Analytics] source
* Première commande du client [!DNL Google Analytics] medium
* Première commande du client [!DNL Google Analytics] campaign

* **Table des clients**

* Première commande du client [!DNL Google Analytics] source
* Première commande du client [!DNL Google Analytics] medium
* Première commande du client [!DNL Google Analytics] campaign

## Création des dimensions

Pour créer des dimensions, ouvrez le [Gestionnaire de Data Warehouse](../data-warehouse-mgr/tour-dwm.md) en cliquant **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### Table des commandes, round 1

Cet exemple crée la variable **Commande [!DNL Google Analytics] Source** dimension.

1. Dans la liste des tableaux du Data Warehouse, cliquez sur le tableau (ici : `orders`) qui contient les informations sur votre commande.
1. Cliquez sur **[!UICONTROL Create a Column]**.
1. Attribuez un nom à la colonne.
1. Sélectionner `Joined Column` de la [liste déroulante de définitions](../data-warehouse-mgr/calc-column-types.md). Cet exemple fonctionne avec un [relation un-à-un](../data-warehouse-mgr/table-relationships.md), correspondant au `eCommerce.transactionID` à une seule ligne de la colonne `orders` table.
1. Vous devez ensuite définir le chemin ou la manière dont le tableau et la colonne utilisés sont connectés. Cliquez sur le bouton `Select a table and column` menu déroulant.
1. Le chemin dont vous avez besoin n’est pas disponible. Vous devez donc en créer un nouveau. Cliquez sur **[!UICONTROL Create new Path]**.
1. Dans la fenêtre qui s’affiche, définissez la variable `Many` côté à `orders.order\_id`ou de la colonne dans la variable `orders` qui contient l’identifiant de commande.
1. Sur le `One` , recherchez la variable `Google ECommerce` , puis définissez la colonne sur `transactionID`.

   ![](../../assets/google-ecommerce-table.png)

1. Cliquez sur **[!UICONTROL Save]** pour créer le chemin.
1. Une fois le chemin ajouté, cliquez sur le bouton **[!UICONTROL Select table and column]** à nouveau.
1. Recherchez la variable `ECommerce` puis cliquez sur le bouton `Source` colonne . Cela lie les commandes aux informations source.
1. Une fois que vous êtes revenu dans le schéma de la table, cliquez sur **[!UICONTROL Save]** pour créer à nouveau la dimension.

Voici un aperçu de l’ensemble du processus :

![](../../assets/help_center.gif)

Essayez ensuite de créer **Commande [!DNL Google Analytics] medium** et `campaign`. Peu de changements pour ces dimensions, essayez-le. Mais si vous êtes coincé, vous pouvez vérifier [la fin de cet article](#stuck) pour voir ce qui est différent.

### Table des clients {#customers}

Cet exemple crée la variable **Première commande du client [!DNL Google Analytics] source** dimension.

1. Dans la liste des tableaux du Data Warehouse, cliquez sur le tableau (ici : `customers`) qui contient les informations sur vos clients.
1. Cliquez sur **[!UICONTROL Create a Column]**.
1. Attribuez un nom à la colonne.
1. Dans cet exemple, sélectionnez l’option `is MAX` à partir de la définition [liste déroulante de définitions](../../data-analyst/data-warehouse-mgr/calc-column-types.md). Le `is MIN` La définition peut également fonctionner si elle est appliquée à une colonne de texte avec une seule valeur possible. L’important est de s’assurer que les filtres appropriés sont définis, ce que vous faites plus tard.
1. Cliquez sur le bouton **[!UICONTROL Select a table and column]** et sélectionnez l’option `orders` , puis le `Order's [!DNL Google Analytics] source` colonne .
1. Cliquez sur **[!UICONTROL Save]**.
1. Une fois que vous êtes revenu dans le schéma de la table, cliquez sur le bouton `Options` menu déroulant, puis `Filters`.
1. Cliquez sur **[!UICONTROL Add Filter Set]** puis sélectionnez l’option `Orders we count` définie. Vous souhaitez que seules les commandes incluses dans les commandes que vous comptabilisez soient incluses. Il est donc important que cet ensemble de filtres soit sélectionné.
1. Cliquez sur **[!UICONTROL Add Filter]**. Vous souhaitez trouver le [!DNL Google Analytics] source, vous devez donc ajouter un filtre :

   _orders.Numéro de commande du client = 1

   _
1. Cliquez sur **[!UICONTROL Save]** pour créer la dimension.

Essayez ensuite de créer **Première commande du client [!DNL Google Analytics] medium** et `campaign`. Peu de changements pour ces dimensions, essayez-le. Mais si vous êtes coincé, vous pouvez vérifier [la fin de cet article](#stuck) pour voir ce qui est différent.

### Bonus : Table des commandes, 2e tour

Vous pouvez vous arrêter ici si vous le souhaitez, mais cette section permet une analyse plus approfondie en apportant la variable **Première commande du client [!DNL Google Analytics] dimensions** que vous avez créé dans la variable [dernière section](#customers) dans la `orders` table. La création de dimensions dans cette section vous permet d’analyser toutes les mesures créées sur votre `orders` table - `Revenue`, `Number of orders`, `Distinct buyers`, etc. - à l’aide de la fonction [!DNL Google Analytics] attributs de la première commande d’un client.

Cet exemple joint le `Customer's first order's [!DNL Google Analytics] source` à la dimension `orders` table.

1. Dans la liste des tableaux du Data Warehouse, cliquez sur le tableau (ici : `orders`) qui contient les informations sur votre commande.
1. Cliquez sur **[!UICONTROL Create a Column]**.
1. Attribuez un nom à la colonne.
1. Sélectionner `Joined Column` dans la liste déroulante des définitions. Cette opération associe les dimensions client que vous avez créées dans la section précédente au `orders` table.
1. Cliquez sur le bouton **[!UICONTROL Select a table and column]** , puis sélectionnez la variable `customers` et le `Customer's first order's [!DNL Google Analytics] source` colonne .
1. Si un chemin n’est pas automatiquement renseigné, sélectionnez le chemin qui connecte le mieux les clients et les tables de commandes.
1. Cliquez sur **[!UICONTROL Save]** pour créer la dimension.

Voici un aperçu de l’ensemble du processus :

![](../../assets/help_center2.gif)

Terminez en rejoignant la section `Customer's first order's` medium et `campaign` aux dimensions `orders` table. Rejoindre les dimensions et, en cas de problème, extraire [la fin de l’article ;](#stuck) si vous avez besoin d&#39;aide.

### Remplissage

Vous avez fini de créer les dimensions, ce qui signifie que vous pouvez désormais créer des analyses puissantes qui effectuent le suivi des performances de vos différents canaux et campagnes. N’oubliez pas que la variable **de nouvelles colonnes ne seront disponibles qu’une fois la prochaine mise à jour terminée.**.

Certaines des dimensions les plus populaires sont abordées dans cet article, mais le ciel est la limite - essayez de créer la vôtre ou n’hésitez pas à nous envoyer un ping si vous voulez de l’aide pour explorer d’autres options. 

### Je suis coincé ! Qu&#39;est-ce qui est différent ? {#stuck}

**`Orders`table #1 :** Lors de la création de la variable `Order's [!DNL Google Analytics]` medium et `campaign` dimensions, la différence est les colonnes sélectionnées à l’étape 12. Dans cet exemple, la colonne était `Source`.

**`Customers`table :** Lors de la création de la variable `Customer's first order's [!DNL Google Analytics]` medium et `campaign` dimensions, la différence est les colonnes sélectionnées à l’étape 5. Dans cet exemple, la colonne était `Order's [!DNL Google Analytics]` source.

**`Orders`table #2 :** Lorsque vous rejoignez la `Customer's first order's [!DNL Google Analytics]` medium et `campaign` aux colonnes `orders` , la différence réside dans les colonnes sélectionnées à l’étape 5. Dans cet exemple, la colonne était `Customer's first order's [!DNL Google Analytics]` source.
