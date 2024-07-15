---
title: Utilisation d’un rapport
description: Découvrez comment utiliser les données de votre rapport.
exl-id: 94d4db27-0e06-4066-9c03-036b109d2d9b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 0%

---

# Utiliser un rapport

Utilisez les rapports de [!DNL Adobe Commerce Intelligence] pour vous aider à répondre aux questions professionnelles, que vous souhaitiez simplement consulter les recettes du mois par rapport à l’année dernière ou comprendre les coûts d’acquisition pour votre dernière campagne [!DNL Google AdWords].

A quoi ressemble exactement cette voie de question à réponse ?

Pour vous aider à visualiser ce processus, cet itinéraire est mappé ci-dessous. Ce sujet jette un éclairage sur la manière dont vous appréhendez une question analytique et sur la logistique du serveur principal nécessaire pour obtenir les données dont vous avez besoin.

## Commencer par la question

Vous savez que vous posez constamment des questions pour améliorer votre activité, de l’augmentation de la satisfaction client à la réduction des coûts d’approvisionnement. Vous vous concentrez sur la manière de traduire vos questions en analyses qui vous aident à prendre des décisions.

Dans cet exemple, supposons que vous souhaitiez répondre à la question suivante :

* À quelle vitesse mes nouveaux inscrits se convertissent-ils ?

## Identification d&#39;une mesure

Il est temps d&#39;identifier une liste d&#39;analyses et de mesures possibles pour aider à répondre à la question. Dans cet exemple, concentrez-vous sur la mesure suivante :

* Durée moyenne par utilisation entre l’enregistrement et la date du premier achat.

Cela révèle la durée moyenne qui s’écoule entre la date d’enregistrement et la première date d’achat des utilisateurs et donne une idée du comportement des utilisateurs à cette dernière étape de l’entonnoir de conversion.

## Recherche des données

Comprendre ce qu&#39;il faut mesurer ne fait qu&#39;y contribuer. Pour évaluer la durée moyenne entre l’enregistrement et la date du premier achat par utilisateur, vous devez identifier tous les points de données contenus dans votre mesure.

Ventilez votre mesure dans ses composants principaux. Vous devez connaître le nombre, ou le nombre, de personnes qui se sont enregistrées, le nombre de personnes qui ont effectué un achat et le temps qui s’est écoulé entre ces deux événements.

À un niveau supérieur, vous devez savoir où trouver ces données dans la base de données, en particulier :

* Le tableau qui enregistre une ligne de données chaque fois qu’une personne enregistre
* Le tableau qui enregistre une ligne de données chaque fois qu’une personne effectue un achat
* La colonne pouvant être utilisée pour joindre ou référencer la table `purchase` à la table `customer` : nous permet de savoir qui a effectué un achat.

À un niveau plus granulaire, vous devez identifier les champs de données exacts utilisés pour cette analyse :

* La table de données et la colonne contenant la date d&#39;enregistrement d&#39;un client : par exemple `user.created\_at`
* La table de données et la colonne contenant une date d’achat : par exemple `order.created\_at`

## Création de colonnes de données à analyser

Outre les colonnes de données natives décrites ci-dessus, vous avez également besoin d’un ensemble de champs de données calculées pour permettre cette analyse, notamment :

* `Customer's first purchase date` qui renvoie un `MIN(order.created_at` d’utilisateur spécifique)

Il est ensuite utilisé pour créer :

* `Time between a customer's registration date and first purchase date`, qui renvoie le délai d’un utilisateur spécifique écoulé entre l’enregistrement et la date du premier achat. C’est la base de votre mesure ultérieurement.

Ces deux champs doivent être créés au niveau de l’utilisateur (par exemple, sur la table `user`). Cela permet à l’analyse moyenne d’être normalisée par les utilisateurs (en d’autres termes, le dénominateur dans ce calcul de moyenne est le nombre d’utilisateurs).

