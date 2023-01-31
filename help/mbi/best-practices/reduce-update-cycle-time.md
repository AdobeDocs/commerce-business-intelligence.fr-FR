---
title: Réduction du temps de cycle de mise à jour
description: Découvrez comment réduire la durée de votre cycle de mise à jour.
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# Réduction du temps de traitement du cycle de mise à jour

[!DNL MBI] se synchronise avec votre base de données tout au long de la journée pour répliquer les nouvelles données, en veillant à ce que vos tableaux de bord affichent toujours les informations les plus récentes.

De nombreux facteurs peuvent s’ajouter à un temps de mise à jour déjà long. Certaines méthodes de réplication, des fréquences de contrôle plus élevées et le nombre de tableaux de bord et de graphiques ne sont que quelques facteurs. Cette rubrique présente certaines bonnes pratiques pour réduire les temps de mise à jour.

## Diminuer la fréquence de rechargement

Dans une table de base de données, il peut y avoir des colonnes de données avec des valeurs modifiables. Par exemple, dans un **commandes** tableau il peut y avoir une colonne appelée **status**. Lorsqu’une commande est initialement écrite dans la base de données, la colonne d’état peut contenir la valeur `pending`. L’ordre sera ensuite répliqué dans votre [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) avec `pending` .

Les colonnes modifiables doivent être [revérifié pour les valeurs mises à jour](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) au fil du temps. Par défaut, [!DNL MBI] vérifie ces colonnes à chaque mise à jour, mais s’il existe une grande quantité de données à vérifier et à répliquer, cela peut avoir une incidence négative sur le temps de mise à jour. Au lieu d’exécuter des nouvelles vérifications à chaque mise à jour, nous vous recommandons de définir la fréquence des nouvelles vérifications sur une fréquence quotidienne, hebdomadaire ou mensuelle.

## Utilisation de méthodes de réplication incrémentielle

Comme mentionné ci-dessus, les temps de mise à jour longs sont directement corrélés à la quantité de données à vérifier et à répliquer. [Méthodes de réplication incrémentielle](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) peut réduire considérablement la quantité de données traitées pendant le cycle de mise à jour. Dans la mesure du possible, nous vous recommandons d’utiliser ces méthodes ou d’apporter des modifications à votre base de données pour prendre en charge une méthode incrémentielle.

## Suppression des graphiques inutilisés des tableaux de bord

A la fin du cycle de mise à jour, [!DNL MBI] exécute une opération de mise en cache pour tous les graphiques. Un cache stocke les données afin que les demandes d’informations ultérieures puissent être effectuées plus rapidement. Dans [!DNL MBI], cela signifie que les tableaux de bord se chargent rapidement, car les graphiques n’ont pas besoin d’interroger les données à chaque chargement.

Depuis [!DNL MBI] effectue uniquement des opérations de cache pour les graphiques figurant dans un tableau de bord ; la suppression des graphiques inutilisés des tableaux de bord réduit le temps de mise à jour. Gardez à l’esprit que le même graphique peut se trouver sur plusieurs tableaux de bord. Vérifiez auprès de votre équipe qu’il a également supprimé les graphiques inutilisés.

>[!NOTE]
>
>Le fait de supprimer des graphiques du tableau de bord ne les supprime pas. Vous pouvez [à chaque fois que vous le rajoutez](../data-user/dashboards/add-charts-dashboard.md).

## Optimisation de la base de données pour l’analyse

Outre la réévaluation des fréquences de contrôle, des méthodes de réplication et de l’utilité des graphiques, vous pouvez également [optimiser votre base de données pour l’analyse ;](../best-practices/opt-db-analysis.md).

## Remplissage

Si le temps de mise à jour semble encore lent, même après la mise en oeuvre de ces recommandations, [contactez notre équipe d’assistance](../guide-overview.md).
