---
title: Analyse de l'impact des coupons
description: Découvrez comment analyser l’impact des coupons sur l’acquisition et la fidélisation des clients.
exl-id: b0619365-fa75-49b5-a393-87f3364a390f
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 1%

---

# Coupon Impact

L’analyse de la manière dont les clients utilisent vos coupons peut fournir des informations importantes sur votre entreprise. Plus précisément, l’analyse de la manière dont vous acquérez et fidélisez des clients au moyen de bons. Cette rubrique explore des analyses qui peuvent vous aider à répondre aux types de questions suivants :

* Combien de clients achetez-vous au moyen de coupons ?
* Les clients ayant obtenu un bon sont-ils plus susceptibles de procéder à des achats répétés que les clients n’ayant pas effectué l’acquisition par l’intermédiaire de bons ?
* En quoi le revenu moyen sur la durée de vie diffère-t-il entre les clients rachetés par des coupons et les clients non rachetés par des coupons ?
* Les clients achetés à partir de coupons effectuent-ils des achats répétés avec des coupons ?

Répondez à ces questions en vous concentrant sur la [comparaison des clients ayant acheté des coupons avec des clients n’ayant pas acheté des coupons](#compare), l’ [ analyse des détails de première commande à partir des acquisitions de coupons](#firstorder) et la [consultation des attributs des clients qui utilisent des coupons dans leur première commande](#attributes).

Commencez !

## Comparaison des clients ayant obtenu un bon et des clients n’ayant pas obtenu un bon {#compare}

Lorsque vous effectuez des analyses qui explorent l’acquisition et la rétention de vos bons, pensez à utiliser les mesures suivantes :

### Nombre de nouveaux clients

Cette mesure indique le nombre de clients ayant obtenu un bon et de clients n’ayant pas obtenu un bon au cours de la période écoulée. Cela peut vous aider à déterminer le ratio d’acquisitions client au moyen de coupons.

### Chiffre d’affaires moyen

Cette mesure vous montre les recettes moyennes sur la durée de vie des clients ayant souscrit un coupon ou un autre coupon. Cela peut vous aider à déterminer si la valeur de durée de vie d’un client varie en fonction de son type d’acquisition.

### Nombre de commandes répétées

Cette mesure indique le nombre de commandes répétées effectuées par les deux types d’acquisitions de clients. Cela peut aider à déterminer si d’autres commandes de relance sont passées par les clients achetés ou non par coupon.

### Nombre et pourcentage de commandes répétées avec coupon

Cela indique le nombre de commandes répétées effectuées avec un coupon appliqué et le pourcentage de commandes répétées effectuées avec un coupon. Cela peut vous aider à déterminer si les clients rachetés par coupon ont tendance à effectuer plus de commandes répétées avec un coupon que les clients non coupon acquis et si les clients rachetés par coupon utilisent disproportionnellement les coupons dans leurs commandes de relance.

Comparez les mesures d’acquisition de coupons à celles des autres types de données :

| **Acquisition client** | **Nombre de nouveaux clients** | **Chiffre d’affaires moyen de la durée de vie** | **Nombre de commandes répétées** | **Nombre de commandes répétées avec coupon** | **% des commandes répétées avec coupon** |
|-----|-----|-----|-----|-----|-----|
| Bon | 1 206 | 356,91 $ | 2 570 | 1 248 | 48,56 % |
| Non-coupon | 11 561 | 498,30 $ | 20 145 | 3 251 | 16,14 % |

{style="table-layout:auto"}

Regardez ce que vous pouvez en retirer :

### Nombre de nouveaux clients

Dans l’exemple ci-dessus, il existe un nombre beaucoup plus important d’acquisitions de coupons que d’acquisitions de coupons. Toutefois, 1 206 clients sont encore acquis par l&#39;intermédiaire d&#39;un coupon qui, autrement, n&#39;aurait pas été devenu client.

### Chiffre d’affaires moyen

Dans cet exemple, les acquisitions de coupons ont une durée de vie moyenne plus élevée que les acquisitions de coupons. Cela signifie que les acquisitions sans coupon effectuent davantage d’achats répétés et/ou effectuent des achats de valeur plus élevée.

### Nombre de commandes répétées

Le nombre de commandes répétées pour les acquisitions sans coupon est beaucoup plus élevé que les acquisitions de coupons. Cela est attendu car il y a beaucoup plus de clients non-coupons acquis.

### Nombre de commandes répétées avec coupon

De même, le nombre de commandes répétées effectuées avec un coupon est plus élevé pour les acquisitions sans coupon.

## Pourcentage de commandes répétées avec coupon

Les clients non-coupon acquis ont un pourcentage beaucoup plus faible de commandes répétées avec un coupon appliqué que les clients ayant acheté un coupon. Ainsi, pour les clients rachetés par coupon, près de la moitié des commandes répétées a un coupon appliqué. Dans cet exemple, les clients achetés par coupon ont tendance à effectuer des achats répétés avec des coupons.

## Analyse des détails de première commande à partir des acquisitions de coupons {#firstorder}

Cette section se concentre uniquement sur les **premières commandes issues des acquisitions de coupons, segmentées par coupon.** Utilisez ces mesures dans votre analyse :

### Nombre de commandes/clients

Cette mesure indique le nombre de premières commandes pour chaque coupon ou le nombre de clients qui ont utilisé ce coupon dans leur première commande. Cela peut vous aider à déterminer si un certain coupon encourage plus d’achats pour la première fois que les autres.

### Chiffre d’affaires brut

Cette mesure révèle les recettes que vous obtenez à partir d’un coupon particulier qui a été utilisé dans la première commande d’un client. Cette recette est un calcul des articles vendus avant l’application de remises.

### Remises sur les coupons

Cette mesure vous indique le montant total de remise appliqué par les coupons.

### Chiffre d’affaires net

Cette mesure révèle les recettes que vous obtenez à partir d’un coupon particulier qui a été utilisé dans la première commande d’un client. Cette recette est un calcul des articles vendus après l’application de toutes les remises. Il est important de noter que les recettes nettes peuvent ne pas avoir été générées sans les coupons.

### Valeur de commande moyenne

Cette mesure révèle la valeur de commande moyenne d’un coupon particulier.

### Durée de vie moyenne des commandes

Cette mesure permet d’évaluer la fidélité et le nombre moyen de commandes générées par les clients qui utilisent un certain coupon.

### Chiffre d’affaires moyen

Cette mesure permet d’évaluer la fidélité et les recettes moyennes générées par les clients qui utilisent un certain coupon. Lorsque vous évaluez si les clients qui utilisent des coupons ont une valeur supérieure à d’autres, veillez à tenir compte du nombre de commandes dans lesquelles chaque coupon a été utilisé pour vous assurer que vous disposez d’une taille d’échantillon significative.

Examinez maintenant un exemple impliquant trois bons différents utilisés pour la première commande d’un client :

| **Coupon** | **Premières commandes (FTO)** | **Chiffre d&#39;affaires brut de FTO** | **Remises appliquées à FTO** | **Chiffre d’affaires net de FTO** | **Valeur de commande moyenne pour FTO** |
|-----|-----|-----|-----|-----|-----|
| **25 % de remise de 100 $ ou plus** | 56 | 8 531,04 $ | 2 132,76 $ | 6 398,28 $ | 152,34 $ |
| **$10 off** | 87 | 3 707,07 $ | 426,10 $ | 3 280,97 $ | 42,61 $ |
| **20 % de remise** | 145 | 10 975,05 $ | 2 195,01 $ | 8 780,04 $ | 75,69 $ |

{style="table-layout:auto"}

Que peut-on en tirer ? Tout d’abord, le coupon &quot;20 % de réduction&quot; a eu le plus grand nombre de premières commandes. Cependant, le nombre de commandes associées à chaque coupon peut varier en fonction de plusieurs facteurs, notamment :

* le montant de la publicité pour chaque coupon.
* la durée pendant laquelle les coupons ont été proposés.
* l’heure du jour/de la semaine/du mois/de l’année où les bons ont été proposés.
* la saison pendant laquelle les coupons ont été proposés, en fonction de l&#39;activité.

  **Exemple :** le coupon &quot;20 % de réduction&quot; a été offert pendant les mois d’été, mais l’entreprise vend des vêtements d’hiver.
* les restrictions sur les coupons.

  **Exemple :** le coupon &quot;10 % de réduction&quot; n’est offert qu’aux clients qui achètent un manteau d’hiver dans la même commande.

Le **revenu brut** du coupon &quot;25 % de 100 $ ou plus&quot; est beaucoup plus élevé que le revenu brut du coupon &quot;10 $ de réduction&quot;. Cependant, le coupon &quot;$10 off&quot; a un nombre de commandes **beaucoup plus important**. L’analyse de la **valeur de commande moyenne** permet d’analyser ces différences. Même si le coupon &quot;25 % de 100 $ ou plus&quot; avait moins de commandes, la valeur de commande moyenne est plus de trois fois supérieure à celle du coupon &quot;10 $ de réduction&quot;. Ainsi, un revenu brut plus élevé est attribué au coupon &quot;25 % de 100 $ ou plus&quot;.

Les **remises** et les **recettes nettes** pour les coupons &quot;25 % de remise de 100 $ ou plus&quot; et &quot;20 % de remise&quot; ont une valeur proche. Même si la valeur de commande moyenne pour &quot;25 % de 100 $ ou plus&quot; est près de deux fois la valeur de commande moyenne pour &quot;20 % de réduction&quot;, ce dernier coupon a un peu moins de trois fois le nombre de commandes.

## Attributs des clients qui utilisent des bons dans leur première commande {#attributes}

Maintenant que vous avez examiné les commandes, consultez les clients qui utilisent des coupons dans leurs premières commandes :

| **Coupon de première commande du client** | **Nombre de clients** | **Nombre moyen de commandes pendant la durée de vie** | **Chiffre d’affaires moyen de la durée de vie** |
|-----|-----|-----|-----|
| **25 % de remise de 100 $ ou plus** | 56 | 2,8 | 554,54 $ |
| **$10 off** | 87 | 1,9 | 115,50 $ |
| **20 % de remise** | 145 | 1,3 | 103,75 $ |

{style="table-layout:auto"}

Vous remarquerez que le nombre de premières commandes est le même que le nombre de clients pour chaque coupon. Cela est logique, car chaque client ne peut avoir qu’une seule première commande.

Le plus grand nombre de clients a été racheté via le coupon &quot;20% de réduction&quot;. Cependant, ces clients ont le **nombre de commandes moyen le plus faible** et le **chiffre d’affaires de durée de vie moyenne** ; en règle générale, la plupart des clients ayant obtenu un coupon n’effectuent aucune commande répétée. En outre, les clients acquis par le biais du coupon &quot;25 % de réduction de 100 $ ou plus&quot; génèrent des **commandes de durée de vie moyenne** plus élevées et, à leur tour, des **recettes de durée de vie moyenne** plus élevées. En règle générale, les utilisateurs qui ont été achetés via ce coupon reviennent généralement et effectuent davantage d’achats répétés.

## Remplissage {#wrapup}

Vous pouvez créer une multitude d’analyses pour mieux comprendre l’utilisation des bons par vos clients. Avez-vous déjà réfléchi à la manière dont vos clients utilisent vos coupons ou au temps nécessaire à leur utilisation ? Qu’en est-il de la recherche du montant de remise optimal : quel montant encourage les acheteurs réguliers, une valeur de commande moyenne plus élevée et des recettes de durée de vie plus élevées ? Pour obtenir de l’aide sur ces types de questions, [contactez l’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr).
