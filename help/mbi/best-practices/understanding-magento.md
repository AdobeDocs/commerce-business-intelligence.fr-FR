---
title: Compréhension  [!DNL Commerce Intelligence]  votre environnement
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

La plupart de vos tableaux contiennent une colonne nommée `entity\_id`. Dans chaque tableau contenant une `entity\_id`, cette colonne est utilisée pour identifier les lignes uniques.

Par exemple, chaque ligne du tableau `sales\_order` est un ordre unique. La clé primaire de ce tableau est appelée `entity\_id`. Cette colonne peut être considérée comme `order\_id`. Dans un tableau distinct, `customer\_entity`, chaque ligne représente un client unique. La clé primaire de ce tableau est également appelée `entity\_id`, ce qui peut être considéré comme `customer\_id`.

Dans ces tableaux, `sales\_order.entity\_id` n’est pas égal à `customer\_entity.entity\_id`. Cela vaut pour tous les ensembles de tables contenant des `entity\_id` : `table\_A.entity\_id` n’est pas égal à `table\_B.entity\_id`.

## [!DNL Guest orders]

Si vous autorisez les clients à commander sur votre site sans avoir de compte (commandes d’invités), ces clients ne sont pas renseignés sous forme de ligne dans votre tableau de `customer\_entity`. En outre, chaque commande passée par un invité a une valeur de `customer\_id` nulle sur la table `sales\_order`.

Par conséquent, si vous souhaitez suivre les comportements de vos invités au fil du temps, toutes les colonnes au niveau du client doivent être calculées sur la table `sales\_order`, à l’aide d’un identifiant client tel que `customer\_email`.

Si vous utilisez la table `sales\_order` comme table des clients, vous devez faire attention lors de la création de mesures au niveau du client. Prenons l’exemple d’une mesure de chiffre d’affaires durée de vie moyenne. Cette mesure est utilisée pour identifier le chiffre d’affaires moyen sur la durée de vie de votre base de clients. Cela nécessite tout d’abord une nouvelle colonne qui, pour chaque client, renvoie son chiffre d’affaires cumulé. Vous devez ensuite calculer la moyenne de cette colonne pour obtenir le chiffre d’affaires moyen sur toute la durée de vie de vos clients.

Si vous pouvez utiliser le tableau `customer\_entity`, chaque ligne correspond à un seul client et chaque client n&#39;existe dans ce tableau qu&#39;une seule fois. Par conséquent, lorsque vous disposez de la colonne de chiffre d’affaires sur la durée de vie, il vous suffit de créer une mesure moyenne. Cependant, si vous utilisez la table `sales\_order` comme table des clients, un client peut potentiellement exister dans de nombreuses lignes. Après avoir configuré la colonne du chiffre d’affaires cumulé, chaque commande (ligne) passée par un client donné affichera le chiffre d’affaires cumulé de ce client, mais vous ne souhaitez inclure ce client qu’une seule fois dans votre mesure moyenne globale.

L’astuce ici consiste à ajouter un filtre à votre mesure afin de ne pouvoir inclure chaque client qu’une seule fois. Adobe vous encourage à créer et à utiliser un jeu de filtres nommé **Clients que nous comptabilisons** qui filtre pour **Numéro de commande du client = 1** (parmi d’autres filtres, vous devrez peut-être exclure les clients indésirables). L’ajout de ce filtre vous garantit de n’inclure qu’une seule fois chaque client dans une mesure au niveau du client.

## Produits et catégories

Les produits peuvent avoir plusieurs catégories, et les catégories peuvent être utilisées pour plusieurs produits. Par conséquent, lors de la configuration d’analyses au niveau des catégories, vous devez veiller à utiliser les définitions correctes. Voulez-vous la catégorie de niveau supérieur ? Catégorie de deuxième niveau ? Que se passe-t-il si le produit peut appartenir à plusieurs catégories de niveau supérieur ?

Imaginez une paire de jeans appartenant à trois niveaux de catégorie différents, tels que définis par une implémentation de Commerce : « Vêtements » (niveau supérieur), « Vêtements d&#39;extérieur » (deuxième niveau) et « Pantalons » (troisième niveau). Vous pouvez analyser les performances de vos catégories par nombre d&#39;unités vendues. La mesure dont vous avez besoin pour cette analyse est _Articles vendus_, qui est basée sur le tableau `sales\_order\_item`. Par conséquent, vous devez déplacer les informations au niveau de la catégorie vers le tableau des éléments. Chaque ligne du tableau `sales\_order\_item` est associée à une `product\_id`. Par conséquent, si vous connaissez les catégories associées à un produit, vous pouvez apporter ces informations au tableau souhaité.

Avant de déplacer des données, vous devez d’abord connaître les jointures et les filtres appropriés pour vous assurer d’obtenir la catégorie appropriée. Pour certaines analyses, vous devrez peut-être connaître le mot « pantalon », mais dans d&#39;autres analyses, le mot « vêtement » pourrait être plus approprié. Il s’agit de catégories distinctes qui sont identifiées séparément. Savoir comment chaque niveau de catégorie est défini vous permet d’attribuer des ventes unitaires à la catégorie appropriée pour votre analyse spécifique.

Maintenant, imaginez que vous ayez également une `Our Favorites` catégorie de niveau supérieur sur la page d’accueil de votre site web. Vous avez peut-être implémenté votre boutique Commerce pour inclure ces jeans dans la catégorie `Clothing` et la catégorie `Our Favorites`. Si oui, cette paire de jeans a plus d&#39;une catégorie de premier niveau. Dans ce cas, il n’est pas très logique de déplacer une seule catégorie de niveau supérieur vers le tableau `sales\_order\_item`, car il existe plusieurs options. Pour en tenir compte, Adobe suggère de créer des colonnes Oui/Non qui vérifient des catégories spécifiques. Par exemple, les colonnes `Is product in Clothing category?` et `Is product in Our Favorites category?` vous permettent de vérifier si un produit appartient à ces catégories spécifiques.
