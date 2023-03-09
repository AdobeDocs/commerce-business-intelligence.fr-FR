---
title: Configuration des contrôles de données
description: Découvrez comment configurer des colonnes de données avec des valeurs modifiables.
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# Configuration des contrôles de données

Dans une table de base de données, il peut y avoir des colonnes de données avec des valeurs modifiables. Par exemple, dans un `orders`). Il peut y avoir une colonne appelée `status`. Lorsqu’une commande est initialement écrite dans la base de données, la colonne d’état peut contenir la valeur _pending_. L’ordre est répliqué dans votre [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) avec `pending` .

Les statuts des commandes peuvent toutefois changer, car ils ne sont pas toujours dans un `pending` statut. Finalement elle pourrait devenir `complete` ou `cancelled`. Pour vous assurer que votre Data Warehouse synchronise cette modification, la colonne doit être vérifiée à nouveau pour les nouvelles valeurs.

En quoi cela s’intègre-t-il à la variable [méthodes de réplication](../data-warehouse-mgr/cfg-replication-methods.md) qui a été discuté ? Le traitement des nouvelles vérifications varie en fonction de la méthode de réplication choisie. Le `Modified\_At` la méthode de réplication est le meilleur choix pour le traitement des valeurs qui changent, car les nouvelles vérifications n’ont pas à être configurées. Le `Auto-Incrementing Primary Key` et `Primary Key Batch Monitoring` Les méthodes nécessitent une configuration de nouveau contrôle.

Lors de l’utilisation de l’une de ces méthodes, les colonnes modifiables doivent être marquées pour la nouvelle vérification. Il existe trois façons de procéder :

* Processus de contrôle qui s’exécute dans le cadre des colonnes des indicateurs de mise à jour à vérifier.

   >[!NOTE]
   >
   >L&#39;auditeur s&#39;appuie sur un processus d&#39;échantillonnage et les colonnes en évolution ne peuvent pas être capturées immédiatement.

* Vous pouvez les définir vous-même en cochant la case en regard de la colonne dans le Gestionnaire de Data Warehouse, en cliquant sur **[!UICONTROL Set Recheck Frequency]**, et en choisissant un intervalle de temps approprié pour lequel vous devez vérifier les modifications.
* Un membre du [!DNL MBI] L’équipe de Data Warehouse peut marquer manuellement les colonnes à des fins de nouvelle vérification dans votre Data Warehouse. Si vous connaissez des colonnes modifiables, contactez l’équipe pour demander que les nouvelles vérifications soient définies. Incluez une liste de colonnes, ainsi que la fréquence, à votre requête.

## Fréquences de rechargement {#frequency}

**Le saviez-vous ?**
Définir une nouvelle vérification sur un `primary key` ne vérifie pas les valeurs modifiées dans la colonne. Le tableau recherche les lignes supprimées et toutes les suppressions sont purgées du Data Warehouse.

Lorsqu’une colonne est marquée pour une nouvelle vérification, vous pouvez également définir la fréquence à laquelle une nouvelle vérification a lieu. Si une colonne particulière ne change pas souvent, le choix d’une vérification moins fréquente peut [optimiser votre cycle de mise à jour](../../best-practices/reduce-update-cycle-time.md).

Les options de fréquence sont les suivantes :

* `always` - une nouvelle vérification survient à chaque mise à jour
* `daily` - la première vérification a lieu après la mise à jour de minuit pour votre fuseau horaire déclaré
* `weekly` - la vérification a lieu après 21 h, la mise à jour du vendredi a lieu chaque semaine pour votre fuseau horaire déclaré.
* `monthly` - la vérification a lieu après 21 h, la mise à jour du vendredi toutes les quatre semaines pour le fuseau horaire déclaré
* `once` : ne se produit que lors de la prochaine mise à jour (actualisation ponctuelle)

Comme les heures de mise à jour sont corrélées à la quantité de données à synchroniser, Adobe recommande de choisir une `daily`, `weekly`ou `monthly` revérifiez plutôt que chaque mise à jour.

## Gestion des fréquences de recontrôle {#manage}

Les fréquences de contrôle peuvent être gérées dans le Data Warehouse en cliquant sur le nom d&#39;une table, puis en vérifiant les colonnes individuelles. L’état de synchronisation et la fréquence de vérification (le **Changements ?** s’affiche pour chaque colonne du tableau.

Pour modifier la fréquence de vérification, cochez la case en regard des colonnes que vous souhaitez modifier. Cliquez ensuite sur le bouton **[!UICONTROL Set Recheck Frequency]** et définissez la fréquence souhaitée.

![](../../assets/dwm-recheck.png)

Parfois, vous verrez `Paused` dans le `Changes?` colonne . Cette valeur s’affiche lorsque le [méthode de réplication](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) est défini sur `Paused`.

Adobe recommande de consulter ces colonnes afin d’optimiser vos mises à jour et de s’assurer que les colonnes modifiables sont à nouveau vérifiées. Si la fréquence de vérification d’une colonne est élevée, étant donné la fréquence à laquelle les données changent, Adobe recommande de la réduire afin d’optimiser vos mises à jour.

Contactez-nous pour toute question ou pour toute question concernant les méthodes de réplication ou les nouvelles vérifications actuelles.

**En rapport :**

* [Réduction des temps de mise à jour](../../best-practices/reduce-update-cycle-time.md)
* [Optimisation de la base de données pour l’analyse](../../best-practices/opt-db-analysis.md)
