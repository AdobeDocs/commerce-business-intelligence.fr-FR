---
title: Intégration d’Adobe Commerce Intelligence
description: En savoir plus sur l’intégration d’Adobe Commerce Intelligence.
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# Intégration [!DNL Adobe Commerce Intelligence]

Les questions relatives à l’intégration liées à `store` et `database` assurez-vous que vous configurez correctement vos rapports. Grâce à ces réponses, Adobe diffuse vos rapports qui sont précisément adaptés à la configuration de votre magasin.

## Paramètres de magasin

- *Votre boutique accepte-t-elle le paiement des invités ?* - Sélectionner **oui** si vous autorisez les clients à effectuer un achat sur votre boutique sans vous enregistrer pour un compte.

- `Timezone` - Sélectionnez la variable `timezone` dans lequel vous souhaitez voir vos rapports.

- `Currency` - Sélectionnez la variable `currency` que votre magasin opère.

- `Your week starts on...` - Sélectionnez dans vos rapports le jour de la semaine qui doit être le début de la semaine.

- *Quelle version de Commerce utilisez-vous ?* - Sélectionnez la variable `currency` que votre magasin opère.

- *Votre boutique est-elle basée dans l&#39;Union Européenne ?* - Si vous répondez `Yes` à cette question, Adobe d’héberger votre Data Warehouse et toutes vos données dans l’Union européenne, conformément au RGPD.

## Paramètres de base de données

- `Database name` - Qu’est-ce que la variable *nom du [!DNL MySQL] base* où résident vos données transactionnelles Commerce ?

- `Table prefix (optional)` - Les tables contenues dans votre base de données Commerce sont-elles précédées de tout élément (par exemple : `store_`) ? Normalement, ce n’est pas le cas, mais il s’agit d’une personnalisation qui peut être effectuée.
