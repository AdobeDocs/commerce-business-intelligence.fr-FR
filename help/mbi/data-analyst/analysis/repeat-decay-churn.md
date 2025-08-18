---
title: Analyse de la désintégration et de l’attrition de la probabilité de répétition
description: Découvrez et comprenez comment s’écoule le temps entre les commandes et le moment où les clients sont censés résilier la commande.
exl-id: ea26052d-ac74-43b7-a4a6-977800d4c719
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 0%

---

# Répétition de l’atténuation et de l’attrition de probabilité

Si une partie de vos revenus provient d&#39;achats répétés, vous êtes probablement conscient de l&#39;énorme valeur d&#39;une clientèle fidèle. À cette fin, il est essentiel de comprendre le délai entre les commandes et le moment où les clients sont censés résilier les commandes.

Cette rubrique explore les analyses qui peuvent vous aider à répondre aux questions suivantes :

* Quelle est la probabilité qu’un client effectue un autre achat ?
* Comment la probabilité de commande répétée varie-t-elle avec le temps depuis le dernier achat du client ?
* Quand un client doit-il être considéré comme résilié ? Par conséquent, quand une campagne de réactivation doit-elle démarrer ?

## Mesures recommandées

Lors de l’analyse de l’atténuation et de l’attrition de la probabilité de répétition, pensez à utiliser ([ou à créer](../../data-user/reports/ess-manage-data-metrics.md)) ces mesures :

### Probabilité d’ordre de répétition initiale

Cette mesure correspond au nombre total de commandes répétées, exprimé en pourcentage du total des commandes. Autrement dit, il s&#39;agit de la probabilité qu&#39;un ordre soit suivi d&#39;un autre ordre. Lorsque cette probabilité est supérieure à 50 %, cela signifie que plus de la moitié de toutes les commandes sont suivies d’une commande ultérieure.

### Probabilité de répétition de l’ordre donnée en mois depuis l’ordre

Cette mesure démontre la probabilité qu’un utilisateur commande à nouveau, compte tenu du nombre de mois écoulés depuis sa dernière commande. La formule utilisée pour générer cette mesure se simplifie pour :

![Formule de probabilité de répétition](../../assets/Repeat_probability_formula.png)

Selon votre modèle commercial, la probabilité de commande répétée peut diminuer immédiatement après le passage d’une commande par un client et continuer à diminuer au cours des mois suivants, ou elle peut présenter des variations saisonnières et des pics.

Comprendre le pourcentage de clients qui sont censés effectuer des achats répétés (et comment cette tendance se dessine au fil du temps) vous permet de cibler vos clients à intervalles réguliers afin de maximiser la probabilité d’un achat répété. Ainsi, lorsque la probabilité d’achat de répétition diminue, vous pouvez choisir un moment pour identifier un client comme résilié et redéployer vos efforts de rétention vers réactivation.

## Exemple d’aujourd’hui

Examinez la diminution de la probabilité de répétition pour une entreprise d’e-commerce type.

![Probabilité d’ordre de répétition initiale probabilité d’ordre de répétition mois donnés depuis l’ordre.](../../assets/Order_probability_reports.png)

### Probabilité d’ordre de répétition initiale

Dans cet exemple, la probabilité de commande de répétition initiale, ou la probabilité qu’un client effectue un achat de répétition, est de 60 %. Cela signifie que 60 % de toutes les commandes passées avec cette entreprise sont suivies d&#39;une commande ultérieure.

### Probabilité de répétition de l’ordre donnée en mois depuis l’ordre

Ce rapport indique la probabilité qu’un client passe à nouveau une commande, étant donné que quelques mois se sont écoulés depuis sa dernière commande. Bien qu’il n’existe pas de définition unique du seuil de résiliation compte tenu de ce rapport, Adobe recommande de définir la résiliation comme le point où la décroissance de probabilité dépasse la valeur qui est la moitié du taux de probabilité de répétition initial.

Puisque le taux de probabilité de répétition initial pour cet exemple est de 60 %, la date de résiliation serait l’heure à laquelle la probabilité d’ordre de répétition chute en dessous de 60 %/2 = 30 %, soit à environ 6 mois. Sur les 60 % de commandes qui devaient être suivies d’une autre commande, la moitié ont été passées dans les six premiers mois.

En d&#39;autres termes, si un client devait passer une commande de suivi, il est plus probable qu&#39;il l&#39;ait fait dans les six mois suivant sa dernière commande qu&#39;après la limite de six mois. Si un client n’a pas effectué de rachat après six mois, une campagne de réactivation doit être lancée pour le réintégrer.

En fonction de votre modèle commercial, vous pouvez plutôt choisir un seuil différent, comme le point où la probabilité d’ordre de répétition tombe en dessous de 50 % ou de 10 %. Si vos connaissances internes suggèrent un nombre différent, alors vous devez absolument l&#39;utiliser !

En fin de compte, l’objectif est de sélectionner le seuil où il est logique de passer des efforts de rétention aux efforts de réactivation. Les efforts de rétention peuvent impliquer des e-mails pour réengager les clients existants avec des suggestions d’achats de suivi à effectuer, tandis que les efforts de réactivation peuvent impliquer des e-mails pour les clients obsolètes avec des coupons et des offres.

## Quelles questions dois-je prendre en compte ?

Pour mieux comprendre la probabilité d’ordre de répétition qui s’applique à votre entreprise, Adobe vous suggère de tenir compte des questions suivantes lorsque vous explorez vos propres données :

* La probabilité d’ordre de répétition initiale est-elle attendue ? Sinon, pourquoi pensez-vous qu&#39;il devrait être plus élevé ou plus bas?
* Existe-t-il des baisses importantes de la probabilité de répétition de l’ordre pour des mois spécifiques depuis la dernière commande ? Dans l&#39;affirmative, ces changements sont-ils attendus ?
* Quel est votre seuil d’attrition actuel ?
* Votre seuil d’attrition actuel correspond-il à l’une des valeurs de votre probabilité d’ordre de répétition données mois depuis le dernier rapport d’ordre ?
* Votre seuil actuel reflète-t-il vos efforts publicitaires passant de la rétention à la réactivation ?
* Est-il logique pour votre entreprise de modifier le seuil au mois où la baisse de probabilité dépasse la valeur qui est la moitié du taux de probabilité de répétition initial ?

## Que dois-je analyser d’autre ?

Après avoir créé l’analyse ci-dessus et déterminé un seuil d’attrition, vous pouvez créer d’autres analyses pour identifier les tendances courantes chez les utilisateurs attriés. Par exemple, les clients qui ont résilié des achats ont-ils fait l’objet d’une acquisition au cours de la même période ou ont-ils acheté des produits similaires lors de leur dernière commande ? Une fois qu’un seuil d’attrition est défini, vous pouvez explorer plus en détail les caractéristiques spécifiques de ces clients attriés.

Si vous proposez plusieurs produits, vous vous demandez probablement comment les clients qui achètent un produit spécifique se comportent différemment au fil du temps par rapport aux autres clients. Vous souhaitez en savoir plus ? Consultez ce tutoriel pour découvrir le comportement d’achat au cours de la durée de vie des cohortes de clients en fonction de produits spécifiques qu’elles ont achetés.

Cette bonne pratique est fournie par [!DNL Adobe Commerce Intelligence] Data Analysis Services (DAS). [Contactez l’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) pour plus d’informations.

### Connexe

* [Analyse de l’impact des coupons sur l’acquisition et la fidélisation des clients](../analysis/coupon-impact.md)
* [Analyse du comportement de rachat des clients](../analysis/repurchase-behavior.md)
