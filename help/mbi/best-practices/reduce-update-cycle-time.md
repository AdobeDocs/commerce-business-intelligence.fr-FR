---
title: Réduction du temps de cycle de mise à jour
description: Découvrez comment réduire la durée de votre cycle de mise à jour.
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
role: Admin, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Réduction du temps de traitement du cycle de mise à jour

[!DNL Adobe Commerce Intelligence] se synchronise avec votre base de données tout au long de la journée pour répliquer les nouvelles données, en veillant à ce que vos tableaux de bord affichent toujours les informations les plus récentes.

De nombreux facteurs peuvent ajouter à un temps de mise à jour déjà long. Certaines méthodes de réplication, des fréquences de contrôle plus élevées et le nombre de tableaux de bord et de graphiques ne sont que quelques facteurs. Cette rubrique présente certaines bonnes pratiques pour réduire les temps de mise à jour.

## Diminuer la fréquence de rechargement

Dans une table de base de données, il peut y avoir des colonnes de données avec des valeurs modifiables. Par exemple, dans une table **orders**, il peut y avoir une colonne appelée **status**. Lorsqu’une commande est initialement écrite dans la base de données, la colonne d’état peut contenir la valeur `pending`. L’ordre est répliqué dans votre [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) avec cette valeur `pending`.

Les colonnes modifiables doivent être [ revérifiées pour les valeurs mises à jour ](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) au fil du temps. Par défaut, [!DNL Commerce Intelligence] vérifie à nouveau ces colonnes à chaque mise à jour, mais s’il existe une grande quantité de données à vérifier et à répliquer, cela peut avoir une incidence négative sur le temps de mise à jour. Au lieu d’exécuter des nouvelles vérifications à chaque mise à jour, Adobe recommande de définir la fréquence des nouvelles vérifications sur une fréquence quotidienne, hebdomadaire ou mensuelle.

## Utilisation de méthodes de réplication incrémentielle

Comme mentionné ci-dessus, les temps de mise à jour longs sont directement corrélés à la quantité de données à vérifier et à répliquer. [Les méthodes de réplication incrémentielle](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) peuvent réduire considérablement la quantité de données traitées pendant le cycle de mise à jour. Si possible, Adobe recommande d’utiliser ces méthodes ou de modifier votre base de données pour prendre en charge une méthode incrémentielle.

## Suppression des graphiques inutilisés des tableaux de bord

À la fin du cycle de mise à jour, [!DNL Commerce Intelligence] effectue une opération de mise en cache pour tous les graphiques. Un cache stocke les données afin que les demandes d’informations ultérieures puissent être effectuées plus rapidement. Dans [!DNL Commerce Intelligence], cela signifie que les tableaux de bord se chargent rapidement, car les graphiques n’ont pas besoin d’interroger les données à chaque chargement.

Puisque [!DNL Commerce Intelligence] effectue uniquement des opérations de mise en cache pour les graphiques figurant dans un tableau de bord, la suppression des graphiques inutilisés des tableaux de bord réduit la durée de mise à jour. Gardez à l’esprit que le même graphique peut se trouver sur plusieurs tableaux de bord. Vérifiez auprès de votre équipe qu’il a également supprimé les graphiques inutilisés.

>[!NOTE]
>
>Le fait de supprimer des graphiques du tableau de bord ne les supprime pas. Vous pouvez [l&#39;ajouter à tout moment](../data-user/dashboards/add-charts-dashboard.md).

## Optimisation de la base de données pour l’analyse

Outre la réévaluation des fréquences de contrôle, des méthodes de réplication et de l&#39;utilité des graphiques, vous pouvez également [optimiser votre base de données pour l&#39;analyse](../best-practices/opt-db-analysis.md).

## Remplissage

Si le temps de mise à jour semble encore long même après la mise en oeuvre de ces recommandations, [contactez l&#39;équipe d&#39;assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr).
