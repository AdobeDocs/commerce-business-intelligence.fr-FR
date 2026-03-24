---
title: Nouvelle architecture
description: Découvrez les avantages de la transition vers une nouvelle architecture.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Import/Export
TQID: https://experienceleague.adobe.com/EtbKFT7OKaTZQ55XNz0NwpxQNSXyazk47dGwKhETNjM
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 390
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

L’équipe [!DNL Adobe Commerce Intelligence] [Services](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) peut effectuer votre nouvelle implémentation moyennant un coût supplémentaire. Contactez l’équipe chargée de votre compte [&#128279;](../../guide-overview.md#Submitting-a-Support-Ticket) et préparez-vous à fournir une liste des tableaux de bord/rapports que vous souhaitez créer en priorité dans le nouveau compte

### Conservation de l’architecture existante

Si ces fonctionnalités ne sont pas importantes pour vous, vous pouvez vous en tenir à votre compte existant. La conservation de votre compte existant n’entraîne aucun frais supplémentaire. Adobe continue à prendre en charge ces comptes sans modification.
