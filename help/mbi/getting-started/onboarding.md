---
title: Intégration à Adobe Commerce Intelligence
description: En savoir plus sur l’intégration à Adobe Commerce Intelligence.
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# Intégration [!DNL Adobe Commerce Intelligence]

Les questions d&#39;intégration liées aux paramètres `store` et `database` vous permettent de configurer correctement vos rapports. Grâce à ces réponses, Adobe diffuse vos rapports qui sont précisément adaptés à la configuration de votre magasin.

## Paramètres de magasin

- *Votre boutique accepte-t-elle le passage en caisse des invités ?* - Sélectionnez **oui** si vous autorisez les clients à effectuer un achat sur votre boutique sans s’inscrire pour un compte.

- `Timezone` - Sélectionnez le `timezone` dans lequel vous souhaitez afficher vos rapports.

- `Currency` - Sélectionnez le `currency` dans lequel votre magasin fonctionne.

- `Your week starts on...` - Sélectionnez le jour de la semaine qui doit être le début de la semaine dans vos rapports.

- *Quelle version de Commerce utilisez-vous ?* - Sélectionnez le `currency` dans lequel votre magasin fonctionne.

- *Votre boutique est-elle basée dans l’Union européenne ?* - Si vous répondez `Yes` à cette question, Adobe héberge votre Data Warehouse et toutes vos données dans l’Union européenne, conformément au RGPD.

## Paramètres de base de données

- `Database name` - Quel est le *nom de la base de données [!DNL MySQL]* où se trouvent vos données transactionnelles Commerce ?

- `Table prefix (optional)` - Les tables contenues dans votre base de données Commerce sont-elles précédées de quelque chose (par exemple, `store_`) ? Normalement, ce n’est pas le cas, mais il s’agit d’une personnalisation qui peut être effectuée.
