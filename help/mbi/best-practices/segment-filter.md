---
title: Dimensions de données recommandées pour la segmentation et le filtrage
description: Découvrez les bonnes pratiques en matière de segmentation et de filtrage.
exl-id: 66391bce-bdeb-4e9d-8089-1c796e00d91e
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 0%

---

# Segmentation et filtrage

Une bonne segmentation permet de transformer une statistique superficielle en une mesure commerciale qui oriente les décisions.

Vous voulez savoir qui sont vos clients les plus précieux ? Quels sont vos canaux marketing les plus précieux ? Quels sont vos produits qui se déplacent le plus rapidement et pourquoi ? Pour obtenir l’une de ces réponses, vous devez commencer par segmenter vos données.

Cette rubrique couvre les segments critiques qui sont souvent recommandés aux clients. Il explique également en détail les questions auxquelles ces segments peuvent vous aider à répondre. Techniquement, les segments sont des colonnes de données dans votre base de données. En [!DNL Adobe Commerce Intelligence], on parle de dimensions.

![Tableau de bord présentant les segments et filtres critiques des clients](../../mbi/assets/mbi-critical-segments.png)


## Segments d’utilisateurs

Les segments d’utilisateurs vous aident à comprendre qui sont vos utilisateurs et comment ils se comportent.

* **Âge / Année de naissance** : quel âge ont vos utilisateurs ? Quel âge ont vos utilisateurs les plus actifs ? Il est généralement logique de regrouper les valeurs dans des plages pour une analyse plus efficace.
* **Genre** : des genres différents interagissent-ils différemment avec votre site web ?
* **Adresse** : d’où viennent vos utilisateurs ? Devriez-vous concentrer vos efforts de marketing sur une région en particulier? Vos récentes campagnes publicitaires ont-elles donné les résultats escomptés dans vos régions cibles ?
* **Source d’acquisition du client**\ : connaissez-vous le canal marketing d’où proviennent vos utilisateurs ? Ont-ils cliqué sur une annonce ou vous ont-ils trouvé par le biais d&#39;une recherche ? La [segmentation de vos données par source d’acquisition d’utilisateurs](../data-analyst/analysis/google-track-user-acq.md) est la première étape de l’optimisation de votre nouvelle acquisition de clients. La deuxième étape consiste à dépenser plus d&#39;argent dans ce qui fonctionne et à tuer ce qui ne fonctionne pas.
* **Appareil d&#39;enregistrement** : Les utilisateurs se sont-ils enregistrés via votre application mobile ou votre site web ? iOS ou Android™ ? Votre base d’utilisateurs mobiles est-elle suffisamment large pour allouer davantage de ressources au développement de votre produit mobile ? Si vous ne suivez pas encore cet élément, consultez cette rubrique [à propos du suivi des appareils utilisateur](../data-analyst/analysis/track-usr-dev-browser.md).
* **Référencé par** : Qui sont vos meilleurs influenceurs ? Combien d’utilisateurs ont été directement recommandés par d’autres ?
* **Secteur d’activité** : si vous êtes une entreprise B2B, dans quels secteurs d’activité vos utilisateurs travaillent-ils ? Quelles organisations commerciales méritent d&#39;être rejointes ?
* **Réponses à un questionnaire** : si vous réalisez des questionnaires auprès des clients, utilisez les réponses comme des segments pour approfondir le profilage. Vous pouvez poser des questions qui complètent ce que vous savez déjà sur vos utilisateurs ou confirmer vos hypothèses.
* **Montant de la première commande et catégorie de produits** : existe-t-il une corrélation entre la première commande d’un utilisateur et les tendances d’achat futures ?

## Segments Commandes/Événements

Les segments de commande et d’événement permettent d’analyser le comportement et l’engagement des utilisateurs au fil du temps.

