---
title: Créer et utiliser des vues de Data Warehouse
description: Découvrez une méthode de création de tables stockées en modifiant une table existante ou en associant ou en consolidant plusieurs tables à l’aide de SQL.
exl-id: 5aa571c9-7f38-462c-8f1b-76a826c9dc55
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 6%

---

# Utilisation des vues de Data Warehouse

Ce document décrit l’objectif et les utilisations de `Data Warehouse Views` accessibles en accédant à **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**. Vous trouverez ci-dessous une explication de ce qu’il fait et comment créer des vues, ainsi qu’un exemple d’utilisation de `Data Warehouse Views` pour consolider les données [!DNL Facebook] et [!DNL AdWords] dépensées.

## Objectif général

La fonction `Data Warehouse Views` est une méthode pour créer de nouvelles tables stockées en modifiant une table existante, ou en associant ou en consolidant plusieurs tables à l’aide de SQL. Une fois qu’un `Data Warehouse View` a été créé et traité par un cycle de mise à jour, il est renseigné dans votre Data Warehouse en tant que nouveau tableau sous la liste déroulante `Data Warehouse Views`, comme illustré ci-dessous :

![](../../assets/Data_Warehouse.png)

À partir de là, votre nouvelle vue fonctionne comme n’importe quel autre tableau, ce qui vous permet de créer de nouvelles colonnes calculées ou de créer des mesures et des rapports.

`Data Warehouse Views` sont principalement utilisés pour consolider plusieurs tableaux similaires mais disparates, de sorte que tous les rapports puissent être créés sur un seul nouveau tableau. Quelques exemples courants incluent la consolidation des tables d’une base de données héritée et d’une base de données active afin de combiner des données historiques et actuelles, ou la combinaison de plusieurs sources d’annonces comme Facebook et AdWords dans une table `Consolidated ad spend` unique.

Si vous connaissez SQL, ces deux exemples de consolidation utilisent la fonction `UNION`, mais vous pouvez utiliser n’importe quelle syntaxe et fonction PostgreSQL lors de la création d’une nouvelle vue.

## Création et gestion des vues de Data Warehouse

De nouveaux `Data Warehouse Views` peuvent être créés et les vues existantes peuvent être supprimées en accédant à **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**, comme illustré ci-dessous :

![](../../assets/Data_Warehouse_Views.png)

À partir de là, vous pouvez créer une vue en suivant les exemples d’instructions ci-dessous :

1. Si vous observez une vue existante, cliquez sur **[!UICONTROL New Data Warehouse View]** pour ouvrir une fenêtre de requête vide. Si une fenêtre de requête vierge est déjà ouverte, passez à l’étape suivante.
1. Attribuez un nom à la vue en saisissant dans le champ `View Name`. Le nom fourni ici détermine le nom d’affichage de la vue dans le Data Warehouse. `View names` sont limités à des lettres minuscules, des chiffres et des traits de soulignement (_). Tous les autres caractères sont interdits.
1. Saisissez votre requête dans la fenêtre intitulée `Select Query`, en utilisant la syntaxe PostgreSQL standard.

   >[!NOTE]
   >
   >Votre requête doit référencer des noms de colonne spécifiques. L&#39;utilisation du caractère `*` pour sélectionner toutes les colonnes n&#39;est pas autorisée.

1. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save]** pour enregistrer votre vue. Votre vue a temporairement un état `Pending` jusqu’à ce qu’elle soit traitée d’ici le cycle de mise à jour complet suivant, à ce moment-là l’état passe à `Active`. Après avoir été traité par une mise à jour, votre vue est prête à être utilisée dans les rapports.

Il est important de mentionner qu’après l’enregistrement, la requête sous-jacente utilisée pour générer un `Data Warehouse View` ne peut pas être modifiée. Si vous devez ajuster la structure d’un `Data Warehouse View`, vous devez créer une vue et migrer manuellement toutes les colonnes, mesures ou rapports calculés de la vue d’origine vers la nouvelle. Une fois la migration terminée, vous pouvez supprimer la vue d’origine en toute sécurité. Étant donné que `Data Warehouse Views` n’est pas modifiable, Adobe vous recommande de tester la sortie de votre requête à l’aide de `SQL Report Builder` avant d’enregistrer votre requête en tant que vue du Data Warehouse.

## Exemple : [!DNL Facebook] et [!DNL Google AdWords] données

Regardez de plus près l&#39;un des exemples mentionnés précédemment dans cet article : la consolidation des [!DNL Facebook] et [!DNL AdWords] dépenses des données dans un nouveau tableau publicitaire consolidé. Cela implique le plus souvent la consolidation de deux tables, avec les exemples de jeux de données ci-dessous :

`Ad source: Google AdWords`

`Table name: campaigns67890`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | eee | 60 | 2017-05-05 00:00:00 | 2000 | 10,2 |
| 2 | ggg | 40 | 2017-05-23 00:00:00 | 900 | 4,6 |
| 3 | aaa | 22 | 2017-06-12 00:00:00 | 400 | 2,5 |
| 4 | eee | 350 | 2017-06-30 00:00:00 | 14500 | 35 |
| 5 | fff | 280 | 2017-07-10 00:00:00 | 10200 | 28,5 |

`Ad source: Facebook`

