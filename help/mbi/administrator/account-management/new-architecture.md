---
title: Nouvelle architecture
description: Découvrez les avantages liés au passage à une nouvelle architecture.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Import/Export
source-git-commit: ddda796c9f32d22b1d679fc245eb11b92cd491cf
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Nouvelle architecture

[!DNL Adobe Commerce Intelligence] Les équipes produit et ingénierie se sont concentrées sur les améliorations les plus radicales et les plus demandées possibles au cours de l’année écoulée. Adobe est ravi d’annoncer la disponibilité d’une nouvelle architecture de produit [!DNL Commerce Intelligence] qui rend ces améliorations concrètes.

## Avantages de la nouvelle architecture

* Créez des types de colonnes dans le Data Warehouse, y compris des colonnes calculées avec SQL.
* De nouvelles colonnes sont disponibles immédiatement.
* La latence des données a été considérablement améliorée.

## Avantages techniques

Les principales différences sont répertoriées ci-dessus, mais la principale modification est la façon dont les calculs sont effectués pendant le cycle de mise à jour. Les calculs ne sont plus exécutés sur chaque colonne à chaque mise à jour ; ils le sont plutôt sur demande à partir du Report Builder visuel.

### Passage à la nouvelle architecture

Comme les comptes sont créés de manière fondamentalement différente, il n’existe aucun processus automatique pour migrer votre Data Warehouse ou vos rapports vers un nouveau compte d’architecture. Le passage à la nouvelle architecture nécessite une nouvelle mise en oeuvre de votre compte existant.

### Coût de la transition vers la nouvelle architecture

Aucun coût supplémentaire ! Adobe va créer ce nouveau compte pour que vous puissiez recommencer la mise en oeuvre, ce qui est gratuit pendant au moins un mois. Cela vous permet de disposer du temps nécessaire pour que les deux comptes soient ouverts afin que vous puissiez plus facilement effectuer la remise en oeuvre et que votre équipe ne dispose pas d’une interruption de service.

### Temps nécessaire pour réimplémenter le compte dans la nouvelle architecture

Les délais de mise en oeuvre varient en fonction de ce que vous souhaitez recréer. Adobe vous recommande d’effectuer les étapes suivantes dans votre compte existant afin d’obtenir une idée de ce qui serait impliqué dans votre mise en oeuvre à nouveau :

* Identifiez un ensemble principal de rapports/tableaux de bord.
* Identifiez les mesures et dimensions requises pour créer ces rapports.
* Identifiez les colonnes requises pour recréer ces mesures et dimensions.

Une fois cette opération terminée, vous savez quelles données vous devez synchroniser avec le nouveau Data Warehouse d’architecture afin de reconstruire ces rapports principaux.

### Obtention d’aide

L’ [!DNL Adobe Commerce Intelligence] [équipe des services](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) peut effectuer votre remise en oeuvre pour un coût supplémentaire. Contactez votre [ équipe de compte d’Adobe ](../../guide-overview.md#Submitting-a-Support-Ticket) et soyez prêt à fournir une liste de tableaux de bord/rapports que vous souhaitez créer en priorité dans le nouveau compte.

### Rester avec l’architecture existante

Si ces fonctionnalités ne sont pas importantes pour vous, vous pouvez vous en tenir à votre compte existant. La conservation de votre compte existant n’entraîne aucuns frais supplémentaires. Adobe continue à prendre en charge ces comptes sans modification.
