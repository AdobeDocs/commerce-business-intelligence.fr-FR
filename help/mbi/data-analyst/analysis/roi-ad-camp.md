---
title: Augmentation du retour sur investissement sur vos campagnes publicitaires
description: Découvrez quelques différentes méthodes d’évaluation des performances de votre campagne.
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 0%

---

# Campagnes publicitaires et retour sur investissement

L’IMS vous permet de facilement [mariage des données de coûts publicitaires et des données de recettes](../../data-analyst/importing-data/integrations/google-adwords.md) de votre base de données. Vous pouvez ainsi identifier les campagnes qui ont le meilleur retour sur investissement. Dans cet article, nous explorons quelques méthodes différentes d’évaluation des performances de votre campagne.

## Conditions préalables

* Importez vos données de coûts publicitaires :
   * [Connectez-vous à [!DNL Google AdWords] to [!DNL MBI]](../importing-data/integrations/google-adwords.md): Cela synchronise automatiquement votre [!DNL Adwords] dépenser dans [!DNL MBI]
   * [Chargement d’autres données de coûts publicitaires](../importing-data/connecting-data/import-offline-ad-data.md): Ceci est recommandé pour les canaux sans connecteur direct vers [!DNL MBI]
   * Si vous importez des données de coût provenant de plusieurs sources, nous pouvons [consolidation](../../best-practices/consolidating-your-tables.md) les données de [!DNL MBI]. Simplement [envoi d’un ticket d’assistance](../../guide-overview.md).
* [Suivi des données du canal d’acquisition des utilisateurs](../analysis/google-track-user-acq.md)

## Campagnes d’acquisition d’utilisateurs

Les campagnes ciblées sur l’acquisition d’utilisateurs peuvent être mesurées sous de nombreux angles, notamment :

1. Nombre de nouveaux utilisateurs acquis des opérations
1. Taux de conversion de l’enregistrement à l’achat de campagnes
1. ROI des campagnes selon la valeur de durée de vie moyenne de l’utilisateur (LTV)

Les analyses (1) et (2) ci-dessus sont explorées dans un tutoriel distinct sur [identification des principaux canaux marketing](../analysis/most-value-source-channel.md). Nous étudions ici l’analyse (3) afin de mesurer le retour sur investissement de la campagne au fil du temps. Cela permet de déterminer si les utilisateurs acquis à partir d’une campagne spécifique ont généré suffisamment de recettes sur toute la durée de vie pour couvrir leurs coûts d’acquisition.

>[!NOTE]
>
>Nous partons du principe que tous les coûts de campagne ont été exclusivement utilisés pour acquérir de nouveaux utilisateurs. En réalité, le coût de votre campagne est également partagé avec l’acquisition de visites non converties, d’acheteurs réguliers, etc. Pourtant, en supposant que tous les coûts soient utilisés pour acquérir de nouveaux utilisateurs enregistrés, le ROI qui en résulte tiendra compte du pire scénario (coût par acquisition le plus élevé), afin que vous puissiez vous assurer que votre ROI réel est supérieur à notre calcul.
>
>Exemple : En supposant que vous ayez dépensé 20 $ pour une campagne qui a généré 10 nouveaux utilisateurs et 10 acheteurs réguliers, le coût réel par nouvel utilisateur est de 1 $, mais en supposant que tous les coûts ont été engagés pour acquérir de nouveaux utilisateurs, le coût par acquisition est de 2 $.)

**1. Commencez par créer un graphique qui segmente le coût de votre publicité par campagnes :**

1. Créez un [!UICONTROL Metric] qui additionne vos dépenses au fil du temps
1. Accédez à [!UICONTROL Data > Metrics]
1. Sélectionner `Add New Metric` et sélectionnez la variable [!DNL `Adwords...`] table qui enregistre votre [!DNL AdWords] données de coût.
1. Dans l’éditeur de mesures, attribuez un nom à votre mesure (par exemple, [!UICONTROL AdWord Cost])
1. À l’aide des listes déroulantes, effectuez une **Somme** sur le `adCost` dans la colonne [!DNL Adwords...] tableau (modification) ordonné par la variable `date` colonne .
   ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. nous en avons fini. Cliquez sur `Back to Metric List` dans la partie supérieure et accédez à n’importe quel tableau de bord.

1. Créer un rapport qui segmente les dépenses par campagnes
1. Dans n’importe quel tableau de bord, cliquez sur [!UICONTROL Add Report > Create new report]
1. Sélectionnez la [!UICONTROL Adword Cost] mesure que nous venons de créer
1. Définissez la variable [!UICONTROL Time period] to `All-time`, et [!UICONTROL Interval] to `None`
1. Sous , `Group by` onglet, ajouter `campaign` as [!UICONTROL grouping field], puis cliquez sur `Add All` dans la boîte.
1. Ce rapport présente votre [!DNL AdWords] coût par opération