`Table name: facebook_ads_insights_12345`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | aaa | 25 | 2017-05-01 00:00:00 | 1200 | 5 |
| 2 | jj | 12 | 2017-05-15 00:00:00 | 800 | 2,5 |
| 3 | aaa | 40 | 2017-05-22 00:00:00 | 2000 | 7 |
| 4 | aaa | 110 | 2017-06-08 00:00:00 | 6000 | 10 |
| 5 | ccc | 5 | 2017-07-06 00:00:00 | 300 | 1,2 |

Pour créer une table de dépenses publicitaires unique contenant à la fois les campagnes [!DNL Facebook] et [!DNL Google AdWords], vous devez écrire une requête SQL et utiliser la fonction `UNION ALL` . Une instruction `UNION ALL` est généralement utilisée pour combiner plusieurs requêtes SQL distinctes tout en ajoutant les résultats de chaque requête à une seule sortie.

Il existe quelques exigences d’une instruction `UNION` qui méritent d’être mentionnées, comme indiqué dans la [documentation](https://www.postgresql.org/docs/8.3/queries-union.html) de PostgreSQL :

* Toutes les requêtes doivent renvoyer le même nombre de colonnes
* Les colonnes correspondantes doivent comporter des types de données identiques.

Lors de l’exécution d’une instruction `UNION` ou `UNION ALL`, les noms des colonnes dans la sortie finale reflètent le nommage des colonnes dans votre première requête.

En règle générale, consolider vos [!DNL Facebook] et [!DNL Google AdWords] dépensent des données dans un `Data Warehouse View` nécessite la création d&#39;un tableau avec sept colonnes, avec une requête similaire à celle-ci :

```sql
    SELECT
        "_id" as id,
        'AdWords' as ad_source,
        "date",
        "campaign",
        "adCost" as spend,
        "impressions",
        "adClicks" as clicks
    FROM campaigns67890
    UNION
    SELECT
        "_id" as id,
        'Facebook' as ad_source,
        "date_start" as date,
        "campaign_name" as campaign,
        "spend",
        "impressions",
        "clicks"
    FROM facebook_ads_insights_12345
```

Voici quelques points importants :

* Par souci de clarté, toutes les colonnes sont affectées d’un alias au-dessus afin que les noms correspondent à toutes les requêtes. Cependant, il ne s’agit pas d’une exigence. L’ordre dans lequel les colonnes sont appelées dans les requêtes SELECT détermine la manière dont elles sont alignées.
* Une nouvelle colonne appelée `ad_source` est créée pour faciliter le filtrage des données [!DNL AdWords] ou [!DNL Facebook]. N’oubliez pas que cette requête combine toutes les données des deux tables. Si vous ne créez pas de colonne comme `ad_source`, il n’existe aucun moyen facile d’identifier les dépenses à partir d’une source particulière.

L’enregistrement de la requête ci-dessus en tant que `Data Warehouse View` crée une table avec les dépenses [!DNL Facebook] et [!DNL AdWords], comme ci-dessous :

| **`id`** | **`ad_source`** | **`date`** | **`campaign`** | **`spend`** | **`impressions`** | **`clicks`** |
|--- |--- |--- |--- |--- |--- |--- |
| **1** | [!DNL Facebook] | 2017-05-01 00:00:00 | aaa | 5 | 1200 | 25 |
| **1** | [!DNL Google AdWords] | 2017-05-05 00:00:00 | eee | 10,2 | 2000 | 60 |
| **2** | [!DNL Facebook] | 2017-05-15 00:00:00 | jj | 2,5 | 800 | 12 |
| **2** | [!DNL Google AdWords] | 2017-05-23 00:00:00 | ggg | 4,6 | 900 | 40 |
| **3** | [!DNL Facebook] | 2017-05-22 00:00:00 | aaa | 7 | 2000 | 40 |
| **3** | [!DNL Google AdWords] | 2017-06-12 00:00:00 | aaa | 2,5 | 400 | 22 |
| **4** | [!DNL Facebook] | 2017-06-08 00:00:00 | aaa | 10 | 6000 | 110 |
| **4** | [!DNL Google AdWords] | 2017-06-30 00:00:00 | eee | 35 | 14500 | 350 |
| **5** | [!DNL Facebook] | 2017-07-06 00:00:00 | ccc | 1,2 | 300 | 5 |
| **5** | [!DNL Google AdWords] | 2017-07-10 00:00:00 | fff | 28,5 | 10200 | 280 |

Plutôt que de créer un ensemble distinct de mesures marketing pour chaque source publicitaire, vous pouvez créer un seul ensemble de mesures à l’aide du tableau ci-dessus pour capturer toutes vos publicités.

**Vous recherchez une aide supplémentaire ?**

L’écriture de SQL et la création de `Data Warehouse Views` ne sont pas incluses dans le support technique. Cependant, l’ [équipe des services](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) offre une assistance pour la création de vues. Pour tout savoir sur la migration d’une base de données héritée avec une nouvelle base de données afin de créer une vue de Data Warehouse unique aux fins d’une analyse spécifique, l’équipe d’assistance peut vous aider.

En règle générale, la création d’un nouveau `Data Warehouse View` dans le but de consolider 2 à 3 tables structurées de la même manière nécessite cinq heures de service, ce qui représente environ 1 250 $ de travail. Vous trouverez ci-dessous quelques facteurs courants susceptibles d’accroître l’investissement attendu nécessaire :

* Consolidation de plus de trois tables en une seule vue
* Création de plusieurs vues de Data Warehouse
* Logique de jointure complexe ou conditions de filtrage
* Consolidation de deux tableaux ou plus avec des structures de données différentes
