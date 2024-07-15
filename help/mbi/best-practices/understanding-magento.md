---
title: Présentation de votre environnement  [!DNL Commerce Intelligence]
description: Découvrez comment utiliser et améliorer votre environnement  [!DNL Commerce Intelligence] .
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---

# Votre environnement [!DNL Adobe Commerce Intelligence]

Lorsque vous analysez vos données commerciales, tenez compte de ces facteurs et des idées fausses courantes. Si vous avez besoin d’aide pour vous assurer que vous utilisez correctement votre schéma Commerce, n’hésitez pas à [contacter l’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## [!DNL entity\_id]

La plupart de vos tables contiennent une colonne nommée `entity\_id`. Dans chaque table contenant un `entity\_id`, cette colonne est utilisée pour identifier des lignes uniques.

Par exemple, chaque ligne de la table `sales\_order` est un ordre unique. La clé primaire de cette table est appelée `entity\_id`. Cette colonne peut être considérée comme `order\_id`. Dans un tableau distinct, `customer\_entity`, chaque ligne représente un client unique. La clé primaire de cette table est également appelée `entity\_id`, qui peut être considérée comme `customer\_id`.

Dans ces tables, `sales\_order.entity\_id` n&#39;est pas égal à `customer\_entity.entity\_id`. Cela est vrai pour tous les ensembles de tables contenant `entity\_id` : `table\_A.entity\_id` n’est pas égal à `table\_B.entity\_id`.

## [!DNL Guest orders]

Si vous autorisez les clients à commander sur votre site sans avoir de compte (commandes d’invités), ces clients ne sont pas renseignés en ligne dans votre table `customer\_entity`. En outre, chaque commande placée par un invité a une valeur `customer\_id` null sur la table `sales\_order`.

Par conséquent, si vous souhaitez suivre le comportement de vos invités au fil du temps, toutes les colonnes au niveau du client doivent être calculées sur la table `sales\_order`, à l’aide d’un identifiant de client tel que `customer\_email`.

Si vous utilisez la table `sales\_order` comme table client, vous devez ensuite être prudent lors de la création de mesures au niveau client. Prenons l’exemple d’une mesure de recettes sur la durée de vie moyenne. Cette mesure permet d’identifier les recettes de durée de vie moyenne pour votre base de clients. Cela nécessite tout d’abord une nouvelle colonne qui, pour chaque client, renvoie les recettes de sa durée de vie. Vous devez ensuite utiliser la moyenne de cette colonne pour obtenir les recettes de durée de vie moyenne de vos clients.

Si vous pouvez utiliser la table `customer\_entity`, chaque ligne est un seul client et chaque client n’existe dans ce tableau qu’une seule fois. Par conséquent, lorsque vous disposez de la colonne des recettes de la durée de vie, il vous suffit de créer une mesure moyenne. Cependant, si vous utilisez la table `sales\_order` comme table client, un client peut potentiellement exister dans de nombreuses lignes. Après avoir configuré la colonne des recettes sur la durée de vie, chaque commande (ligne) placée par un client donné indique les recettes sur la durée de vie du client ; mais vous ne souhaitez inclure ce client qu’une seule fois dans votre mesure moyenne globale.

L’astuce est que vous devez ajouter un filtre à votre mesure afin de n’inclure chaque client qu’une seule fois. Adobe vous encourage à créer et à utiliser un jeu de filtres nommé **Clients que nous comptons** qui filtre le **numéro de commande du client = 1** (parmi d’autres filtres, vous devrez peut-être exclure les clients indésirables). L’ajout de ce filtre permet de n’inclure chaque client qu’une seule fois dans une mesure au niveau du client.

## Produits et catégories

Les produits peuvent comporter plusieurs catégories et les catégories peuvent être utilisées pour plusieurs produits. Par conséquent, lors de la configuration des analyses au niveau de la catégorie, vous devez veiller à utiliser les définitions correctes. Voulez-vous la catégorie de niveau supérieur ? Catégorie de second niveau ? Que se passe-t-il si le produit peut appartenir à plusieurs catégories de niveau supérieur ?

Imaginez une paire de jeans qui se divise en trois niveaux de catégorie différents, comme défini par une mise en oeuvre de Commerce : &#39;Vêtements&#39; (niveau supérieur), &#39;Outerwear&#39; (deuxième niveau) et &#39;Pants&#39; (troisième niveau). Vous souhaiterez peut-être analyser les performances de vos catégories par nombre d&#39;unités vendues. La mesure dont vous avez besoin pour cette analyse est _Éléments vendus_, qui est créée sur la table `sales\_order\_item`. Par conséquent, vous devez déplacer les informations au niveau de la catégorie sur le tableau d’éléments. Chaque ligne de la table `sales\_order\_item` est associée à un `product\_id`. Par conséquent, si vous connaissez les catégories associées à un produit, vous pouvez transmettre ces informations à la table souhaitée.

Avant de déplacer des données, vous devez d’abord connaître les jointures et les filtres appropriés pour vous assurer que vous attrapez la catégorie appropriée. Pour certaines analyses, vous devrez peut-être connaître &quot;Pantalon&quot;, mais dans d’autres analyses, &quot;Vêtements&quot; pourrait être plus approprié. Il s’agit de catégories distinctes qui sont identifiées séparément. Connaître la définition de chaque niveau de catégorie vous permet d’attribuer les ventes unitaires à la catégorie appropriée pour votre analyse spécifique.

Maintenant, imaginez que vous ayez également une catégorie de niveau supérieur `Our Favorites` sur la page d’accueil de votre site web. Vous avez peut-être implémenté votre boutique Commerce pour inclure ces jeans dans la catégorie `Clothing` et la catégorie `Our Favorites`. Si c&#39;est le cas, ce jean a plus d&#39;une catégorie supérieure. Dans ce cas, déplacer une seule catégorie de niveau supérieur vers la table `sales\_order\_item` n’a pas de sens, car il existe plusieurs options. Pour en tenir compte, Adobe propose de créer des colonnes oui/non qui vérifient des catégories spécifiques. Par exemple, les colonnes `Is product in Clothing category?` et `Is product in Our Favorites category?` vous permettent de vérifier si un produit appartient à ces catégories spécifiques.
