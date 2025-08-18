---
title: Tableaux de bord prêts à l’emploi
description: Découvrez les tableaux de bord prêts à l’emploi pour fournir insight à votre entreprise.
exl-id: fe61c92e-de87-4317-96d7-01d2a9846bf9
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1950'
ht-degree: 0%

---

# Tableaux de bord prêts à l’emploi

[!DNL Adobe Commerce Intelligence] comprend des tableaux de bord prêts à l’emploi pour fournir insight à votre entreprise. Grâce aux tableaux de bord, vous pouvez vérifier l’intégrité des mesures essentielles, telles que le chiffre d’affaires de durée de vie de l’utilisateur, le nombre d’achats répétés, les principaux produits achetés sur une période donnée, etc. Ces tableaux de bord préconfigurés ont été créés pour vous aider à prendre des décisions commerciales éclairées.

>[!NOTE]
>
>L’accès à ces tableaux de bord dépend de votre type de compte et de votre niveau d’accès. Si ces tableaux de bord ne s’affichent pas, contactez l’[assistance technique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## Disponibilité des rapports

Pour les tableaux de bord `Customers` et `Executive Summary`, certains rapports ne sont disponibles que selon la configuration de passage en caisse de votre magasin. Plus précisément, si votre boutique autorise le passage en caisse des invités ou ne l’autorise pas.

## Clients (passage en caisse invité autorisé)

Le tableau de bord Clients (passage en caisse invité autorisé) fournit des informations sur votre base de clients, telles que leur comportement d’achat. Ce tableau de bord peut vous aider à améliorer la fidélisation de la clientèle et à déterminer quels clients génèrent le chiffre d’affaires le plus élevé.

### Rapports

| Nom | Description |
|---|---|
| `Orders by New Customers (Past 30 Days)` | Commandes au cours des 30 derniers jours de clients qui n’ont jamais passé de commande. |
| `Orders by Existing Customers (Past 30 Days)` | Commandes au cours des 30 derniers jours provenant de clients qui ont déjà passé au moins une commande. |
| `Total Unique Customers (Past 30 Days)` | Nombre de clients uniques ayant passé des commandes au cours des 30 derniers jours. |
| `Orders by New vs Existing Customers` | Nombre de commandes passées par des clients sans commandes précédentes par rapport aux clients ayant passé au moins une commande précédente. |
| `Subsequent Order Probability (All Time)` | Probabilité que les clients qui ont passé une commande en passent une autre. |
| `% of Customers with Multiple Orders (All Time)` | Pourcentage de tous les clients qui ont passé plusieurs commandes. |
| `Median Time Between Orders (All Time)` | Temps moyen que met chaque client entre passer une commande et la suivante. |
| `Subsequent Order Probability` | Probabilité que les clients qui ont passé une commande passent une autre commande, ventilée par numéro de commande. C’est-à-dire le pourcentage de clients avec une commande qui passent une seconde, le pourcentage de clients avec deux qui passent une troisième, etc. |
| `Time Between Orders` | Temps moyen et médian que les clients passent entre les commandes, ventilé par numéro de commande (c’est-à-dire le temps écoulé entre les commandes une et deux, deux et trois, etc.). |
| `Number of Customers - Lifetime Orders` | Pour un nombre donné de commandes passées au cours de la durée de vie d&#39;un client, le nombre de clients qui ont passé autant de commandes et le pourcentage de l&#39;ensemble de la base de clients que ce nombre représente. |
| `One-Time Customers who Bought 3-6 Months Ago` | Les clients qui ont effectué leur premier et seul achat il y a entre trois et six mois. |
| `Avg LTV by First Order` | Compare le chiffre d’affaires cumulé moyen sur la durée de vie du client entre les cohortes. Les cohortes sont définies par le mois au cours duquel un client a effectué son premier achat. Par exemple, une cohorte `Jan 2020` affiche la moyenne cumulée des VVC pour les clients dont le premier achat a eu lieu en janvier 2020. |
| `Customer's First 30 Day vs Lifetime Revenue` | Comparaison du chiffre d’affaires moyen des clients dans les 30 jours suivant leur premier achat par rapport à l’ensemble de leur durée de vie. Chaque bulle correspond à une région d’expédition, et la taille de chaque bulle représente le nombre de clients acquis depuis cette région. |

## Clients (aucun passage en caisse invité autorisé)

Le tableau de bord Clients (aucun passage en caisse des invités autorisé) fournit des informations sur votre base de clients, telles que leur comportement d’achat et les conversions entre les enregistrements de compte et les placements de commande. Ce tableau de bord peut vous aider à améliorer la fidélisation de la clientèle et à déterminer quels clients génèrent le chiffre d’affaires le plus élevé.

### Rapports

| Nom | Description |
|---|---|
| `Account Registration (Past 30 Days)` | Nombre de personnes qui se sont enregistrées pour un compte dans votre boutique au cours des 30 derniers jours. |
| `Accounts Registered (Past 30 Days) with 1 or More Orders` | Nombre de personnes qui se sont enregistrées pour un compte dans votre boutique au cours des 30 derniers jours et qui ont également passé au moins une commande. |
| `% Conversion from Registration to First Order (Past 30 Days)` | Pourcentage de comptes enregistrés au cours des 30 derniers jours ayant passé une commande. |
| `% Conversion from Registration to First Order` | Pourcentage de comptes enregistrés ayant passé une commande, par mois d’enregistrement. |
| `Orders by New vs Existing Customers` | Nombre de commandes passées par des clients sans commandes précédentes par rapport aux clients ayant passé au moins une commande précédente. |
| `Subsequent Order Probability (All Time)` | Probabilité que les clients qui ont passé une commande en passent une autre. |
| `% of Customers with Multiple Orders (All Time)` | Pourcentage de tous les clients qui ont passé plusieurs commandes. |
| `Median Time Between Orders (All Time)` | Temps moyen que met chaque client entre passer une commande et la suivante. |
| `Subsequent Order Probability` | Probabilité que les clients qui ont passé une commande en passent une autre, ventilée par numéro de commande. C’est-à-dire le pourcentage de clients ayant passé une commande, ayant passé une deuxième commande, ayant passé une troisième commande, etc. |
| `Time Between Orders` | Temps moyen et médian que les clients passent entre les commandes, ventilé par numéro de commande (c’est-à-dire le temps écoulé entre les commandes une et deux, deux et trois, etc.). |
| `Number of Customers - Lifetime Orders` | Pour un nombre donné de commandes passées au cours de la durée de vie d&#39;un client, le nombre de clients qui ont passé autant de commandes et le pourcentage de l&#39;ensemble de la base de clients que ce nombre représente. |
| `One-Time Customers who Bought 3-6 Months Ago` | Les clients qui ont effectué leur premier et seul achat il y a entre trois et six mois. |
| `Avg LTV by First Order` | Compare le chiffre d’affaires cumulé moyen sur la durée de vie du client entre les cohortes. Les cohortes sont définies par le mois au cours duquel un client a effectué son premier achat. Par exemple, une cohorte de janvier 2020 affiche le LTV moyen cumulé pour les clients dont le premier achat a eu lieu en janvier 2020. |
| `Customer's First 30 Day vs Lifetime Revenue` | Comparaison du chiffre d’affaires moyen des clients dans les 30 jours suivant leur premier achat par rapport à l’ensemble de leur durée de vie. Chaque bulle correspond à une région d’expédition, et la taille de chaque bulle représente le nombre de clients acquis depuis cette région. |

## Résumé (passage en caisse des invités autorisé)

Le tableau de bord du résumé exécutif (passage en caisse pour les invités) vous donne un aperçu succinct de la situation de l’entreprise en termes de commandes et de chiffre d’affaires. Ce tableau de bord est conçu pour que les cadres aient une compréhension globale des performances commerciales, mais il peut également s’avérer instructif pour d’autres personnes.

### Rapports

| Nom | Description |
|---|---|
| `Revenue (Current Month)` | Chiffre d’affaires généré par votre boutique pour le mois en cours. Dans ce cas, le chiffre d’affaires est défini comme le prix final payé par un client sur une commande. |
| `Revenue (Past 6 Months by Day)` | Chiffre d’affaires quotidien total, superposé au chiffre d’affaires quotidien moyen des sept jours précédents. Dans ce cas, le chiffre d’affaires est défini comme le prix final payé par un client sur une commande. |
| `% Change in Revenue (MoM MTD)` | Comparaison des revenus du mois en cours (jusqu’à présent) par rapport à la même partie du mois précédent. |
| `Revenue from New vs Existing Customers (Current Month)` | Chiffre d’affaires pour le mois en cours (jusqu’à présent) attribué aux nouveaux (nouveaux) clients par rapport aux clients existants (passant une deuxième commande ou une commande ultérieure). |
| `Average Order Value (Current Month)` | Valeur moyenne quotidienne des commandes passées au cours du mois en cours (jusqu&#39;à présent). La valeur de commande est définie comme le prix final payé par un client sur une commande. |
| `Orders (Current Month)` | Nombre de commandes passées dans votre magasin pour le mois en cours (jusqu’à présent). |
| `% Change in Orders (MoM MTD)` | Comparaison du nombre de commandes pour le mois en cours (jusqu’à présent) par rapport à la même partie du mois précédent. |
| `Orders by New Customers (Current Month)` | Commandes pour le mois en cours provenant de clients qui n&#39;ont jamais passé de commande auparavant. |
| `Orders by Existing Customers (Current Month)` | Commandes pour le mois en cours provenant de clients qui ont déjà passé au moins une commande. |
| `Orders by New vs Existing Customers (Current Year by Week)` | Nombre de commandes passées par des clients sans commandes précédentes par rapport au nombre de commandes passées par des clients avec au moins une commande précédente, pour chaque semaine de l’année en cours (jusqu’à présent). |

## Résumé (passage en caisse des invités non autorisé)

Le tableau de bord du résumé exécutif (passage en caisse interdit aux invités) vous donne un aperçu succinct de la situation de l’entreprise en termes de commandes, de chiffre d’affaires et d’enregistrements de compte. Ce tableau de bord est conçu pour que les cadres aient une compréhension globale des performances commerciales, mais il peut également s’avérer instructif pour d’autres personnes.

### Rapports

| Nom | Description |
|---|---|
| `Revenue (Current Month)` | Chiffre d’affaires généré par votre boutique ce mois-ci. Dans ce cas, le chiffre d’affaires est défini comme le prix final payé par un client sur une commande. |
| `Revenue (Past 6 Months by Day)` | Chiffre d’affaires quotidien total, superposé au chiffre d’affaires quotidien moyen des sept jours précédents. Dans ce cas, le chiffre d’affaires est défini comme le prix final payé par un client sur une commande. |
| `% Change in Revenue (MoM MTD)` | Comparaison des revenus réalisés jusqu’à présent ce mois-ci par rapport à la même partie du mois précédent. |
| `Revenue from New vs Existing Customers (Current Month)` | Chiffre d’affaires pour le mois en cours (jusqu’à présent) attribué aux nouveaux (nouveaux) clients par rapport aux clients existants (passant une deuxième commande ou une commande ultérieure). |
| `Average Order Value (Current Month)` | Valeur moyenne quotidienne des commandes passées au cours du mois en cours (jusqu&#39;à présent). La valeur de commande est définie comme le prix final payé par un client sur une commande. |
| `Orders (Current Month)` | Nombre de commandes passées dans votre magasin pour le mois en cours (jusqu’à présent). |
| `% Change in Orders (MoM MTD)` | Comparaison du nombre de commandes pour le mois en cours (jusqu’à présent) par rapport à la même partie du mois précédent. |
| `Account Registrations (Current Month)` | Nombre de nouveaux comptes enregistrés jusqu’à présent ce mois-ci. |
| `% Conversion from Registration to First Order (Current Month)` | Pourcentage de comptes enregistrés à ce jour ce mois-ci qui ont passé une commande. |
| `% Conversion from Registration to First Order (Current Year by Week)` | Pourcentage de comptes enregistrés chaque semaine jusqu’à présent cette année qui ont passé une commande. |

## Commandes

Le tableau de bord Commandes fournit des informations sur le volume transactionnel des commandes, leur statut, les codes coupon utilisés, le chiffre d’affaires généré et les modes de paiement utilisés. Vous pouvez, par exemple, effectuer le suivi du processus d’exécution et vous assurer qu’il n’y a aucun problème ou goulot d’étranglement.

>[!NOTE]
>
>Les rapports de ce tableau de bord sont disponibles pour les comptes connectés aux magasins avec l’un ou l’autre type de configuration (passage en caisse des invités, pas de passage en caisse des invités).

### Rapports

| Nom | Description |
|---|---|
| `Orders (Past 30 Days)` | Nombre de commandes passées dans votre magasin au cours des 30 derniers jours. |
| `Revenue (Past 30 Days)` | Chiffre d’affaires généré par votre boutique au cours des 30 derniers jours. Le chiffre d’affaires est défini comme le prix final payé par un client sur une commande. |
| `Average Order Value (Past 30 Days)` | Valeur moyenne des commandes passées au cours des 30 derniers jours. La valeur de commande est définie comme le prix final payé par un client sur une commande. |
| `Orders` | Nombre de commandes passées dans votre magasin chaque mois. |
| `Revenue by Payment Method` | Chiffre d’affaires généré par votre boutique, ventilé par mode de paiement. Le chiffre d’affaires est défini comme le prix final payé par un client sur une commande. |
| `AOV by New vs Existing Customers` | Valeur moyenne mensuelle des commandes passées dans votre magasin, divisée par les commandes passées par des clients sans commandes précédentes par rapport aux clients ayant au moins une commande précédente. La valeur de commande est définie comme le prix final payé par un client sur une commande. |
| `% Orders by Status (Past 30 Days)` | Pourcentage de commandes de chaque jour au cours des 30 derniers jours qui sont actuellement dans chaque statut de commande. |
| `Incomplete Orders (Created more than 1 Day Ago)` | Liste de toutes les commandes passées il y a plus d&#39;un jour et dont le statut est toujours Incomplet (non annulées ou terminées). |
| `Orders Per Hour (Past 7 Days)` | Classer le volume par jour et par heure. |
| `Revenue Details (Past 30 Days)` | Répartition du chiffre d’affaires quotidien pour les 30 derniers jours dans tous les composants de la valeur du chiffre d’affaires total. |
| `Order Details by Coupon Code (Past 30 Days)` | Pour chaque code de coupon proposé par votre boutique, des détails sur la manière dont ce code a été utilisé et sur les retours qu’il a apportés au cours des 30 derniers jours. |
| `% Orders with Coupon (Past 30 Days)` | Pourcentage de commandes passées au cours des 30 derniers jours qui ont utilisé un coupon par rapport à celles qui n’en ont pas utilisé. |

## Produits

Le tableau de bord Produits présente les performances générales des produits en termes de produits commandés, de leur valeur brute (VMG) et des principaux produits achetés et remboursés. Il peut vous aider à équilibrer les achats et les retours, et à déterminer le succès et la popularité du produit. Votre boutique doit être [configurée pour effectuer le suivi des remboursements](https://experienceleague.adobe.com/docs/commerce-admin/customers/customer-accounts/store-credit/credit-configure.html) pour que ces graphiques soient renseignés.

>[!NOTE]
>
>Les rapports de ce tableau de bord sont disponibles pour les comptes connectés aux magasins avec l’un ou l’autre type de configuration (passage en caisse des invités, pas de passage en caisse des invités).

### Rapports

| Nom | Description |
|---|---|
| `GMV (Past 30 Days)` | Valeur brute de tous les produits vendus au cours des 30 derniers jours. La valeur moyenne globale correspond à la quantité commandée multipliée par le prix de base pour chaque produit. |
| `% GMV (Past 30 Days) Refunded` | Pourcentage de la VMG des produits achetés au cours des 30 derniers jours qui ont donné lieu à un remboursement. |
| `Product Quantity Ordered (Past 30 Days)` | Nombre total d’articles commandés au cours des 30 derniers jours. |
| `% Purchased Products (Past 30 Days) Refunded` | Pourcentage d’articles achetés au cours des 30 derniers jours qui ont donné lieu à un remboursement. |
| `Gross Merchandise Value` | Valeur brute de tous les produits vendus, par mois. La valeur moyenne globale correspond à la quantité commandée multipliée par le prix de base pour chaque produit. |
| `Purchases vs Refund Rate per Product (Past 30 Days)` | Pour chaque produit, une comparaison du nombre total commandé au cours des 30 derniers jours avec le taux auquel le produit a été remboursé. La taille de chaque bulle représente le taux de remboursement. |
| `Product Performance Details (Past 30 Days)` | Informations détaillées sur les ventes et les remboursements ultérieurs au cours des 30 derniers jours, par SKU de produit et par nom de produit. |
| `Top Purchased Products by GMV (Past 30 Days)` | Produits vendus au cours des 30 derniers jours qui ont généré le plus de chiffre d’affaires (top 10). |
| `Top Refunded Products by GMV (Past 30 Days)` | Produits achetés au cours des 30 derniers jours qui ont entraîné le plus grand nombre de pertes de VGM dues à des remboursements (top 10). |
| `Top Purchased Products by Quantity (Past 30 Days)` | Produits vendus au cours des 30 derniers jours en plus grand nombre (top 10). |
| `Top Refunded Products by Quantity (Past 30 Days)` | Produits achetés au cours des 30 derniers jours qui ont entraîné le remboursement de la plus grande quantité (top 10). |
