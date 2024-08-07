---
title: Suivi UTM en Google Analytics
description: Découvrez les bonnes pratiques relatives au suivi UTM (balisage) en Google Analytics.
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Suivi UTM

Le suivi `UTM` est une convention de balisage pour les URL qui vous permet d’analyser d’où viennent vos utilisateurs. Si vous observez les URL sur lesquelles vous cliquez dans la plupart des bannières publicitaires ou des emails marketing, le balisage UTM s’affiche. Ce sont ces liens longs qui se terminent par des éléments comme `utm\_source` et `utm\_medium`.

[!DNL Google Analytics] utilise le balisage `UTM` pour savoir d’où provient votre trafic. Certaines de ces informations proviennent du [référent HTTP](https://en.wikipedia.org/wiki/HTTP_referer), mais le reste de ces informations nécessite des paramètres `UTM`. Lorsque vous voyez `google adwords` ou `email marketing`, cela signifie que ces `UTM` paramètres sont enregistrés à partir du clic sur le lien d’origine, puis stockés dans les cookies des utilisateurs. À partir de là, [!DNL Google Analytics] utilise ces données pour [attribuer des comportements intéressants](../data-analyst/analysis/google-track-user-acq.md) sur votre site. Comprendre ces paramètres vous aide à comprendre comment configurer et utiliser au mieux le balisage UTM.

## Bonnes pratiques relatives au balisage UTM

Vous trouverez ci-dessous les cinq éléments les plus importants à retenir lors de la configuration de vos URL avec un balisage `UTM`.

### 1. Visez à baliser toutes les URL que vous pouvez contrôler en provenance de votre site.

Chaque fois que vous demandez aux personnes de cliquer sur un lien, vous devez configurer le balisage `UTM`. Cela inclut tous vos liens de courrier électronique (votre fournisseur de service de messagerie peut probablement baliser automatiquement vos URL), liens publicitaires, articles de presse, billets de blog.

### 2. Utilisez un outil pour créer l’URL

Les URL balisées de `UTM` peuvent être fastidieuses. Au lieu d&#39;essayer de les taper longuement, utilisez un outil [comme celui-ci](https://support.google.com/analytics/answer/1033867?hl=en) pour vous aider. Vous avez ainsi la garantie de réfléchir en ajoutant tous les paramètres appropriés à l’URL, et vous obtenez l’URL à copier-coller immédiatement. Pour gérer les liens sociaux, des outils tels que [!DNL Hootsuite] incluent l’option permettant d’ajouter des paramètres d’URL personnalisés à tous vos liens.

### 3. Assurez-vous d’être sensible à la casse dans les valeurs de paramètre.

Il est important de rappeler que la balise `utm\_source=adwords` est une balise différente de `utm\_source=Adwords`. Pensez à tout mettre en minuscules.

### 4. Stockez les valeurs des paramètres UTM dans votre base de données.

Chaque fois qu’une transaction ou un événement se produit, vous souhaitez évaluer les performances de vos activités marketing. Pour ce faire, vous pouvez lire les valeurs des paramètres UTM du cookie [[!DNL Google Analytics] dans votre base de données](../data-analyst/analysis/google-track-user-acq.md).

### 5. Comment nommer des campagnes

Afin de suivre l’amélioration de vos efforts marketing au fil du temps, vous devez être intelligent sur vos conventions d’affectation des noms. Restez simple et minimisez autant que possible. Les systèmes de nommage compliqués sont plus difficiles à gérer.

Une fois que vous capturez ces données dans votre base de données, vous pouvez évaluer les performances de votre marketing et de votre publicité par une analyse plus sophistiquée, y compris [Valeur de durée de vie du client](../data-analyst/analysis/ess-expected-ltv.md), [Taux d’achat répétés](../data-analyst/analysis/repurchase-behavior.md) et [Valeur de commande moyenne](../data-analyst/analysis/basic-analytics.md).
