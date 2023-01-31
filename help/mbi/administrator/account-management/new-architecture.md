---
title: Nouvelle architecture
description: Découvrez les avantages liés au passage à une nouvelle architecture.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Nouvelle architecture

Nos équipes produit et ingénierie se sont concentrées sur les améliorations les plus radicales et les plus demandées possibles au cours de l’année écoulée. Nous sommes ravis d’annoncer la disponibilité d’un nouveau [!DNL MBI] architecture de produit qui rend ces améliorations réelles.

## Avantages de la nouvelle architecture

* Créez de nouveaux types de colonnes dans l’entrepôt de données, y compris des colonnes calculées avec SQL.
* De nouvelles colonnes sont disponibles immédiatement.
* La latence des données a été considérablement améliorée.

## Avantages techniques

Les principales différences sont répertoriées ci-dessus, mais ce qui a techniquement changé est la façon dont nous effectuons les calculs pendant le cycle de mise à jour. Les calculs ne sont plus exécutés sur chaque colonne à chaque mise à jour ; à la place, elles sont exécutées à la demande à partir du Report Builder visuel.

### Passage à la nouvelle architecture

Comme les comptes sont fondamentalement créés différemment, il n’existe aucun processus automatique que nous pouvons utiliser pour migrer votre entrepôt de données ou vos rapports vers un nouveau compte d’architecture. Le passage à la nouvelle architecture nécessite donc une nouvelle mise en oeuvre de votre compte existant.

### Coût de la transition vers la nouvelle architecture

Aucun coût supplémentaire ! Nous allons créer un nouveau compte pour que vous puissiez commencer la mise en oeuvre à nouveau, ce qui est gratuit pendant au moins un mois. Cela vous permet de disposer du temps nécessaire pour que les deux comptes soient ouverts afin que vous puissiez plus facilement effectuer la remise en oeuvre et que votre équipe ne dispose pas d’une interruption de service.

### Temps nécessaire pour réimplémenter le compte dans la nouvelle architecture

Les délais de mise en oeuvre varient en fonction de ce que vous souhaitez recréer. Nous vous recommandons d’effectuer les étapes suivantes dans votre compte existant pour obtenir une idée de ce qui serait impliqué dans votre mise en oeuvre à nouveau :

* Identifiez un ensemble principal de rapports/tableaux de bord.
* Identifiez les mesures et dimensions requises pour créer ces rapports.
* Identifiez les colonnes requises pour recréer ces mesures et dimensions.

Une fois cette opération terminée, vous saurez quelles données vous devez synchroniser avec le nouvel entrepôt de données de la nouvelle architecture afin de reconstruire ces rapports principaux.

### Obtention d’aide

Le [!DNL MBI] L’équipe des services peut effectuer votre réimplémentation pour un coût supplémentaire. Contactez notre [Équipe de succès client](../../guide-overview.md) et être prêt à fournir une liste de tableaux de bord/rapports que vous souhaitez créer en priorité dans le nouveau compte.

### Rester avec l’architecture existante

Si ces fonctionnalités ne sont pas importantes pour vous, vous pouvez vous en tenir à votre compte existant. La conservation de votre compte existant n’entraîne aucun coût supplémentaire, et nous continuerons à prendre en charge ces comptes sans modification.
