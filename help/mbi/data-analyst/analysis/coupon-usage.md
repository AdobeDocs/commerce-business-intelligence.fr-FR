---
title: Analyse de l’utilisation des coupons
description: Découvrez comment analyser l’utilisation des coupons pour acquérir et retenir des clients.
exl-id: d4d1393f-1695-43f2-980a-84525f84031e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 2%

---

# Utilisation du coupon

Vous demandez-vous quel impact a l’offre de coupons sur votre activité ? Vous souhaitez savoir quels coupons aident ou nuisent aux performances ? Dans cet article, nous explorons des analyses qui vous donnent une bonne image de l’utilisation des coupons de vos clients en répondant à ces questions :

* Combien de clients utilisent des coupons ?
* Combien de coupons sont utilisés ?
* Quelles sont vos recettes avant et après l’application des coupons ?
* Quelle est la valeur moyenne de la commande avant et après l’application des coupons ?
* Quel type de clients attirez-vous avec des coupons ?

Commençons !

## Mesures recommandées {#metrics}

Lorsque vous analysez l’utilisation des coupons, pensez à utiliser ([ou construction](../../data-user/reports/ess-manage-data-metrics.md)) ces mesures :

### Nombre de commandes

Cette mesure indique le nombre de commandes avec et sans coupons au fil du temps. Cela indique si et à quelle fréquence les clients utilisent vos coupons, et comment cela change au fil du temps.

### Chiffre d’affaires brut

Cette mesure révèle les recettes brutes que vous obtenez des commandes qui incluent un coupon particulier. Le chiffre d’affaires brut est un calcul du prix total des articles vendus, avant toute remise. Cela peut vous aider à déterminer quels coupons sont associés aux recettes brutes les plus élevées et les plus faibles.

### Remises sur les coupons

Cette mesure peut vous indiquer le montant total de remise appliqué par les coupons. il est important de noter que ces commandes n’ont peut-être pas eu lieu sans les coupons.

### Chiffre d’affaires net

Cette mesure indique les recettes nettes que vous obtenez des commandes qui incluent un coupon particulier. Le chiffre d’affaires net est un calcul du prix des articles vendus après l’application de toutes les remises. Cela peut vous aider à déterminer quels coupons sont associés aux recettes nettes les plus élevées et les plus faibles.

### Pourcentage de réduction

Vous affichez ainsi la part du revenu brut qui est compensée par des remises. Pour les coupons qui offrent une remise en pourcentage, cette valeur est déjà connue (par exemple, 10 % de réduction). Malgré cela, cette mesure fournit des informations et une méthode de comparaison pour les coupons qui sont une remise fixe en dollars.

### Valeur nette moyenne de la commande

Cette mesure affiche la valeur de commande moyenne lorsqu’un coupon est appliqué. Vous pouvez analyser si les commandes avec coupons ont toujours une valeur de commande inférieure à celle des commandes sans coupons.

### Réduction moyenne des commandes

Vous affichez ainsi la valeur en dollars moyen actualisée de chaque commande pour laquelle des coupons sont appliqués. Ceci affiche la différence entre la valeur de commande nette moyenne et la valeur de commande brute moyenne.

### Acheteurs distincts

Cette mesure affiche le nombre d’acheteurs distincts qui utilisent un certain coupon.

### Chiffre d’affaires moyen

Cette mesure permet d’évaluer la fidélité et les recettes moyennes générées par les clients qui utilisent un certain coupon. Lorsque vous évaluez si les clients qui utilisent des coupons ont une valeur supérieure à d’autres, veillez à tenir compte du nombre d’acheteurs distincts dans chaque catégorie pour vous assurer que vous disposez d’une taille d’échantillon significative.

## Exemple {#example}

Maintenant que nous savons quelles mesures examiner, prenons un exemple impliquant trois bons différents : 10 % de réduction, 20 $ de moins 100 $ et 10 $ de réduction.

| **Bon** | **Nombre de commandes** | **Chiffre d’affaires brut** | **Remises brutes sur les coupons** | **Chiffre d’affaires net** | **Pourcentage de réduction** |
|-----|-----|-----|-----|-----|-----|
| **10 % de remise** | 79 | $19,757.02 | $1,975.70 | $17,781.32 | 10.00% |
| **20 $ sur plus de 100 $** | 101 | $13,928.91 | $2,020.00 | $11,908.91 | 14.50% |
| **10 $ de réduction** | 201 | $14,542.35 | $2,010.00 | $12,532.35 | 13.82% |

{style=&quot;table-layout:auto&quot;}


| **Bon** | **Durée valeur nette de la commande** | **Durée réduction sur commande** | **Acheteurs distincts** | **Durée revenu total** |
|-----|-----|-----|-----|-----|
| **10 % de remise** | $225.08 | $25.01 | 79 | $361.50 |
| **20 $ sur plus de 100 $** | $117.91 | $20.00 | 95 | $218.76 |
| **10 $ de réduction** | $62.35 | $10.00 | 199 | $84.27 |