* **[!UICONTROL Billing / Shipping Address]** : D&#39;où viennent la plupart de vos commandes ? Existe-t-il une différence entre les adresses de facturation et d’expédition ?
* **[!UICONTROL Status]** : Combien de vos commandes n&#39;ont pas été exécutées ? Quel est le ratio des commandes en attente au cours des sept derniers jours ?
* **[!UICONTROL Customer acquisition source]** : au-delà du suivi des données d’acquisition des utilisateurs au niveau de l’utilisateur, vous pouvez également [le suivre au niveau de la commande ou de l’événement](../data-analyst/analysis/google-track-user-acq.md). Un utilisateur enregistré via une source peut continuer à accéder à votre site via d’autres sources.
* **[!UICONTROL Device]** : Le nombre de commandes mobiles augmente-t-il ? Quelle part de vos revenus provient d&#39;achats mobiles ? (Si vous n’effectuez pas encore de suivi, consultez cette rubrique [à propos du suivi des données d’appareil de commande](../data-analyst/analysis/track-usr-dev-browser.md).
* **[!UICONTROL Fulfillment Center]** : Lequel de vos centres de traitement des commandes génère le plus de chiffre d&#39;affaires ? Si vous analysez la différence entre le délai de commande et le délai d’expédition, quel centre de traitement des commandes est le plus réactif ?
* **[!UICONTROL Delivery Carrier]** : Quel est le transporteur le plus populaire ? Quel transporteur a le moins d&#39;articles retournés ?
* **[!UICONTROL Discount / Coupon Codes]** : Vos promotions génèrent-elles réellement des affaires supplémentaires ? Combien d&#39;articles supplémentaires vos clients ont-ils achetés en plus de l&#39;article en vente ? Comment les coupons affectent-ils la valeur moyenne de votre commande ? Quelle est votre marge moyenne sur les articles avec ou sans remise ?
* **[!UICONTROL Satisfaction / Rating]** : Dans quelle mesure vos clients sont-ils satisfaits de leurs commandes ? Vos clients sont-ils susceptibles de vous recommander des clients?

## Segments de produit

Les segments de produit vous aident à prendre des décisions de marchandisage.

* **[!UICONTROL Merchant / Brand]** : Une marque spécifique vend-elle plus rapidement que les autres ? Quelles marques sont peu performantes ?
* **[!UICONTROL Type / Category]** : les différents segments d’utilisateurs bénéficient-ils de différents types de produits ? Quelles catégories de produits génèrent le chiffre d’affaires le plus important ?
* **[!UICONTROL Discount / Coupon Codes]** : Les promotions nuisent-elles aux ventes de produits à prix réduit ? Comment les coupons affectent-ils la valeur perçue de vos produits ?
* **[!UICONTROL Social Activity]** : Existe-t-il une corrélation entre le buzz généré sur les médias sociaux et la quantité vendue pour un produit ?
* **[!UICONTROL Size / Variant]** : Quel est le ratio d’inventaire dont vous avez besoin pour chaque variante ? Quelles variantes peuvent être vendues à des taux de remise ?

Si vous êtes intéressé par le marchandisage, consultez [Comment utiliser les segments de produit pour stimuler les activités commerciales récurrentes](../data-analyst/analysis/most-value-source-channel.md).

## Définir des profils client

Les experts en segmentation peuvent vouloir aller au-delà des tranches unidimensionnelles et commencer à établir de vrais profils client. Par exemple, les personnes âgées de 13 à 24 ans qui se sont enregistrées via un appareil mobile ont été incluses dans un groupe « Jeunes et mobiles ». Comment le comportement de ce groupe se compare-t-il au reste de votre base d’utilisateurs ?

Ce type d&#39;analyse est ce que les spécialistes du marketing des entreprises Fortune 1000 font toute la journée. Avant l&#39;avènement des plateformes d&#39;intelligence d&#39;affaires en nuage comme [!DNL Commerce Intelligence], elles étaient largement hors de portée pour le reste d&#39;entre nous. Heureusement, ce n&#39;est plus le cas.

## Suivi de nouveaux segments

La première étape pour segmenter vos mesures en fonction des dimensions ci-dessus est de vous assurer que vous suivez ces données dans votre base de données. Si elles ne sont pas suivies, rencontrez votre équipe technique et trouvez un moyen de commencer à suivre ces données.

Une fois que vous avez confirmé que les données sont suivies dans votre base de données, [contactez l’équipe d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) pour intégrer les dimensions à vos mesures et graphiques [!DNL Commerce Intelligence]. Vous pouvez également utiliser l’outil *Gestion des champs* pour effectuer le suivi de ces champs dans [!DNL Commerce Intelligence].

## Connexe

* [Optimisation de votre base de données pour l’analyse](../best-practices/opt-db-analysis.md)
