---
title: Augmentation du retour sur investissement sur vos campagnes publicitaires
description: Découvrez quelques différentes méthodes d’évaluation des performances de votre campagne.
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
role: Admin, User
feature: Data Warehouse Manager, Reports, Campaigns
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1247'
ht-degree: 0%

---

# Campagnes Advertising et retour sur investissement

[!DNL Adobe Commerce Intelligence] vous permet de [ facilement &lbrace;marier les données de coût de publicité et les données de recettes](../../data-analyst/importing-data/integrations/google-adwords.md) de votre base de données. Vous pouvez ainsi identifier les campagnes qui génèrent le meilleur retour sur investissement. Cette rubrique explore quelques différentes méthodes d’évaluation des performances de votre campagne.

## Conditions préalables

* Importez vos données de coûts publicitaires :
   * [Connectez votre  [!DNL Google AdWords] à [!DNL Commerce Intelligence]](../importing-data/integrations/google-adwords.md) : cela synchronise vos [!DNL Adwords] dépenses dans [!DNL Commerce Intelligence]
   * [Télécharger d’autres données de coûts publicitaires](../importing-data/connecting-data/import-offline-ad-data.md) : cette méthode est recommandée pour les canaux sans connecteur direct vers [!DNL Commerce Intelligence]
   * Si vous importez des données de coût provenant de plusieurs sources, vous pouvez [consolider](../../best-practices/consolidating-your-tables.md) les données dans [!DNL Commerce Intelligence]. Il vous suffit de [ envoyer un ticket d’assistance](../../guide-overview.md#Submitting-a-Support-Ticket).
* [Suivi des données du canal d’acquisition des utilisateurs](../analysis/google-track-user-acq.md)

## Campagnes d’acquisition d’utilisateurs

Les campagnes ciblées sur l’acquisition d’utilisateurs peuvent être mesurées sous de nombreux angles, notamment :

1. Nombre de nouveaux utilisateurs acquis des opérations
1. Taux de conversion de l’enregistrement à l’achat de campagnes
1. ROI des campagnes selon la valeur de durée de vie moyenne de l’utilisateur (LTV)

Les analyses (1) et (2) ci-dessus sont explorées dans un tutoriel distinct sur l’ [identification de vos principaux canaux marketing](../analysis/most-value-source-channel.md). Vous découvrez ici l’analyse (3) pour mesurer le retour sur investissement de la campagne au fil du temps. Cela indique si les utilisateurs acquis à partir d’une campagne spécifique ont généré suffisamment de recettes sur la durée de vie pour couvrir le coût d’acquisition.

>[!NOTE]
>
>Cet exemple suppose que tous les coûts de campagne ont été utilisés exclusivement pour acquérir de nouveaux utilisateurs. En réalité, le coût de votre campagne est également partagé avec l’acquisition de visites non converties, d’acheteurs réguliers, etc. En supposant que tous les coûts soient utilisés pour acquérir de nouveaux utilisateurs enregistrés, le ROI qui en résulte tient compte du scénario le plus défavorable (coût par acquisition le plus élevé). Vous pouvez être certain que votre ROI réel est supérieur à votre calcul.
>
>Exemple : en supposant que vous ayez dépensé 20 € pour une campagne qui a généré 10 nouveaux utilisateurs et 10 acheteurs réguliers, le coût réel par nouvel utilisateur est de 1 €. Toutefois, en supposant que tous les coûts aient été engagés pour acquérir de nouveaux utilisateurs, le coût par acquisition est de 2 $.

**1. Commencez par créer un graphique qui segmente votre coût de publicité par campagnes :**

1. Créez un [!UICONTROL Metric] qui additionne vos dépenses au fil du temps
1. Accédez à [!UICONTROL Data > Metrics]
1. Sélectionnez `Add New Metric` et sélectionnez la table [!DNL `Adwords...`] qui enregistre vos données de coût [!DNL AdWords].
1. Dans l’éditeur de mesures, attribuez un nom à votre mesure (par exemple, [!UICONTROL AdWord Cost]).
1. À l’aide des listes déroulantes, effectuez une **Somme** sur la colonne `adCost` de la table [!DNL Adwords...] (Modification) triée par la colonne `date`.
   ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. Cliquez sur `Back to Metric List` en haut de l’écran et accédez à n’importe quel tableau de bord.

1. Créer un rapport qui segmente les dépenses par campagnes
1. Dans n&#39;importe quel tableau de bord, cliquez sur [!UICONTROL Add Report > Create report]
1. Sélectionnez la mesure [!UICONTROL Adword Cost] que vous venez de créer.
1. Définissez le [!UICONTROL Time period] sur `All-time` et [!UICONTROL Interval] sur `None`
1. Sous l’onglet `Group by`, ajoutez `campaign` en tant que [!UICONTROL grouping field], puis cliquez sur `Add All` dans la zone.
1. Ce rapport présente le coût [!DNL AdWords] de votre activité par campagne (coût total)

**2. Créez un rapport qui comptabilise les nouveaux utilisateurs par campagnes :**

1. Dans n&#39;importe quel tableau de bord, cliquez sur **[!UICONTROL Add Report > Create report]**
1. Sélectionnez la mesure `New users` qui comptabilise le nombre de nouveaux utilisateurs enregistrés au fil du temps.
1. Définissez le [!UICONTROL Time period] sur `All-time` et [!UICONTROL Interval] sur `None`
1. Sous l’onglet `Group by`, ajoutez `campaign` comme `grouping field`, puis cliquez sur **`Add All`** dans la zone
1. Ce rapport présente les utilisateurs enregistrés en temps réel par les campagnes

**3. Créez un rapport qui segmente la LTV de l’utilisateur moyen par campagnes :**

1. Dans n&#39;importe quel tableau de bord, cliquez sur **[!UICONTROL Add Report > Create report]**
1. Sélectionnez la mesure `Average lifetime revenue` qui calcule les recettes de durée de vie moyenne d’un utilisateur.
1. Définissez le [!UICONTROL Time period] sur `All-time` et [!UICONTROL Interval] sur `None`
1. Sous l’onglet `Group by`, ajoutez `campaign` ou `utm\_campaign` en tant que [!UICONTROL grouping field], puis cliquez sur `Add All` dans la zone.
1. Ce rapport présente les recettes moyennes de la durée de vie de l’utilisateur par campagnes.

**Enfin, calculez le retour sur investissement de la campagne en rassemblant ces trois analyses dans un seul rapport :**

1. Dans n&#39;importe quel tableau de bord, cliquez sur **[!UICONTROL Add Report > Create new report]**
1. Ajoutez comme entrée, utilisez les trois mesures utilisées ci-dessus. Une lettre leur est affectée (par exemple,\[`A`\], \[`B`\] et \[`C`\]).
1. [!UICONTROL Cost] : ajoutez la mesure Coût des AdWords - il s’agit de la variable \[A\]. Cela renvoie le coût par campagnes.
1. [!UICONTROL Users] : ajoutez la mesure Nouveaux utilisateurs - il s’agit de la variable \[B\]. Cette opération renvoie le nombre d’utilisateurs par campagne.
1. [!UICONTROL LTV] : ajoutez la mesure Recettes sur la durée de vie moyenne - il s’agit de la variable \[`C`\]. Cela renvoie LTV par campagnes.

1. Cliquez sur l’icône de masquage en regard du mot Graphique pour vous concentrer sur le tableau.
1. Maintenant, utilisez `Add Formula` pour combiner ces mesures, comme suit :
1. [!UICONTROL ROI] : Entrez la formule `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`, si \[`A`\] représente `Ad Cost by Campaigns`, \[`B`\] représente `New users by campaigns` et \[`C`\] `LTV by campaigns`. Cela renvoie le ratio (LTV utilisateur moyen - coût moyen par acquisition) / (coût moyen par acquisition)
1. [!UICONTROL Avg Return per User] : Entrez la formule **\[`C`\]-(\[`A`\]/\[`B`\])**. Cela renvoie la marge moyenne réalisée sur un utilisateur en calculant (LTV utilisateur moyen) - (coût moyen par acquisition).
1. [!UICONTROL CPA] : Entrez la formule **`\[A\]/\[B\]`**. Cette opération renvoie le coût par acquisition réel de la campagne.
1. D’autres mesures potentielles à inclure à partir des données [!DNL AdWords] incluent les sommes de `Impressions` et `adClicks` (à partir des données [!DNL AdWords]), ainsi que le total `number of orders` effectué via une campagne spécifique.
1. Il peut également être intéressant de calculer le retour sur investissement d’après LTV 30 jours et 90 jours après l’enregistrement ou le premier achat d’un utilisateur.

1. N’hésitez pas à cliquer et à faire glisser vos mesures et formules pour réorganiser les colonnes de votre rapport.
1. Nommez votre rapport et veillez à l’enregistrer en tant que tableau.

## Campagnes sur les produits

Effectuez-vous des publicités spécifiques à un produit ? Si tel est le cas, vous pouvez mesurer le ROI de ces campagnes en calculant les recettes/coûts pour des produits spécifiques.

>[!NOTE]
>
>Cet exemple suppose que tous les coûts de campagne ont été utilisés exclusivement pour générer des achats de produits spécifiques. En supposant que tout le coût ait été dépensé pour générer des achats, le retour sur investissement qui en résulte tient compte du scénario le plus défavorable (coût par achat le plus élevé). Vous pouvez être certain que votre ROI réel est supérieur à ce calcul. Exemple : en supposant que vous ayez dépensé 20 € pour une campagne qui a généré 10 nouveaux utilisateurs et 10 achats, le coût réel par achat est de 1 €. En supposant que tous les coûts aient été engagés pour acquérir de nouveaux utilisateurs, le coût par achat est de 2 $.

Avant de commencer, [envoyez un ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) pour joindre les dimensions suivantes à votre table d’éléments de ligne (`sales\_flat\_order\_item, order\_item`) :

* Source de la commande (si vous effectuez uniquement le suivi de la source de référence au niveau de l’utilisateur, rejoignez la source de l’utilisateur)
* Campagne de la commande (si vous effectuez uniquement le suivi de la source de référence au niveau de l’utilisateur, rejoignez la campagne de l’utilisateur)
* Support de la commande (si vous effectuez uniquement le suivi de la source de référence au niveau de l’utilisateur, rejoignez le support de l’utilisateur)

**1. Commencez maintenant par créer un graphique qui renvoie les recettes par campagne pour un ou plusieurs produits spécifiques :**

1. Dans n&#39;importe quel tableau de bord, cliquez sur **[!UICONTROL Add Report > Create new report]**
1. Sélectionnez la mesure `Revenue by items` qui calcule les recettes au niveau des éléments de ligne.
1. Définissez le [!UICONTROL Time period] sur `All-time` et [!UICONTROL Interval] sur `None`
1. Sous l’onglet `Filter by` , ajoutez `product name 'IN'` Produit `A`, Produit `B`, Produit `C`, ...&quot; et incluez tous les noms de produits ciblés par votre campagne, séparés par une virgule (par exemple, `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`).
1. Sous l’onglet `Group by`, ajoutez `order's campaign` ou `order's utm\_campaign` comme champ `grouping`, puis cliquez sur **[!UICONTROL Add All]** dans la zone.
1. Ce rapport présente les recettes de produits spécifiques par campagnes.

**2. Pour calculer le retour sur investissement, vous combinez à nouveau des mesures dans un rapport :**

1. Dans n&#39;importe quel tableau de bord, cliquez sur **[!UICONTROL Add Report > Create new report]**
1. Ajoutez la mesure `Revenue by items`, en suivant le filtre et le groupe par directions à partir de la campagne pour le rapport produit(s) spécifique(s) ci-dessus et cliquez sur **[!UICONTROL Hide]** sous la valeur scalaire de la mesure.
1. Ajoutez maintenant la mesure [!DNL AdWords Cost], en suivant le filtre et le groupe par directions du rapport `Ad cost by campaigns` que vous avez exploré dans la section `User acquisition campaigns` ci-dessus, puis cliquez sur **[!UICONTROL Hide]** sous la valeur scalaire de la mesure.
1. Une fois ces mesures en place, ajoutez des formules :
1. [!UICONTROL ROI] : Entrez la formule `\[A\]/\[B\]`, si `\[A\]` représente `Revenue per campaign for specific product(s)` et `\[B\]` représente `Ad cost by campaigns`. Cela renvoie le ratio (Recettes pour un ou plusieurs produits spécifiques) / (Coût de la campagne)
1. [!UICONTROL Return] : Entrez la formule `\[A\]-\[B\]`. Renvoie la marge moyenne réalisée sur un utilisateur en calculant (LTV utilisateur moyen) - (coût moyen par acquisition)
1. (Facultatif) [!UICONTROL Revenue] : affichez la mesure `Revenue by items` afin d’afficher les recettes pour des produits spécifiques par campagne.
1. (Facultatif) [!UICONTROL Cost] : affichez la mesure `AdWords Cost` pour afficher le coût des campagnes.

1. Attribuez un nom à votre rapport et veillez à l’enregistrer en tant que tableau

**3. Répétez les étapes 1 et 2 ci-dessus pour chacun de vos produits ou groupes de produits annoncés.**

## Documentation connexe

* [Suivi de la source de référence de commande via [!DNL Google Analytics] E-Commerce](../importing-data/integrations/google-ecommerce.md)
* [Suivi de la source de référence des utilisateurs dans votre base de données](../analysis/google-track-user-acq.md)
* [Suivi des données de périphérique, de navigateur et de système d’exploitation utilisateur dans votre base de données](../analysis/track-usr-dev-browser.md)
* [Découvrez vos sources et canaux d’acquisition les plus précieux](../analysis/most-value-source-channel.md)
* [Connectez-vous à votre compte  [!DNL Google Adwords] ](../importing-data/integrations/google-adwords.md)
* [Comment fonctionne l’attribution de [!DNL Google Analytics] UTM ?](../analysis/utm-attributes.md)
* [Cinq bonnes pratiques pour le balisage UTM dans [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
