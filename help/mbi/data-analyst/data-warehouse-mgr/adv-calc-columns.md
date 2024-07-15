---
title: Types de colonne calculés avancés
description: Découvrez les principes de base de la plupart des cas d’utilisation des colonnes, mais vous souhaiterez peut-être que les colonnes calculées soient un peu plus complexes que ce que le Gestionnaire de Data Warehouse peut créer.
exl-id: 9871fa19-95b3-46e4-ae2d-bd7c524d12db
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 2%

---

# Types de colonne calculés avancés

De nombreuses analyses que vous souhaitez peut-être créer impliquent l’utilisation d’une **nouvelle colonne** que vous souhaitez `group by` ou `filter by`. Le tutoriel [Création de colonnes calculées](../data-warehouse-mgr/creating-calculated-columns.md) aborde les bases de la plupart des cas d’utilisation, mais vous pouvez souhaiter que la colonne calculée soit un peu plus complexe que ce que le Gestionnaire de Data Warehouse peut créer.
{ : #top}

Ces types de colonnes peuvent être créés par l’équipe Adobe des analystes de Data Warehouse. Pour définir une nouvelle colonne calculée, renseignez les informations suivantes :

1. **`definition`** de cette colonne (y compris les entrées, les formules ou la mise en forme)
1. **`table`** sur lequel vous souhaitez créer la colonne
1. Tout **`example data points`** qui décrit ce que la colonne doit contenir

Voici quelques exemples courants de colonnes calculées avancées que les utilisateurs trouvent souvent utiles :

* [Ordre séquentiel (ou classement) de l’événement](#compareevents)
* [Rechercher l’intervalle entre deux événements](#twoevents)
* [Comparaison des valeurs d’événement séquentiel](#sequence)
* [Convertir une devise](#currency)
* [Conversion des fuseaux horaires](#timezone)
* [Quelque chose d’autre](#else)

## J’essaie de classer les événements de manière séquentielle. {#compareevents}

Il s’agit d’une colonne calculée **numéro d’événement**. Cela signifie que vous essayez de trouver la séquence dans laquelle les événements se sont produits pour un propriétaire d’événement particulier, comme un client ou un utilisateur.

Voici un exemple :

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Owner's event number`** |
|-----|-----|-----|-----|
| 1 | `A` | 2015-01-01 00:00:00 | 1 |
| 2 | `B` | 2015-01-01 00:30:00 | 1 |
| 3 | `A` | 2015-01-01 02:00:00 | 2 |
| 4 | `A` | 2015-01-02 13:00:00 | 3 |
| 5 | `B` | 2015-01-03 13:00:00 | 2 |

{style="table-layout:auto"}

Une colonne calculée de numéro d’événement peut être utilisée pour observer les différences de comportement entre les premiers événements, les événements de répétition ou les énièmes événements de vos données.

Vous souhaitez que la colonne Numéro de commande du client soit en action ? Cliquez sur l’image pour l’afficher comme dimension Groupe par dans un rapport.

![Utilisation d&#39;une colonne calculée de numéro d&#39;événement à Group By le numéro de commande du client.](../../assets/EventNumber.gif)<!--{: style="max-width: 500px;"}-->

Pour créer ce type de colonne calculée, vous devez savoir :

* Le tableau sur lequel vous souhaitez créer cette colonne
* Le champ qui identifie le propriétaire des événements (`owner\_id` dans cet exemple)
* Le champ par lequel vous souhaitez classer les événements (`timestamp` dans cet exemple)

[Haut de page](#top)

## J&#39;essaie de trouver le temps entre deux événements. {#twoevents}

Il s’agit d’une colonne calculée `date difference`. Cela signifie que vous essayez de trouver l’heure entre deux événements appartenant à un seul enregistrement, en fonction des horodatages de l’événement.

Voici un exemple :

| `id` | `timestamp\_1` | `timestamp\_2` | `Seconds between timestamp\_2 and timestamp\_1` |
|-----|-----|-----|-----|
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style="table-layout:auto"}

Une colonne calculée de différence de date peut être utilisée pour créer une mesure qui calcule la durée moyenne ou médiane entre deux événements. Cliquez sur l’image ci-dessous pour découvrir comment la mesure `Average time to first order` est utilisée dans un rapport.

![ Utilisation d&#39;une colonne calculée de différence de date pour calculer le temps moyen jusqu&#39;au premier ordre.](../../assets/DateDifference.gif)<!--{: style="max-width: 500px;"}-->

Pour créer ce type de colonne calculée, vous devez savoir :

* Le tableau sur lequel vous souhaitez créer cette colonne
* Les deux horodatages entre lesquels vous souhaitez connaître la différence

[Haut de page](#top)

## J’essaie de comparer les valeurs d’événement séquentiel. {#sequence}

On parle alors de **comparaison d’événements séquentiels**. Cela signifie que vous essayez de trouver le delta entre une valeur (devise, nombre, horodatage) et la valeur correspondante pour l’événement précédent du propriétaire.

Voici un exemple :

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|-----|-----|-----|-----|
| 1 | `A` | 2015-01-01 00:00:00 | NULL |
| 2 | `B` | 2015-01-01 00:30:00 | NULL |
| 3 | `A` | 2015-01-01 02:00:00 | 7720 |
| 4 | `A` | 2015-01-02 13:00:00 | 126000 |
| 5 | `B` | 2015-01-03 13:00:00 | 217800 |

{style="table-layout:auto"}

Une comparaison d’événements séquentiels peut être utilisée pour trouver la durée moyenne ou médiane entre chaque événement séquentiel. Cliquez sur l’image ci-dessous pour afficher les mesures **Durée moyenne et moyenne entre les commandes** en action.

=![Utilisation d’une colonne calculée de comparaison d’événements séquentiels pour calculer la durée moyenne et moyenne entre les commandes.](../../assets/SeqEventComp.gif)<!--{: style="max-width: 500px;"}-->

Pour créer ce type de colonne calculée, vous devez savoir :

* Le tableau sur lequel vous souhaitez créer cette colonne
* Le champ qui identifie le propriétaire des événements (`owner\_id` dans l’exemple)
* Le champ de valeur dont vous souhaitez voir la différence entre pour chaque événement séquentiel (`timestamp` dans cet exemple)

[Haut de page](#top)

## J&#39;essaie de convertir des devises. {#currency}

Une colonne calculée de **conversion de devise** convertit les montants d’une transaction d’une devise enregistrée en devise de création de rapports, en fonction du taux d’exchange au moment de l’événement.

Voici un exemple :

| **`id`** | **`timestamp`** | **`transaction\_value\_EUR`** | **`transaction\_value\_USD`** |
|-----|-----|-----|-----|
| `1` | 2015-01-01 00:00:00 | 30 | 33,57 |
| `2` | 2015-01-02 00:00:00 | 50 | 55,93 |

{style="table-layout:auto"}

Pour créer ce type de colonne calculée, vous devez savoir :

* Le tableau sur lequel vous souhaitez créer cette colonne
* Colonne du montant de la transaction que vous souhaitez convertir
* La colonne qui indique la devise dans laquelle les données ont été enregistrées (généralement un code ISO)
* Devise de création de rapports préférée

[Haut de page](#top)

## J’essaie de convertir les fuseaux horaires. {#timezone}

Une colonne calculée **conversion de fuseau horaire** convertit les horodatages d’une source de données spécifique de leur fuseau horaire enregistré en fuseau horaire de création de rapports.

Voici un exemple :

| **`id`** | **`timestamp\_UTC`** | **`timestamp\_ET`** |
|-----|-----|-----|
| `1` | 2015-01-01 00:00:00 | 2014-12-31 19:00:00 |
| `2` | 2015-01-01 12:00:00 | 2015-01-01 07:00:00 |

{style="table-layout:auto"}

Pour créer ce type de colonne calculée, vous devez savoir :

* Le tableau sur lequel vous souhaitez créer cette colonne
* La colonne d’horodatage que vous souhaitez convertir
* Le fuseau horaire dans lequel les données ont été enregistrées
* Fuseau horaire de création de rapports préféré

[Haut de page](#top)

## J&#39;essaie de faire quelque chose qui n&#39;est pas listé ici. {#else}

Pas de quoi s&#39;inquiéter. Ce n&#39;est pas parce qu&#39;il n&#39;est pas répertorié ici que ce n&#39;est pas possible. L’équipe Adobe d’analystes Data Warehouse peut vous aider.

Pour définir une nouvelle colonne calculée, [envoyez un ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) avec des détails précis sur ce que vous souhaitez créer.

## Documentation connexe

* [Créer des colonnes calculées](../data-warehouse-mgr/creating-calculated-columns.md)
* [Types de colonnes calculés](../data-warehouse-mgr/calc-column-types.md)
* [Construire des dimensions avec des données de commande et de client [!DNL Google ECommerce] ](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
