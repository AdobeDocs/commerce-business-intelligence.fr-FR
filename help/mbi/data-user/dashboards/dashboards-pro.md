---
title: Tableaux de bord prêts à l’emploi
description: Découvrez les tableaux de bord d’usine pour vous donner des informations sur votre entreprise.
exl-id: fe61c92e-de87-4317-96d7-01d2a9846bf9
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1950'
ht-degree: 0%

---

# Tableaux de bord d’usine

[!DNL Adobe Commerce Intelligence] comprend des tableaux de bord prêts à l’emploi pour fournir des informations sur votre entreprise. Les tableaux de bord vous permettent de vérifier l’intégrité des mesures essentielles telles que les recettes de durée de vie des utilisateurs, le nombre d’achats répétés, les principaux produits achetés au cours d’une période donnée, etc. Ces tableaux de bord préconfigurés ont été créés pour vous aider à prendre des décisions professionnelles éclairées.

>[!NOTE]
>
>L’accès à ces tableaux de bord dépend du type de compte et du niveau d’accès. Si vous ne voyez pas ces tableaux de bord, contactez [support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## Disponibilité des rapports

Pour les tableaux de bord `Customers` et `Executive Summary`, certains rapports ne sont disponibles que selon la configuration de passage en caisse de votre boutique. Plus précisément, si votre boutique autorise le passage en caisse des invités ou n’autorise pas le passage en caisse des invités.

## Clients (passage en caisse autorisé pour les invités)

Le tableau de bord Clients (passage en caisse autorisé) fournit des informations sur votre base de clients, telles que leur comportement d’achat. Ce tableau de bord peut vous aider à améliorer la rétention des clients et à déterminer les clients qui génèrent les recettes les plus élevées.

### Rapports

| Nom | Description |
|---|---|
| `Orders by New Customers (Past 30 Days)` | Commandes effectuées au cours des 30 derniers jours auprès de clients qui n’ont jamais passé de commande auparavant. |
| `Orders by Existing Customers (Past 30 Days)` | Commandes des clients qui ont passé au moins une commande au cours des 30 derniers jours. |
| `Total Unique Customers (Past 30 Days)` | Nombre de clients uniques qui passent des commandes au cours des 30 derniers jours. |
| `Orders by New vs Existing Customers` | Nombre de commandes passées par les clients n’ayant pas de commande précédente, par rapport aux clients ayant passé au moins une commande précédente. |
| `Subsequent Order Probability (All Time)` | La probabilité que les clients qui ont passé une commande en placent une autre. |
| `% of Customers with Multiple Orders (All Time)` | Pourcentage de tous les clients ayant passé plusieurs commandes. |
| `Median Time Between Orders (All Time)` | Durée moyenne de chaque client entre le placement d’une commande et le suivant. |
| `Subsequent Order Probability` | La probabilité que les clients qui ont passé une commande placent une autre commande, ventilée par numéro de commande. C&#39;est-à-dire le pourcentage de clients avec une commande qui en passent une seconde, le pourcentage de clients avec deux qui en passent une troisième, etc. |
| `Time Between Orders` | Le temps moyen et médian pris par les clients entre les commandes, ventilé par numéro de commande (c’est-à-dire le temps entre les commandes un et deux, deux et trois, etc.). |
| `Number of Customers - Lifetime Orders` | Pour un nombre donné de commandes passées dans la durée de vie d’un client, le nombre de clients qui ont passé autant de commandes et le pourcentage de l’ensemble de la base de clients représentée par ce nombre. |
| `One-Time Customers who Bought 3-6 Months Ago` | Les clients qui ont effectué leur premier et unique achat il y a de trois à six mois. |
| `Avg LTV by First Order` | Compare les recettes cumulées moyennes sur la durée de vie des clients entre les cohortes. Les cohortes sont définies par le mois au cours duquel un client a effectué un premier achat. Par exemple, une cohorte de `Jan 2020` affiche la moyenne cumulée des télévisions pour les clients dont le premier achat a eu lieu en janvier 2020. |
| `Customer's First 30 Day vs Lifetime Revenue` | Comparaison des recettes moyennes des clients dans les 30 jours suivant leur premier achat et dans l’ensemble de leur vie. Chaque bulle correspond à une région d’expédition, et la taille de chaque bulle représente le nombre de clients acquis de cette région. |

## Clients (aucun passage en caisse autorisé pour les invités)

Le tableau de bord Clients (aucun passage en caisse invité autorisé) fournit des informations sur votre base de clients, telles que leur comportement d’achat et les conversions des inscriptions au compte vers les emplacements de commande. Ce tableau de bord peut vous aider à améliorer la rétention des clients et à déterminer les clients qui génèrent les recettes les plus élevées.

### Rapports

| Nom | Description |
|---|---|
| `Account Registration (Past 30 Days)` | Nombre de personnes qui se sont enregistrées pour un compte auprès de votre boutique au cours des 30 derniers jours. |
| `Accounts Registered (Past 30 Days) with 1 or More Orders` | Nombre de personnes qui se sont enregistrées pour un compte auprès de votre boutique au cours des 30 derniers jours et qui ont également passé au moins une commande. |
| `% Conversion from Registration to First Order (Past 30 Days)` | Pourcentage de comptes enregistrés au cours des 30 derniers jours ayant passé une commande. |
| `% Conversion from Registration to First Order` | Pourcentage des comptes enregistrés ayant passé une commande, par mois d’inscription. |
| `Orders by New vs Existing Customers` | Nombre de commandes passées par les clients n’ayant pas de commande précédente, par rapport aux clients ayant passé au moins une commande précédente. |
| `Subsequent Order Probability (All Time)` | La probabilité que les clients qui ont passé une commande en placent une autre. |
| `% of Customers with Multiple Orders (All Time)` | Pourcentage de tous les clients ayant passé plusieurs commandes. |
| `Median Time Between Orders (All Time)` | Durée moyenne de chaque client entre le placement d’une commande et le suivant. |
| `Subsequent Order Probability` | La probabilité que les clients qui ont passé une commande en placent une autre, ventilée par numéro de commande. C&#39;est-à-dire, le pourcentage de clients avec une commande qui en passent une seconde, le pourcentage de clients avec deux qui en passent une troisième, etc. |
| `Time Between Orders` | Le temps moyen et médian pris par les clients entre les commandes, ventilé par numéro de commande (c’est-à-dire le temps entre les commandes un et deux, deux et trois, etc.). |
| `Number of Customers - Lifetime Orders` | Pour un nombre donné de commandes passées dans la durée de vie d’un client, le nombre de clients qui ont passé autant de commandes et le pourcentage de l’ensemble de la base de clients représentée par ce nombre. |
| `One-Time Customers who Bought 3-6 Months Ago` | Les clients qui ont effectué leur premier et unique achat il y a de trois à six mois. |
| `Avg LTV by First Order` | Compare les recettes cumulées moyennes sur la durée de vie des clients entre les cohortes. Les cohortes sont définies par le mois au cours duquel un client a effectué un premier achat. Par exemple, une cohorte de janvier 2020 affiche la moyenne cumulée des télévisions pour les clients dont le premier achat a eu lieu en janvier 2020. |
| `Customer's First 30 Day vs Lifetime Revenue` | Comparaison des recettes moyennes des clients dans les 30 jours suivant leur premier achat et dans l’ensemble de leur vie. Chaque bulle correspond à une région d’expédition, et la taille de chaque bulle représente le nombre de clients acquis de cette région. |

## Résumé (passage en caisse des invités autorisé)

Le tableau de bord du résumé (paiement des invités autorisé) vous donne une vue succincte des commandes et des recettes de l’entreprise. Ce tableau de bord est conçu pour permettre aux cadres de mieux comprendre les performances de l’entreprise, mais il peut également être intéressant pour les autres.

### Rapports

| Nom | Description |
|---|---|
| `Revenue (Current Month)` | Les recettes générées par votre boutique pour le mois en cours. Dans ce cas, les recettes sont définies comme le prix final payé par un client lors d’une commande. |
| `Revenue (Past 6 Months by Day)` | Chiffre d’affaires quotidien total, superposé avec les recettes journalières moyennes pour les sept jours précédents. Dans ce cas, les recettes sont définies comme le prix final payé par un client lors d’une commande. |
| `% Change in Revenue (MoM MTD)` | Comparaison des recettes du mois en cours (à ce jour) et de la même partie du mois précédent. |
| `Revenue from New vs Existing Customers (Current Month)` | Recettes pour le mois en cours (jusqu’à présent) attribuées aux nouveaux clients (pour la première fois) par rapport aux clients existants (deuxième ou deuxième commande). |
| `Average Order Value (Current Month)` | Valeur moyenne quotidienne des commandes passées au cours du mois en cours (à ce jour). La valeur de la commande est définie comme le prix final payé par un client lors d’une commande. |
| `Orders (Current Month)` | Nombre de commandes passées dans votre boutique pour le mois en cours (jusqu’à présent). |
| `% Change in Orders (MoM MTD)` | Comparaison du nombre de commandes du mois en cours (à ce jour) par rapport à la même partie du mois précédent. |
| `Orders by New Customers (Current Month)` | Commandes pour le mois en cours de clients qui n’ont jamais passé de commande. |
| `Orders by Existing Customers (Current Month)` | Commandes pour le mois en cours des clients qui ont passé au moins une commande. |
| `Orders by New vs Existing Customers (Current Year by Week)` | Nombre de commandes passées par des clients n’ayant pas passé de commande, par rapport à des clients ayant passé au moins une commande, pour chaque semaine de l’année en cours (à ce jour). |

## Résumé (pas de passage en caisse des invités autorisé)

Le tableau de bord du résumé (pas de passage en caisse autorisé) vous donne une vue succincte de l’activité en termes de commandes, de recettes et d’inscriptions au compte. Ce tableau de bord est conçu pour permettre aux cadres de mieux comprendre les performances de l’entreprise, mais il peut également être intéressant pour les autres.

### Rapports

| Nom | Description |
|---|---|
| `Revenue (Current Month)` | Les recettes générées par votre magasin ce mois-ci. Dans ce cas, les recettes sont définies comme le prix final payé par un client lors d’une commande. |
| `Revenue (Past 6 Months by Day)` | Chiffre d’affaires quotidien total, superposé avec les recettes journalières moyennes pour les sept jours précédents. Dans ce cas, les recettes sont définies comme le prix final payé par un client lors d’une commande. |
| `% Change in Revenue (MoM MTD)` | Comparaison des recettes pour le mois en cours par rapport à la même partie du mois précédent. |
| `Revenue from New vs Existing Customers (Current Month)` | Recettes pour le mois en cours (jusqu’à présent) attribuées aux nouveaux clients (pour la première fois) par rapport aux clients existants (deuxième ou deuxième commande). |
| `Average Order Value (Current Month)` | Valeur moyenne quotidienne des commandes passées au cours du mois en cours (à ce jour). La valeur de la commande est définie comme le prix final payé par un client lors d’une commande. |
| `Orders (Current Month)` | Nombre de commandes passées dans votre boutique pour le mois en cours (jusqu’à présent). |
| `% Change in Orders (MoM MTD)` | Comparaison du nombre de commandes du mois en cours (à ce jour) par rapport à la même partie du mois précédent. |
| `Account Registrations (Current Month)` | Nombre de comptes nouvellement enregistrés jusqu’à présent ce mois-ci. |
| `% Conversion from Registration to First Order (Current Month)` | Le pourcentage de comptes enregistrés à ce jour ce mois-ci qui ont passé une commande. |
| `% Conversion from Registration to First Order (Current Year by Week)` | Le pourcentage de comptes enregistrés chaque semaine jusqu&#39;à présent cette année qui ont passé une commande. |

## Commandes

Le tableau de bord Commandes fournit des informations sur le volume transactionnel des commandes, leur statut, les codes de coupon utilisés, les recettes générées et les méthodes de paiement utilisées. Vous pouvez, par exemple, effectuer le suivi du processus d’exécution et vous assurer qu’il n’y a aucun problème ni aucune occurrence de goulot d’étranglement.

>[!NOTE]
>
>Les rapports de ce tableau de bord sont disponibles pour les comptes connectés à des magasins avec l’un ou l’autre type de configuration (passage en caisse des invités, pas de passage en caisse des invités).

### Rapports

| Nom | Description |
|---|---|
| `Orders (Past 30 Days)` | Nombre de commandes passées avec votre boutique au cours des 30 derniers jours. |
| `Revenue (Past 30 Days)` | Les recettes générées par votre boutique au cours des 30 derniers jours. Les recettes sont définies comme le prix final payé par un client lors d’une commande. |
| `Average Order Value (Past 30 Days)` | Valeur moyenne des commandes passées au cours des 30 derniers jours. La valeur de la commande est définie comme le prix final payé par un client lors d’une commande. |
| `Orders` | Nombre de commandes passées dans votre boutique chaque mois. |
| `Revenue by Payment Method` | Les recettes générées par votre boutique, fractionnées par mode de paiement. Les recettes sont définies comme le prix final payé par un client lors d’une commande. |
| `AOV by New vs Existing Customers` | Moyenne mensuelle des commandes passées en magasin, fractionnée par les commandes passées par des clients sans commandes précédentes, par rapport aux clients ayant passé au moins une commande. La valeur de la commande est définie comme le prix final payé par un client lors d’une commande. |
| `% Orders by Status (Past 30 Days)` | Pourcentage de commandes passées chaque jour au cours des 30 derniers jours et actuellement dans chaque état de commande. |
| `Incomplete Orders (Created more than 1 Day Ago)` | Liste de toutes les commandes passées il y a plus d’un jour et qui sont toujours dans un état incomplet (non annulées ou terminées). |
| `Orders Per Hour (Past 7 Days)` | Classer le volume par jour et par heure. |
| `Revenue Details (Past 30 Days)` | Ventilation des recettes quotidiennes pour les 30 derniers jours dans tous les composants de la valeur totale des recettes. |
| `Order Details by Coupon Code (Past 30 Days)` | Pour chaque code de bon proposé par votre boutique, des détails sur l’utilisation de ce code de bon et sur les retours apportés au cours des 30 derniers jours. |
| `% Orders with Coupon (Past 30 Days)` | Pourcentage de commandes passées au cours des 30 derniers jours qui utilisaient un coupon par rapport à celles qui n’en utilisaient pas. |

## Produits

Le tableau de bord Produits présente les performances générales du produit en termes de produits commandés, de leur valeur brute de marchandisage (GMV) et des principaux produits achetés et remboursés. Il peut vous aider à équilibrer les achats et les retours, ainsi qu’à déterminer le succès et la popularité du produit. Votre magasin doit être [ configuré pour effectuer le suivi des remboursements](https://experienceleague.adobe.com/docs/commerce-admin/customers/customer-accounts/store-credit/credit-configure.html) pour que ces graphiques soient renseignés.

>[!NOTE]
>
>Les rapports de ce tableau de bord sont disponibles pour les comptes connectés à des magasins avec l’un ou l’autre type de configuration (passage en caisse des invités, pas de passage en caisse des invités).

### Rapports

| Nom | Description |
|---|---|
| `GMV (Past 30 Days)` | La valeur brute de la marchandise de tous les produits vendus au cours des 30 derniers jours. Le GMV est défini comme la quantité commandée multipliée par le prix de base de chaque produit. |
| `% GMV (Past 30 Days) Refunded` | Pourcentage de GMV pour les produits achetés au cours des 30 derniers jours ayant abouti à un remboursement. |
| `Product Quantity Ordered (Past 30 Days)` | Nombre total d’articles commandés au cours des 30 derniers jours. |
| `% Purchased Products (Past 30 Days) Refunded` | Pourcentage d’articles achetés au cours des 30 derniers jours qui ont abouti à un remboursement. |
| `Gross Merchandise Value` | La valeur brute de la marchandise de tous les produits vendus, par mois. Le GMV est défini comme la quantité commandée multipliée par le prix de base de chaque produit. |
| `Purchases vs Refund Rate per Product (Past 30 Days)` | Pour chaque produit, une comparaison du nombre total commandé au cours des 30 derniers jours par rapport au taux de remboursement du produit. La taille de chaque bulle représente le taux de remboursement. |
| `Product Performance Details (Past 30 Days)` | Informations détaillées sur les ventes et les remboursements ultérieurs au cours des 30 derniers jours, par SKU et nom du produit. |
| `Top Purchased Products by GMV (Past 30 Days)` | Les produits vendus au cours des 30 derniers jours ont généré le plus de recettes (les 10 premiers). |
| `Top Refunded Products by GMV (Past 30 Days)` | Les produits achetés au cours des 30 derniers jours ont généré le plus de pertes de GMV dues aux remboursements (les 10 premiers). |
| `Top Purchased Products by Quantity (Past 30 Days)` | Les produits vendus dans les 30 derniers jours en grand nombre (10 meilleurs). |
| `Top Refunded Products by Quantity (Past 30 Days)` | Les produits achetés au cours des 30 derniers jours ont généré la plus grande quantité remboursée (les 10 premiers). |
