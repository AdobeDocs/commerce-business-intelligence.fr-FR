---
title: Utilisation d’un rapport
description: Découvrez comment utiliser vos données de rapport.
exl-id: 94d4db27-0e06-4066-9c03-036b109d2d9b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 0%

---

# Utiliser un rapport

Utilisez les rapports dans [!DNL Adobe Commerce Intelligence] pour répondre aux questions commerciales, que vous souhaitiez simplement consulter le chiffre d’affaires de ce mois par rapport à l’année dernière ou comprendre vos coûts d’acquisition pour votre dernière campagne [!DNL Google AdWords].

À quoi ressemble exactement le cheminement de la question à la réponse?

Pour vous aider à visualiser ce processus, cet itinéraire est mappé ci-dessous. Cette rubrique apporte un éclairage sur la manière d’aborder une question analytique et sur la logistique back-end requise pour obtenir les données dont vous avez besoin.

## Commencer par la question

Vous savez que vous posez constamment des questions pour améliorer votre entreprise, de l&#39;augmentation de la satisfaction de la clientèle à la réduction des coûts d&#39;approvisionnement. Vous vous concentrez sur la traduction de vos questions en analyses qui vous aident à prendre des décisions éclairées.

Pour cet exemple, supposons que vous souhaitiez répondre à la question suivante :

* À quelle vitesse mes nouveaux inscrits se convertissent-ils ?

## Identification d’une mesure

Il est temps d&#39;établir une liste d&#39;analyses et de mesures possibles pour aider à répondre à la question. Pour cet exemple, concentrez-vous sur la mesure suivante :

* Durée moyenne depuis l&#39;enregistrement jusqu&#39;à la première date d&#39;achat par utilisation.

Il révèle le temps moyen écoulé entre la date d’enregistrement et la première date d’achat des utilisateurs et donne une idée du comportement des utilisateurs à cette dernière étape de l’entonnoir de conversion.

## Recherche des données

Comprendre ce qu’il faut mesurer ne nous permet d’y parvenir qu’en partie. Pour évaluer le temps moyen écoulé entre l’enregistrement et la première date d’achat par utilisateur, vous devez identifier tous les points de données dont est composée votre mesure.

Ventilez votre mesure en ses composants principaux. Vous devez connaître le nombre de personnes qui se sont inscrites, le nombre de personnes qui ont fait un achat et le temps qui s&#39;est écoulé entre ces deux événements.

À un niveau supérieur, vous devez savoir où trouver ces données dans la base de données, en particulier :

* Le tableau qui enregistre une ligne de données chaque fois qu’une personne s’enregistre
* Le tableau qui enregistre une ligne de données chaque fois qu’un utilisateur effectue un achat
* La colonne qui peut être utilisée pour joindre ou référencer la table de `purchase` à la table de `customer`. Cela nous permet de savoir qui a effectué un achat

À un niveau plus granulaire, vous devez identifier les champs de données exacts utilisés pour cette analyse :

* Le tableau et la colonne de données qui contiennent la date d’enregistrement d’un client ou d’une cliente : par exemple, `user.created\_at`
* Le tableau et la colonne de données contenant une date d’achat : par exemple, `order.created\_at`

## Création de colonnes de données pour l&#39;analyse

Outre les colonnes de données natives décrites ci-dessus, vous avez également besoin d’un ensemble de champs de données calculés pour activer cette analyse, notamment :

* `Customer's first purchase date` qui renvoie le `MIN(order.created_at` d’un utilisateur spécifique)

qui est ensuite utilisé pour créer :

* `Time between a customer's registration date and first purchase date`, qui renvoie le temps écoulé par un utilisateur spécifique entre l’enregistrement et la première date d’achat. C’est la base de votre mesure ultérieurement.

Ces deux champs doivent être créés au niveau de l’utilisateur (par exemple, dans le tableau `user` ). Cela permet de normaliser l&#39;analyse moyenne par les utilisateurs (en d&#39;autres termes, le dénominateur dans ce calcul de moyenne est le nombre d&#39;utilisateurs).

C&#39;est là que [!DNL Commerce Intelligence] intervient ! Vous pouvez utiliser votre [!DNL Commerce Intelligence] Data Warehouse pour créer les colonnes ci-dessus. Contactez l’équipe d’analystes d’Adobe et fournissez la définition spécifique de vos nouvelles colonnes à créer. Vous pouvez également utiliser l’[éditeur de colonnes](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

