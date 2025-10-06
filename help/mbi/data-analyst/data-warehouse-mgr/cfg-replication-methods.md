---
title: Configuration des méthodes de réplication
description: Découvrez comment les tables sont organisées et comment les données des tables se comportent. Vous pouvez ainsi choisir la meilleure méthode de réplication pour vos tables.
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1442'
ht-degree: 0%

---

# Configuration des méthodes de réplication

`Replication` méthodes et [revérifications](../data-warehouse-mgr/cfg-data-rechecks.md) sont utilisées pour identifier les données nouvelles ou mises à jour dans vos tables de base de données. Leur définition correcte est essentielle pour garantir la précision des données et des temps de mise à jour optimisés. Cette rubrique porte sur les méthodes de réplication.

Lorsque de nouvelles tables sont synchronisées dans [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md), une méthode de réplication est automatiquement choisie pour la table. En maîtrisant les différentes méthodes de réplication, l&#39;organisation des tables et le comportement des données des tables, vous pouvez choisir la meilleure méthode de réplication pour vos tables.

## Quelles sont les méthodes de réplication ?

`Replication` méthodes peuvent être classées en trois groupes : `Incremental`, `Full Table` et `Paused`.

[**[!UICONTROL Incremental Replication]**](#incremental) signifie que [!DNL Commerce Intelligence] ne réplique que les données nouvelles ou mises à jour à chaque tentative de réplication. Comme ces méthodes réduisent considérablement la latence, Adobe recommande de l’utiliser autant que possible.

[**[!UICONTROL Full Table Replication]**](#fulltable) signifie que [!DNL Commerce Intelligence] réplique l’intégralité du contenu d’une table à chaque tentative de réplication. En raison de la quantité potentiellement importante de données à répliquer, ces méthodes peuvent augmenter les temps de latence et de mise à jour. Si une table contient des colonnes horodatées ou datetime, Adobe recommande d’utiliser plutôt une méthode incrémentale .

**[!UICONTROL Paused]** indique que la réplication de la table est arrêtée ou mise en pause. [!DNL Commerce Intelligence] ne vérifie pas les données nouvelles ou mises à jour au cours d&#39;un cycle de mise à jour ; cela signifie qu&#39;aucune donnée n&#39;est répliquée à partir d&#39;une table dont c&#39;est la méthode de réplication.

## Méthodes de réplication incrémentielle {#incremental}

### Modifié à (idéal)

La méthode de réplication `Modified At` utilise une colonne datetime, qui est renseignée lorsqu’une ligne est créée, puis mise à jour lorsque les données changent, pour rechercher les données à répliquer. Cette méthode est conçue pour fonctionner avec des tableaux qui répondent aux critères suivants :

* contient une colonne `datetime` qui est initialement renseignée lors de la création d’une ligne et qui est mise à jour chaque fois que la ligne est modifiée ;
* la colonne `datetime` n’est jamais nulle ;
* les lignes ne sont pas supprimées du tableau

Outre ces critères, Adobe recommande d’**indexer** la colonne `datetime` utilisée pour la réplication `Modified At`, car cela permet d’optimiser la vitesse de réplication.

Lors de l’exécution de la mise à jour, les données nouvelles ou modifiées sont identifiées en recherchant les lignes qui contiennent une valeur dans la colonne `datetime` qui se sont produites après la mise à jour la plus récente. Lorsque de nouvelles lignes sont découvertes, elles sont répliquées vers votre Data Warehouse. Si des lignes existent dans le [Gestionnaire Data Warehouse](../data-warehouse-mgr/tour-dwm.md), elles sont remplacées par les valeurs actuelles de la base de données.

Par exemple, un tableau peut avoir une colonne appelée `modified\_at` qui indique la dernière fois que les données ont été modifiées. Si la mise à jour la plus récente s’exécutait mardi à midi, elle recherche toutes les lignes ayant une valeur `modified\_at` supérieure à mardi à midi. Toutes les lignes découvertes qui ont été créées ou modifiées depuis mardi midi sont répliquées vers le Data Warehouse.

**Le saviez-vous ?**
Même si votre base de données ne peut actuellement pas prendre en charge une méthode de réplication `Incremental`, vous pouvez [apporter des modifications à votre base de données](../../best-practices/mod-db-inc-replication.md) ce qui permettrait d’utiliser `Modified At` ou `Single Auto Incrementing PK`.

`Modified At` n’est pas seulement la méthode de réplication la plus idéale, c’est aussi la plus rapide. Cette méthode permet non seulement d’augmenter considérablement la vitesse des jeux de données volumineux, mais elle ne nécessite pas non plus de configuration d’une option de revérification. D’autres méthodes doivent effectuer une itération sur une table entière pour identifier les modifications, même si un petit sous-ensemble de données a été modifié. `Modified At` effectue une itération uniquement sur ce petit sous-ensemble.

### Clé de Principal à incrémentation automatique unique

`Auto Incrementing` est un comportement qui attribue de manière séquentielle des clés primaires aux lignes. Si une table est `Auto Incrementing` et que la clé primaire la plus élevée est 1 000, la valeur primaire suivante est 1 001 ou supérieure. Un tableau qui n&#39;utilise pas `Auto Incrementing` comportement peut attribuer une valeur de clé primaire inférieure à 1 000 ou passer à un nombre beaucoup plus élevé, mais cela n&#39;est pas couramment utilisé.

Cette méthode est conçue pour répliquer de nouvelles données à partir de tables qui répondent aux critères suivants :

* `single-column primary key` ; et
* `primary key` type de données est `integer` ; et
* `auto incrementing` les valeurs de clé primaire.

Lorsqu’une table utilise la réplication `Single Auto Incrementing Primary Key`, les nouvelles données sont découvertes en recherchant des valeurs de clé primaire qui sont supérieures à la valeur la plus élevée actuelle dans votre Data Warehouse. Par exemple, si la valeur de clé primaire la plus élevée de votre Data Warehouse est 500, lors de la prochaine mise à jour, elle recherchera les lignes avec des valeurs de clé primaire supérieures ou égales à 501.

### Ajouter une date

Le fonctionnement de la méthode `Add Date` est similaire à celui de la méthode `Single Auto Incrementing Primary Key`. Au lieu d&#39;utiliser un entier pour la clé primaire de la table, cette méthode utilise une colonne `timestamped` pour rechercher de nouvelles lignes.

Lorsqu’une table utilise la réplication `Add Date`, les nouvelles données sont découvertes en recherchant les valeurs horodatées supérieures à la dernière date synchronisée dans votre Data Warehouse. Par exemple, si une mise à jour a été exécutée pour la dernière fois le 20/12/2015 à 09:00:00, toutes les lignes dont la date et l’heure sont supérieures à cette date seront marquées comme nouvelles données et répliquées.

>[!NOTE]
>
>Contrairement à la méthode `Modified At`, `Add Date` ne vérifie pas les lignes existantes pour obtenir les informations mises à jour. Seules de nouvelles lignes sont recherchées.

## Méthodes de réplication de table complètes {#fulltable}

### Tableau complet

`Full table` réplication actualise la table entière chaque fois que de nouvelles lignes sont détectées. Il s’agit de loin de la méthode de réplication la moins efficace, car toutes les données doivent être retraitées à chaque mise à jour, en supposant qu’il existe de nouvelles lignes.

De nouvelles lignes sont détectées en interrogeant votre base de données au début du processus de synchronisation et en comptant le nombre de lignes. Si votre base de données locale contient plus de lignes que [!DNL Commerce Intelligence], le tableau est actualisé. Si le nombre de lignes est identique ou si [!DNL Commerce Intelligence] contient *plus* de lignes que votre base de données locale, le tableau est ignoré.

Cela soulève un point important, à savoir que **`Full Table`réplication est incompatible lorsque :**

* plus de lignes sont supprimées que créées dans votre table de base de données locale entre les cycles de mise à jour suivants, ou
* les valeurs de colonne sont modifiées, mais aucune ligne supplémentaire n’est créée

Dans l’un ou l’autre des scénarios ci-dessus, `Full Table` réplication ne détecte aucune modification et vos données deviennent obsolètes. En raison de l’inefficacité de cette méthode de réplication et des exigences mentionnées ci-dessus, `Full Table` réplication n’est recommandée qu’en dernier recours.

### Lot de clés de Principal

Lorsqu&#39;une table utilise `Primary Key Batch` (PK Batch), les nouvelles données sont découvertes en comptant les lignes à l&#39;intérieur des plages, ou lots, de valeurs de clé primaire. Bien que vous pensiez généralement que cette fonction soit utilisée avec des entiers, même les valeurs de texte peuvent être organisées de manière à permettre au système de définir des plages constantes.

Supposons, par exemple, qu’une mise à jour s’exécute et effectue un comptage de lignes pour la plage de clés comprise entre 1 et 100. Dans cette mise à jour, le système trouve et consigne 37 lignes. Lors de la prochaine mise à jour, un comptage des lignes est à nouveau effectué sur la plage 1-100 et trouve 41 lignes. Comme le nombre de lignes diffère de celui de la dernière mise à jour, le système examine cette plage (ou ce lot) plus en détail.

Cette méthode est destinée à répliquer les données des tables qui répondent aux critères suivants :

* non entier à une seule colonne ; ou
* clés composites (plusieurs colonnes comprenant la clé primaire) : notez que les colonnes utilisées dans une clé primaire composite ne peuvent jamais avoir de valeurs nulles ; ou
* valeurs de clé primaire à colonne unique, entières, sans incrémentation automatique.

Cette méthode n’est pas idéale, car elle est incroyablement lente en raison de la quantité de traitement qui doit se produire pour examiner les lots et trouver des modifications. Adobe recommande de ne pas utiliser cette méthode, sauf s’il est impossible d’apporter les modifications nécessaires à la prise en charge des autres méthodes de réplication. Les temps de mise à jour sont susceptibles d’augmenter si cette méthode doit être utilisée.

## Définition des méthodes de réplication

Les méthodes de réplication sont définies table par table. Pour définir une méthode de réplication pour une table, vous avez besoin d&#39;autorisations [`Admin`](../../administrator/user-management/user-management.md) pour pouvoir accéder au gestionnaire Data Warehouse.

1. Une fois dans le gestionnaire Data Warehouse, sélectionnez la table dans la liste `Synced Tables` pour afficher son schéma.
1. La méthode de réplication actuelle est répertoriée sous le nom de la table. Pour le modifier, cliquez sur le lien.
1. Dans le pop-up qui s’affiche, cliquez sur le bouton radio en regard de `Incremental` ou `Full Table` réplication pour sélectionner un type de réplication.
1. Cliquez ensuite sur la liste déroulante **[!UICONTROL Replication Method]** pour sélectionner une méthode. Par exemple, `Paused` ou `Modified At`.

   >[!NOTE]
   >
   >**Certaines méthodes incrémentielles nécessitent de définir un`Replication Key`**. [!DNL Commerce Intelligence] utilisera cette clé pour déterminer où le prochain cycle de mise à jour doit commencer.
   >
   >Par exemple, si vous souhaitez utiliser la méthode `modified at` pour votre table `orders`, vous devez définir un `date column` comme clé de réplication. Il peut exister plusieurs options pour les clés de réplication, mais vous sélectionnez `created at` ou l’heure à laquelle la commande a été créée. Si le dernier cycle de mise à jour s’arrêtait le 12/1/2015 à 00:10:00, le cycle suivant commencerait à répliquer les données avec une date de `created at` supérieure à celle-ci.

1. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save]**.

Examinons l’ensemble du processus :

![Démonstration animée de la configuration des méthodes de réplication pour les tables de la base de données](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## Conclusion

Pour terminer, vous avez rassemblé ce tableau qui compare les différentes méthodes de réplication. Cela s’avère incroyablement pratique lors de la sélection d’une méthode pour les tableaux de votre Data Warehouse.

| **`Method`** | **`Syncing New Data`** | **`Processing Rechecks on Large Data Sets`** | **`Handle Composite Keys?`** | **`Handle Non-Integer PKs?`** | **`Handle Non-Sequential PK Population?`** | **`Handle Row Deletion?`** |
|-----|-----|-----|-----|-----|-----|-----|
| `Auto-Incrementing Primary Key` | Plus rapide | Lent | Non | Non | Non | Oui |
| `Primary Key Batch Monitoring` | Lent | Lent | Oui | Oui | Oui | Oui |
| `Modified At` | Plus rapide | Plus rapide | Oui | Oui | Oui | Non |

{style="table-layout:auto"}

## Documentation connexe

* [Comprendre les revérifications de données](../data-warehouse-mgr/cfg-data-rechecks.md)
* [Modification de la base de données pour la prise en charge de &#x200B;](../../best-practices/mod-db-inc-replication.md)
* [Optimisation de votre base de données pour l’analyse](../../best-practices/opt-db-analysis.md)
* [Réduction Du Temps De Mise À Jour](../../best-practices/reduce-update-cycle-time.md)
