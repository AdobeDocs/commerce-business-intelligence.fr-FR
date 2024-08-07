---
title: Importation d’autres données de dépenses publicitaires
description: Découvrez comment importer des données hors ligne ou d’autres données de dépenses publicitaires dans  [!DNL Commerce Intelligence].
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Importation d’autres données de dépenses publicitaires

Le téléchargement de vos données de dépenses publicitaires vous permet de mesurer le retour sur investissement de la campagne en associant vos coûts publicitaires et l’ `customer lifetime value (CLV)` des utilisateurs acquis de vos campagnes.

## Chargement des données de coûts publicitaires

La première étape de l’analyse des données de dépenses publicitaires consiste à obtenir les données. Étant donné que la plupart des plateformes publicitaires vous permettent d’exporter des rapports, Adobe vous recommande d’exporter les données brutes de votre plateforme publicitaire et de les télécharger directement vers [!DNL Commerce Intelligence] sans aucune manipulation. Vous pouvez effectuer des opérations sur les données de votre Data Warehouse. Il n’est donc pas nécessaire de doubler vos efforts.

Après avoir exporté les données de dépenses publicitaires, utilisez la [`File Upload` fonction](../connecting-data/using-file-uploader.md) pour importer les données dans votre Data Warehouse. Vous pouvez charger de nouvelles données sur la même table [!DNL Commerce Intelligence] au fil du temps.

## Sources hors ligne

Outre vos campagnes en ligne, vous pouvez également avoir des publicités hors ligne, comme à la radio ou sur un panneau d’affichage. Pour tenir compte de ces cas, vous pouvez charger manuellement une feuille de calcul avec les données de coût vers [!DNL Commerce Intelligence].

La structure de tableau décrite ci-dessous est recommandée lors de la création d’un fichier `.csv` pour enregistrer les données de dépenses publicitaires. Un fichier de modèle est également joint au bas de cette rubrique pour servir d’exemple. Les colonnes recommandées sont les suivantes :

* `ID` - Il s’agit d’un identifiant unique pour chaque ligne de données utilisée par la base de données comme clé primaire. Cela doit être différent pour chaque ligne.
* `Date` : date d’exécution de la campagne, au format aaaa-mm-jj.
* `Amount` - Il s’agit du montant que vous avez dépensé pour la campagne.
* `campaign` - Il s’agit du nom de la campagne. Si vous utilisez [!DNL Google Analytics] pour effectuer le suivi de vos autres données de dépenses publicitaires, elles doivent correspondre au nom utm\_campaign.
* `source` - Il s’agit du nom source. Si vous utilisez [!DNL Google Analytics], cela doit correspondre au nom `utm_source`.
* `other` (Facultatif) : vous pouvez également incorporer des colonnes supplémentaires pour vous aider à segmenter les campagnes et les coûts. Il peut également s’agir d’un moyen de résumer plusieurs noms de campagne UTM différents en une seule campagne cohérente à des fins de suivi. Plutôt que de configurer cette configuration manuellement, il peut être judicieux d’utiliser une recherche en V dans une seconde feuille afin de faire correspondre chaque nom de campagne à l’autre nom et de le signaler de manière dynamique ici.

## Associé

* [Connect [!DNL AdWords] data](../integrations/google-adwords.md)
* [Augmentation du retour sur investissement des campagnes publicitaires](../../analysis/roi-ad-camp.md)
