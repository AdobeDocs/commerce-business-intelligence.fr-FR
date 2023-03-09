---
title: Importation d’autres données de dépenses publicitaires
description: Découvrez comment importer des données hors ligne ou d’autres données de dépenses publicitaires dans [!DNL MBI].
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Importation d’autres données de dépenses publicitaires

Le téléchargement de vos données de dépenses publicitaires vous permet de mesurer le retour sur investissement de la campagne en associant votre coût publicitaire et le client. `lifetime value (CLV)` des utilisateurs acquis à partir de vos campagnes.

## Chargement des données de coûts publicitaires

La première étape de l’analyse des données de dépenses publicitaires consiste à obtenir les données. Comme la plupart des plateformes publicitaires vous permettent d’exporter des rapports, Adobe vous recommande d’exporter les données brutes de votre plateforme publicitaire et de les transférer directement vers [!DNL MBI] sans aucune manipulation. Vous pouvez effectuer des opérations sur les données de votre Data Warehouse. Il n’est donc pas nécessaire de doubler vos efforts.

Après avoir exporté les données de dépenses publicitaires, utilisez la variable [`File Upload` fonctionnalité](../connecting-data/using-file-uploader.md) pour importer les données dans votre Data Warehouse. Vous pouvez transférer de nouvelles données vers le même [!DNL MBI] au fil du temps.

## Sources hors ligne

Outre vos campagnes en ligne, vous pouvez également avoir des publicités hors ligne, comme à la radio ou sur un panneau d’affichage. Pour tenir compte de ces cas, vous pouvez transférer manuellement une feuille de calcul avec les données de coût vers [!DNL MBI].

La structure de tableau décrite ci-dessous est recommandée lors de la création d’une `.csv` pour enregistrer les données de dépenses publicitaires. Un fichier de modèle est également joint au bas de cet article pour servir d’exemple. Les colonnes recommandées sont les suivantes :

* `ID` - Il s’agit d’un identifiant unique pour chaque ligne de données utilisée par la base de données comme clé Principale. Cela doit être différent pour chaque ligne.
* `Date` - Date d’exécution de la campagne, au format aaaa-mm-jj.
* `Amount` - Il s’agit du montant que vous avez dépensé pour la campagne.
* `campaign` - Il s’agit du nom de la campagne. Si vous utilisez [!DNL Google Analytics] pour effectuer le suivi de vos autres données de dépenses publicitaires, elles doivent correspondre au nom utm\_campaign.
* `source` - Il s’agit du nom de la source. Si vous utilisez [!DNL Google Analytics], cela doit correspondre au `utm_source` nom.
* `other` (Facultatif) - Vous pouvez également incorporer des colonnes supplémentaires qui vous aident à segmenter les campagnes et les coûts. Il peut également s’agir d’un moyen de résumer plusieurs noms de campagne UTM différents en une seule campagne cohérente à des fins de suivi. Plutôt que de configurer cette configuration manuellement, il peut être judicieux d’utiliser une recherche en V dans une seconde feuille afin de faire correspondre chaque nom de campagne à l’autre nom et de le signaler de manière dynamique ici.

## Associé

* [Connexion [!DNL AdWords] data](../integrations/google-adwords.md)
* [Augmentation du retour sur investissement des campagnes publicitaires](../../analysis/roi-ad-camp.md)
