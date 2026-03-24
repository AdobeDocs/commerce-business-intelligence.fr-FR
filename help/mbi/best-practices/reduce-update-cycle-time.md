---
title: Réduction De La Durée Du Cycle De Mise À Jour
description: Découvrez comment réduire la durée du cycle de mise à jour.
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
role: Admin, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager, Dashboards
TQID: https://experienceleague.adobe.com/DFlzL9E95teiWI31j7qWRU8Ab6GkbFX7iPPdaxGq48A
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 398
ht-degree: 0%

---

# Réduction Du Temps De Traitement Du Cycle De Mise À Jour

[!DNL Adobe Commerce Intelligence] se synchronise avec votre base de données tout au long de la journée pour répliquer de nouvelles données, en veillant à ce que vos tableaux de bord affichent toujours les informations les plus récentes.

De nombreux facteurs peuvent s’ajouter à une durée de mise à jour déjà longue. Certaines méthodes de réplication, des fréquences de vérification plus élevées et le nombre de tableaux de bord et de graphiques ne sont que quelques-uns des facteurs qui contribuent à la situation. Cette rubrique présente quelques bonnes pratiques pour réduire le temps nécessaire à la mise à jour.

## Réduire la fréquence de revérification

Dans une table de base de données, il peut y avoir des colonnes de données dont les valeurs peuvent être modifiées. Par exemple, dans une table **orders** il peut y avoir une colonne appelée **status**. Lorsqu’une commande est initialement écrite dans la base de données, la colonne d’état peut contenir la valeur `pending`. La commande est répliquée dans votre [](../data-analyst/data-warehouse-mgr/tour-dwm.md) avec cette valeur de `pending`.

Les colonnes modifiables doivent être [revérifiées pour les valeurs mises à jour](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) au fil du temps. Par défaut, [!DNL Commerce Intelligence] vérifie à nouveau ces colonnes à chaque mise à jour, mais si une grande quantité de données doit être vérifiée et répliquée, cela peut avoir un impact négatif sur la durée de votre mise à jour. Au lieu d’exécuter des vérifications à chaque mise à jour, Adobe recommande de définir la fréquence de vérification sur quotidienne, hebdomadaire ou mensuelle.

## Utilisation de méthodes de réplication incrémentielle

Comme mentionné ci-dessus, les longues durées de mise à jour sont directement liées à la quantité de données à revérifier et à répliquer. [Les méthodes de réplication incrémentielle](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) peuvent réduire considérablement la quantité de données traitées pendant le cycle de mise à jour. Dans la mesure du possible, Adobe recommande d’utiliser ces méthodes ou de modifier votre base de données pour prendre en charge une méthode incrémentielle.

## Supprimer les graphiques inutilisés des tableaux de bord

À la fin du cycle de mise à jour, [!DNL Commerce Intelligence] effectue une opération de mise en cache pour tous les graphiques. Un cache stocke les données afin que les futures demandes d’informations puissent être traitées plus rapidement. En [!DNL Commerce Intelligence], cela signifie que les tableaux de bord se chargent rapidement, car les graphiques n’ont pas besoin d’interroger les données à chaque chargement.

Étant donné que [!DNL Commerce Intelligence] effectue uniquement des opérations de cache pour les graphiques figurant dans un tableau de bord, la suppression des graphiques inutilisés de vos tableaux de bord réduit le temps de mise à jour. N’oubliez pas que le même graphique peut se trouver sur plusieurs tableaux de bord. Vérifiez auprès de votre équipe qu’elle a également supprimé les graphiques inutilisés.

>[!NOTE]
>
>La suppression de graphiques de votre tableau de bord ne supprime pas le graphique. Vous pouvez [l’ajouter à tout moment](../data-user/dashboards/add-charts-dashboard.md).

## Optimisation de votre base de données pour l’analyse

En plus de réévaluer la fréquence des vérifications, les méthodes de réplication et l’utilité des graphiques, vous pouvez également [optimiser votre base de données pour l’analyse](../best-practices/opt-db-analysis.md).

## Conclusion

Si le temps nécessaire à la mise à jour semble toujours lent, même après l’implémentation de ces recommandations, [contactez l’équipe d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
