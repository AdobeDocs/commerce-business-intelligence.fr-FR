---
title: Analyse de la décroissance et de la perte de clientèle des répétitions
description: Découvrez et comprenez l’écart de temps entre les commandes et le moment où les clients sont censés se produire.
exl-id: ea26052d-ac74-43b7-a4a6-977800d4c719
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 0%

---

# Répéter la décroissance de probabilité et la perte de clientèle

Si une partie de vos recettes provient d’achats répétés, vous êtes probablement conscient de l’énorme valeur d’une base de clients fidèles. À cette fin, il est essentiel de comprendre l’écart de temps entre les commandes et le moment où les clients sont censés se produire.

Cette rubrique explore les analyses qui peuvent vous aider à répondre aux questions suivantes :

* Quelle est la probabilité qu’un client effectue un autre achat ?
* Comment la probabilité de commandes répétées varie-t-elle avec le temps depuis le dernier achat du client ?
* Quand un client doit-il être considéré comme ayant été généré ? Par conséquent, quand une campagne de réactivation doit-elle démarrer ?

## Mesures recommandées

Lors de l’analyse de l’atténuation et de l’attrition des probabilités de répétition, pensez à utiliser ([ou à créer](../../data-user/reports/ess-manage-data-metrics.md)) ces mesures :

### Probabilité initiale de l’ordre de répétition

Cette mesure est définie comme le nombre total de commandes répétées, en pourcentage du total des commandes. Autrement dit, il s’agit de la probabilité qu’une commande soit suivie d’une autre commande. Lorsque cette probabilité est supérieure à 50 %, cela implique que plus de la moitié de toutes les commandes sont suivies par un ordre ultérieur.

### Probabilité de répétition de l’ordre exprimée en mois depuis la commande

Cette mesure indique la probabilité qu’un utilisateur commande à nouveau, étant donné le nombre de mois écoulés depuis sa dernière commande. La formule utilisée pour générer cette mesure simplifie les opérations suivantes :

![Formule de probabilité de répétition](../../assets/Repeat_probability_formula.png)

Selon votre modèle d’entreprise, la probabilité de commandes répétées peut diminuer immédiatement après qu’un client a passé une commande et continuer à diminuer au cours des mois suivants ou elle peut démontrer des variations et des pics saisonniers.

Comprendre le pourcentage de clients qui sont censés effectuer des achats répétés (et la manière dont cette tendance évolue au fil du temps) vous permet de cibler vos clients à intervalles réguliers, afin d’optimiser la probabilité d’un achat répété. Ainsi, lorsque la probabilité d’achat répété est en baisse, vous pouvez choisir un moment pour identifier un client comme ayant été généré et passer de la rétention à la réactivation.

## Exemple d&#39;aujourd&#39;hui

Examinez la probabilité de récidive pour une activité de commerce électronique classique.

![ La probabilité initiale de répétition de l’ordre la probabilité de répétition de l’ordre donnée des mois depuis la commande.&lbrace;1](../../assets/Order_probability_reports.png)

### Probabilité initiale de l’ordre de répétition

Dans cet exemple, la probabilité initiale de commande répétée - ou la probabilité qu’un client effectue un achat répété - est de 60 %. Cela signifie que 60 % de toutes les commandes passées avec cette entreprise sont suivies d’une commande ultérieure.

### Probabilité de répétition de l’ordre exprimée en mois depuis la commande

Ce rapport présente la probabilité qu’un client commande à nouveau, étant donné que certains mois se sont écoulés depuis sa dernière commande. Bien qu’il n’existe aucune définition unique du seuil de perte de clientèle dans ce rapport, Adobe recommande de définir la perte de clientèle comme le point où la probabilité de perte de clientèle dépasse la valeur qui est la moitié du taux de probabilité de répétition initial.

Comme le taux de probabilité de répétition initial de cet exemple est de 60 %, la date de perte serait l’heure à laquelle la probabilité de répétition de l’ordre chute en dessous de 60 %/2 = 30 %, ou à environ 6 mois. Sur les 60% des commandes qui devaient être suivies d&#39;une autre commande, la moitié d&#39;entre elles ont été passées dans les 6 premiers mois.

Autrement dit, si un client devait passer une commande de relance, il est plus probable qu’il l’ait fait dans les six mois suivant sa dernière commande qu’après le délai de six mois. Si un client n’a pas effectué ses achats au bout de six mois, une campagne de réactivation doit être lancée pour le rappeler.

Selon votre modèle d’entreprise, vous pouvez choisir un seuil différent, comme le point où la probabilité de l’ordre de répétition chute en dessous de 50 % ou 10 %. Si vos connaissances internes suggèrent un nombre différent, alors vous devriez l&#39;utiliser par tous les moyens !

En fin de compte, l’objectif est de sélectionner le seuil où il est logique de passer de la rétention aux efforts de réactivation. Les efforts de rétention peuvent impliquer des emails pour réengager les clients existants avec des suggestions d’achats de relance à effectuer, tandis que les efforts de réactivation peuvent impliquer des emails pour les clients obsolètes avec des bons et des offres.

## Quelles questions dois-je prendre en compte ?

Pour vous aider à comprendre la probabilité de répétition d’ordre telle qu’elle s’applique à votre entreprise, Adobe vous suggère de prendre en compte ces questions lorsque vous explorez vos propres données :

* La probabilité initiale de l’ordre de répétition est-elle attendue ? Si ce n&#39;est pas le cas, pourquoi pensez-vous qu&#39;elle devrait être plus ou moins élevée ?
* Existe-t-il des baisses importantes de la probabilité de répétition de l’ordre pour des mois spécifiques depuis le dernier ordre ? Si tel est le cas, ces modifications sont-elles attendues ?
* Quel est votre seuil de perte de clientèle actuel ?
* Votre seuil de perte de clientèle actuel est-il aligné sur l’une des valeurs de votre probabilité de répétition d’ordre données des mois depuis le rapport de dernière commande ?
* Votre seuil actuel reflète-t-il vos efforts publicitaires qui passent de la rétention à la réactivation ?
* Est-il logique pour votre entreprise de modifier le seuil jusqu’au mois où la probabilité de décomposition dépasse la valeur qui est la moitié du taux de probabilité de répétition initial ?

## Que dois-je analyser d&#39;autre ?

Après avoir créé l’analyse ci-dessus et déterminé un seuil de perte de clientèle, vous pouvez créer davantage d’analyses afin d’identifier les tendances courantes chez les utilisateurs perte de clientèle. Par exemple, les clients qui ont effectué des achats au cours de la même période ou ont-ils acheté des produits similaires dans leur dernière commande ? Une fois qu’un seuil de perte de clientèle est défini, vous pouvez approfondir l’analyse des caractéristiques spécifiques de ces clients perte de clientèle.

Si vous proposez plusieurs produits, vous vous demandez probablement comment les clients qui achètent un produit spécifique se comportent différemment au fil du temps par rapport aux autres clients. Vous voulez en savoir plus ? Consultez ce tutoriel pour découvrir le comportement d’achat de durée de vie des cohortes de clients en fonction de produits spécifiques qu’ils ont achetés.

Cette bonne pratique est fournie par [!DNL Adobe Commerce Intelligence] Data Analysis Services (DAS). [Contactez l’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) pour plus d’informations.

### Associé

* [Analyse de l&#39;impact des coupons sur l&#39;acquisition et la fidélisation des clients](../analysis/coupon-impact.md)
* [Analyse du comportement de réachat des clients](../analysis/repurchase-behavior.md)
