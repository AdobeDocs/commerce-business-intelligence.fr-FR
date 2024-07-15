---
title: Configuration des contrôles de données
description: Découvrez comment configurer des colonnes de données avec des valeurs modifiables.
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# Configuration des contrôles de données

Dans une table de base de données, il peut y avoir des colonnes de données avec des valeurs modifiables. Par exemple, dans une table `orders`, il peut y avoir une colonne appelée `status`. Lorsqu’une commande est initialement écrite dans la base de données, la colonne d’état peut contenir la valeur _pending_. L’ordre est répliqué dans votre [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) avec cette valeur `pending`.

Les états de commande peuvent changer, bien qu’ils ne soient pas toujours dans un état `pending`. Il peut éventuellement devenir `complete` ou `cancelled`. Pour vous assurer que votre Data Warehouse synchronise cette modification, la colonne doit être vérifiée à nouveau pour les nouvelles valeurs.

En quoi cela s’intègre-t-il aux [méthodes de réplication](../data-warehouse-mgr/cfg-replication-methods.md) discutées ? Le traitement des nouvelles vérifications varie en fonction de la méthode de réplication choisie. La méthode de réplication `Modified\_At` est le meilleur choix pour traiter les valeurs de changement, car les nouvelles vérifications n’ont pas à être configurées. Les méthodes `Auto-Incrementing Primary Key` et `Primary Key Batch Monitoring` nécessitent une configuration de nouveau contrôle.

Lors de l’utilisation de l’une de ces méthodes, les colonnes modifiables doivent être marquées pour la nouvelle vérification. Il existe trois façons de procéder :

1. Processus de contrôle qui s’exécute dans le cadre des colonnes des indicateurs de mise à jour à vérifier.

   >[!NOTE]
   >
   >L&#39;auditeur s&#39;appuie sur un processus d&#39;échantillonnage et les colonnes en évolution ne peuvent pas être capturées immédiatement.

1. Vous pouvez les définir vous-même en cochant la case en regard de la colonne dans le gestionnaire de Data Warehouse, en cliquant sur **[!UICONTROL Set Recheck Frequency]**, puis en sélectionnant un intervalle de temps approprié pour lequel vous devez vérifier les modifications.

1. Un membre de l’équipe de Data Warehouse [!DNL Adobe Commerce Intelligence] peut marquer manuellement les colonnes pour une nouvelle vérification dans votre Data Warehouse. Si vous connaissez des colonnes modifiables, contactez l’équipe pour demander que les nouvelles vérifications soient définies. Incluez une liste de colonnes, ainsi que la fréquence, à votre requête.

## Fréquences de rechargement {#frequency}

**Saviez-vous ?**
La définition d’une nouvelle vérification sur une colonne `primary key` ne vérifie pas la présence de valeurs modifiées dans la colonne. Le tableau recherche les lignes supprimées et toutes les suppressions sont purgées du Data Warehouse.

Lorsqu’une colonne est marquée pour une nouvelle vérification, vous pouvez également définir la fréquence à laquelle une nouvelle vérification a lieu. Si une colonne particulière ne change pas souvent, le choix d&#39;une vérification moins fréquente peut [optimiser votre cycle de mise à jour](../../best-practices/reduce-update-cycle-time.md).

Les options de fréquence sont les suivantes :

* `always` - la vérification a lieu à chaque mise à jour
* `daily` - la première vérification a lieu après minuit pour la mise à jour de votre fuseau horaire déclaré
* `weekly` - la vérification a lieu après 21 h, la mise à jour du vendredi toutes les semaines pour le fuseau horaire déclaré
* `monthly` - la vérification a lieu après 21 h, la mise à jour du vendredi toutes les quatre semaines pour le fuseau horaire déclaré
* `once` : survient uniquement lors de la prochaine mise à jour (actualisation ponctuelle)

Comme les heures de mise à jour sont corrélées à la quantité de données à synchroniser, Adobe recommande de choisir une nouvelle vérification `daily`, `weekly` ou `monthly` au lieu de chaque mise à jour.

## Gestion des fréquences de recontrôle {#manage}

Les fréquences de contrôle peuvent être gérées dans le Data Warehouse en cliquant sur le nom d&#39;une table, puis en vérifiant les colonnes individuelles. L&#39;état de synchronisation et la fréquence des nouvelles vérifications (les **Modifications ?**) s’affiche pour chaque colonne du tableau.

Pour modifier la fréquence de vérification, cochez la case en regard des colonnes que vous souhaitez modifier. Cliquez ensuite sur la liste déroulante **[!UICONTROL Set Recheck Frequency]** et définissez la fréquence souhaitée.

![](../../assets/dwm-recheck.png)

Vous pouvez parfois voir `Paused` dans la colonne `Changes?`. Cette valeur s’affiche lorsque la [méthode de réplication](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) de la table est définie sur `Paused`.

[!DNL Adobe] recommande de consulter ces colonnes afin d’optimiser vos mises à jour et de s’assurer que les colonnes modifiables sont à nouveau vérifiées. Si la fréquence de vérification d’une colonne est élevée, étant donné la fréquence à laquelle les données changent, Adobe recommande de la réduire afin d’optimiser vos mises à jour.

Contactez-nous pour toute question ou pour toute question concernant les méthodes de réplication ou les nouvelles vérifications actuelles.

**Associé :**

* [Réduction des temps de mise à jour](../../best-practices/reduce-update-cycle-time.md)
* [Optimisation de la base de données pour l’analyse](../../best-practices/opt-db-analysis.md)
