---
title: Augmentation du retour sur investissement de vos campagnes publicitaires
description: Découvrez quelques méthodes différentes pour évaluer les performances de votre campagne.
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
role: Admin, User
feature: Data Warehouse Manager, Reports, Campaigns
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1253'
ht-degree: 0%

---

# Campagnes Advertising et retour sur investissement

[!DNL Adobe Commerce Intelligence] vous permet de [associer facilement les données sur les coûts publicitaires et les données sur les recettes](../../data-analyst/importing-data/integrations/google-adwords.md) à partir de votre base de données. Vous pouvez ainsi identifier les campagnes qui présentent le retour sur investissement (ROI) le plus élevé. Cette rubrique explore quelques méthodes différentes pour évaluer les performances de votre campagne.

## Conditions préalables

* Importez vos données de coûts publicitaires :
   * [Connecter votre [!DNL Google AdWords] à [!DNL Commerce Intelligence]](../importing-data/integrations/google-adwords.md) : synchronise vos dépenses [!DNL Adwords] dans [!DNL Commerce Intelligence]
   * [Charger d’autres données de coût publicitaire](../importing-data/connecting-data/import-offline-ad-data.md) : cela est recommandé pour les canaux sans connecteur direct vers [!DNL Commerce Intelligence]
   * Si vous importez des données de coût provenant de plusieurs sources, vous pouvez [consolider](../../best-practices/consolidating-your-tables.md) les données dans [!DNL Commerce Intelligence]. Il vous suffit [soumettre un ticket d’assistance](../../guide-overview.md#Submitting-a-Support-Ticket).
* [Suivre les données du canal d’acquisition des utilisateurs](../analysis/google-track-user-acq.md)

## Campagnes d’acquisition d’utilisateurs

Les campagnes ciblées sur l’acquisition d’utilisateurs peuvent être mesurées sous de nombreux angles, notamment :

1. Nombre de nouveaux utilisateurs acquis dans les campagnes
1. Taux de conversion de l’enregistrement à l’achat de campagnes
1. Retour sur investissement des campagnes en fonction de la valeur moyenne de la durée de vie de l’utilisateur

Les analyses (1) et (2) ci-dessus sont explorées dans un tutoriel distinct sur l’[identification de vos principaux canaux marketing](../analysis/most-value-source-channel.md). Vous explorez ici l’analyse (3) pour mesurer le retour sur investissement de la campagne au fil du temps. Cela permet de déterminer si les utilisateurs acquis à partir d’une campagne particulière ont généré un chiffre d’affaires suffisant pour couvrir le coût d’acquisition.

>[!NOTE]
>
>Cet exemple suppose que tous les coûts de campagne ont été utilisés exclusivement pour acquérir de nouveaux utilisateurs. En réalité, le coût de votre campagne est également partagé avec l’acquisition de visites non converties, les acheteurs répétés, etc. En supposant que tous les coûts soient utilisés pour acquérir de nouveaux utilisateurs enregistrés, le retour sur investissement qui en résulte prend en compte le scénario le plus pessimiste (coût le plus élevé par acquisition). Vous pouvez être sûr que votre retour sur investissement réel est supérieur à votre calcul.
>
>Exemple : en supposant que vous ayez dépensé 20 $ dans une campagne qui a généré 10 nouveaux utilisateurs et 10 acheteurs réguliers, votre coût réel par nouvel utilisateur est de 1 $. Mais, en supposant que tous les coûts aient servi à acquérir de nouveaux utilisateurs, le coût par acquisition est de 2 $.

**1. Commencez par créer un graphique qui segmente votre coût publicitaire par campagnes :**

1. Créer une [!UICONTROL Metric] qui additionne vos dépenses au fil du temps
1. Accéder à la [!UICONTROL Data > Metrics]
1. Sélectionnez `Add New Metric` et sélectionnez la table de [!DNL `Adwords...`] qui enregistre vos données de coûts [!DNL AdWords].
1. Dans l’éditeur de mesures, attribuez un nom à votre mesure (par exemple, [!UICONTROL AdWord Cost])
1. À l’aide des listes déroulantes, effectuez une **Somme** sur la colonne `adCost` du tableau [!DNL Adwords...] (Modification) triée par colonne `date`.
   ![Message de réussite après l’ajout d’une nouvelle mesure](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. Cliquez sur `Back to Metric List` dans la partie supérieure et accédez à n’importe quel tableau de bord.

1. Créer un rapport qui segmente les dépenses par campagne
1. Dans un tableau de bord, cliquez sur [!UICONTROL Add Report > Create report]
1. Sélectionnez la mesure [!UICONTROL Adword Cost] que vous venez de créer
1. Définissez la [!UICONTROL Time period] sur `All-time` et la [!UICONTROL Interval] sur `None`
1. Sous l’onglet `Group by` , ajoutez des `campaign` en tant que [!UICONTROL grouping field], puis cliquez sur `Add All` dans la zone.
1. Ce rapport affiche le coût [!DNL AdWords] permanent par campagne

**2. Créez un rapport qui comptabilise les nouveaux utilisateurs par campagne :**

1. Dans un tableau de bord, cliquez sur **[!UICONTROL Add Report > Create report]**
1. Sélectionnez la mesure de `New users` qui comptabilise le nombre de nouveaux utilisateurs enregistrés au fil du temps
1. Définissez la [!UICONTROL Time period] sur `All-time` et la [!UICONTROL Interval] sur `None`
1. Sous l’onglet `Group by` , ajoutez des `campaign` en tant que `grouping field`, puis cliquez sur **`Add All`** dans la zone
1. Ce rapport présente les utilisateurs enregistrés à tout moment par campagne

3 **. Créez un rapport qui segmente le LTV de l’utilisateur moyen par campagne :**

1. Dans un tableau de bord, cliquez sur **[!UICONTROL Add Report > Create report]**
1. Sélectionner la mesure de `Average lifetime revenue` qui calcule le chiffre d’affaires de durée de vie d’un utilisateur moyen
1. Définissez la [!UICONTROL Time period] sur `All-time` et la [!UICONTROL Interval] sur `None`
1. Sous l’onglet `Group by` , ajoutez `campaign` ou `utm\_campaign` comme [!UICONTROL grouping field], puis cliquez sur `Add All` dans la zone
1. Ce rapport présente le chiffre d’affaires moyen de l’utilisateur au cours de la durée de vie par campagne

**Enfin, calculez le retour sur investissement de la campagne en rassemblant ces trois analyses dans un seul rapport :**

1. Dans un tableau de bord, cliquez sur **[!UICONTROL Add Report > Create new report]**
1. Ajoutez en tant qu’entrée, utilisez les trois mesures utilisées ci-dessus. Une lettre est affectée à chaque élément (par exemple,\[`A`\], \[`B`\] et \[`C`\])
1. [!UICONTROL Cost] : ajoutez la mesure Coût d’AdWords - il s’agit de la variable \[A\]. Cela renvoie le coût par campagne.
1. [!UICONTROL Users] : ajoutez la mesure Nouveaux utilisateurs - il s’agit de la variable \[B\]. Cette fonction renvoie le nombre d’utilisateurs par campagne.
1. [!UICONTROL LTV] : ajoutez la mesure Chiffre d’affaires moyen sur toute la durée de vie - il s’agit de la variable \[`C`\]. Cette option renvoie le LTV par campagne.

1. Cliquez sur l’icône de masquage en regard du mot Graphique pour placer le focus sur le tableau
1. Utilisez maintenant `Add Formula` pour combiner ces mesures, comme suit :
1. [!UICONTROL ROI] : saisissez la formule `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`, si \[`A`\] représente `Ad Cost by Campaigns`, \[`B`\] représente `New users by campaigns` et \[`C`\] `LTV by campaigns`. Renvoie le ratio (coût moyen par acquisition - LTV de l’utilisateur moyen) / (coût moyen par acquisition)
1. [!UICONTROL Avg Return per User] : saisissez la formule **\[`C`\]-(\[`A`\]/\[`B`\])**. Cette option renvoie la marge moyenne réalisée sur un utilisateur en calculant (coût moyen par acquisition) - (coût moyen par utilisateur).
1. [!UICONTROL CPA] : saisissez le **`\[A\]/\[B\]`** de formule. Elle renvoie le coût réel de la campagne par acquisition.
1. D’autres mesures potentielles à inclure à partir des données [!DNL AdWords] incluent les sommes de `Impressions` et de `adClicks` (à partir des données [!DNL AdWords]), ainsi que le `number of orders` total effectué via une campagne particulière.
1. Il peut également être intéressant de calculer le retour sur investissement sur la base du LTV 30 jours et 90 jours après l’enregistrement ou le premier achat d’un utilisateur.

1. N’hésitez pas à cliquer et à faire glisser vos mesures et formules pour réorganiser les colonnes de votre rapport
1. Nommez votre rapport et veillez à l’enregistrer en tant que tableau.

## Campagnes de produit

Exécutez-vous des publicités spécifiques au produit ? Si tel est le cas, vous pouvez mesurer le retour sur investissement sur ces campagnes en calculant le chiffre d’affaires/coût pour un ou plusieurs produits spécifiques.

>[!NOTE]
>
>Cet exemple suppose que tous les coûts de campagne ont été utilisés exclusivement pour générer des achats de produit(s) spécifique(s). En supposant que l’intégralité du coût ait été dépensée pour générer des achats, le retour sur investissement qui en résulte prend en compte le pire scénario (coût le plus élevé par achat). Vous pouvez être sûr que votre retour sur investissement réel est supérieur à ce calcul. Exemple : en supposant que vous ayez dépensé 20 $ dans une campagne qui a généré 10 nouveaux utilisateurs et 10 achats, votre coût réel par achat est de 1 $. En supposant que tous les coûts aient servi à acquérir de nouveaux utilisateurs, le coût par achat est de 2 $.

Avant de commencer, [soumettez un ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) pour joindre les dimensions suivantes à votre tableau d’éléments de ligne (`sales\_flat\_order\_item, order\_item`) :

* Source de la commande (si vous suivez uniquement la source de référence au niveau de l’utilisateur, rejoignez la source de l’utilisateur).
* Campagne de la commande (si vous suivez uniquement la source de référence au niveau de l’utilisateur, rejoignez la campagne de l’utilisateur)
* Support de la commande (si vous suivez uniquement la source de référence au niveau de l’utilisateur, rejoignez le support de l’utilisateur)

**1. Commencez maintenant par créer un graphique qui renvoie le chiffre d’affaires par campagne pour un ou plusieurs produits spécifiques :**

1. Dans un tableau de bord, cliquez sur **[!UICONTROL Add Report > Create new report]**
1. Sélectionner la mesure de `Revenue by items` qui calcule le chiffre d’affaires au niveau des lignes
1. Définissez la [!UICONTROL Time period] sur `All-time` et la [!UICONTROL Interval] sur `None`
1. Sous l’onglet `Filter by` , ajoutez `product name 'IN'` nom de produit `A`, `B` de produit, `C` de produit, etc. et incluez tous les noms de produits ciblés par votre campagne séparés par une virgule (par exemple, `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`)
1. Sous l’onglet `Group by` , ajoutez `order's campaign` ou `order's utm\_campaign` comme champ `grouping`, puis cliquez sur **[!UICONTROL Add All]** dans la zone
1. Ce rapport présente le chiffre d’affaires pour un ou plusieurs produits spécifiques par campagne

**2. Pour calculer le retour sur investissement, combinez à nouveau les mesures dans un seul rapport :**

1. Dans un tableau de bord, cliquez sur **[!UICONTROL Add Report > Create new report]**
1. Ajoutez la mesure de `Revenue by items`, en suivant les instructions de filtrage et de regroupement de la campagne pour le rapport produit(s) spécifique(s) ci-dessus, puis cliquez sur **[!UICONTROL Hide]** sous la valeur scalaire de la mesure
1. Ajoutez maintenant la mesure [!DNL AdWords Cost], en suivant les instructions de filtrage et de regroupement par rapport au rapport `Ad cost by campaigns` que vous avez exploré dans la section `User acquisition campaigns` ci-dessus. Cliquez ensuite sur **[!UICONTROL Hide]** sous la valeur scalaire de la mesure
1. Une fois ces mesures en place, ajoutez des formules :
1. [!UICONTROL ROI] : saisissez la `\[A\]/\[B\]` de formule, si `\[A\]` représente `Revenue per campaign for specific product(s)` et `\[B\]` représente `Ad cost by campaigns`. Cette opération renvoie le ratio de (chiffre d’affaires pour un ou plusieurs produits spécifiques) / (coût de la campagne)
1. [!UICONTROL Return] : saisissez le `\[A\]-\[B\]` de formule. Elle renvoie la marge moyenne réalisée sur un utilisateur en calculant (coût moyen par acquisition) - (coût moyen par utilisateur)
   1. (Facultatif) [!UICONTROL Revenue] : affichez la mesure `Revenue by items` pour afficher le chiffre d’affaires de produit(s) spécifique(s) par campagne
   1. (Facultatif) [!UICONTROL Cost] : affichez la mesure de `AdWords Cost` pour afficher le coût des campagnes

1. Attribuez un nom à votre rapport et veillez à l’enregistrer sous forme de tableau

3 **. Répétez les étapes 1 et 2 ci-dessus pour chacun des produits ou groupes de produits annoncés.**

## Documentation connexe

* [Suivre la source de référence des commandes via [!DNL Google Analytics] E-Commerce](../importing-data/integrations/google-ecommerce.md)
* [Suivre la source de référence des utilisateurs dans votre base de données](../analysis/google-track-user-acq.md)
* [Effectuez le suivi des données relatives aux appareils, aux navigateurs et aux systèmes d’exploitation dans votre base de données](../analysis/track-usr-dev-browser.md)
* [Découvrez vos sources et canaux d’acquisition les plus précieux.](../analysis/most-value-source-channel.md)
* [Connecter votre  [!DNL Google Adwords] &#x200B;](../importing-data/integrations/google-adwords.md)
* [Comment fonctionne  [!DNL Google Analytics] ’attribution UTM ?](../analysis/utm-attributes.md)
* [Cinq bonnes pratiques pour le balisage UTM dans  [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
