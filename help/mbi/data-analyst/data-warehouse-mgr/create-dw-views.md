---
title: Création et utilisation de vues Data Warehouse
description: Découvrez une méthode permettant de créer de nouvelles tables d'entrepôt de données en modifiant une table existante ou en joignant ou en consolidant plusieurs tables ensemble à l'aide de SQL.
exl-id: 5aa571c9-7f38-462c-8f1b-76a826c9dc55
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1120'
ht-degree: 6%

---

# Utilisation des vues Data Warehouse

Ce document décrit l’objectif et les utilisations des `Data Warehouse Views` accessibles en accédant à **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**. Vous trouverez ci-dessous une explication de son fonctionnement et de la manière de créer des vues, ainsi qu’un exemple de la manière d’utiliser `Data Warehouse Views` pour consolider les données de [!DNL Facebook] et de dépenses [!DNL AdWords].

## Usage général

La fonction `Data Warehouse Views` permet de créer de nouvelles tables d&#39;entrepôt de données en modifiant une table existante ou en joignant ou en consolidant plusieurs tables ensemble à l&#39;aide de SQL. Une fois qu’un `Data Warehouse View` a été créé et traité par un cycle de mise à jour, il est renseigné dans votre Data Warehouse sous la forme d’un nouveau tableau sous la liste déroulante `Data Warehouse Views` , comme illustré ci-dessous :

Interface de Data Warehouse ![affichant les options de gestion de table](../../assets/Data_Warehouse.png)

À partir de là, votre nouvelle vue fonctionne comme toute autre table, vous permettant de créer des colonnes calculées ou de créer des mesures et des rapports sur celle-ci.

Les `Data Warehouse Views` sont principalement utilisés pour consolider plusieurs tableaux similaires mais disparates, de sorte que tous les rapports puissent être créés sur un seul nouveau tableau. Parmi les exemples courants, citons la consolidation des tables d’une base de données héritée et d’une base de données active pour combiner les données historiques et actuelles, ou la combinaison de plusieurs sources publicitaires telles que Facebook et AdWords en une seule table `Consolidated ad spend`.

Si vous connaissez SQL, ces deux exemples de consolidation utilisent la fonction `UNION`, mais vous pouvez utiliser n’importe quelle syntaxe et fonction PostgreSQL lors de la création d’une vue.

## Création et gestion des vues Data Warehouse

Vous pouvez créer de nouvelles `Data Warehouse Views` et supprimer des vues existantes en accédant à **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**, comme illustré ci-dessous :

Section ![Vues Data Warehouse affichant les configurations d’affichage personnalisées](../../assets/Data_Warehouse_Views.png)

À partir de là, vous pouvez créer une vue en suivant les exemples d’instructions ci-dessous :

1. Si vous observez une vue existante, cliquez sur **[!UICONTROL New Data Warehouse View]** pour ouvrir une fenêtre de requête vide. Si une fenêtre de requête vierge est déjà ouverte, passez à l’étape suivante.
1. Attribuez un nom à la vue en saisissant dans le champ `View Name`. Le nom fourni ici détermine le nom d’affichage de la vue dans le Data Warehouse. Les `View names` sont limités aux lettres minuscules, aux chiffres et aux traits de soulignement (_). Tout autre caractère est interdit.
1. Saisissez votre requête dans la fenêtre intitulée `Select Query`, en utilisant la syntaxe PostgreSQL standard.

   >[!NOTE]
   >
   >Votre requête doit référencer des noms de colonne spécifiques. L’utilisation du caractère `*` pour sélectionner toutes les colonnes n’est pas autorisée.

1. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save]** pour enregistrer votre vue. Votre vue a temporairement un statut `Pending` jusqu’à ce qu’elle soit traitée par le prochain cycle de mise à jour complet, auquel cas le statut passe à `Active`. Après avoir été traitée par une mise à jour, votre vue est prête à être utilisée dans les rapports.

Il est important de mentionner qu’après l’enregistrement, la requête sous-jacente utilisée pour générer un `Data Warehouse View` ne peut pas être modifiée. Si vous devez ajuster la structure d&#39;une `Data Warehouse View`, vous devez créer une vue et migrer manuellement les colonnes calculées, les mesures ou les rapports de la vue d&#39;origine vers la nouvelle. Une fois la migration terminée, vous pouvez supprimer en toute sécurité la vue d’origine. Étant donné que les `Data Warehouse Views` ne sont pas modifiables, Adobe vous recommande de tester la sortie de votre requête à l’aide du `SQL Report Builder` avant d’enregistrer votre requête en tant que vue Data Warehouse.

## Exemple : [!DNL Facebook] et [!DNL Google AdWords] des données

Regardez de plus près l’un des exemples mentionnés précédemment dans cet article : consolidation des données de [!DNL Facebook] et de dépenses [!DNL AdWords] dans un nouveau tableau publicitaire consolidé. Le plus souvent, cela implique la consolidation de deux tableaux, avec les exemples de jeux de données ci-dessous :

`Ad source: Google AdWords`

`Table name: campaigns67890`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | voir | 60 | 2017-05-05 00:00:00 | 2000 | 10,2 |
| 2 | gg | 40 | 23 00:00:00 2017-05 | 900 | 4,6 |
| 3 | aaa | 22 | 2017-06-12 00:00:00 | 400 | 2,5 |
| 4 | voir | 350 | 30 00:00:00 2017-06 | 14500 | 35 |
| 5 | fff | 280 | 2017-07-10 :00: | 10200 | 28,5 |

