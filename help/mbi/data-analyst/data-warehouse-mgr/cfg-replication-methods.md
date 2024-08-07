---
title: Configuration des méthodes de réplication
description: Découvrez comment les tables sont organisées et comment les données du tableau se comportent vous permet de choisir la meilleure méthode de réplication pour vos tables.
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Data Import/Export
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 0%

---

# Configuration des méthodes de réplication

Les méthodes `Replication` et [rechecks](../data-warehouse-mgr/cfg-data-rechecks.md) sont utilisés pour identifier les données nouvelles ou mises à jour dans les tables de base de données. Les définir correctement est essentiel pour garantir à la fois la précision des données et des temps de mise à jour optimisés. Cette rubrique porte sur les méthodes de réplication.

Lorsque de nouvelles tables sont synchronisées dans le [Gestionnaire de Data Warehouse](../data-warehouse-mgr/tour-dwm.md), une méthode de réplication est automatiquement sélectionnée pour la table. La présentation des différentes méthodes de réplication, de l’organisation des tables et du comportement des données tabulaires vous permet de choisir la meilleure méthode de réplication pour vos tables.

## Quelles sont les méthodes de réplication ?

Les méthodes `Replication` se divisent en trois groupes : `Incremental`, `Full Table` et `Paused`.

[**[!UICONTROL Incremental Replication]**](#incremental) signifie que [!DNL Commerce Intelligence] réplique uniquement les données nouvelles ou mises à jour à chaque tentative de réplication. Comme ces méthodes réduisent considérablement la latence, Adobe recommande de l’utiliser si possible.

[**[!UICONTROL Full Table Replication]**](#fulltable) signifie que [!DNL Commerce Intelligence] réplique l’intégralité du contenu d’un tableau à chaque tentative de réplication. En raison de la quantité potentiellement importante de données à répliquer, ces méthodes peuvent augmenter la latence et les temps de mise à jour. Si un tableau contient des colonnes horodatées ou datetime, Adobe recommande d’utiliser plutôt une méthode incrémentielle .

**[!UICONTROL Paused]** indique que la réplication de la table est arrêtée ou suspendue. [!DNL Commerce Intelligence] ne recherche pas de données nouvelles ou mises à jour au cours d’un cycle de mise à jour ; cela signifie qu’aucune donnée n’est répliquée à partir d’une table qui possède cette méthode de réplication.

## Méthodes de réplication incrémentielle {#incremental}

### Modifié à (idéal)

La méthode de réplication `Modified At` utilise une colonne datetime (qui est renseignée lorsqu’une ligne est créée, puis mise à jour lorsque les données changent) pour trouver les données à répliquer. Cette méthode est conçue pour fonctionner avec des tables répondant aux critères suivants :

* contient une colonne `datetime` initialement renseignée lors de la création d’une ligne et mise à jour dès que la ligne est modifiée ;
* la colonne `datetime` n’est jamais nulle ;
* les lignes ne sont pas supprimées du tableau

En plus de ces critères, Adobe recommande **indexing** de la colonne `datetime` utilisée pour la réplication `Modified At`, car cela permet d’optimiser la vitesse de réplication.

Lorsque la mise à jour s’exécute, les données nouvelles ou modifiées sont identifiées en recherchant les lignes ayant une valeur dans la colonne `datetime` qui se sont produites après la mise à jour la plus récente. Lorsque de nouvelles lignes sont découvertes, elles sont répliquées vers votre Data Warehouse. S’il existe des lignes dans le [Gestionnaire de Data Warehouse](../data-warehouse-mgr/tour-dwm.md), elles sont remplacées par les valeurs de base de données actuelles.

Par exemple, une table peut avoir une colonne appelée `modified\_at` qui indique la dernière modification des données. Si la mise à jour la plus récente s’est déroulée le mardi à midi, la mise à jour recherche toutes les lignes ayant une valeur `modified\_at` supérieure à mardi à midi. Toutes les lignes découvertes qui ont été créées ou modifiées depuis midi le mardi sont répliquées vers le Data Warehouse.

**Saviez-vous ?**
Même si votre base de données ne prend actuellement pas en charge une méthode de réplication `Incremental`, vous pouvez [ apporter des modifications à votre base de données ](../../best-practices/mod-db-inc-replication.md) qui permettraient l’utilisation de `Modified At` ou `Single Auto Incrementing PK`.

`Modified At` est non seulement la méthode de réplication la plus idéale, mais elle est également la plus rapide. Cette méthode produit non seulement des augmentations de vitesse perceptibles avec des jeux de données volumineux, mais elle ne nécessite pas non plus de configurer une option de nouveau contrôle. D’autres méthodes doivent itérer sur un tableau entier pour identifier les modifications, même si un petit sous-ensemble de données a changé. `Modified At` effectue une itération uniquement sur ce petit sous-ensemble.

### Incrémentation automatique unique par clé de Principal

`Auto Incrementing` est un comportement qui attribue de manière séquentielle des clés primaires aux lignes. Si une table est `Auto Incrementing` et que la clé primaire la plus élevée de la table est de 1 000, la valeur primaire suivante est de 1 001 ou plus. Un tableau qui n’utilise pas le comportement `Auto Incrementing` peut affecter une valeur de clé primaire inférieure à 1 000 ou passer à un nombre beaucoup plus grand, mais cette valeur n’est pas couramment utilisée.

Cette méthode est conçue pour répliquer de nouvelles données à partir de tableaux qui répondent aux critères suivants :

* `single-column primary key`; et
* `primary key` datatype est `integer`; et
* `auto incrementing` valeurs de clé primaire.

Lorsqu’une table utilise la réplication `Single Auto Incrementing Primary Key`, de nouvelles données sont découvertes en recherchant des valeurs de clé primaire supérieures à la valeur la plus élevée actuelle dans votre Data Warehouse. Par exemple, si la valeur de clé primaire la plus élevée dans votre Data Warehouse est 500, lors de la prochaine mise à jour, il recherche des lignes dont les valeurs de clé primaire sont supérieures ou égales à 501.

### Ajouter une date

La méthode `Add Date` fonctionne de la même manière que la méthode `Single Auto Incrementing Primary Key`. Au lieu d’utiliser un entier pour la clé primaire de la table, cette méthode utilise une colonne `timestamped` pour rechercher de nouvelles lignes.

Lorsqu’une table utilise la réplication `Add Date`, de nouvelles données sont découvertes en recherchant des valeurs horodatées supérieures à la dernière date synchronisée avec votre Data Warehouse. Par exemple, si une mise à jour s’est exécutée pour la dernière fois le 20/12/2015 09:00:00, toutes les lignes dont l’horodatage est supérieur à celui-ci seront marquées comme de nouvelles données et répliquées.

>[!NOTE]
>
>Contrairement à la méthode `Modified At`, `Add Date` ne vérifie pas les lignes existantes à la recherche d’informations mises à jour ; il se réjouit uniquement de nouvelles lignes.

## Méthodes de réplication de table complète {#fulltable}

### Tableau complet

La réplication `Full table` actualise la table entière chaque fois que de nouvelles lignes sont détectées. Il s’agit de loin de la méthode de réplication la moins efficace, car toutes les données doivent être retraitées à chaque mise à jour, en supposant qu’il y ait de nouvelles lignes.

De nouvelles lignes sont détectées en interrogeant votre base de données au début du processus de synchronisation et en comptabilisant le nombre de lignes. Si votre base de données locale contient plus de lignes que [!DNL Commerce Intelligence], le tableau est actualisé. Si le nombre de lignes est identique ou si [!DNL Commerce Intelligence] contient *plus* lignes par rapport à votre base de données locale, la table est ignorée.

Cela soulève le point important que la réplication **`Full Table`est incompatible lorsque :**

* plus de lignes sont supprimées que créées dans votre tableau de base de données local entre les cycles de mise à jour suivants, ou
* les valeurs de colonne sont modifiées, mais aucune ligne supplémentaire n’est créée.

Dans l’un des scénarios ci-dessus, la réplication `Full Table` ne détecte aucune modification et vos données deviennent obsolètes. En raison de l’inefficacité de cette méthode de réplication et des exigences mentionnées ci-dessus, la réplication `Full Table` n’est recommandée qu’en dernier recours.

### Lot de clé de Principal

Lorsqu’un tableau utilise `Primary Key Batch` (lot PK), de nouvelles données sont découvertes en comptant les lignes dans des plages de valeurs de clé primaire, ou lots. Bien que vous pensiez généralement que cela est utilisé avec des entiers, même les valeurs de texte peuvent être triées de manière à permettre au système de définir des plages constantes.

Supposons, par exemple, qu’une mise à jour s’exécute et effectue un comptage des lignes pour la plage de clés comprise entre 1 et 100. Dans cette mise à jour, le système détecte et consigne 37 lignes. Lors de la prochaine mise à jour, un nombre de lignes est à nouveau effectué sur la plage 1-100 et détecte 41 lignes. En raison d’une différence de nombre de lignes par rapport à la dernière mise à jour, le système examine cette plage (ou lot) plus en détail.

Cette méthode est destinée à répliquer les données des tableaux qui répondent aux critères suivants :

* une colonne non entière ; ou
* clé composite (plusieurs colonnes comprenant la clé primaire) : notez que les colonnes utilisées dans une clé primaire composite ne peuvent jamais avoir de valeurs nulles ; ou
* des valeurs de clé primaire à une seule colonne, entiers, sans incrémentation automatique.

Cette méthode n’est pas idéale, car elle est incroyablement lente en raison de la quantité de traitement qui doit se produire pour examiner les lots et rechercher les modifications. Adobe recommande de ne pas utiliser cette méthode à moins qu’il ne soit pas possible d’apporter les modifications nécessaires pour prendre en charge les autres méthodes de réplication. Attendez-vous à ce que les temps de mise à jour augmentent si cette méthode doit être utilisée.

## Définition des méthodes de réplication

Les méthodes de réplication sont définies table par table. Pour définir une méthode de réplication pour une table, vous avez besoin d’autorisations [`Admin`](../../administrator/user-management/user-management.md) afin d’accéder au Gestionnaire de Data Warehouse.

1. Une fois dans le Gestionnaire de Data Warehouse, sélectionnez la table dans la liste `Synced Tables` pour afficher le schéma de la table.
1. La méthode de réplication actuelle est répertoriée sous le nom de la table. Pour le modifier, cliquez sur le lien.
1. Dans la fenêtre contextuelle qui s’affiche, cliquez sur le bouton radio en regard de la réplication `Incremental` ou `Full Table` pour sélectionner un type de réplication.
1. Cliquez ensuite sur la liste déroulante **[!UICONTROL Replication Method]** pour sélectionner une méthode. Par exemple, `Paused` ou `Modified At`.

   >[!NOTE]
   >
   >**Certaines méthodes incrémentielles nécessitent que vous définissiez un`Replication Key`**. [!DNL Commerce Intelligence] utilisera cette clé pour déterminer où doit commencer le cycle de mise à jour suivant.
   >
   >Par exemple, si vous souhaitez utiliser la méthode `modified at` pour votre table `orders`, vous devez définir un `date column` comme clé de réplication. Plusieurs options pour les clés de réplication peuvent exister, mais vous sélectionnez `created at`, ou l’heure à laquelle la commande a été créée. Si le dernier cycle de mise à jour s’arrêtait à 12/1/2015 00:10:00, le cycle suivant commencerait à répliquer les données avec une date `created at` supérieure à celle-ci.

1. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save]**.

Examinez l’ensemble du processus :

![](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## Remplissage

Pour terminer, vous avez assemblé ce tableau qui compare les différentes méthodes de réplication. Cette méthode est particulièrement pratique lorsque vous sélectionnez une méthode pour les tableaux dans votre Data Warehouse.

| **`Method`** | **`Syncing New Data`** | **`Processing Rechecks on Large Data Sets`** | **`Handle Composite Keys?`** | **`Handle Non-Integer PKs?`** | **`Handle Non-Sequential PK Population?`** | **`Handle Row Deletion?`** |
|-----|-----|-----|-----|-----|-----|-----|
| `Auto-Incrementing Primary Key` | Plus rapide | Lent | Non | Non | Non | Oui |
| `Primary Key Batch Monitoring` | Lent | Lent | Oui | Oui | Oui | Oui |
| `Modified At` | Plus rapide | Plus rapide | Oui | Oui | Oui | Non |

{style="table-layout:auto"}

## Documentation connexe

* [Comprendre les contrôles des données](../data-warehouse-mgr/cfg-data-rechecks.md)
* [Modification de la base de données pour la prise en charge ](../../best-practices/mod-db-inc-replication.md)
* [Optimisation de la base de données pour l’analyse](../../best-practices/opt-db-analysis.md)
* [Réduction des temps de mise à jour](../../best-practices/reduce-update-cycle-time.md)