Il est recommandé d’éviter de créer directement ces champs de données calculés dans votre base de données, car cela alourdit inutilement les serveurs de production.

## Création de la mesure

Maintenant que vous disposez des champs de données requis pour l’analyse, il est temps de trouver ou de créer la mesure appropriée pour construire votre analyse.

Ici, vous devez effectuer le calcul suivant :


_[SOMME des `Time between a customer's registration date and first purchase date`] / [Nombre total de clients qui se sont inscrits et qui ont acheté]_

Et vous souhaitez que ce calcul soit porté au fil du temps, ou en tendance, en fonction de la date d’enregistrement d’un client. Et voici comment [créer cette mesure](../../data-user/reports/ess-manage-data-metrics.md) dans [!DNL Commerce Intelligence] :

1. Accédez à **[!UICONTROL Data]** et sélectionnez l’onglet `Metrics` .
1. Cliquez sur **[!UICONTROL Add New Metric]** et sélectionnez la table de `user` (où vous avez créé les dimensions ci-dessus).
1. Dans la liste déroulante, sélectionnez `Average` dans la colonne `Time between a customer's registration date and first purchase date` du tableau `user` trié par la colonne `Customer's registration date` .
1. Ajoutez des filtres ou des ensembles de filtres appropriés.

Cette mesure est maintenant prête.

## Créer le rapport

La nouvelle mesure étant configurée, vous pouvez l’utiliser pour générer des rapports sur le temps moyen écoulé entre l’enregistrement et la première date d’achat, par date d’enregistrement.

Il vous suffit d’accéder à n’importe quel tableau de bord et de [créer un rapport](../../data-user/reports/ess-manage-data-metrics.md) en utilisant la mesure créée ci-dessus.

### `Visual Report Builder` {#visualrb}

[La `Visual Report Builder`](../../data-user/reports/ess-rpt-build-visual.md) est le moyen le plus simple de visualiser vos données. Si vous ne connaissez pas SQL ou si vous souhaitez créer rapidement un rapport, le Visual Report Builder est le meilleur choix. En quelques clics seulement, vous pouvez ajouter des mesures, segmenter vos données et créer des rapports pour à l’échelle de votre organisation. Cette option est parfaite pour les débutants comme pour les experts, car elle ne nécessite aucune expertise technique.

|  |  |
|--- |--- |
| **C&#39;est parfait pour...** | **Ce n&#39;est pas si génial pour...** |
| - Tous les niveaux d’analyse/d’expérience technique<br>- Création rapide de rapports<br>- Création d’analyses à partager avec d’autres utilisateurs | - Analyses qui nécessitent des fonctions spécifiques à SQL<br>- Test de nouvelles colonnes - Les colonnes calculées dépendent des cycles de mise à jour pour le remplissage de données initial, contrairement à celles créées à l’aide de SQL. |

{style="table-layout:auto"}

### Descriptions des rapports et images

#### Ajout de descriptions aux rapports

Lors de la création de rapports partagés avec d’autres membres de votre équipe, Adobe recommande d’ajouter des descriptions qui permettent à d’autres utilisateurs de mieux comprendre votre analyse.

1. Cliquez sur **[!UICONTROL i]** en haut de n’importe quel rapport.
1. Saisissez une description dans la zone des mots.
1. Cliquez sur **[!UICONTROL Save Description]**.

Voir ci-dessous :

![Description du graphique](../../assets/Chart_Description.gif)

#### Exportation de rapports en tant qu’images

Vous souhaitez inclure un rapport dans une présentation ou un document ? Tout rapport peut être enregistré en tant qu’image (au format PNG, PDF ou SVG) à l’aide du menu `Report Options` situé dans le coin supérieur droit de chaque rapport.

1. Cliquez sur l’icône d’engrenage dans le coin supérieur droit d’un rapport.
1. Dans la liste déroulante, sélectionnez `Enlarge`.
1. Lorsque le rapport s’agrandit, cliquez sur **[!UICONTROL Download]** dans le coin supérieur droit du rapport.
1. Sélectionnez le format d’image souhaité dans la liste déroulante. Le téléchargement commence immédiatement.

Voir ci-dessous :

![](../../assets/exp-rep-as-image.gif)
