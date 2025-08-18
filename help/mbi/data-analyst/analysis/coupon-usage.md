---
title: Analyse de l’utilisation des coupons
description: Découvrez comment analyser l’utilisation des coupons pour acquérir et fidéliser des clients.
exl-id: d4d1393f-1695-43f2-980a-84525f84031e
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 0%

---

# Utilisation des coupons

Vous êtes-vous déjà demandé comment l&#39;offre de coupons affecte votre entreprise ? Vous voulez savoir quels coupons aident ou nuisent à la performance ? Cette rubrique explore les analyses qui vous donnent une bonne idée de l’utilisation des coupons par vos clients en répondant aux questions suivantes :

* Combien de clients utilisent des coupons ?
* Combien de coupons sont utilisés ?
* Quel est votre chiffre d’affaires avant et après l’application des coupons ?
* Quelle est la valeur de commande moyenne avant et après l&#39;application des coupons ?
* Quel type de clients attirez-vous avec les coupons ?

## Mesures recommandées {#metrics}

Lors de l’analyse de l’utilisation des coupons, pensez à utiliser ([ou à créer](../../data-user/reports/ess-manage-data-metrics.md)) les mesures suivantes :

### Nombre de commandes

Cette mesure vous indique le nombre de commandes avec et sans coupons au fil du temps. Cela indique si et à quelle fréquence les clients utilisent vos coupons, et comment cela change au fil du temps.

### Chiffre d’affaires brut

Cette mesure révèle le chiffre d’affaires brut que vous tirez des commandes qui incluent un coupon particulier. Le revenu brut est un calcul du prix total des articles vendus, avant que des remises ne soient appliquées. Cela peut aider à déterminer quels coupons sont associés aux revenus bruts les plus élevés et les plus bas.

### Remises sur coupons

Cette mesure peut vous montrer le montant total de la remise appliquée à partir des coupons. Il est important de noter que ces commandes n&#39;auraient peut-être pas été effectuées sans les coupons.

### Chiffre d’affaires net

Cette mesure montre le revenu net que vous tirez des commandes qui incluent un coupon particulier. Le revenu net est un calcul du prix des articles vendus une fois toutes les remises appliquées. Cela peut aider à déterminer quels coupons sont associés aux revenus nets les plus élevés et les plus bas.

### Pourcentage de remise

Cela indique la part du revenu brut qui est compensée par des remises. Pour les coupons qui offrent une réduction en pourcentage, cette valeur est déjà connue (par exemple, 10 % de réduction). Malgré cela, cette mesure fournit insight et une méthode de comparaison pour les coupons qui sont une remise en dollars fixe.

### Valeur nette de commande moyenne

Cette mesure affiche la valeur de commande moyenne lors de l’application d’un coupon. Vous pouvez déterminer si les commandes avec coupons ont systématiquement une valeur de commande inférieure à celle des commandes sans coupons.

### Remise de commande moyenne

Cela indique la valeur moyenne en dollars actualisée de chaque commande pour laquelle des coupons sont appliqués. Cette option affiche la différence entre la valeur de commande nette moyenne et la valeur de commande brute moyenne.

### Acheteurs distincts

Cette mesure affiche le nombre d’acheteurs distincts qui utilisent un certain coupon.

### Chiffre d’affaires moyen sur la durée de vie

Cette mesure permet d’évaluer la fidélité et le chiffre d’affaires moyen générés par les clients qui utilisent un certain coupon. Lorsque vous évaluez si les clients qui utilisent des coupons ont une valeur supérieure aux autres, veillez à tenir compte du nombre d’acheteurs distincts dans chaque catégorie pour vous assurer que vous disposez d’une taille d’échantillon significative.

## Exemple {#example}

Maintenant que vous savez quels indicateurs examiner, prenez l’exemple de trois coupons différents : 10 % de réduction, 20 $ de réduction d’au moins 100 $ et 10 $ de réduction.

| **Bon** | **de commandes** | **Chiffre d’affaires brut** | **Remises brutes sur coupons** | **Chiffre d’affaires net** | **Pourcentage de remise** |
|-----|-----|-----|-----|-----|-----|
| **10 % de réduction** | 79 | 19 757,02 $ | 1 975,70 $ | 17 781,32 $ | 10 % |
| **20 $ de réduction sur 100 $ et** | 101 | 13 928,91 $ | 2 020,00 $ | 11 908,91 $ | 14,50 % |
| **10 $ de réduction** | 201 | 14 542,35 $ | 2 010,00 $ | 12 532,35 $ | 13,82 % |

{style="table-layout:auto"}


| **Bon** | **Moy. valeur nette de commande** | **Moy. remise de commande** | **Acheteurs distincts** | **Moy. chiffre d’affaires cumulé** |
|-----|-----|-----|-----|-----|
| **10 % de réduction** | 225,08 $ | 25,01 $ | 79 | 361,50 $ |
| **20 $ de réduction sur 100 $ et** | 117,91 $ | 20 $ | 95 | 218,76 $ |
| **10 $ de réduction** | 62,35 $ | 10 $ | 199 | 84,27 $ |