{style=&quot;table-layout:auto&quot;}

## Que pouvons-nous en retirer ?

Environ 80 commandes ont été passées avec le coupon &quot;10 % de réduction&quot;, 100 commandes avec le coupon &quot;20 $ de moins 100 $&quot; et 200 commandes avec le coupon &quot;10 $ de réduction&quot;. Le **nombre de commandes** Les attributs associés à chaque coupon peuvent varier en fonction de plusieurs facteurs, notamment :

* durée pendant laquelle les coupons ont été proposés.
* l’heure du jour/de la semaine/du mois/de l’année où les bons ont été proposés.
* la saison pendant laquelle les coupons ont été proposés, en fonction de l&#39;activité. Par exemple :
* Le coupon &quot;10% de réduction&quot; a été offert pendant les mois d&#39;été, mais l&#39;entreprise vend des vêtements d&#39;hiver.

* les restrictions sur les coupons. Par exemple :
* Le coupon &quot;$10 off&quot; n&#39;est offert qu&#39;aux nouveaux clients.
* Le coupon &quot;10% de réduction&quot; n&#39;est proposé qu&#39;aux clients qui achètent un manteau d&#39;hiver dans la même commande.

* le comportement d’achat typique du client.

Lorsque la variable **remises brutes** pour les trois coupons, le nombre de commandes de chacun d&#39;eux est sensiblement différent (environ 2 000 $). L’analyse des remises par commande permet d’expliquer les raisons de ces nombres contrastés. Le coupon &quot;10 % de réduction&quot; a le moins de commandes, mais un **réduction moyenne des commandes** de 25 dollars environ. Bien que ce coupon ait un petit nombre de commandes, sa valeur de remise moyenne élevée entraîne un montant de remise brut d’environ 2 000 $.

**Chiffre d&#39;affaires brut et net** fournissent une idée globale de la valeur complète des commandes associées à chaque coupon. Toutefois, cette image globale ne permet pas de comprendre les différents comportements liés à chaque coupon. Une fois que vous observez la base de la commande, vous pouvez constater que le coupon &quot;10 % de réduction&quot; est très élevé. **commande nette moyenne** qui, à son tour, mène à sa valeur élevée **revenu net**.

En revanche, le coupon &quot;10 % de réduction&quot; a une valeur de remise moyenne très élevée (25,01 $), mais la plus faible **pourcentage actualisé**. Cela est logique lorsque vous prenez en compte la valeur moyenne de la commande nette de 225,08 $. Le coupon &quot;10 % de réduction&quot; a une faible remise d’un pourcentage de la valeur moyenne de la commande nette, de sorte que la remise moyenne de la commande est un montant important.

Jetons un coup d’oeil au **acheteurs distincts** et **revenu moyen** pour chaque coupon. Le coupon &quot;10 % de réduction&quot; a le même nombre de commandes que les acheteurs distincts. Cela peut être dû au fait que chaque client est limité à un coupon. D’un autre côté, les coupons &quot;$20 de 100 $ ou plus&quot; et &quot;$10 de moins&quot; ont moins d’acheteurs distincts que le nombre de commandes, ce qui implique que certains clients ont utilisé ces coupons plusieurs fois.

Pour les recettes de durée de vie moyenne, vous pouvez constater que la moyenne des recettes sur la durée de vie de chaque coupon est supérieure aux recettes respectives. **commande nette moyenne** . Cela signifie que les clients ont effectué des achats répétés et/ou que leur valeur de commande était beaucoup plus élevée que la valeur de commande nette moyenne.

## Que puis-je analyser d&#39;autre ? {#otheranalyses}

Les analyses que nous avons abordées dans cet article peuvent vous donner un aperçu précieux de la manière dont vos clients utilisent vos coupons, mais il existe une multitude d’autres analyses qui vous permettent de creuser un peu plus en détail.

**Vous pouvez analyser les acquisitions de vos clients à partir de coupons.**

Quels coupons encouragent les clients à passer des commandes ? Ces bons attirent-ils des acheteurs uniques ou encouragent-ils la fidélité de la clientèle (c’est-à-dire des clients qui effectuent des achats répétés) ?

**Vous pouvez analyser le temps nécessaire à vos clients pour utiliser vos bons.**

Vos coupons sont-ils utilisés le jour de leur publication ou une semaine ou deux s’écoulent-ils avant que la majorité de vos clients ne les utilisent ?

**Vous pouvez découvrir le montant optimal de remise qui augmente la fidélité des clients et la valeur globale.**

Quel montant de remise encouragera les acheteurs réguliers, une valeur de commande moyenne plus élevée et des recettes de durée de vie plus élevées ?

Répondre à ces questions vous donnera des informations sur vos clients, leur comportement et les bons qui vous procurent le plus de valeur.
