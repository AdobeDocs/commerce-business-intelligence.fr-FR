---
title: Utilisation d’un rapport
description: Découvrez comment utiliser les données de votre rapport.
exl-id: 94d4db27-0e06-4066-9c03-036b109d2d9b
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 0%

---

# Utilisation d’un rapport

Utilisation des rapports dans [!DNL Adobe Commerce Intelligence] pour vous aider à répondre aux questions d’entreprise, que vous souhaitiez simplement consulter les recettes de ce mois par rapport à l’année précédente ou comprendre vos coûts d’acquisition pour vos dernières [!DNL Google AdWords] campaign.

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
* La colonne qui peut être utilisée pour joindre ou référencer le `purchase` au `customer` table : permet de savoir qui a effectué un achat.

À un niveau plus granulaire, vous devez identifier les champs de données exacts utilisés pour cette analyse :

* Le tableau de données et la colonne contenant la date d’enregistrement d’un client : par exemple `user.created\_at`
* Le tableau de données et la colonne contenant une date d’achat : par exemple `order.created\_at`

## Création de colonnes de données à analyser

Outre les colonnes de données natives décrites ci-dessus, vous avez également besoin d’un ensemble de champs de données calculées pour permettre cette analyse, notamment :

* `Customer's first purchase date` qui renvoie un `MIN(order.created_at`)

Il est ensuite utilisé pour créer :

* `Time between a customer's registration date and first purchase date`, qui renvoie l’intervalle d’un utilisateur spécifique entre l’enregistrement et la date du premier achat. C’est la base de votre mesure ultérieurement.

Ces deux champs doivent être créés au niveau de l’utilisateur (par exemple, sur la variable `user` ). Cela permet à l’analyse moyenne d’être normalisée par les utilisateurs (en d’autres termes, le dénominateur dans ce calcul de moyenne est le nombre d’utilisateurs).

C’est là que [!DNL Commerce Intelligence] entrez ! Vous pouvez utiliser [!DNL Commerce Intelligence] Data Warehouse pour créer les colonnes ci-dessus. Contactez l’équipe d’analystes d’Adobe et fournissez-nous la définition spécifique de vos nouvelles colonnes à créer. Vous pouvez également utiliser la variable [Éditeur de colonnes](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

Il est recommandé d’éviter de créer directement ces champs de données calculés dans votre base de données, car cela impose un fardeau inutile aux serveurs de production.

## Création de la mesure

Maintenant que vous disposez des champs de données requis pour l’analyse, il est temps de trouver ou de créer la mesure appropriée pour construire votre analyse.

Ici, vous souhaitez effectuer le calcul suivant :


_[SOMME de `Time between a customer's registration date and first purchase date`] / [Nombre total de clients qui se sont inscrits et ont acheté]_

Et vous souhaitez voir ce calcul tracé au fil du temps, ou tendance, selon la date d’enregistrement d’un client. Et voici comment [créer cette mesure](../../data-user/reports/ess-manage-data-metrics.md) in [!DNL Commerce Intelligence]:

1. Accédez à **[!UICONTROL Data]** et sélectionnez la variable `Metrics` .
1. Cliquez sur **[!UICONTROL Add New Metric]** et sélectionnez la variable `user` (où vous avez créé les dimensions ci-dessus).
1. Dans la liste déroulante, sélectionnez `Average` sur le`Time between a customer's registration date and first purchase date` dans la colonne `user` tableau trié par la variable `Customer's registration date`  colonne .
1. Ajoutez les filtres ou jeux de filtres appropriés.

Cette mesure est maintenant prête.

## Créer le rapport

Une fois la nouvelle mesure configurée, vous pouvez l’utiliser pour créer des rapports sur la durée moyenne entre l’enregistrement et la date du premier achat par date d’enregistrement.

Il vous suffit d’accéder à n’importe quel tableau de bord et [création d’un rapport](../../data-user/reports/ess-manage-data-metrics.md) en utilisant la mesure créée ci-dessus.

### `Visual Report Builder` {#visualrb}

[Le `Visual Report Builder`](../../data-user/reports/ess-rpt-build-visual.md) est le moyen le plus simple de visualiser vos données. Si vous ne connaissez pas SQL ou si vous souhaitez créer rapidement un rapport, le Report Builder visuel est votre meilleur choix. En quelques clics seulement, vous pouvez ajouter des mesures, segmenter vos données et créer des rapports pour l’ensemble de votre organisation. Cette option est idéale pour les débutants comme pour les experts, car elle ne nécessite aucune expertise technique.

|  |  |
|--- |--- |
| **C&#39;est parfait pour...** | **Ce n&#39;est pas si bien pour...** |
| - Tous les niveaux d’analyse/d’expérience technologique<br>- Création rapide de rapports<br>- Créer des analyses à partager avec d&#39;autres utilisateurs | - Analyses nécessitant des fonctions spécifiques à SQL<br>- Test de nouvelles colonnes : les colonnes calculées dépendent des cycles de mise à jour de la population initiale de données, contrairement à celles créées à l’aide de SQL. |

{style="table-layout:auto"}

### Descriptions des rapports et images

#### Ajout de descriptions aux rapports

Lors de la création de rapports partagés avec d’autres membres de votre équipe, Adobe recommande d’ajouter des descriptions qui permettent à d’autres utilisateurs de mieux comprendre votre analyse.

1. Cliquez sur **[!UICONTROL i]** dans la partie supérieure de tout rapport.
1. Saisissez une description dans la zone de texte.
1. Cliquez sur **[!UICONTROL Save Description]**.

Voir ci-dessous :

![Description du graphique](../../assets/Chart_Description.gif)

#### Exporter des rapports sous forme d’images

Vous devez inclure un rapport dans une présentation ou un document ? Tout rapport peut être enregistré sous forme d’image (au format PNG, PDF ou SVG) à l’aide de la variable `Report Options` dans le coin supérieur droit de chaque rapport.

1. Cliquez sur l’icône d’engrenage dans le coin supérieur droit d’un rapport.
1. Dans la liste déroulante, sélectionnez `Enlarge`.
1. Lorsque le rapport s’agrandit, cliquez sur **[!UICONTROL Download]** dans le coin supérieur droit du rapport.
1. Sélectionnez le format d’image de votre choix dans la liste déroulante. Le téléchargement commence immédiatement.

Voir ci-dessous :

![](../../assets/exp-rep-as-image.gif)
