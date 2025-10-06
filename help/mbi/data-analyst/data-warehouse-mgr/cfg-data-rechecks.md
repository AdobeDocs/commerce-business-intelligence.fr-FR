---
title: Configuration des contrôles de données
description: Découvrez comment configurer des colonnes de données avec des valeurs modifiables.
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Configuration des contrôles de données

Dans une table de base de données, il peut y avoir des colonnes de données dont les valeurs peuvent être modifiées. Par exemple, dans un tableau `orders`, il peut y avoir une colonne appelée `status`. Lorsqu’une commande est initialement écrite dans la base de données, la colonne d’état peut contenir la valeur _en attente_. La commande est répliquée dans votre [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) avec cette valeur de `pending`.

Les statuts de commande peuvent changer, mais ils ne sont pas toujours dans un statut `pending`. Cela pourrait finir par devenir `complete` ou `cancelled`. Pour que votre Data Warehouse synchronise cette modification, de nouvelles valeurs doivent être recherchées dans la colonne.

Comment cela s’intègre-t-il avec les [ méthodes de réplication ](../data-warehouse-mgr/cfg-replication-methods.md) qui ont été abordées ? Le traitement des nouvelles vérifications varie en fonction de la méthode de réplication choisie. La méthode de réplication `Modified\_At` est le meilleur choix pour traiter les valeurs qui changent, car les revérifications n’ont pas à être configurées. Les méthodes `Auto-Incrementing Primary Key` et `Primary Key Batch Monitoring` nécessitent de revérifier la configuration.

Lors de l’utilisation de l’une de ces méthodes, les colonnes modifiables doivent être marquées pour vérification. Pour ce faire, trois méthodes sont possibles :

1. Processus d’audit s’exécutant dans le cadre de la mise à jour des colonnes d’indicateurs à revérifier.

   >[!NOTE]
   >
   >L&#39;auditeur s&#39;appuie sur un processus d&#39;échantillonnage et il se peut que les colonnes changeantes ne soient pas détectées immédiatement.

1. Vous pouvez les définir vous-même en cochant la case en regard de la colonne dans le gestionnaire Data Warehouse, en cliquant sur **[!UICONTROL Set Recheck Frequency]**, puis en choisissant un intervalle approprié pour le moment où vous devez vérifier les modifications.

1. Un membre de l’équipe [!DNL Adobe Commerce Intelligence] Data Warehouse peut marquer manuellement les colonnes pour les réarchiver dans votre Data Warehouse. Si vous connaissez des colonnes modifiables, contactez l’équipe pour demander que des revérifications soient définies. Incluez une liste de colonnes, ainsi que la fréquence, avec votre requête.

## Vérifier à nouveau les fréquences {#frequency}

**Le saviez-vous ?**
La définition d’une revérification sur une colonne `primary key` ne vérifie pas les valeurs modifiées dans la colonne. La recherche des lignes supprimées dans le tableau est effectuée et toutes les suppressions sont purgées du Data Warehouse.

Lorsqu’une colonne est marquée pour vérification, vous pouvez également définir la fréquence de vérification. Si une colonne particulière ne change pas souvent, le choix d’une revérification moins fréquente peut [optimiser votre cycle de mise à jour](../../best-practices/reduce-update-cycle-time.md).

Les options de fréquence sont :

* `always` - une nouvelle vérification se produit lors de chaque mise à jour
* `daily` - une nouvelle vérification a lieu après la première mise à jour de minuit pour votre fuseau horaire déclaré
* `weekly` - une nouvelle vérification de votre fuseau horaire déclaré est effectuée chaque semaine après 21h00, le vendredi
* `monthly` - une nouvelle vérification de votre fuseau horaire déclaré est effectuée toutes les quatre semaines après 21h00
* `once` - survient uniquement lors de la prochaine mise à jour (actualisation ponctuelle)

Comme les durées de mise à jour sont corrélées à la quantité de données à synchroniser, Adobe recommande de choisir un `daily`, une `weekly` ou une revérification de `monthly` au lieu de chaque mise à jour.

## Gestion des fréquences de vérification {#manage}

Les fréquences de revérification peuvent être gérées dans le Data Warehouse en cliquant sur le nom d’un tableau, puis en vérifiant les colonnes individuelles. Le statut de synchronisation et la fréquence de revérification (le **Modifications ?** colonne) s’affiche pour chaque colonne du tableau.

Pour modifier la fréquence de revérification, cochez la case en regard des colonnes à modifier. Cliquez ensuite sur la liste déroulante **[!UICONTROL Set Recheck Frequency]** et définissez la fréquence souhaitée.

![Data Warehouse Manager affiche les options de configuration de revérification](../../assets/dwm-recheck.png)

Il se peut que vous voyiez parfois des `Paused` dans la colonne `Changes?` . Cette valeur s&#39;affiche lorsque la méthode de réplication [ de la table](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) est définie sur `Paused`.

[!DNL Adobe] vous recommande de consulter ces colonnes pour optimiser vos mises à jour et vous assurer que les colonnes modifiables sont à nouveau vérifiées. Si la fréquence de revérification d’une colonne est élevée compte tenu de la fréquence de modification des données, Adobe recommande de la diminuer pour optimiser vos mises à jour.

Contactez-nous pour toute question ou pour en savoir plus sur les méthodes de réplication ou les revérifications actuelles.

**Connexe :**

* [Réduction Du Temps De Mise À Jour](../../best-practices/reduce-update-cycle-time.md)
* [Optimisation de votre base de données pour l&#39;analyse](../../best-practices/opt-db-analysis.md)
