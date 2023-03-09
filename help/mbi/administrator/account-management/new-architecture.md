---
title: Nouvelle architecture
description: Découvrez les avantages liés au passage à une nouvelle architecture.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Nouvelle architecture

Les équipes produit et ingénierie de l&#39;IMS se sont concentrées sur les améliorations les plus radicales et les plus demandées possibles au cours de l&#39;année écoulée. Adobe est ravi d&#39;annoncer la disponibilité d&#39;un nouveau [!DNL MBI] architecture de produit qui rend ces améliorations réelles.

## Avantages de la nouvelle architecture

* Créez des types de colonnes dans le Data Warehouse, y compris des colonnes calculées avec SQL.
* De nouvelles colonnes sont disponibles immédiatement.
* La latence des données a été considérablement améliorée.

## Avantages techniques

Les principales différences sont répertoriées ci-dessus, mais la principale modification est la façon dont les calculs sont effectués pendant le cycle de mise à jour. Les calculs ne sont plus exécutés sur chaque colonne à chaque mise à jour ; à la place, elles sont exécutées à la demande à partir du Report Builder visuel.

### Passage à la nouvelle architecture

Comme les comptes sont créés de manière fondamentalement différente, il n’existe aucun processus automatique pour migrer votre Data Warehouse ou vos rapports vers un nouveau compte d’architecture. Le passage à la nouvelle architecture nécessite une réimplémentation de votre compte existant.

### Coût de la transition vers la nouvelle architecture

Aucun coût supplémentaire ! Adobe crée ce nouveau compte pour que vous puissiez commencer la mise en oeuvre, qui est gratuite pendant au moins un mois. Cela vous permet de disposer du temps nécessaire pour que les deux comptes soient ouverts afin que vous puissiez plus facilement effectuer la remise en oeuvre et que votre équipe ne dispose pas d’une interruption de service.

### Temps nécessaire pour réimplémenter le compte dans la nouvelle architecture

Les délais de mise en oeuvre varient en fonction de ce que vous souhaitez recréer. Adobe vous recommande d’effectuer les étapes suivantes dans votre compte existant afin d’obtenir une idée de ce qui serait impliqué dans votre remise en oeuvre :

* Identifiez un ensemble principal de rapports/tableaux de bord.
* Identifiez les mesures et dimensions requises pour créer ces rapports.
* Identifiez les colonnes requises pour recréer ces mesures et dimensions.

Une fois cette opération terminée, vous savez quelles données vous devez synchroniser avec le nouveau Data Warehouse d’architecture afin de reconstruire ces rapports principaux.

### Obtention d’aide

Le [!DNL MBI] L’équipe des services peut effectuer votre remise en oeuvre moyennant des frais supplémentaires. Contactez votre [Équipe du compte Adobe](../../guide-overview.md) et être prêt à fournir une liste de tableaux de bord/rapports que vous souhaitez créer en priorité dans le nouveau compte.

### Rester avec l’architecture existante

Si ces fonctionnalités ne sont pas importantes pour vous, vous pouvez vous en tenir à votre compte existant. La conservation de votre compte existant n’entraîne aucuns frais supplémentaires. Adobe continue à prendre en charge ces comptes sans modification.
