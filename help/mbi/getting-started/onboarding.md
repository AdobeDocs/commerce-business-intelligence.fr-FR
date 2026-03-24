---
title: Adobe Commerce Intelligence d’intégration
description: En savoir plus sur l’intégration de Adobe Commerce Intelligence.
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
TQID: https://experienceleague.adobe.com/36wmj-7QyDdemBWFwHTf1NJkd4H06tED9FZPqhFz8eg
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: b5f00040-57a0-4a6d-a39e-383b1936c2c9id: f42e0a1a-0d79-488d-a83f-f2c30672b137
subfeature_v2: id: bcbf87e7-9b75-4596-bffe-0f376b4c73a7
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 194
ht-degree: 0%

---

# [!DNL Adobe Commerce Intelligence] d’intégration

Les questions d’intégration relatives aux paramètres de `store` et de `database` vous permettent de configurer correctement les rapports. Grâce à ces réponses, Adobe diffuse vos rapports qui sont précisément adaptés à la configuration de votre boutique.

## Paramètres de la boutique

- *Votre boutique accepte-t-elle le passage en caisse des invités ?* - Sélectionnez **oui** si vous autorisez les clients à effectuer un achat dans votre boutique sans s’inscrire à un compte.

- `Timezone` - Sélectionnez les `timezone` dans lesquelles vous souhaitez afficher vos rapports.

- `Currency` - Sélectionnez le `currency` dans lequel votre boutique opère.

- `Your week starts on...` - Sélectionnez le jour de la semaine qui doit être le début de la semaine dans vos rapports.

- *Quelle version de Commerce utilisez-vous ?* - Sélectionnez le `currency` dans lequel votre boutique opère.

- *Votre magasin est-il basé dans l&#39;Union européenne ?* - Si vous répondez `Yes` cette question, Adobe hébergera votre Data Warehouse et toutes vos données dans l’Union européenne, conformément au RGPD.

## Paramètres de la base de données

- `Database name` - Quel est le *nom de la base de données [!DNL MySQL]* où se trouvent vos données transactionnelles Commerce ?

- `Table prefix (optional)` - Les tables contenues dans votre base de données Commerce sont-elles précédées d’un préfixe (par exemple, `store_`) ? Ce n’est normalement pas le cas, mais il s’agit d’une personnalisation qui peut être effectuée.
