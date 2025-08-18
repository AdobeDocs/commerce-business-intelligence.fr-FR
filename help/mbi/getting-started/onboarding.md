---
title: Adobe Commerce Intelligence d’intégration
description: En savoir plus sur l’intégration de Adobe Commerce Intelligence.
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '194'
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