C’est là que [!DNL Commerce Intelligence] entre en scène ! Vous pouvez utiliser votre Data Warehouse [!DNL Commerce Intelligence] pour créer les colonnes ci-dessus. Contactez l’équipe d’analystes d’Adobe et fournissez-nous la définition spécifique de vos nouvelles colonnes à créer. Vous pouvez également utiliser l’ [éditeur de colonnes](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

Il est recommandé d’éviter de créer directement ces champs de données calculés dans votre base de données, car cela impose une charge inutile à vos serveurs de production.

## Création de la mesure

Maintenant que vous disposez des champs de données requis pour l’analyse, il est temps de trouver ou de créer la mesure appropriée pour construire votre analyse.

Ici, vous souhaitez effectuer le calcul suivant :


_[SOMME de `Time between a customer's registration date and first purchase date`] / [Nombre total de clients qui se sont inscrits et ont acheté]_

Et vous souhaitez voir ce calcul tracé au fil du temps, ou tendance, en fonction de la date d’enregistrement d’un client. Et voici comment [créer cette mesure](../../data-user/reports/ess-manage-data-metrics.md) dans [!DNL Commerce Intelligence] :

1. Accédez à **[!UICONTROL Data]** et sélectionnez l’onglet `Metrics` .
1. Cliquez sur **[!UICONTROL Add New Metric]** et sélectionnez la table `user` (dans laquelle vous avez créé les dimensions ci-dessus).
1. Dans la liste déroulante, sélectionnez `Average` sur la colonne `Time between a customer's registration date and first purchase date` de la table `user` triée par la colonne `Customer's registration date`.
1. Ajoutez les filtres ou jeux de filtres appropriés.

Cette mesure est maintenant prête.

## Créer le rapport

Une fois la nouvelle mesure configurée, vous pouvez l’utiliser pour créer des rapports sur la durée moyenne entre l’enregistrement et la date du premier achat par date d’enregistrement.

Il vous suffit d’accéder à n’importe quel tableau de bord et de [créer un rapport](../../data-user/reports/ess-manage-data-metrics.md) à l’aide de la mesure créée ci-dessus.

### `Visual Report Builder` {#visualrb}

[ `Visual Report Builder`](../../data-user/reports/ess-rpt-build-visual.md) est le moyen le plus simple de visualiser vos données. Si vous ne connaissez pas SQL ou si vous souhaitez créer rapidement un rapport, le Report Builder visuel est votre meilleur choix. En quelques clics seulement, vous pouvez ajouter des mesures, segmenter vos données et créer des rapports pour l’ensemble de votre organisation. Cette option est idéale pour les débutants comme pour les experts, car elle ne nécessite aucune expertise technique.

|  |  |
|--- |--- |
| **C&#39;est parfait pour...** | **Ce n&#39;est pas très bien pour...** |
| - Tous les niveaux d’analyse/d’expérience technologique<br> - Création rapide de rapports<br> - Création d’analyses à partager avec d’autres utilisateurs | - Analyses nécessitant des fonctions spécifiques SQL<br> - Test de nouvelles colonnes - les colonnes calculées dépendent des cycles de mise à jour de la population de données initiale, contrairement à celles créées à l’aide de SQL. |

{style="table-layout:auto"}

### Descriptions des rapports et images

#### Ajout de descriptions aux rapports

Lors de la création de rapports partagés avec d’autres membres de votre équipe, Adobe recommande d’ajouter des descriptions qui permettent à d’autres utilisateurs de mieux comprendre votre analyse.

1. Cliquez sur **[!UICONTROL i]** en haut d’un rapport.
1. Saisissez une description dans la zone de texte.
1. Cliquez sur **[!UICONTROL Save Description]**.

Voir ci-dessous :

![Description du graphique](../../assets/Chart_Description.gif)

#### Exporter des rapports sous forme d’images

Vous devez inclure un rapport dans une présentation ou un document ? Tout rapport peut être enregistré sous forme d’image (au format PNG, PDF ou SVG) à l’aide du menu `Report Options`, situé dans le coin supérieur droit de chaque rapport.

1. Cliquez sur l’icône d’engrenage dans le coin supérieur droit d’un rapport.
1. Dans la liste déroulante, sélectionnez `Enlarge`.
1. Lorsque le rapport s’agrandit, cliquez sur **[!UICONTROL Download]** dans le coin supérieur droit du rapport.
1. Sélectionnez le format d’image préféré dans la liste déroulante. Le téléchargement commence immédiatement.

Voir ci-dessous :

![](../../assets/exp-rep-as-image.gif)
