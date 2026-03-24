---
title: Comprendre les résultats entre la base de données et l'éditeur SQL
description: Découvrez comment comprendre les résultats entre la base de données et l’éditeur SQL.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/pScH-yKW8hbSNZzsJ537CN7rxhcuygaLmCu3fdVaYgk
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 257
ht-degree: 0%

---

# Résultats de la base de données par rapport aux résultats [!DNL SQL Editor]

Vous êtes peut-être curieux de savoir quel est le champ `Last successful update began` dans votre page `Integrations` :

![Last_successful_update.png](../../../assets/Last_successful_update.png)

## Comprendre le champ `timestamp`

Elle affiche la `timestamp` de début (dans le fuseau horaire défini sur votre compte) du _dernier cycle de mise à jour réussi_ sur votre compte.

- Si l&#39;une des tables synchronisées rencontre un problème lors du dernier cycle de mise à jour, cet horodatage n&#39;est *pas mis à jour*.
- Par conséquent, il peut y avoir des cas où les rapports ont été mis à jour avec des données récentes, mais où la *Dernière mise à jour réussie a commencé* est toujours en retard.

## Identifier le dernier point de données « réel »

Le dernier point de données d’une intégration spécifique est déterminé par l’horodatage `Last Data Point Received` situé à droite de chaque intégration. Cet horodatage fait référence au dernier point auquel votre Data Warehouse a reçu avec succès des points de données de cette source, qu’il s’agisse d’une base de données, d’une API ou d’une intégration tierce.

Pour vérifier l’actualisation des données de *tableaux spécifiques*, Adobe recommande de créer un rapport [[!DNL SQL]  rapide](../../dev-reports/sql-rpt-bldr.md) qui effectue une `MAX(timestamp)` sur le tableau le plus important de votre compte. La comparaison de cet horodatage avec le `Last Data Point` indique si le problème a affecté l’ensemble du compte ou un sous-ensemble des tables. Adobe recommande de le faire pour trois à quatre tableaux importants couramment utilisés.

- Si les valeurs `MAX(timestamp)` sont plus récentes que `Last Data Point Received`, cela signifie qu’un sous-ensemble des tables a été affecté, mais que le cycle de mise à jour du compte global est stable.
- Si les valeurs `MAX(timestamp)` sont égales ou antérieures à `Last Data Point Received`, cela signifie que le cycle de mise à jour du compte a été affecté. Dans ce cas, [soumettez un ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