**2. Nous allons ensuite créer un rapport qui comptabilise les nouveaux utilisateurs par campagnes :**

1. Dans n’importe quel tableau de bord, cliquez sur **[!UICONTROL Add Report > Create new report]**
1. Sélectionnez la `New users` mesure qui comptabilise le nombre de nouveaux utilisateurs enregistrés au fil du temps
1. Définissez la variable [!UICONTROL Time period] to `All-time`, et [!UICONTROL Interval] to `None`
1. Sous , `Group by` onglet, ajouter `campaign` as `grouping field`, puis cliquez sur **`Add All`** dans la zone
1. Ce rapport présente les utilisateurs enregistrés en temps réel par les campagnes.

**3. Créons également un rapport qui segmente la moyenne des utilisateurs LTV par campagnes :**

1. Dans n’importe quel tableau de bord, cliquez sur **[!UICONTROL Add Report > Create new report]**
1. Sélectionnez la `Average lifetime revenue` mesure qui calcule les recettes sur la durée de vie moyenne d’un utilisateur
1. Définissez la variable [!UICONTROL Time period] to `All-time`, et [!UICONTROL Interval] to `None`
1. Sous , `Group by` onglet, ajouter `campaign` ou `utm\_campaign` as [!UICONTROL grouping field], puis cliquez sur `Add All` dans la zone
1. Ce rapport présente les recettes moyennes de la durée de vie de l’utilisateur par campagnes.

**Enfin, nous allons calculer le retour sur investissement de la campagne en rassemblant les trois analyses suivantes dans un seul rapport :**

1. Dans n’importe quel tableau de bord, cliquez sur **[!UICONTROL Add Report > Create new report]**
1. Ajoutez comme entrée : nous utiliserons les trois mesures que nous avons utilisées ci-dessus. Une lettre leur est affectée (par exemple,\[`A`\], \[`B`\] et \[`C`\])
1. [!UICONTROL Cost]: Ajoutez la mesure Coût des AdWords : il s’agira de la variable \[A\]. Cela renverra simplement les coûts par campagnes.
1. [!UICONTROL Users]: Ajoutez la mesure Nouveaux utilisateurs : il s’agira de la variable \[B\]. Cela renverra simplement le nombre d’utilisateurs par campagne.
1. [!UICONTROL LTV]: Ajoutez la mesure Recettes sur la durée de vie moyenne - il s’agira de variable \[`C`\]. Cela renverra simplement LTV par des campagnes.

1. Cliquez sur l’icône de masquage en regard du mot Graphique pour vous concentrer sur le tableau.
1. Maintenant, nous allons utiliser `Add Formula` pour combiner ces mesures, comme suit :
1. [!UICONTROL ROI]: Saisir la formule `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`, si \[`A`\] représente `Ad Cost by Campaigns`, \[`B`\] représente `New users by campaigns`, et \[`C`\] `LTV by campaigns`. Cela renverra le ratio (LTV utilisateur moyen - coût moyen par acquisition) / (coût moyen par acquisition)
1. [!UICONTROL Avg Return per User]: Saisir la formule **\[`C`\]-(\[`A`\]/\[`B`\])**. Cela renverra la marge moyenne réalisée sur un utilisateur en calculant (LTV utilisateur moyen) - (coût moyen par acquisition).
1. [!UICONTROL CPA]: Saisir la formule **`\[A\]/\[B\]`**. Cela renverra le coût réel de la campagne par acquisition.
1. Autres mesures potentielles à inclure à partir de [!DNL AdWords] Les données incluent des sommes  `Impressions` et `adClicks` (de [!DNL AdWords] data), ainsi que le total `number of orders` effectuées via une opération particulière.
1. Il peut également être intéressant de calculer le retour sur investissement d’après LTV 30 jours et 90 jours après l’enregistrement ou le premier achat d’un utilisateur.

1. N’hésitez pas à cliquer et à faire glisser vos mesures et formules pour réorganiser les colonnes de votre rapport.
1. Nommez votre rapport et veillez à l’enregistrer en tant que tableau.

## Campagnes sur les produits

Effectuez-vous des publicités spécifiques à un produit ? Si tel est le cas, vous pouvez mesurer le ROI de ces campagnes en calculant les recettes/coûts pour des produits spécifiques.

