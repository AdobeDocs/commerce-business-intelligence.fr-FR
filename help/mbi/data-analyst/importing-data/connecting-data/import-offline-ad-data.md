---
title: Importer d’autres données de dépenses publicitaires
description: Découvrez comment importer des données hors ligne ou d’autres données sur les dépenses publicitaires dans  [!DNL Commerce Intelligence].
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Importer d’autres données de dépenses publicitaires

Le chargement de vos données de dépenses publicitaires vous permet de mesurer le retour sur investissement de la campagne en associant votre coût publicitaire et le `customer lifetime value (CLV)` d’utilisateurs acquis à partir de vos campagnes.

## Chargement des données de coût publicitaire

La première étape de l’analyse et de la dépense des données consiste à obtenir les données. Comme la plupart des plateformes publicitaires permettent d’exporter des rapports, Adobe vous recommande d’exporter les données brutes de votre plateforme publicitaire et de les charger directement dans [!DNL Commerce Intelligence] sans aucune manipulation. Vous pouvez effectuer des opérations sur les données dans votre Data Warehouse, il n’est donc pas nécessaire de doubler d’efforts.

Une fois que vous avez exporté les données relatives aux dépenses publicitaires, utilisez la fonction [`File Upload` &#x200B;](../connecting-data/using-file-uploader.md) pour importer les données dans votre Data Warehouse. Vous pouvez charger de nouvelles données dans la même table de [!DNL Commerce Intelligence] au fil du temps.

## Sources hors ligne

Outre vos campagnes en ligne, vous pouvez également avoir des publicités hors ligne, par exemple à la radio ou sur un panneau d’affichage. Pour prendre en compte ces cas, vous pouvez charger manuellement une feuille de calcul avec les données de coûts à [!DNL Commerce Intelligence].

La structure de tableau explorée ci-dessous est recommandée lors de la création d’un fichier `.csv` pour enregistrer les données de dépenses publicitaires. Un fichier modèle est également joint au bas de cette rubrique pour servir d’exemple. Les colonnes recommandées sont les suivantes :

* `ID` - Il s’agit d’un identifiant unique pour chaque ligne de données utilisée par la base de données comme clé primaire. Cela doit être différent pour chaque ligne.
* `Date` - Il s’agit de la date d’exécution de la campagne au format aaaa-mm-jj.
* `Amount` - Il s’agit du montant que vous avez dépensé pour la campagne.
* `campaign` - Il s’agit du nom de la campagne. Si vous utilisez [!DNL Google Analytics] pour suivre vos autres données sur les dépenses publicitaires, elles doivent correspondre au nom utm\_campaign.
* `source` - Il s’agit du nom de la source. Si vous utilisez [!DNL Google Analytics], il doit correspondre au nom du `utm_source`.
* `other` (facultatif) - Vous pouvez également incorporer des colonnes supplémentaires qui vous aident à segmenter les campagnes et les coûts. Il peut également s’agir d’un moyen de résumer plusieurs noms de campagne UTM différents en une seule campagne cohérente à des fins de suivi. Plutôt que de configurer cela manuellement, il peut être préférable d’utiliser une recherche en V sur une seconde feuille pour faire correspondre chaque nom de campagne avec l’autre nom et de le signaler ici de manière dynamique.

## Connexe

* [Connect [!DNL AdWords] data](../integrations/google-adwords.md)
* [Augmentation du retour sur investissement des campagnes publicitaires](../../analysis/roi-ad-camp.md)
