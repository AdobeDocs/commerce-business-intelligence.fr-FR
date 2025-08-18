---
title: Nouvelle architecture
description: Découvrez les avantages de la transition vers une nouvelle architecture.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Import/Export
source-git-commit: ddda796c9f32d22b1d679fc245eb11b92cd491cf
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Nouvelle architecture

[!DNL Adobe Commerce Intelligence] équipes Produit et Ingénierie se sont concentrées sur les améliorations les plus importantes et les plus demandées possibles au cours de l’année écoulée. Adobe est ravi d’annoncer la disponibilité d’une nouvelle architecture de produit [!DNL Commerce Intelligence] qui concrétise ces améliorations.

## Avantages de la nouvelle architecture

* Création de types de colonnes dans le Data Warehouse, y compris les colonnes calculées avec SQL.
* De nouvelles colonnes sont immédiatement disponibles.
* La latence des données a été considérablement améliorée.

## Avantages techniques

Les principales différences sont répertoriées ci-dessus, mais la principale modification concerne la manière dont les calculs sont effectués pendant le cycle de mise à jour. Les calculs ne sont plus exécutés sur chaque colonne à chaque mise à jour ; ils sont exécutés à la demande depuis Visual Report Builder.

### Passage à une nouvelle architecture

Comme les comptes sont créés fondamentalement différemment, il n’existe aucun processus automatique pour migrer vos Data Warehouse ou rapports vers un compte doté d’une nouvelle architecture. Le passage à la nouvelle architecture nécessite une nouvelle implémentation de votre compte existant.

### Coût de la migration vers la nouvelle architecture

Aucun coût supplémentaire ! Adobe créera ce compte pour que vous puissiez commencer la nouvelle implémentation, qui est gratuite pendant au moins un mois. Vous aurez ainsi le temps d’ouvrir les deux comptes afin de pouvoir effectuer plus facilement la nouvelle implémentation et de vous assurer que votre équipe ne présente pas d’interruption de service.

### Temps nécessaire à la réimplémentation du compte dans la nouvelle architecture

Les délais de réimplémentation varient en fonction de ce que vous souhaitez recréer. Adobe vous recommande d’effectuer les étapes suivantes dans votre compte existant pour avoir une idée de ce qui serait impliqué dans votre nouvelle implémentation :

* Identifiez un ensemble de base de rapports/tableaux de bord.
* Identifiez les mesures et les dimensions requises pour créer ces rapports.
* Identifiez les colonnes requises pour recréer ces mesures et dimensions.

Une fois cette opération terminée, vous savez quelles données vous devez synchroniser avec la nouvelle architecture Data Warehouse afin de recréer ces rapports de base.

### Accès à l’aide

L’équipe [!DNL Adobe Commerce Intelligence] [Services](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) peut effectuer votre nouvelle implémentation moyennant un coût supplémentaire. Contactez l’équipe chargée de votre compte [Adobe](../../guide-overview.md#Submitting-a-Support-Ticket) et préparez-vous à fournir une liste des tableaux de bord/rapports que vous souhaitez créer en priorité dans le nouveau compte

### Conservation de l’architecture existante

Si ces fonctionnalités ne sont pas importantes pour vous, vous pouvez vous en tenir à votre compte existant. La conservation de votre compte existant n’entraîne aucun frais supplémentaire. Adobe continue à prendre en charge ces comptes sans modification.