>[!NOTE]
>
>Nous partons du principe que tous les coûts de campagne ont été exclusivement utilisés pour générer des achats de produits spécifiques. En supposant que tous les coûts aient été dépensés pour générer des achats, le retour sur investissement qui en résulte tient compte du scénario le plus défavorable (coût par achat le plus élevé), afin que vous soyez certain que votre retour sur investissement réel est supérieur à ce calcul. Exemple : En supposant que vous ayez dépensé 20 € pour une campagne qui a généré 10 nouveaux utilisateurs et 10 achats, le coût réel par achat est de 1 €, mais en supposant que tous les coûts ont été engagés pour acquérir de nouveaux utilisateurs, le coût par achat est de 2 €.)*

Avant de commencer, [envoi d’un ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) pour joindre les dimensions suivantes à votre tableau d’éléments de ligne (`sales\_flat\_order\_item, order\_item`) :

* Source de la commande (si vous effectuez uniquement le suivi de la source de référence au niveau de l’utilisateur, rejoignez la source de l’utilisateur)
* Campagne de la commande (si vous effectuez uniquement le suivi de la source de référence au niveau de l’utilisateur, rejoignez la campagne de l’utilisateur)
* Support de la commande (si vous effectuez uniquement le suivi de la source de référence au niveau de l’utilisateur, rejoignez le support de l’utilisateur)

**1. Commencez maintenant par créer un graphique qui renvoie les recettes par campagne pour un ou plusieurs produits spécifiques :**

1. Dans n’importe quel tableau de bord, cliquez sur **[!UICONTROL Add Report > Create new report]**
1. Sélectionnez la `Revenue by items` mesure qui calcule les recettes au niveau des éléments de ligne
1. Définissez la variable [!UICONTROL Time period] to `All-time`, et [!UICONTROL Interval] to `None`
1. Sous , `Filter by` onglet, ajouter `product name 'IN'` Produit `A`, produit `B`, produit `C`, ...&quot; et inclure tous les noms de produits ciblés par votre campagne, séparés par une virgule (par exemple, `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`)
1. Sous , `Group by` onglet, ajouter `order's campaign` ou `order's utm\_campaign` as `grouping` puis cliquez sur **[!UICONTROL Add All]** dans la zone
1. Ce rapport présente les recettes de produits spécifiques par campagnes.

**2. Pour calculer le retour sur investissement, nous combinons à nouveau les mesures dans un rapport :**

1. Dans n’importe quel tableau de bord, cliquez sur **[!UICONTROL Add Report > Create new report]**
1. Ajoutez la variable `Revenue by items` , suivez le filtre et le groupe selon les instructions de la campagne pour le rapport produit(s) spécifique(s) ci-dessus, puis cliquez sur **[!UICONTROL Hide]** sous la valeur scalaire de la mesure
1. Ajoutez maintenant la variable [!DNL AdWords Cost] , en suivant le filtre et le groupe par directions à partir de la variable `Ad cost by campaigns` rapport que nous avons exploré dans la section `User acquisition campaigns` la section ci-dessus; puis cliquez sur **[!UICONTROL Hide]** sous la valeur scalaire de la mesure
1. Une fois ces mesures en place, nous allons ajouter des formules :
1. [!UICONTROL ROI]: Saisir la formule `\[A\]/\[B\]`, si `\[A\]` représente `Revenue per campaign for specific product(s)` et `\[B\]` représente `Ad cost by campaigns`. Cela renverra le ratio (Recettes pour un ou plusieurs produits spécifiques) / (Coût de la campagne)
1. [!UICONTROL Return]: Saisir la formule `\[A\]-\[B\]`. Cela renverra la marge moyenne réalisée sur un utilisateur en calculant (LTV utilisateur moyen) - (coût moyen par acquisition)
1. (Facultatif) [!UICONTROL Revenue]: Afficher le `Revenue by items` mesure pour afficher les recettes pour des produits spécifiques par campagne
1. (Facultatif) [!UICONTROL Cost]: Afficher le `AdWords Cost` mesure pour afficher le coût des campagnes

1. Attribuez un nom à votre rapport et veillez à l’enregistrer en tant que tableau.

**3. Répétez les étapes 1 et 2 ci-dessus pour chacun de vos produits ou groupes de produits annoncés.**

## Documentation connexe

* [Suivi de la source de référence de commande via [!DNL Google Analytics] Commerce électronique](../importing-data/integrations/google-ecommerce.md)
* [Suivi de la source de référence des utilisateurs dans votre base de données](../analysis/google-track-user-acq.md)
* [Suivi des données utilisateur, navigateur et système d’exploitation dans votre base de données](../analysis/track-usr-dev-browser.md)
* [Découvrez vos sources et canaux d’acquisition les plus précieux](../analysis/most-value-source-channel.md)
* [Connectez-vous à [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Comment [!DNL Google Analytics] Fonctionnement de l’attribution UTM ?](../analysis/utm-attributes.md)
* [5 bonnes pratiques pour le balisage UTM dans [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