`Ad source: Facebook`

`Table name: facebook_ads_insights_12345`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | aaa | 25 | 2017-05-01 00:00:00 | 1200 | 5 |
| 2 | ddd | 12 | 2017-05-15 00:00:00 | 800 | 2,5 |
| 3 | aaa | 40 | 22/05/2017 00:00:00 | 2000 | 7 |
| 4 | aaa | 110 | 2017-06-08 00:00:00 | 6000 | 10 |
| 5 | ccc | 5 | 2017-07-06 00:00:00 | 300 | 1,2 |

Pour créer une seule table de dépenses publicitaires contenant à la fois les campagnes [!DNL Facebook] et [!DNL Google AdWords], vous devez écrire une requête SQL et utiliser la fonction `UNION ALL` . Une instruction `UNION ALL` est le plus souvent utilisée pour combiner plusieurs requêtes SQL distinctes tout en ajoutant les résultats de chaque requête à une seule sortie.

Il existe quelques exigences d’une instruction `UNION` qui méritent d’être mentionnées, comme indiqué dans la [documentation](https://www.postgresql.org/docs/8.3/queries-union.html) PostgreSQL :

* Toutes les requêtes doivent renvoyer le même nombre de colonnes
* Les colonnes correspondantes doivent avoir des types de données identiques

Lors de l’exécution d’une instruction `UNION` ou `UNION ALL`, les noms des colonnes de la sortie finale reflètent les noms des colonnes de votre première requête.

En règle générale, la consolidation de vos [!DNL Facebook] et [!DNL Google AdWords] données de dépenses dans un `Data Warehouse View` nécessite la création d’un tableau à sept colonnes, avec une requête similaire à la suivante :

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

Quelques points importants à propos de ce qui précède :

* Pour des raisons de clarté, toutes les colonnes sont dotées d’un alias ci-dessus afin que les noms correspondent à toutes les requêtes. Toutefois, ce n&#39;est pas une exigence. L’ordre dans lequel les colonnes sont appelées dans les requêtes SELECT détermine leur alignement.
* Une nouvelle colonne appelée `ad_source` est créée pour faciliter le filtrage des données [!DNL AdWords] ou [!DNL Facebook]. N’oubliez pas que cette requête combine toutes les données des deux tables. Si vous ne créez pas de colonne comme `ad_source`, il n’existe aucun moyen facile d’identifier les dépenses à partir d’une source particulière.

L’enregistrement de la requête ci-dessus en tant que `Data Warehouse View` crée une table avec les dépenses de [!DNL Facebook] et de [!DNL AdWords], comme illustré ci-dessous :

| **`id`** | **`ad_source`** | **`date`** | **`campaign`** | **`spend`** | **`impressions`** | **`clicks`** |
|--- |--- |--- |--- |--- |--- |--- |
| **1** | [!DNL Facebook] | 2017-05-01 00:00:00 | aaa | 5 | 1200 | 25 |
| **1** | [!DNL Google AdWords] | 2017-05-05 00:00:00 | voir | 10,2 | 2000 | 60 |
| **2** | [!DNL Facebook] | 2017-05-15 00:00:00 | ddd | 2,5 | 800 | 12 |
| **2** | [!DNL Google AdWords] | 23 00:00:00 2017-05 | gg | 4,6 | 900 | 40 |
| **3** | [!DNL Facebook] | 22/05/2017 00:00:00 | aaa | 7 | 2000 | 40 |
| **3** | [!DNL Google AdWords] | 2017-06-12 00:00:00 | aaa | 2,5 | 400 | 22 |
| **4** | [!DNL Facebook] | 2017-06-08 00:00:00 | aaa | 10 | 6000 | 110 |
| **4** | [!DNL Google AdWords] | 30 00:00:00 2017-06 | voir | 35 | 14500 | 350 |
| **5** | [!DNL Facebook] | 2017-07-06 00:00:00 | ccc | 1,2 | 300 | 5 |
| **5** | [!DNL Google AdWords] | 2017-07-10 :00: | fff | 28,5 | 10200 | 280 |

Au lieu de créer un ensemble distinct de mesures marketing pour chaque source publicitaire, vous pouvez créer un seul ensemble de mesures à l’aide du tableau ci-dessus pour capturer toutes vos publicités.

**Vous recherchez de l’aide supplémentaire ?**

L’écriture de code SQL et la création de `Data Warehouse Views` ne sont pas incluses avec le support technique. Cependant, l’[équipe Services](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) offre une assistance pour la création de vues. Pour tout, de la migration d’une base de données héritée vers une nouvelle base de données à la création d’une vue Data Warehouse unique à des fins d’analyse spécifique, l’équipe d’assistance peut vous aider.

Habituellement, la création d&#39;un nouveau `Data Warehouse View` dans le but de consolider 2-3 tableaux structurés de manière similaire nécessite cinq heures de service, ce qui se traduit par environ 1 250 $ de travail. Voici toutefois quelques facteurs communs qui peuvent accroître les investissements attendus :

* Consolidation de plus de trois tables en une seule vue
* Création de plusieurs vues Data Warehouse
* Logique de jointure complexe ou conditions de filtrage
* Consolidation de deux tables ou plus avec des structures de données différentes
