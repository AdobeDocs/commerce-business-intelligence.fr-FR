---
title: Analyse de l’impact des coupons
description: Découvrez comment analyser l’impact des coupons sur l’acquisition et la fidélisation des clients.
exl-id: b0619365-fa75-49b5-a393-87f3364a390f
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 1%

---

# Impact Du Coupon

L’analyse de la manière dont les clients utilisent vos coupons peut fournir une insight significative pour votre entreprise. Plus précisément, analyser comment vous achetez et conservez des clients au moyen de coupons. Cette rubrique explore les analyses qui peuvent vous aider à répondre aux types de questions suivants :

* Combien de clients achetez-vous avec des coupons ?
* Les clients ayant acquis des coupons sont-ils plus susceptibles de faire des achats répétés que les clients n&#39;ayant pas acquis de coupons ?
* En quoi le chiffre d’affaires moyen sur la durée de vie diffère-t-il entre les clients avec coupons et les clients sans coupons ?
* Les clients acquis à partir de coupons effectuent-ils des achats répétés avec des coupons ?

Répondez à ces questions en vous concentrant sur [la comparaison des clients avec coupon acquis aux clients sans coupon acquis](#compare), [l’analyse des détails de première commande des acquisitions de coupon](#firstorder) et [l’examen des attributs des clients qui utilisent des coupons dans leur première commande.](#attributes)

Commencez !

## Comparaison entre des clients avec coupon acquis et des clients avec coupon non acquis {#compare}

Lors de la création d’analyses qui explorent l’acquisition et la conservation des coupons, pensez à utiliser les mesures suivantes :

### Nombre de nouveaux clients

Cette mesure vous indique le nombre de clients avec ou sans coupon acquis au fil du temps. Cela peut vous aider à déterminer le ratio d’acquisitions de clients par le biais de coupons.

### Chiffre d’affaires moyen sur la durée de vie

Cette mesure vous indique le chiffre d’affaires moyen sur la durée de vie des clients ayant acquis des coupons et des non-coupons. Cela peut aider à déterminer si la valeur de durée de vie d’un client varie en fonction de son type d’acquisition.

### Nombre d&#39;ordres répétés

Cette mesure indique le nombre de commandes répétées effectuées par les deux types d’acquisitions de clients. Cela peut aider à déterminer si d&#39;autres commandes de suivi sont passées par des clients avec ou sans coupon acquis.

### Nombre et pourcentage de commandes répétées avec coupon

Elles indiquent le nombre de commandes répétées effectuées avec un coupon appliqué et le pourcentage de commandes répétées effectuées avec un coupon. Cela peut vous aider à déterminer si les clients dotés de coupons ont tendance à passer plus de commandes répétées avec un coupon que les clients dotés de coupons sans coupon et si les clients dotés de coupons utilisent de manière disproportionnée des coupons dans leurs commandes de suivi.

Consultez quelques exemples de données pour les mesures d’acquisition de coupons par rapport aux mesures d’acquisition hors coupon :

| **Acquisition des clients** | **Nombre de nouveaux clients** | **Chiffre d’affaires moyen sur la durée de vie** | **Nombre d’ordres répétés** | **Nombre de commandes répétées avec coupon** | **% des commandes répétées avec coupon** |
|-----|-----|-----|-----|-----|-----|
| Coupon | 1 206 | 356,91 $ | 2 570 | 1 248 | 48,56 % |
| Sans coupon | 11 561 | 498,30 $ | 20 145 | 3 251 | 16,14 % |

{style="table-layout:auto"}

Regardez ce que vous pouvez en tirer :

### Nombre de nouveaux clients

Dans l’exemple ci-dessus, le nombre d’acquisitions hors coupon est beaucoup plus important que celui des acquisitions avec coupon. Cependant, il y a encore 1 206 clients acquis par l&#39;intermédiaire d&#39;un coupon qui, autrement, n&#39;aurait pas pu devenir des clients.

### Chiffre d’affaires moyen sur la durée de vie

Dans cet exemple, les acquisitions sans coupon ont un chiffre d’affaires moyen sur toute la durée de vie supérieur aux acquisitions avec coupon. Cela signifie que les acquisitions sans coupon font plus d&#39;achats répétés et/ou font des achats de plus grande valeur.

### Nombre d&#39;ordres répétés

Le nombre de commandes répétées pour les acquisitions sans coupon est beaucoup plus élevé que les acquisitions avec coupon. Cela est prévisible, car il existe beaucoup plus de clients acquis sans coupon.

### Nombre de commandes répétées avec coupon

De même, le nombre de commandes répétées effectuées avec un coupon est plus élevé pour les acquisitions sans coupon.

## Pourcentage de commandes répétées avec coupon

Les clients ayant acquis des coupons sans coupon ont un pourcentage beaucoup plus faible de commandes répétées avec un coupon appliqué que les clients ayant acquis des coupons. Ainsi, pour les clients ayant acquis des coupons, près de la moitié des commandes répétées sont assorties d&#39;un coupon. Dans cet exemple, les clients qui achètent des coupons ont tendance à effectuer des achats répétés avec des coupons.

## Analyse des détails de première commande à partir des acquisitions de coupon {#firstorder}

Cette section se concentre uniquement sur les **premières commandes issues d’acquisitions de coupons, segmentées par coupon.** Utilisez ces mesures dans votre analyse :

### Nombre de commandes/clients

Cette mesure vous indique le nombre de premières commandes pour chaque coupon ou le nombre de clients qui ont utilisé ce coupon lors de leur première commande. Cela peut aider à déterminer si un certain coupon encourage plus d’achats initiaux que d’autres coupons.

### Chiffre d’affaires brut

Cette mesure révèle le chiffre d’affaires que vous tirez d’un coupon spécifique qui a été utilisé lors de la première commande d’un client. Ce chiffre d’affaires correspond au calcul des articles vendus avant l’application des remises.

### Remises sur coupons

Cette mesure vous indique le montant total de la remise appliquée à partir des coupons.

### Chiffre d’affaires net

Cette mesure révèle le chiffre d’affaires que vous tirez d’un coupon spécifique qui a été utilisé lors de la première commande d’un client. Ce chiffre d’affaires correspond au calcul des articles vendus après l’application de toutes les remises. Il est important de noter que le revenu net n&#39;aurait peut-être pas été réalisé sans les coupons.

### Valeur de commande moyenne

Cette mesure révèle la valeur de commande moyenne pour un coupon spécifique.

### Nombre moyen de commandes sur la durée de vie

Cette mesure permet d’évaluer la fidélité et le nombre moyen de commandes générées par les clients qui utilisent un certain coupon.

### Chiffre d’affaires moyen sur la durée de vie

Cette mesure permet d’évaluer la fidélité et le chiffre d’affaires moyen générés par les clients qui utilisent un certain coupon. Lorsque vous évaluez si les clients qui utilisent des coupons ont une valeur supérieure aux autres, veillez à tenir compte du nombre de commandes dans lesquelles chaque coupon a été utilisé afin de vous assurer que vous disposez d’une taille d’échantillon significative.

Maintenant, regardez un exemple impliquant trois coupons différents utilisés pour la première commande des clients :

| **Bon** | **Premières commandes (FTO)** | **Chiffre d’affaires brut des FTO** | **Remises appliquées aux FTO** | **Chiffre d’affaires net des FTO** | **Valeur de commande moyenne pour FTO** |
|-----|-----|-----|-----|-----|-----|
| **25 % de réduction sur 100 $ ou plus** | 56 | 8 531,04 $ | 2 132,76 $ | 6 398,28 $ | 152,34 $ |
| **10 $ de réduction** | 87 | 3 707,07 $ | 426,10 $ | 3 280,97 $ | 42,61 $ |
| **20 % de réduction** | 145 | 10 975,05 $ | 2 195,01 $ | 8 780,04 $ | 75,69 $ |

{style="table-layout:auto"}

Que peut-on en tirer ? Tout d’abord, le coupon « 20 % de réduction » affichait le plus grand nombre de premières commandes. Cependant, le nombre de commandes associées à chaque coupon peut varier en fonction de plusieurs facteurs, notamment :

* le montant de la publicité pour chaque coupon.
* la durée pendant laquelle les coupons ont été offerts.
* l’heure à laquelle les coupons ont été offerts : jour/semaine/mois/année.
* la saison pendant laquelle les coupons ont été offerts, selon l’entreprise.

  **Exemple :** le coupon « 20 % de réduction » a été offert pendant les mois d&#39;été, mais l&#39;entreprise vend des vêtements d&#39;hiver.
* les restrictions sur les coupons.

  **Exemple :** le coupon « 10 % de réduction » n’est proposé qu’aux clients qui achètent un manteau d’hiver dans la même commande.

Le **chiffre d’affaires brut** pour le coupon « 25 % de réduction de 100 $ ou plus » est beaucoup plus élevé que le chiffre d’affaires brut pour le coupon « 10 $ de réduction ». Cependant, le coupon « 10 $ de réduction » comporte un **nombre de commandes** beaucoup plus important. L’analyse de la **valeur de commande moyenne** fournit insight sur ces différences. Même si le coupon « 25 % de réduction de 100 $ ou plus » comportait moins de commandes, la valeur moyenne de la commande est plus du triple de celle du coupon « 10 $ de réduction ». Ainsi, un revenu brut plus important est attribué au coupon « 25 % de réduction de 100 $ ou plus ».

Les **remises** et **revenu net** pour les coupons « 25 % de réduction de 100 $ ou plus » et « 20 % de réduction » ont une valeur proche. Même si la valeur de commande moyenne pour « 25 % de réduction de 100 $ ou plus » est près de deux fois supérieure à la valeur de commande moyenne pour « 20 % de réduction », ce dernier coupon a un peu moins du triple du nombre de commandes.

## Attributs des clients qui utilisent des coupons dans leur première commande {#attributes}

Maintenant que vous avez examiné les commandes elles-mêmes, examinez les clients qui utilisent des coupons dans leurs premières commandes :

| **Bon de première commande du client** | **Nombre de clients** | **Nombre moyen de commandes sur la durée de vie** | **Chiffre d’affaires moyen sur la durée de vie** |
|-----|-----|-----|-----|
| **25 % de réduction sur 100 $ ou plus** | 56 | 2,8 | 554,54 $ |
| **10 $ de réduction** | 87 | 1,9 | 115,50 $ |
| **20 % de réduction** | 145 | 1,3 | 103,75 $ |

{style="table-layout:auto"}

Vous remarquerez que le nombre de premières commandes est identique au nombre de clients pour chaque coupon. Cela est logique, car chaque client ne peut passer qu’une seule première commande.

Le plus grand nombre de clients ont été acquis grâce au coupon « 20 % de réduction ». Cependant, ces clients ont le **nombre moyen de commandes sur la durée de vie** et le **chiffre d’affaires moyen sur la durée de vie** les plus faibles. En règle générale, la plupart des clients ayant acquis des coupons ne passent pas de commandes renouvelées. De plus, les clients qui achètent un coupon « 25 % de réduction de 100 $ ou plus » augmentent **nombre moyen de commandes sur toute la durée de vie** et, par conséquent, **chiffre d’affaires moyen sur toute la durée de vie**. En règle générale, les utilisateurs qui ont été acquis via ce coupon reviennent et effectuent davantage d’achats répétés.

## Conclusion {#wrapup}

Vous pouvez créer une multitude d’analyses pour mieux comprendre comment vos clients utilisent les coupons. Avez-vous déjà pensé à analyser comment vos clients utilisent vos coupons ou le temps qu&#39;il faut pour que les coupons soient utilisés ? Que diriez-vous de trouver le montant de remise optimal ? Quel montant encourage les acheteurs réguliers, une valeur de commande moyenne plus élevée et un chiffre d’affaires plus élevé tout au long de la durée de vie ? Pour obtenir de l’aide sur ce type de questions, [contactez l’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr).