{style="table-layout:auto"}

## Que pouvez-vous en tirer ?

Environ 80 commandes ont été passées avec le coupon « 10 % de réduction », 100 commandes avec le coupon « 20 $ de réduction de 100 $ ou plus » et 200 commandes avec le coupon « 10 $ de réduction ». Le **nombre de commandes** associé à chaque coupon peut varier en fonction de plusieurs facteurs, notamment :

* la durée pendant laquelle les coupons ont été offerts.
* l’heure à laquelle les coupons ont été offerts : jour/semaine/mois/année.
* la saison pendant laquelle les coupons ont été offerts, selon l’entreprise. Par exemple :
* Le coupon « 10 % de réduction » a été offert pendant les mois d&#39;été, mais l&#39;entreprise vend des vêtements d&#39;hiver.

* les restrictions sur les coupons. Par exemple :
* Le coupon « 10 $ de réduction » n’est offert qu’aux nouveaux clients.
* Le coupon « 10 % de réduction » n&#39;est offert qu&#39;aux clients qui achètent un manteau d&#39;hiver dans la même commande.

* le comportement d’achat type du client.

Bien que les **escomptes bruts** pour les trois coupons soient similaires (environ 2 000 $), le nombre de commandes pour chaque coupon est différent. L&#39;analyse des remises par commande permet d&#39;expliquer les raisons de ces chiffres contrastés. Le coupon « 10 % de réduction » comporte le moins de commandes, mais une **remise de commande moyenne** d’environ 25 $. Même si ce coupon a un faible nombre de commandes, sa valeur d&#39;escompte moyenne élevée fait que son montant d&#39;escompte brut approche 2 000 $.

**Chiffre d’affaires brut et net** donnent une idée globale de la valeur totale des commandes associées à chaque coupon. Cependant, ce tableau d’ensemble ne permet pas de comprendre les différents comportements liés à chaque coupon. Une fois que vous examinez la base par commande, vous pouvez voir que le coupon « 10 % de réduction » a une valeur **commande nette moyenne** élevée, ce qui à son tour conduit à son **revenu net** élevé.

D&#39;un autre côté, le coupon « 10 % de réduction » a une valeur de remise moyenne élevée (25,01 $), mais la plus faible **pourcentage de remise**. Cela est logique si l’on tient compte de sa valeur nette moyenne des commandes de 225,08 $. Le coupon « 10 % de réduction » comporte un faible pourcentage de remise correspondant à une valeur de commande nette moyenne élevée. La remise de commande moyenne est donc un montant élevé.

Examinez les **acheteurs distincts** et **revenu moyen à vie** pour chaque coupon. Le coupon « 10 % de réduction » comporte le même nombre de commandes que les acheteurs distincts. Cela peut être dû au fait que chaque client est limité à un coupon. D’un autre côté, les coupons « 20 $ de réduction de 100 $ ou plus » et « 10 $ de réduction » ont moins d’acheteurs distincts que le nombre de commandes, ce qui implique que certains clients ont utilisé ces coupons plusieurs fois.

Pour le chiffre d’affaires cumulé moyen, vous pouvez constater que le chiffre d’affaires cumulé moyen de chaque coupon est supérieur à la valeur correspondante **commande nette moyenne**. Cela signifie que les clients ont effectué des achats répétés et/ou que leur valeur de commande était beaucoup plus élevée que la valeur de commande nette moyenne.

## Que puis-je analyser d’autre ? {#otheranalyses}

Les analyses mentionnées dans cette rubrique peuvent vous donner un aperçu précieux d’insight sur la manière dont vos clients utilisent vos coupons, mais il existe une multitude d’autres analyses qui vous permettent d’approfondir un peu plus votre réflexion.

**Vous pouvez analyser vos acquisitions de clients à partir de coupons.**

Quels coupons encouragent les clients à passer des commandes ? Ces coupons attirent-ils les acheteurs uniques ou encouragent-ils la fidélisation de la clientèle (en d’autres termes, celle qui effectue des achats répétés) ?

**Vous pouvez analyser le temps nécessaire à vos clients pour utiliser vos coupons.**

Vos coupons sont-ils utilisés le jour même de leur émission ou une semaine ou deux s&#39;écoulent-ils avant que la plupart de vos clients les utilisent ?

**Vous pouvez découvrir le montant de remise optimal qui augmente la fidélité du client et la valeur globale.**

Quel montant de remise encourage les acheteurs réguliers, une valeur de commande moyenne plus élevée et un chiffre d’affaires plus élevé sur toute la durée de vie ?

Répondre à ces questions vous donne un aperçu de vos clients, de leur comportement et des coupons qui offrent le plus de valeur à votre entreprise.
