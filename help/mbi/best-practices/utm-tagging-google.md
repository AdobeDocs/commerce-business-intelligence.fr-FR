---
title: Suivi UTM dans Google Analytics
description: Découvrez les bonnes pratiques relatives au suivi UTM (balisage) dans Google Analytics.
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Suivi UTM

Le tracking `UTM` est une convention de balisage des URL qui vous permet d’analyser la provenance de vos utilisateurs et utilisatrices. Si vous regardez sur les URL sur lesquelles vous cliquez dans la plupart des e-mails marketing ou des bannières publicitaires, vous verrez le balisage UTM. Ce sont ces longs liens qui se terminent par des choses comme `utm\_source` et `utm\_medium`.

[!DNL Google Analytics] utilise le balisage `UTM` pour savoir d’où vient votre trafic. Certaines de ces informations proviennent du [ référent HTTP ](https://en.wikipedia.org/wiki/HTTP_referer), mais le reste vous devez vous fournir des paramètres de `UTM`. Lorsque vous voyez `google adwords` ou `email marketing`, cela signifie que ces paramètres de `UTM` sont enregistrés à partir du clic sur le lien d’origine, puis stockés dans les cookies des utilisateurs. Ensuite, [!DNL Google Analytics] utilise ces données pour [attribuer des comportements intéressants](../data-analyst/analysis/google-track-user-acq.md) sur votre site. Comprendre à quoi servent ces paramètres vous aide à comprendre la meilleure façon de configurer et d’utiliser le balisage UTM.

## Bonnes pratiques relatives au balisage UTM

Vous trouverez ci-dessous la liste des cinq éléments les plus importants à retenir lors de la configuration de vos URL avec le balisage `UTM`.

### &#x200B;1. Visez à baliser chaque URL que vous pouvez contrôler en accédant à votre site

Chaque fois que vous demandez à des personnes de cliquer sur un lien, vous devez configurer le balisage `UTM`. Cela inclut tous vos liens d’e-mail (votre fournisseur de services de messagerie dispose probablement d’un moyen de baliser automatiquement vos URL), ainsi que les liens, articles de presse et articles de blog.

### &#x200B;2. Utiliser un outil pour créer l’URL

Les URL avec balisage `UTM` peuvent être fastidieuses. Au lieu d’essayer de les taper à la main, utilisez un outil [comme celui-ci](https://support.google.com/analytics/answer/1033867?hl=en) pour vous aider. Cela vous permet de réfléchir à l’ajout de tous les paramètres sensibles à l’URL et d’obtenir l’URL à copier-coller directement à partir de celle-ci. Pour gérer les liens de réseaux sociaux, des outils tels que [!DNL Hootsuite] incluent la possibilité d’ajouter des paramètres d’URL personnalisés à tous vos liens.

### &#x200B;3. Veillez à respecter la casse dans les valeurs de paramètre

Il est important de se rappeler que la balise `utm\_source=adwords` est une balise différente de `utm\_source=Adwords`. Pensez à tout mettre en minuscules.

### &#x200B;4. Stockez les valeurs de paramètre UTM dans votre base de données

Chaque fois qu’une transaction ou un événement se produit, vous devez évaluer les performances de vos activités marketing. Pour ce faire, lisez les valeurs des valeurs des paramètres UTM du [[!DNL Google Analytics]  cookie dans votre base de données](../data-analyst/analysis/google-track-user-acq.md).

### &#x200B;5. Pensez à la manière dont vous nommez les campagnes

Pour suivre l’amélioration de vos efforts marketing au fil du temps, vous devez connaître intelligemment vos conventions de nommage. Restez simple et minimisez autant que possible. Les systèmes de nommage complexes sont plus difficiles à gérer.

Une fois que vous avez capturé ces données dans votre base de données, vous pouvez évaluer les performances de vos campagnes marketing et publicitaires à l’aide d’une analyse plus sophistiquée, notamment [Valeur durée de vie du client](../data-analyst/analysis/ess-expected-ltv.md), [Taux d’achat répétés](../data-analyst/analysis/repurchase-behavior.md) et [Valeur moyenne de la commande](../data-analyst/analysis/basic-analytics.md).
