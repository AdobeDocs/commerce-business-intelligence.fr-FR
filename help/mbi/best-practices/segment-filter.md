---
title: Dimensions de données recommandées pour la segmentation et le filtrage
description: Découvrez les bonnes pratiques de segmentation et de filtrage.
exl-id: 66391bce-bdeb-4e9d-8089-1c796e00d91e
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# Segmentation et filtrage

Une bonne segmentation est ce qui transforme une statistique superficielle en une mesure commerciale qui détermine les décisions.

Vous voulez savoir qui sont vos clients les plus précieux ? Quels sont vos canaux marketing les plus précieux ? Lequel de vos produits se déplace plus vite et pourquoi ? Pour obtenir l’une de ces réponses, vous devez commencer par segmenter vos données.

Dans cet article, nous partageons certains segments critiques que nous recommandons souvent à nos clients. Nous allons également examiner en détail les questions auxquelles ces segments peuvent vous aider à répondre. Techniquement, les segments sont des colonnes de données dans votre base de données. Dans [!DNL MBI], nous les appelons dimensions.

![](../../mbi/assets/mbi-critical-segments.png)


## Segments d’utilisateur

Les segments d’utilisateurs vous aident à comprendre qui sont vos utilisateurs et comment ils se comportent.

* **Age / Année de naissance**: Quel âge ont vos utilisateurs ? Quel âge ont vos utilisateurs les plus principaux ? Il est généralement logique de regrouper les valeurs dans des plages pour une analyse plus efficace.
* **Genre**: Les hommes et les femmes interagissent-ils différemment avec votre site web ?
* **Adresse**: D’où viennent vos utilisateurs ? Devriez-vous concentrer vos efforts marketing sur une région spécifique ? Vos campagnes publicitaires récentes ont-elles été exécutées comme prévu dans vos régions cibles ?
* **Source d’acquisition client**\: Savez-vous de quel canal marketing viennent vos utilisateurs ? Ont-ils cliqué sur une publicité ou vous ont-ils trouvée par recherche ? [Segmenter vos données par source d’acquisition d’utilisateurs](../data-analyst/analysis/google-track-user-acq.md) est la première étape de l’optimisation de votre nouvelle acquisition de clients. La deuxième étape consiste à dépenser plus d&#39;argent dans ce qui fonctionne et à tuer ce qui ne fonctionne pas.
* **Appareil d’enregistrement**: Les utilisateurs se sont-ils inscrits via votre application mobile ou votre site web ? iOS ou Android ? Votre base d’utilisateurs mobiles est-elle assez grande pour allouer plus de ressources pour développer votre produit mobile ? (Si vous n’effectuez pas encore le suivi, consultez cette rubrique [à propos du suivi des appareils utilisateur](../data-analyst/analysis/track-usr-dev-browser.md).
* **Référencé par**: Qui sont vos principaux influenceurs ? Combien d’utilisateurs ont été directement référencés par d’autres utilisateurs ?
* **Secteur industriel**: Si vous êtes une entreprise B2B, dans laquelle vos utilisateurs travaillent-ils ? Quelles organisations commerciales valent la peine d&#39;être rejointes ?
* **Réponses à un questionnaire**: Si vous effectuez des enquêtes sur les clients, utilisez les réponses comme segments pour un niveau de profilage plus profond. Vous pouvez poser des questions qui complètent ce que vous savez déjà sur vos utilisateurs ou confirmer vos estimations.
* **Montant de la première commande et catégorie de produits**: Existe-t-il une corrélation entre la première commande d’un utilisateur et les futurs modèles d’achat ?

## Segments Commandes / Événements

Les segments de commande et d’événement permettent d’analyser le comportement et l’engagement des utilisateurs au fil du temps.

* **[!UICONTROL Billing / Shipping Address]**: D&#39;où viennent la plupart de vos commandes ? Y a-t-il une différence entre les adresses de facturation et de livraison ?
* **[!UICONTROL Status]**: Combien de vos commandes ont échoué ? Quel est le rapport entre les commandes en attente au cours des sept derniers jours ?
* **[!UICONTROL Customer acquisition source]**: Outre le suivi des données d’acquisition d’utilisateurs au niveau de l’utilisateur, vous pouvez également [le suivre au niveau d’une commande ou d’un événement ;](../data-analyst/analysis/google-track-user-acq.md). Un utilisateur enregistré via une source peut très bien continuer à accéder à votre site par le biais d’autres sources.
* **[!UICONTROL Device]**: Le nombre de commandes mobiles augmente-t-il ? Quel est actuellement le montant de vos recettes généré par les achats mobiles ? (Si vous n’effectuez pas encore le suivi, consultez cette rubrique [à propos du suivi des données de périphérique de l’ordre](../data-analyst/analysis/track-usr-dev-browser.md).
* **[!UICONTROL Fulfillment Center]**: Quel de vos centres d’exécution génère le plus de recettes ? Si vous analysez la différence entre le délai de commande et le délai d’expédition, quel centre d’exécution est le plus réactif ?
* **[!UICONTROL Delivery Carrier]**: Quel est le transporteur le plus populaire ? Quel opérateur a le moins d’articles renvoyés ?
* **[!UICONTROL Discount / Coupon Codes]**: Vos promotions génèrent-elles réellement des activités supplémentaires ? Combien d’articles supplémentaires vos clients ont-ils achetés en plus de l’article en vente ? Comment les bons affectent-ils la valeur moyenne de la commande ? Quelle est votre marge moyenne sur les articles à prix réduit par rapport aux articles à prix réduit ?
* **[!UICONTROL Satisfaction / Rating]**: Quel est le degré de satisfaction de vos clients quant à leurs commandes ? Vos clients sont-ils susceptibles de vous faire part de leurs activités ?

## Segments de produit

Les segments de produit vous aident à prendre des décisions de marchandisage.

* **[!UICONTROL Merchant / Brand]**: Une marque spécifique vend-elle plus rapidement que le reste ? Quelles marques sont peu performantes ?
* **[!UICONTROL Type / Category]**: Les différents segments d’utilisateurs bénéficient-ils de différents types de produits ? Quelles sont les catégories de produits qui génèrent le plus de répétitions ?
* **[!UICONTROL Discount / Coupon Codes]**: Les promotions nuisent-elles aux ventes de produits non réduits ? Comment les bons affectent-ils la valeur perçue de vos produits ?
* **[!UICONTROL Social Activity]**: Existe-t-il une corrélation entre le buzz généré sur les médias sociaux et la quantité vendue pour un produit ?
* **[!UICONTROL Size / Variant]**: Quel est le ratio de stock dont vous avez besoin pour chaque variante ? Quelles variantes peuvent être vendues à des taux d&#39;escompte ?

Si vous êtes intéressé par le marchandisage, consultez un billet de blog où nous explorons [utilisation des segments de produit pour générer des activités répétées](../data-analyst/analysis/most-value-source-channel.md).

## Définition des profils client

Les experts en segmentation peuvent souhaiter dépasser les tranches unidimensionnelles et commencer à créer des profils clients réels. Par exemple, les personnes âgées de 13 à 24 ans qui se sont enregistrées via un appareil mobile placé dans un groupe &quot;Jeunes et mobiles&quot;. Comment le comportement de ce groupe se compare-t-il au reste de votre base d’utilisateurs ?

Ce type d’analyse est ce que les marketeurs des sociétés Fortune 1000 font toute la journée. Avant l’avènement de plateformes de Business Intelligence basées sur le cloud, telles que [!DNL MBI], c&#39;était largement hors de portée pour le reste d&#39;entre nous. Heureusement, ce n&#39;est plus le cas.

## Suivi des nouveaux segments

La première étape pour segmenter vos mesures selon les dimensions ci-dessus consiste à vous assurer que vous effectuez le suivi de ces données dans votre base de données. S’il n’est pas suivi, rencontrez votre équipe technique et trouvez un moyen de commencer à suivre ces données.

Une fois que nous avons confirmé que les données sont suivies dans votre base de données, [contactez notre équipe d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) pour pousser les dimensions vers vos [!DNL MBI] mesures et graphiques ou utilisez simplement notre outil de gestion des champs pour effectuer le suivi de ces champs dans [!DNL MBI].

## Associé

* [Optimisation de la base de données pour l’analyse](../best-practices/opt-db-analysis.md)
