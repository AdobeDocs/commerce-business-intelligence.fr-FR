---
title: Comprendre votre [!DNL Commerce Intelligence] Environnement
description: En savoir plus sur l’utilisation et l’amélioration de votre [!DNL Commerce Intelligence] environnement.
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---

# Votre [!DNL Adobe Commerce Intelligence] Environnement

Lorsque vous analysez vos données commerciales, tenez compte de ces facteurs et des idées fausses courantes. Si vous avez besoin d’aide pour vous assurer que vous utilisez correctement votre schéma Commerce, n’hésitez pas à [support technique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## [!DNL entity\_id]

La plupart de vos tableaux contiennent une colonne nommée `entity\_id`. Dans chaque tableau contenant un `entity\_id`, cette colonne est utilisée pour identifier les lignes uniques.

Par exemple, chaque ligne du `sales\_order` table est un ordre unique. La clé primaire de ce tableau est appelée `entity\_id`. Cette colonne peut être considérée comme `order\_id`. Dans une table séparée, `customer\_entity`, chaque ligne représente un client unique. La clé primaire de ce tableau est également appelée `entity\_id`, qui peut être considéré comme `customer\_id`.

Dans ces tableaux, `sales\_order.entity\_id` n’est pas égal à `customer\_entity.entity\_id`. Cela est vrai pour tous les ensembles de tables qui contiennent `entity\_id`: `table\_A.entity\_id` n’est pas égal à `table\_B.entity\_id`.

## [!DNL Guest orders]

Si vous autorisez les clients à commander sur votre site sans avoir de compte (commandes d’invités), ces clients ne sont pas renseignés en ligne dans votre `customer\_entity` table. En outre, chaque commande passée par un invité a une valeur nulle `customer\_id` sur la variable `sales\_order` table.

Par conséquent, si vous souhaitez suivre le comportement de vos invités au fil du temps, toutes les colonnes au niveau du client doivent être calculées sur la variable `sales\_order` table, à l’aide d’un identifiant de client, tel que `customer\_email`.

Si vous utilisez la variable `sales\_order` en tant que tableau client, vous devez ensuite être prudent lors de la création de mesures au niveau client. Prenons l’exemple d’une mesure de recettes sur la durée de vie moyenne. Cette mesure permet d’identifier les recettes de durée de vie moyenne pour votre base de clients. Cela nécessite tout d’abord une nouvelle colonne qui, pour chaque client, renvoie les recettes de sa durée de vie. Vous devez ensuite utiliser la moyenne de cette colonne pour obtenir les recettes de durée de vie moyenne de vos clients.

Si vous pouvez utiliser la variable `customer\_entity` , chaque ligne est un client unique et chaque client n’existe dans ce tableau qu’une seule fois. Par conséquent, lorsque vous disposez de la colonne des recettes de la durée de vie, il vous suffit de créer une mesure moyenne. Cependant, si vous utilisez la variable `sales\_order` tableau en tant que tableau client, un client peut potentiellement exister dans de nombreuses lignes. Après avoir configuré la colonne des recettes sur la durée de vie, chaque commande (ligne) placée par un client donné indique les recettes sur la durée de vie du client ; mais vous ne souhaitez inclure ce client qu’une seule fois dans votre mesure moyenne globale.

L’astuce est que vous devez ajouter un filtre à votre mesure afin de n’inclure chaque client qu’une seule fois. Adobe vous encourage à créer et à utiliser un jeu de filtres nommé **Clients que nous comptons** qui filtre pour **Numéro de commande du client = 1** (entre autres filtres, vous devrez peut-être exclure les clients indésirables). L’ajout de ce filtre permet de n’inclure chaque client qu’une seule fois dans une mesure au niveau du client.

## Produits et catégories

Les produits peuvent comporter plusieurs catégories et les catégories peuvent être utilisées pour plusieurs produits. Par conséquent, lors de la configuration des analyses au niveau de la catégorie, vous devez veiller à utiliser les définitions correctes. Voulez-vous la catégorie de niveau supérieur ? Catégorie de second niveau ? Que se passe-t-il si le produit peut appartenir à plusieurs catégories de niveau supérieur ?

Imaginez une paire de jeans qui se divise en trois niveaux de catégorie différents, comme défini par une implémentation Commerce : &#39;Vêtements&#39; (niveau supérieur), &#39;Outerwear&#39; (deuxième niveau) et &#39;Pants&#39; (troisième niveau). Vous souhaiterez peut-être analyser les performances de vos catégories par nombre d&#39;unités vendues. La mesure dont vous avez besoin pour cette analyse est : _Articles vendus_, qui repose sur la fonction `sales\_order\_item` table. Par conséquent, vous devez déplacer les informations au niveau de la catégorie sur le tableau d’éléments. Chaque ligne du `sales\_order\_item` est associée à un tableau `product\_id`, donc si vous connaissez les catégories associées à un produit, vous pouvez transmettre ces informations au tableau souhaité.

Avant de déplacer des données, vous devez d’abord connaître les jointures et les filtres appropriés pour vous assurer que vous attrapez la catégorie appropriée. Pour certaines analyses, vous devrez peut-être connaître &quot;Pantalon&quot;, mais dans d’autres analyses, &quot;Vêtements&quot; pourrait être plus approprié. Il s’agit de catégories distinctes qui sont identifiées séparément. Connaître la définition de chaque niveau de catégorie vous permet d’attribuer les ventes unitaires à la catégorie appropriée pour votre analyse spécifique.

Maintenant, imaginez que vous ayez aussi une `Our Favorites` catégorie de niveau supérieur sur la page d’accueil de votre site web. Vous avez peut-être mis en oeuvre votre boutique Commerce pour inclure ces jeans dans les deux `Clothing` et la catégorie `Our Favorites` catégorie. Si c&#39;est le cas, ce jean a plus d&#39;une catégorie supérieure. Dans ce cas, le déplacement d’une seule catégorie de niveau supérieur vers le `sales\_order\_item` n’a pas tout à fait de sens, car il existe plusieurs options. Pour en tenir compte, Adobe propose de créer des colonnes oui/non qui vérifient des catégories spécifiques. Par exemple : `Is product in Clothing category?` et `Is product in Our Favorites category?` vous permet de vérifier si un produit appartient à ces catégories spécifiques.
